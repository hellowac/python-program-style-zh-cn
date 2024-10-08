# PEP 8 - 风格代码例子

pep8-examples.md# 编码样式指南

## 变量交换

```python
# Bad
tmp = a
a = b
b = tmp

# Pythonic
a,b = b,a
```

## 列表推导

```python
# Bad
my_list = []
for i in range(10):
    my_list.append(i*2)

# Pythonic
my_list = [i*2 for i in range(10)]
```

## 单行表达式

虽然列表推导式由于其简洁性及表达性，被广受推崇。

但是有许多可以写成单行的表达式，并不是好的做法。

```python
# Bad
print 'one'; print 'two'

if x == 1: print 'one'

if <complex comparison> and <other complex comparison>:
    # do something

# Pythonic

print 'one'
print 'two'

if x == 1:
    print 'one'

cond1 = <complex comparison>
cond2 = <other complex comparison>
if cond1 and cond2:
    # do something
```

## 带索引遍历

```python
# Bad
for i in range(len(my_list)):
    print(i, "-->", my_list[i])

# Pythonic
for i,item in enumerate(my_list):
    print(i, "-->",item)
```

## 字符串拼接

```python
# Bad
letters = ['s', 'p', 'a', 'm']
s=""
for let in letters:
    s += let

# Pythonic
letters = ['s', 'p', 'a', 'm']
word = ''.join(letters)
```

## 真假判断

```python
# Bad
if attr == True:
    print 'True!'

if attr == None:
    print 'attr is None!'

# Pythonic
if attr:
    print 'attr is truthy!'

if not attr:
    print 'attr is falsey!'

if attr is None:
    print 'attr is None!'
```

真假值对照表：

| 类型   | False          | True                                             |
| ------ | -------------- | ------------------------------------------------ |
| 布尔   | False(与0等价) | True(与1等价)                                    |
| 字符串 | ""(空字符串)   | 非空字符串，例如 " ", "blog"                     |
| 数值   | 0, 0.0         | 非0的数值，例如：1, 0.1, -1, 2                   |
| 容器   | [], (),        | 至少有一个元素的容器对象，例如：[0],(None,),[''] |
| None   | None           | 非None对象                                       |

## 访问字典元素

```python
# Bad

d = {'hello': 'world'}
if d.has_key('hello'):
    print d['hello']    # prints 'world'
else:
    print 'default_value'

# Pythonic

d = {'hello': 'world'}

print d.get('hello', 'default_value') # prints 'world'
print d.get('thingy', 'default_value') # prints 'default_value'

# Or:
if 'hello' in d:
    print d['hello']
```

## 操作列表

```python
# Bad

a = [3, 4, 5]
b = []
for i in a:
    if i > 4:
        b.append(i)

# Pythonic

a = [3, 4, 5]
b = [i for i in a if i > 4]
# Or:
b = filter(lambda x: x > 4, a)
Bad

a = [3, 4, 5]
for i in range(len(a)):
    a[i] += 3

# Pythonic

a = [3, 4, 5]
a = [i + 3 for i in a]
# Or:
a = map(lambda i: i + 3, a)
```

## 文件读取

```python
# Bad

f = open('file.txt')
a = f.read()
print a
f.close()

# Pythonic

with open('file.txt') as f:
    for line in f:
        print line
```

## 代码续行

```python
# Bad
my_very_big_string = """For a long time I used to go to bed early. Sometimes, \
    when I had put out my candle, my eyes would close so quickly that I had not even \
    time to say “I’m going to sleep.”"""

from some.deep.module.inside.a.module import a_nice_function, another_nice_function, \
    yet_another_nice_function

# Pythonic
my_very_big_string = (
    "For a long time I used to go to bed early. Sometimes, "
    "when I had put out my candle, my eyes would close so quickly "
    "that I had not even time to say “I’m going to sleep.”"
)

from some.deep.module.inside.a.module import (
    a_nice_function, another_nice_function, yet_another_nice_function)
```

## 显式代码

```python
# Bad
def make_complex(*args):
    x, y = args
    return dict(**locals())

# Pythonic
def make_complex(x, y):
    return {'x': x, 'y': y}
```

## 使用占位符

```python
# Pythonic
filename = 'foobar.txt'
basename, _, ext = filename.rpartition('.')
```

## 链式比较

```python
# Bad
if age > 18 and age < 60:
    print("young man")

# Pythonic

if 18 < age < 60:
    print("young man")

# 理解了链式比较操作，那么你应该知道为什么下面这行代码输出的结果是 False
>>> False == False == True 
False
```

## 三目运算

这个保留意见。随使用习惯就好。

```python
# Bad
if a > 2:
    b = 2
else:
    b = 1
#b = 2

# Pythonic

a = 3   

b = 2 if a > 2 else 1
#b = 2
```

## or赋值

某些情况下，`or`可以替换`if else` 达到代码简化的作用，比如在变量赋值时, 并且支持链式调用

```python
# 基本用法
v = p1 or p2
# v = p1 if p1 else p2

# 链式用法, 直到找到为真的值来赋值，否则赋值最后的值
v = p1 or p2 or p3 or default

# if p1:
#     v = p1
# elif p2:
#     v = p2
# elif p3:
#     v = p3
# else:
#     v = defualt
```

## Python3 新特性

### \*和\*\*解构

```python
# Pythonic

a, *rest = [1, 2, 3]
# a = 1, rest = [2, 3]

a, *middle, c = [1, 2, 3, 4]
# a = 1, middle = [2, 3], c = 4

# 解构字典和列表
print(*[1], *[2], 3, *[4, 5])

def fn(a, b, c, d):
    print(a, b, c, d)

fn(**{'a': 1, 'c': 3}, **{'b': 2, 'd': 4})

# 也可以解构元祖，集合set等
*range(4), 4

[*range(4), 4]

{*range(4), 4, *(5, 6, 7)}

{'x': 1, **{'y': 2}}
```

### 字符串格式化

```python
# 早期 - python 2

print("name:%s, age:%s, sex: %s," %('张三', 18, '男'))

# 后来 - python 2

print("name:{}, age:{}, sex:{}".format('张三', 18, '男'))
print("name:{name}, age:{age}, sex:{sex}".format(name='张三', age=18, sex='男'))

# 现在 - python3
name, age, sex = ('张三', 18, '男') # 自动解包
print(f"name:{name}, age:{age}, sex:{sex}")
```

### f字符串支持用=

自动记录表达式和调试文档

增加 = 说明符用于 [f-string](https://docs.python.org/zh-cn/3.8/glossary.html#term-f-string)。 形式为 `f'{expr=}'` 的 f-字符串将扩展表示为表达式文本，加一个等于号，再加表达式的求值结果。

```python
# 基本用法
>>> import datetime
>>> user = 'eric_idle'
>>> member_since = datetime.date(1975, 7, 31)
>>> f'{user=} {member_since=}'
"user='eric_idle' member_since=datetime.date(1975, 7, 31)"

# 通常的 f-字符串格式说明符 允许更细致地控制所要显示的表达式结果:
>>> delta = datetime.date.today() - member_since
>>> f'{user=!s}  {delta.days=:,d}'
'user=eric_idle  delta.days=17,436'

# = 说明符将输出整个表达式，以便详细演示计算过程:
>>> from math import cos, radians
>>> theta = 30
>>> print(f'{theta=}  {cos(radians(theta))=:.3f}')
theta=30  cos(radians(theta))=0.866
```

### 字典新增合并运算

python 3.9新增特性

合并 (`|`) 与更新 (`|=`) 运算符已被加入内置的 `dict` 类。 它们为现有的 `dict.update` 和 `{**d1, **d2}` 字典合并方法提供了补充。

```python
>>> x = {"name": "张三", "sex": "男"}
>>> y = {"name": "张小三", "sex": "男"}
>>> print(x | y)  # 取并集并覆盖
{'name': '张小三', 'sex': '男'}
>>> print(y | x)  # 取并集并覆盖
{'name': '张三', 'sex': '男'}
```

### 数字加下划线

数字中可以使用下划线增强可读性

```python
print(1_000_000_000_000_00)
print(0x_FF_FF_FF_FF)

# 字符串格式化也支持下划线_选项
```

### 类型标注

参考官网: <https://docs.python.org/zh-cn/3/library/typing.html>

#### 变量标注

```python
# 需要一部分IDE支持
primes: list[int] = []

captain: str  # Note: no initial value!

class Starship:
    stats: dict[str, int] = {}

primes.append('sda')  # 这里会类型检查不通过
print(primes)
```

#### 类型别名

把类型赋给别名，就可以定义类型别名。

```python
# Vector 和 list[float] 相同，可互换
Vector = list[float]

def scale(scalar: float, vector: Vector) -> Vector:
    return [scalar * num for num in vector]

# 通过类型检查; 一个浮点数的列表组合 类型为 Vector.
new_vector = scale(2.0, [1.0, -4.2, 5.4])
```

**类型别名**主要适用于简化复杂的类型签名

```python
from collections.abc import Sequence  # 序列泛型

ConnectionOptions = dict[str, str]
Address = tuple[str, int]
Server = tuple[Address, ConnectionOptions]

def broadcast_message(message: str, servers: Sequence[Server]) -> None:
    ...

# 静态类型检查器会将前一个类型签名视为与当前类型签名完全相同。
def broadcast_message(
        message: str,
        servers: Sequence[tuple[tuple[str, int], dict[str, str]]]) -> None:
    ...
```

## 标准库

### csv

参考标准库: <https://docs.python.org/zh-cn/3/library/csv.html>

`CSV` (Comma Separated Values) 格式是电子表格和数据库中最常见的输入、输出文件格式。

`csv` 模块实现了 `CSV` 格式表单数据的读写

```python
# 基本读写
import csv

# csv.reader 读取
with open('eggs.csv', newline='') as csvfile:
    spamreader = csv.reader(csvfile, delimiter=' ', quotechar='|')
    for row in spamreader:
        print(', '.join(row))

# csv.writer 写入
with open('eggs.csv', 'w', newline='') as csvfile:
    spamwriter = csv.writer(csvfile, delimiter=' ',
                            quotechar='|', quoting=csv.QUOTE_MINIMAL)
    spamwriter.writerow(['Spam'] * 5 + ['Baked Beans'])
    spamwriter.writerow(['Spam', 'Lovely Spam', 'Wonderful Spam'])

# 字典读写
import csv

# csv.DictReader 读取字典格式
with open('names.csv', newline='') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        print(row['first_name'], row['last_name'])

# csv.DictWriter 写入字典格式
with open('names.csv', 'w', newline='') as csvfile:
    fieldnames = ['first_name', 'last_name']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

    writer.writeheader()
    writer.writerow({'first_name': 'Baked', 'last_name': 'Beans'})
    writer.writerow({'first_name': 'Lovely', 'last_name': 'Spam'})
    writer.writerow({'first_name': 'Wonderful', 'last_name': 'Spam'})
```

### io

参考官网: <https://docs.python.org/zh-cn/3/library/io.html>

io 模块提供了 Python 用于处理各种 I/O 类型的主要工具。三种主要的 I/O类型分别为: 文本 I/O, 二进制 I/O 和 原始 I/O。

#### 文本IO

内存中文本流作为 [StringIO](https://docs.python.org/zh-cn/3/library/io.html#io.StringIO) 对象使用：

```python
# 文本I/O预期并生成 str 对象。
f = io.StringIO("some initial text data")

# 主要用于生成小的文本文件（例如：csv），便于处理，而非创建一个临时文件（磁盘IO）
```

#### 二进制 I/O

二进制I/O（也称为**缓冲I/O**）预期 [bytes-like objects](https://docs.python.org/zh-cn/3/glossary.html#term-bytes-like-object) 并生成 [bytes](https://docs.python.org/zh-cn/3/library/stdtypes.html#bytes) 对象。

```python
# 存储二进制数据
f = io.BytesIO(b"some initial binary data: \x00\x01")

# 多常用于图片、验证码等。
```

### collections 常用容器

#### ChainMap

一个 [ChainMap](https://docs.python.org/zh-cn/3/library/collections.html#collections.ChainMap) 将多个字典或者其他映射组合在一起，创建一个单独的可更新的视图。 如果没有 maps 被指定，就提供一个默认的空字典，这样一个新链至少有一个映射。

```python
>>> baseline = {'music': 'bach', 'art': 'rembrandt'}
>>> adjustments = {'art': 'van gogh', 'opera': 'carmen'}
>>> list(ChainMap(adjustments, baseline))
['music', 'art', 'opera']

# python3 新语法 针对字典 的 | 运算符也可以
```

#### Counter

一个计数器工具提供快速和方便的计数

```python
>>> from collections import Counter
>>> for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
...     cnt[word] += 1
... 
>>> cnt
Counter({'blue': 3, 'red': 2, 'green': 1})
```

#### defaultdict

返回一个新的类似字典的对象。 `defaultdict` 是内置 `dict` 类的子类。 它重载了一个方法并添加了一个可写的实例变量。 其余的功能与 `dict` 类相同因而不在此文档中写明。

```python
>>> from collections import defaultdict
>>> s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
>>> d = defaultdict(list)
>>> for k, v in s:
...     d[k].append(v)
... 
>>> sorted(d.items())
[('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]
```

#### namedtuple

命名元组赋予每个位置一个含义，提供可读性和自文档性。它们可以用于任何普通元组，并添加了通过名字获取值的能力，通过索引值也是可以的。

```python
>>> from collections import namedtuple
>>> Point = namedtuple('Point', ['x', 'y'])  # 使用位置或关键字参数实例化
>>> p = Point(11, y=22)                      # 像普通元组 (11, 22) 一样可索引
>>> p[0] + p[1]
33
>>> x, y = p                                 # 像普通元组一样解构
>>> x, y
(11, 22)
>>> p.x + p.y                                # 也可按名称访问字段
33
>>> p
Point(x=11, y=22)                            # 以可读的name=value形式作为__repr__的输出
```

## 内置函数

### map

返回一个迭代器，它将函数应用于可迭代的每个项目，产生结果。 如果传递了额外的可迭代参数，则函数必须采用那么多参数，并并行应用于所有可迭代的项目。

```python
# 有时候需要批量需要将pk的集合转化为str，然后进行join操作
>>> pk_list = [1,2,3,4,5,6]
>>> pk_list_str = ','.join(map(lambda x: str(x), pk_list))
>>> pk_list_dtr
>>> pk_list_str
'1,2,3,4,5,6'
```

### filter

从 `iterable` 的那些元素构造一个迭代器，其中 `function` 为真。 `iterable` 可以是序列、支持迭代的容器或迭代器。 如果 `function` 为 `None`，则假设为恒等函数，即 `iterable` 中所有为 `false` 的元素都将被移除。

```python
# 保留执行函数为真的值
>>> pk_list = [1,2,3,4,5,6, 7, 8]
>>> pk_list = filter(lambda x: x%2==0, pk_list)  # 保留能被2整除的PK
>>> pk_list_str = ','.join(map(lambda x: str(x), pk_list))
>>> pk_list_str
'2,4,6,8'

# 过滤值bool判断为false的值
>>> pk_list = [0, 1,3,0,2, -1, 0, 6]
>>> pk_list = filter(None, pk_list) 
>>> pk_list_str = ','.join(map(lambda x: str(x), pk_list))
>>> pk_list_str
'1,3,2,-1,6'
```

### any

如果 `iterable` 的任一元素为真值则返回 `True`。 如果可迭代对象为空，返回 `False`。 等价于:

```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

### all

如果 `iterable` 的所有元素均为真值（或可迭代对象为空）则返回 `True` 。 等价于：

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

### zip

在多个迭代器上并行迭代，从每个迭代器返回一个数据项组成元组

```python
# 有时候经常遇到sql执行之后返回这样的值
>>> keys = ('a', 'b', 'c')
>>> values = [[1,2,3], [4,5,6], [7,8,9]]
>>> list(map(dict, map(lambda items: zip(keys, items), values)))
[{'a': 1, 'b': 2, 'c': 3}, {'a': 4, 'b': 5, 'c': 6}, {'a': 7, 'b': 8, 'c': 9}]
```

### sorted

定义: `sorted(iterable, /, *, key=None, reverse=False)`

根据 `iterable` 中的项返回一个新的已排序列表。

具有两个可选参数，它们都必须指定为关键字参数。

`key` 指定带有单个参数的函数，用于从 `iterable` 的每个元素中提取用于比较的键 (例如 `key=str.lower`)。 默认值为 `None` (直接比较元素)。

`reverse` 为一个布尔值。 如果设为 `True`，则每个列表元素将按反向顺序比较进行排序。

### sum

定义: `sum(iterable, /, start=0)`

从 `start` 开始自左向右对 `iterable` 的项求和并返回总计值。 `iterable` 的项通常为数字，而 `start` 值则不允许为字符串。

对某些用例来说，存在 `sum()` 的更好替代。 拼接字符串序列的更好更快方式是调用 `''.join(sequence)`。 要以扩展精度对浮点值求和，参考 `math.fsum()`。 要拼接一系列可迭代对象，请参考使用 `itertools.chain()`。

### range

生成指定区间的整数数列

```python
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1, 11))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> list(range(0, 30, 5))
[0, 5, 10, 15, 20, 25]
>>> list(range(0, 10, 3))
[0, 3, 6, 9]
```

### getattr

返回对象命名属性的值。 名称必须是字符串。 

### setattr

赋值指定属性以及值给对象。

如 `setattr(x, 'foobar', 123)` 等价于 `x.foobar = 123`。

### hasattr

判断一个对象是否拥有某个属性， 如果拥有返回`True`、否则返回`False`

### enumerate

返回一个枚举对象。`iterable` 必须是一个序列，或 `iterator`，或其他支持迭代的对象。 `enumerate()` 返回的迭代器的 `__next__()` 方法返回一个元组，里面包含一个计数值（从 `start` 开始，默认为 `0`）和通过迭代 `iterable` 获得的值。

```python
>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

等价于:

```python
def enumerate(iterable, start=0):
    n = start
    for elem in iterable:
        yield n, elem
        n += 1
```

## 项目实战

### 代码优化1

优化前

```python
def get_access_token(cls, data):
    param = data.get('param')
    code = param.get('code')
    home_url = param.get('home_url')
    if not code:
        raise Exception('缺少参数code')
    url = 'https://api.weixin.qq.com/sns/oauth2/access_token?grant_type=authorization_code&appid={}&secret={}&' \
            'code={}'.format(
            public_account_config.get('app_id'), public_account_config.get('secret'), code)
    # 获取到微信的access_token、openid
    res = requests.get(url, params=data).json()

    # 存在跳转链接
    if home_url:
        return redirect_link(home_url, res)
    return {
        'code': UserStatusCode.OK,
        'message': 'ok',
        'data': res
    }
```

优化后:

```python
def get_access_token(cls, data: dict):
    param = data.get('param')
    code = param.get('code')
    home_url = param.get('home_url')
    app_id = public_account_config.get('app_id')
    secret = public_account_config.get('secret')

    if not code:
        raise Exception('缺少参数code')
    
    parameters = (
        ('grant_type', 'authorization_code'),
        ('appid', app_id),
        ('secret', secret),
        ('code', code),
    )

    param_url = '&'.join([f'{key}={val}' for (key, val) in parameters])

    url = f'https://api.weixin.qq.com/sns/oauth2/access_token?{param_url}'
    # 获取到微信的access_token、openid
    res = requests.get(url).json()

    # 存在跳转链接
    if home_url:
        return redirect_link(home_url, res)

    return {
        'code': UserStatusCode.OK,
        'message': 'ok',
        'data': res
    }
```