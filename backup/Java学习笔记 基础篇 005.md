

## 10. 注解(Annotation)
### 10.1 注解概述
#### 10.1.1 什么是注解
注解（Annotation）是从`JDK5.0`开始引入，以“`@注解名`”在代码中存在。例如：

```java
@Override
```

```java
@Deprecated
```

```java
@SuppressWarnings(value=”unchecked”)
```

Annotation 可以像修饰符一样被使用，可用于修饰包、类、构造器、方法、成员变量、参数、局部变量的声明。还可以添加一些参数值，这些信息被保存在 Annotation 的 “name=value” 对中。

注解可以在类编译、运行时进行加载，体现不同的功能。

#### 10.1.2 注解与注释
注解也可以看做是一种注释，通过使用 Annotation，程序员可以在不改变原有逻辑的情况下，在源文件中嵌入一些补充信息。但是，注解，不同于单行注释和多行注释。

+ 对于单行注释和多行注释是给程序员看的。
+ 而注解是可以被编译器或其他程序读取的。程序还可以根据注解的不同，做出相应的处理。

#### 10.1.3 注解的重要性
在JavaSE中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在`JavaEE/Android中注解占据了更重要的角色`，例如用来配置应用程序的任何切面，代替JavaEE旧版中所遗留的`繁冗代码`和`XML配置`等。

未来的开发模式都是基于注解的，JPA是基于注解的，Spring2.5以上都是基于注解的，Hibernate3.x以后也是基于注解的，Struts2有一部分也是基于注解的了。`注解是一种趋势`，一定程度上可以说：`框架 = 注解 + 反射 + 设计模式`。





#### 介绍
注解不会直接影响代码的执行，但它们可以在编译时、类加载时或运行时被读取，并用于生成代码、编译检查、处理代码等。Java 5引入了注解，并且随着Java的发展，注解的使用变得越来越广泛。

以下是一些Java注解的基本特性和用途：

1. **元数据**：注解可以为类、方法、变量等添加额外的信息。
2. **编译时处理**：一些注解在编译时被处理，例如`@Override`，它检查被注解的方法是否确实覆盖了父类中的方法。
3. **运行时处理**：一些注解在运行时被处理，例如`@Transactional`，它用于声明事务边界。
4. **类文件处理**：注解信息可以被保留在编译后的类文件中，供反射使用。
5. **自定义注解**：除了Java自带的注解，开发者可以创建自定义注解来满足特定的需求。

Java中一些常用的注解包括：

+ `@Override`：表示一个方法声明打算重写父类中的另一个方法。
+ `@Deprecated`：表示某个程序元素（类、方法等）已经过时。
+ `@SuppressWarnings`：关闭编译器警告。
+ `@Retention`：指定注解的保留策略，可以是源代码、类文件或运行时。
+ `@Target`：指定注解可以应用于哪些Java元素（例如类、方法、变量等）。
+ `@Documented`：表示注解应该被包含在JavaDoc中。
+ `@Inherited`：允许子类继承父类中的注解。
+ `@Autowired`：Spring框架中的注解，用于自动注入依赖。
+ `@Transactional`：Spring框架中的注解，用于声明事务。

注解的基本语法如下：

```java
public @interface MyAnnotation {
    String value();
}
```

使用注解：

```java
@MyAnnotation(value = "SomeValue")
public class MyClass {
    // ...
}
```

注解可以有参数，这些参数在声明注解时必须指定。注解也可以没有参数





### 10.2 常见的Annotation作用
**示例1：生成文档相关的注解**

```java
@author 标明开发该类模块的作者，多个作者之间使用,分割
@version 标明该类模块的版本
@see 参考转向，也就是相关主题
@since 从哪个版本开始增加的
@param 对方法中某参数的说明，如果没有参数就不能写
@return 对方法返回值的说明，如果方法的返回值类型是void就不能写
@exception 对方法可能抛出的异常进行说明 ，如果方法没有用throws显式抛出的异常就不能写
```

```java
package com.annotation.javadoc;
/**
 * @author 尚硅谷-宋红康
 * @version 1.0
 * @see Math.java
 */
public class JavadocTest {
    /**
     * 程序的主方法，程序的入口
     * @param args String[] 命令行参数
     */
    public static void main(String[] args) {
    }
    
    /**
     * 求圆面积的方法
     * @param radius double 半径值
     * @return double 圆的面积
     */
    public static double getArea(double radius){
        return Math.PI * radius * radius;
    }
}

```

**示例2：在编译时进行格式检查(JDK内置的三个基本注解)**

`@Override`: 限定重写父类方法，该注解只能用于方法

`@Deprecated`: 用于表示所修饰的元素(类，方法等)已过时。通常是因为所修饰的结构危险或存在更好的选择

`@SuppressWarnings`: 抑制编译器警告

```java
package com.annotation.javadoc;
 
public class AnnotationTest{
 
    public static void main(String[] args) {
        @SuppressWarnings("unused")
        int a = 10;
    }
    @Deprecated
    public void print(){
        System.out.println("过时的方法");
    }
 
    @Override
    public String toString() {
        return "重写的toString方法()";
    }
}

```

**示例3：跟踪代码依赖性，实现替代配置文件功能**

+ Servlet3.0提供了注解(annotation)，使得不再需要在web.xml文件中进行Servlet的部署。

```java
@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;
    
    protected void doGet(HttpServletRequest request, HttpServletResponse response) { }
    
    protected void doPost(HttpServletRequest request, HttpServletResponse response) {
        doGet(request, response);
    }  
}

```

```xml
 <servlet>
    <servlet-name>LoginServlet</servlet-name>

    <servlet-class>com.servlet.LoginServlet</servlet-class>

  </servlet>

  <servlet-mapping>
    <servlet-name>LoginServlet</servlet-name>

    <url-pattern>/login</url-pattern>

  </servlet-mapping>

```

+ Spring框架中关于“事务”的管理

```java
@Transactional(propagation=Propagation.REQUIRES_NEW,isolation=Isolation.READ_COMMITTED,readOnly=false,timeout=3)
public void buyBook(String username, String isbn) {
    //1.查询书的单价
    int price = bookShopDao.findBookPriceByIsbn(isbn);
    //2. 更新库存
    bookShopDao.updateBookStock(isbn);	
    //3. 更新用户的余额
    bookShopDao.updateUserAccount(username, price);
}

```

```xml
<!-- 配置事务属性 -->
<tx:advice transaction-manager="dataSourceTransactionManager" id="txAdvice">
       <tx:attributes>
       <!-- 配置每个方法使用的事务属性 -->
       <tx:method name="buyBook" propagation="REQUIRES_NEW" 
     isolation="READ_COMMITTED"  read-only="false"  timeout="3" />
       </tx:attributes>

</tx:advice>

```

### 10.3 三个最基本的注解
#### 10.3.1 @Override
+ 用于检测被标记的方法为有效的重写方法，如果不是，则报编译错误！
+ 只能标记在方法上。
+ 它会被编译器程序读取。



#### 10.3.2 @Deprecated
+ 用于表示被标记的数据已经过时，不推荐使用。
+ 可以用于修饰 属性、方法、构造、类、包、局部变量、参数。
+ 它会被编译器程序读取。



#### 10.3.3 @SuppressWarnings
+ 抑制编译警告。当我们不希望看到警告信息的时候，可以使用 SuppressWarnings 注解来抑制警告信息
+ 可以用于修饰类、属性、方法、构造、局部变量、参数
+ 它会被编译器程序读取。
+ 可以指定的警告类型有（了解）
    - all，抑制所有警告
    - unchecked，抑制与未检查的作业相关的警告
    - unused，抑制与未用的程式码及停用的程式码相关的警告
    - deprecation，抑制与淘汰的相关警告
    - nls，抑制与非 nls 字串文字相关的警告
    - null，抑制与空值分析相关的警告
    - rawtypes，抑制与使用 raw 类型相关的警告
    - static-access，抑制与静态存取不正确相关的警告
    - static-method，抑制与可能宣告为 static 的方法相关的警告
    - super，抑制与置换方法相关但不含 super 呼叫的警告
    - ...

示例代码：

```java
package com.atguigu.annotation;

import java.util.ArrayList;

public class TestAnnotation {
    @SuppressWarnings("all")
    public static void main(String[] args) {
        int i;

        ArrayList list = new ArrayList();
        list.add("hello");
        list.add(123);
        list.add("world");

        Father f = new Son();
        f.show();
        f.methodOl();
    }
}

class Father{
    @Deprecated
    void show() {
        System.out.println("Father.show");
    }
    void methodOl() {
        System.out.println("Father Method");
    }
}

class Son extends Father{
/*	@Override
    void method01() {
        System.out.println("Son Method");
    }*/
}
```

### 10.4 元注解
JDK1.5在java.lang.annotation包定义了4个标准的meta-annotation类型，它们被用来提供对其它 annotation类型作说明。

（1）**@Target：**用于描述注解的使用范围

+ 可以通过枚举类型ElementType的10个常量对象来指定
+ TYPE，METHOD，CONSTRUCTOR，PACKAGE.....

（2）**@Retention：**用于描述注解的生命周期

+ 可以通过枚举类型RetentionPolicy的3个常量对象来指定
+ SOURCE（源代码）、CLASS（字节码）、RUNTIME（运行时）
+ `唯有RUNTIME阶段才能被反射读取到`。

（3）**@Documented**：表明这个注解应该被 javadoc工具记录。

（4）**@Inherited：**允许子类继承父类中的注解

示例代码：

```java
package java.lang;

import java.lang.annotation.*;

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {
}
```

```java
package java.lang;

import java.lang.annotation.*;
import static java.lang.annotation.ElementType.*;

@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings {
    String[] value();
}
```

```java
package java.lang;

import java.lang.annotation.*;
import static java.lang.annotation.ElementType.*;

@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(value={CONSTRUCTOR, FIELD, LOCAL_VARIABLE, METHOD, PACKAGE, PARAMETER, TYPE})
public @interface Deprecated {
}
```

> 拓展：元数据
>
> String name = "Tom";
>

### 10.5 自定义注解的使用
一个完整的注解应该包含三个部分：  
（1）声明  
（2）使用  
（3）读取

#### 10.5.1 声明自定义注解
```java
【元注解】
【修饰符】 @interface 注解名{
    【成员列表】
}
```

+ 自定义注解可以通过四个元注解@Retention,@Target，@Inherited,@Documented，分别说明它的声明周期，使用位置，是否被继承，是否被生成到API文档中。
+ Annotation 的成员在 Annotation 定义中以无参数有返回值的抽象方法的形式来声明，我们又称为配置参数。返回值类型只能是八种基本数据类型、String类型、Class类型、enum类型、Annotation类型、以上所有类型的数组
+ 可以使用 default 关键字为抽象方法指定默认返回值
+ 如果定义的注解含有抽象方法，那么使用时必须指定返回值，除非它有默认值。格式是“方法名 = 返回值”，如果只有一个抽象方法需要赋值，且方法名为value，可以省略“value=”，所以如果注解只有一个抽象方法成员，建议使用方法名value。

```java
package com.atguigu.annotation;

import java.lang.annotation.*;

@Inherited
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Table {
    String value();
}
```

```java
package com.atguigu.annotation;

import java.lang.annotation.*;

@Inherited
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface Column {
    String columnName();
    String columnType();
}
```

#### 10.5.2 使用自定义注解
```java
package com.atguigu.annotation;

@Table("t_stu")
public class Student {
    @Column(columnName = "sid",columnType = "int")
    private int id;
    @Column(columnName = "sname",columnType = "varchar(20)")
    private String name;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}

```

#### 10.5.3 读取和处理自定义注解
自定义注解必须配上注解的信息处理流程才有意义。

我们自己定义的注解，只能使用反射的代码读取。所以自定义注解的声明周期必须是RetentionPolicy.RUNTIME。

具体的使用见`《尚硅谷_宋红康_第17章_反射机制.md》`。

### 10.6 JUnit单元测试
#### 10.6.1 测试分类
**黑盒测试：**不需要写代码，给输入值，看程序是否能够输出期望的值。 

**白盒测试：**需要写代码的。关注程序具体的执行流程。

![](images/image-20220524102038600.png)

#### 10.6.2 JUnit单元测试介绍
JUnit 是由 Erich Gamma 和 Kent Beck 编写的一个测试框架（regression testing framework），供Java开发人员编写单元测试之用。

**JUnit测试是程序员测试，即所谓白盒测试，因为程序员知道被测试的软件如何（How）完成功能和完成什么样（What）的功能。**

要使用JUnit，必须在项目的编译路径中`引入JUnit的库`，即相关的.class文件组成的jar包。jar就是一个压缩包，压缩包都是开发好的第三方（Oracle公司第一方，我们自己第二方，其他都是第三方）工具类，都是以class文件形式存在的。

#### 10.6.3 引入本地JUnit.jar
第1步：在项目中File-Project Structure中操作：添加Libraries库

![](images/image-20221002195547325.png)

其中，junit-libs包内容如下：

![](images/image-20220813005206452.png)

第2步：选择要在哪些module中应用JUnit库

![](images/image-20220813005511062.png)

第3步：检查是否应用成功

![](images/image-20220813005729233.png)

**注意Scope：选择Compile，否则编译时，无法使用JUnit。**

第4步：下次如果有新的模块要使用该libs库，这样操作即可

![](images/image-20220813005944022.png)

![](images/image-20220813010018152.png)

![](images/image-20220813010055217.png)

![](images/image-20220813010124381.png)

#### 10.6.4 编写和运行@Test单元测试方法
JUnit4版本，要求@Test标记的方法必须满足如下要求：

+ 所在的类必须是public的，非抽象的，包含唯一的无参构造器。
+ @Test标记的方法本身必须是public，非抽象的，非静态的，void无返回值，()无参数的。

```java
package com.atguigu.junit;

import org.junit.Test;

public class TestJUnit {
    @Test
    public void test01(){
        System.out.println("TestJUnit.test01");
    }

    @Test
    public void test02(){
        System.out.println("TestJUnit.test02");
    }

    @Test
    public void test03(){
        System.out.println("TestJUnit.test03");
    }
}
```

![](images/image-20220106152412245.png)

#### 10.6.5 设置执行JUnit用例时支持控制台输入
**1. 设置数据：**

默认情况下，在单元测试方法中使用Scanner时，并不能实现控制台数据的输入。需要做如下设置：

在`idea64.exe.vmoptions配置文件`中加入下面一行设置，重启idea后生效。

```properties
-Deditable.java.test.console=true
```

**2. 配置文件位置：**

![](images/image-20220813011625546.png)

![](images/image-20220813011642180.png)

添加完成之后，重启IDEA即可。

**3. 如果上述位置设置不成功，需要继续修改如下位置**

修改位置1：IDEA安装目录的bin目录（例如：`D:\develop_tools\IDEA\IntelliJ IDEA 2022.1.2\bin`）下的idea64.exe.vmoptions文件。 

修改位置2：C盘的用户目录`C:\Users\用户名\AppData\Roaming\JetBrains\IntelliJIdea2022.1` 下的idea64.exe.vmoptions`件。

#### 10.6.6 定义test测试方法模板
选中自定义的模板组，点击”+”（1.Live Template）来定义模板。

![](images/image-20211229100040505.png)

框架 = 注解 + 反射 + 设计模式











## 11. 包装类
```java
public class WrapperTest {
    public static void main(String[] args) {
        //基本数据类型->包装类
        int num1 = 10;
        //将基本数据类型int转换为包装类Integer
        Integer integer = num1;
        //输出包装类Integer的字符串表示
        System.out.println(integer.toString());
        //输出包装类Integer的值
        System.out.println(integer);

        //包装类->基本数据类型
        Integer integer1 = new Integer(100);
        //将包装类Integer转换为基本数据类型int
        int num2 = integer1.intValue();
        //输出基本数据类型int的值
        System.out.println(num2);

        boolean b = true;
        //将基本数据类型boolean转换为包装类Boolean
        Boolean boolean1 = b;
        //输出包装类Boolean的字符串表示
        System.out.println(boolean1.toString());
        //输出包装类Boolean的值
        System.out.println(boolean1);

        Boolean boolean2 = new Boolean(true);
        //将包装类Boolean转换为基本数据类型boolean
        boolean b1 = boolean2.booleanValue();
        //输出基本数据类型boolean的值
        System.out.println(b1);

        String str = "false";
        //将字符串转换为包装类Boolean
        Boolean boolean3 = Boolean.valueOf(str);
        //输出包装类Boolean的值
        System.out.println(boolean3);

        String str1 = "123";
        //将字符串转换为包装类Boolean
        Boolean boolean4 = Boolean.valueOf(str1);
        System.out.println(boolean4);//输出为false
        //只要不是true 就转化为false

        String str2 = "True";
        //将字符串转换为包装类Boolean
        Boolean boolean5 = Boolean.valueOf(str2);
        System.out.println(boolean5);//输出为true

    }
}
```

```java
//包装类转化为基本数据类型
        int num3 = boolean5.intValue();
        System.out.println(num3);//输出为1
```

### 11.1 为什么需要包装类
Java提供了两个类型系统，`基本数据类型`与`引用数据类型`。使用基本数据类型在于效率，然而当要使用只针对对象设计的API或新特性（例如泛型），怎么办呢？例如：



为了使得基本数据类型的变量具有引用数据类型的特征（比如 封装性 多态性），我们给各个基本类型都提供包装类以获得引用数据类型的特征

#### 为什么需要转换
> 一方面，在有些场景下，需要基本数据类型对应的包装类的对象。此时就需要将基本数据类型变量转换为包装类的对象
>
> 比如
>
> ArrayList 的 add(Object obj); Object 类的 equals(Object obj)
>

> 对于包装类来讲，既然使用的是对象，那么对象是不能进行加减乘除运算的，为了能进行运算，我们就需要将它转化为基本数据类型
>



#### 包装类的命名一般为基本数据类型首字母大写
+ byte - Byte
+ short - Short
+ long - Long
+ float - Float
+ double - Double
+ boolean - Boolean

#### 特殊
+ int - Integer
+ char - Char



```java
//情况1：方法形参
Object类的equals(Object obj)

//情况2：方法形参
ArrayList类的add(Object obj)
//没有如下的方法：
add(int number)
add(double d)
add(boolean b)

//情况3：泛型
Set<T>
List<T>
Cllection<T>
Map<K,V>
```

### 11.2 有哪些包装类
Java针对八种基本数据类型定义了相应的引用类型：包装类（封装类）。有了类的特点，就可以调用类中的方法，Java才是真正的面向对象。

封装以后的，内存结构对比：

```java
public static void main(String[] args){
    int num = 520;
    Integer obj = new Integer(520);
}
```

### 11.3 自定义包装类
```java
public class MyInteger {
    int value;

    public MyInteger() {
    }

    public MyInteger(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return String.valueOf(value);
    }
}

```

### 11.4 包装类与基本数据类型间的转换
```java
public class WaperTest {
    public static void main(String[] args) {
        //基本数据类型，包装类 -> String类型
        //方式一
        
        int a = 10;
        //将基本数据类型a转换为字符串类型
        String str = a + "";
        System.out.println(str);

        //方式二
        //将基本数据类型a转换为字符串类型
        String str1 = String.valueOf(a);
        System.out.println(str1);

        //String转化为基本数据类型
        //调用包装类的parseXxx方法
        String str2 = "123";
        //将字符串类型str2转换为int类型
        int i = Integer.parseInt(str2);
        System.out.println(i);
        
    }
}
```

#### 11.4.1 装箱
 **装箱：把基本数据类型转为包装类对象**

> 转为包装类的对象，是为了使用专门为对象设计的API和特性
>

基本数值---->包装对象

```java
Integer obj1 = new Integer(4);//使用构造函数函数
Float f = new Float(“4.56”);
Long l = new Long(“asdf”);  //NumberFormatException

Integer obj2 = Integer.valueOf(4);//使用包装类中的valueOf方法
```

#### 11.4.2 拆箱
**拆箱：把包装类对象拆为基本数据类型**

> 转为基本数据类型，一般是因为需要运算，Java中的大多数运算符是为基本数据类型设计的。比较、算术等
>

包装对象---->基本数值

```java
Integer obj = new Integer(4);
int num1 = obj.intValue();
```

**自动装箱与拆箱：**

由于我们经常要做基本类型与包装类之间的转换，从`JDK5.0 `开始，基本类型与包装类的装箱、拆箱动作可以自动完成。例如：

```java
Integer i = 4;//自动装箱。相当于Integer i = Integer.valueOf(4);
i = i + 5;//等号右边：将i对象转成基本数值(自动拆箱) i.intValue() + 5;
//加法运算完成后，再次装箱，把基本数值转成对象。
```

> 注意：只能与自己对应的类型之间才能实现自动装箱与拆箱。
>

```java
Integer i = 1;
Double d = 1;//错误的，1是int类型
```

### 11.5 基本数据类型、包装类与字符串间的转换
**（1）基本数据类型转为字符串**

**方式1：**调用字符串重载的valueOf()方法

```java
int a = 10;
//String str = a;//错误的

String str = String.valueOf(a);
```

**方式2：**更直接的方式

```java
int a = 10;

String str = a + "";
```

**（2）字符串转为基本数据类型**

**方式1：**除了Character类之外，其他所有包装类都具有parseXxx静态方法可以将字符串参数转换为对应的基本类型，例如：

+ `public static int parseInt(String s)`：将字符串参数转换为对应的int基本类型。
+ `public static long parseLong(String s)`：将字符串参数转换为对应的long基本类型。
+ `public static double parseDouble(String s)`：将字符串参数转换为对应的double基本类型。

**方式2：**字符串转为包装类，然后可以自动拆箱为基本数据类型

+ ```public static Integer valueOf(String s)```：将字符串参数转换为对应的Integer包装类，然后可以自动拆箱为int基本类型
+ ```public static Long valueOf(String s)```：将字符串参数转换为对应的Long包装类，然后可以自动拆箱为long基本类型
+ ```public static Double valueOf(String s)```：将字符串参数转换为对应的Double包装类，然后可以自动拆箱为double基本类型

注意:如果字符串参数的内容无法正确转换为对应的基本类型，则会抛出`java.lang.NumberFormatException`异常。

**方式3：**通过包装类的构造器实现

```java
int a = Integer.parseInt("整数的字符串");
double d = Double.parseDouble("小数的字符串");
boolean b = Boolean.parseBoolean("true或false");

int a = Integer.valueOf("整数的字符串");
double d = Double.valueOf("小数的字符串");
boolean b = Boolean.valueOf("true或false");

int i = new Integer(“12”);

```



```java

```

其他方式小结：

![](images/image-20220813012801907.png)

### 11.6 包装类的其它API
#### 11.6.1 数据类型的最大最小值
```java
Integer.MAX_VALUE和Integer.MIN_VALUE
    
Long.MAX_VALUE和Long.MIN_VALUE
    
Double.MAX_VALUE和Double.MIN_VALUE
```

#### 11.6.2 字符转大小写
```java
Character.toUpperCase('x');

Character.toLowerCase('X');
```

#### 11.6.3 整数转进制
```java
Integer.toBinaryString(int i) 
    
Integer.toHexString(int i)
    
Integer.toOctalString(int i)
```

#### 11.6.4 比较的方法
```java
Double.compare(double d1, double d2)
    
Integer.compare(int x, int y) 
```

### 11.7 包装类对象的特点
#### 11.7.1 包装类缓存对象
| 包装类 | 缓存对象 |
| --- | --- |
| Byte | -128~127 |
| Short | -128~127 |
| Integer | -128~127 |
| Long | -128~127 |
| Float | 没有 |
| Double | 没有 |
| Character | 0~127 |
| Boolean | true和false |


```java
Integer a = 1;
Integer b = 1;
System.out.println(a == b);//true

Integer i = 128;
Integer j = 128;
System.out.println(i == j);//false

Integer m = new Integer(1);//新new的在堆中
Integer n = 1;//这个用的是缓冲的常量对象，在方法区
System.out.println(m == n);//false

Integer x = new Integer(1);//新new的在堆中
Integer y = new Integer(1);//另一个新new的在堆中
System.out.println(x == y);//false
```

```java
Double d1 = 1.0;
Double d2 = 1.0;
System.out.println(d1==d2);//false 比较地址，没有缓存对象，每一个都是新new的
```

#### 11.7.2 类型转换问题
```java
Integer i = 1000;
double j = 1000;
System.out.println(i==j);//true  会先将i自动拆箱为int，然后根据基本数据类型“自动类型转换”规则，转为double比较
```

```java
Integer i = 1000;
int j = 1000;
System.out.println(i==j);//true 会自动拆箱，按照基本数据类型进行比较
```

```java
Integer i = 1;
Double d = 1.0
System.out.println(i==d);//编译报错
```

#### 11.7.3 包装类对象不可变
```java
public class TestExam {
    public static void main(String[] args) {
        int i = 1;
        Integer j = new Integer(2);
        Circle c = new Circle();
        change(i,j,c);
        System.out.println("i = " + i);//1
        System.out.println("j = " + j);//2
        System.out.println("c.radius = " + c.radius);//10.0
    }
    
    /*
     * 方法的参数传递机制：
     * （1）基本数据类型：形参的修改完全不影响实参
     * （2）引用数据类型：通过形参修改对象的属性值，会影响实参的属性值
     * 这类Integer等包装类对象是“不可变”对象，即一旦修改，就是新对象，和实参就无关了
     */
    public static void change(int a ,Integer b,Circle c ){
        a += 10;
//		b += 10;//等价于  b = new Integer(b+10);
        c.radius += 10;
        /*c = new Circle();
        c.radius+=10;*/
    }
}
class Circle{
    double radius;
}
```

### 11.8 练习
笔试题：如下两个题目输出结果相同吗？各是什么。

```java
Object o1 = true ? new Integer(1) : new Double(2.0);
System.out.println(o1);//1.0

```

```java
Object o2;
if (true)
    o2 = new Integer(1);
else
    o2 = new Double(2.0);
System.out.println(o2);//1

```

面试题：

```java
public void method1() {
    Integer i = new Integer(1);
    Integer j = new Integer(1);
    System.out.println(i == j);

    Integer m = 1;
    Integer n = 1;
    System.out.println(m == n);//

    Integer x = 128;
    Integer y = 128;
    System.out.println(x == y);//
}

```

练习：

利用Vector代替数组处理：从键盘读入学生成绩（以负数代表输入结束），找出最高分，并输出学生成绩等级。

+ 提示：数组一旦创建，长度就固定不变，所以在创建数组前就需要知道它的长度。而向量类java.util.Vector可以根据需要动态伸缩。
+ 创建Vector对象：Vector v=new Vector();
+ 给向量添加元素：v.addElement(Object obj);  //obj必须是对象
+ 取出向量中的元素：Object obj=v.elementAt(0);
    - 注意第一个元素的下标是0，返回值是Object类型的。
+ 计算向量的长度：v.size();
+ 若与最高分相差10分内：A等；20分内：B等；30分内：C等；其它：D等

```java
import java.util.Scanner;
import java.util.Vector;

public class ScoreTest {

    public static void main(String[] args) {/*...*/
        //创建Vector对象
        Vector v = new Vector();
        //从键盘获取多个学生成绩
        Scanner input = new Scanner(System.in);
        int Max = 0;
        while (true) {
            //输入学生成绩，直到负数结束
            int score = input.nextInt();
            if (score < 0) {
                break;
            }

            //将学生成绩添加到Vector中
            v.add(score);

            if (score > Max) {
                Max = score;
            }
        }
        input.close();
        //输出Vector中所有学生成绩
        for (int i = 0; i < v.size(); i++) {
            //拆箱
            Object obj = v.get(i);
            int score = (Integer) obj;
            System.out.println(score);

            //System.out.println(v.get(i));
            if (Max - score < 10) {
                System.out.println("A");
            } else if (Max - score < 20) {
                System.out.println("B");
            } else if (Max - score < 30) {
                System.out.println("C");
            } else {
                System.out.println("D");
            }

            System.out.println("Student" + i + " score is " + score);
        }
        System.out.println("Max score is " + Max);
    }

}
```











## 1. 异常概述
### 1.1 什么是生活的异常
男主角小明每天开车上班，正常车程1小时。但是，不出意外的话，可能会出现意外。

![](images/image-20220814203918560.png)

出现意外，即为异常情况。我们会做相应的处理。如果不处理，到不了公司。处理完了，就可以正常开车去公司。



4.异常的体系结构

java.lang.Throwable:异常体系的根父类

1-java.ang.Error:错误。Java虛拟机无法解决的严重问题。如:JVM系统内部错误、资源耗尽等严重情况。

一般不编写针对性的代码进行处理。

----StackOverflowError、0utOfMemoryError

---java.lang.Exception:异常。我们可以编写针对性的代码进行处理。

----编译时异常:(受检异常)在执行javac.exe命令时，出现的异常

----运行时异常:(非受检异常)在执行java.exe命令时，出现的异常，



Java异常处理是Java程序中非常重要的一部分，它允许程序在发生错误时不会立即崩溃，而是能够优雅地处理错误或异常情况。Java异常处理机制基于几个关键概念和组件：

### 1. 异常类
Java中的所有异常都是`Throwable`类的子类。`Throwable`有两个重要的子类：`Exception`（可检查异常）和`Error`（系统错误）。

+ **Error**：通常是JVM无法处理的问题，比如`OutOfMemoryError`。这些错误通常不推荐在代码中进行捕获。
+ **Exception**：可以被程序处理的异常，分为可检查异常（checked exceptions）和非检查异常（unchecked exceptions）。
    - **可检查异常**：必须在编译时处理的异常，比如`IOException`、`SQLException`等。
    - **非检查异常**：不需要强制处理的异常，通常是程序逻辑错误，比如`NullPointerException`、`ArithmeticException`等。

### 2. 异常处理关键字
+ **try**：用于包裹可能发生异常的代码块。
+ **catch**：用于捕获并处理try块中发生的特定类型的异常。
+ **finally**：无论是否发生异常，finally块中的代码都会执行，常用于资源清理。
+ **throw**：用于手动抛出异常。
+ **throws**：用于声明方法可能抛出的异常类型。

### 3. 异常处理流程
1. **抛出异常**：当异常发生时，JVM会抛出一个异常实例。
2. **捕获异常**：可以使用try-catch语句捕获异常。
3. **处理异常**：在catch块中处理异常，比如打印错误信息、记录日志、恢复操作等。
4. **资源清理**：在finally块中进行资源清理，如关闭文件流或数据库连接。

### 4. 异常处理示例
```java
try {
    // 可能抛出异常的代码
    int division = 10 / 0;
} catch (ArithmeticException e) {
    // 处理除以零的异常
    System.out.println("Cannot divide by zero!");
} finally {
    // 资源清理代码
    System.out.println("Cleanup resources");
}
```

### 5. 自定义异常
你可以创建自己的异常类来表示特定的错误情况，这通常是通过继承`Exception`类或其子类来实现的。

```java
public class MyCustomException extends Exception {
    public MyCustomException(String message) {
        super(message);
    }
}
```

### 6. 异常传播
+ **声明异常**：使用`throws`关键字声明方法可能抛出的异常。
+ **传播异常**：方法可以将异常传递给调用者处理。

### 7. 异常链
当一个异常的处理器中又抛出了另一个异常时，可以使用`Throwable`类的`initCause`方法将原始异常设置为新异常的原因，这样可以保留原始异常的信息。





### 1.2 什么是程序的异常
在使用计算机语言进行项目开发的过程中，即使程序员把代码写得`尽善尽美`，在系统的运行过程中仍然会遇到一些问题，因为很多问题不是靠代码能够避免的，比如：`客户输入数据的格式问题`，`读取文件是否存在`，`网络是否始终保持通畅`等等。

+ **异常** ：指的是程序在执行过程中，出现的非正常情况，如果不处理最终会导致JVM的非正常停止。

> 异常指的并不是语法错误和逻辑错误。语法错了，编译不通过，不会产生字节码文件，根本不能运行。
>
> 代码逻辑错误，只是没有得到想要的结果，例如：求a与b的和，你写成了a-b
>

### 1.3 异常的抛出机制
Java中是如何表示不同的异常情况，又是如何让程序员得知，并处理异常的呢？

Java中把不同的异常用不同的类表示，一旦发生某种异常，就`创建该异常类型的对象`，并且抛出（throw）。然后程序员可以捕获(catch)到这个异常对象，并处理；如果没有捕获(catch)这个异常对象，那么这个异常对象将会导致程序终止。

举例：

运行下面的程序，程序会产生一个数组角标越界异常`ArrayIndexOfBoundsException`。我们通过图解来解析下异常产生和抛出的过程。

```java
public class ArrayTools {
    // 对给定的数组通过给定的角标获取元素。
    public static int getElement(int[] arr, int index) {
        int element = arr[index];
        return element;
    }
}
```

 测试类

```java
public class ExceptionDemo {
    public static void main(String[] args) {
        int[] arr = { 34, 12, 67 };
        intnum = ArrayTools.getElement(arr, 4)
        System.out.println("num=" + num);
        System.out.println("over");
    }
}
```

上述程序执行过程图解：

![](images/异常产生过程.png)

### 1.4 如何对待异常
 对于程序出现的异常，一般有两种解决方法：一是遇到错误就终止程序的运行。另一种方法是程序员在编写程序时，就充分考虑到各种可能发生的异常和错误，极力预防和避免。实在无法避免的，要编写相应的代码进行异常的检测、以及`异常的处理`，保证代码的`健壮性`。

## 2. Java异常体系
### 2.1 Throwable
`java.lang.Throwable` 类是Java程序执行过程中发生的异常事件对应的类的**根父类**。

**Throwable中的常用方法：**

+ `public void printStackTrace()`：打印异常的详细信息。包含了异常的类型、异常的原因、异常出现的位置、在开发和调试阶段都得使用printStackTrace。
+ `public String getMessage()`：获取发生异常的原因。

### 2.2 Error 和 Exception
Throwable可分为两类：Error和Exception。分别对应着`java.lang.Error`与`java.lang.Exception`两个类。

**Error：**Java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源耗尽等严重情况。一般不编写针对性的代码进行处理。

+ 例如：StackOverflowError（栈内存溢出）和OutOfMemoryError（堆内存溢出，简称OOM）。

**Exception:** 其它因编程错误或偶然的外在因素导致的一般性问题，需要使用针对性的代码进行处理，使程序继续运行。否则一旦发生异常，程序也会挂掉。例如：

+ 空指针访问
+ 试图读取不存在的文件
+ 网络连接中断
+ 数组角标越界

> 说明：
>
> 1. 无论是Error还是Exception，还有很多子类，异常的类型非常丰富。当代码运行出现异常时，特别是我们不熟悉的异常时，不要紧张，把异常的简单类名，拷贝到API中去查去认识它即可。
> 2. 我们本章讲的异常处理，其实针对的就是Exception。
>

### 2.3 编译时异常和运行时异常
Java程序的执行分为编译时过程和运行时过程。有的错误只有在`运行时`才会发生。比如：除数为0，数组下标越界等。

因此，根据异常可能出现的阶段，可以将异常分为：

+ **编译时期异常**（即checked异常、受检异常）：在代码编译阶段，编译器就能明确`警示`当前代码`可能发生（不是一定发生）`xx异常，并`明确督促`程序员提前编写处理它的代码。如果程序员`没有编写`对应的异常处理代码，则编译器就会直接判定编译失败，从而不能生成字节码文件。通常，这类异常的发生不是由程序员的代码引起的，或者不是靠加简单判断就可以避免的，例如：FileNotFoundException（文件找不到异常）。
+ **运行时期异常**（即runtime异常、unchecked异常、非受检异常）：在代码编译阶段，编译器完全不做任何检查，无论该异常是否会发生，编译器都不给出任何提示。只有等代码运行起来并确实发生了xx异常，它才能被发现。通常，这类异常是由程序员的代码编写不当引起的，只要稍加判断，或者细心检查就可以避免。
    - **java.lang.RuntimeException**类及它的子类都是运行时异常。比如：ArrayIndexOutOfBoundsException数组下标越界异常，ClassCastException类型转换异常。

![](images/1562771528807.png)

## 3. 常见的错误和异常
### 3.1 Error
最常见的就是VirtualMachineError，它有两个经典的子类：StackOverflowError、OutOfMemoryError。

```java
package com.atguigu.exception;

import org.junit.Test;

public class TestStackOverflowError {
    @Test
    public void test01(){
        //StackOverflowError
        recursion();
    }

    public void recursion(){ //递归方法
        recursion(); 
    }
}

```

```java
package com.atguigu.exception;

import org.junit.Test;

public class TestOutOfMemoryError {
    @Test
    public void test02(){
        //OutOfMemoryError
        //方式一：
        int[] arr = new int[Integer.MAX_VALUE];
    }
    @Test
    public void test03(){
        //OutOfMemoryError
        //方式二：
        StringBuilder s = new StringBuilder();
        while(true){
            s.append("atguigu");
        }
    }
}

```

### 3.2 运行时异常
```java
package com.atguigu.exception;

import org.junit.Test;

import java.util.Scanner;

public class TestRuntimeException {
    @Test
    public void test01(){
        //NullPointerException
        int[][] arr = new int[3][];
        System.out.println(arr[0].length);
    }

    @Test
    public void test02(){
        //ClassCastException
        Object obj = 15;
        String str = (String) obj;
    }

    @Test
    public void test03(){
        //ArrayIndexOutOfBoundsException
        int[] arr = new int[5];
        for (int i = 1; i <= 5; i++) {
            System.out.println(arr[i]);
        }
    }

    @Test
    public void test04(){
        //InputMismatchException
        Scanner input = new Scanner(System.in);
        System.out.print("请输入一个整数：");//输入非整数
        int num = input.nextInt();
        input.close();
    }

    @Test
    public void test05(){
        int a = 1;
        int b = 0;
        //ArithmeticException
        System.out.println(a/b);
    }
}

```

### 3.3 编译时异常
```java
package com.atguigu.exception;

import org.junit.Test;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class TestCheckedException {
    @Test
    public void test06() {
        Thread.sleep(1000);//休眠1秒  InterruptedException
    }

    @Test
    public void test07(){
        Class c = Class.forName("java.lang.String");//ClassNotFoundException
    }

    @Test
    public void test08() {
        Connection conn = DriverManager.getConnection("....");  //SQLException
    }
    @Test
    public void test09()  {
        FileInputStream fis = new FileInputStream("尚硅谷Java秘籍.txt"); //FileNotFoundException
    }
    @Test
    public void test10() {
        File file = new File("尚硅谷Java秘籍.txt");
        FileInputStream fis = new FileInputStream(file);//FileNotFoundException
        int b = fis.read();//IOException
        while(b != -1){
            System.out.print((char)b);
            b = fis.read();//IOException
        }
        
        fis.close();//IOException
    }
}
```

## 4. 异常的处理
### 4.1 异常处理概述
在编写程序时，经常要在可能出现错误的地方加上检测的代码，如进行x/y运算时，要`检测分母为0`，`数据为空`，`输入的不是数据而是字符`等。过多的if-else分支会导致程序的`代码加长`、`臃肿`，`可读性差`，程序员需要花很大的精力“`堵漏洞`”。因此采用异常处理机制。

**Java异常处理**

Java采用的异常处理机制，是`将异常处理的程序代码集中在一起`，与正常的程序代码分开，使得程序简洁、优雅，并易于维护。

**Java异常处理的方式：**

方式一：try-catch-finally

方式二：throws + 异常类型

![](images/image-20220331111051496.png)

### 4.2 方式1：捕获异常（try-catch-finally）
Java提供了异常处理的**抓抛模型**。

+ 前面提到，Java程序的执行过程中如出现异常，会生成一个异常类对象，该异常对象将被提交给Java运行时系统，这个过程称为`抛出(throw)异常`。
+ 如果一个方法内抛出异常，该异常对象会被抛给调用者方法中处理。如果异常没有在调用者方法中处理，它继续被抛给这个调用方法的上层方法。这个过程将一直继续下去，直到异常被处理。这一过程称为`捕获(catch)异常`。
+ 如果一个异常回到main()方法，并且main()也不处理，则程序运行终止。

#### 4.2.1 try-catch-finally基本格式
捕获异常语法如下：

```java
try{
    ......	//可能产生异常的代码
}
catch( 异常类型1 e ){
    ......	//当产生异常类型1型异常时的处置措施
}
catch( 异常类型2 e ){
    ...... 	//当产生异常类型2型异常时的处置措施
}  
finally{
    ...... //无论是否发生异常，都无条件执行的语句
} 

```

**1、整体执行过程：**

当某段代码可能发生异常，不管这个异常是编译时异常（受检异常）还是运行时异常（非受检异常），我们都可以使用try块将它括起来，并在try块下面编写catch分支尝试捕获对应的异常对象。

+ 如果在程序运行时，try块中的代码没有发生异常，那么catch所有的分支都不执行。
+ 如果在程序运行时，try块中的代码发生了异常，根据异常对象的类型，将从上到下选择第一个匹配的catch分支执行。此时try中发生异常的语句下面的代码将不执行，而整个try...catch之后的代码可以继续运行。
+ 如果在程序运行时，try块中的代码发生了异常，但是所有catch分支都无法匹配（捕获）这个异常，那么JVM将会终止当前方法的执行，并把异常对象“抛”给调用者。如果调用者不处理，程序就挂了。

**2、try**

+ 捕获异常的第一步是用`try{…}语句块`选定捕获异常的范围，将可能出现异常的业务逻辑代码放在try语句块中。

**3、catch (Exceptiontype e)**

+ catch分支，分为两个部分，catch()中编写异常类型和异常参数名，{}中编写如果发生了这个异常，要做什么处理的代码。
+ 如果明确知道产生的是何种异常，可以用该异常类作为catch的参数；也可以用其父类作为catch的参数。比如：可以用ArithmeticException类作为参数的地方，就可以用RuntimeException类作为参数，或者用所有异常的父类Exception类作为参数。但不能是与ArithmeticException类无关的异常，如NullPointerException（catch中的语句将不会执行）。
+ 每个try语句块可以伴随一个或多个catch语句，用于处理可能产生的不同类型的异常对象。
+ 如果有多个catch分支，并且多个异常类型有父子类关系，必须保证小的子异常类型在上，大的父异常类型在下。否则，报错。
+ catch中常用异常处理的方式
    - `public String getMessage()`：获取异常的描述信息，返回字符串
    - `public void printStackTrace()`：打印异常的跟踪栈信息并输出到控制台。包含了异常的类型、异常的原因、还包括异常出现的位置，在开发和调试阶段，都得使用printStackTrace()。

将可能出现异常的代码声明在try语句中。一旦代码出现异常，就会自动生成一个对应异常类的对象。并将此对象抛出。

针对于try中抛出的异常类的对象，使用之后的catch语句进行匹配。一旦匹配上，就进入catch语句块进行处理。

一旦处理接触，代码就可继续向下执行

如果声明了多个 catch 结构 ，不同的异常类型在不存在的子父类关系的情况下，声明前后顺序无所谓，但是若满足父类关系，要将父类声明在子类下面，否则编译报错



catch 中异常的处理方式

1， 自己编写输出语句

2， printStackTrace() 打印异常的详细信息（推荐 用的多）

3 ， getMessage() 获取发生异常的原因



其它说明

 try 中声明的变量出来 try 就无法调用



开发体会:

> 对于运行时异常:  
开发中，通常就不进行显示的处理了，  
一旦在程序执行中，出现了运行时异常，那么就根据异常的提示信息修改代码即可  
对于编译时异常:  
一定要进行处理。否则编译不通过。
>

#### 4.2.2 使用举例
举例1：

```java
public class IndexOutExp {
    public static void main(String[] args) {
        String friends[] = { "lisa", "bily", "kessy" };
        try {
            for (int i = 0; i < 5; i++) {
            System.out.println(friends[i]);
            }
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("index err");
        }
        System.out.println("\nthis is the end");
    }
}

```

举例2：

```java
public class DivideZero1 {
    int x;
    public static void main(String[] args) {
        int y;
        DivideZero1 c = new DivideZero1();
        try {
            y = 3 / c.x;
        } catch (ArithmeticException e) {
            System.out.println("divide by zero error!");
        }
        System.out.println("program ends ok!");
    }
}

```

举例3：

```java
@Test
public void test1(){
    try{
        String str1 = "atguigu.com";
        str1 = null;
        System.out.println(str1.charAt(0));
    }catch(NullPointerException e){
        //异常的处理方式1
        System.out.println("不好意思，亲~出现了小问题，正在加紧解决...");	
    }catch(ClassCastException e){
        //异常的处理方式2
        System.out.println("出现了类型转换的异常");
    }catch(RuntimeException e){
        //异常的处理方式3
        System.out.println("出现了运行时异常");
    }
    //此处的代码，在异常被处理了以后，是可以正常执行的
    System.out.println("hello");
}
```

举例4：

```java

```

#### 4.2.3 finally使用及举例


finally的使用说明:

finally的理解

我们将一定要被执行的代码声明在finally结构中。

更深刻的理解:无论try中或catch中是否存在仍未被处理的异常，无论try中或catch中是否存在return语句等，finally

中声明的语句都一定要被执行，

但有一个例外 System.exit(0)会强行终止 java 虚拟机



+ 因为异常会引发程序跳转，从而会导致有些语句执行不到。而程序中有一些特定的代码无论异常是否发生，都`需要执行`。例如，数据库连接、输入流输出流、Socket连接、Lock锁的关闭等，这样的代码通常就会放到finally块中。所以，我们通常将一定要被执行的代码声明在finally中。
    - 唯一的例外，使用 System.exit(0) 来终止当前正在运行的 Java 虚拟机。
+ 不论在try代码块中是否发生了异常事件，catch语句是否执行，catch语句是否有异常，catch语句中是否有return，finally块中的语句都会被执行。
+ finally语句和catch语句是可选的，但finally不能单独使用。



什么样的代码我们一定要声明在finally中呢?

> 我们在开发中，有一些资源(比如:输入流、输出流，数据库连接、Socket连接等资源)，在使用完以后，必须显式的进行  
关闭操作，否则，GC不会自动的回收这些资源。进而导致内存的泄漏。  
为了保证这些资源在使用完以后，不管是否出现了未被处理的异常的情况下，这些资源能被关闭。我们必须将这些操作声明  
在finally中!
>



```java
try{
     
}finally{
    
} 
```

举例1：确保资源关闭

```java
package com.atguigu.keyword;

import java.util.InputMismatchException;
import java.util.Scanner;

public class TestFinally {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        try {
            System.out.print("请输入第一个整数：");
            int a = input.nextInt();
            System.out.print("请输入第二个整数：");
            int b = input.nextInt();
            int result = a/b;
            System.out.println(a + "/" + b +"=" + result);
        } catch (InputMismatchException e) {
            System.out.println("数字格式不正确，请输入两个整数");
        }catch (ArithmeticException e){
            System.out.println("第二个整数不能为0");
        } finally {
            System.out.println("程序结束，释放资源");
            input.close();
        }
    }
    
    @Test
    public void test1(){
        FileInputStream fis = null;
        try{
            File file = new File("hello1.txt");
            fis = new FileInputStream(file);//FileNotFoundException
            int b = fis.read();//IOException
            while(b != -1){
                System.out.print((char)b);
                b = fis.read();//IOException
            }

        }catch(IOException e){
            e.printStackTrace();
        }finally{
            try {
                if(fis != null)
                    fis.close();//IOException
            } catch (IOException e) {
                e.printStackTrace();
            }	
        }
    }
}
```

举例2：从try回来

```java
public class FinallyTest1 {
    public static void main(String[] args) {
        int result = test("12");
        System.out.println(result);
    }

    public static int test(String str){
        try{
            Integer.parseInt(str);
            return 1;
        }catch(NumberFormatException e){
            return -1;
        }finally{
            System.out.println("test结束");
        }
    }
}
```

举例3：从catch回来

```java
public class FinallyTest2 {
    public static void main(String[] args) {
        int result = test("a");
        System.out.println(result);
    }

    public static int test(String str) {
        try {
            Integer.parseInt(str);
            return 1;
        } catch (NumberFormatException e) {
            return -1;
        } finally {
            System.out.println("test结束");
        }
    }
}
```

举例4：从finally回来

```java
public class FinallyTest3 {
    public static void main(String[] args) {
        int result = test("a");
        System.out.println(result);
    }

    public static int test(String str) {
        try {
            Integer.parseInt(str);
            return 1;
        } catch (NumberFormatException e) {
            return -1;
        } finally {
            System.out.println("test结束");
            return 0;
        }
    }
}
```

笔试题：

```java
public class ExceptionTest {
    public static void main(String[] args) {
        int result = test();
        System.out.println(result); //100
    }

    public static int test(){
        int i = 100;
        try {
            return i;
        } finally {
            i++;
        }
    }
}
```

> 笔试题：final、finally、finalize有什么区别？
>

#### 4.2.4 练习
编写一个类ExceptionTest，在main方法中使用try、catch、finally，要求：

+ 在try块中，编写被零除的代码。
+ 在catch块中，捕获被零除所产生的异常，并且打印异常信息
+ 在finally块中，打印一条语句。

#### 4.2.5 异常处理的体会
+ 前面使用的异常都是`RuntimeException类`或是它的`子类`，这些类的异常的特点是：即使没有使用try和catch捕获，Java自己也能捕获，并且编译通过 ( 但运行时会发生异常使得程序运行终止 )。所以，对于这类异常，可以不作处理，因为这类异常很普遍，若全处理可能会对程序的可读性和运行效率产生影响。
+ 如果抛出的异常是IOException等类型的`非运行时异常`，则必须捕获，否则`编译错误`。也就是说，我们必须处理编译时异常，将异常进行捕捉，转化为运行时异常。

### 4.3 方式2：声明抛出异常类型（throws）
+ 如果在编写方法体的代码时，某句代码可能发生某个`编译时异常`，不处理编译不通过，但是在当前方法体中可能`不适合处理`或`无法给出合理的处理方式`，则此方法应`显示地`声明抛出异常，表明该方法将不对这些异常进行处理，而由该方法的调用者负责处理。
+ 具体方式：在方法声明中用`throws语句`可以声明抛出异常的列表，throws后面的异常类型可以是方法中产生的异常类型，也可以是它的父类。

#### 4.3.1 throws基本格式
**声明异常格式：**

```plain
修饰符 返回值类型 方法名(参数) throws 异常类名1,异常类名2…{   }	
```

在throws后面可以写多个异常类型，用逗号隔开。

举例：

```java
public void readFile(String file)  throws FileNotFoundException,IOException {
    ...
    // 读文件的操作可能产生FileNotFoundException或IOException类型的异常
    FileInputStream fis = new FileInputStream(file);
    //...
}

```

#### 4.3.2 throws 使用举例
是否真正处理了异常?

从编译是否能通过的角度看，看成是给出了异常万一要是出现时候的解决方案。此方案就是，继续向上抛出(throws)

但是，此throws的方式，仅是将可能出现的异常抛给了此方法的调用者。此调用者仍然需要考虑如何处理相关异常。

从这个角度来看，throws的方式不算是真正意义上处理了异常。



**举例：针对于编译时异常**

```java
package com.atguigu.keyword;

public class TestThrowsCheckedException {
    public static void main(String[] args) {
        System.out.println("上课.....");
        try {
            afterClass();//换到这里处理异常
        } catch (InterruptedException e) {
            e.printStackTrace();
            System.out.println("准备提前上课");
        }
        System.out.println("上课.....");
    }

    public static void afterClass() throws InterruptedException {
        for(int i=10; i>=1; i--){
            Thread.sleep(1000);//本来应该在这里处理异常
            System.out.println("距离上课还有：" + i + "分钟");
        }
    }
}

```

**举例：针对于运行时异常：**

throws后面也可以写运行时异常类型，只是运行时异常类型，写或不写对于编译器和程序执行来说都没有任何区别。如果写了，唯一的区别就是调用者调用该方法后，使用try...catch结构时，IDEA可以获得更多的信息，需要添加哪种catch分支。

```java
package com.atguigu.keyword;

import java.util.InputMismatchException;
import java.util.Scanner;

public class TestThrowsRuntimeException {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        try {
            System.out.print("请输入第一个整数：");
            int a = input.nextInt();
            System.out.print("请输入第二个整数：");
            int b = input.nextInt();
            int result = divide(a,b);
            System.out.println(a + "/" + b +"=" + result);
        } catch (ArithmeticException | InputMismatchException e) {
            e.printStackTrace();
        } finally {
            input.close();
        }
    }

    public static int divide(int a, int b)throws ArithmeticException{
        return a/b;
    }
}

```

#### 4.3.3 方法重写中throws的要求
方法重写时，对于方法签名是有严格要求的。复习：

```plain
（1）方法名必须相同
（2）形参列表必须相同
（3）返回值类型
    - 基本数据类型和void：必须相同
    - 引用数据类型：<=
（4）权限修饰符：>=，而且要求父类被重写方法在子类中是可见的
（5）不能是static，final修饰的方法
```

此外，对于throws异常列表要求：

+ 如果父类被重写方法的方法签名后面没有 “throws  编译时异常类型”，那么重写方法时，方法签名后面也不能出现“throws  编译时异常类型”。
+ 如果父类被重写方法的方法签名后面有 “`throws  编译时异常类型`”，那么重写方法时，throws的编译时异常类型必须 <= 被重写方法throws的编译时异常类型，或者不throws编译时异常。
+ 方法重写，对于“`throws 运行时异常类型`”没有要求。

```java
package com.atguigu.keyword;

import java.io.IOException;

class Father{
    public void method()throws Exception{
        System.out.println("Father.method");
    }
}
class Son extends Father{
    @Override
    public void method() throws IOException,ClassCastException {
        System.out.println("Son.method");
    }
}
```





#### 方法的重写的要求:
子类重写的方法抛出的异常类型可以与父类被重写的方法抛出的异常类型相同，或是父类被重写的方法抛出的异常类型的子类。

```java
import java.io.IOException;

public class OverrideTest {

    public static void main(String[] args) {
        // ...
    }
}

class Father {

    public void method1() throws IOException {
        // ...
    }
}

class Son extends Father {

    @Override
    public void method1() throws IOException {
        // ...
    }
    //抛出与父类相同
    //抛出父类更小范围
}
```

### 4.4 两种异常处理方式的选择
前提：对于异常，使用相应的处理方式。此时的异常，主要指的是编译时异常。

+ 如果程序代码中，涉及到资源的调用（流、数据库连接、网络连接等），则必须考虑使用try-catch-finally来处理，保证不出现内存泄漏。
+ 如果父类被重写的方法没有throws异常类型，则子类重写的方法中如果出现异常，只能考虑使用try-catch-finally进行处理，不能throws。
+ 开发中，方法a中依次调用了方法b,c,d等方法，方法b,c,d之间是递进关系。此时，如果方法b,c,d中有异常，我们通常选择使用throws，而方法a中通常选择使用try-catch-finally。



## 5. 手动抛出异常对象：throw
在实际开发中，如果出现不满足具体场景的代码问题，我们就有必要手动抛出一个指定类型的异常对象

Java 中异常对象的生成有两种方式：

+ 由虚拟机**自动生成**：程序运行过程中，虚拟机检测到程序发生了问题，那么针对当前代码，就会在后台自动创建一个对应异常类的实例对象并抛出。
+ 由开发人员**手动创建**：`new 异常类型([实参列表]);`，如果创建好的异常对象不抛出对程序没有任何影响，和创建一个普通对象一样，但是一旦throw抛出，就会对程序运行产生影响了。

### 5.1 使用格式
```java
throw new 异常类名(参数);
```

throw语句抛出的异常对象，和JVM自动创建和抛出的异常对象一样。

+ 如果是编译时异常类型的对象，同样需要使用throws或者try...catch处理，否则编译不通过。
+ 如果是运行时异常类型的对象，编译器不提示。
+ 可以抛出的异常必须是Throwable或其子类的实例。下面的语句在编译时将会产生语法错误：

```java
throw new String("want to throw");
```

### 5.2 使用注意点：
无论是编译时异常类型的对象，还是运行时异常类型的对象，如果没有被try..catch合理的处理，都会导致程序崩溃。

throw语句会导致程序执行流程被改变，throw语句是明确抛出一个异常对象，因此它`下面的代码将不会执行`。

如果当前方法没有try...catch处理这个异常对象，throw语句就会`代替return语句`提前终止当前方法的执行，并返回一个异常对象给调用者。

```java
package com.atguigu.keyword;

public class TestThrow {
    public static void main(String[] args) {
        try {
            System.out.println(max(4,2,31,1));
        } catch (Exception e) {
            e.printStackTrace();
        }
        try {
            System.out.println(max(4));
        } catch (Exception e) {
            e.printStackTrace();
        }
        try {
            System.out.println(max());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static int max(int... nums){
        if(nums == null || nums.length==0){
            throw new IllegalArgumentException("没有传入任何整数，无法获取最大值");
        }
        int max = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if(nums[i] > max){
                max = nums[i];
            }
        }
        return max;
    }
}

```

## 6. 自定义异常
### 6.1 为什么需要自定义异常类
Java中不同的异常类，分别表示着某一种具体的异常情况。那么在开发中总是有些异常情况是核心类库中没有定义好的，此时我们需要根据自己业务的异常情况来定义异常类。例如年龄负数问题，考试成绩负数问题，某员工已在团队中等。

### 6.2 如何自定义异常类
（1）要继承一个异常类型

			自定义一个编译时异常类型：自定义类继承`java.lang.Exception`。

			自定义一个运行时异常类型：自定义类继承`java.lang.RuntimeException`。

（2）建议大家提供至少两个构造器，一个是无参构造，一个是(String message)构造器。

（3）自定义异常需要提供`serialVersionUID`

### 6.3 注意点
1. 自定义的异常只能通过throw抛出。
2. 自定义异常最重要的是异常类的名字和message属性。当异常出现时，可以根据名字判断异常类型。比如：`TeamException("成员已满，无法添加"); `、 `TeamException("该员工已是某团队成员");`
3. 自定义异常对象只能手动抛出。抛出后由try..catch处理，也可以甩锅throws给调用者处理。

### 6.4 举例
举例1：

```java
class MyException extends Exception {
    static final long serialVersionUID = 23423423435L;
    private int idnumber;

    public MyException(String message, int id) {
        super(message);
        this.idnumber = id;
    }

    public int getId() {
        return idnumber;
    }
}

```

```java
public class MyExpTest {
    public void regist(int num) throws MyException {
        if (num < 0)
            throw new MyException("人数为负值，不合理", 3);
        else
            System.out.println("登记人数" + num);
    }
    public void manager() {
        try {
            regist(100);
        } catch (MyException e) {
            System.out.print("登记失败，出错种类" + e.getId());
        }
        System.out.print("本次登记操作结束");
    }
    public static void main(String args[]) {
        MyExpTest t = new MyExpTest();
        t.manager();
    }
}

```

举例2：

```java
package com.atguigu.define;
//自定义异常：
public class NotTriangleException extends Exception{
    static final long serialVersionUID = 13465653435L;

    public NotTriangleException() {
    }

    public NotTriangleException(String message) {
        super(message);
    }
}

```

```java
package com.atguigu.define;

public class Triangle {
    private double a;
    private double b;
    private double c;

    public Triangle(double a, double b, double c) throws NotTriangleException {
        if(a<=0 || b<=0 || c<=0){
            throw new NotTriangleException("三角形的边长必须是正数");
        }
        if(a+b<=c || b+c<=a || a+c<=b){
            throw new NotTriangleException(a+"," + b +"," + c +"不能构造三角形，三角形任意两边之后必须大于第三边");
        }
        this.a = a;
        this.b = b;
        this.c = c;
    }

    public double getA() {
        return a;
    }

    public void setA(double a) throws NotTriangleException{
        if(a<=0){
            throw new NotTriangleException("三角形的边长必须是正数");
        }
        if(a+b<=c || b+c<=a || a+c<=b){
            throw new NotTriangleException(a+"," + b +"," + c +"不能构造三角形，三角形任意两边之后必须大于第三边");
        }
        this.a = a;
    }

    public double getB() {
        return b;
    }

    public void setB(double b) throws NotTriangleException {
        if(b<=0){
            throw new NotTriangleException("三角形的边长必须是正数");
        }
        if(a+b<=c || b+c<=a || a+c<=b){
            throw new NotTriangleException(a+"," + b +"," + c +"不能构造三角形，三角形任意两边之后必须大于第三边");
        }
        this.b = b;
    }

    public double getC() {
        return c;
    }

    public void setC(double c) throws NotTriangleException {
        if(c<=0){
            throw new NotTriangleException("三角形的边长必须是正数");
        }
        if(a+b<=c || b+c<=a || a+c<=b){
            throw new NotTriangleException(a+"," + b +"," + c +"不能构造三角形，三角形任意两边之后必须大于第三边");
        }
        this.c = c;
    }

    @Override
    public String toString() {
        return "Triangle{" +
                "a=" + a +
                ", b=" + b +
                ", c=" + c +
                '}';
    }
}
```

```java
package com.atguigu.define;

public class TestTriangle {
    public static void main(String[] args) {
        Triangle t = null;
        try {
            t = new Triangle(2,2,3);
            System.out.println("三角形创建成功：");
            System.out.println(t);
        } catch (NotTriangleException e) {
            System.err.println("三角形创建失败");
            e.printStackTrace();
        }

        try {
            if(t != null) {
                t.setA(1);
            }
            System.out.println("三角形边长修改成功");
        } catch (NotTriangleException e) {
            System.out.println("三角形边长修改失败");
            e.printStackTrace();
        }
    }
}
```

面试 throw 和 throws 的区别

+ throw 我们主动抛出异常

> throw new RuntimeException("非法输入");
>

+ throws 将异常抛给上级处理

> public void method1() throws IOException {}
>



1. <font style="color:rgb(6, 6, 7);">如何自定义异常类？</font>
    - <font style="color:rgb(6, 6, 7);">继承于现有的异常体系。通常继承于</font><font style="color:rgb(6, 6, 7);"> </font>`RuntimeException`<font style="color:rgb(6, 6, 7);"> </font><font style="color:rgb(6, 6, 7);">或</font><font style="color:rgb(6, 6, 7);"> </font>`Exception`<font style="color:rgb(6, 6, 7);">。</font>
    - <font style="color:rgb(6, 6, 7);">通常提供几个重载的构造器。</font>
    - <font style="color:rgb(6, 6, 7);">提供一个全局常量，声明为：</font>`static final long serialVersionUID;`



如何自定义异常类?

<font style="color:rgb(6, 6, 7);">可使用自定义异常类： 具体的代码中，满足指定条件的情况下，需要手动使用“throw + 自定义异常类的对象”方式，将异常对象抛出。 如果自定义异常类是非运行时异常，则必须考虑如何处理此异常类的对象。（具体的：① try-catch-finally ② throws）</font>

<font style="color:rgb(6, 6, 7);"></font>

<font style="color:rgb(6, 6, 7);">为什么需要自定义异常类？ </font>

<font style="color:rgb(6, 6, 7);">我们其实更关心的是，通过异常的名称就能直接判断此异常出现的原因。因此，在实际开发场景中，当不满足我们指定的条件时，指明我们自己特有的异常类就显得很有必要。通过此异常类的名称，就能判断出具体出现的问题。</font>

<font style="color:rgb(6, 6, 7);"></font>

## 7. 练习
**练习1：**

```java
public class ReturnExceptionDemo {
    static void methodA() {
        try {
            System.out.println("进入方法A");
            throw new RuntimeException("制造异常");
        }finally {
            System.out.println("用A方法的finally");
        }
    }

    static void methodB() {
        try {
            System.out.println("进入方法B");
            return;
        } finally {
            System.out.println("调用B方法的finally");
        }
    }
    public static void main(String[] args) {
        try {
            methodA();
           } catch (Exception e) {
          	System.out.println(e.getMessage());
        }
        methodB();
      }
}

```

**练习2：**

从键盘接收学生成绩，成绩必须在0~100之间。

自定义成绩无效异常。

编写方法接收成绩并返回该成绩，如果输入无效，则抛出自定义异常。

**练习3：**

编写应用程序EcmDef.java，接收命令行的两个参数，要求不能输入负数，计算两数相除。  
对数据类型不一致(NumberFormatException)、缺少命令行参数(ArrayIndexOutOfBoundsException、  
除0(ArithmeticException)及输入负数(EcDef 自定义的异常)进行异常处理。

提示：   
(1)在主类(EcmDef)中定义异常方法(ecm)完成两数相除功能。

(2)在main()方法中使用异常处理语句进行异常处理。

(3)在程序中，自定义对应输入负数的异常类(EcDef)。

(4)运行时接受参数 java EcmDef 20 10   //args[0]=“20” args[1]=“10”

(5)Interger类的static方法parseInt(String s)将s转换成对应的int值。  
     如：int a=Interger.parseInt(“314”);	//a=314;

## 8. 小结与小悟
### 8.1 小结：异常处理5个关键字
> 类比：上游排污，下游治污
>

### 8.2 感悟
**小哲理：**

世界上最遥远的`距离`，是我在`if`里你在`else`里，似乎一直相伴又永远分离；

世界上最痴心的`等待`，是我当`case`你是`switch`，或许永远都选不上自己；

世界上最真情的`相依`，是你在`try`我在`catch`。无论你发神马脾气，我都默默承受，静静处理。到那时，再来期待我们的`finally`。

****

****

![](images/try.png)
