java

```plain
public class NormalExample {
    public void sayHello() {
        System.out.println("Hello, World!");
    }

    public static void main(String[] args) {
        // 正常方式创建对象并调用方法
        NormalExample example = new NormalExample();
        example.sayHello();
    }
}
```

### 反射方式
java

```plain
import java.lang.reflect.Method;

public class ReflectionExample {
    public void sayHello() {
        System.out.println("Hello, World!");
    }

    public static void main(String[] args) {
        try {
            // 反射方式创建对象并调用方法
            Class<?> clazz = Class.forName("ReflectionExample");
            Object instance = clazz.getDeclaredConstructor().newInstance();
            Method method = clazz.getMethod("sayHello");
            method.invoke(instance);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 说明
1. **正常方式**：
    - 直接使用 `new` 关键字创建对象。
    - 直接调用对象的方法。
2. **反射方式**：
    - 使用 `Class.forName` 获取类的 `Class` 对象。
    - 使用 `getDeclaredConstructor().newInstance()` 创建对象实例。
    - 使用 `getMethod` 获取方法对象。
    - 使用 `invoke` 调用方法。



反射可以调用类中私有的构造器



### Person类
java

```plain
public class Person {
    private String name;
    private int age;

    private Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

### 反射调用私有构造器
java

```plain
import java.lang.reflect.Constructor;

public class ReflectionTest {
    @Test
    public void test3() throws Exception {
        // 1. 调用私有的构造器，创建Person的实例
        Class<Person> clazz = Person.class;
        Constructor<Person> cons = clazz.getDeclaredConstructor(String.class, int.class);
        cons.setAccessible(true);
        Person p1 = cons.newInstance("Tom", 12);
        System.out.println(p1);
    }
}
```

### 说明
1. **Person类**：
    - 定义了一个私有的构造器 `Person(String name, int age)`。
    - 重写了 `toString()` 方法以便于输出对象信息。
2. **反射调用私有构造器**：
    - 使用 `Class.getDeclaredConstructor` 获取私有构造器。
    - 使用 `setAccessible(true)` 使私有构造器可访问。
    - 使用 `newInstance` 创建对象实例。



### 面向对象中创建对象和调用结构的方式
#### 不使用反射
+ **封装性**：需要考虑封装性，不能调用类中私有的结构。
+ **直接调用**：通过直接创建对象并调用其方法和属性。

**示例**：

+ java

```plain
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person("Tom", 12);
        person.sayHello();
    }
}
```

#### 使用反射
+ **动态性**：可以在运行时动态地获取对象所属的类，动态地调用相关的方法和属性，包括私有的结构。
+ **灵活性**：可以调用运行时类中任意的构造器、属性、方法。

**示例**：

+ java

```plain
import java.lang.reflect.Constructor;
import java.lang.reflect.Method;

public class Person {
    private String name;
    private int age;

    private Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    private void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}

public class ReflectionExample {
    public static void main(String[] args) {
        try {
            Class<Person> clazz = Person.class;
            Constructor<Person> cons = clazz.getDeclaredConstructor(String.class, int.class);
            cons.setAccessible(true);
            Person person = cons.newInstance("Tom", 12);

            Method method = clazz.getDeclaredMethod("sayHello");
            method.setAccessible(true);
            method.invoke(person);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 使用场景对比
#### 非反射方式
+ **常见场景**：日常开发中，完成业务代码时使用非反射方式较多，因为相关的对象、方法的调用都是确定的。
+ **优点**：代码直观、性能高、易于维护。

#### 反射方式
+ **常见场景**：设计框架时大量使用反射，因为反射体现了动态性，可以在运行时动态地获取对象所属的类，动态地调用相关的方法。
+ **优点**：灵活性高，可以处理未知类型和方法。
+ **缺点**：性能较低，代码复杂度高。

### 框架开发
+ **框架 = 注解 + 反射 + 设计模式**：在设计框架时，反射是一个重要的组成部分，结合注解和设计模式，可以实现高度灵活和可扩展的框架。





### 单例模式与反射
#### 单例模式
单例模式确保一个类只有一个实例，并提供一个全局访问点。常见的单例模式有两种实现方式：饿汉式和懒汉式。

**饿汉式**：

java

```plain
public class Singleton {
    private static final Singleton instance = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return instance;
    }
}
```

**懒汉式**：

java

```plain
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

#### 通过反射创建多个对象
通过反射，可以调用类中私有的构造器，从而创建多个实例。这确实会破坏单例模式的约束。

**示例代码**：

java

```plain
import java.lang.reflect.Constructor;

public class ReflectionSingletonTest {
    public static void main(String[] args) {
        try {
            Class<Singleton> clazz = Singleton.class;
            Constructor<Singleton> cons = clazz.getDeclaredConstructor();
            cons.setAccessible(true);

            Singleton instance1 = cons.newInstance();
            Singleton instance2 = cons.newInstance();

            System.out.println(instance1);
            System.out.println(instance2);
            System.out.println(instance1 == instance2); // false
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### 封装性与反射
+ **封装性**：封装性体现的是是否建议我们调用内部API的问题。比如，`private`声明的结构，意味着不建议调用。
+ **反射**：反射体现的是我们能否调用的问题。因为类的完整结构都加载到了内存中，所以我们有能力进行调用。

### 总结
反射可以突破封装性，调用类中私有的结构，但这并不意味着Java语言设计存在Bug。封装性和反射是两个不同的概念：

+ **封装性**：建议不调用内部API。
+ **反射**：提供了调用的能力。





### Class类的理解
#### Java类的加载过程
1. **编译**：
    - 编写好的 `.java` 源文件通过 `javac.exe` 编译，会生成一个或多个 `.class` 字节码文件。
2. **解释运行**：
    - 使用 `java.exe` 命令对指定的 `.class` 文件进行解释运行。
    - 在解释运行的过程中，需要将 `.class` 字节码文件加载到内存中（存放在方法区）。
3. **Class实例**：
    - 加载到内存中的 `.class` 文件对应的结构即为 `Class` 的一个实例。
    - 例如：加载到内存中的 `Person` 类、`String` 类或 `User` 类，都作为 `Class` 的一个实例。

#### 示例代码
java

```plain
// 获取运行时类的Class实例
Class clazz1 = Person.class;
Class clazz2 = String.class;
Class clazz3 = User.class;
Class clazz4 = Comparable.class;
```

### 说明
+ **Class类**：`Class` 类是Java反射机制的核心类，它表示正在运行的Java应用程序中的类和接口。
+ **实例化**：通过 `Class` 类的实例，可以获取类的详细信息，如类名、方法、构造器、字段等。
+ **用途**：`Class` 类的实例在反射机制中非常重要，可以用来动态地创建对象、调用方法、访问字段等。



#### Class的实例可以指向哪些结构
Class的实例可以指向所有Java类型，包括：

1. **class**：外部类、成员（成员内部类、静态内部类）、局部内部类、匿名内部类。
2. **interface**：接口。
3. **[]**：数组。
4. **enum**：枚举。
5. **annotation**：注解（`@interface`）。
6. **primitive type**：基本数据类型。
7. **void**：空类型。

### 示例代码
java

```plain
public class ReflectionDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        // 通过类名
        Class<Person> clazz1 = Person.class;

        // 通过对象的getClass()方法
        Person person = new Person();
        Class<? extends Person> clazz2 = person.getClass();

        // 通过Class.forName()方法
        Class<?> clazz3 = Class.forName("com.example.Person");

        // 打印Class实例
        System.out.println(clazz1);
        System.out.println(clazz2);
        System.out.println(clazz3);
    }
}

class Person {
    // 类的定义
}
```







![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731924703356-8b426c12-76c9-4fbc-bb9c-c5bd73b174b3.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731924692648-274dba6a-9edd-4b50-9b86-058979a5db85.png)



java 能识别的字节码文件都以 cafebabe 开头

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731924857685-1f20ed1e-cd8c-44af-9d84-03753c4b68cf.png)



### 类的加载过程
#### 1. 加载（Loading）
将类的 `.class` 文件读入内存，并为之创建一个 `java.lang.Class` 对象。此过程由类加载器完成。

#### 2. 链接（Linking）
链接过程包括三个阶段：

1. **验证（Verify）**：
    - 确保加载的类信息符合JVM规范，例如：以 `cafebabe` 开头，没有安全方面的问题。
2. **准备（Prepare）**：
    - 正式为类变量（`static`）分配内存并设置类变量默认初始值的阶段，这些内存都将在方法区中进行分配。
3. **解析（Resolve）**：
    - 虚拟机常量池内的符号引用（常量名）替换为直接引用（地址）的过程。

#### 3. 初始化（Initialization）
执行类构造器 `<clinit>()` 方法的过程。类构造器 `<clinit>()` 方法是由编译期自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。

### 关于类的加载器（以JDK8版本为例）
类加载器负责将 `.class` 文件加载到内存中，并为之创建 `java.lang.Class` 对象。类加载器的主要类型包括：

1. **启动类加载器（Bootstrap ClassLoader）**：
    - 加载核心类库，如 `rt.jar`。
2. **扩展类加载器（Extension ClassLoader）**：
    - 加载扩展类库，如 `ext` 目录下的类库。
3. **应用程序类加载器（Application ClassLoader）**：
    - 加载应用程序类路径（`classpath`）下的类库。





### 关于类的加载器（以JDK8版本为例）
#### 5.1 作用
类加载器负责将类的 `.class` 文件加载到内存中，并为之创建一个 `java.lang.Class` 对象。

#### 5.2 分类
类加载器主要分为两种：

1. **BootstrapClassLoader（引导类加载器、启动类加载器）**：
    - 使用C/C++语言编写，不能通过Java代码获取其实例。
    - 负责加载Java的核心库（如 `JAVA_HOME/jre/lib/rt.jar` 或 `sun.boot.class.path` 路径下的内容）。
        * rt.jar（runtime 核心类）
2. **继承于ClassLoader的类加载器**：
    - **ExtensionClassLoader（扩展类加载器）**：
        * 负责加载扩展库（如 `JAVA_HOME/jre/lib/ext` 目录下的内容）。
    - **SystemClassLoader/ApplicationClassLoader（系统类加载器、应用程序类加载器）**：
        * 负责加载应用程序类路径（`classpath`）下的类库。
    - **用户自定义类的加载器**：
        * 用户可以根据需要自定义类加载器，以实现特定的类加载逻辑。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1731925764229-5f6aa8ca-ed09-49d1-a0b1-202b46fe28f4.png)

注意，以上的加载器没有继承关系

### 继承于ClassLoader的类加载器
#### 1. ExtensionClassLoader（扩展类加载器）
+ **作用**：负责加载从 `java.ext.dirs` 系统属性所指定的目录中加载类库，或从JDK的安装目录的 `jre/lib/ext` 子目录下加载类库。

#### 2. SystemClassLoader/ApplicationClassLoader（系统类加载器、应用程序类加载器）
+ **作用**：负责加载应用程序类路径（`classpath`）下的类库。我们自定义的类，默认使用的就是这个类加载器。

#### 3. 用户自定义类的加载器
+ **作用**：用户可以根据需要自定义类加载器，以实现特定的类加载逻辑，例如实现应用的隔离（同一个类在一个应用程序中可以加载多份）和数据的加密。

### 类加载器的继承关系
虽然类加载器之间存在父子关系，但它们并不是通过继承实现的，而是通过组合关系实现的。具体来说，`ClassLoader` 类中有一个 `parent` 字段，用于指向父类加载器。

java

```plain
public class ClassLoader {
    private final ClassLoader parent;

    protected ClassLoader(ClassLoader parent) {
        this.parent = parent;
    }
}
```

### 双亲委派机制
双亲委派机制是Java类加载器的一种工作机制，确保类加载的安全性和稳定性。具体来说，当一个类加载器收到类加载请求时，它会将请求传递给它的父类加载器，直到请求到达最顶层的启动类加载器（Bootstrap ClassLoader）。如果父类加载器无法加载该类，才由当前类加载器尝试加载。

### Java双亲委派机制
**双亲委派机制**（Parent Delegation Model）是Java类加载器的一种工作机制。它的主要目的是为了保证Java类加载的安全性和稳定性。具体来说，双亲委派机制遵循以下原则：

1. **类加载请求的传递**：
    - 当一个类加载器收到类加载请求时，它不会立即尝试加载该类，而是将请求传递给它的父类加载器。
    - 这个过程会一直向上递归，直到请求到达最顶层的启动类加载器（Bootstrap ClassLoader）。
2. **类加载的执行**：
    - 启动类加载器尝试加载该类。如果成功，则返回该类的Class对象。
    - 如果启动类加载器无法加载该类，则将请求传递给它的子类加载器（即扩展类加载器）。
    - 扩展类加载器重复上述过程，直到请求传递回最初的类加载器。
3. **类加载的结果**：
    - 如果某个类加载器能够成功加载该类，则返回该类的Class对象。
    - 如果所有类加载器都无法加载该类，则抛出ClassNotFoundException异常。

### 双亲委派机制的优点
1. **安全性**：通过双亲委派机制，可以避免重复加载同一个类，确保核心类库的安全性。例如，防止自定义的`java.lang.String`类替换核心类库中的`String`类。
2. **稳定性**：通过统一的类加载机制，可以确保Java应用程序的稳定性，避免类冲突和版本不兼容问题。

### 示例代码


```plain
public class ParentDelegationDemo {
    public static void main(String[] args) {
        // 获取系统类加载器
        ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
        System.out.println("系统类加载器: " + systemClassLoader);

        // 获取扩展类加载器
        ClassLoader extClassLoader = systemClassLoader.getParent();
        System.out.println("扩展类加载器: " + extClassLoader);

        // 获取启动类加载器
        ClassLoader bootstrapClassLoader = extClassLoader.getParent();
        System.out.println("启动类加载器: " + bootstrapClassLoader); // 可能为null，因为启动类加载器是用C/C++实现的
    }
}
```







```plain
import java.lang.reflect.Field;

public class ReflectionTest {
    public void test2() throws Exception {
        // 获取Person类的Class对象
        Class<Person> clazz = Person.class;

        // 创建Person类的实例
        Person per = (Person) clazz.getDeclaredConstructor().newInstance();

        // 通过Class实例调用getDeclaredField(String fieldName)，获取运行时类指定名的属性
        Field nameField = clazz.getDeclaredField("name");

        // 确保此属性是可以访问的
        nameField.setAccessible(true);

        // 通过Field类的实例调用get(Object obj)获取属性值或set(Object obj, Object value)设置属性值
        nameField.set(per, "Tom");
        System.out.println(nameField.get(per));
    }

    public static void main(String[] args) {
        try {
            new ReflectionTest().test2();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class Person {
    private String name;
    private int age;

    public Person() {
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}
```

### 说明
1. **获取Class对象**：通过 `Class<Person> clazz = Person.class` 获取 `Person` 类的 `Class` 对象。
2. **创建实例**：通过 `clazz.getDeclaredConstructor().newInstance()` 创建 `Person` 类的实例。
3. **获取字段**：通过 `clazz.getDeclaredField("name")` 获取 `Person` 类中名为 `name` 的字段。
4. **设置字段可访问**：通过 `nameField.setAccessible(true)` 设置字段可访问。
5. **设置字段值**：通过 `nameField.set(per, "Tom")` 设置字段值。
6. **获取字段值**：通过 `System.out.println(nameField.get(per))` 获取并打印字段值。



### 调用指定的方法（步骤）
**通过Class的实例调用getDeclaredMethod(String methodName, Class<?>... parameterTypes)**：

    - 获取指定的方法。
1. java

```plain
Method method = clazz.getDeclaredMethod("methodName", String.class);
```

**setAccessible(true)**：

    - 确保此方法是可访问的。
2. java

```plain
method.setAccessible(true);
```

**通过Method实例调用invoke(Object obj, Object... args)**：

    - 调用Method对应的方法。
3. java

```plain
Object returnValue = method.invoke(obj, "argument");
```

    - 特别的：如果Method对应的方法的返回值类型为void，则invoke()返回值为null





二、企业真题

2.1 反射概述

(微*银行)

1.对反射了解吗?反射有什么好处?为什么需要反射?

类似问题:

> Java反射的作用是什么?(三*重工、上海*和网络)

>Java反射机制的作用有什么?(上海明*物联网)

反射的具体用途?(阿***芝*信用项目组)

>

2.反射的使用场合和作用、及其优缺点(*软国际)

类似问题:

>反射机制的优缺点(君*科技)

> Java反射你怎么用的?(吉*航空)



### 反射概述
#### 1. 对反射的了解
反射是Java语言的一种机制，允许程序在运行时获取有关类的信息，并且可以动态地调用类的方法、访问类的属性和创建类的实例。反射的好处在于它提供了极大的灵活性和动态性，使得程序可以在运行时进行自我检查和修改。

#### 反射的好处
+ **动态性**：可以在运行时动态地获取类的信息，调用方法和访问属性。
+ **灵活性**：可以处理未知类型和方法，适用于需要高度灵活性的场景。
+ **框架设计**：许多Java框架（如Spring、Hibernate）都大量使用反射来实现依赖注入、动态代理等功能。

#### 为什么需要反射
+ **动态代理**：反射是实现动态代理的基础，可以在运行时创建代理类并调用方法。
+ **框架设计**：反射使得框架可以在运行时动态地加载和配置类，提供高度的灵活性和可扩展性。
+ **工具开发**：反射可以用于开发通用的工具和库，如序列化、反序列化、对象拷贝等。

### 反射的使用场合和作用、及其优缺点
#### 使用场合
+ **框架设计**：如Spring、Hibernate等框架，通过反射实现依赖注入、动态代理等功能。
+ **工具开发**：如序列化、反序列化、对象拷贝等通用工具。
+ **动态代理**：通过反射实现动态代理，增强方法的功能。

#### 作用
+ **获取类信息**：可以在运行时获取类的构造器、方法、属性等信息。
+ **调用方法**：可以在运行时调用类的方法，包括私有方法。
+ **访问属性**：可以在运行时访问类的属性，包括私有属性。
+ **创建实例**：可以在运行时创建类的实例。

#### 优缺点
**优点**：

+ **灵活性高**：可以在运行时动态地获取和操作类的信息。
+ **适用范围广**：适用于框架设计、工具开发、动态代理等场景。

**缺点**：

+ **性能开销**：反射的性能较低，因为它需要在运行时进行类型检查和方法调用。
+ **安全性问题**：反射可以绕过访问控制，访问私有属性和方法，可能导致安全问题。
+ **代码复杂度**：反射代码较为复杂，不易阅读和维护。





3.实现Java反射的类有什么?(君*科技)

类似问题:

> Java反射 API 有几类?(北京*蓝)

问API。

4.反射是怎么实现的?

(上海立*网络)

2.2 Class的理解

1.Class类的作用?生成class对象的方法有哪些?(顺顺*)

2.class.forName("全路径")会调用哪些方法? 会调用构造方法吗?加载的类会放在哪?(上*

银行外包)



### 反射API的几类
#### 反射API的主要类
1. **java.lang.Class**：提供了类的元数据。
2. **java.lang.reflect.Field**：提供了对类的属性的操作。
3. **java.lang.reflect.Method**：提供了对类的方法的操作。
4. **java.lang.reflect.Constructor**：提供了对类的构造器的操作。
5. **java.lang.reflect.Array**：提供了对数组的操作。

### 反射的实现
#### 4. 反射是怎么实现的
反射通过Java的反射API实现，主要步骤如下：

1. **获取Class对象**：通过`Class.forName()`、`类名.class`或`对象.getClass()`获取Class对象。
2. **获取类的构造器、方法和属性**：通过Class对象的`getDeclaredConstructor()`、`getDeclaredMethod()`和`getDeclaredField()`方法获取类的构造器、方法和属性。
3. **调用构造器、方法和属性**：通过Constructor、Method和Field对象的`newInstance()`、`invoke()`和`get()`、`set()`方法调用类的构造器、方法和属性。

### Class的理解
#### 1. Class类的作用
Class类表示类或接口的元数据。它的作用包括：

+ 获取类的名称、修饰符、父类、接口等信息。
+ 获取类的构造器、方法和属性。
+ 创建类的实例。

#### 生成Class对象的方法
**通过类名**：

1. java

```plain
Class<Person> clazz1 = Person.class;
```

**通过对象的getClass()方法**：

2. java

```plain
Person person = new Person();
Class<? extends Person> clazz2 = person.getClass();
```

**通过Class.forName()方法**：

3. java

```plain
Class<?> clazz3 = Class.forName("com.example.Person");
```

#### 2. class.forName("全路径")会调用哪些方法
+ **加载类**：`Class.forName("全路径")` 会加载指定的类。
+ **初始化类**：默认情况下，会初始化类，执行静态代码块和静态变量的初始化。
+ **不调用构造方法**：`Class.forName()` 不会调用类的构造方法。

#### 加载的类会放在哪
+ **方法区**：加载的类会放在方法区中，方法区是JVM内存的一部分，用于存储类的元数据、常量、静态变量等



2.2 Class的理解

1.Class类的作用?生成class对象的方法有哪些?(顺*)

反射的源头。 主要有三种。

2.Class.forName("全路径")会调用哪些方法? 会调用构造方法吗?加载的类会放在哪?(上*

银行外包)

Class.forName() 会执行执行类构造器<c1init>()方法。

不会调用构造方法

加载的类放在方法区。



针对于核心 api，内部的私有的结构在 jdk17 中就不可以通过反射调用了





