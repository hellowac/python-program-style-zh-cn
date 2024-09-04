# 编程命名和英文字母缩写

## 命名规则

目前，业界共有四种命名法则：**驼峰命名法**、**匈牙利命名法**、**帕斯卡命名法**和**下划线命名法**，其中前三种是较为流行的命名，而第四种在python中则有特殊的意义，详细参考[pep8-命名约定](pep8.md#_20)

### 驼峰命名法

驼峰式命名法，又叫**小驼峰式命名法**（所以自然就存在大驼峰命名法啦)。

该命名规范，要求第一个单词首字母小写，后面其他单词首字母大写，简单粗暴易学易用。

```c
int myAge;
char myName[10];
float manHeight;
```

### 匈牙利命名法

匈牙利命名法是早期的规范，由微软的一个匈牙利人发明的，是 IDE 还十分智障的年代的产物。那个年代，当代码量很多的时候，想要确定一个变量的类型是很麻烦的，不像现在 IDE 都会给提示，所以才产生了这样一个命名规范，估计现在已经没啥人用了吧……一个十分系统却又琐碎的命名规范。

该命名规范，要求前缀字母用变量类型的缩写，其余部分用变量的英文或英文的缩写，单词第一个字母大写。

```c
int iMyAge;        #  "i": int
char cMyName[10];  #  "c": char
float fManHeight;  #  "f": float
```

其他前缀类型还有：

```text
a      数组（Array）
b      布尔值（Boolean）
by     字节（Byte）
c      有符号字符（Char）
cb     无符号字符（Char Byte，并没有神马人用的）
cr     颜色参考值（Color Ref）
cx,cy  坐标差（长度 Short Int）
dw     双字（Double Word）
fn     函数（Function）
h      Handle（句柄）
i      整形（Int）
l      长整型（Long Int）
lp     长指针（Long Pointer）
m_     类成员（Class Member）
n      短整型（Short Int）
np     近程指针（Near Pointer）
p      指针（Pointer）
s      字符串（String）
sz     以 Null 做结尾的字符串型（String with Zero End）
w      字（Word）
```

还有其他更多的前缀是根据微软自己的 MFC/句柄/控件/结构等东西定义的，就不过多描述了。

### 帕斯卡命名法

帕斯卡命名法，又叫大驼峰式命名法。

与小驼峰式命名法的最大区别在于，每个单词的第一个字母都要大写。

```java
int MyAge;
char MyName[10];
float ManHeight;
```

二者都是采用了帕斯卡命名法。

### 下划线命名法

下划线命名法并不如大小驼峰式命名法那么备受推崇，但是也是浓墨重彩的一笔。尤其在宏定义和常量中使用比较多，通过下划线来分割全部都是大写的单词。

该命名规范，也是很简单，要求单词与单词之间通过下划线连接即可。

```c
int my_age;
char my_name[10];
float man_height;
```

## 命名的基本原则

??? "(1)标识符的命名要清晰、明了，有明确含义，同时使用完整的单词或大家基本可以理解的缩写"

    避免使人产生误解——尽量采用采用英文单词或全部中文全拼表示，若出现英文单词和中文混合定义时，使用连字符**“_”**将英文与中文割开。较短的单词可通过去掉“**元音**”形成缩写；较长的单词可取单词的头几个字母形成缩写；一些单词有大家公认的缩写。例如：`temp`->`tmp`、`flag`->`flg`、`statistic`->`stat`、`increment`->`inc`、`message`->`msg`等缩写能够被大家基本认可。

??? "(2)命名中若使用特殊约定或缩写，则要有注释说明"

    应该在源文件的开始之处，对文件中所使用的缩写或约定，特别是特殊的缩写，进行必要的注释说明。

??? "(3)命名规范必须与所使用的系统风格保持一致，并在同一项目中统一"

    为了项目后期的方便运维和理解以及再次开发。

??? "(4)对于变量命名，禁止取单个字符(如i 、j 、k... )"

    建议除了要有具体含义外，还能表明其变量类型、数据类型等，但`i` 、`j` 、`k` 作局部循环变量是允许的。变量，尤其是局部变量，如果用单个字符表示，很容易敲错(如`i`写成`j`)，而编译时又检查不出来，有可能为了这个小小的错误而花费大量的查错时间。

## 编程单词缩写规则

1. 大于2个单词则采用缩写规则，否则不用缩写。
2. 缩写的规则采用国际惯用方法：

    元音字母剔除法，首字母除外。

    使用单词的头一个或几个字母。

??? "组合单词使用规则"

    1. 使用变量名中每个有典型意义的单词。如Count of Failure写成FailCnt。
    2. 去掉无用的单词后缀 ing, ed等。如Paging Request写成PagReq。

参考缩写项目: [identifier-abbr](https://github.com/dablelv/identifier-abbr/tree/main){target="_blank"}

### A

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| A | Addition | Add‍ | 除了 |
|   | Accumulator | Acc | 蓄电池 |
|   | Address | Addr | 地址 |
|   | Action | Act | 行动 |
|   | Active | Act | 活跃的 |
|   | Amplitude | Amp | 振幅 |
|   | Analog Input | AI | 模拟输入 |
|   | Anolog I/O | AIO | 模拟输入/输出 |
|   | All | All | 所有 |
|   | Alarm | Alm | 报警 |
|   | Allocate | Alloc | 分配 |
|   | Analog Output | AO | 模拟输出 |
|   | Apparent | App | 明显的 |
|   | Argument | Arg | 参数 |
|   | Arrange | Arrng | 数列 |
|   | Array | Array | 数组 |
|   | Assemble | Asm | 集合/组合/聚集/组成/聚合 |
|   | Attribute | Attrib | 属性 |

### B

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| B | Bar | Bar | 酒吧/珊/块 |
|   | Bit | Bit | 位/ |
|   | Byte | Byte | 字节 |
|   | Block | Blk | 块 |
|   | Buffer | Buf | 缓冲 |
|   | Button | Btn | 按钮 |
|   | Bypass | Bypass | 绕过/分流 |

### C

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| C | Calibration | Cal | 校准 |
|   | Calculate | Calc | 计算 |
|   | Category | cate | 分类 |
|   | Configuration | Cfg | 配置 |
|   | Channel | Ch | 通道/渠道 |
|   | Change | Chg | 改变 |
|   | Check | Chk | 检查 |
|   | Clock | Clk | 时钟 |
|   | Clear | Clr | 清晰的 |
|   | Clear Screen | Cls | 清晰的屏幕 |
|   | Command | Cmd | 命令 |
|   | Compare | Cmp | 比较 |
|   | Complete | Comp | 完整的 |
|   | Count | Cnt | 数 |
|   | Counter | Ctr | 计数器 |
|   | Column | Col | 列 |
|   | Communication | Comm | 沟通 |
|   | Connect | Con | 连接 |
|   | Construct | Cons | 构造 |
|   | Control | Ctrl | 控制 |
|   | Context | Ctx | 上下文 |
|   | Convert | Conv | 转换 |
|   | Copy | Cp | 复制 |
|   | Current | Cur | 当前的 |
|   | Cursor | Csr | 光标 |
|   | Control Word | CW | 控制字 |

### D

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| D | Date | Date | 日期 |
|   | Day | Day | 一天 |
|   | Debounce | Debounce | 防反跳 |
|   | Decrease | Dec | 减少 |
|   | Decimal | Dec | 小数 |
|   | Decode | Decode | 解码 |
|   | Define | Def | 定义 |
|   | Degree | Deg | 学位 |
|   | Delete | Del | 删除 |
|   | Destination | Dst | 目的地 |
|   | Descriptor | Desc | 描述符 |
|   | Device | Dev | 设备 |
|   | Discrete Input | DI | 离散输入 |
|   | Digit | Dig | 数字 |
|   | Discrete I/O | DIO | 离散I / O |
|   | Discrete Output(s) | DO | 离散输出(年代) |
|   | Disable | Dis | 禁用 |
|   | Display | Disp | 显示 |
|   | Discovery | Disc | 发现 |
|   | Division | Div | 部门 |
|   | Divisor/Division | Div | 除数/部门 |
|   | Delay | Dly | 延迟 |
|   | Day-of-week | DOW | 一周中的第几天 |
|   | Down | Down | 下来 |
|   | Dummy | Dummy | 假 |
|   | Dynamic | Dyn | 动态 |

### E

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| E | Edge | Edge | 边缘 |
|   | Effective | Eff | 有效的 |
|   | Electric | Elec | 电 |
|   | Empty | Empty | 空 |
|   | Enable | En | 启用 |
|   | Engine | Eng | 引擎 |
|   | Enter | Enter | 输入 |
|   | Entries | Entries | 条目 |
|   | Equivalent | Equiv | 等效 |
|   | Error(s) | Err | 错误(年代) |
|   | Ethernet | Eth | 以太网 |
|   | Engineering Units | EU | 工程单位 |
|   | Event(s) | Event | 事件(年代) |
|   | Extension | Ext | 扩展 |
|   | Exit | Exit | 退出 |
|   | Exception | Exc | 异常 |
|   | Expiration | Exp | 过期 |
|   | Exponent | Exp | 指数 |

### F

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| F | Field | Fld | 场 |
|   | Flag | Flag | 国旗 |
|   | Flush | Flush | 冲洗 |
|   | Function(s) | Fnct | 函数(年代) |
|   | Format | Format | 格式 |
|   | Fraction | Fract | 分数 |
|   | Free | Free | 免费的 |
|   | Frequency | Freq | 频率 |
|   | Full | Full | 完整的 |

### G

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| G | Gain | Gain | 获得 |
|   | Get | Get | 得到 |
|   | Generate | Gen | 生成 |
|   | Group(s) | Grp | 集团(年代) |

### H

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| H | Handler | Handler | 处理程序 |
|   | Harmonic | Harm | 谐波 |
|   | Hexadecimal | Hex | 十六进制 |
|   | High | Hi | 高 |
|   | History | Hist | 历史 |
|   | Hit | Hit | 打击 |
|   | High Priority Task | HPT | 高优先级任务 |
|   | Hour(s) | Hr | 小时(年代) |

### I

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| I | I.D. | Id | 身份证 |
|   | Idle | Idle | 闲置 |
|   | Impulse | Imp | 冲动 |
|   | Input(s) | In | 输入(年代) |
|   | Initialization | Init | 初始化 |
|   | Initialize | Init | 初始化 |
|   | Instruction | Instr | 指令 |
|   | Interrupt | Int | 中断 |
|   | Invert | Inv | 反 |
|   | Interrupt Service Routine | ISR | 中断服务例程 |
|   | Index | Ix | 指数 |

### K

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| K | Key | Key | 关键 |
|   | Keyboard | Key | 键盘 |
|   | Key Word | Kw | 关键字 |

### L

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| L | Length | Len | 长度 |
|   | Limit | Lim | 限制 |
|   | List | List | 列表 |
|   | Low | Lo | 低 |
|   | Lower | Le | 较低的 |
|   | Lowest | Lo | 最低 |
|   | Lock | Lock | 锁 |
|   | Low Priority Task | LTP | 低优先级的任务 |

### M

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| M | Magnitude | Mag | 级 |
|   | Mantissa | Man | 尾数 |
|   | Manual | Man | 手册 |
|   | Manufacture | Mfg | 制造 |
|   | Maximum | Max | 最大 |
|   | Mailbox | Mbox | 邮箱 |
|   | Minimum | Min | 最低 |
|   | Mode | Mode | 模式 |
|   | Month | Month | 月 |
|   | Move | Mov | 移动 |
|   | Message | Msg | 消息 |
|   | Measure | Meas | 测量 |
|   | Mask | Msk | 面具 |
|   | Multiplication | Mul | 乘法 |
|   | Multiplex | Mux | 多路复用 |
|   | Make | Mk | 使 |

### N

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| N | Negative | Neg | 负 |
|   | Number of  | Num | 的数量 |
|   | Nesting | Nesting | 嵌套 |
|   | Neutral | Neut | 中性 |
|   | New | New | 新 |
|   | Next | Next | 下一个 |

### O

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| O | Offset | Offset | 抵消 |
|   | Old | Old | 老 |
|   | Operation System | OS | 操作系统 |
|   | Optimize | Opt | 优化 |
|   | Original | Orig | 原始 |
|   | Output | Out | 输出 |
|   | Overflow | Ovf | 溢出 |

### P

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| P | Package | Pkg | 包 |
|   | Parameter | Param | 参数 |
|   | Pass | Pass | 通过 |
|   | Performance | Perf | 性能 |
|   | Period | Per | 期 |
|   | Phase | Ph | 阶段 |
|   | Port | Port | 港口 |
|   | Position | Pos | 位置 |
|   | Positive | Pos | 积极的 |
|   | Power | Pwr | 权力 |
|   | Previous | Prev | 以前的 |
|   | Priority | Prio | 优先级 |
|   | Printer | Prt | 打印机 |
|   | process | Proc | 过程 |
|   | Product | Prod | 产品 |
|   | Protocol | Prot | 协议 |
|   | Pointer | Ptr | 指针 |
|   | Put | Put | 把 |

### Q

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| Q | Queue | Q | 队列 |
|   | Quality | Qlty | 质量 |
|   | Quarter | Quar | 季度 |

### R

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| R | Raw | Raw | 生 |
|   | Reactive | React | 无功 |
|   | Recall | Rcl | 回忆 |
|   | Rectangle | Rect | 矩形 |
|   | Read | Rd | 读 |
|   | Ready | Rdy | 准备好了 |
|   | Reference | Ref | 参考 |
|   | Register | Reg | 注册 |
|   | Request | Req | 请求 |
|   | Reset | Reset | 重置 |
|   | Reserve | Resv | 储备 |
|   | Resume | Resume | 的简历 |
|   | Response | Resp | 响应 |
|   | Return | Rtn | 返回 |
|   | Reverse | Revs | 反向 |
|   | Ring | Ring | 环 |
|   | Row | Row | 行 |
|   | Repeat | Rpt | 重复 |
|   | Real-Time | RT | 实时 |
|   | Running | Running | 运行 |
|   | Receive | Rx | 收到 |

### S

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| S | Sample | Smp | 样本 |
|   | Scale | Scale | 规模 |
|   | Scale Factor | SF | 比例因子 |
|   | Scaling | Scaling | 扩展 |
|   | Scan | Scan | 扫描 |
|   | Schedule | Sched | 时间表 |
|   | Scheduler | Sched | 调度器 |
|   | Screen | Scr | 屏幕 |
|   | Second(s) | Sec | 第二个(s) |
|   | Segment(s) | Seg | 段(年代) |
|   | Select | Sel | 选择 |
|   | Semaphore | Sem | 信号量 |
|   | Sequence | Seq | 序列 |
|   | Server | Svr | 服务器 |
|   | Set | Set | 集 |
|   | Setting | Setting | 设置 |
|   | Signal | Sig | 信号 |
|   | Size | Size | 大小 |
|   | Seven-segments | SS | 七段 |
|   | Sourse | Src | 万恶之源 |
|   | Start | Start | 开始 |
|   | Statistic(s) | Stat | 统计(s) |
|   | Status | Stat | 状态 |
|   | Stack | Stk | 堆栈 |
|   | Standard | Std | 标准 |
|   | Stop | Stop | 停止 |
|   | String | Str | 字符串 |
|   | Subtraction | Sub | 减法 |
|   | Suspend | Suspend | 暂停 |
|   | Switch | Sw | 开关 |
|   | Synchronize | Synch | 同步 |
|   | System | Syst | 系统 |

### T

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| T | Task | Task | 任务 |
|   | Table | Tbl | 表 |
|   | Threshold | Th | 阈值 |
|   | Tick | Tick | 蜱虫 |
|   | Time | Time | 时间 |
|   | Timer | Tmr | 计时器 |
|   | Toggle | Tgl | 切换 |
|   | Total | Tot | 总 |
|   | Trigger | Trig | 触发 |
|   | Time-stamp | TS | 时间戳 |
|   | Timeout | TO | 超时 |

### U

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| U | Unlock | Unlock | 解锁 |
|   | Up | Up | 向上 |
|   | Update | Update | 更新 |
|   | Utility | Util | 实用程序 |

### V

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| V | Value | Val | 价值 |
|   | Vector | Vect | 向量 |
|   | Version | Ver | 版本 |
|   | Variable | Var | 变量 |
|   | Visible | Vis | 可见 |
|   | Voltage | Vol | 电压 |

### W

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| W | Watchdog | Wdog | 监管机构 |
|   | Write | Wr | 写 |

### Y

| 序号 | 描述 | 缩写词 | 机翻中文 |
| :--: | :--: | :--: | :--: |
| Y | Year | Year | 一年 |
