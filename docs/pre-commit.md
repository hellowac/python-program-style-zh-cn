# pre-commit 维护代码风格

参考: [在Git项目中使用pre-commit统一管理hooks](https://juejin.cn/post/6982168137609248805#heading-0){target="_blank"}

## 介绍

Git 钩子脚本对于在提交代码审查之前识别简单问题很有用。我们{==**在每次提交时运行hooks(钩子)，以自动指出代码中的问题**==}，例如缺少分号、尾随空格和调试语句。通过在代码审查之前指出这些问题，代码审查者可以专注于更改的架构，而不会浪费时间在琐碎的样式挑剔上。

随着我们创建更多的库和项目，我们认识到跨项目共享我们的预提交挂钩是痛苦的。我们将笨拙的 bash 脚本从一个项目复制并粘贴到另一个项目，并且必须手动更改挂钩以适用于不同的项目结构。

我们相信您应该始终使用最好的行业标准 linters。一些最好的 linters 是用你没有在你的项目中使用或安装在你的机器上的语言编写的。例如 scss-lint 是用 Ruby 编写的 SCSS 的 linter。如果您在 node 中编写项目，您应该能够使用 scss-lint 作为预提交挂钩，而无需将 Gemfile 添加到您的项目或了解如何安装 scss-lint。

我们构建了预提交来解决我们的钩子问题。它是一个用于预提交挂钩的多语言包管理器。您指定所需的挂钩列表，并在每次提交之前预提交管理以任何语言编写的任何挂钩的安装和执行。预提交专门设计为不需要 root 访问权限。如果您的开发人员之一没有安装节点但修改了 JavaScript 文件，预提交会自动处理下载和构建节点以在没有 root 的情况下运行 eslint。

## 安装

在运行挂钩之前，您需要安装`pre-commit`包管理器。

使用pip:

```bash
pip install pre-commit
```

在一个python项目中，将下面的行添加到你的依赖文件`requirements.txt`（或`requirements-dev.txt`）中。

```bash
pre-commit
```

也可以像0依赖的[zipapp](https://docs.python.org/3/library/zipapp.html){target="_blank"}那样安装:

- 从[github发布历史](https://github.com/pre-commit/pre-commit/releases){target="_blank"}中找到并下载`.pyz`文件
- 在运行 `pre-commit ...` 的地方替换为 `python pre-commit-#.#.#.pyz ...`

使用 [homebrew](https://brew.sh/){target="_blank"} 安装:

```bash
brew install pre-commit
```

使用 [conda](https://conda.io/){target="_blank"}(又称 [conda-forge](https://conda-forge.org/){target="_blank"})安装:

```bash
conda install -c conda-forge pre-commit
```

### 快速开始

1. 安装 pre-commit

    - 按照上面的[安装](#_2)说明进行操作
    - `pre-commit --version` 应该显示出你使用的版本是多少

        ```bash
        $ pre-commit --version
        pre-commit 3.3.1
        ```

1. 添加一个 pre-commit 配置

    - 创建一个名称为`.pre-commit-config.yaml`的文件
    - 你可以使用`pre-commit sample-config`命令生成一个非常基础的配置文件
    - [下面](#插件)列出了配置的所有选项
    - 此示例使用 python 代码的格式化程序，但是`pre-commit`适用于任何编程语言
    - 其他[被支持的钩子](https://pre-commit.com/hooks.html){target="_blank"}同样是可用的

    ```yml
    repos:
    -   repo: https://github.com/pre-commit/pre-commit-hooks
        rev: v2.3.0
        hooks:
        -   id: check-yaml
        -   id: end-of-file-fixer
        -   id: trailing-whitespace
    -   repo: https://github.com/psf/black
        rev: 22.10.0
        hooks:
        -   id: black
    ```

1. 安装 git hook 脚本
    - 运行 `pre-commit install` 来设置git hook脚本

    ```bash
    $ pre-commit install
    pre-commit installed at .git/hooks/pre-commit
    ```

1. (可选)针对所有文件运行

    - 添加新hook(钩子)时，对所有文件运行hook(钩子)通常是个好主意（通常`pre-commit`只会在 git hook 存在的期间对更改的文件运行）

    ```bash
    $ pre-commit run --all-files
    [INFO] Initializing environment for https://github.com/pre-commit/pre-commit-hooks.
    [INFO] Initializing environment for https://github.com/psf/black.
    [INFO] Installing environment for https://github.com/pre-commit/pre-commit-hooks.
    [INFO] Once installed this environment will be reused.
    [INFO] This may take a few minutes...
    [INFO] Installing environment for https://github.com/psf/black.
    [INFO] Once installed this environment will be reused.
    [INFO] This may take a few minutes...
    Check Yaml...............................................................Passed
    Fix End of Files.........................................................Passed
    Trim Trailing Whitespace.................................................Failed
    - hook id: trailing-whitespace
    - exit code: 1
    
    Files were modified by this hook. Additional output:
    
    Fixing sample.py
    
    black....................................................................Passed
    ```

    - oops! 看起来一些文件有尾随空格。
    - 也考虑在[CI](https://pre-commit.com/#usage-in-continuous-integration){target="_blank"}中运行它

## 为你的项目添加pre-commit插件

一旦安装了`pre-commit`, 就可以使用`.pre-commit-config.yaml`配置文件将`pre-commit`插件添加到项目中。

添加一个名为`.pre-commit-config.yaml`的根目录下的文件。`pre-commit`配置文件描述了安装了哪些存储库和hooks(钩子)。

### `.pre-commit-config.yaml` - top level

| 名称 | 描述 |
| :--: | :--: |
| `repos` | [存储库](#pre-commit-configyaml-repos)映射列表 |
| `default_install_hook_types` | (可选的, 默认: `[pre-commit]`)  运行 `pre-commit install` 时默认使用的 `--hook-type` 列表  <br/> 版本2.18.0中添加 |
| `default_language_version` | (可选的, 默认: `{}`) 从语言到应该用于该语言的默认值的映射 。参考官网。 |
| `default_stages` | (可选的, 默认: (all stages(所有阶段))) `hook` 的 stage 属性的配置范围默认值，这只会覆盖钩子中没有设置`stages`属性的钩子. 例如: `default_stages: [pre-commit, pre-push]` |
| `files` | (可选的, 默认: `''`) 全局文件包含模式 |
| `exclude` | (可选的, 默认: `''`) 全局文件不包含模式 |
| `fail_fast` | (可选的, 默认: `false`) 设置为`true`则表示在pre-commit第一次失败之后不会运行钩子 |
| `minimum_pre_commit_version` | (可选的, 默认: `0`) pre-commit 运行时需要的最低版本|

一个简单的 顶层配置:

```yml
exclude: '^$'
fail_fast: false
repos:
-    ...
```

### .pre-commit-config.yaml - repos

存储库映射告诉pre-commit从哪里获取hook(挂钩)代码。

| 名称 | 描述 |
| :--: | :--: |
| `repo` | `git clone` 从那个仓库URL克隆 |
| `rev` | 要克隆的版本或标签。 |
| `hooks` | [hook映射](#pre-commit-configyaml-hooks)列表

一个简单的仓库:

```yml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v1.2.3
    hooks:
    -   ...
```

### .pre-commit-config.yaml - hooks

hook映射配置使用存储库中的哪个挂钩并允许自定义。所有可选密钥将从存储库的配置中接收默认值。

| 名称 | 描述 |
| :--: | :--: |
| `id` | 要使用的存储库中的哪个挂钩。 |
| `alias` | （可选）允许在使用 `pre-commit run <hookid>` 时使用附加 id 引用挂钩 |
| `name` | （可选）覆盖挂钩的名称 - 在挂钩执行期间显示。 |
| `language_version` | （可选）覆盖挂钩的语言版本。参考: [覆盖语言版本](https://pre-commit.com/#overriding-language-version) |
| `files` | （可选）覆盖要运行的文件的默认模式。 |
| `exclude` | （可选）文件排除模式。 |
| `types` | （可选）覆盖要运行的默认文件类型 (AND)。请参阅：[使用类型过滤文件](https://pre-commit.com/#filtering-files-with-types) |
| `types_or` | （可选）覆盖要运行的默认文件类型（或）。请参阅 [使用类型过滤文件](https://pre-commit.com/#filtering-files-with-types)。 2.9.0 中的新功能。 |
| `exclude_types` | （可选）要排除的文件类型。 |
| `args` | （可选）要传递给挂钩的附加参数列表。 |
| `stages` | （可选）选择要运行的 git 钩子。请参阅[限制挂钩在特定阶段运行](https://pre-commit.com/#confining-hooks-to-run-at-certain-stages)。 |
| `additional_dependencies` | （可选）将在运行此挂钩的环境中安装的依赖项列表。一个有用的应用程序是为挂钩安装插件，例如`eslint`. |
| `always_run` | （可选）如果`true`，即使没有匹配的文件，这个钩子也会运行。 |
| `verbose` | （可选）如果`true`，即使挂钩通过，也强制打印挂钩的输出。 |
| `log_file` | （可选）如果存在，则当挂钩失败或详细信息为时，挂钩输出将写入文件或者[verbose](https://pre-commit.com/#config-verbose)为`true`。 |

一个完整配置的示例：

```yml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v1.2.3
    hooks:
    -   id: trailing-whitespace
```

此配置表示下载 `pre-commit-hooks` 项目并运行其 `trailing-whitespace` 挂钩。

### 自动更新hooks

您可以通过运行`pre-commit autoupdate`自动将hooks(钩子)更新到最新版本。默认情况下，这会将hooks(钩子)带到默认分支上的最新标签。

## 用法

运行`pre-commit install` 去安装 pre-commit 到你的git hooks中。 现在 pre-commit 会在你commit时自动运行。 每次你克隆一个项目时，使用 pre-commit 运行 `pre-commit install` 应该是你首先要做的事。

如果你想手动运行所有的 pre-commit 钩子，使用 `pre-commit run --all-files` 命令。 要运行个别的钩子，使用 `pre-commit run <hook_id>` 命令。

第一次在文件上运行pre-commit时，它会自动下载、安装和运行hook(钩子)。 请注意，第一次运行挂钩可能会很慢。 例如：如果机器没有安装node，pre-commit将下载并构建node的副本。

```bash
$ pre-commit install
pre-commit installed at /home/asottile/workspace/pytest/.git/hooks/pre-commit
$ git commit -m "Add super awesome feature"
black....................................................................Passed
blacken-docs.........................................(no files to check)Skipped
Trim Trailing Whitespace.................................................Passed
Fix End of Files.........................................................Passed
Check Yaml...........................................(no files to check)Skipped
Debug Statements (Python)................................................Passed
Flake8...................................................................Passed
Reorder python imports...................................................Passed
pyupgrade................................................................Passed
rst ``code`` is two backticks........................(no files to check)Skipped
rst..................................................(no files to check)Skipped
changelog filenames..................................(no files to check)Skipped
[main 146c6c2c] Add super awesome feature
 1 file changed, 1 insertion(+)
```

## 创建新的钩子

参考官网: [Creating new hooks](https://pre-commit.com/#creating-new-hooks){target="_blank"}

## 命令行界面

参考官网: [Command line interface](https://pre-commit.com/#command-line-interface){target="_blank"}

## 高级功能

参考官网: [Advanced features](https://pre-commit.com/#advanced-features){target="_blank"}

## 贡献

参考官网: [Contributing](https://pre-commit.com/#contributing){target="_blank"}
