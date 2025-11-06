# 廖雪峰的Python

> [!IMPORTANT]
>
> - Python 大小写敏感
> - // 地板除 / 精确除
> - Python 通过缩进来控制代码快
> - 赋值语句 a, b = b, a + b 相当于： a = b，b = a+b



## 命令行

- Python -i 可以交互式执行命令

### pip

- pip list 查看所有安装的三方库
- pip show package 看出某个三方库信息

## 基本函数

- int()函数用于 str 转型 int

```python
int("1")
```

- float()函数用于 str 转型 float

```python
float("1.1")
```

- isinstance()函数用于判断类型

```python
isinstance(x, A_tuple)#用于判断x是否属于A_tuple类型
```

- type()函数来判断对象类型

```plain
>>> type(123)
<class 'int'>
>>> type('str')
<class 'str'>
>>> type(None)
<type(None) 'NoneType'>
```

## 基础

### 输入输出

- print() 输出

- input() 输入

  - 传入 String 可以作为提示语

    ```
    input('tip：')
    ```

### 数据类型

#### 整型、浮点型

- 数字之间可以用_分隔用于分辨数字过长

#### 布尔值

- 可以直接 True 、False 表示
- and 就是 &&
- or 就是 ||
- not 就是 !

#### 空值

- none 表示

#### 字符串

- “ ”，' '都能表示字符串

- r' '表示内部的都不转义 （**结束的‘’ ' 前的\不能出现奇数个**）

- '" "'可以多行使用

- `ord()` 函数获取字符的整数

- `chr()` 函数把编码转换为对应的字符

- 与字符数组转换

  - 字符数组 b'xxx'表示

  - 在 `bytes` 中，无法显示为 ASCII 字符的字节，用 `\x##` 显示。

  - String - bytes

    - "xxx".encode(编码方式)

    - ```
      >>> 'ABC'.encode('ascii')
      b'ABC'
      >>> '中文'.encode('utf-8')
      b'\xe4\xb8\xad\xe6\x96\x87'
      ```

  - bytes - String

  - b'xxx'.decode(编码方式)

  - ```
      >>> b'ABC'.decode('ascii')
      'ABC'
      >>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
      '中文'
      ```

  - 可以传入 `errors='ignore'` 忽略错误的

  - ```
      >>> b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore')
      '中'
      ```

- len()函数计算长度 len(xxx)

  - String 算的是字符的数量
  - bytes 算的是字节的数量

- 格式化

  - 采用的格式化方式和 C 语言

  - 占位符 %

    - 有几个 `%?` 占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个 `%?`，括号可以省略

    - `%` 是一个普通字符需要转义，用 `%%` 来表示一个 `%`

    - ```
      >>> 'Age: %s. Gender: %s' % (25, True)
      'Age: 25. Gender: True'
      >>> 'growth rate: %d %%' % 7
      'growth rate: 7 %'
      ```

  - format()方法

    - 它会用传入的参数依次替换字符串内的占位符 `{0}`、`{1}`……

    - ```
      >>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
      'Hello, 小明, 成绩提升了 17.1%'
      ```

  - f-string

    - 字符串如果包含 `{xxx}`，就会以对应的变量替换

    - ```
      >>> r = 2.5
      >>> s = 3.14 * r ** 2
      >>> print(f'The area of a circle with radius {r} is {s:.2f}')
      The area of a circle with radius 2.5 is 19.62	
      ```

- 常用函数

  - "x".join(list)

    - 返回 str 讲 list 中的 str 元素通过 x 间隔分开

    - ```python
      args = ['gcc', 'hello.c', 'world.c',"ddd","123"]
      print(":".join(args))
      #gcc compile: hello.c, world.c, ddd, 123
      ```

### 容器

#### list

- 有序可变集合

- 类似于 Java 数组的定义方式

  - ```python
    classmates = ['Michael', 'Bob', 'Tracy']
    ```

- 用索引来访问 list 中每一个位置的元素

  - ```python
    classmates[0]
    ```

  - 用-1 可以获取倒数第 1 个元素，以此类推

- 常用方法

  - list.append(obj) 尾部添加 (类似 add)
  - list.insert(index，obj) 插入（类似 set）
  - list.pop(index) 移除根据索引
  - list.remove(obj) 移除根据对象
  - list.clear 清空
  - list.sort 小到大排序

#### tuple

- 有序不可变集合

- 定义方式用（）

  - ```python
    classmates = ('Michael', 'Bob', 'Tracy')
    ```

- 只有 1 个元素的 tuple 定义时必须加一个逗号 `,`

  - ```python
    >>> t = (1,)
    >>> t
    (1,)
    ```

#### dict

- 相当于 map

- 用{}表示

  ```
  d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
  ```

- 可以直接通过索引赋值 也可以通过索引获取值

  ```
  >>> d['Adam'] = 67
  >>> d['Adam']
  67
  ```

- 获取不存在的 key，会出现 error，所以可以通过 get(key)获取。
- 通过 key in dict 可以判断是否有 key（map 的 containsKey）
- 通过 pop(key)方法删除
- for x in a = for x in a.keys

#### set

- 相当于 set

- 也可以用{}表示

  - 如果是 a = {} 则表示的是 dirt

  ```
  a = {1, 2, 3}
  ```

- 通过 add 添加，remove、 pop 移除

- 可以通过 & | 来计算两个 set 的并集 交集

### 控制语句

#### 条件判断

- if x：

   statement

  只要 `x` 是非零数值、非空字符串、非空 list 等，就判断为 `True`，否则为 `False`。

- if else

- if elif

#### 模式匹配

- match （相当于 Java 的 switch）

- case statement：表示匹配条件

- case _:_表示匹配到其他任何情况（类似 default）

- 复杂匹配

  - 匹配多个值、匹配一定范围，并且把匹配后的值绑定到变量

  - ```python
    age = 15
    match age:
        case x if x < 10:
            print(f'< 10 years old: {x}')
        case 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18:
            print('11~18 years old.')
        case _:
            print('not sure.')
    ```

- 集合匹配

  - ```python
    args = ['gcc', 'hello.c', 'world.c']
    match args:
        # 如果仅出现gcc，报错:
        case ['gcc']:
            print('gcc: missing source file(s).')
        # 出现gcc，且至少指定了一个文件:
        case ['gcc', file1, *files]:
            print('gcc compile: ' + file1 + ', ' + ', '.join(files))
        case _:
            print('invalid command.')
    ```

#### 循环语句

##### for in

- for x in list

  - ```python
    names = ['Michael', 'Bob', 'Tracy']
    for name in names:
        print(name)
    ```

- for x in range（number

  - ```python
    sum = 0
    for x in range(101):
        sum = sum + x
    print(sum)
    ```

##### while

- while 条件：statement

  - ```python
    sum = 0
    n = 99
    while n > 0:
        sum = sum + n
        n = n - 2
    print(sum)
    ```

### 函数

#### 函数定义

- def 函数名（参数）：函数体

```python
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```

- return 语句结束并返回函数值，如果没有值则返回 None

- 空函数

  - 如果想定义一个什么事也不做的空函数，可以用 `pass` 语句：

    ```
    def nop():
        pass
    ```

- 返回多个值

  - 实际上是一个返回一个 tuple 类型，当只返回一个 tuple 时可以省略（）

  - 多个变量可以同时接收一个 tuple，按位置赋给对应的值

  - ```
    def move(x, y, step, angle=0):
        nx = x + step * math.cos(angle)
        ny = y - step * math.sin(angle)
        return nx, ny
        
    x, y = move(100, 100, 60, math.pi / 6)
    ```

#### 参数

#####  默认参数

1. 定义默认参数要牢记一点：默认参数必须指向不变对象！

```python
def power(x, n=2):
```

#####  可变参数

1. 定义可变参数和定义一个 list 或 tuple 参数相比，仅仅在参数前面加了一个 `*` 号。在函数内部，参数 `numbers` 接收到的是一个 tuple

   ```python
   def calc(*numbers):
       sum = 0
       for n in numbers:
           sum = sum + n * n
       return sum
   ```

##### 关键字参数

1. 而关键字参数允许你传入 0 个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个 dict

```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
    
>>> person('Michael', 30)
name: Michael age: 30 other: {}
>>> person('Bob', 35, city='Beijing')
name: Bob age: 35 other: {'city': 'Beijing'}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
```

##### 命名关键字参数

1. 如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收 `city` 和 `job` 作为关键字参数。这种方式定义的函数如下

```python
def person(name, age, *, city, job):
    print(name, age, city, job)
```

和关键字参数 `**kw` 不同，命名关键字参数需要一个特殊分隔符 `*`，`*` 后面的参数被视为命名关键字参数。

调用方式如下：

```bash
>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer
```

如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符 `*` 了：

```python
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

### 错误处理

#### 异常处理

##### 捕获

- try ··· except ··· finally 语句快（相当于 Java 的 try-catch）
- 如果没有错误发生，可以在 `except` 语句块后面加一个 `else`，当没有错误发生时，会自动执行 `else` 语句

```python
try:
    print('try...')
    r = 10 / int('2')
    print('result:', r)
except ValueError as e:
    print('ValueError:', e)
except ZeroDivisionError as e:
    print('ZeroDivisionError:', e)
else:
    print('no error!')
finally:
    print('finally...')
print('END')
```

- 所有的错误类型都继承自 `BaseException`，常见的错误类型和继承关系看这里 <https://docs.python.org/3/library/exceptions.html#exception-hierarchy>

##### 抛出错误

- 用 `raise` 语句抛出一个错误的实例
- `raise` 语句如果不带参数，就会把当前错误原样抛出。此外，在 `except` 中 `raise` 一个 Error，还可以把一种类型的错误转化成另一种类型

```python
class FooError(ValueError):
    pass

def foo(s):
    n = int(s)
    if n==0:
        raise FooError('invalid value: %s' % s)
    return 10 / n


def bar():
    try:
        foo('0')
    except ValueError as e:
        print('ValueError!')
        raise

try:
    10 / 0
except ZeroDivisionError:
    raise ValueError('input error!')
```

#### 调试

##### 断言

- assert statement, "error message" 当 statement 为 false 时，抛出 AssertionError

```python
def foo(s):
    n = int(s)
    assert n != 0, 'n is zero!'
    return 10 / n

def main():
    foo('0')
```

- 启动 Python 解释器时可以用 `-O` 参数来关闭 `assert`

```plain
python -O err.py
```

##### logging

- Python 内置的 `logging` 模块可以非常容易地记录错误信息

```python
def main():
    try:
        bar('0')
    except Exception as e:
        logging.exception(e)
```

- 它允许你指定记录信息的级别，有 `debug`，`info`，`warning`，`error` 等几个级别，当我们指定 `level=INFO` 时，`logging.debug` 就不起作用了。同理，指定 `level=WARNING` 后，`debug` 和 `info` 就不起作用了

```python
import logging
logging.basicConfig(level=logging.INFO)

s = '0'
n = int(s)
logging.info('n = %d' % n)
print(10 / n)
```

##### pdb

- 启动 Python 的调试器 pdb，让程序以单步方式运行，可以随时查看运行状态

```plain
# err.py
s = '0'
n = int(s)
print(10 / n)

$ python -m pdb err.py
```

- 以参数 `-m pdb` 启动后，pdb 定位到下一步要执行的代码 `-> s = '0'`。输入命令 `l` 来查看代码
- 输入命令 `n` 可以单步执行代码
- 任何时候都可以输入命令 `p 变量名` 来查看变量
- 输入命令 `q` 结束调试，退出程序

##### pdb.set_trace()

- 只需要 `import pdb`，然后，在可能出错的地方放一个 `pdb.set_trace()`，就可以设置一个断点

```python
import pdb

s = '0'
n = int(s)
pdb.set_trace() # 运行到这里会自动暂停
print(10 / n)
```

- 程序会自动在 `pdb.set_trace()` 暂停并进入 pdb 调试环境，可以用命令 `p` 查看变量，或者用命令 `c` 继续运行

#### 单元测试

// todo

#### 文档测试

// todo

### IO

#### 文件操作

##### 文件读写

- 使用 Python 内置的 `open()` 函数，传入文件名和标示符，标识符有 r 、w 、x 、a 、b 、t 、+模式可以选择，每种代表不同意思
- 调用 `read()` 会一次性读取文件的全部内容；可以调用 `read(size)` 方法，每次最多读取 size 个字节的内容；调用 `readline()` 可以每次读取一行内容，调用 `readlines()` 一次读取所有内容并按行返回 `list`。
- 可以反复调用 `write()` 来写入文件

```python
f = open('/Users/michael/test.txt', 'rw+')
f.read()
f.write('Hello, world!')
```

- 要读取非 UTF-8 编码的文本文件，需要给 `open()` 函数传入 `encoding` 参数，遇到有些编码不规范的文件，你可能会遇到 `UnicodeDecodeError，` open()`函数还接收一个` errors`参数，表示如果遇到编码错误后如何处理。最简单的方式是直接忽略

```python
>>> f = open('/Users/michael/gbk.txt', 'r', encoding='gbk', errors='ignore')
```

- 由于文件读写时都有可能产生 `IOError`，所以，为了保证无论是否出错都能正确地关闭文件，我们可以使用 `try ... finally` 来实现 ，但是每次都这么写实在太繁琐，所以，Python 引入了 `with` 语句来自动帮我们调用 `close()` 方法

```python
with open('/path/to/file', 'r') as f:
    print(f.read())
```

##### 文件夹操作

- Python 内置的 `os` 模块也可以直接调用操作系统提供的接口函数。

```python
>>> os.name # 操作系统类型
'posix'

>>> os.environ # 操作系统中定义的环境变量
environ({'VERSIONER_PYTHON_PREFER_32_BIT': 'no', 'TERM_PROGRAM_VERSION': '326', 'LOGNAME': 'michael', 'USER': 'michael', 'PATH': '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/opt/X11/bin:/usr/local/mysql/bin', ...})

>>> os.environ.get('PATH') # 获取某个环境变量的值
'/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/opt/X11/bin:/usr/local/mysql/bin'
>>> os.environ.get('x', 'default')
'default'

# 查看当前目录的绝对路径:
>>> os.path.abspath('.')
'/Users/michael'
# 在某个目录下创建一个新目录，首先把新目录的完整路径表示出来:
>>> os.path.join('/Users/michael', 'testdir')
'/Users/michael/testdir'
# 然后创建一个目录:
>>> os.mkdir('/Users/michael/testdir')
# 删掉一个目录:
>>> os.rmdir('/Users/michael/testdir')

>>> os.path.split('/Users/michael/testdir/file.txt') # 拆分路径
('/Users/michael/testdir', 'file.txt')

>>> os.path.splitext('/path/to/file.txt') # 得到文件扩展名
('/path/to/file', '.txt')

# 对文件重命名:
>>> os.rename('test.txt', 'test.py')
# 删掉文件:
>>> os.remove('test.py')
```

- `shutil` 模块中找到很多实用函数，它们可以看做是 `os` 模块的补充，比如 `copyfile()` 的函数用来复制文件

#### StringIO 和 BytesIO

##### StringIO

- 要把 `str` 写入 `StringIO`，我们需要先创建一个 `StringIO`，然后，像文件一样写入即可，`getvalue()` 方法用于获得写入后的 `str`。

```plain
>>> from io import StringIO
>>> f = StringIO()
>>> f.write('hello')
5
>>> f.write(' ')
1
>>> f.write('world!')
6
>>> print(f.getvalue())
hello world!
```

##### BytesIO

- 如果要操作二进制数据，就需要使用 `BytesIO`

```plain
>>> from io import BytesIO
>>> f = BytesIO()
>>> f.write('中文'.encode('utf-8'))
6
>>> print(f.getvalue())
b'\xe4\xb8\xad\xe6\x96\x87'
```

- tell 方法获取当前流读取指针的位置
- seek 方法，用于移动文件读写指针到指定位置, 有两个参数，第一个 offset: 偏移量，需要向前或向后的字节数，正为向后，负为向前；第二个 whence: 可选值，默认为 0，表示文件开头，1 表示相对于当前的位置，2 表示文件末尾。用 seek 方法时，需注意，如果你打开的文件没有用二进制的方式打开，则 offset 无法使用负值

#### 序列化

- Python 提供了 `pickle` 模块来实现序列化
- `pickle.dumps()` 方法把任意对象序列化成一个 `bytes`，然后，就可以把这个 `bytes` 写入文件。或者用另一个方法 `pickle.dump()` 直接把对象序列化后写入一个 file-like Object

```python
>>> import pickle
>>> d = dict(name='Bob', age=20, score=88)
>>> pickle.dumps(d)
b'\x80\x03}q\x00(X\x03\x00\x00\x00ageq\x01K\x14X\x05\x00\x00\x00scoreq\x02KXX\x04\x00\x00\x00nameq\x03X\x03\x00\x00\x00Bobq\x04u.'

>>> f = open('dump.txt', 'wb')
>>> pickle.dump(d, f)
>>> f.close()
```

- 要把对象从磁盘读到内存时，可以先把内容读到一个 `bytes`，然后用 `pickle.loads()` 方法反序列化出对象，也可以直接用 `pickle.load()` 方法从一个 `file-like Object` 中直接反序列化出对象。我们打开另一个 Python 命令行来反序列化刚才保存的对象：

```plain
>>> f = open('dump.txt', 'rb')
>>> d = pickle.load(f)
>>> f.close()
>>> d
{'age': 20, 'score': 88, 'name': 'Bob'}
```

##### JSON

- Python 内置的 `json` 模块提供了非常完善的 Python 对象到 JSON 格式的转换，dumps()`方法返回一个` str `，内容就是标准的JSON。类似的，` dump()`方法可以直接把JSON写入一个` file-like Object

```python
>>> import json
>>> d = dict(name='Bob', age=20, score=88)
>>> json.dumps(d)
'{"age": 20, "score": 88, "name": "Bob"}'

>>> json_str = '{"age": 20, "score": 88, "name": "Bob"}'
>>> json.loads(json_str)
{'age': 20, 'score': 88, 'name': 'Bob'}
```

- 要把 JSON 反序列化为 Python 对象，用 `loads()` 或者对应的 `load()` 方法，前者把 JSON 的字符串反序列化，后者从 `file-like Object` 中读取字符串并反序列化

```plain
>>> json_str = '{"age": 20, "score": 88, "name": "Bob"}'
>>> json.loads(json_str)
{'age': 20, 'score': 88, 'name': 'Bob'}
```

- Python 的 `dict` 对象可以直接序列化为 JSON 的 `{}`，不过，很多时候，我们更喜欢用 `class` 表示对象
- `dumps()` 方法可选参数 `default` 就是把任意一个对象变成一个可序列为 JSON 的对象, 通常 `class` 的实例都有一个 `__dict__` 属性，它就是一个 `dict`，用来存储实例变量。也有少数例外，比如定义了 `__slots__` 的 class

```python
def student2dict(std):
    return {
        'name': std.name,
        'age': std.age,
        'score': std.score
    }
    
>>> print(json.dumps(s, default=student2dict))
{"age": 20, "name": "Bob", "score": 88}

print(json.dumps(s, default=lambda obj: obj.__dict__))
```

- 把 JSON 反序列化为一个 `Student` 对象实例，`loads()` 方法首先转换出一个 `dict` 对象，然后，我们传入的 `object_hook` 函数负责把 `dict` 转换为 `Student` 实例

```python
def dict2student(d):
    return Student(d['name'], d['age'], d['score'])

>>> json_str = '{"age": 20, "score": 88, "name": "Bob"}'
>>> print(json.loads(json_str, object_hook=dict2student))
<__main__.Student object at 0x10cd3c190>
```

## 高级

### 高级特性

#### 切片

- 取一个 list、tuple、str 的部分元素

- [s:e:i] s-开始位置 e-结束位置 i-间隔

  ``` python
  L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
  >>> L[0:3]
  ['Michael', 'Sarah', 'Tracy']
  >>> L[-2:]
  ['Bob', 'Jack']
  
  L = list(range(100))
  >>> L[:10:2]
  [0, 2, 4, 6, 8]
  ```


#### 列表生成器

- 写列表生成式时，把要生成的元素 `x * x` 放到前面，后面跟 `for` 循环，就可以把 list 创建出来
- `for` 循环其实可以同时使用两个甚至多个变量，比如 `dict` 的 `items()` 可以同时迭代 key 和 value：

```python
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> for k, v in d.items():
    	print(k, '=', v)
```

- 在一个列表生成式中，`for` 前面的 `if ... else` 是表达式，必须要 else，而 `for` 后面的 `if` 是过滤条件，不能带 `else`。

```python
>>> [x if x % 2 == 0 else -x for x in range(1, 11)]
[-1, 2, -3, 4, -5, 6, -7, 8, -9, 10]
```

#### 生成器

- 一边循环一边计算的机制，称为生成器：generator。

- 只要把一个列表生成式的 `[]` 改成 `()`，就创建了一个 generator：
- 可以通过 `next()` 函数获得 generator 的下一个返回值，每次调用 `next(g)`，就计算出 `g` 的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出 `StopIteration` 的错误。
- 可以用 for 循环迭代生成器

```plain
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>

>>> next(g)
0
```

- 可以用函数来实现
- 如果一个函数定义中包含 `yield` 关键字，那么这个函数就不再是一个普通函数，而是一个 generator 函数，调用一个 generator 函数将返回一个 generator：
- 普通函数是顺序执行，遇到 `return` 语句或者最后一行函数语句就返回。而变成 generator 的函数，在每次调用 `next()` 的时候执行，遇到 `yield` 语句返回，再次执行时从上次返回的 `yield` 语句处继续执行。
- 在执行过程中，遇到 `yield` 就中断，下次又继续执行。

```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'

>>> for n in fib(6):
...     print(n)
1
1
2
3
5
8
```

#### 迭代器

- 可以直接作用于 `for` 循环的对象统称为可迭代对象：`Iterable`
- 可以使用 `isinstance()` 判断一个对象是否是 `Iterable` 对象
- 可以被 `next()` 函数调用并不断返回下一个值的对象称为迭代器：`Iterator`
- 可以使用 `isinstance()` 判断一个对象是否是 `Iterator` 对象

### 函数式编程

#### 高阶函数

##### map

- `map()` 函数接收两个参数，一个是函数，一个是 `Iterable`，`map` 将传入的函数依次作用到序列的每个元素，并把结果作为新的 `Iterator` 返回

```plain
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

##### reduce

- `reduce` 把一个函数作用在一个序列 `[x1, x2, x3, ...]` 上，这个函数必须接收两个参数，`reduce` 把结果继续和序列的下一个元素做累积计算

```plain
>>> from functools import reduce
>>> def add(x, y):
...     return x + y
...
>>> reduce(add, [1, 3, 5, 7, 9])
25
```

##### filter

- `filter()` 也接收一个函数和一个序列，把传入的函数依次作用于每个元素，然后根据返回值是 `True` 还是 `False` 决定保留还是丢弃该元素

  ```python
  def is_odd(n):
      return n % 2 == 1
  
  list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
  # 结果: [1, 5, 9, 15]
  ```

##### sorted

- Python 内置的 `sorted()` 函数就可以对 list 进行排序：

- `sorted()` 函数也是一个高阶函数，它还可以接收一个 `key` 函数来实现自定义的排序

```plain
>>> sorted([36, 5, -12, 9, -21])
[-21, -12, 5, 9, 36]

>>> sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]
```

#### 返回函数

- 高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回。

```python
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum

>>> f = lazy_sum(1, 3, 5, 7, 9)
>>> f
<function lazy_sum.<locals>.sum at 0x101c6ed90>
```

- 相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）

> [!NOTE]
>
> 返回闭包时牢记一点：返回函数不要引用任何循环变量，或者后续会发生变化的变量。

- 如果一定要引用循环变量怎么办？方法是再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变

##### nonlocal

- 使用闭包，就是内层函数引用了外层函数的局部变量。如果只是读外层变量的值，我们会发现返回的闭包函数调用一切正常：

- 但是，如果对外层变量赋值，由于 Python 解释器会把 `x` 当作函数 `fn()` 的局部变量，它会报错：

- 使用闭包时，对外层变量赋值前，需要先使用 nonlocal 声明该变量不是当前函数的局部变量。

```python
def inc():
    x = 0
    def fn():
        nonlocal x
        x = x + 1
        return x
    return fn

f = inc()
print(f()) # 1
print(f()) # 2
```

#### 匿名函数

匿名函数 `lambda x: x * x` 实际上就是：

```python
def f(x):
    return x * x
```

- 关键字 `lambda` 表示匿名函数，冒号前面的 `x` 表示函数参数。
- 匿名函数有个限制，就是只能有一个表达式，不用写 `return`，返回值就是该表达式的结果
- 用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量。

#### 装饰器

- 函数对象有一个 `__name__` 属性（注意：是前后各两个下划线），可以拿到函数的名字
- 在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）
- 本质上，decorator 就是一个返回函数的高阶函数

```python
def now():
    print('2024-6-1')
    
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper

@log
def now():
    print('2024-6-1')
    
>>> now()
call now():
2024-6-1
```

- 调用 `now()` 函数，不仅会运行 `now()` 函数本身，还会在运行 `now()` 函数前打印一行日志
- 由于 `log()` 是一个 decorator，返回一个函数，所以，原来的 `now()` 函数仍然存在，只是现在同名的 `now` 变量指向了新的函数，于是调用 `now()` 将执行新函数，即在 `log()` 函数中返回的 `wrapper()` 函数
- 如果 decorator 本身需要传入参数，那就需要编写一个返回 decorator 的高阶函数，写出来会更复杂。

```python
def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```

- 函数也是对象，它有 `__name__` 等属性，但你去看经过 decorator 装饰之后的函数，它们的 `__name__` 已经从原来的 `'now'` 变成了 `'wrapper'`

- 需要把原始函数的 `__name__` 等属性复制到 `wrapper()` 函数中，否则，有些依赖函数签名的代码执行就会出错

```python
def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```

#### 偏函数

- `functools.partial` 就是帮助我们创建一个偏函数的
- 把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单

```plain
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```

- 实际上固定了 int()函数的关键字参数 `base`

- ```python
  int2('10010') 
  相当于：
  kw = { 'base': 2 }
  int('10010', **kw)
  ```

### 进程和线程

//todo



## 面向对象

### 类和实例

- 定义类是通过 `class` 关键字

```python
class Student(object):
    pass
```

- 类名通常是大写开头的单词，紧接着是 `(object)`，表示该类是从哪个类继承下来的，如果没有合适的继承类，就使用 `object` 类，这是所有类最终都会继承的类。

#### 构造方法

`__init__`

`__init__` 方法的第一个参数永远是 `self`，表示创建的实例本身，因此，在 `__init__` 方法内部，就可以把各种属性绑定到 `self`，因为 `self` 就指向创建的实例本身, 但 `self` 不需要传，Python 解释器自己会把实例变量传进去.

#### 数据封装

- 如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线 `__`，在 Python 中，实例的变量名如果以 `__` 开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问
- 变量名类似 `__xxx__` 的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是 private 变量
- 能直接访问 `__name` 是因为 Python 解释器对外把 `__name` 变量改成了 `_Student__name`，所以，仍然可以通过 `_Student__name` 来访问 `__name` 变量, 但是不同版本的 Python 解释器可能会把 `__name` 改成不同的变量名。

#### 获取对象信息

- 使用 `dir()` 函数获得一个对象的所有属性和方法

```python
>>> dir('ABC')
['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
```

- len()函数试图获取一个对象的长度，在 `len()` 函数内部，它自动去调用该对象的 `__len__()` 方法

```plain
>>> len('ABC')
3
>>> 'ABC'.__len__()
3
```

自己写的类，如果也想用 `len(myObj)` 的话，就自己写一个 `__len__()` 方法

```python
>>> class MyDog(object):
...     def __len__(self):
...         return 100
```

- `lower()` 返回小写的字符串

```Python
>>> 'ABC'.lower()
'abc'
```

- `getattr()`、`setattr()` 以及 `hasattr()`，我们可以直接操作一个对象的状态

```python
>>> hasattr(obj, 'x') # 有属性'x'吗？
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> getattr(obj, 'y') # 获取属性'y'
```

如果试图获取不存在的属性，会抛出 AttributeError 的错误，可以传入一个 default 参数，如果属性不存在，就返回默认值：

```python
>>> getattr(obj, 'z', 404) # 获取属性'z'，如果不存在，返回默认值404
404
```

也可以获得对象的方法：

```python
>>> hasattr(obj, 'power') # 有属性'power'吗？
True
>>> getattr(obj, 'power') # 获取属性'power'
<bound method MyObject.power of <__main__.MyObject object at 0x10077a6a0>>
>>> fn = getattr(obj, 'power') # 获取属性'power'并赋值到变量fn
>>> fn # fn指向obj.power
<bound method MyObject.power of <__main__.MyObject object at 0x10077a6a0>>
>>> fn() # 调用fn()与调用obj.power()是一样的
81
```

### 高级特性

#### 多继承

- Python 允许使用多重继承

```python
class Dog(Mammal, Runnable):
    pass

# Dog继承了Mammal和Runnableliang'g
```

#### 使用\_slots_

- 在定义 `class` 的时候，定义一个特殊的 `__slots__` 变量，来限制该 `class` 实例能添加的属性

```python
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```

- 使用 `__slots__` 要注意，`__slots__` 定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。除非在子类中也定义 `__slots__`，这样，子类实例允许定义的属性就是自身的 `__slots__` 加上父类的 `__slots__`

#### 使用@property

- Python 内置的 `@property` 装饰器就是负责把一个方法变成属性调用的

```python
class Student(object):
    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, value):
        self._score = value
        
>>> s = Student()
>>> s.score = 60 # OK，实际转化为s.score(60)
>>> s.score # OK，实际转化为s.score()
60
```

- 属性方法名和实例变量重名，会造成递归调用，导致栈溢出报错！

#### 枚举类

- 如果需要更精确地控制枚举类型，可以从 `Enum` 派生出自定义类，`@unique` 装饰器可以帮助我们检查保证没有重复值

```python
from enum import Enum, unique

@unique
class Weekday(Enum):
    Sun = 0 # Sun的value被设定为0
    Mon = 1
    Tue = 2
    Wed = 3
    Thu = 4
    Fri = 5
    Sat = 6
    
>>> day1 = Weekday.Mon
>>> print(day1)
Weekday.Mon
>>> print(Weekday.Tue)
Weekday.Tue
>>> print(Weekday['Tue'])
Weekday.Tue
>>> print(Weekday.Tue.value)
2
>>> print(day1 == Weekday.Mon)
True
>>> print(day1 == Weekday.Tue)
False
>>> print(Weekday(1))
Weekday.Mon
>>> print(day1 == Weekday(1))
True
>>> Weekday(7)
Traceback (most recent call last):
  ...
ValueError: 7 is not a valid Weekday
>>> for name, member in Weekday.__members__.items():
...     print(name, '=>', member)
...
Sun => Weekday.Sun
Mon => Weekday.Mon
Tue => Weekday.Tue
Wed => Weekday.Wed
Thu => Weekday.Thu
Fri => Weekday.Fri
Sat => Weekday.Sat
```

#### 定制类

##### \_str_& \__repr__()

- `__str__()` 返回用户看到的字符串，而 `__repr__()` 返回程序开发者看到的字符串

```python
class Student(object):
    def __init__(self, name):
        self.name = name
    def __str__(self):
        return 'Student object (name=%s)' % self.name
    __repr__ = __str__
    
>>> print(Student('Michael'))
Student object (name: Michael)
```

##### \__iter__

- 如果一个类想被用于 `for ... in` 循环，类似 list 或 tuple 那样，就必须实现一个 `__iter__()` 方法，该方法返回一个迭代对象，然后，Python 的 for 循环就会不断调用该迭代对象的 `__next__()` 方法拿到循环的下一个值，直到遇到 `StopIteration` 错误时退出循环

```python
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1 # 初始化两个计数器a，b

    def __iter__(self):
        return self # 实例本身就是迭代对象，故返回自己

    def __next__(self):
        self.a, self.b = self.b, self.a + self.b # 计算下一个值
        if self.a > 100000: # 退出循环的条件
            raise StopIteration()
        return self.a # 返回下一个值
    
>>> for n in Fib():
...     print(n)
...
1
1
2
3
5
...
46368
75025
```

##### \__getitem__

- 表现得像 list 那样按照下标取出元素，需要实现 `__getitem__()` 方法

```python
class Fib(object):
    def __getitem__(self, n):
        if isinstance(n, int): # n是索引
            a, b = 1, 1
            for x in range(n):
                a, b = b, a + b
            return a
        if isinstance(n, slice): # n是切片
            start = n.start
            stop = n.stop
            if start is None:
                start = 0
            a, b = 1, 1
            L = []
            for x in range(stop):
                if x >= start:
                    L.append(a)
                a, b = b, a + b
            return L
    
>>> f = Fib()
>>> f[0]
1
>>> f[1]
1
>>> f[2]
2
>>> f[3]
3
>>> f[10]
89
>>> f[100]
573147844013817084101
>>> f = Fib()
>>> f[0:5]
[1, 1, 2, 3, 5]
>>> f[:10]
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

##### \__getattr__

- 写一个 `__getattr__()` 方法，动态返回一个属性, 当调用不存在的属性时，比如 `score`，Python 解释器会试图调用 `__getattr__(self, 'score')` 来尝试获得属性

```python
class Student(object):
    def __init__(self):
        self.name = 'Michael'

    def __getattr__(self, attr):
        if attr=='score':
            return 99
>>> s = Student()
>>> s.name
'Michael'
>>> s.score
99
```

- 返回函数也是完全可以的

```python
class Student(object):
    def __getattr__(self, attr):
        if attr=='age':
            return lambda: 25
#只是调用方式要变为       
>>> s.age()
25
```

##### \__call__

- 只需要定义一个 `__call__()` 方法，就可以直接对实例进行调用

```python
class Student(object):
    def __init__(self, name):
        self.name = name

    def __call__(self):
        print('My name is %s.' % self.name)
        
>>> s = Student('Michael')
>>> s() # self参数不要传入
My name is Michael.
```

- 我们需要判断一个对象是否能被调用，能被调用的对象就是一个 `Callable` 对象, 通过 `callable()` 函数，我们就可以判断一个对象是否是“可调用”对象。

## 常用库

### 内建库

#### 正则表达式

//todo

#### datetime

是 Python 处理日期和时间的标准库。

`datetime` 是模块，`datetime` 模块还包含一个 `datetime` 类，通过 `from datetime import datetime` 导入的才是 `datetime` 这个类

##### 获取当前日期和时间

- `datetime.now()` 返回当前日期和时间，其类型是 `datetime`。

##### 获取指定日期和时间

- 要指定某个日期和时间，我们直接用参数构造一个 `datetime`

```plain
>>> dt = datetime(2015, 4, 19, 12, 20) # 用指定日期时间创建datetime
>>> print(dt)
2015-04-19 12:20:00
```

##### datetime 转换 timestamp

- Python 的 timestamp 是一个浮点数，整数位表示秒

- timestamp 是一个浮点数，它没有时区的概念，而 datetime 是有时区的。上述转换是在 timestamp 和本地时间做转换

```Python
dt.timestamp() #datetime转timestamp
datetime.fromtimestamp(t) #timestamp转datetime
```

##### str 转换 datetime

- 字符串 `'%Y-%m-%d %H:%M:%S'` 规定了日期和时间部分的格式。详细的说明请参考 [Python 文档](https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior)。

```plain
datetime.strptime('2015-6-1 18:19:59', '%Y-%m-%d %H:%M:%S') str转datetime
obj.strftime('%a, %b %d %H:%M') datetime转str
```

##### timedelta

- 通过 timedelta 类实现+ - 时间和日期

- 一个 `datetime` 类型有一个时区属性 `tzinfo`，但是默认为 `None`，所以无法区分这个 `datetime` 到底是哪个时区，除非强行给 `datetime` 设置一个时区

```plain
tz_utc_8 = timezone(timedelta(hours=8))
obj.replace(tzinfo=tz_utc_8) #替换时区
```

- 通过 timedelta 进行时区转换

#### Collections

- Python 内建的一个集合模块，提供了许多有用的集合类

#### argparse

- 使用 [argparse](https://docs.python.org/3/library/argparse.html) 解析参数，只需定义好参数类型，就可以获得有效的参数输入，能大大简化获取命令行参数的工作。

#### base64

- Python 内置的 `base64` 可以直接进行 base64 的编解码

#### struct

- Python 提供了一个 `struct` 模块来解决 `bytes` 和其他二进制数据类型的转换

#### hashlib

- Python 的 `hashlib` 提供了常见的哈希算法，如 MD5，SHA1 等等

#### hmac

- Python 自带的 hmac 模块实现了标准的 Hmac 算法

#### itertools

- Python 的内建模块 `itertools` 提供了非常有用的用于操作迭代对象的函数

#### contextlib

- Python 的 contextlib 模块给我们提供了更方便的方式来实现一个自定义的上下文管理器
- [【Python 学习笔记】with 语句与上下文管理器 - 恋曲 1990 - 博客园](https://www.cnblogs.com/nnnkkk/p/4309275.html)

#### XML & HTMLParser

- 操作 XML 有两种方法：DOM 和 SAX。DOM 会把整个 XML 读入内存，解析为树，因此占用内存大，解析慢，优点是可以任意遍历树的节点。SAX 是流模式，边读边解析，占用内存小，解析快，缺点是我们需要自己处理事件。
- HTML 本质上是 XML 的子集，但是 HTML 的语法没有 XML 那么严格，所以不能用标准的 DOM 或 SAX 来解析 HTML。Python 提供了 `HTMLParser` 来非常方便地解析 HTML.

#### venv

- `venv` 为应用提供了隔离的 Python 运行环境，解决了不同应用间安装多版本的冲突问题

#### Tkinter

- Tk 是一个图形库，支持多个操作系统，使用 Tcl 语言开发；

- Tk 会调用操作系统提供的本地 GUI 接口，完成最终的 GUI



### 三方库

- 所有的第三方模块都会在 [PyPI - the Python Package Index](https://pypi.python.org/) 上注册

#### Pillow

- PIL：Python Imaging Library，已经是 Python 平台事实上的图像处理标准库了。在 PIL 的基础上创建了兼容的版本，名字叫 [Pillow](https://github.com/python-pillow/Pillow)，支持最新 Python 3.x，又加入了许多新特性
- 官方文档 [https://pillow.readthedocs.org/](https://pillow.readthedocs.org/)

#### requests & httpx

- 用于访问网络资源 处理 URL 资源相对内置的 `urllib` 模块方便
- `httpx` 是一个现代、高性能的 Python HTTP 客户端，支持 **同步 & 异步** 请求，比 `requests` 更强大（支持 HTTP/2、WebSocket 等）

#### chardet

- 对于未知编码的 `bytes`, 用它来检测编码，简单易用。

#### psutil

- 顾名思义，psutil = process and system utilities，它不仅可以通过一两行代码实现系统监控

## module

- 通过 import module 来导入一个模块
- 通过 from module import xxx 来导入某个模块中的某一个类

### 作用域

- 在一个模块中，我们可能会定义很多函数和变量，但有的函数和变量我们希望给别人使用，有的函数和变量我们希望仅仅在模块内部使用。在 Python 中，是通过 `_` 前缀来实现的。
- 类似 `__xxx__` 这样的变量是特殊变量，可以被直接引用，但是有特殊用途
- 类似 `_xxx` 和 `__xxx` 这样的函数或变量就是非公开的（private），不应该被直接引用.
