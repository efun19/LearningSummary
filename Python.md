# Python



> [!IMPORTANT]
>
> - Python大小写敏感
> - // 地板除 / 精确除
> - Python通过缩进来控制代码快
> - 赋值语句 a, b = b, a + b相当于： a = b，b=a+b



## 命令行

- Python -i 可以交互式执行命令

### pip

- pip list 查看所有安装的三方库
- pip show package 看出某个三方库信息

## 基本函数

- int()函数用于str转型int

```python
int("1")
```

- float()函数用于str转型float

```python
float("1.1")
```

- isinstance()函数用于判断类型

```python
isinstance(x, A_tuple)#用于判断x是否属于A_tuple类型
```

## 基础

### 输入输出

- print() 输出

- input() 输入

  - 传入String可以作为提示语

    ```
    input('tip：')
    ```

### 数据类型

#### 整型、浮点型

- 数字之间可以用_分隔用于分辨数字过长

#### 布尔值

- 可以直接True 、False表示
- and 就是 &&
- or 就是 ||
- not 就是 !

#### 空值

- none表示

#### 字符串

- “ ”，' '都能表示字符串

- r' '表示内部的都不转义 （**结束的‘’ ' 前的\不能出现奇数个**）

- '" "'可以多行使用

- `ord()`函数获取字符的整数

- `chr()`函数把编码转换为对应的字符

- 与字符数组转换

  - 字符数组 b'xxx'表示

  - 在`bytes`中，无法显示为ASCII字符的字节，用`\x##`显示。

  - String - bytes

    - "xxx".encode(编码方式)

    - ```
      >>> 'ABC'.encode('ascii')
      b'ABC'
      >>> '中文'.encode('utf-8')
      b'\xe4\xb8\xad\xe6\x96\x87'
      ```

  -  bytes - String 

    - b'xxx'.decode(编码方式)

    - ```
      >>> b'ABC'.decode('ascii')
      'ABC'
      >>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
      '中文'
      ```

    - 可以传入`errors='ignore'`忽略错误的

    - ```
      >>> b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore')
      '中'
      ```

- len()函数计算长度 len(xxx)

  - String算的是字符的数量
  - bytes算的是字节的数量

- 格式化

  - 采用的格式化方式和C语言

  - 占位符 % 

    - 有几个`%?`占位符，后面就跟几个变量或者值，顺序要对应好。如果只有一个`%?`，括号可以省略

    - `%`是一个普通字符需要转义，用`%%`来表示一个`%`

    - ```
      >>> 'Age: %s. Gender: %s' % (25, True)
      'Age: 25. Gender: True'
      >>> 'growth rate: %d %%' % 7
      'growth rate: 7 %'
      ```

  - format()方法

    - 它会用传入的参数依次替换字符串内的占位符`{0}`、`{1}`……

    - ```
      >>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
      'Hello, 小明, 成绩提升了 17.1%'
      ```

  - f-string

    - 字符串如果包含`{xxx}`，就会以对应的变量替换

    - ```
      >>> r = 2.5
      >>> s = 3.14 * r ** 2
      >>> print(f'The area of a circle with radius {r} is {s:.2f}')
      The area of a circle with radius 2.5 is 19.62	
      ```

- 常用函数

  - "x".join(list)

    - 返回str 讲list中的str元素通过x间隔分开

    - ```python
      args = ['gcc', 'hello.c', 'world.c',"ddd","123"]
      print(":".join(args))
      #gcc compile: hello.c, world.c, ddd, 123
      ```

### 容器

#### list

- 有序可变集合

- 类似于java数组的定义方式

  - ```python
    classmates = ['Michael', 'Bob', 'Tracy']
    ```

- 用索引来访问list中每一个位置的元素

  - ```python
    classmates[0]
    ```

  - 用-1可以获取倒数第1个元素，以此类推

- 常用方法

  - list.append(obj) 尾部添加 (类似add)
  - list.insert(index，obj) 插入（类似set）
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

- 只有1个元素的tuple定义时必须加一个逗号`,`

  - ```python
    >>> t = (1,)
    >>> t
    (1,)
    ```

#### dict

- 相当于map

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

- 获取不存在的key，会出现error，所以可以通过get(key)获取。
- 通过 key in dict 可以判断是否有key（map的containsKey）
- 通过pop(key)方法删除
- for x in a = for x in a.keys

#### set

- 相当于set

- 也可以用{}表示

  - 如果是 a = {} 则表示的是dirt

  ```
  a = {1, 2, 3}
  ```

- 通过add 添加，remove、 pop移除

- 可以通过 & | 来计算两个set的并集 交集

### 控制语句

#### 条件判断

- if x：

  ​	statement

  只要`x`是非零数值、非空字符串、非空list等，就判断为`True`，否则为`False`。

- if else

- if elif

#### 模式匹配

- match （相当于Java的switch）

- case statement：表示匹配条件

- case _: _表示匹配到其他任何情况（类似default）

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

- return语句结束并返回函数值，如果没有值则返回None

- 空函数

  - 如果想定义一个什么事也不做的空函数，可以用`pass`语句：

    ```
    def nop():
        pass
    ```

- 返回多个值

  - 实际上是一个返回一个tuple类型，当只返回一个tuple时可以省略（）

  - 多个变量可以同时接收一个tuple，按位置赋给对应的值

  - ```
    def move(x, y, step, angle=0):
        nx = x + step * math.cos(angle)
        ny = y - step * math.sin(angle)
        return nx, ny
        
    x, y = move(100, 100, 60, math.pi / 6)
    ```

#### 参数

##### 	默认参数

1. 定义默认参数要牢记一点：默认参数必须指向不变对象！

```python
def power(x, n=2):
```

##### 	可变参数

1. 定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个`*`号。在函数内部，参数`numbers`接收到的是一个tuple

   ```python
   def calc(*numbers):
       sum = 0
       for n in numbers:
           sum = sum + n * n
       return sum
   ```

##### 关键字参数

1. 而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict

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

1. 如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收`city`和`job`作为关键字参数。这种方式定义的函数如下

```python
def person(name, age, *, city, job):
    print(name, age, city, job)
```

和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。

调用方式如下：

```bash
>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer
```

如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符`*`了：

```python
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

## 高级

### 高级特性

#### 切片

- 取一个list、tuple、str的部分元素

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

- 写列表生成式时，把要生成的元素`x * x`放到前面，后面跟`for`循环，就可以把list创建出来
- `for`循环其实可以同时使用两个甚至多个变量，比如`dict`的`items()`可以同时迭代key和value：

```python
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> for k, v in d.items():
    	print(k, '=', v)
```

- 在一个列表生成式中，`for`前面的`if ... else`是表达式，必须要else，而`for`后面的`if`是过滤条件，不能带`else`。

```python
>>> [x if x % 2 == 0 else -x for x in range(1, 11)]
[-1, 2, -3, 4, -5, 6, -7, 8, -9, 10]
```

#### 生成器

- 一边循环一边计算的机制，称为生成器：generator。

- 只要把一个列表生成式的`[]`改成`()`，就创建了一个generator：
- 可以通过`next()`函数获得generator的下一个返回值，每次调用`next(g)`，就计算出`g`的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出`StopIteration`的错误。
- 可以用for循环迭代生成器

```plain
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>

>>> next(g)
0
```

- 可以用函数来实现
- 如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator函数，调用一个generator函数将返回一个generator：
- 普通函数是顺序执行，遇到`return`语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行。
- 在执行过程中，遇到`yield`就中断，下次又继续执行。

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

- 可以直接作用于`for`循环的对象统称为可迭代对象：`Iterable`
- 可以使用`isinstance()`判断一个对象是否是`Iterable`对象

- 可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`
- 可以使用`isinstance()`判断一个对象是否是`Iterator`对象