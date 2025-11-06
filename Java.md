# OnJava

## 对象无处不在

- BigInteger 支持任意精度的整数（对应于int）、BigDecimal支持任意精度的浮点数（对应于float）



# 廖雪峰

## 开发环境

### JDK

1. jdk的bin目录下部分可执行文件作用

- java：这个可执行程序其实就是JVM，运行Java程序，就是启动JVM，然后让JVM执行指定的编译后的代码；
- javac：这是Java的编译器，它用于把Java源码文件（以`.java`后缀结尾）编译为Java字节码文件（以`.class`后缀结尾）；
- jar：用于把一组`.class`文件打包成一个`.jar`文件，便于发布；
- javadoc：用于从Java源码中自动提取注释并生成文档；
- jdb：Java调试器，用于开发阶段的运行调试。

2. 从Java 11开始新增的一个功能，它可以直接运行一个单文件源码



## Java基础

### 运算

整数运算在除数为`0`时会报错，而浮点数运算在除数为`0`时，不会报错，但会返回几个特殊值：

- `NaN`表示Not a Number
- `Infinity`表示无穷大
- `-Infinity`表示负无穷大

```java
double d1 = 0.0 / 0; // NaN
double d2 = 1.0 / 0; // Infinity
double d3 = -1.0 / 0; // -Infinity
```



### 字符串

从Java 13开始，字符串可以用`"""..."""`表示多行字符串

```java
// 多行字符串
public class Main {
    public static void main(String[] args) {
        String s = """
                   SELECT * FROM
                     users
                   WHERE id > 100
                   ORDER BY name DESC
                   """;
        System.out.println(s);
    }
}
```

### 数组

- 打印多维数组可以使用`Arrays.deepToString()`



### 流程控制

#### switch

- 从Java 14开始，`switch`语句升级为更简洁的表达式语法，使用类似模式匹配（Pattern Matching）的方法，保证只有一种路径会被执行，并且不需要`break`语句

```java
        String fruit = "apple";
        switch (fruit) {
        case "apple" -> System.out.println("Selected apple");
        case "pear" -> System.out.println("Selected pear");
        case "mango" -> {
            System.out.println("Selected mango");
            System.out.println("Good choice!");
        }
        default -> System.out.println("No fruit selected");
        }
```

- 使用新的`switch`语法，不但不需要`break`，还可以直接返回值

```java
        String fruit = "apple";
        int opt = switch (fruit) {
            case "apple" -> 1;
            case "pear", "mango" -> 2;
            default -> 0;
        }; // 注意赋值语句要以;结束
        System.out.println("opt = " + opt);
```

- 如果需要复杂的语句，我们也可以写很多语句，放到`{...}`里，然后，用`yield`返回一个值作为`switch`语句的返回值

```java
        String fruit = "orange";
        int opt = switch (fruit) {
            case "apple" -> 1;
            case "pear", "mango" -> 2;
            default -> {
                int code = fruit.hashCode();
                yield code; // switch语句返回值
            }
        };
```

### 面相对象

#### 继承

- 从Java 17开始，允许使用`sealed`修饰class，并通过`permits`明确写出能够从该class继承的子类名称。

```java
public sealed class Shape permits Rect, Circle, Triangle {
    ...
}
```

- 从Java 14开始，判断`instanceof`后，可以直接转型为指定变量，避免再次强制转型

```java
        Object obj = "hello";
        if (obj instanceof String s) {
            // 可以直接使用变量s:
            System.out.println(s.toUpperCase());
        }
```

#### 包

- `import static`的语法，它可以导入一个类的静态字段和静态方法

```java
// 导入System类的所有静态字段和静态方法:
import static java.lang.System.*
```

#### 模块（JAVA 9新特性）

//todo

#### String

- `String`提供了`isEmpty()`和`isBlank()`来判断字符串是否为空和空白字符串

```java
"".isEmpty(); // true，因为字符串长度为0
"  ".isEmpty(); // false，因为字符串长度不为0
"  \n".isBlank(); // true，因为只包含空白字符
" Hello ".isBlank(); // false，因为包含非空白字符
```

- 拼接字符串使用静态方法`join()`，它用指定的字符串连接字符串数组

```java
String[] arr = {"A", "B", "C"};
String s = String.join("***", arr); // "A***B***C"
```

- 字符串提供了`formatted()`方法和`format()`静态方法，可以传入其他参数，替换占位符，然后生成新的字符串

```java
        String s = "Hi %s, your score is %d!";
        System.out.println(s.formatted("Alice", 80));
        System.out.println(String.format("Hi %s, your score is %.2f!", "Bob", 59.5));
```

- 要特别注意，`Integer`有个`getInteger(String)`方法，它不是将字符串转换为`int`，而是把该字符串对应的系统变量转换为`Integer`

```java
Integer.getInteger("java.version"); // 版本号，11
```

- Java的`String`和`char`在内存中总是以Unicode编码表示

- 如果我们要手动把字符串转换成其他编码，可以这样做
- 如果要把已知编码的`byte[]`转换为`String`

```java
byte[] b1 = "Hello".getBytes(); // 按系统默认编码转换，不推荐
byte[] b2 = "Hello".getBytes("UTF-8"); // 按UTF-8编码转换
byte[] b2 = "Hello".getBytes("GBK"); // 按GBK编码转换
byte[] b3 = "Hello".getBytes(StandardCharsets.UTF_8); // 按UTF-8编码转换

byte[] b = ...
String s1 = new String(b, "GBK"); // 按GBK转换
String s2 = new String(b, StandardCharsets.UTF_8); // 按UTF-8转换
```
