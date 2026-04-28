## HelloWorld 示例

编写第一个Java程序：

```java
class HelloChina {
    public static void main(String[] args) {
        System.out.println("你好，世界！");
    }
}
```

### 编译和运行步骤

1. 编译：使用 `javac` 命令编译 Java 源文件：
    ```bash
    javac HelloChina.java
    ```

2. 生成的字节码文件：编译后会生成一个名为 `HelloChina.class` 的字节码文件。

3. 运行：使用 `java` 命令运行字节码文件：
    ```bash
    java HelloChina
    ```

### 中文编码问题

如果使用中文输出，需将编码设置为 ANSI（GBK），以避免中文字符乱码问题。

## Java 基础

### 类

在Java中，**类**是构造程序的基本单位，定义类的语法格式如下：

```java
class 类名 {
    // 类的成员变量
    // 类的成员方法
}
```

### 主方法（Main Method）

每个 Java 程序都必须包含一个 `main` 方法，作为程序的入口点。其固定格式如下：

```java
public static void main(String[] args) {
    // 程序执行的代码
}
```

- `public`: 表示公共的，任何地方都可以访问。
- `static`: 表示静态的，不依赖对象实例。
- `void`: 表示该方法无返回值。
- `main`: 方法名称，是程序的入口。
- `String[] args`: 参数为字符串数组，存储命令行传入的参数，全称是 `arguments`。

### 控制台输出

在Java中，可以使用 `System.out.println` 和 `System.out.print` 进行控制台输出：

- `System.out.println("内容");`：输出内容并换行。
- `System.out.print("内容");`：输出内容但不换行。

示例：

```java
System.out.println("Hello, World!"); // 输出后换行
System.out.print("Hello");           // 输出不换行
System.out.print(" World!");         // 输出继续在同一行
```

### 注意事项

- **Windows大小写问题**：Windows 系统的命令行不区分大小写，但 Java 是区分大小写的语言，类名和方法名等必须严格区分大小写。
  
- **public 类限制**：一个 Java 源文件中只能有一个 `public` 类，且该类的名称必须与源文件名相同。例如，类名为 `HelloChina`，文件名应为 `HelloChina.java`。

## Tips

- Java 程序通常是面向对象的，类是其中的核心结构。
- 编译生成的 `.class` 文件可以跨平台运行，只需确保目标系统安装了 JVM（Java 虚拟机）。

以下是整理并补充后的**Java数据类型**学习笔记，格式为Markdown：


## 基本数据类型

Java中有8种基本数据类型，它们可以分为四类：

1. **整型**：
    - `byte`：1字节，范围 -128 ~ 127
    - `short`：2字节，范围 -32,768 ~ 32,767
    - `int`：4字节，范围 -2^31 ~ 2^31-1（常用）
    - `long`：8字节，范围 -2^63 ~ 2^63-1（需在数值后加`L`，如`123L`）

2. **浮点型**：
    - `float`：4字节，精度较差，需在数值后加`F`，如`12.3F`
    - `double`：8字节，双精度，表示范围更大（默认浮点型为`double`）

3. **字符型**：
    - `char`：2字节，用于表示单个字符，支持 Unicode 编码（例如：`char c1 = '中';`）

4. **布尔型**：
    - `boolean`：只能取 `true` 或 `false`，占4字节（与`int`相同）

![image (11)](https://github.com/user-attachments/assets/c2fd13cd-c71f-485b-947f-89f24ffd1e7e)

![image (12)](https://github.com/user-attachments/assets/e749edf3-c595-45d6-a671-9695a257c3e7)


![image (13)](https://github.com/user-attachments/assets/0c6b360b-b12e-4431-8021-9992964c6130)


## 浮点型的精度问题

- `float`精度较低，但占用空间较小，用于需要节省内存的场景。
- `double`提供更高的精度，推荐在多数情况下使用`double`表示浮点数。

示例：
```java
int radius = 1;
double radius2 = 1.5;
```

## 字符型（char）

- 使用单引号 `' '` 来表示字符，如：`char c1 = '中';`。
- 只能包含一个字符，错误示范：`char c2 = 'ab';`
- 可以使用 Unicode 编码表示字符：`char c3 = '\u0036';`（表示字符'6'）
- 支持转义字符，如：
    - `char c4 = '\t';` // 制表符
    - `char c5 = '\n';` // 换行符
- 也可以使用字符对应的数值来表示，如：`char c6 = 97;`（'a' 的 ASCII 码是97）

## 布尔类型（boolean）

- 布尔类型只有两个值：`true` 和 `false`。
- 示例：
    ```java
    boolean bo1 = true;
    ```

## 数据类型的运算

### 自动类型提升

在运算时，数据类型可以自动进行类型提升。当不同类型的数据一起运算时，较小范围的类型会自动提升为较大范围的类型：

- 示例：
    ```java
    byte b1 = 12;
    short s1 = 10;
    int result = b1 + s1; // b1 + s1 自动提升为 int
    ```

- **注意**：`byte`、`short` 和 `char` 参与运算时，结果会自动提升为 `int`。

### 强制类型转换

如果需要将大容量的类型转换为小容量类型，必须使用**强制类型转换**，但这可能会丢失数据：

- 示例：
    ```java
    int i1 = 100;
    byte b2 = (byte) i1; // 强制类型转换
    ```

### 特别说明

- 整数常量默认是 `int` 类型，浮点常量默认是 `double` 类型。例如：
    ```java
    float f2 = 12.3F; // 必须加上 F，表明这是一个 float 类型
    ```

- 如果不加`F`，如 `float f3 = 12.3;`，会出现编译错误，因为 `12.3` 被认为是 `double` 类型，不能自动转换为 `float`。

### 示例：
```java
long l1 = 123L; // long 类型常量，需要加 L
long l2 = 123;  // int 类型常量，自动类型提升为 long

byte b3 = 20;
byte b4 = b3 + 1; // 报错，因为 b3 + 1 的结果是 int，需要使用 int 接收
```

## 数据类型练习题
![image (15)](https://github.com/user-attachments/assets/fec94a9f-b7f2-4c2a-9c4d-993422bddd85)

### 特殊注意：

- Java 变量名不能以数字开头，这是为了避免与数字字面量（如整型、浮点型）混淆。



### 示例：
```java
System.out.println('a' + 1 + "Hello!"); 
// 输出为 98Hello! 因为 'a' 的 ASCII 码为 97，97 + 1 = 98
```

## 引用数据类型

**String 类**属于引用数据类型，用于表示字符串。

- String 可以与其他数据类型进行连接运算，但不能用于其他运算。
  
![image (16)](https://github.com/user-attachments/assets/05226a91-4a22-452d-a5fc-6c7779e93ee8)
![image (17)](https://github.com/user-attachments/assets/c637543b-0bd5-4265-9c8f-4348bad6a0c4)
![image (18)](https://github.com/user-attachments/assets/2a6f0092-a88a-4eb5-ba73-1a7703e512a6)

- 示例：
    ```java
    String phoneNumber = "123-456-7890"; // 电话号码使用 String 表示
    System.out.println("Hello " + phoneNumber);
    ```
![image (14)](https://github.com/user-attachments/assets/2ec53abc-6b61-4d65-b1ad-6ab12f8793a8)


# Java 数据类型学习笔记

## 进制转换

### 常见进制

Java 中可以使用不同的进制表示数值：

- **二进制**：以 `0b` 或 `0B` 开头，如 `0b1101` 表示 13。
- **八进制**：以 `0` 开头，如 `015` 表示十进制的 13。
- **十进制**：默认表示法，如 `13`。
- **十六进制**：以 `0x` 或 `0X` 开头，如 `0xD` 表示 13。

![image (19)](https://github.com/user-attachments/assets/7044bf5f-5fa1-4f54-b820-6c8f6a08f201)
![image (20)](https://github.com/user-attachments/assets/72e7c261-f0f3-4bd1-bea5-58ec50af74ab)


### 进制转换规则

在Java程序中，编写时可以使用不同的进制，但**编译和运行的结果将以十进制展示**。

- 例如：
    ```java
    int binary = 0b1101;  // 二进制数 1101 (十进制 13)
    int octal = 015;      // 八进制数 015 (十进制 13)
    int hex = 0xD;        // 十六进制数 0xD (十进制 13)

    System.out.println(binary);  // 输出 13
    System.out.println(octal);   // 输出 13
    System.out.println(hex);     // 输出 13
    ```

### 了解即可

进制转换在 Java 编程中不是重点，了解即可。主要的进制操作包括将不同进制的数字转换为十进制结果。

![image (21)](https://github.com/user-attachments/assets/622d41f1-343e-44b9-98af-cc147e172cc3)

Java 中的数据类型分为两大类：**基本数据类型**和**引用数据类型**。

### 1. 基本数据类型
Java 提供了 8 种基本数据类型，它们直接存储在栈（stack）内存中。这 8 种类型可以分为四类：

- **整数类型**：
  - `byte`：1字节，范围是 -128 到 127
  - `short`：2字节，范围是 -32,768 到 32,767
  - `int`：4字节，范围是 -2^31 到 2^31-1
  - `long`：8字节，范围是 -2^63 到 2^63-1，表示较大的整数。可以使用后缀 `L` 表示长整型数值，例如 `100L`

- **浮点数类型**：
  - `float`：4字节，单精度浮点数，需要加后缀 `f`，例如 `3.14f`
  - `double`：8字节，双精度浮点数，是默认的浮点数类型，例如 `3.14`

- **字符类型**：
  - `char`：2字节，表示单个字符，使用单引号，例如 `'A'`。其存储 Unicode 编码（范围 0 到 65,535）

- **布尔类型**：
  - `boolean`：表示布尔值 `true` 或 `false`

### 2. 引用数据类型
引用数据类型包括类（`class`）、接口（`interface`）、数组（`array`）等。它们的值是对象的内存地址，而不直接存储对象的实际内容。

### 3. 自动类型提升（Widening Primitive Conversion）
自动类型提升是指当不同数据类型混合运算时，系统会自动将较小的数据类型提升为较大的数据类型，以确保运算的正确性。

自动类型提升遵循以下规则：
- `byte` → `short` → `int` → `long` → `float` → `double`
- `char` → `int`

**例子**：
```java
int a = 10;
double b = 5.5;
double result = a + b;  // int 类型 a 自动提升为 double
System.out.println(result);  // 输出 15.5
```

在上述例子中，`int` 类型的变量 `a` 被自动提升为 `double` 类型，然后与 `double` 类型的 `b` 进行运算。

### 4. 强制类型转换（Narrowing Primitive Conversion）
强制类型转换是指当需要将一个较大的数据类型转换为较小的数据类型时，必须显式地进行转换。因为可能会丢失精度或溢出，因此需要开发者使用显式的转换语法。

**语法**：
```java
目标类型 变量名 = (目标类型) 原始变量;
```

**例子**：
```java
double d = 9.78;
int i = (int) d;  // 强制类型转换，将 double 转为 int
System.out.println(i);  // 输出 9（小数部分被舍弃）
```

在这个例子中，`double` 类型的 `d` 被强制转换为 `int` 类型，结果是去掉了小数部分，只保留了整数部分。

### 5. 自动类型提升与强制类型转换的应用
#### 自动类型提升：
```java
byte b = 42;
char c = 'A';
int i = b + c;  // byte 和 char 被提升为 int
System.out.println(i);  // 输出 107 ('A' 的 Unicode 值为 65)
```

#### 强制类型转换：
```java
long l = 1000L;
int i = (int) l;  // 强制将 long 转为 int
System.out.println(i);  // 输出 1000
``` 




### 原码、反码与补码

在二进制系统中，负数的表示方式有三种：

- **原码**：符号位加上数值的绝对值。
- **反码**：除了符号位，其他位全部取反（0变1，1变0）。
- **补码**：反码的基础上加 1。

![image (22)](https://github.com/user-attachments/assets/03046cc6-8cd9-4c5d-a114-d0f804077c53)
![image (23)](https://github.com/user-attachments/assets/c76fc5a4-c4b6-4959-a882-9033ed258ddc)


例如，对于一个负数 `-5`：

- 原码：`1000 0101`
- 反码：符号位不变，其他位取反，得到：`1111 1010`
- 补码：反码加 1，得到：`1111 1011`

在Java中，所有负数的表示和计算都是通过**补码**来实现的。


# Java 学习笔记

## 书写规范

### Java 注释

Java 提供了三种类型的注释，用于解释代码或生成文档：

1. **单行注释**：使用 `//`，表示一行注释，后面的内容不会被编译执行。
    ```java
    // 这是单行注释
    ```

2. **多行注释**：使用 `/* */`，可以跨多行书写注释，适合解释较长的代码段。
    ```java
    /* 这是多行注释
       可以跨越多行 */
    ```

3. **文档注释**：使用 `/** */`，用于生成 Java 文档（API文档）。文档注释常用于类、方法等，并可以包含一些特殊标记。
    ```java
    /**
    * @author 作者名
    * @version 1.0
    * 这是文档注释，可以生成网页形式的API文档。
    */
    ```

![image (24)](https://github.com/user-attachments/assets/bf61f39b-f598-4d01-9f78-e7049470fb9d)


### Java API 文档

Java 提供了强大的 **API文档**（Application Programming Interface），包含了所有 Java 类库、方法的详细说明。你可以通过文档注释的方式，在编写代码时自动生成类似的网页文档，方便使用者了解代码结构和功能。

- 生成文档命令：使用 `javadoc` 命令生成 Java 文档。例如：
    ```bash
    javadoc MyClass.java
    ```

生成的文档可以通过浏览器查看，方便阅读和共享。

## JVM（Java虚拟机）

Java 的 **JVM**（Java Virtual Machine）是其核心部分，负责将编译后的字节码（`.class` 文件）解释为机器指令执行。JVM具有以下特点：

1. **跨平台性**：Java 语言具有“编写一次，处处运行”的特性，因为不同平台只需要提供不同的 JVM 实现。字节码文件在各个平台的 JVM 上都可以运行。

2. **自动内存管理**：Java 通过垃圾回收机制（Garbage Collection, GC）自动管理内存分配和回收，开发者无需手动释放内存，减少了内存泄漏的风险。

3. **无指针**：与 C、C++ 等语言不同，Java 没有直接操作内存的指针，避免了很多指针引发的错误，提高了代码的安全性。

- JVM 主要包含三个部分：
    - **类加载器（Class Loader）**：负责加载 Java 字节码文件。
    - **执行引擎（Execution Engine）**：将字节码解释为机器指令执行。
    - **内存管理（Memory Management）**：负责对象的内存分配与垃圾回收。

JVM 提供了一个封闭、隔离的运行环境，增强了程序的安全性和跨平台性。


## 特殊字符

在Java中，常用的转义字符有：

- `\n`：换行符，将输出内容移至下一行。
    ```java
    System.out.println("Hello\nWorld"); 
    // 输出：
    // Hello
    // World
    ```

- `\t`：制表符，用于输出制表符的效果，相当于跳到下一个水平制表位置。
    ```java
    System.out.println("Hello\tWorld"); 
    // 输出：Hello   World
    ```

## 推荐书籍

在学习 Java 的过程中，以下书籍是非常经典和推荐的：

1. **《Java核心技术》**（Core Java）  
   适合入门及中级开发者，全面讲解了 Java 基础、面向对象编程及相关技术。

2. **《Effective Java》**  
   高级 Java 编程的最佳实践，书中列举了很多使用 Java 时应当遵循的规则和技巧，适合进阶开发者。

3. **《Java编程思想》**（Thinking in Java）  
   深入分析了 Java 的面向对象特性及高级编程技术，是很多开发者必读的经典书籍。

4. **《剑指Java》**  
   侧重于面试准备，涵盖了Java编程的各个方面，适合有一定基础、准备面试的开发者。

## 图形化用户界面（GUI）和命令行界面（CLI）

### 图形化GUI

Java 提供了多种工具来开发图形化用户界面（GUI），例如：

- **Swing**：轻量级的 GUI 工具包，适合开发桌面应用程序。
- **JavaFX**：现代化的 GUI 库，支持更丰富的图形效果和交互方式。

### 命令行CLI

在学习 Java 编程时，命令行界面（CLI）也是非常重要的。命令行操作可以帮助编译、运行程序，管理文件等。

### 常用 DOS 命令

在 Windows 系统下，常用的 DOS 命令有：

- `dir`：列出当前目录下的文件和文件夹。
    ```bash
    dir
    ```

- `cd`：切换当前目录。
    ```bash
    cd 文件夹路径
    ```

- `md`：创建新目录。
    ```bash
    md 文件夹名
    ```

- `rd`：删除空目录。
    ```bash
    rd 文件夹名
    ```

这些命令在使用命令行编译、运行 Java 程序时非常实用，有助于提高开发效率。


