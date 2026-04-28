测试方式

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731933602728-b78e05ef-e607-4227-a83c-2cd748ffeb91.png)

### DK版本的里程碑
+ **JDK 5.0**：引入了泛型、增强的for循环、自动装箱/拆箱、枚举类型、可变参数、静态导入、注解等。
+ **JDK 8.0**：引入了Lambda表达式、函数式接口、Stream API、新的日期时间API（java.time）、默认方法、Optional类等。
+ **JDK 9.0**（2017年9月）：引入模块化系统（Project Jigsaw）、JShell（交互式编程工具）、改进的JVM编译器接口等。从此版本开始，每半年发布一个新的版本。
+ **JDK 11**（2018年9月）：引入了新的字符串方法、HTTP Client API、局部变量类型推断（var）等。此版本为长期支持（LTS）版本。
+ **JDK 17**（2021年9月）：引入了新的语言特性和API改进，此版本也是长期支持（LTS）版本。

### 如何学习新特性
#### 角度1：新的语法规则（多关注）
+ **自动装箱、自动拆箱**：简化了基本类型和包装类型之间的转换。
+ **注解**：提供了元数据的支持。
+ **enum**：引入枚举类型。
+ **Lambda表达式**：简化了匿名内部类的使用，增强了函数式编程的能力。
+ **方法引用**：简化了方法调用的语法。
+ **switch表达式**：增强了switch语句的功能。
+ **try-catch变化**：改进了异常处理机制。
+ **record**：引入了一种简洁的类定义方式。

#### 角度2：增加、过时、删除API
+ **StringBuilder**：替代StringBuffer，提供了更高效的字符串操作。
+ **ArrayList**：增强了集合框架的功能。
+ **新的日期时间API**：提供了更强大和灵活的日期时间处理能力。
+ **Optional**：解决了空指针异常的问题。

#### 角度3：底层的优化、JVM参数的调整、GC的变化、内存结构
+ **底层优化**：包括性能提升和安全性增强。
+ **JVM参数的调整**：提供了更多的配置选项。
+ **GC的变化**：引入了新的垃圾回收器，如G1、ZGC等。
+ **内存结构**：从永久代（PermGen）转变为元空间（Metaspace），提高了内存管理的效率。



jjs 直接运行 js 脚本

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934138063-6be101fa-db49-4430-93d2-6f6b6b65c1b6.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934133817-d0eb9f20-b8af-4e22-aae4-da8912561b56.png)



（重要）Lambda 表达式

凡是确定的都可以删掉

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934274025-a2fd0c56-7523-4f96-99d6-f833b74427e7.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934293558-c831a980-b88f-4b2c-b1f3-70e2a421bb7b.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934356970-dd38b560-05db-4985-94aa-526b7675337c.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934376384-11476564-8007-407e-86e4-8707a010d904.png)



方法应用和表达式

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731934422947-7c408d63-f899-498c-ab1e-5f2d2589f439.png)

### Lambda表达式的使用举例
#### 1. 使用举例
java

```plain
(o1, o2) -> Integer.compare(o1, o2);
```

这个例子展示了一个简单的Lambda表达式，用于比较两个整数。

#### 2. Lambda表达式的格式举例
Lambda表达式的格式如下：

java

```plain
(parameters) -> expression
```

或者

java

```plain
(parameters) -> { statements; }
```

**示例**：

java

```plain
(int x, int y) -> x + y
```

或者

java

```plain
(String s) -> { System.out.println(s); }
```

#### 3. Lambda表达式的格式
Lambda操作符或箭头操作符 `->` 将Lambda表达式分为两部分：

+ **左边**：Lambda形参列表，对应着要重写的接口中的抽象方法的形参列表。
+ **右边**：Lambda体，对应着接口的实现类要重写的方法的方法体。

### Lambda表达式的本质
Lambda表达式的本质是对接口的实现。它提供了一种简洁的语法来实现函数式接口（即只有一个抽象方法的接口）。Lambda表达式可以看作是匿名内部类的一种简化形式。



### Lambda表达式的本质
+ **万事万物皆对象**：Lambda表达式作为接口的实现类的对象。
+ **匿名函数**：Lambda表达式是一个匿名函数，没有名称，但有参数列表和函数体。

### 函数式接口
#### 5.1 什么是函数式接口？为什么需要函数式接口？
+ **函数式接口**：如果接口中只声明有一个抽象方法，则此接口就称为函数式接口。
+ **需要函数式接口的原因**：只有给函数式接口提供实现类的对象时，我们才可以使用Lambda表达式。

#### 5.2 API中函数式接口所在的包
+ **java.util.function**：JDK 8中声明的函数式接口都在`java.util.function`包下。

#### 5.3 4个基本的函数式接口
**Consumer<T>**：接受一个输入参数并且不返回结果。

1. java

```plain
Consumer<String> consumer = s -> System.out.println(s);
consumer.accept("Hello, World!");
```

**Supplier<T>**：不接受任何参数，返回一个结果。

2. java

```plain
Supplier<String> supplier = () -> "Hello, World!";
System.out.println(supplier.get());
```

**Function<T, R>**：接受一个输入参数，返回一个结果。

3. java

```plain
Function<Integer, String> function = i -> "Number: " + i;
System.out.println(function.apply(5));
```

**Predicate<T>**：接受一个输入参数，返回一个布尔值。

4. java

```plain
Predicate<Integer> predicate = i -> i > 0;
System.out.println(predicate.test(5)); // true
```

### Lambda表达式的语法规则总结
**无参数，无返回值**：

1. java

```plain
() -> System.out.println("Hello, World!");
```

**一个参数，无返回值**：

2. java

```plain
(x) -> System.out.println(x);
```

**多个参数，有返回值**：

3. java

```plain
(x, y) -> x + y;
```

**Lambda体中有多条语句**：

4. java

```plain
(x, y) -> {
    int sum = x + y;
    return sum;
};
```

**Lambda表达式的参数类型可以省略**：

5. java

```plain
(x, y) -> x + y;
```



四个基本的函数式接口

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731935310443-30031d3b-a4a8-448a-b091-dd6cac4237c1.png)



### 4个基本的函数式接口
#### 接口及其对应的抽象方法
1. **消费型接口：Consumer<T>**
    - **抽象方法**：`void accept(T t)`
    - **作用**：对给定的参数执行某种操作，不返回结果。

**示例**：

    - java

```plain
Consumer<String> consumer = s -> System.out.println(s);
consumer.accept("Hello, World!");
```

2. **供给型接口：Supplier<T>**
    - **抽象方法**：`T get()`
    - **作用**：提供一个结果，不接受参数。

**示例**：

    - java

```plain
Supplier<String> supplier = () -> "Hello, World!";
System.out.println(supplier.get());
```

3. **函数型接口：Function<T, R>**
    - **抽象方法**：`R apply(T t)`
    - **作用**：对给定的参数进行处理，并返回一个结果。

**示例**：

    - java

```plain
Function<Integer, String> function = i -> "Number: " + i;
System.out.println(function.apply(5));
```

4. **判断型接口：Predicate<T>**
    - **抽象方法**：`boolean test(T t)`
    - **作用**：对给定的参数进行判断，返回一个布尔值。

**示例**：

    - java

```plain
Predicate<Integer> predicate = i -> i > 0;
System.out.println(predicate.test(5)); // true
```

这些函数式接口在Java 8中引入，位于`java.util.function`包下，极大地简化了代码的编写，提高了代码的可读性和可维护性。



### Lambda表达式的语法规则总结
#### 左边：Lambda形参列表
+ **参数类型省略**：参数的类型可以省略，编译器会根据上下文推断参数类型。

**单个参数省略括号**：如果形参只有一个，则一对 `()` 也可以省略。

+ java

```plain
// 示例
(x) -> x * x
x -> x * x
```

#### 右边：Lambda体
+ **单行语句省略大括号**：如果方法体中只有一行执行语句，则一对 `{}` 可以省略。

**省略return关键字**：如果有 `return` 关键字，则必须一并省略。

+ java

```plain
// 示例
(x, y) -> x + y
(x, y) -> {
    return x + y;
}
```

### 示例代码
java



```plain
// 无参数，无返回值
() -> System.out.println("Hello, World!");

// 一个参数，无返回值
x -> System.out.println(x);

// 多个参数，有返回值
(x, y) -> x + y;

// Lambda体中有多条语句
(x, y) -> {
    int sum = x + y;
    return sum;
};

```



### 方法引用的理解
#### 1. 举例
java

```plain
Integer::compare;
```

这个例子展示了如何使用方法引用来替代Lambda表达式。

#### 2. 方法引用的理解
+ **方法引用**：可以看作是基于Lambda表达式的进一步刻画。当需要提供一个函数式接口的实例时，我们可以使用Lambda表达式提供此实例。
+ **替换Lambda表达式**：当满足一定的条件时，我们还可以使用方法引用或构造器引用替换Lambda表达式。

#### 3. 方法引用的本质
+ **函数式接口的实例**：方法引用作为了函数式接口的实例。
+ **匿名函数**：方法引用是一个匿名函数，没有名称，但有参数列表和函数体。

### 函数式接口
#### 5.1 什么是函数式接口？为什么需要函数式接口？
+ **函数式接口**：如果接口中只声明有一个抽象方法，则此接口就称为函数式接口。
+ **需要函数式接口的原因**：只有给函数式接口提供实现类的对象时，我们才可以使用Lambda表达式。

#### 5.2 API中函数式接口所在的包
+ **java.util.function**：JDK 8中声明的函数式接口都在`java.util.function`包下。

#### 5.3 4个基本的函数式接口
1. **消费型接口：Consumer<T>**
    - **抽象方法**：`void accept(T t)`
    - **作用**：对给定的参数执行某种操作，不返回结果。

**示例**：

    - java

```plain
Consumer<String> consumer = s -> System.out.println(s);
consumer.accept("Hello, World!");
```

2. **供给型接口：Supplier<T>**
    - **抽象方法**：`T get()`
    - **作用**：提供一个结果，不接受参数。

**示例**：

    - java

```plain
Supplier<String> supplier = () -> "Hello, World!";
System.out.println(supplier.get());
```

3. **函数型接口：Function<T, R>**
    - **抽象方法**：`R apply(T t)`
    - **作用**：对给定的参数进行处理，并返回一个结果。

**示例**：

    - java

```plain
Function<Integer, String> function = i -> "Number: " + i;
System.out.println(function.apply(5));
```

4. **判断型接口：Predicate<T>**
    - **抽象方法**：`boolean test(T t)`
    - **作用**：对给定的参数进行判断，返回一个布尔值。

**示例**：

    - java

```plain
Predicate<Integer> predicate = i -> i > 0;
System.out.println(predicate.test(5)); // true
```











### Lambda表达式与方法引用示例
#### 1. Lambda表达式
java

```plain
Consumer<String> con2 = s -> System.out.println(s);
con2.accept("hello!");
```

在这个例子中，`Consumer<String>` 接口的 `accept` 方法被实现为一个Lambda表达式，用于打印传入的字符串。

#### 2. 方法引用
java

```plain
Consumer<String> con3 = System.out::println;
con3.accept("hello!");
```

在这个例子中，方法引用 `System.out::println` 被用来替代Lambda表达式，实现了相同的功能，即打印传入的字符串。

### 方法引用的理解
+ **方法引用**：可以看作是基于Lambda表达式的进一步刻画。当需要提供一个函数式接口的实例时，我们可以使用Lambda表达式提供此实例。
+ **替换Lambda表达式**：当满足一定的条件时，我们还可以使用方法引用或构造器引用替换Lambda表达式。

### 方法引用的本质
+ **函数式接口的实例**：方法引用作为了函数式接口的实例。
+ **匿名函数**：方法引用是一个匿名函数，没有名称，但有参数列表和函数体。







### 方法引用的理解
#### 1. 举例
java

```plain
Integer::compare;
```

这个例子展示了如何使用方法引用来替代Lambda表达式。

#### 2. 方法引用的理解
+ **方法引用**：可以看作是基于Lambda表达式的进一步刻画。当需要提供一个函数式接口的实例时，我们可以使用Lambda表达式提供此实例。
+ **替换Lambda表达式**：当满足一定的条件时，我们还可以使用方法引用或构造器引用替换Lambda表达式。

#### 3. 方法引用的本质
+ **函数式接口的实例**：方法引用作为了函数式接口的实例。
+ **匿名函数**：方法引用是一个匿名函数，没有名称，但有参数列表和函数体。

### 方法引用的格式
+ **格式**：类(或对象)::方法名

### 具体使用情况说明
#### 情况1：对象::实例方法
+ **要求**：函数式接口中的抽象方法a与其内部实现时调用的对象的某个方法b的形参列表和返回值类型都相同（或一致）。
+ 此时可以考虑使用方法 b 实现对方法 a 的替换，覆盖。此替换或覆盖即为方法引用。

注意：可以考虑使用方法 b 实现对方法 a 的替换，覆盖。此替换或覆盖即为方法引用。

**示例**：

+ java

```plain
Consumer<String> con3 = System.out::println;
con3.accept("hello!");
```

#### 情况2：类::静态方法
**示例**：

+ java

```plain
BiFunction<Integer, Integer, Integer> compare = Integer::compare;
System.out.println(compare.apply(5, 3)); // 输出：1
```

要求 函数式接口的抽象方法 a 与其内部实现时调用的类的某个静态方法 b 的形参列表和返回值类型都相同（或一致）。

此时可以考虑使用方法 b 实现对方法 a 的 替换，覆盖。此替或覆盖即为方法引用



注意 此方法 b 是静态方法，需要类调用



情况 3  类 :: 实例方法



要求:函数式接口中的抽象方法a与其内部实现时调用的对象的某个方法b的返回值类型相同。

同时，抽象方法a中有n个参数，方法b中有n-1个参效，且抽象方法a的第1个参数作为方法b的调用者，且抽象方法a

的后n-1个参数与方法b的n山个参数的类型相同(或一致)。则可以考虑使用方法b实现对方法a的替换、覆盖。此替换或覆盖

注意;此方法b是非静态的方法，需要对象调用。但是形式上，写出对象a所属的类



### 构造器引用
#### 1.1 格式
java

```plain
类名::new
```

#### 1.2 说明
构造器引用调用了类名对应的类中的某一个确定的构造器。具体调用的是类中的哪一个构造器，取决于函数式接口的抽象方法的形参列表。

### 示例代码
java

```plain
// 使用构造器引用创建Person对象
Supplier<Person> personSupplier = Person::new;
Person person = personSupplier.get();
```

### 数组引用
#### 格式
java

```plain
数组名[]::new
```

### 示例代码
java

```plain
// 使用数组引用创建一个String数组
Function<Integer, String[]> arrayFunction = String[]::new;
String[] stringArray = arrayFunction.apply(10);
```





![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731937830963-04df85ba-31f1-4458-ae72-592fae6f68f3.png)



Stream API

Stream API vs 集合框架

Stream API 关注的是多个数据的计算(排序、查找、过滤、映射、遍历等)，面向CPU的。

集合关注的数据的存储，向下内存的。

Stream API 之于集合，类似于SQL之于数据表的查询。

### Stream的使用说明
1. **Stream 自己不会存储元素**：
    - Stream 是对数据源（如集合、数组）的抽象，不会存储实际的数据。
2. **Stream 不会改变源对象**：
    - Stream 操作不会修改源对象，而是返回一个持有结果的新Stream。
3. **Stream 操作是延迟执行的**：
    - Stream 操作是延迟执行的，只有在需要结果的时候才会执行。这意味着一旦执行终止操作，就会执行中间操作链，并产生结果。
4. **Stream 一旦执行了终止操作，就不能再调用其它中间操作或终止操作了**：
    - 一旦执行了终止操作（如 `forEach`、`collect`），Stream 就会被关闭，不能再进行其他操作。

### Stream 执行流程
**Stream的实例化**：

    - 通过数据源（如集合、数组）创建Stream实例。
1. java

```plain
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();
```

**一系列的中间操作**：

    - 中间操作是对Stream进行转换，如 `filter`、`map`、`sorted` 等。这些操作是延迟执行的，只有在终止操作时才会执行。
2. java

```plain
Stream<String> filteredStream = stream.filter(s -> s.startsWith("a"));
```

**执行终止操作**：

    - 终止操作会触发Stream的执行，并生成结果，如 `forEach`、`collect`、`reduce` 等。
3. java

```plain
filteredStream.forEach(System.out::println);
```



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732013492177-643e57dd-6fb5-43f9-aed2-f3e0bc53d6b8.png)



