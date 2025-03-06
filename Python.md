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

### 函数式编程

#### 高阶函数

##### map

- `map()`函数接收两个参数，一个是函数，一个是`Iterable`，`map`将传入的函数依次作用到序列的每个元素，并把结果作为新的`Iterator`返回

```plain
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

##### reduce

- `reduce`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce`把结果继续和序列的下一个元素做累积计算

```plain
>>> from functools import reduce
>>> def add(x, y):
...     return x + y
...
>>> reduce(add, [1, 3, 5, 7, 9])
25
```

##### filter

- `filter()`也接收一个函数和一个序列，把传入的函数依次作用于每个元素，然后根据返回值是`True`还是`False`决定保留还是丢弃该元素

  ```python
  def is_odd(n):
      return n % 2 == 1
  
  list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
  # 结果: [1, 5, 9, 15]
  ```

##### sorted

- Python内置的`sorted()`函数就可以对list进行排序：

- `sorted()`函数也是一个高阶函数，它还可以接收一个`key`函数来实现自定义的排序

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

- 但是，如果对外层变量赋值，由于Python解释器会把`x`当作函数`fn()`的局部变量，它会报错：

- 使用闭包时，对外层变量赋值前，需要先使用nonlocal声明该变量不是当前函数的局部变量。

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

匿名函数`lambda x: x * x`实际上就是：

```python
def f(x):
    return x * x
```

- 关键字`lambda`表示匿名函数，冒号前面的`x`表示函数参数。
- 匿名函数有个限制，就是只能有一个表达式，不用写`return`，返回值就是该表达式的结果
- 用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量。

#### 装饰器

- 函数对象有一个`__name__`属性（注意：是前后各两个下划线），可以拿到函数的名字
- 在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）
- 本质上，decorator就是一个返回函数的高阶函数

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

- 调用`now()`函数，不仅会运行`now()`函数本身，还会在运行`now()`函数前打印一行日志
- 由于`log()`是一个decorator，返回一个函数，所以，原来的`now()`函数仍然存在，只是现在同名的`now`变量指向了新的函数，于是调用`now()`将执行新函数，即在`log()`函数中返回的`wrapper()`函数
- 如果decorator本身需要传入参数，那就需要编写一个返回decorator的高阶函数，写出来会更复杂。

```python
def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```

- 函数也是对象，它有`__name__`等属性，但你去看经过decorator装饰之后的函数，它们的`__name__`已经从原来的`'now'`变成了`'wrapper'`

- 需要把原始函数的`__name__`等属性复制到`wrapper()`函数中，否则，有些依赖函数签名的代码执行就会出错

```python
def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```

#### 偏函数

- `functools.partial`就是帮助我们创建一个偏函数的
- 把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单

```plain
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```

- 实际上固定了int()函数的关键字参数`base`

- ```python
  int2('10010') 
  相当于：
  kw = { 'base': 2 }
  int('10010', **kw)
  ```



## 面向对象

### 类和实例

- 定义类是通过`class`关键字

```python
class Student(object):
    pass
```

- 类名通常是大写开头的单词，紧接着是`(object)`，表示该类是从哪个类继承下来的，如果没有合适的继承类，就使用`object`类，这是所有类最终都会继承的类。

#### 构造方法

`__init__`

`__init__`方法的第一个参数永远是`self`，表示创建的实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身,但`self`不需要传，Python解释器自己会把实例变量传进去.

#### 数据封装

- 如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线`__`，在Python中，实例的变量名如果以`__`开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问
- 变量名类似`__xxx__`的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量
- 能直接访问`__name`是因为Python解释器对外把`__name`变量改成了`_Student__name`，所以，仍然可以通过`_Student__name`来访问`__name`变量,但是不同版本的Python解释器可能会把`__name`改成不同的变量名。

#### 获取对象信息

- 使用`dir()`函数获得一个对象的所有属性和方法

```python
>>> dir('ABC')
['__add__', '__class__',..., '__subclasshook__', 'capitalize', 'casefold',..., 'zfill']
```

- len()函数试图获取一个对象的长度，在`len()`函数内部，它自动去调用该对象的`__len__()`方法

```plain
>>> len('ABC')
3
>>> 'ABC'.__len__()
3
```

自己写的类，如果也想用`len(myObj)`的话，就自己写一个`__len__()`方法

```python
>>> class MyDog(object):
...     def __len__(self):
...         return 100
```

- `lower()`返回小写的字符串

```Python
>>> 'ABC'.lower()
'abc'
```

- `getattr()`、`setattr()`以及`hasattr()`，我们可以直接操作一个对象的状态

```python
>>> hasattr(obj, 'x') # 有属性'x'吗？
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> getattr(obj, 'y') # 获取属性'y'
```

如果试图获取不存在的属性，会抛出AttributeError的错误，可以传入一个default参数，如果属性不存在，就返回默认值：

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

- Python允许使用多重继承

```python
class Dog(Mammal, Runnable):
    pass

# Dog继承了Mammal和Runnableliang'g
```

#### 使用\_slots_

- 在定义`class`的时候，定义一个特殊的`__slots__`变量，来限制该`class`实例能添加的属性

```python
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```

- 使用`__slots__`要注意，`__slots__`定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。除非在子类中也定义`__slots__`，这样，子类实例允许定义的属性就是自身的`__slots__`加上父类的`__slots__`

#### 使用@property

- Python内置的`@property`装饰器就是负责把一个方法变成属性调用的

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

- 如果需要更精确地控制枚举类型，可以从`Enum`派生出自定义类，`@unique`装饰器可以帮助我们检查保证没有重复值

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

##### \_str_ & \__repr__()

- `__str__()`返回用户看到的字符串，而`__repr__()`返回程序开发者看到的字符串

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

- 如果一个类想被用于`for ... in`循环，类似list或tuple那样，就必须实现一个`__iter__()`方法，该方法返回一个迭代对象，然后，Python的for循环就会不断调用该迭代对象的`__next__()`方法拿到循环的下一个值，直到遇到`StopIteration`错误时退出循环

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

- 表现得像list那样按照下标取出元素，需要实现`__getitem__()`方法

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

- 写一个`__getattr__()`方法，动态返回一个属性,当调用不存在的属性时，比如`score`，Python解释器会试图调用`__getattr__(self, 'score')`来尝试获得属性

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

- 只需要定义一个`__call__()`方法，就可以直接对实例进行调用

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

- 我们需要判断一个对象是否能被调用，能被调用的对象就是一个`Callable`对象,通过`callable()`函数，我们就可以判断一个对象是否是“可调用”对象。

## module

- 通过import module 来导入一个模块
- 通过from module import xxx 来导入某个模块中的某一个类

### 作用域

- 在一个模块中，我们可能会定义很多函数和变量，但有的函数和变量我们希望给别人使用，有的函数和变量我们希望仅仅在模块内部使用。在Python中，是通过`_`前缀来实现的。
- 类似`__xxx__`这样的变量是特殊变量，可以被直接引用，但是有特殊用途
- 类似`_xxx`和`__xxx`这样的函数或变量就是非公开的（private），不应该被直接引用