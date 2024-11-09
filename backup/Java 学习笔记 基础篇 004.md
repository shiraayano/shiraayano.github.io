## 1. 关键字：static


static 关键字的使用

static 静态的   用来修饰的结构，属性，方法：代码块，内部类；

代码示例

```java
public class ChineseTest {
    public static void main(String[] args) {
        Chinese c = new Chinese();
        c.name = "张三";
        c.age = 20;

        Chinese c2 = new Chinese();
        c2.name = "李四";
        c2.age = 30;

        System.out.println(c);
        System.out.println(c2);

        System.out.println("++++++++++++++++++++++");
        System.out.println(c.country);
        System.out.println(c2.country);

        c2.country = "中国";

        System.out.println("++++++++++++++++++++++");
        System.out.println(c.country);
        System.out.println(c2.country);

        //我们这里更改c2,可以发现c1的值也遭到了变更
        //因为country是静态变量,属于类,不属于某个对象


        //静态变量在内存中只有一份,被所有对象共享
        //非静态变量在内存中有几份,取决于对象有多少份
        //静态变量可以通过类名直接访问,也可以通过对象名访问
        //非静态变量只能通过对象名访问
        //静态变量和非静态变量,访问时,优先使用非静态变量
        
    }
}
class Chinese {//中国人 类
    //非静态变量,实例变量
    String name;
    int age;
    //静态变量,类变量

    static String country = "China";
    //非静态方法,实例方法

    public void sayHello() {
        System.out.println("你好,我是" + name);
    }

    //快捷键alt insert
    @Override
    public String toString() {
        // TODO Auto-generated method stub
        //return super.toString();
        return "Chinese{"+"name="+name+",age="+age+"}";
    }

    
    
    

}
```



3 2  
静态变量:类中的属性使用static进行修饰。  
对比静态变量与实例变量:  
① 个数

> 静态变量:在内存空间中只有一份，被类的多个对象所共享。  
实例变量:类的每一个实例(或对象)都保存着一份实例变量  
②内存位置  
静态变量:jdk6及之前:存放在方法区。jdk7及之后:存放在堆空间  
实例变量:随着对象的创建而加载，每个对象都有一份实例变量。  
存放在堆空间的对象实体中。  
③ 加载时机  
静态变量:随着类的加载而加载，由于类只会加载一次，所以静态变量也只要一份  
随着类的加载而加载，由于类只会加载一次，所以静态变量也只有一份。  
实例变量 随着对象的创建而被加载，每个对象拥有一份实例变量  
④ 调用者  
静态变量 可以被类直接调用，也可以使用对象调用  
实例变量:只能使用对象调用  
⑤判断是否可以调用  
--->从生命周期的角度解释
>
> 类可以调用类变量 不能调用实例变量
>
> 对象都可以调用
>
> 
>
> 消亡时机
>
> 静态变量 随着类的卸载而消亡
>
> 实例变量 随着对象的消亡而消亡
>



static修饰方法:

(类方法、静态方法)

随着类的加载而加载

可以通过“类.静态方法"的方式，直接调用静态方法

静态方法内可以调用静态的属性和静态的方法 不可以调用非静态的结构

static 修饰的方法内不能使用 this 和 super

补充 在类的静态方法中 可以调用当前类中的静态结构（属性 方法）或非静态结构（属性 方法）



### <font style="color:rgb(6, 6, 7);">静态变量（Static Variables）</font>
1. **<font style="color:rgb(6, 6, 7);">定义</font>**<font style="color:rgb(6, 6, 7);">：静态变量是使用</font><font style="color:rgb(6, 6, 7);"> </font>`static`<font style="color:rgb(6, 6, 7);"> </font><font style="color:rgb(6, 6, 7);">关键字声明的变量，它属于类的静态成员，而不是类的某个特定对象。</font>
2. **<font style="color:rgb(6, 6, 7);">作用域</font>**<font style="color:rgb(6, 6, 7);">：静态变量在类的所有实例之间共享，即所有实例共享同一个静态变量。</font>
3. **<font style="color:rgb(6, 6, 7);">生命周期</font>**<font style="color:rgb(6, 6, 7);">：静态变量的生命周期与类本身相同，只要类被加载，静态变量就存在，直到程序结束。</font>
4. **<font style="color:rgb(6, 6, 7);">访问方式</font>**<font style="color:rgb(6, 6, 7);">：可以通过类名直接访问静态变量，也可以通过实例访问。</font>
5. **<font style="color:rgb(6, 6, 7);">用途</font>**<font style="color:rgb(6, 6, 7);">：通常用于存储类级别的信息，比如配置信息或者计数器等。</font>

### <font style="color:rgb(6, 6, 7);">实例变量（Instance Variables）</font>
1. **<font style="color:rgb(6, 6, 7);">定义</font>**<font style="color:rgb(6, 6, 7);">：实例变量是类中没有</font><font style="color:rgb(6, 6, 7);"> </font>`static`<font style="color:rgb(6, 6, 7);"> </font><font style="color:rgb(6, 6, 7);">关键字的成员变量，每个类的实例都有自己的一份实例变量。</font>
2. **<font style="color:rgb(6, 6, 7);">作用域</font>**<font style="color:rgb(6, 6, 7);">：实例变量的作用域仅限于创建它的对象。</font>
3. **<font style="color:rgb(6, 6, 7);">生命周期</font>**<font style="color:rgb(6, 6, 7);">：实例变量的生命周期与对象的生命周期相同，当对象被创建时实例变量被创建，对象被销毁时实例变量也被销毁。</font>
4. **<font style="color:rgb(6, 6, 7);">访问方式</font>**<font style="color:rgb(6, 6, 7);">：通常通过对象的实例来访问实例变量。</font>
5. **<font style="color:rgb(6, 6, 7);">用途</font>**<font style="color:rgb(6, 6, 7);">：用于存储对象特有的数据，每个对象的实例变量可以有不同的值。</font>

### <font style="color:rgb(6, 6, 7);">区别</font>
+ **<font style="color:rgb(6, 6, 7);">存储位置</font>**<font style="color:rgb(6, 6, 7);">：静态变量存储在方法区（或静态区），实例变量存储在堆内存中。</font>
+ **<font style="color:rgb(6, 6, 7);">访问限制</font>**<font style="color:rgb(6, 6, 7);">：静态变量可以在没有创建类实例的情况下被访问，而实例变量必须通过对象实例来访问。</font>
+ **<font style="color:rgb(6, 6, 7);">内存分配</font>**<font style="color:rgb(6, 6, 7);">：静态变量在内存中只有一个拷贝，而实例变量每个对象都有一个拷贝。</font>
+ **<font style="color:rgb(6, 6, 7);">使用场景</font>**<font style="color:rgb(6, 6, 7);">：静态变量适用于不需要依赖于对象实例的数据，实例变量适用于需要依赖于对象实例的数据。</font>
+ <font style="color:rgb(6, 6, 7);"></font>



开发中什么时候需要将属性声明为静态变量？

 判断当前类的多个实例是否需要共享此成员变量，且此成员变量的值是相同的

 开发中· 常将一些变量声明为静态的 比如 Math 类中的 PI



什么时候需要将方法声明为静态的？

 方法内操作的变量如果都是静态变量而非实例变量 的话 则此方法建议声明为静态方法

 开发中 常常将工具类的方法声明为静态



```java
public class ChineseTest {
    public static void main(String[] args) {
        // 在没有对象前就可以调用
        Chinese.show();

        Chinese c = new Chinese();
        c.name = "张三";
        c.age = 20;

        Chinese c2 = new Chinese();
        c2.name = "李四";
        c2.age = 30;

        System.out.println(c);
        System.out.println(c2);

        System.out.println("++++++++++++++++++++++");
        System.out.println(c.country);
        System.out.println(c2.country);

        c2.country = "中国";

        System.out.println("++++++++++++++++++++++");
        System.out.println(c.country);
        System.out.println(c2.country);

        // 我们这里更改c2,可以发现c1的值也遭到了变更
        // 因为country是静态变量,属于类,不属于某个对象

        // 静态变量在内存中只有一份,被所有对象共享
        // 非静态变量在内存中有几份,取决于对象有多少份
        // 静态变量可以通过类名直接访问,也可以通过对象名访问
        // 非静态变量只能通过对象名访问
        // 静态变量和非静态变量,访问时,优先使用非静态变量

    }
}

class Chinese {// 中国人 类
    // 非静态变量,实例变量
    String name;
    int age;
    // 静态变量,类变量

    static String country = "China";
    // 非静态方法,实例方法

    public void sayHello() {
        System.out.println("你好,我是" + name);
    }

    // 快捷键alt insert
    @Override
    public String toString() {
        // TODO Auto-generated method stub
        // return super.toString();
        return "Chinese{" + "name=" + name + ",age=" + age + "}";
    }

    public static void show() {
        System.out.println("================");
        System.out.println("我是中国人");
        // 调用静态的结构
        // 静态方法只能访问静态的结构
        System.out.println(country);
        method1();
        System.out.println("++++++++++++++++++++++");

        // 调用非静态的结构测试
        // System.out.println(this.name);
        //System.out.println(name);

        /*
         * Exception in thread "main" java.lang.Error: Unresolved compilation problem:
         * Cannot use this in a static context
         * 
         * at Chinese.show(ChineseTest.java:72)
         * at ChineseTest.main(ChineseTest.java:6)
         * 
         * 
         * 
         * 线程“main”java.lang中出现异常。错误：未解决的编译问题：
         * 不能在静态上下文中使用它
         * 在Chinese.show（中文测试java:72）上
         * 在ChineseTest.main（ChineseTest.java:6）
         */

         //this.eat("饺子");

         System.out.println("++++++++++++++++++++++");
         method2();
    }

    public static void method1() {
        System.out.println("我是静态方法");
    }
    public static void eat(String food) {
        System.out.println("我正在吃"+food);
    }
    //非静态方法可以访问静态的和非静态的
    public void method2() {
        System.out.println("我是非静态方法");
        System.out.println(country);
        method1();
        eat("面条");
    }

}
```





**回顾类中的实例变量（即非static的成员变量）**

```java
class Circle{
    private double radius;
    public Circle(double radius){
        this.radius=radius;
    }
    public double findArea(){
        return Math.PI*radius*radius;
    }
}
```

创建两个Circle对象：

```java
Circle c1=new Circle(2.0);	//c1.radius=2.0
Circle c2=new Circle(3.0);	//c2.radius=3.0
```

Circle类中的变量radius是一个实例变量(instance variable)，它属于类的每一个对象，c1中的radius变化不会影响c2的radius，反之亦然。

**如果想让一个成员变量被类的所有实例所共享，就用static修饰即可，称为类变量（或类属性）！**

### 1.1 类属性、类方法的设计思想
当我们编写一个类时，其实就是在描述其对象的属性和行为，而并没有产生实质上的对象，只有通过new关键字才会产出对象，这时系统才会分配内存空间给对象，其方法才可以供外部调用。我们有时候希望无论是否产生了对象或无论产生了多少对象的情况下，`某些特定的数据在内存空间里只有一份`。例如，所有的中国人都有个国家名称，每一个中国人都共享这个国家名称，不必在每一个中国人的实例对象中都单独分配一个用于代表国家名称的变量。

![](images/image-20220325213629311.png)



此外，在类中声明的实例方法，在类的外面必须要先创建对象，才能调用。但是有些方法的调用者和当前类的对象无关，这样的方法通常被声明为`类方法`，由于不需要创建对象就可以调用类方法，从而简化了方法的调用。

这里的类变量、类方法，只需要使用`static`修饰即可。所以也称为静态变量、静态方法。

### 1.2 static关键字
+ 使用范围：
    - 在Java类中，可用static修饰属性、方法、代码块、内部类
+ 被修饰后的成员具备以下特点：
    - 随着类的加载而加载
    - 优先于对象存在
    - 修饰的成员，被所有对象所共享
    - 访问权限允许时，可不创建对象，直接被类调用

### 1.3 静态变量
#### 1.3.1 语法格式
使用static修饰的成员变量就是静态变量（或类变量、类属性）

```java
[修饰符] class 类{
    [其他修饰符] static 数据类型 变量名;
}
```

#### 1.3.2 静态变量的特点
+ 静态变量的默认值规则和实例变量一样。
+ 静态变量值是所有对象共享。
+ 静态变量在本类中，可以在任意方法、代码块、构造器中直接使用。
+ 如果权限修饰符允许，在其他类中可以通过“`类名.静态变量`”直接访问，也可以通过“`对象.静态变量`”的方式访问（但是更推荐使用类名.静态变量的方式）。
+ 静态变量的get/set方法也静态的，当局部变量与静态变量`重名时`，使用“`类名.静态变量`”进行区分。

#### 1.3.3 举例
```java
public class AccountTest {
    public static void main(String[] args) {
        Account a1 = new Account();
        System.out.println(a1);

        Account a2 = new Account();
        System.out.println(a2);

        Account a3 = new Account();
        System.out.println(a3);

        System.out.println("银行存款利率为" + Account.getInterestRate());

    }
    
}
```

```java
public class Account {
    private int Id;
    private String Password;
    private double balance;//余额
    private static double interestRate;//利率

    private static int init = 1001;//账户数量

    public Account() {
        Id = init++;
        Password = "123456";
        balance = 0.0;
        interestRate = 0.3;
        
    }
    public Account(int id, String password, double balance) {
        Id = init++;
        Password = password;
        this.balance = balance;
    }

    public int getId() {
        return Id;
    }

    public void setId(int id) {
        Id = id;
    }

    public String getPassword() {
        return Password;
    }

    public void setPassword(String password) {
        Password = password;
    }

    public static double getInterestRate() {
        return interestRate;
    }

    @Override
    public String toString() {
        // TODO Auto-generated method stub
        //return super.toString();
        return "Account {Id=" + Id + ", Password=" + Password + ", balance=" + balance + "}";
    }

    

}
```

举例1：

```java
class Chinese{
    //实例变量
    String name;
    int age;
    //类变量
    static String nation;//国籍

    public Chinese() {
    }

    public Chinese(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Chinese{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", nation='" + nation + '\'' +
                '}';
    }
}
public class StaticTest {
    public static void main(String[] args) {
        Chinese c1 = new Chinese("康师傅",36);
        c1.nation = "中华人民共和国";

        Chinese c2 = new Chinese("老干妈",66);

        System.out.println(c1);
        System.out.println(c2);

        System.out.println(Chinese.nation);
    }
}
```

对应的内存结构：（以经典的JDK6内存解析为例，此时静态变量存储在方法区）

举例2：

```java
package com.atguigu.keyword;

public class Employee {
    private static int total;//这里私有化，在类的外面必须使用get/set方法的方式来访问静态变量
    static String company; //这里缺省权限修饰符，是为了方便类外以“类名.静态变量”的方式访问
    private int id;
    private String name;

    public Employee() {
        total++;
        id = total;//这里使用total静态变量的值为id属性赋值
    }

    public Employee(String name) {
        this();
        this.name = name;
    }

    public void setId(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public static int getTotal() {
        return total;
    }

    public static void setTotal(int total) {
        Employee.total = total;
    }

    @Override
    public String toString() {
        return "Employee{company = " + company + ",id = " + id + " ,name=" + name +"}";
    }
}
```

```java
package com.atguigu.keyword;

public class TestStaticVariable {
    public static void main(String[] args) {
        //静态变量total的默认值是0
        System.out.println("Employee.total = " + Employee.getTotal());

        Employee e1 = new Employee("张三");
        Employee e2 = new Employee("李四");
        System.out.println(e1);//静态变量company的默认值是null
        System.out.println(e2);//静态变量company的默认值是null
        System.out.println("Employee.total = " + Employee.getTotal());//静态变量total值是2

        Employee.company = "尚硅谷";
        System.out.println(e1);//静态变量company的值是尚硅谷
        System.out.println(e2);//静态变量company的值是尚硅谷

        //只要权限修饰符允许,虽然不推荐，但是也可以通过“对象.静态变量”的形式来访问
        e1.company = "超级尚硅谷";

        System.out.println(e1);//静态变量company的值是超级尚硅谷
        System.out.println(e2);//静态变量company的值是超级尚硅谷
    }
}
```





### 1.4 静态方法
#### 1.4.1 语法格式
用static修饰的成员方法就是静态方法。

```java
[修饰符] class 类{
    [其他修饰符] static 返回值类型 方法名(形参列表){
        方法体
    }
}
```

#### 1.4.2 静态方法的特点
+ 静态方法在本类的任意方法、代码块、构造器中都可以直接被调用。
+ 只要权限修饰符允许，静态方法在其他类中可以通过“类名.静态方法“的方式调用。也可以通过”对象.静态方法“的方式调用（但是更推荐使用类名.静态方法的方式）。
+ 在static方法内部只能访问类的static修饰的属性或方法，不能访问类的非static的结构。
+ 静态方法可以被子类继承，但不能被子类重写。
+ 静态方法的调用都只看编译时类型。
+ 因为不需要实例就可以访问static方法，因此static方法内部不能有this，也不能有super。如果有重名问题，使用“类名.”进行区别。

#### 1.4.3 举例
```java
package com.atguigu.keyword;

public class Father {
    public static void method(){
        System.out.println("Father.method");
    }

    public static void fun(){
        System.out.println("Father.fun");
    }
}
```

```java
package com.atguigu.keyword;

public class Son extends Father{
//    @Override //尝试重写静态方法，加上@Override编译报错，去掉Override不报错，但是也不是重写
    public static void fun(){
        System.out.println("Son.fun");
    }
}
```

```java
package com.atguigu.keyword;

public class TestStaticMethod {
    public static void main(String[] args) {
        Father.method();
        Son.method();//继承静态方法

        Father f = new Son();
        f.method();//执行Father类中的method
    }
}
```

### 1.5 练习
笔试题：如下程序执行会不会报错

```java
/**
 * @author 尚硅谷-宋红康
 * @create 14:30
 */
public class StaticTest {
    public static void main(String[] args) {
        Demo test = null;
        test.hello();
    }
}

class Demo{
    public static void hello(){
        System.out.println("hello!");
    }
}
```

练习：

编写一个类实现银行账户的概念，包含的属性有“帐号”、“密码”、“存款余额”、“利率”、“最小余额”，定义封装这些属性的方法。`账号要自动生成。`

编写主类，使用银行账户类，输入、输出3个储户的上述信息。

考虑：哪些属性可以设计成static属性。

## 2. 单例(Singleton)设计模式
### 2.1 设计模式概述
**设计模式**是在大量的`实践中总结`和`理论化`之后优选的代码结构、编程风格、以及解决问题的思考方式。设计模式免去我们自己再思考和摸索。就像是经典的棋谱，不同的棋局，我们用不同的棋谱。"套路"

经典的设计模式共有23种。每个设计模式均是特定环境下特定问题的处理方法。

> 简单工厂模式并不是23中经典模式的一种，是其中工厂方法模式的简化版
>

> 对软件设计模式的研究造就了一本可能是面向对象设计方面最有影响的书籍：《设计模式》：《Design Patterns: Elements of Reusable Object-Oriented Software》（即后述《设计模式》一书），由 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissides 合著（Addison-Wesley，1995）。这几位作者常被称为"四人组（Gang of Four）"，而这本书也就被称为"四人组（或 GoF）"书。
>

经典的设计模式一共有 23 种



### 2.2 何为单例模式
所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类**只能存在一个对象实例**，并且该类只提供一个取得其对象实例的方法。

### 2.3 实现思路
如果我们要让类在一个虚拟机中只能产生一个对象，我们首先必须将`类的构造器的访问权限设置为private`，这样，就不能用new操作符在类的外部产生类的对象了，但在类内部仍可以产生该类的对象。因为在类的外部开始还无法得到类的对象，`只能调用该类的某个静态方法`以返回类内部创建的对象，静态方法只能访问类中的静态成员变量，所以，指向类内部产生的`该类对象的变量也必须定义成静态的`。

### 2.4 单例模式的两种实现方式
#### 2.4.1 饿汉式
```java
class Singleton {
    // 1.私有化构造器
    private Singleton() {
    }

    // 2.内部提供一个当前类的实例
    // 4.此实例也必须静态化
    private static Singleton single = new Singleton();

    // 3.提供公共的静态的方法，返回当前类的对象
    public static Singleton getInstance() {
        return single;
    }
}

```



```java
public class Banktest {
    public static void main(String[] args) {
        // 单例模式
        Bank bank = Bank.getInstance();
                Bank bank1 = Bank.getInstance();
                System.out.println(bank == bank1);
                //输出为true
                
        
            }
        
        }
        //饿汉式
        class Bank {
            // 私有化构造方法
            private Bank() {
        
            }
        
            // 在类中创建当前类的实例
            private static Bank instance = new Bank();
        
            // 对外提供公共的访问方法
            public static Bank getInstance() {
        return instance;
    }

}
```



#### 2.4.2 懒汉式
```java
class Singleton {
    // 1.私有化构造器
    private Singleton() {
    }
    // 2.内部提供一个当前类的实例
    // 4.此实例也必须静态化
    private static Singleton single;
    // 3.提供公共的静态的方法，返回当前类的对象
    public static Singleton getInstance() {
        if(single == null) {
            single = new Singleton();
        }
        return single;
    }
}

```

#### 2.4.3 饿汉式 vs 懒汉式
饿汉式：

+ 特点：`立即加载`，即在使用类的时候已经将对象创建完毕。
+ 优点：实现起来`简单`；没有多线程安全问题。
+ 缺点：当类被加载的时候，会初始化static的实例，静态变量被创建并分配内存空间，从这以后，这个static的实例便一直占着这块内存，直到类被卸载时，静态变量被摧毁，并释放所占有的内存。因此在某些特定条件下会`耗费内存`。

懒汉式：

+ 特点：`延迟加载`，即在调用静态方法时实例才被创建。
+ 优点：实现起来比较简单；当类被加载的时候，static的实例未被创建并分配内存空间，当静态方法第一次被调用时，初始化实例变量，并分配内存，因此在某些特定条件下会`节约内存`。
+ 缺点：在多线程环境中，这种实现方法是完全错误的，`线程不安全`，根本不能保证单例的唯一性。
    - 说明：在多线程章节，会将懒汉式改造成线程安全的模式。

4.对比两种模式(特点、优缺点)  
特点:

> 饿汉式:"立即加载”,随着类的加载，当前的唯一实例就创建了  
懒汉式:"延迟加载"在需要使用的时候，进行创建。  
优缺点:  
饿汉式:  
(优点)写法简单，由于内存中较早加载，使用更方便、更快。是线程安全的。  
(缺点)内存中占用时间较长。  
懒汉式:  
(缺点)线程不安全(放到多线程章节时解决)(优点)在需要的时候进行创建，节省内存空间。
>

饿汉式生命周期过长，容易造成资源浪费，但是能保证线程安全，面试优先写饿汉式

### 2.5 单例模式的优点及应用场景
由于单例模式只生成一个实例，减少了`系统性能开销`，当一个对象的产生需要比较多的资源时，如读取配置、产生其他依赖对象时，则可以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方式来解决。

举例：

**应用场景**

+ Windows的Task Manager (任务管理器)就是很典型的单例模式
+ Windows的Recycle Bin (回收站)也是典型的单例应用。在整个系统运行过程中，回收站一直维护着仅有的一个实例。
+ Application 也是单例的典型应用
+ 应用程序的日志应用，一般都使用单例模式实现，这一般是由于共享的日志文件一直处于打开状态，因为只能有一个实例去操作，否则内容不好追加。
+ 数据库连接池的设计一般也是采用单例模式，因为数据库连接是一种数据库资源。

## 3. 理解main方法的语法
由于JVM需要调用类的main()方法，所以该方法的访问权限必须是public，又因为JVM在执行main()方法时不必创建对象，所以该方法必须是static的，该方法接收一个String类型的数组参数，该数组中保存执行Java命令时传递给所运行的类的参数。 

又因为main() 方法是静态的，我们不能直接访问该类中的非静态成员，必须创建该类的一个实例对象后，才能通过这个对象去访问类中的非静态成员，这种情况，我们在之前的例子中多次碰到。

**命令行参数用法举例**

```java
public class CommandPara {
    public static void main(String[] args) {
        for (int i = 0; i < args.length; i++) {
            System.out.println("args[" + i + "] = " + args[i]);
        }
    }
}

```

```java
//运行程序CommandPara.java
java CommandPara "Tom" "Jerry" "Shkstart"
```

```java
//输出结果
args[0] = Tom
args[1] = Jerry
args[2] = Shkstart

```





main()方法的剖析

public static void main(String args[]){}

1.理解1:看做是一个普通的静态方法

理解2:看做是程序的入口，格式是固定的

```java
public class Main {
    public static void main(String[] args) {// 程序的入口
        // TODO Auto-generated method stub

        String[] args1 = { "a", "b", "c" };
        MainTest.Test(args1);

    }
}

class MainTest {
    public static void Test(String[] args) {// 看作普通方方法
        System.out.println("Main的MainTest()调用");
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }

}
```

### 1. `Main` 类（了解）
```java
public class Main {
    public static void main(String[] args) { // 程序的入口
        // TODO Auto-generated method stub

        String[] args1 = { "a", "b", "c" };
        MainTest.Test(args1);
    }
}
```

+ `public class Main`: 定义了一个名为 `Main` 的公共类。在 Java 中，每个程序至少需要一个类，并且通常这个类包含 `main` 方法作为程序的入口点。
+ `public static void main(String[] args)`: 这是 Java 程序的主入口点。当程序启动时，JVM 会调用这个方法。`public` 表示这个方法是公共的，可以从外部访问；`static` 表示这个方法属于类本身而不是类的实例；`void` 表示这个方法不返回任何值；`String[] args` 是一个字符串数组，用于接收命令行参数。
+ `String[] args1 = { "a", "b", "c" };`: 定义了一个字符串数组 `args1`，并初始化为包含三个元素 `"a"`、`"b"` 和 `"c"`。
+ `MainTest.Test(args1);`: 调用 `MainTest` 类中的 `Test` 方法，并将 `args1` 作为参数传递给它。

### 2. `MainTest` 类
```java
class MainTest {
    public static void Test(String[] args) { // 看作普通方法
        System.out.println("Main的MainTest()调用");
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```

+ `class MainTest`: 定义了一个名为 `MainTest` 的类。这个类不是公共的，所以只能在同一文件中访问。
+ `public static void Test(String[] args)`: 定义了一个静态方法 `Test`，它接受一个字符串数组 `args` 作为参数。`public` 表示这个方法是公共的，可以从外部访问；`static` 表示这个方法属于类本身而不是类的实例；`void` 表示这个方法不返回任何值；`String[] args` 是一个字符串数组，用于接收传入的参数。
+ `System.out.println("Main的MainTest()调用");`: 输出字符串 `"Main的MainTest()调用"` 到控制台。
+ `for (int i = 0; i < args.length; i++)`: 使用一个 `for` 循环遍历传入的字符串数组 `args`。`args.length` 返回数组的长度。
+ `System.out.println(args[i]);`: 在循环体内，输出数组 `args` 的第 `i` 个元素到控制台。

### 总结
+ `Main`** 类** 包含了程序的入口点 `main` 方法。在这个方法中，创建了一个字符串数组 `args1` 并调用了 `MainTest` 类中的 `Test` 方法。
+ `MainTest`** 类** 包含了一个静态方法 `Test`，这个方法接收一个字符串数组作为参数，并打印出数组中的每一个元素。

运行输出是：

```plain
Main的MainTest()调用
a
b
c
```





2.与控制台交互

如何从键盘获取数据？

+ 方式一 使用 Scanner

```java
import java.util.Scanner;

public class scanner {
    public static void main(String[] args) {
        // 创建Scanner对象，用于获取键盘输入
        Scanner scanner = new Scanner(System.in);

        System.out.println("name：");
        // 调用next()方法读取一行文本（不包括换行符）
        String name = scanner.next();

        System.out.println("age：");
        // 调用nextInt()方法读取一个整数
        int age = scanner.nextInt();

        // 输出获取到的信息
        System.out.println("name：" + name);
        System.out.println("age：" + age);
        // 关闭Scanner对象
        scanner.close();
    }
}
```

+ 方式二 使用 main() 的形式传递值

```java
public class MainTest {
    public static void Test(String[] args) {// 看作普通方方法
        System.out.println("Main的MainTest()调用");
        for (int i = 0; i < args.length; i++) {
            System.out.println(args[i]);
        }
    }

}
```

> javac MainTest.java
>
> java MainTest "Tom" Jerry aa 11 22
>

####  如此 可在命令行中传参


在 idea 中可以自定义启动参数 run-Edit Config。。。-Choose Class（选择类）-Program arguments















## 4. 类的成员之四：代码块


回顾:类中可以声明的结构:属性、方法、构造器:代码块(或初始化块)、内部类

1.代码块(或初始化块)的使用

用来初始化类或对象的信息(即初始化类或对象的成员变量)

代码块的修饰:

只能使用static进行修饰。

3.代码块的分类:

静态代码块:使用static修饰

非静态代码块:没有使用static修饰

具体使用:

4.1 静态代码块:

+ 随着类的加载而调用 
+ 由于类的加载只会执行一次，所以静态代码块只会执行一次
+ 作用：用来初始化类的信息
+ 内部类可以声明变量 调用属性或方法 编写输出语句等操作
+ 声明多个静态代码块按照声明先后执行
+ 静态代码块只能调用静态的结构（静态的属性，方法），不能调用非静态的结构（非静态的属性或方法）

4.2 非静态代码块:

+ 随着对象的创建而执行 
+ 每创建当前类的一个实例就会执行一次
+ 作用：用于初始化对象的信息
+ 内部类可以声明变量 调用属性或方法 编写输出语句等操作
+ 非静态代码块可以调用静态结构，也可以调用非静态的结构

**静态代码块优先于非静态代码块执行**

```java
public class Person{
    //非静态代码块
    {
        System.out.println("Person代码块");
    }
    //静态代码块
    static{
        System.out.println("Person静态代码块");
    }
}
```



```java
public class Person{
    //非静态代码块
    //随着对象的创建而执行
    //每创建一个对象，执行一次
    {
        System.out.println("Person代码块");
    }

    //静态代码块
    //随着类的加载而执行
    //只执行一次
    static{
        System.out.println("Person静态代码块");
    }
    //静态代码块优先执行
    static String info="我是一个人";
}
```

如果成员变量想要初始化的值不是一个硬编码的常量值，而是需要通过复杂的计算或读取文件、或读取运行环境信息等方式才能获取的一些值，该怎么办呢？此时，可以考虑代码块（或初始化块）。

+ 代码块(或初始化块)的`作用`：
+ 对Java类或对象进行初始化
+ 代码块(或初始化块)的`分类`：
    - 一个类中代码块若有修饰符，则只能被static修饰，称为静态代码块(static block)
    - 没有使用static修饰的，为非静态代码块。

### 4.1 静态代码块
如果想要为静态变量初始化，可以直接在静态变量的声明后面直接赋值，也可以使用静态代码块。

#### 4.1.1 语法格式
在代码块的前面加static，就是静态代码块。

```java
【修饰符】 class 类{
    static{
        静态代码块
    }
}
```

#### 4.1.2 静态代码块的特点
1. 可以有输出语句。
2. 可以对类的属性、类的声明进行初始化操作。
3. 不可以对非静态的属性初始化。即：不可以调用非静态的属性和方法。
4. 若有多个静态的代码块，那么按照从上到下的顺序依次执行。
5. 静态代码块的执行要先于非静态代码块。
6. 静态代码块随着类的加载而加载，且只执行一次。

```java
package com.atguigu.keyword;

public class Chinese {
//    private static String country = "中国";

    private static String country;
    private String name;

    {
        System.out.println("非静态代码块，country = " + country);
    }

    static {
        country = "中国";
        System.out.println("静态代码块");
    }

    public Chinese(String name) {
        this.name = name;
    }
}
```

```java
package com.atguigu.keyword;

public class TestStaticBlock {
    public static void main(String[] args) {
        Chinese c1 = new Chinese("张三");
        Chinese c2 = new Chinese("李四");
    }
}

```

### 4.2 非静态代码块
#### 4.2.1 语法格式
```java
【修饰符】 class 类{
    {
        非静态代码块
    }
    【修饰符】 构造器名(){
        // 实例初始化代码
    }
    【修饰符】 构造器名(参数列表){
        // 实例初始化代码
    }
}
```

#### 4.2.2 非静态代码块的作用
和构造器一样，也是用于实例变量的初始化等操作。

#### 4.2.3 非静态代码块的意义
如果多个重载的构造器有公共代码，并且这些代码都是先于构造器其他代码执行的，那么可以将这部分代码抽取到非静态代码块中，减少冗余代码。

#### 4.2.4 非静态代码块的执行特点
1. 可以有输出语句。
2. 可以对类的属性、类的声明进行初始化操作。
3. 除了调用非静态的结构外，还可以调用静态的变量或方法。
4. 若有多个非静态的代码块，那么按照从上到下的顺序依次执行。
5. 每次创建对象的时候，都会执行一次。且先于构造器执行。

### 4.3 举例
**举例1：**

（1）声明User类，

+ 包含属性：username（String类型），password（String类型），registrationTime（long类型），私有化
+ 包含get/set方法，其中registrationTime没有set方法
+ 包含无参构造，
    - 输出“新用户注册”，
    - registrationTime赋值为当前系统时间，
    - username就默认为当前系统时间值，
    - password默认为“123456”
+ 包含有参构造(String username, String password)，
    - 输出“新用户注册”，
    - registrationTime赋值为当前系统时间，
    - username和password由参数赋值
+ 包含public String getInfo()方法，返回：“用户名：xx，密码：xx，注册时间：xx”

（2）编写测试类，测试类main方法的代码如下：

```java
    public static void main(String[] args) {
        User u1 = new User();
        System.out.println(u1.getInfo());

        User u2 = new User("song","8888");
        System.out.println(u2.getInfo());
    }
```

如果不用非静态代码块，User类是这样的：

```java
package com.atguigu.block.no;

public class User {
    private String username;
    private String password;
    private long registrationTime;

    public User() {
        System.out.println("新用户注册");
        registrationTime = System.currentTimeMillis();
        username = registrationTime+"";
        password = "123456";
    }

    public User(String username,String password) {
        System.out.println("新用户注册");
        registrationTime = System.currentTimeMillis();
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public long getRegistrationTime() {
        return registrationTime;
    }
    public String getInfo(){
        return "用户名：" + username + "，密码：" + password + "，注册时间：" + registrationTime;
    }
}
```

如果提取构造器公共代码到非静态代码块，User类是这样的：

```java
package com.atguigu.block.use;

public class User {
    private String username;
    private String password;
    private long registrationTime;

    {
        System.out.println("新用户注册");
        registrationTime = System.currentTimeMillis();
    }

    public User() {
        username = registrationTime+"";
        password = "123456";
    }

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public long getRegistrationTime() {
        return registrationTime;
    }
    public String getInfo(){
        return "用户名：" + username + "，密码：" + password + "，注册时间：" + registrationTime;
    }
}
```

**举例2：**

```java
private static DataSource dataSource = null;

static{
    InputStream is = null;
    try {
        is = DBCPTest.class.getClassLoader().getResourceAsStream("dbcp.properties");
        Properties pros = new Properties();
        pros.load(is);
        //调用BasicDataSourceFactory的静态方法，获取数据源。
        dataSource = BasicDataSourceFactory.createDataSource(pros);
    } catch (Exception e) {
        e.printStackTrace();
    }finally{
        if(is != null){
            try {
                is.close();
            } catch (IOException e) {
                e.printStackTrace();
            }		
        }		
    }		
}
```

### 4.4 小结：实例变量赋值顺序
### 4.5 练习
练习1：分析加载顺序

```java
class Root{
    static{
        System.out.println("Root的静态初始化块");
    }
    {
        System.out.println("Root的普通初始化块");
    }
    public Root(){
        System.out.println("Root的无参数的构造器");
    }
}
class Mid extends Root{
    static{
        System.out.println("Mid的静态初始化块");
    }
    {
        System.out.println("Mid的普通初始化块");
    }
    public Mid(){
        System.out.println("Mid的无参数的构造器");
    }
    public Mid(String msg){
        //通过this调用同一类中重载的构造器
        this();
        System.out.println("Mid的带参数构造器，其参数值："
            + msg);
    }
}
class Leaf extends Mid{
    static{
        System.out.println("Leaf的静态初始化块");
    }
    {
        System.out.println("Leaf的普通初始化块");
    }	
    public Leaf(){
        //通过super调用父类中有一个字符串参数的构造器
        super("尚硅谷");
        System.out.println("Leaf的构造器");
    }
}
public class LeafTest{
    public static void main(String[] args){
        new Leaf(); 
        //new Leaf();
    }
}
```

练习2：分析加载顺序

```java
class Father {
    static {
        System.out.println("11111111111");
    }
    {
        System.out.println("22222222222");
    }

    public Father() {
        System.out.println("33333333333");

    }

}

public class Son extends Father {
    static {
        System.out.println("44444444444");
    }
    {
        System.out.println("55555555555");
    }
    public Son() {
        System.out.println("66666666666");
    }


    public static void main(String[] args) { 
        System.out.println("77777777777");
        System.out.println("************************");
        new Son();
        System.out.println("************************");

        new Son();
        System.out.println("************************");
        new Father();
    }

}

```

练习3：

```java
package com.atguigu05.field.interview;

/**
 * @author 尚硅谷-宋红康
 * @create 16:04
 */
public class Test04 {
    public static void main(String[] args) {
        Zi zi = new Zi();
    }
}
class Fu{
    private static int i = getNum("（1）i");
    private int j = getNum("（2）j");
    static{
        print("（3）父类静态代码块");
    }
    {
        print("（4）父类非静态代码块，又称为构造代码块");
    }
    Fu(){
        print("（5）父类构造器");
    }
    public static void print(String str){
        System.out.println(str + "->" + i);
    }
    public static int getNum(String str){
        print(str);
        return ++i;
    }
}
class Zi extends Fu{
    private static int k = getNum("（6）k");
    private int h = getNum("（7）h");
    static{
        print("（8）子类静态代码块");
    }
    {
        print("（9）子类非静态代码块，又称为构造代码块");
    }
    Zi(){
        print("（10）子类构造器");
    }
    public static void print(String str){
        System.out.println(str + "->" + k);
    }
    public static int getNum(String str){
        print(str);
        return ++k;
    }
}

```



### 总结 - 属性赋值的过程


1.可以给类的非静态的属性(即实例变量)赋值的位置有:

① 默认初始化

② 显式初始化

③ 构造器中初始化

⑤ 代码块中初始化

##########################

④ 有了对象以后，通过"对象.属性"或"对象,方法"的方法进行赋值

2.执行的先后顺序:

1-2/5-3-4

##### (超纲)关于字节码文件中的<init>的简单说明:(通过插件jclasslib bytecode viewer查看)
<init>方法可以在字节码文件中看到 每个<init>方法都有对应着一个类的构造器 （类中声明了几个构造器久游几个<init>）

<init>方法内部代码包含了实例变量的显示赋值 代码块中的赋值和构造器中的代码

<init>方法用来初始化当前创建对象的信息的



给实例变量赋值的位置很多，开发中如何选?

需求分析（废话）

显示赋值，比较于每个对象的属性值相同的场景

构造器中赋值，比较适合于每个对象属性值不同的场景







## 5. final关键字
### 5.1 final的意义
final：最终的，不可更改的

### 5.2 final的使用
#### 5.2.1 final修饰类
```java
class A{
    
}
class B extends A{
    //正常来讲可以用B继承A
}
final class C{
    
}
class D extends C{
    //正常来讲可以用D继承C
    //报错
    //使用final修饰的类不能被继承
}
```

表示这个类不能被继承，没有子类。提高安全性，提高程序的可读性。

例如：String类、System类、StringBuffer类

```java
final class Eunuch{//太监类
    
}
class Son extends Eunuch{//错误
    
}
```





```java
class E{
    public void show(){
        System.out.println("show");
    }
    public final void show2(){
        System.out.println("show2");
    }
}
class F extends E{
    //正常来讲可以用F继承E
    //使用final修饰的方法不能被重写
    public void show(){
        System.out.println("show");
    }
    public void show2(){
        System.out.println("show2");
    }
}
```

#### 5.2.2 final修饰方法
表示这个方法不能被子类重写。

例如：Object类中的getClass()

```java
class Father{
    public final void method(){
        System.out.println("father");
    }
}
class Son extends Father{
    public void method(){//错误
        System.out.println("son");
    }
}
```





```java
// final修饰的变量是常量
class FinalTest2 {
    public static void main(String[] args) {
        final int a = 10;
        // a=20;不能修改
        // final修饰的变量必须初始化
        final int b = 10;
        System.out.println(b);
        System.out.println("____________________");
        b = 20;// 不能修改 报错
        System.out.println(b);
        /*
         * cworkspaceStorage\x5ce79013143972bf905b0cf9274b6425dd\x5credhat.java\
         * x5cjdt_ws\x5c1_6f9ffb3d\x5cbin' 'FinalTest2'
         * ;f0033315-a209-4a07-8e6e-2f27dcd3450eException in thread "main"
         * java.lang.Error: Unresolved compilatio
         * n problem:
         * The final local variable b cannot be assigned. It must be blank and not using
         * a compound assignment
         * 
         * at FinalTest2.main(FinalTest.java:45)
         * PS C:\code\java\Week2\1>
         */
    }
}
```

```java
class FinalTest3 {
    //final修饰的变量可以在初始化时赋值
    final int a;
    final int b = 10;
    final int c;
    //也可以在构造器中赋值
    public FinalTest3() {
        a = 10;
    }

    //还可以在代码块中赋值
    {
        c = 10;
    }  
}
```



```java
//final和static搭配
//修饰的变量是常量，称为全局常量
class FinalTest4 {
    public static void main(String[] args) {
        System.out.println(FinalTest4.NUM);
        //NUM=20;不能修改
    }

    public static final int NUM = 10;
}
```

#### 5.2.3 final修饰变量
final修饰某个变量（成员变量或局部变量），一旦赋值，它的值就不能被修改，即常量，常量名建议使用大写字母。

例如：final double MY_PI = 3.14;

> 如果某个成员变量用final修饰后，没有set方法，并且必须初始化（可以显式赋值、或在初始化块赋值、实例变量还可以在构造器中赋值）
>

+ 修饰成员变量

```java
public final class Test {
    public static int totalNumber = 5;
    public final int ID;

    public Test() {
        ID = ++totalNumber; // 可在构造器中给final修饰的“变量”赋值
    }
    public static void main(String[] args) {
        Test t = new Test();
        System.out.println(t.ID);
    }
}

```

+ 修饰局部变量：

```java
public class TestFinal {
    public static void main(String[] args){
        final int MIN_SCORE ;
        MIN_SCORE = 0;
        final int MAX_SCORE = 100;
        MAX_SCORE = 200; //非法
    }
}
```

+ 错误演示：

```java
class A {
    private final String INFO = "atguigu";  //声明常量

    public void print() {
        //The final field A.INFO cannot be  assigned
        //INFO = "尚硅谷"; 
    }
}

```

### 5.3 笔试题
题1：排错

```java
public class Something {
    public int addOne(final int x) {
        return ++x;
        // return x + 1;
    }
}
```

题2：排错

```java
public class Something {
    public static void main(String[] args) {
        Other o = new Other();
        new Something().addOne(o);
    }
    public void addOne(final Other o) {
        // o = new Other();
        o.i++;
    }
}
class Other {
    public int i;
}

```









## 6. 抽象类与抽象方法(或abstract关键字)


让父类不能造对象，不能实例化

```java
public class PersonTest {
    // abstact例子
    // abstract修饰类，该类就是抽象类
    // 抽象类中可以定义抽象方法，抽象方法没有方法体
    // 抽象类中可以定义非抽象方法
    // 抽象类不能实例化
    // 抽象类中可以定义构造方法
    // 抽象类的子类必须重写父类中的所有抽象方法，否则子类也是抽象类

    String name;
    int age;

    public PersonTest() {

    }

    public PersonTest(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void eat() {/* ... */
        System.out.println("人吃饭");
    }

    public void sleep() {/* ... */
        System.out.println("人睡觉");
    }

}
//抽象类
abstract class Person{
    //定义抽象方法
    public abstract void say();


}
```

```java
public class Student extends PersonTest {
    String school;

    public Student() {

    }

    public Student(String name, int age, String school) {
        super(name, age);
        this.school = school;
    }

    public void eat() {/* ... */
        System.out.println("学生吃饭");
    }

    public void sleep() {/* ... */
        System.out.println("学生睡觉");
    }

    public void say() {
        System.out.println("我是学生");
    }

    public static void main(String[] args) {
        Student s = new Student();
        s.eat();
        s.sleep();

        PersonTest P = new PersonTest();
        P.eat();
        P.sleep();
        
        s.say();
    }

}
```

  
 abstract修饰类:

> 此类称为抽象类  
抽象类不能实例化。  
抽象类中是包含构造器的，因为子类对象实例化时，需要直接或间接的调用到父类的构造器。  
抽象类中可以役有抽象方法。反之，抽象方法所在的类，一定是抽象类。
>

abstract修饰方法

> 此方法即为抽象方法  
抽象方法只有方法的声明，没有方法体。  
抽象方法其功能是确定的(通过方法的声明即可确定)，只是不知道如何实现，因为没有方法体
>
> 子类必须重写父类所有抽方法后才可实例化，否则子类仍然时一个抽象类
>
> 
>



abstract不能使用的场景

 abstract 不能修饰哪些结构?  
属性、构造器、代码块等。  
 abstract 不能与哪些关键字共用?(自治)  
不能用abstract修饰私有方法、静态方法、final的方法、final的类。

> 私有方法不能重写
>



### 6.1 由来
举例1：

随着继承层次中一个个新子类的定义，类变得越来越具体，而父类则更一般，更通用。类的设计应该保证父类和子类能够共享特征。有时将一个父类设计得非常抽象，以至于它没有具体的实例，这样的类叫做抽象类。

![](images/image-20220325231608838.png)

举例2：

我们声明一些几何图形类：圆、矩形、三角形类等，发现这些类都有共同特征：求面积、求周长。那么这些共同特征应该抽取到一个共同父类：几何图形类中。但是这些方法在父类中又`无法给出具体的实现`，而是应该交给子类各自具体实现。那么父类在声明这些方法时，`就只有方法签名，没有方法体`，我们把没有方法体的方法称为**抽象方法**。Java语法规定，包含抽象方法的类必须是**抽象类**。

### 6.2 语法格式
+ **抽象类**：被abstract修饰的类。
+ **抽象方法**：被abstract修饰没有方法体的方法。

抽象类的语法格式

```java
[权限修饰符] abstract class 类名{
    
}
[权限修饰符] abstract class 类名 extends 父类{
    
}
```

抽象方法的语法格式

```java
[其他修饰符] abstract 返回值类型 方法名([形参列表]);
```

> 注意：抽象方法没有方法体
>

![](images/image-20220517204707255.png)

代码举例：

```java
public abstract class Animal {
    public abstract void eat();
}
```

```java
public class Cat extends Animal {
    public void eat (){
          System.out.println("小猫吃鱼和猫粮"); 
    }
}
```

```java
public class CatTest {
      public static void main(String[] args) {
        // 创建子类对象
        Cat c = new Cat(); 
       
        // 调用eat方法
        c.eat();
      }
}
```

此时的方法重写，是子类对父类抽象方法的完成实现，我们将这种方法重写的操作，也叫做**实现方法**。

### 6.3 使用说明
1. 抽象类**不能创建对象**，如果创建，编译无法通过而报错。只能创建其非抽象子类的对象。

> 理解：假设创建了抽象类的对象，调用抽象的方法，而抽象方法没有具体的方法体，没有意义。
>
> 抽象类是用来被继承的，抽象类的子类必须重写父类的抽象方法，并提供方法体。若没有重写全部的抽象方法，仍为抽象类。
>

2. 抽象类中，也有构造方法，是供子类创建对象时，初始化父类成员变量使用的。

> 理解：子类的构造方法中，有默认的super()或手动的super(实参列表)，需要访问父类构造方法。
>

3. 抽象类中，不一定包含抽象方法，但是有抽象方法的类必定是抽象类。

> 理解：未包含抽象方法的抽象类，目的就是不想让调用者创建该类对象，通常用于某些特殊的类结构设计。
>

4. 抽象类的子类，必须重写抽象父类中**所有的**抽象方法，否则，编译无法通过而报错。除非该子类也是抽象类。 

> 理解：假设不重写所有抽象方法，则类中可能包含抽象方法。那么创建对象后，调用抽象的方法，没有意义。
>

### 6.4 注意事项
+ 不能用abstract修饰变量、代码块、构造器；
+ 不能用abstract修饰私有方法、静态方法、final的方法、final的类。

### 6.5 应用举例1
![](images/image-20220325232847872.png)

在航运公司系统中，Vehicle类需要定义两个方法分别`计算运输工具的燃料效率`和`行驶距离`。

**问题：**卡车(Truck)和驳船(RiverBarge)的燃料效率和行驶距离的计算方法完全不同。Vehicle类不能提供计算方法，但子类可以。

**解决方案：**Java允许类设计者指定：超类声明一个方法但不提供实现，该方法的实现由子类提供。这样的方法称为抽象方法。有一个或更多抽象方法的类称为抽象类。

```java
//Vehicle是一个抽象类，有两个抽象方法。
public abstract class Vehicle{
    public abstract double calcFuelEfficiency();	//计算燃料效率的抽象方法
    public abstract double calcTripDistance();	//计算行驶距离的抽象方法
}
public class Truck extends Vehicle{
    public double calcFuelEfficiency( )   { //写出计算卡车的燃料效率的具体方法   }
    public double calcTripDistance( )    {  //写出计算卡车行驶距离的具体方法   }
}
public class RiverBarge extends Vehicle{
     public double calcFuelEfficiency( ) { //写出计算驳船的燃料效率的具体方法  }
     public double calcTripDistance( )  {  //写出计算驳船行驶距离的具体方法}
}

```

### 6.6 应用举例2：模板方法设计模式(TemplateMethod)
抽象类体现的就是一种模板模式的设计，抽象类作为多个子类的通用模板，子类在抽象类的基础上进行扩展、改造，但子类总体上会保留抽象类的行为方式。

**解决的问题**：

+ 当功能内部一部分实现是确定的，另一部分实现是不确定的。这时可以把不确定的部分暴露出去，让子类去实现。
+ 换句话说，在软件开发中实现一个算法时，整体步骤很固定、通用，这些步骤已经在父类中写好了。但是某些部分易变，易变部分可以抽象出来，供不同子类实现。这就是一种模板模式。

**类比举例：**英语六级模板

制作月饼的模板：

举例1：

```java
abstract class Template {
    public final void getTime() {
        long start = System.currentTimeMillis();
        code();
        long end = System.currentTimeMillis();
        System.out.println("执行时间是：" + (end - start));
    }

    public abstract void code();
}

class SubTemplate extends Template {
    public void code() {
        for (int i = 0; i < 10000; i++) {
            System.out.println(i);
        }
    }
}

```

举例2：

```java
package com.atguigu.java;
//抽象类的应用：模板方法的设计模式
public class TemplateMethodTest {

    public static void main(String[] args) {
        BankTemplateMethod btm = new DrawMoney();
        btm.process();

        BankTemplateMethod btm2 = new ManageMoney();
        btm2.process();
    }
}
abstract class BankTemplateMethod {
    // 具体方法
    public void takeNumber() {
        System.out.println("取号排队");
    }

    public abstract void transact(); // 办理具体的业务 //钩子方法

    public void evaluate() {
        System.out.println("反馈评分");
    }

    // 模板方法，把基本操作组合到一起，子类一般不能重写
    public final void process() {
        this.takeNumber();

        this.transact();// 像个钩子，具体执行时，挂哪个子类，就执行哪个子类的实现代码

        this.evaluate();
    }
}

class DrawMoney extends BankTemplateMethod {
    public void transact() {
        System.out.println("我要取款！！！");
    }
}

class ManageMoney extends BankTemplateMethod {
    public void transact() {
        System.out.println("我要理财！我这里有2000万美元!!");
    }
}

```

模板方法设计模式是编程中经常用得到的模式。各个框架、类库中都有他的影子，比如常见的有：

+ 数据库访问的封装
+ Junit单元测试
+ JavaWeb的Servlet中关于doGet/doPost方法调用
+ Hibernate中模板程序
+ Spring中JDBCTemlate、HibernateTemplate等

### 6.7 思考与练习
**思考：**

问题1：为什么抽象类不可以使用final关键字声明？

问题2：一个抽象类中可以定义构造器吗？

问题3：是否可以这样理解：抽象类就是比普通类多定义了抽象方法，除了不能直接进行类的实例化操作之外，并没有任何的不同？

**练习1：**

编写一个Employee类，声明为抽象类，包含如下三个属性：name，id，salary。提供必要的构造器和抽象方法：work()。

对于Manager类来说，他既是员工，还具有奖金(bonus)的属性。

请使用继承的思想，设计CommonEmployee类和Manager类，要求类中提供必要的方法进行属性访问。

**练习2：软件外包公司外派管理**

有一家软件外包公司，可以外派开发人员，该公司有两个角色：普通开发人员Developer和项目经理Manager。他们的关系如下图：

![](images/image-20220504164925878.png)

普通开发人员的工作内容是“开发项目”，项目经理的工作内容是“项目管理”。对外的报价是普通开发人员每天500,元，超过60天每天400元。项目经理每天800元，超过60天每天700元。

有一家银行需要1名项目经理、2名开发人员，现场开发90天，计算银行需要付给软件公司的总金额。

提示：创建数组 Employee[] emps = new Employee[3]。其中存储驻场的3名员工。

**练习3：**

创建父类Shape，包含绘制形状的抽象方法draw()。

创建Shape的子类Circle和Rectangle，重写draw()方法，绘制圆形和矩形。

绘制多个圆形和矩形。

**练习4：**

1、声明抽象父类Person，包含抽象方法public abstract void eat();  
2、声明子类中国人Chinese，重写抽象方法，打印用筷子吃饭  
3、声明子类美国人American，重写抽象方法，打印用刀叉吃饭  
4、声明子类印度人Indian，重写抽象方法，打印用手抓饭  
5、声明测试类PersonTest，创建Person数组，存储各国人对象，并遍历数组，调用eat()方法

**练习5：工资系统设计**

编写工资系统，实现不同类型员工(多态)的按月发放工资。如果当月出现某个Employee对象的生日，则将该雇员的工资增加100元。

实验说明：

（1）定义一个Employee类，该类包含：

private成员变量name,number,birthday，其中birthday 为MyDate类的对象；

abstract方法earnings()；

toString()方法输出对象的name,number和birthday。

（2）MyDate类包含:

private成员变量year,month,day ；

toDateString()方法返回日期对应的字符串：xxxx年xx月xx日

（3）定义SalariedEmployee类继承Employee类，实现按月计算工资的员工处理。该类包括：private成员变量monthlySalary；

实现父类的抽象方法earnings(),该方法返回monthlySalary值；toString()方法输出员工类型信息及员工的name，number,birthday。

（4）参照SalariedEmployee类定义HourlyEmployee类，实现按小时计算工资的员工处理。该类包括：

private成员变量wage和hour；

实现父类的抽象方法earnings(),该方法返回wage*hour值；

toString()方法输出员工类型信息及员工的name，number,birthday。

（5）定义PayrollSystem类，创建Employee变量数组并初始化，该数组存放各类雇员对象的引用。利用循环结构遍历数组元素，输出各个对象的类型,name,number,birthday,以及该对象生日。当键盘输入本月月份值时，如果本月是某个Employee对象的生日，还要输出增加工资信息。

```java
//提示：
//定义People类型的数组People c1[]=new People[10];
//数组元素赋值
c1[0]=new People("John","0001",20);
c1[1]=new People("Bob","0002",19);
//若People有两个子类Student和Officer，则数组元素赋值时，可以使父类类型的数组元素指向子类。
c1[0]=new Student("John","0001",20,85.0);
c1[1]=new Officer("Bob","0002",19,90.5);

```

















## 7. 接口(interface)


1，接口的理解:接口的本质是契约、标准、规范，就像我们的法律一样。制定好后大家都要遵守。  
2.定义接口的关键字:interface  
3.接口内部结构的说明:

> 可以声明:  
属性:必须使用public static final修饰  
方法:jdk8之前:声明抽象方法，修饰为public abstract  
idk8:声明静态方法、默认方法  
jdk9:声明私有方法
>
> 
>
> 不可以声明构造器 代码块等
>

```java
public class InterfaceTest {
    public static void main(String[] args) {

        System.out.println(Flyable.MIN_SPEED);
        System.out.println(Flyable.MAX_SPEED);
        System.out.println(Flyable.MAX_SPEED2);
        // MAX_SPEED2 = 1000;//报错 不能更改
        // System.out.println(Flyable.MAX_SPEED2);
    }

}

interface Flyable {
    // 全局变量
    public static final int MIN_SPEED = 10;
    public static final int MAX_SPEED = 100;

    // 可以省略public static final
    int MAX_SPEED2 = 100;

    // 抽象方法
    public abstract void fly();

    // 可以简写
    void fly2();

}
```

接口与类的关系，实现关系

格式 class A implements B,C{ }

A 相较于 SuperA 来讲叫做子类

A 相较于 B，C 来讲 叫做实现类



满足此关系之后，说明:

类可以实现多个接口。

类针对于接口的多实现，一定程度上就弥补了类的单继承的局限性。

类必须将实现接口中的所有方法都重写（或实现），方可实例化。否则，此实现类必须声明为抽象类



接口与接口间的关系：继承关系，且可以多继承

接口的多态性 ： 接口名 变量名 = new 实现类对象;



面试题 区分抽象类和接口

 

共性 都可以声明抽象方法 都不能实例化



不同

> 抽象类一定有构造器 接口没有构造器
>
> 类与类之间继承关系 类与接口之间时实现关系 接口与接口之间时多继承关系
>



 



### 7.1 类比
生活中大家每天都在用USB接口，那么USB接口与我们今天要学习的接口有什么相同点呢？

```plain
 USB，（Universal Serial Bus，通用串行总线）是Intel公司开发的总线架构，使得在计算机上添加串行设备（鼠标、键盘、打印机、扫描仪、摄像头、充电器、MP3机、手机、数码相机、移动硬盘等）非常容易。
```

其实，不管是电脑上的USB插口，还是其他设备上的USB插口都只是`遵循了USB规范`的一种具体设备而已。

![](images/bbcc80f541000c71b81650cfaa770c86.png)

只要设备遵循USB规范的，那么就可以与电脑互联，并正常通信。至于这个设备、电脑是哪个厂家制造的，内部是如何实现的，我们都无需关心。

Java的软件系统会有很多模块组成，那么各个模块之间也应该采用这种`面向接口`的`低耦合`，为系统提供更好的可扩展性和可维护性。

### 7.2 概述
接口就是规范，定义的是一组规则，体现了现实世界中“如果你是/要...则必须能...”的思想。继承是一个"是不是"的is-a关系，而接口实现则是 "能不能"的`has-a`关系。

+ 例如：电脑都预留了可以插入USB设备的USB接口，USB接口具备基本的数据传输的开启功能和关闭功能。你能不能用USB进行连接，或是否具备USB通信功能，就看你能否遵循USB接口规范
+ 例如：Java程序是否能够连接使用某种数据库产品，那么要看该数据库产品能否实现Java设计的JDBC规范

> 接口的本质是契约、标准、规范，就像我们的法律一样。制定好后大家都要遵守。
>

### 7.3 定义格式
接口的定义，它与定义类方式相似，但是使用 `interface` 关键字。它也会被编译成.class文件，但一定要明确它并不是类，而是另外一种引用数据类型。

> 引用数据类型：数组，类，枚举，接口，注解。
>

#### 7.3.1 接口的声明格式
```java
[修饰符] interface 接口名{
    //接口的成员列表：
    // 公共的静态常量
    // 公共的抽象方法
    
    // 公共的默认方法（JDK1.8以上）
    // 公共的静态方法（JDK1.8以上）
    // 私有方法（JDK1.9以上）
}
```

示例代码：

```java
package com.atguigu.interfacetype;

public interface USB3{
    //静态常量
    long MAX_SPEED = 500*1024*1024;//500MB/s

    //抽象方法
    void in();
    void out();

    //默认方法
    default void start(){
        System.out.println("开始");
    }
    default void stop(){
        System.out.println("结束");
    }

    //静态方法
    static void show(){
        System.out.println("USB 3.0可以同步全速地进行读写操作");
    }
}
```

#### 7.3.2 接口的成员说明
**在JDK8.0 之前**，接口中只允许出现：

（1）公共的静态的常量：其中`public static final`可以省略

（2）公共的抽象的方法：其中`public abstract`可以省略

> 理解：接口是从多个相似类中抽象出来的规范，不需要提供具体实现
>

**在JDK8.0 时**，接口中允许声明`默认方法`和`静态方法`：

（3）公共的默认的方法：其中public 可以省略，建议保留，但是default不能省略

（4）公共的静态的方法：其中public 可以省略，建议保留，但是static不能省略

**在JDK9.0 时**，接口又增加了：

（5）私有方法

除此之外，接口中没有构造器，没有初始化块，因为接口中没有成员变量需要动态初始化。

### 7.4 接口的使用规则
**1、类实现接口（implements）**

接口**不能创建对象**，但是可以被类实现（`implements` ，类似于被继承）。

类与接口的关系为实现关系，即**类实现接口**，该类可以称为接口的实现类。实现的动作类似继承，格式相仿，只是关键字不同，实现使用 ` implements`关键字。

```java
【修饰符】 class 实现类  implements 接口{
    // 重写接口中抽象方法【必须】，当然如果实现类是抽象类，那么可以不重写
      // 重写接口中默认方法【可选】
}

【修饰符】 class 实现类 extends 父类 implements 接口{
    // 重写接口中抽象方法【必须】，当然如果实现类是抽象类，那么可以不重写
      // 重写接口中默认方法【可选】
}
```

注意：

1. 如果接口的实现类是非抽象类，那么必须`重写接口中所有抽象方法`。
2. 默认方法可以选择保留，也可以重写。

> 重写时，default单词就不要再写了，它只用于在接口中表示默认方法，到类中就没有默认方法的概念了
>

3. 接口中的静态方法不能被继承也不能被重写

举例：

```java
interface USB{		// 
    public void start() ;
    public void stop() ;	
}
class Computer{
    public static void show(USB usb){	
        usb.start() ;
        System.out.println("=========== USB 设备工作 ========") ;
        usb.stop() ;
    }
};
class Flash implements USB{
    public void start(){	// 重写方法
        System.out.println("U盘开始工作。") ;
    }
    public void stop(){		// 重写方法
        System.out.println("U盘停止工作。") ;
    }
};
class Print implements USB{
    public void start(){	// 重写方法
        System.out.println("打印机开始工作。") ;
    }
    public void stop(){		// 重写方法
        System.out.println("打印机停止工作。") ;
    }
};
public class InterfaceDemo{
    public static void main(String args[]){
        Computer.show(new Flash()) ;
        Computer.show(new Print()) ;

        c.show(new USB(){
            public void start(){
                System.out.println("移动硬盘开始运行");
            }
            public void stop(){
                System.out.println("移动硬盘停止运行");
            }
        });
    }
};
```

**2、接口的多实现（implements）**

之前学过，在继承体系中，一个类只能继承一个父类。而对于接口而言，一个类是可以实现多个接口的，这叫做接口的`多实现`。并且，一个类能继承一个父类，同时实现多个接口。

实现格式：

```java
【修饰符】 class 实现类  implements 接口1，接口2，接口3。。。{
    // 重写接口中所有抽象方法【必须】，当然如果实现类是抽象类，那么可以不重写
      // 重写接口中默认方法【可选】
}

【修饰符】 class 实现类 extends 父类 implements 接口1，接口2，接口3。。。{
    // 重写接口中所有抽象方法【必须】，当然如果实现类是抽象类，那么可以不重写
      // 重写接口中默认方法【可选】
}
```

> 接口中，有多个抽象方法时，实现类必须重写所有抽象方法。**如果抽象方法有重名的，只需要重写一次**。
>

举例：

![](images/1562216188519.png)

定义多个接口：

```java
package com.atguigu.interfacetype;

public interface A {
    void showA();
}
```

```java
package com.atguigu.interfacetype;

public interface B {
    void showB();
}
```

定义实现类：

```java
package com.atguigu.interfacetype;

public class C implements A,B {
    @Override
    public void showA() {
        System.out.println("showA");
    }

    @Override
    public void showB() {
        System.out.println("showB");
    }
}

```

测试类

```java
package com.atguigu.interfacetype;

public class TestC {
    public static void main(String[] args) {
        C c = new C();
        c.showA();
        c.showB();
    }
}
```

**3、接口的多继承(extends)**

一个接口能继承另一个或者多个接口，接口的继承也使用 `extends` 关键字，子接口继承父接口的方法。

定义父接口：

```java
package com.atguigu.interfacetype;

public interface Chargeable {
    void charge();
    void in();
    void out();
}
```

定义子接口：

```java
package com.atguigu.interfacetype;

public interface UsbC extends Chargeable,USB3 {
    void reverse();
}
```

定义子接口的实现类：

```java
package com.atguigu.interfacetype;

public class TypeCConverter implements UsbC {
    @Override
    public void reverse() {
        System.out.println("正反面都支持");
    }

    @Override
    public void charge() {
        System.out.println("可充电");
    }

    @Override
    public void in() {
        System.out.println("接收数据");
    }

    @Override
    public void out() {
        System.out.println("输出数据");
    }
}
```

> 所有父接口的抽象方法都有重写。
>
> 方法签名相同的抽象方法只需要实现一次。
>

**4、接口与实现类对象构成多态引用**

实现类实现接口，类似于子类继承父类，因此，接口类型的变量与实现类的对象之间，也可以构成多态引用。通过接口类型的变量调用方法，最终执行的是你new的实现类对象实现的方法体。

接口的不同实现类：

```java
package com.atguigu.interfacetype;

public class Mouse implements USB3 {
    @Override
    public void out() {
        System.out.println("发送脉冲信号");
    }

    @Override
    public void in() {
        System.out.println("不接收信号");
    }
}
```

```java
package com.atguigu.interfacetype;

public class KeyBoard implements USB3{
    @Override
    public void in() {
        System.out.println("不接收信号");
    }

    @Override
    public void out() {
        System.out.println("发送按键信号");
    }
}

```

测试类

```java
package com.atguigu.interfacetype;

public class TestComputer {
    public static void main(String[] args) {
        Computer computer = new Computer();
        USB3 usb = new Mouse();
        computer.setUsb(usb);
        usb.start();
        usb.out();
        usb.in();
        usb.stop();
        System.out.println("--------------------------");

        usb = new KeyBoard();
        computer.setUsb(usb);
        usb.start();
        usb.out();
        usb.in();
        usb.stop();
        System.out.println("--------------------------");

        usb = new MobileHDD();
        computer.setUsb(usb);
        usb.start();
        usb.out();
        usb.in();
        usb.stop();
    }
}
```

**5、使用接口的静态成员**

接口不能直接创建对象，但是可以通过接口名直接调用接口的静态方法和静态常量。

```java
package com.atguigu.interfacetype;

public class TestUSB3 {
    public static void main(String[] args) {
        //通过“接口名.”调用接口的静态方法 (JDK8.0才能开始使用)
        USB3.show();
        //通过“接口名.”直接使用接口的静态常量
        System.out.println(USB3.MAX_SPEED);
    }
}
```

**6、使用接口的非静态方法**

+ 对于接口的静态方法，直接使用“`接口名.`”进行调用即可
    - 也只能使用“接口名."进行调用，不能通过实现类的对象进行调用
+ 对于接口的抽象方法、默认方法，只能通过实现类对象才可以调用
    - 接口不能直接创建对象，只能创建实现类的对象

```java
package com.atguigu.interfacetype;

public class TestMobileHDD {
    public static void main(String[] args) {
        //创建实现类对象
        MobileHDD b = new MobileHDD();

        //通过实现类对象调用重写的抽象方法，以及接口的默认方法，如果实现类重写了就执行重写的默认方法，如果没有重写，就执行接口中的默认方法
        b.start();
        b.in();
        b.stop();

        //通过接口名调用接口的静态方法
//        MobileHDD.show();
//        b.show();
        Usb3.show();
    }
}
```

```java
public class Test {

    //在JDK8以前，接口中只能定义全局常量和抽象方法
    //JDK8以后，接口中可以定义静态方法和默认方法
    public static void main(String[] args) {
        //接口中的静态方法只能通过接口名调用
        MyInterface1.method1();
        //接口中的默认方法可以通过实现类对象调用，也可以通过接口名调用
        MyInterface1.method2();
                new MyInterface1Impl().method2();
            }
        
        }
        interface MyInterface1{
            //全局常量
            public static final int NUM = 10;
            //抽象方法
            public abstract void method();
            //静态方法
            public static void method1(){
                System.out.println("静态方法");
            }
            //默认方法
            public static void method2(){
        System.out.println("默认方法");
    }

}
class MyInterface1Impl implements MyInterface1{

    @Override
    public void method() {
        System.out.println("抽象方法");
    }
    public void method2(){
        System.out.println("实现类重写的默认方法");
    }

}
//接口中的静态方法只能通过接口名调用，不能通过实现类对象调用
//接口中的默认方法可以通过实现类对象调用，也可以通过接口名调用
//接口中声明的默认方法可以实现类继承，实现类在没有重写的情况下，默认使用接口中的默认方法,如果实现类重写了此方法，则使用实现类重写的方法
//类实现了两个接口，而两个接口中都有默认方法，则类必须重写此方法，否则编译报错
```

### 7.5 JDK8中相关冲突问题
#### 7.5.1 默认方法冲突问题
**（1）类优先原则**

当一个类，既继承一个父类，又实现若干个接口时，父类中的成员方法与接口中的抽象方法重名，子类就近选择执行父类的成员方法。代码如下：

定义接口：

```java
package com.atguigu.interfacetype;

public interface Friend {
    default void date(){//约会
        System.out.println("吃喝玩乐");
    }
}
```

定义父类：

```java
package com.atguigu.interfacetype;

public class Father {
    public void date(){//约会
        System.out.println("爸爸约吃饭");
    }
}
```

定义子类：

```java
package com.atguigu.interfacetype;

public class Son extends Father implements Friend {
    @Override
    public void date() {
        //(1)不重写默认保留父类的
        //(2)调用父类被重写的
//        super.date();
        //(3)保留父接口的
//        Friend.super.date();
        //(4)完全重写
        System.out.println("跟康师傅学Java");
    }
}
```

定义测试类：

```java
package com.atguigu.interfacetype;

public class TestSon {
    public static void main(String[] args) {
        Son s = new Son();
        s.date();
    }
}
```

**（2）接口冲突（左右为难）**

+ 当一个类同时实现了多个父接口，而多个父接口中包含方法签名相同的默认方法时，怎么办呢？

![](images/选择困难.jpg)

无论你多难抉择，最终都是要做出选择的。

声明接口：

```java
package com.atguigu.interfacetype;

public interface BoyFriend {
    default void date(){//约会
        System.out.println("神秘约会");
    }
}
```

选择保留其中一个，通过“`接口名.super.方法名`"的方法选择保留哪个接口的默认方法。

```java
package com.atguigu.interfacetype;

public class Girl implements Friend,BoyFriend{

    @Override
    public void date() {
        //(1)保留其中一个父接口的
//        Friend.super.date();
//        BoyFriend.super.date();
        //(2)完全重写
        System.out.println("跟康师傅学Java");
    }

}
```

测试类

```java
package com.atguigu.interfacetype;

public class TestGirl {
    public static void main(String[] args) {
        Girl girl = new Girl();
        girl.date();
    }
}
```

+ 当一个子接口同时继承了多个接口，而多个父接口中包含方法签名相同的默认方法时，怎么办呢？

另一个父接口：

```java
package com.atguigu.interfacetype;

public interface USB2 {
    //静态常量
    long MAX_SPEED = 60*1024*1024;//60MB/s

    //抽象方法
    void in();
    void out();

    //默认方法
    public default void start(){
        System.out.println("开始");
    }
    public default void stop(){
        System.out.println("结束");
    }

    //静态方法
    public static void show(){
        System.out.println("USB 2.0可以高速地进行读写操作");
    }
}
```

子接口：

```java
package com.atguigu.interfacetype;

public interface USB extends USB2,USB3 {
    @Override
    default void start() {
        System.out.println("Usb.start");
    }

    @Override
    default void stop() {
        System.out.println("Usb.stop");
    }
}

```

> 小贴士：
>
> 子接口重写默认方法时，default关键字可以保留。
>
> 子类重写默认方法时，default关键字不可以保留。
>

#### 7.5.2 常量冲突问题
+ 当子类继承父类又实现父接口，而父类中存在与父接口常量同名的成员变量，并且该成员变量名在子类中仍然可见。
+ 当子类同时实现多个接口，而多个接口存在相同同名常量。

此时在子类中想要引用父类或父接口的同名的常量或成员变量时，就会有冲突问题。

父类和父接口：

```java
package com.atguigu.interfacetype;

public class SuperClass {
    int x = 1;
}
```

```java
package com.atguigu.interfacetype;

public interface SuperInterface {
    int x = 2;
    int y = 2;
}
```

```java
package com.atguigu.interfacetype;

public interface MotherInterface {
    int x = 3;
}
```

子类：

```java
package com.atguigu.interfacetype;

public class SubClass extends SuperClass implements SuperInterface,MotherInterface {
    public void method(){
//        System.out.println("x = " + x);//模糊不清
        System.out.println("super.x = " + super.x);
        System.out.println("SuperInterface.x = " + SuperInterface.x);
        System.out.println("MotherInterface.x = " + MotherInterface.x);
        System.out.println("y = " + y);//没有重名问题，可以直接访问
    }
}
```

### 7.6 接口的总结与面试题
+ 接口本身不能创建对象，只能创建接口的实现类对象，接口类型的变量可以与实现类对象构成多态引用。
+ 声明接口用interface，接口的成员声明有限制：
    - （1）公共的静态常量
    - （2）公共的抽象方法
    - （3）公共的默认方法（JDK8.0 及以上）
    - （4）公共的静态方法（JDK8.0 及以上）
    - （5）私有方法（JDK9.0 及以上）
+ 类可以实现接口，关键字是implements，而且支持多实现。如果实现类不是抽象类，就必须实现接口中所有的抽象方法。如果实现类既要继承父类又要实现父接口，那么继承（extends）在前，实现（implements）在后。
+ 接口可以继承接口，关键字是extends，而且支持多继承。
+ 接口的默认方法可以选择重写或不重写。如果有冲突问题，另行处理。子类重写父接口的默认方法，要去掉default，子接口重写父接口的默认方法，不要去掉default。
+ 接口的静态方法不能被继承，也不能被重写。接口的静态方法只能通过“接口名.静态方法名”进行调用。

**面试题**

**1、为什么接口中只能声明公共的静态的常量？**

因为接口是标准规范，那么在规范中需要声明一些底线边界值，当实现者在实现这些规范时，不能去随意修改和触碰这些底线，否则就有“危险”。

例如：USB1.0规范中规定最大传输速率是1.5Mbps，最大输出电流是5V/500mA

           USB3.0规范中规定最大传输速率是5Gbps(500MB/s)，最大输出电流是5V/900mA

例如：尚硅谷学生行为规范中规定学员，早上8:25之前进班，晚上21:30之后离开等等。

**2、为什么JDK8.0 之后允许接口定义静态方法和默认方法呢？因为它违反了接口作为一个抽象标准定义的概念。**

`静态方法`：因为之前的标准类库设计中，有很多Collection/Colletions或者Path/Paths这样成对的接口和类，后面的类中都是静态方法，而这些静态方法都是为前面的接口服务的，那么这样设计一对API，不如把静态方法直接定义到接口中使用和维护更方便。

`默认方法`：（1）我们要在已有的老版接口中提供新方法时，如果添加抽象方法，就会涉及到原来使用这些接口的类就会有问题，那么为了保持与旧版本代码的兼容性，只能允许在接口中定义默认方法实现。比如：Java8中对Collection、List、Comparator等接口提供了丰富的默认方法。（2）当我们接口的某个抽象方法，在很多实现类中的实现代码是一样的，此时将这个抽象方法设计为默认方法更为合适，那么实现类就可以选择重写，也可以选择不重写。

**3、为什么JDK1.9要允许接口定义私有方法呢？因为我们说接口是规范，规范是需要公开让大家遵守的。**

**私有方法**：因为有了默认方法和静态方法这样具有具体实现的方法，那么就可能出现多个方法由共同的代码可以抽取，而这些共同的代码抽取出来的方法又只希望在接口内部使用，所以就增加了私有方法。

### 7.7 接口与抽象类之间的对比
![](images/image-20220328002053452.png)

> 在开发中，常看到一个类不是去继承一个已经实现好的类，而是要么继承抽象类，要么实现接口。
>

### 7.8 练习
**笔试题：**排错

```java
interface A {
    int x = 0;
}
class B {
    int x = 1;
}
class C extends B implements A {
    public void pX() {
        System.out.println(x);
    }
    public static void main(String[] args) {
        new C().pX();
    }
}

```

**笔试题：**排错

```java
interface Playable {
    void play();
}

interface Bounceable {
    void play();
}

interface Rollable extends Playable, Bounceable {
    Ball ball = new Ball("PingPang");

}

class Ball implements Rollable {
    private String name;

    public String getName() {
        return name;
    }

    public Ball(String name) {
        this.name = name;
    }

    public void play() {
        ball = new Ball("Football");
        System.out.println(ball.getName());
    }
}

```

**练习1：**

定义一个接口用来实现两个对象的比较。

```java
interface CompareObject{
    //若返回值是 0 , 代表相等; 若为正数，代表当前对象大；负数代表当前对象小
    public int compareTo(Object o);  
}
```

定义一个Circle类，声明redius属性，提供getter和setter方法

定义一个ComparableCircle类，继承Circle类并且实现CompareObject接口。在ComparableCircle类中给出接口中方法compareTo的实现体，用来比较两个圆的半径大小。

定义一个测试类InterfaceTest，创建两个ComparableCircle对象，调用compareTo方法比较两个类的半径大小。

思考：参照上述做法定义矩形类Rectangle和ComparableRectangle类，在ComparableRectangle类中给出compareTo方法的实现，比较两个矩形的面积大小。

**练习2：交通工具案例**

阿里的一个工程师，声明的属性和方法如下：

![](images/image-20220504172547709.png)

其中，有一个乘坐交通工具的方法takingVehicle()，在此方法中调用交通工具的run()。为了出行方便，他买了一辆捷安特自行车、一辆雅迪电动车和一辆奔驰轿车。这里涉及到的相关类及接口关系如下：

![](images/image-20220504172918861.png)

其中，电动车增加动力的方式是充电，轿车增加动力的方式是加油。在具体交通工具的run()中调用其所在类的相关属性信息。

请编写相关代码，并测试。

提示：创建Vehicle[]数组，保存阿里工程师的三辆交通工具，并分别在工程师的takingVehicle()中调用。















## 8. 内部类（InnerClass)
### 8.1 概述


内部类举例

thread 类声明了 State 类 ，表示线程生命周期

SashMap 类声明了 Node 类 表示封装 key 和 value



4.内部类的分类:(参考变量的分类)  
成员内部类:直接声明在外部类的里面。  
使用static修饰的:静态的成员内部类

> 不使用static修饰的:非静态的成员内部类  
局部内部类:声明在方法内、构造器内、代码块内的内部类  
匿名的局部内部类  
非匿名的局部内部类
>

内部类这节要讲的知识:

> 成员内部类的理解
>

> 如何创建成员内部类的实例
>

> 如何在成员内部类中调用外部类的结构
>

> 局部内部类的基本使用
>



关于成员内部类的理解

> 从类的角度看:  
内部可以声明属性、方法、构造器、代码块、内部类等结构  
此内部类可以声明父类，可以实现接口  
可以使用final修饰  
可以使用abstract修饰
>

> 从外部类的成员的角度看:  
在内部可以调用外部类的结构。比如:属性、方法等  
除了使用public、缺省权限修饰之外，还可以使用private、protected修饰  
可以使用static修饰
>

```java
public class OutherClassTest {
    public static void main(String[] args) {
        SubA subA = new SubA();
        subA.method();

        // 其它写法

        //方法1 提供接口 匿名实现类的对象
        A a = new A() {
            @Override
            public void method() {
                System.out.println("匿名实现类的方法");
            }
        };
        a.method(); // 调用匿名内部类的方法

        //方法2
        new SubA(){
            public void method(){
                System.out.println("匿名实现类的方法");
            }
        }
        .method(); // 调用匿名内部类的方法
    }
}

interface A {
    void method();
}

class SubA implements A {
    @Override
    public void method() {
        System.out.println("SubA");
    }
}
```

### 8.1.1 什么是内部类
```java
public class OutherClassTest {
    public static void main(String[] args) {
        SubA subA = new SubA();
        subA.method();

        // 其它写法

        //方法1 提供接口 匿名实现类的对象
        A a = new A() {
            @Override
            public void method() {
                System.out.println("匿名实现类的方法");
            }
        };
        a.method(); // 调用匿名内部类的方法

        //方法2
        new SubA(){
            @Override
            public void method(){
                System.out.println("匿名实现类的方法");
            }
        }
        .method(); // 调用匿名内部类的方法

        //方法3
        C s1 = new C();
        s1.method();

        //方法4 提供了继承于抽象类的匿名子类的对象
        B b = new B(){
            @Override
            public void method() {
                System.out.println("继承于抽象类的子类调用的方法");
            }
        };

        b.method();

        //方法5  
        new B(){
            @Override
            public void method() {
                System.out.println("继承于抽象类的子类调用的方法");
            }
        }
        .method(); // 调用匿名内部类的方法

        //方法6
        D d = new D();
        d.method();

        //方法7
        D f = new D(){
            
        };
        f.method();
        System.out.println(f.getClass());
        System.out.println(f.getClass().getSuperclass());

        D f2 = new D(){
            @Override
            public void method() {
                System.out.println("继承于抽象类的子类调用的方法");
            }
        };
        f2.method();
    }
    
}

interface A {
    void method();
}

class SubA implements A {
    @Override
    public void method() {
        System.out.println("SubA");
    }
}

abstract class B {
    public abstract void method();
    //抽象类
    
}

class C extends B {
    @Override
    public void method() {
        System.out.println("C");
    }
}

class D {
    public void method() {
        System.out.println("D");
    }
}
```



将一个类A定义在另一个类B里面，里面的那个类A就称为`内部类（InnerClass）`，类B则称为`外部类（OuterClass）`。

#### 8.1.2 为什么要声明内部类呢
具体来说，当一个事物A的内部，还有一个部分需要一个完整的结构B进行描述，而这个内部的完整的结构B又只为外部事物A提供服务，不在其他地方单独使用，那么整个内部的完整结构B最好使用内部类。

总的来说，遵循`高内聚、低耦合`的面向对象开发原则。

#### 8.1.3 内部类的分类
根据内部类声明的位置（如同变量的分类），我们可以分为：

![](images/image-20221124223912529.png)

### 8.2 成员内部类
#### 8.2.1 概述
如果成员内部类中不使用外部类的非静态成员，那么通常将内部类声明为静态内部类，否则声明为非静态内部类。

**语法格式：**

```java
[修饰符] class 外部类{
    [其他修饰符] [static] class 内部类{
    }
}
```

**成员内部类的使用特征，概括来讲有如下两种角色：**

+ 成员内部类作为`类的成员的角色`：
    - 和外部类不同，Inner class还可以声明为private或protected；
    - 可以调用外部类的结构。（注意：在静态内部类中不能使用外部类的非静态成员）
    - Inner class 可以声明为static的，但此时就不能再使用外层类的非static的成员变量；
+ 成员内部类作为`类的角色`：
    - 可以在内部定义属性、方法、构造器等结构
    - 可以继承自己的想要继承的父类，实现自己想要实现的父接口们，和外部类的父类和父接口无关
    - 可以声明为abstract类 ，因此可以被其它的内部类继承
    - 可以声明为final的，表示不能被继承
    - 编译以后生成OuterClass$InnerClass.class字节码文件（也适用于局部内部类）

注意点：

2. 外部类访问成员内部类的成员，需要“内部类.成员”或“内部类对象.成员”的方式
3. 成员内部类可以直接使用外部类的所有成员，包括私有的数据
4. 当想要在外部类的静态成员部分使用内部类时，可以考虑内部类声明为静态的

#### 8.2.2 创建成员内部类对象
+ 实例化静态内部类

```plain
外部类名.静态内部类名 变量 = 外部类名.静态内部类名();
变量.非静态方法();
```

+ 实例化非静态内部类

```plain
外部类名 变量1 = new 外部类();
外部类名.非静态内部类名 变量2 = 变量1.new 非静态内部类名();
变量2.非静态方法();
```

#### 8.2.3 举例
```java
public class TestMemberInnerClass {
    public static void main(String[] args) {
        //创建静态内部类实例，并调用方法
        Outer.StaticInner inner = new Outer.StaticInner();
        inner.inFun();
        //调用静态内部类静态方法
        Outer.StaticInner.inMethod();

        System.out.println("*****************************");
        
        //创建非静态内部类实例（方式1），并调用方法
        Outer outer = new Outer();
        Outer.NoStaticInner inner1 = outer.new NoStaticInner();
        inner1.inFun();

        //创建非静态内部类实例（方式2）
        Outer.NoStaticInner inner2 = outer.getNoStaticInner();
        inner1.inFun();
    }
}
class Outer{
    private static String a = "外部类的静态a";
    private static String b  = "外部类的静态b";
    private String c = "外部类对象的非静态c";
    private String d = "外部类对象的非静态d";

    static class StaticInner{
        private static String a ="静态内部类的静态a";
        private String c = "静态内部类对象的非静态c";
        public static void inMethod(){
            System.out.println("Inner.a = " + a);
            System.out.println("Outer.a = " + Outer.a);
            System.out.println("b = " + b);
        }
        public void inFun(){
            System.out.println("Inner.inFun");
            System.out.println("Outer.a = " + Outer.a);
            System.out.println("Inner.a = " + a);
            System.out.println("b = " + b);
            System.out.println("c = " + c);
//            System.out.println("d = " + d);//不能访问外部类的非静态成员
        }
    }

    class NoStaticInner{
        private String a = "非静态内部类对象的非静态a";
        private String c = "非静态内部类对象的非静态c";

        public void inFun(){
            System.out.println("NoStaticInner.inFun");
            System.out.println("Outer.a = " + Outer.a);
            System.out.println("a = " + a);
            System.out.println("b = " + b);
            System.out.println("Outer.c = " + Outer.this.c);
            System.out.println("c = " + c);
            System.out.println("d = " + d);
        }
    }


    public NoStaticInner getNoStaticInner(){
        return new NoStaticInner();
    }
}
```

### 8.3 局部内部类
#### 8.3.1 非匿名局部内部类
语法格式：

```java
[修饰符] class 外部类{
    [修饰符] 返回值类型  方法名(形参列表){
            [final/abstract] class 内部类{
        }
    }    
}
```

+ 编译后有自己的独立的字节码文件，只不过在内部类名前面冠以外部类名、$符号、编号。
    - 这里有编号是因为同一个外部类中，不同的方法中存在相同名称的局部内部类
+ 和成员内部类不同的是，它前面不能有权限修饰符等
+ 局部内部类如同局部变量一样，有作用域
+ 局部内部类中是否能访问外部类的非静态的成员，取决于所在的方法

举例：

```java
/**
 * ClassName: TestLocalInner
 * @Author 尚硅谷-宋红康
 * @Create 17:19
 * @Version 1.0
 */
public class TestLocalInner {
    public static void main(String[] args) {
        Outer.outMethod();
        System.out.println("-------------------");

        Outer out = new Outer();
        out.outTest();
        System.out.println("-------------------");

        Runner runner = Outer.getRunner();
        runner.run();

    }
}
class Outer{

    public static void outMethod(){
        System.out.println("Outer.outMethod");
        final String c = "局部变量c";
        class Inner{
            public void inMethod(){
                System.out.println("Inner.inMethod");
                System.out.println(c);
            }
        }

        Inner in = new Inner();
        in.inMethod();
    }

    public void outTest(){
        class Inner{
            public void inMethod1(){
                System.out.println("Inner.inMethod1");
            }
        }

        Inner in = new Inner();
        in.inMethod1();
    }

    public static Runner getRunner(){
        class LocalRunner implements Runner{
            @Override
            public void run() {
                System.out.println("LocalRunner.run");
            }
        }
        return new LocalRunner();
    }

}
interface Runner{
    void run();
}
```

#### 8.3.2 匿名内部类
因为考虑到这个子类或实现类是一次性的，那么我们“费尽心机”的给它取名字，就显得多余。那么我们完全可以使用匿名内部类的方式来实现，避免给类命名的问题。

```java
new 父类([实参列表]){
    重写方法...
}
```

```java
new 父接口(){
    重写方法...
}
```

举例1：使用匿名内部类的对象直接调用方法：

```java
interface A{
    void a();
}
public class Test{
    public static void main(String[] args){
        new A(){
            @Override
            public void a() {
                System.out.println("aaaa");
            }
        }.a();
    }
}
```

举例2：通过父类或父接口的变量多态引用匿名内部类的对象

```java
interface A{
    void a();
}
public class Test{
    public static void main(String[] args){
        A obj = new A(){
            @Override
            public void a() {
                System.out.println("aaaa");
            }
        };
        obj.a();
    }
}
```

举例3：匿名内部类的对象作为实参

```java
interface A{
    void method();
}
public class Test{
    public static void test(A a){
        a.method();
    }
    
    public static void main(String[] args){
        test(new A(){

            @Override
            public void method() {
                System.out.println("aaaa");
            }
        });
    }   
}
```

### 8.4 练习
练习：判断输出结果为何？

```java
public class Test {
    public Test() {
        Inner s1 = new Inner();
        s1.a = 10;
        Inner s2 = new Inner();
        s2.a = 20;
        Test.Inner s3 = new Test.Inner();
        System.out.println(s3.a);
    }
    class Inner {
        public int a = 5;
    }
    public static void main(String[] args) {
        Test t = new Test();
        Inner r = t.new Inner();
        System.out.println(r.a);
    }
}

```

练习2：

编写一个匿名内部类，它继承Object，并在匿名内部类中，声明一个方法public void test()打印尚硅谷。

请编写代码调用这个方法。

```java
package com.atguigu.test01;

public class Test01 {
    public static void main(String[] args) {
        new Object(){
            public void test(){
                System.out.println("尚硅谷");
            }
        }.test();
    }
}

```

## 9. 枚举类
```java
public class SeasonTest {
    //枚举类
    public static void main(String[] args) {
        Season spring = Season.SPRING;
        System.out.println(spring);
        System.out.println(Season.SPRING.getSeasonName());
        System.out.println(Season.SPRING.getSeasonDesc());

    }
}

enum Season {
    SPRING("春天", "春暖花开"),
    SUMMER("夏天", "夏日炎炎"),
    AUTUMN("秋天", "秋高气爽"),
    WINTER("冬天", "冰天雪地");

    private String seasonName;
    private String seasonDesc;

    private Season(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }

    @Override   
    public String toString() {
        return "Season{" +
                "seasonName='" + seasonName + '\'' +
                ", seasonDesc='" + seasonDesc + '\'' +
                '}';
    }
}

//枚举类
//枚举类是一种特殊的类，它用于表示一组常量。在Java中，枚举类使用关键字enum来定义。
//枚举类中的每个常量都是一个枚举类型的实例，它们都是public static final的，可以直接通过枚举类名来访问。
//枚举类可以包含构造方法、成员变量、成员方法和静态方法等。
```

### 9.1 概述
+ 枚举类型本质上也是一种类，只不过是这个类的对象是有限的、固定的几个，不能让用户随意创建。
+ 枚举类的例子举不胜举：
    - `星期`：Monday(星期一)......Sunday(星期天)
    - `性别`：Man(男)、Woman(女)
    - `月份`：January(1月)......December(12月)
    - `季节`：Spring(春节)......Winter(冬天)
    - `三原色`：red(红色)、green(绿色)、blue(蓝色)
    - `支付方式`：Cash（现金）、WeChatPay（微信）、Alipay(支付宝)、BankCard(银行卡)、CreditCard(信用卡)
    - `就职状态`：Busy(忙碌)、Free(空闲)、Vocation(休假)、Dimission(离职)
    - `订单状态`：Nonpayment（未付款）、Paid（已付款）、Fulfilled（已配货）、Delivered（已发货）、Checked（已确认收货）、Return（退货）、Exchange（换货）、Cancel（取消）
    - `线程状态`：创建、就绪、运行、阻塞、死亡
+ **若枚举只有一个对象, 则可以作为一种单例模式的实现方式。**
+ 枚举类的实现：
    - 在JDK5.0 之前，需要程序员自定义枚举类型。
    - 在JDK5.0 之后，Java支持`enum`关键字来快速定义枚举类型。



开发中，如果针对某个类其实例是确定个数的，则推荐使用枚举类

如果枚举类的实例只有一个，则可以看作是单类的形式



### 9.2 定义枚举类（JDK5.0 之前）
在JDK5.0 之前如何声明枚举类呢？

+ `私有化`类的构造器，保证不能在类的外部创建其对象
+ 在类的内部创建枚举类的实例。声明为：`public static final` ，对外暴露这些常量对象
+ 对象如果有`实例变量`，应该声明为`private final`（建议，不是必须），并在构造器中初始化

示例代码：

```java
class Season{
    private final String SEASONNAME;//季节的名称
    private final String SEASONDESC;//季节的描述
    private Season(String seasonName,String seasonDesc){
        this.SEASONNAME = seasonName;
        this.SEASONDESC = seasonDesc;
    }
    public static final Season SPRING = new Season("春天", "春暖花开");
    public static final Season SUMMER = new Season("夏天", "夏日炎炎");
    public static final Season AUTUMN = new Season("秋天", "秋高气爽");
    public static final Season WINTER = new Season("冬天", "白雪皑皑");

    @Override
    public String toString() {
        return "Season{" +
                "SEASONNAME='" + SEASONNAME + '\'' +
                ", SEASONDESC='" + SEASONDESC + '\'' +
                '}';
    }
}
class SeasonTest{
    public static void main(String[] args) {
        System.out.println(Season.AUTUMN);
    }
}
```

### 9.3 定义枚举类（JDK5.0 之后）
#### 9.3.1 enum关键字声明枚举
```java
【修饰符】 enum 枚举类名{
    常量对象列表
}

【修饰符】 enum 枚举类名{
    常量对象列表;
    
    对象的实例变量列表;
}
```

举例1：

```java
package com.atguigu.enumeration;

public enum Week {
    MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY,SUNDAY;
}
```

```java
public class TestEnum {
    public static void main(String[] args) {
        Season spring = Season.SPRING;
        System.out.println(spring);
    }
}
```



`enum` 关键字用于定义枚举类型。枚举是一种特殊的类，它用于定义一组常量。枚举类型是固定的，一旦定义就不能被修改，这使得枚举类型非常适合用于表示一组有限的、固定的常量集合，比如一周的天数、月份、方向等。

以下是`enum`关键字的一些基本特性和用法：

1. **定义枚举**：  
使用`enum`关键字来定义一个枚举类型，枚举类型的名称通常以大写字母开头，以区分于类名。

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}
```

2. **枚举成员**：  
枚举类型的每个常量称为枚举成员，它们是枚举类型的实例。
3. **构造函数**：  
枚举可以有自己的构造函数，并且可以传递参数给构造函数。

```java
public enum Day {
    MONDAY(1), TUESDAY(2), WEDNESDAY(3), THURSDAY(4), FRIDAY(5), SATURDAY(6), SUNDAY(7);
    private int dayNumber;
    private Day(int number) {
        this.dayNumber = number;
    }
}
```

4. **方法**：  
枚举可以有自己的方法，包括静态方法和实例方法。

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
    public boolean isWeekday() {
        return this != SATURDAY && this != SUNDAY;
    }
}
```

5. **实现接口**：  
枚举类型可以实现接口。

```java
public interface Color {
    boolean isDark();
}
public enum Day implements Color {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
    public boolean isDark() {
        return this == SATURDAY || this == SUNDAY;
    }
}
```

6. **switch语句**：  
枚举类型非常适合在`switch`语句中使用。

```java
Day d
```



#### 9.3.2 enum方式定义的要求和特点
+ 枚举类的常量对象列表必须在枚举类的首行，因为是常量，所以建议大写。
+ 列出的实例系统会自动添加 public static final 修饰。
+ 如果常量对象列表后面没有其他代码，那么“；”可以省略，否则不可以省略“；”。
+ 编译器给枚举类默认提供的是private的无参构造，如果枚举类需要的是无参构造，就不需要声明，写常量对象列表时也不用加参数
+ 如果枚举类需要的是有参构造，需要手动定义，有参构造的private可以省略，调用有参构造的方法就是在常量对象名后面加(实参列表)就可以。
+ 枚举类默认继承的是java.lang.Enum类，因此不能再继承其他的类型。
+ JDK5.0 之后switch，提供支持枚举类型，case后面可以写枚举常量名，无需添加枚举类作为限定。

举例2：

```java
public enum SeasonEnum {
    SPRING("春天","春风又绿江南岸"),
    SUMMER("夏天","映日荷花别样红"),
    AUTUMN("秋天","秋水共长天一色"),
    WINTER("冬天","窗含西岭千秋雪");

    private final String seasonName;
    private final String seasonDesc;
    
    private SeasonEnum(String seasonName, String seasonDesc) {
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }
    public String getSeasonName() {
        return seasonName;
    }
    public String getSeasonDesc() {
        return seasonDesc;
    }
}

```

举例3：

```java
package com.atguigu.enumeration;

public enum Week {
    MONDAY("星期一"),
    TUESDAY("星期二"),
    WEDNESDAY("星期三"),
    THURSDAY("星期四"),
    FRIDAY("星期五"),
    SATURDAY("星期六"),
    SUNDAY("星期日");

    private final String description;

    private Week(String description){
        this.description = description;
    }

    @Override
    public String toString() {
        return super.toString() +":"+ description;
    }
}
```

```java
package com.atguigu.enumeration;

public class TestWeek {
    public static void main(String[] args) {
        Week week = Week.MONDAY;
        System.out.println(week);

        switch (week){
            case MONDAY:
                System.out.println("怀念周末，困意很浓");break;
            case TUESDAY:
                System.out.println("进入学习状态");break;
            case WEDNESDAY:
                System.out.println("死撑");break;
            case THURSDAY:
                System.out.println("小放松");break;
            case FRIDAY:
                System.out.println("又信心满满");break;
            case SATURDAY:
                System.out.println("开始盼周末，无心学习");break;
            case SUNDAY:
                System.out.println("一觉到下午");break;
        }
    }
}
```

> 经验之谈：
>
> 开发中，当需要定义一组常量时，强烈建议使用枚举类。
>

### 9.4 enum中常用方法
```plain
String toString(): 默认返回的是常量名（对象名），可以继续手动重写该方法！
    
static 枚举类型[] values():返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值，是一个静态方法
    
static 枚举类型 valueOf(String name)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。
    
String name():得到当前枚举常量的名称。建议优先使用toString()。
    
int ordinal():返回当前枚举常量的次序号，默认从0开始

```

举例：

```java
package com.atguigu.enumeration;

import java.util.Scanner;

public class TestEnumMethod {
    public static void main(String[] args) {
        //values()
        Week[] values = Week.values();
        for (int i = 0; i < values.length; i++) {
            //ordinal()、name()
            System.out.println((values[i].ordinal()+1) + "->" + values[i].name());
        }
        System.out.println("------------------------");

        Scanner input = new Scanner(System.in);
        System.out.print("请输入星期值：");
        int weekValue = input.nextInt();
        Week week = values[weekValue-1];
        //toString()
        System.out.println(week);

        System.out.print("请输入星期名：");
        String weekName = input.next();
        //valueOf()
        week = Week.valueOf(weekName);
        System.out.println(week);

        input.close();
    }
}
```

### 9.5 实现接口的枚举类
+ 和普通 Java 类一样，枚举类可以实现一个或多个接口
+ 若每个枚举值在调用实现的接口方法呈现相同的行为方式，则只要统一实现该方法即可。
+ 若需要每个枚举值在调用实现的接口方法呈现出不同的行为方式，则可以让每个枚举值分别来实现该方法

语法：

```java
//1、枚举类可以像普通的类一样，实现接口，并且可以多个，但要求必须实现里面所有的抽象方法！
enum A implements 接口1，接口2{
    //抽象方法的实现
}

//2、如果枚举类的常量可以继续重写抽象方法!
enum A implements 接口1，接口2{
    常量名1(参数){
        //抽象方法的实现或重写
    },
    常量名2(参数){
        //抽象方法的实现或重写
    },
    //...
}
```

举例：

```java
interface Info{
    void show();
}

//使用enum关键字定义枚举类
enum Season1 implements Info{
    //1. 创建枚举类中的对象,声明在enum枚举类的首位
    SPRING("春天","春暖花开"){
        public void show(){
            System.out.println("春天在哪里？");
        }
    },
    SUMMER("夏天","夏日炎炎"){
        public void show(){
            System.out.println("宁静的夏天");
        }
    },
    AUTUMN("秋天","秋高气爽"){
        public void show(){
            System.out.println("秋天是用来分手的季节");
        }
    },
    WINTER("冬天","白雪皑皑"){
        public void show(){
            System.out.println("2002年的第一场雪");
        }
    };
    
    //2. 声明每个对象拥有的属性:private final修饰
    private final String SEASON_NAME;
    private final String SEASON_DESC;
    
    //3. 私有化类的构造器
    private Season1(String seasonName,String seasonDesc){
        this.SEASON_NAME = seasonName;
        this.SEASON_DESC = seasonDesc;
    }
    
    public String getSEASON_NAME() {
        return SEASON_NAME;
    }

    public String getSEASON_DESC() {
        return SEASON_DESC;
    }
}
```



#### 注意
使用 enmu 关键字定义的枚举类，其父类是 java.kang.Enmu 类

使用 enmu 关键字定义的枚举类，不要再显示的定义其父类，否则报错



#### 熟悉 enmu 常用的方法
1. **values()**：返回枚举类型的所有值的数组。这是一个静态方法，可以直接通过枚举类型调用，而不需要实例。

```java
public static E[] values();
```

2. **valueOf(String name)**：返回一个指定名称的枚举常量。这也是一个静态方法，如果找不到匹配的常量，则抛出`IllegalArgumentException`。

```java
public static E valueOf(String name);
```

3. **ordinal()**：返回枚举常量的序号，序号从0开始。这是实例方法。

```java
public final int ordinal();
```

4. **name()**：返回枚举常量的名称。这是实例方法。

```java
public final String name();
```

5. **compareTo(E o)**：比较两个枚举常量的顺序。如果调用对象的序号小于参数的序号，则返回负数；如果相等，则返回0；如果大于，则返回正数。这是实例方法。

```java
public final int compareTo(E o);
```

6. **equals(Object obj)** 和 **hashCode()**：这些方法通常被重写以提供基于枚举常量名称的相等性和哈希码。

```java
@Override
public boolean equals(Object obj);
@Override
public int hashCode();
```

7. **toString()**：返回枚举常量的字符串表示，通常就是它的名称。

```java
@Override
public String toString();
```

8. **clone()**：由于枚举是单例的，所以`clone()`方法总是抛出`CloneNotSupportedException`。

```java
@Override
protected final Object clone() throws CloneNotSupportedException;
```



枚举类接口操作

情况 1： 枚举类实现接口，在枚举类中重写接口中的抽象方法，当通过不同的枚举类对象调用此方法时，执行同一个方法。

情况 2：让枚举类的每一个对象重写接口的抽象方法，当通过不同的枚举类对象调用此方法时，执行的是不同的实现方法



练习

```java
public class ColorTest {
    public static void main(String[] args) {
        Color color = Color.RED;
        System.out.println(color);
    
    }
    
}
enum Color {
    RED(255,0,0,"红色"),
    GREEN(0,255,0,"绿色"),
    BLUE(0,0,255,"蓝色");

    private int redValue;
    private int greenValue;
    private int blueValue;
    private String colorName;

    private Color(int redValue, int greenValue, int blueValue, String colorName) {
        this.redValue = redValue;
        this.greenValue = greenValue;
        this.blueValue = blueValue;
        this.colorName = colorName;
    }
    public String getColorName() {
        return colorName;
    }

    public int getRedValue() {
        return redValue;
    }

    public int getGreenValue() {
        return greenValue;
    }

    public int getBlueValue() {
        return blueValue;
    }

    @Override
    public String toString() {
        return "Color{" +
                "redValue=" + redValue +
                ", greenValue=" + greenValue +
                ", blueValue=" + blueValue +
                ", colorName='" + colorName + '\'' +
                '}';
    }
}
```






