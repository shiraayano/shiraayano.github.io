# 递归
# 面向对象

### 面向对象编程（OOP）笔记

![image (54)](https://github.com/user-attachments/assets/a651492b-5e75-4e2f-ad61-cbcf4dc2cbe8)


#### Java类及类的成员
1. **类的成员**
   - **属性**：定义对象的状态和特征（通常称为类的字段或成员变量）。
   - **方法**：定义对象的行为，用于操作类的属性。
   - **构造器**：初始化对象实例，为属性赋初值。
2. **代码块**
   - **普通代码块**：在方法内部，用于局部范围内逻辑块的处理。
   - **静态代码块**：在类加载时执行，仅执行一次，用于初始化静态资源。
3. **内部类**
   - 定义在另一个类内部的类，可用于封装更为复杂的结构，便于组织逻辑和代码。

#### 面向对象的特征
1. **封装**：隐藏对象的内部实现，仅对外提供访问接口。
2. **继承**：子类继承父类的属性和方法，促进代码复用。
3. **多态**：对象可以表现为多种形态，具体表现由运行时动态决定。

#### 编程范式
- **面向过程编程（POP）**：强调按顺序执行一系列指令来实现功能。
- **面向对象编程（OOP）**：通过对象的属性和方法来封装行为。
- **指令式编程**：按步骤操作数据。
- **函数式编程**：用函数来封装行为，以不可变的数据传递流为核心。

![image (55)](https://github.com/user-attachments/assets/8c8d2e97-bfb3-4f05-94dd-fc7549a2c592)
![image (56)](https://github.com/user-attachments/assets/ea86d0a0-4c78-40c5-94ac-b6c01dfcb1d5)


#### 调用方法
- 对象.属性
- 对象.方法

#### 示例代码

![image (57)](https://github.com/user-attachments/assets/e5a90cb0-35b1-4df2-a698-44c6932d09ed)
![image (58)](https://github.com/user-attachments/assets/122d3852-eceb-47e5-9c12-53907f34ccec)


1. **创建对象并操作属性**

```java
// 创建Phone类的对象p1
Phone p1 = new Phone();
p1.name = "huawei";   // 设置属性
p1.price = 6999;      // 设置属性

// 输出属性
System.out.println("name=" + p1.name);  // 输出 name 属性
```

2. **用户类层次结构**

```java
// 用户类
public class User {
    private String username;  // 用户名
    private String password;  // 密码

    // 构造器，初始化用户名和密码
    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    // Getter 和 Setter 方法
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

    // 通用用户登录方法
    public void login() {
        System.out.println(username + " is logging in.");
    }
}

// 管理员类，继承User类
public class Admin extends User {
    public Admin(String username, String password) {
        super(username, password);
    }

    // 管理员特有方法
    public void manageUsers() {
        System.out.println(getUsername() + " is managing users.");
    }
}

// 超级管理员类，继承Admin类
public class SuperAdmin extends Admin {
    public SuperAdmin(String username, String password) {
        super(username, password);
    }

    // 超级管理员特有方法
    public void grantAdminRights() {
        System.out.println(getUsername() + " is granting admin rights.");
    }
}

// 用户管理类，用于测试创建用户、管理员和超级管理员
public class UserManager {
    public static void main(String[] args) {
        // 创建普通用户
        User regularUser = new User("johnDoe", "password123");
        regularUser.login();

        // 创建管理员
        Admin adminUser = new Admin("janeAdmin", "adminpass");
        adminUser.login();
        adminUser.manageUsers();

        // 创建超级管理员
        SuperAdmin superAdminUser = new SuperAdmin("bobSuper", "superpass");
        superAdminUser.login();
        superAdminUser.manageUsers();
        superAdminUser.grantAdminRights();
    }
}
```
![image (59)](https://github.com/user-attachments/assets/ccf01c78-125c-48f5-b10e-e01faa7f211f)



#### 对象的独立性和引用

1. **独立实体**：每个对象在堆空间中都有一个独立的实体，保存着类属性的副本。更改一个对象的属性不会影响其他对象。
   
   - 示例：
     ```java
     Person p1 = new Person();
     Person p2 = new Person();
     
     p1.age = 18;  // 修改 p1 的 age
     p2.age = 28;  // p2 的 age 独立不受影响
     p1.age = 30;  // 修改 p1 的 age 后，p2 的 age 仍为 28
     ```

2. **引用变量共享**：如果两个变量指向同一个对象，修改其中一个的属性会影响另一个。

   - 示例：
     ```java
     Person p1 = new Person();
     Person p3 = p1;  // p3 引用 p1 的对象
     
     p3.age = 25;     // 修改 p3 的 age
     System.out.println(p1.age);  // 访问 p1 的 age，值为 25
     ```

这些内容包含了Java面向对象编程的基本要点和细节，代码示例提供了清晰的参考。

---


### Java 面向对象笔记（详细版）

---

#### 成员变量与局部变量

1. **成员变量（Field）**
   - **定义**：在类中定义，但不在任何方法、构造方法或代码块中的变量。
   - **特点**：
     1. **作用域**：整个类内可见，类的所有方法均可访问。
     2. **生命周期**：与对象绑定，对象创建时初始化，随对象销毁而销毁。
     3. **初始化**：未显式赋值时，自动初始化为默认值（例如 `int` 默认值为 `0`，对象引用默认值为 `null`）。
     4. **访问控制**：可以使用 `public`、`private`、`protected` 等访问修饰符来控制可见性。
   - **示例**：

     ```java
     public class Person {
         private String name; // 成员变量
         private int age;     // 成员变量

         public Person(String name, int age) {
             this.name = name; // 初始化成员变量
             this.age = age;
         }

         public void displayInfo() {
             System.out.println("Name: " + name + ", Age: " + age);
         }
     }
     ```

2. **局部变量（Local Variable）**
   - **定义**：在方法、构造方法或代码块中声明的变量。
   - **特点**：
     1. **作用域**：仅在定义它的块内可见，块结束后超出作用域。
     2. **生命周期**：随方法执行过程创建和销毁。
     3. **初始化**：必须显式初始化，否则会导致编译错误。
     4. **访问控制**：不能使用访问修饰符，因为它们仅在当前块内可见。
   - **示例**：

     ```java
     public class Calculator {
         public int add(int a, int b) {
             int sum = a + b; // 局部变量
             return sum;
         }
     }
     ```

#### 内部类与外部类实例化

1. **内部类**：将一个类定义在另一个类的内部，内部类可以访问外部类的所有成员（包括私有成员）。

   - **示例**：

     ```java
     public class OuterClass {
         private String outerField = "Outer field";

         public class InnerClass {
             public void display() {
                 System.out.println("Accessing outer field: " + outerField);
             }
         }

         public InnerClass getInnerClassInstance() {
             return new InnerClass();
         }
     }

     public class TestInnerClass {
         public static void main(String[] args) {
             OuterClass outer = new OuterClass();
             OuterClass.InnerClass inner = outer.getInnerClassInstance();
             inner.display();
         }
     }
     ```

2. **外部类实例化**：在一个类中创建另一个类的实例，通过实例访问方法和属性。

   - **示例**：

     ```java
     public class Car {
         private String brand = "Toyota";
         
         public void startEngine() {
             System.out.println(brand + " engine started");
         }
     }

     public class Garage {
         Car myCar;

         public Garage() {
             myCar = new Car(); // 创建 Car 实例
         }

         public void startCarEngine() {
             myCar.startEngine(); // 调用 Car 实例的方法
         }
     }

     public class TestGarage {
         public static void main(String[] args) {
             Garage garage = new Garage();
             garage.startCarEngine();
         }
     }
     ```

#### 方法（Method）

- **方法的定义**：

  ```java
  [访问修饰符] [static] 返回类型 方法名(参数类型 参数名, ...) {
      // 方法体
      return 返回值; // 如果有返回值
  }
  ```

  - **访问修饰符**：定义方法可见性，如 `public`、`private`、`protected`。
  - **static**：用于静态方法，直接通过类名调用，无需实例化。
  - **返回类型**：方法返回的数据类型。若无返回值，用 `void`。
  - **方法名**：符合命名规范，表示方法功能。
  - **参数**：方法输入的数据。
  - **方法体**：方法的执行内容。

- **方法的调用**：

  ```java
  public class Calculator {

      // 无返回值的方法
      public void displayMessage() {
          System.out.println("Hello, World!");
      }

      // 有参数有返回值的方法
      public int add(int num1, int num2) {
          int sum = num1 + num2;
          return sum; // 返回结果
      }

      public static void main(String[] args) {
          Calculator calc = new Calculator(); // 创建实例

          // 调用无返回值方法
          calc.displayMessage();

          // 调用有返回值方法
          int result = calc.add(5, 10);
          System.out.println("The sum is: " + result);
      }
  }
  ```

- **注意事项**：
  1. 静态方法可通过类名直接调用，如 `ClassName.methodName()`。
  2. 非静态方法需在类实例上调用。
  3. 方法参数必须与定义时参数类型和顺序一致。
  4. `return` 结束方法，并将值返回给调用者，`return` 后不可再有代码。



- **方法的分类**：
  - **无返回值类型**：`void` 类型，无需返回值。
  - **有返回值类型**：需要使用 `return` 语句返回与定义类型匹配的数据。

#### 示例代码

1. **成员变量与局部变量的比较**

   ```java
   public class Example {

       // 成员变量，生命周期与对象一致
       private String name;

       public void methodExample() {
           // 局部变量，生命周期仅在当前方法内
           int number = 10;
           System.out.println("Local variable number: " + number);
       }
   }
   ```

2. **使用方法与参数**

   ```java
   public class Person {

       public void sleep(int hours) {
           System.out.println("人每天至少睡：" + hours + "小时");
       }
   }
   ```

   - **说明**：方法定义时根据功能决定参数类型；参数列表为空时表示无输入要求。


![image (60)](https://github.com/user-attachments/assets/9e7c9b33-2e75-4378-a986-52b51c0bac67)



### 方法的定义与调用

在 Java 中，方法是实现功能模块的基本单元。一个方法可以包含逻辑代码、接收参数并返回数据。方法的定义结构包括访问修饰符、可选的 `static` 关键字、返回值类型、方法名和参数列表。

#### 方法的定义结构

```java
[访问修饰符] [static] 返回类型 方法名(参数类型 参数名, 参数类型 参数名, ...) {
    // 方法体
    // ...
    // 返回语句（如果方法有返回值）
    return 返回值;
}
```

**要点：**
- **访问修饰符**：如 `public`、`private`、`protected`，控制方法的访问权限。
- **static**：若方法为静态，则使用类名直接调用，不需要创建实例。
- **返回类型**：指定方法返回的数据类型，若没有返回值，使用 `void`。
- **方法名**：方法的标识符，遵循 Java 命名规范。
- **参数**：方法的输入，可以在调用时传递数据。

#### 方法的调用

调用方法时使用方法名，并传入相应的参数（如果有）。方法的返回值可以用于后续操作。

**示例：**

```java
public class Calculator {

    // 无参数、无返回值的方法
    public void displayMessage() {
        System.out.println("Hello, World!");
    }

    // 有参数、有返回值的方法
    public int add(int num1, int num2) {
        int sum = num1 + num2;
        return sum; // 返回计算结果
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator(); // 创建 Calculator 类的实例

        // 调用无参数、无返回值的方法
        calc.displayMessage();

        // 调用有参数、有返回值的方法，并打印结果
        int result = calc.add(5, 10);
        System.out.println("The sum is: " + result);
    }
}
```

在这个例子中，`Calculator` 类包含两个方法：`displayMessage` 和 `add`。`displayMessage` 没有参数，也没有返回值，它仅打印消息。`add` 方法接受两个整数参数，返回它们的和。

#### 注意事项

- **静态方法**：可通过类名直接调用，如 `Calculator.displayMessage()`。
- **非静态方法**：必须在实例上调用，如 `calc.displayMessage()`。
- **参数匹配**：传入的参数必须与方法定义的参数类型和顺序相匹配。
- **调用限制**：方法可以调用同一类中的其他方法，包括自己。

### 方法声明

![image (60)](https://github.com/user-attachments/assets/8afa91f3-d9f5-4c9b-9f43-495979185092)


```java
权限修饰符 [其它修饰符（非必要）] 返回值类型 方法名（形参列表）{
    // 方法体
}
```

#### 方法分类

1. **无返回值类型**：若方法没有返回值，使用 `void`，如 `public void displayMessage()`。
2. **有返回值类型**：返回具体的数据类型，如 `int`、`String` 等，并必须包含 `return` 语句。

#### 形参列表的使用

当方法需要外部数据时，形参列表可指定接收的参数：

```java
public void sleep(int hour) {
    System.out.println("人每天最少睡：" + hour + " 小时");
}
```

#### 注意 `return` 语句

- `return` 用于结束方法并返回值。
- `return` 后不能有任何可执行语句，否则编译错误。



### Java 递归方法

**递归**指的是方法在自身内部调用自己。递归是一种强大的编程技术，通常用于解决具有重复子结构的问题，比如分治法、树结构处理和数学计算等场景。

#### 递归方法的分类

1. **直接递归**：方法直接调用自己。
2. **间接递归**：方法通过其他方法间接调用自身。例如，`A()` 调用 `B()`，然后 `B()` 再调用 `A()`。

#### 递归的特性

- **隐式循环**：递归方法通过方法调用栈来实现循环，因此可以被认为包含一种隐式的循环。
- **递归终止条件**：递归方法一定要在已知的方向上递归，即每次递归调用要朝着满足条件的方向收敛。否则会出现**无限递归**，最终导致栈内存溢出（StackOverflowError）。
  
#### 递归示例

以下是一个简单的递归示例：**计算阶乘**。

**阶乘的定义**：  
- n! = n × (n - 1) × (n - 2) × ... × 1  
- 特殊情况：0! = 1

**代码实现：**

```java
public class Factorial {
    // 递归计算阶乘的方法
    public static int factorial(int n) {
        // 递归终止条件：当 n 为 0 时返回 1
        if (n == 0) {
            return 1;
        }
        // 递归调用：计算 n * (n-1)!
        return n * factorial(n - 1);
    }

    public static void main(String[] args) {
        int number = 5;
        int result = factorial(number);
        System.out.println(number + "! = " + result);  // 输出结果
    }
}
```

**代码说明**：
- `factorial` 方法在每次调用时都会检查是否满足终止条件 `n == 0`。
- 如果满足条件则返回 1，否则继续调用 `factorial(n - 1)` 计算 `(n - 1)!`。
- 最终每层递归都会返回计算值，直至整个阶乘计算完成。

#### 注意事项

1. **确保递归终止条件**：递归方法必须有明确的终止条件，否则会导致无限递归。
2. **优化递归**：递归效率较低，尤其是在需要重复计算的情况下（如斐波那契数列）。这时可以考虑使用**动态规划**等优化方式。

---

递归的概念和用法主要总结如上，适用于解决许多复杂问题。


这个代码定义了多个递归和非递归方法，来展示递归的应用。代码有一些需要修改和完善的地方，我已为你整理并补充了注释。

---

### 递归示例代码

```java
// 文件名: RecursionTest.java
public class RecursionTest {
    public static void main(String[] args) {
        // 创建当前类的对象，用于调用实例方法
        RecursionTest rt = new RecursionTest();

        // 调用求和方法（非递归）
        rt.method2();

        // 调用递归求和方法
        System.out.println("1到100的总和：" + rt.method3(100));

        // 调用递归计算阶乘方法
        System.out.println("5的阶乘：" + rt.method4(5));

        // 调用斐波那契数列计算方法
        System.out.println("斐波那契数列第10项：" + rt.method5(10));
    }

    // 递归方法示例：无限递归
    public void method1() {
        System.out.println("method1。。。");
        // 自己调用自己，会导致无限递归
        method1();
    }

    // 非递归求和方法：计算1到100之间的总和
    public void method2() {
        int sum = 0;
        for (int i = 1; i <= 100; i++) {
            sum += i;
        }
        System.out.println("1到100的总和：" + sum);
    }

    // 递归求和方法：计算1到num的总和
    public int method3(int num) {
        if (num == 1) {
            return 1;
        } else {
            return num + method3(num - 1);
        }
    }

    // 递归计算阶乘：计算n的阶乘 n!
    public int method4(int n) {
        if (n == 1) {
            return 1;
        } else {
            return n * method4(n - 1);
        }
    }

    // 递归计算斐波那契数列：f(n) = f(n-1) + f(n-2)
    public int method5(int n) {
        if (n == 1 || n == 2) {
            return 1;
        } else {
            return method5(n - 1) + method5(n - 2);
        }
    }
}
```

```java
// 文件名: RecursionExer.java
public class RecursionExer {
    public static void main(String[] args) {
        RecursionExer exer = new RecursionExer();

        // 测试自定义递归方法 f 和 func
        System.out.println("f(20)的值：" + exer.f(20));
        System.out.println("func(20)的值：" + exer.func(20));
    }

    // 递归方法：根据自定义规则定义的递归公式
    public int f(int n) {
        if (n == 20) {
            return 1;
        } else if (n == 21) {
            return 4;
        } else {
            return f(n + 1) + f(n + 2);
        }
    }

    // 递归方法：另一个自定义的递归公式
    public int func(int n) {
        if (n == 0) {
            return 1;
        } else if (n == 1) {
            return 4;
        } else {
            return 2 * func(n - 1) + 2 * func(n - 2);
        }
    }
}
```

### 代码说明

1. **method1**：无限递归调用自己，无终止条件，会导致**栈溢出错误**（StackOverflowError）。
2. **method2**：非递归方法，用于计算 1 到 100 的总和。
3. **method3**：递归求和方法，计算从 1 到 `num` 的总和。终止条件为 `num == 1`。
4. **method4**：递归阶乘方法，计算 `n!`。终止条件为 `n == 1`。
5. **method5**：递归实现的斐波那契数列，终止条件为 `n == 1` 或 `n == 2`。
6. **f** 和 **func**：两个自定义递归方法，依次计算指定规则的递归序列。

### 注意事项

- 递归方法中务必设置**递归终止条件**，防止无限递归。
- 对于计算量大的递归问题，可以考虑使用**缓存**或**动态规划**来提高效率，如斐波那契数列等。


# 
# 关键字
关键字 package 包 import



package ，成为包， 用于指明文件中定义的类 。接口等结构所在的包

package 顶层包名.子包名;

语法 package pack1.pack2;

在Java中，`import static`语句允许你导入一个类或接口中的静态成员（包括方法和变量），这样你就可以直接通过成员名来访问它们，而不需要每次都指定类名。这可以使代码更加简洁，尤其是在使用频繁调用的静态方法时。

以下是`import static`的一些使用场景：

1. **导入单个静态成员**：

```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;

public class Test {
    public static void main(String[] args) {
        double area = sqrt(4) * PI; // 使用导入的静态成员
    }
}
```

2. **导入多个静态成员**：

```java
import static java.lang.Math.{PI, sqrt};

public class Test {
    public static void main(String[] args) {
        double area = sqrt(4) * PI; // 使用导入的静态成员
    }
}
```

3. **导入整个类的静态成员**：

```java
import static java.lang.Math.*;

public class Test {
    public static void main(String[] args) {
        double area = sqrt(4) * PI; // 使用导入的静态成员
    }
}
```

使用`import static`时需要注意的几点：

+ 它只能用于导入静态成员。
+ 如果多个类有相同名称的静态成员，你需要指定使用哪一个。
+ 过度使用`import static`可能会导致代码的可读性降低，因为读者需要知道被导入的静态成员来自哪个类。

使用`import static`可以提高代码的可读性和简洁性，但应该适度使用，以保持代码的清晰和易于维护。



import 导入

import 语句来显示引入指定包下的类，相当于 import 语句告诉编译器去哪里找到这个类

import 包名.类名;

写在包的声明和类的声明之间

可以使用.*一键导入包中所有的类中和所有接口

如果导入的类或接口 是 java.lang 包下的，或是当前包下的则可以省略 import 语句

如果在包下出现不同包下同名的类，那么就需要使用类的全类名方式指明调用的是哪个类（java.sql.Date data1= new java.sql.Date(12121212121L);）

（了解）import static 组合的使用 调用指定类或接口下的静态的属性或方法









Java中的`package`是一个关键词，用于声明类属于哪个包（package）。包是Java中组织类和接口的一种方式，它有助于避免命名冲突，并允许开发者将功能相关的类组织在一起。下面是关于Java包的一些基本介绍和使用规范：

### 1. 定义包
在Java文件的最开始，可以使用`package`关键词来声明该文件属于哪个包。例如：

```java
package com.example.myapp;
```

这行代码声明了该Java文件属于`com.example.myapp`包。

### 2. 使用包
+ **导入类**：如果你要使用其他包中的类，可以使用`import`语句。例如：

```java
import com.example.myapp.MyClass;
```

或者使用`import`语句的通配符形式：

```java
import com.example.myapp.*;
```

这将导入`com.example.myapp`包下的所有类。

### 3. 包的使用规范
+ **避免命名冲突**：包名通常采用全小写字母，使用点`.`分隔不同级别的组织结构，如域名的逆序。例如，`com.example.myapp`。
+ **组织结构**：包通常按照功能或模块来组织。例如，一个大型项目可能包含多个子项目，每个子项目都有自己的包。
+ **访问控制**：Java的访问修饰符（public, protected, default, private）与包的使用密切相关。默认访问权限（没有指定访问修饰符）的类或成员只能在同一个包内被访问。
+ **避免过度使用**：虽然包可以帮助组织代码，但过度使用包会使项目结构变得复杂难懂。合理地划分包的粒度很重要。
+ **遵循Java平台模块系统**：从Java 9开始，Java引入了模块系统（JPMS），它允许更细粒度的控制包的可见性和依赖关系。使用模块可以提高代码的封装性和安全性。

### 4. 包与目录结构
在文件系统中，包对应于目录结构。例如，`com.example.myapp`包对应的目录结构可能是：

```plain
src/
└── com/
    └── example/
        └── myapp/
```

每个包名的组成部分对应于目录结构中的一个目录。

### 5. 包的声明顺序
在Java文件中，`package`声明必须是文件的第一行非注释代码，它不能与其他语句或声明一起使用。

通过合理使用包，可以提高Java项目的可维护性和可读性。

是的，Java中包名的一种常见约定是使用公司或组织的域名的倒置形式。这种约定有助于确保包名的唯一性，因为域名是唯一的，并且可以避免不同组织之间的命名冲突。下面是一些关于使用域名倒置作为包名的要点：

1. **域名倒置**：将域名的各个部分倒置，并将它们用点`.`分隔。例如，如果域名是`example.com`，则包名可以是`com.example`。
2. **添加项目或模块名称**：在域名倒置的基础上，可以添加项目或模块的名称，以进一步组织代码。例如，如果项目名称是`myapp`，则完整的包名可能是`com.example.myapp`。
3. **避免使用顶级域名**：在倒置的域名后面，通常会添加至少一个额外的名称，以避免直接使用顶级域名（如`com`、`org`等）作为包名的顶级元素。
4. **保持简洁**：虽然使用域名倒置可以确保唯一性，但包名应该尽可能简洁，以便于理解和使用。
5. **遵循Java命名约定**：Java的命名约定建议使用全小写字母，并且单词之间用驼峰命名法连接。这些约定同样适用于包名。

使用域名倒置作为包名是一种广泛接受的最佳实践，它有助于确保包名的唯一性，并提供一个清晰的组织结构。这种命名方式在Java社区中非常流行，也被许多其他编程语言和框架所采用。



包名不要以 java 开头（安全问题）



 用域名命名规范主要是便于区分不同组织



在计算机编程和软件开发中，“包”（Package）这个概念扮演着重要的角色，它的作用可以从多个角度来理解：

### 1. 组织和管理代码
+ **逻辑分组**：包允许开发者将功能相关的类和接口组织在一起，形成逻辑上的分组，这有助于代码的模块化和清晰性。
+ **层次结构**：包提供了一种层次结构，允许开发者按照功能模块或业务逻辑创建嵌套的包结构。

### 2. 避免命名冲突
+ **命名空间**：在大型项目或多团队协作中，不同的开发者可能会定义相同名称的类或方法。通过使用包，可以为每个类创建一个唯一的命名空间，从而避免命名冲突。

### 3. 控制访问权限
+ **封装性**：包可以包含具有不同访问权限的类和成员（如public、protected、private）。这有助于控制不同包之间的访问级别，增强代码的封装性。
+ **默认访问权限**：在Java中，没有指定访问修饰符的类或成员默认只能在同一个包内被访问，这有助于保护内部实现细节。

### 4. 提高代码的可维护性
+ **模块化**：通过将功能相关的代码组织在同一个包中，可以提高代码的可维护性。当需要修改或更新某个功能时，只需要关注相应的包。
+ **重用性**：包内的类和接口可以被其他包重用，这有助于减少代码的重复，并提高代码的重用性。

### 5. 便于部署和分发
+ **依赖管理**：在现代软件开发中，包管理系统（如Maven、NPM）使用包的概念来管理项目的依赖关系，这使得依赖的安装、更新和版本控制变得更加容易。
+ **分发单元**：包可以作为代码分发的基本单元，使得开发者可以轻松地共享和部署代码。

### 6. 支持多视图和国际化
+ **本地化**：在支持多语言的应用程序中，包可以用来组织不同语言的资源文件，如字符串、图像等，以支持国际化和本地化。

### 7. 遵循标准和约定
+ **行业标准**：在许多编程语言中，包的使用遵循特定的行业标准和约定，如Java中的包名通常采用域名倒置的格式。

总的来说，包是软件开发中用于组织代码、控制访问权限、提高代码重用性和可维护性的重要工具。通过合理使用包，开发者可以构建更加清晰、模块化和易于维护的软件系统。



Java Development Kit (JDK) 提供了许多内置的包（package），这些包包含了大量的类和接口，用于支持各种编程任务。以下是一些JDK中非常重要的包：

1. **java.lang**：
    - 包含Java语言的核心类，如`Object`、`String`、`Math`、`System`、`Thread`等。这些类是Java程序的基石，每个Java程序都会隐式地使用这个包。
2. **java.util**：
    - 提供了一系列实用工具类，包括集合框架（`List`、`Set`、`Map`等）、日期和时间API（`Date`、`Calendar`）、并发工具类（`ThreadLocal`、`Executor`等）。
3. **java.io**：
    - 包含输入/输出相关的类，用于处理文件、网络和管道通信。核心类包括`File`、`InputStream`、`OutputStream`、`Reader`、`Writer`等。
4. **java.net**：
    - 提供了网络编程所需的类，如`URL`、`URLConnection`、`Socket`、`ServerSocket`等。
5. **java.nio**（New Input/Output）：
    - 从Java 1.4开始引入，提供了一种更高效的I/O操作方式，支持文件锁定、内存映射文件等。核心类包括`ByteBuffer`、`FileChannel`、`Selector`等。
6. **java.sql**：
    - 提供了数据库编程所需的类和接口，如`Connection`、`Statement`、`ResultSet`等，用于执行SQL语句和处理数据库查询结果。
7. **javax.swing**：
    - 用于构建图形用户界面（GUI），包含`JFrame`、`JPanel`、`JButton`等组件。
8. **java.awt**：
    - 包含用于创建图形用户界面的基本组件，如`Frame`、`Panel`、`Button`等，以及处理图形和图像的类。
9. **java.beans**：
    - 提供了与JavaBean相关的类和接口，JavaBean是一种特殊的Java类，遵循特定的命名约定，用于开发可重用的组件。
10. **java.text**：
    - 包含用于格式化、解析和处理文本的类，如`DateFormat`、`NumberFormat`等。
11. **java.security**：
    - 提供了安全和加密相关的类和接口，如`Key`、`Certificate`、`MessageDigest`等。
12. **java.lang.reflect**：
    - 提供了Java反射API，允许程序在运行时访问、检查和修改类的行为。
13. **java.time**（Java 8引入）：
    - 替代了`java.util.Date`和`java.util.Calendar`，提供了更加强大和灵活的日期和时间API，如`LocalDate`、`LocalTime`、`ZonedDateTime`等。
14. **javafx**（JavaFX SDK）：
    - 用于构建富客户端应用程序的现代GUI工具包，提供了`Stage`、`Scene`、`Pane`等组件。

这些包是JDK中非常核心的部分，涵盖了基础功能、I/O操作、网络编程、数据库访问、GUI构建等多个方面。了解和掌握这些包对于Java开发者来说非常重要。



MVC（Model-View-Controller）设计模式是一种用于软件设计，特别是用户界面设计中常用的设计模式。它将应用程序分为三个核心组件：模型（Model）、视图（View）和控制器（Controller），以实现关注点分离，提高代码的可维护性和可扩展性。下面是这三个组件的简要介绍：

1. **模型（Model）**：
    - **定义**：模型代表应用程序的数据结构和业务逻辑。它是应用程序的主体，负责管理数据、执行业务规则和逻辑。
    - **职责**：包括数据的存储、检索、验证、计算等。模型通常不包含任何界面元素，只负责数据的处理。
    - **交互**：模型可以通知视图关于数据的变化，以便视图可以更新显示。
2. **视图（View）**：
    - **定义**：视图是用户界面组件，负责显示数据（即模型）并收集用户的输入。
    - **职责**：展示模型中的数据，提供用户界面元素（如文本框、按钮、列表等），并处理用户的交互（如点击、输入等）。
    - **交互**：视图从模型接收数据，并在用户进行操作时，通过控制器更新模型。
3. **控制器（Controller）**：
    - **定义**：控制器是应用程序的中介者，它接收用户的输入并调用模型和视图去完成用户的需求。
    - **职责**：处理用户的输入，将输入转换为模型的数据操作，更新模型的状态，并选择合适的视图来显示模型的数据。
    - **交互**：控制器接收来自视图的用户输入，调用模型进行处理，然后根据模型的状态更新视图。

MVC设计模式的主要优点包括：

+ **关注点分离**：将数据处理、用户界面和用户输入处理分开，使得各个部分可以独立开发和维护。
+ **提高代码的可维护性**：由于关注点分离，修改一个组件不会影响其他组件，降低了维护的复杂性。
+ **提高可扩展性**：新的功能可以更容易地添加到模型、视图或控制器中，而不需要重写整个应用程序。
+ **多视图支持**：同一个模型可以支持多个视图，这意味着你可以为不同的用户界面或设备提供不同的视图，而不需要改变模型本身。

MVC模式也有其局限性，例如可能导致过多的控制器代码，以及在大型应用程序中可能导致组件之间的复杂交互。为了解决这些问题，衍生出了MVC的变体，如MVP（Model-View-Presenter）和MVVM（Model-View-ViewModel），它们在某些方面对MVC进行了改进。





在Java中，`import`语句用于导入其他包中的类或整个包，以便在当前文件中使用这些类而不需要完全限定类名。这有助于简化代码，使其更加清晰和易于维护。以下是`import`语句的一些使用方式：

### 导入单个类
如果你只需要使用某个包中的一个或几个类，可以单独导入这些类：

```java
import java.util.List;
import java.util.Map;
```

这样，你就可以在代码中直接使用`List`和`Map`，而不需要每次都写`java.util.List`。

### 导入整个包
如果你需要使用某个包中的多个类，可以导入整个包：

```java
import java.util.*;
```

这将导入`java.util`包中的所有类，但请注意，这种做法可能会导致命名冲突，并且不推荐在大型项目中使用，因为它降低了代码的清晰度。

### 静态导入
Java 5引入了静态导入，允许导入静态方法和静态字段，使得调用这些成员时不需要指定类名：

```java
import static java.lang.Math.PI;
import static java.lang.Math.sqrt;
```

之后，你可以直接使用`PI`和`sqrt`，而不需要`Math.PI`和`Math.sqrt`。

### 导入规则和最佳实践
1. **避免导入整个包**：虽然导入整个包可以减少代码量，但它可能会导致命名冲突，并使代码难以阅读。推荐按需导入单个类。
2. **保持一致性**：在项目中保持一致的导入风格，比如是否使用`*`来导入整个包。
3. **避免不必要的导入**：只导入实际使用的类，避免导入未使用的类，以减少混乱和潜在的命名冲突。
4. **静态导入的使用**：静态导入适用于频繁使用的静态方法和字段，但也要谨慎使用，以免代码过于依赖静态成员，影响代码的可测试性和模块化。
5. **导入顺序**：通常建议按照以下顺序排列`import`语句：
    - Java核心库类（如`java.*`）
    - Java扩展库类（如`javax.*`）
    - 第三方库类
    - 项目自己的类（按字母顺序）
6. **IDE支持**：现代IDE（如IntelliJ IDEA、Eclipse）通常提供自动导入功能，可以自动管理`import`语句，减少手动操作。

正确使用`import`语句可以提高代码的可读性和可维护性，是Java编程中的一个重要方面。







封装性

封装（Encapsulation）是Java面向对象编程（OOP）的三大特性之一，其他两个是继承（Inheritance）和多态（Polymorphism）。封装的核心思想是将对象的属性和实现细节隐藏起来，只对外提供必要的接口。这种做法不仅提高了代码的安全性和可维护性，还能减少耦合，使代码更易于理解和修改。

### 封装的概念
封装是指将对象的属性和方法隐藏在其内部，只对外提供必要的访问方式。通过这种方式，可以保护对象的内部状态，防止外部程序直接访问和修改对象的内部数据。

### 封装的优点
1. **减少耦合**：良好的封装能够减少类与类之间的耦合度，使得代码更加模块化。
2. **隐藏实现细节**：通过隐藏类的内部实现细节，只暴露必要的接口，可以防止外部直接访问和修改对象的状态。
3. **提高代码的可维护性**：封装使得代码更容易理解和维护，修改类的内部实现不会影响到外部代码。
4. **控制访问**：可以通过访问修饰符（如private、protected、public）来控制对类成员的访问权限，从而提高数据的安全性。

### 实现封装的步骤
1. **将属性设置为私有**：通过将类的属性声明为私有（private），限制外部对这些属性的直接访问。
2. **提供公共的访问方法**：通过提供公共的getter和setter方法，允许外部程序访问和修改私有属性。

### 示例代码
以下是一个简单的Java封装示例：

```java
public class Person {
    // 私有属性
    private String name;
    private int age;

    // 公共的getter方法
    public String getName() {
        return name;
    }

    // 公共的setter方法
    public void setName(String name) {
        this.name = name;
    }

    // 公共的getter方法
    public int getAge() {
        return age;
    }

    // 公共的setter方法
    public void setAge(int age) {
        if (age >= 0) {
            this.age = age;
        } else {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }
}

public class TestPerson {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("Alice");
        person.setAge(25);

        System.out.println("Name: " + person.getName());
        System.out.println("Age: " + person.getAge());
    }
}
```

### 详细解释
1. **私有属性**：在`Person`类中，`name`和`age`属性被声明为私有，这意味着它们只能在类的内部被访问和修改。
2. **公共方法**：通过提供公共的getter和setter方法，外部程序可以访问和修改私有属性。例如，`getName`和`setName`方法允许外部程序访问和修改`name`属性。
3. **数据验证**：在setter方法中，可以添加数据验证逻辑。例如，在`setAge`方法中，添加了一个检查，确保年龄不能为负数。

### 封装的实际应用
1. **数据验证**：在setter方法中，可以对输入的数据进行验证，以确保其符合预期的格式或范围。
2. **懒加载**：在getter方法中，可以实现懒加载策略，即只在第一次需要访问某个属性时才加载该属性的值。
3. **日志记录**：在getter和setter方法中，可以添加日志记录功能，以记录对对象内部状态的访问和修改操作。

### 总结
封装是Java面向对象编程的重要特性之一，通过将对象的属性和方法隐藏在其内部，并提供必要的访问方式，封装不仅提高了程序的安全性、可维护性和可重用性，还能实现数据验证、懒加载和日志记录等高级功能。因此，在Java编程中，应充分利用封装的优势来设计和实现高质量的代码。



#### 权限修饰符


Java中提供了四种访问权限修饰符，它们可以修饰类、接口中的成员（字段和方法）：

1. **private**：私有权限，被private修饰的成员变量或方法，只能在定义它们的类内部访问，不能被外部访问。
2. **default**（默认）：没有指定访问修饰符，称为默认访问权限。类成员如果采用默认访问权限，则只能被同一个包中的其他类访问。
3. **protected**：受保护的权限，被protected修饰的成员变量或方法可以被同一个包中的其他类访问，也可以被不同包中的子类访问。
4. **public**：公共权限，被public修饰的成员变量或方法可以被任何其他类访问，没有任何访问限制。

以下是权限修饰符的访问级别对比表：

| 类型 | private | default | protected | public |
| --- | --- | --- | --- | --- |
| 同一类 | √ | √ | √ | √ |
| 同一包 | ✗ | √ | √ | √ |
| 不同包，子类 | ✗ | ✗ | √ | √ |
| 不同包，非子类 | ✗ | ✗ | ✗ | √ |


### 权限修饰符的使用规则：
+ **类和接口**：不能被声明为private或protected，但可以声明为public或默认。
+ **成员变量**：可以被声明为private、default、protected或public。
+ **方法**：可以被声明为private、default、protected或public。
+ **构造方法**：可以被声明为private、default、protected或public。
+ **内部类**：可以被声明为private、default、protected或public。

### 权限修饰符的作用：
+ **private**：用于隐藏类的内部信息，确保外部代码不能直接访问对象的内部状态，只能通过公共的接口（getter/setter）进行交互。
+ **default**：用于控制类成员在同一个包内可见，有助于包的封装性，避免过度暴露类的内部实现。
+ **protected**：用于允许类的子类访问其成员，即使子类在不同的包中也能访问。
+ **public**：用于提供类的外部接口，使类成员可以被任何其他类访问。

权限修饰符是Java语言中实现封装和控制访问级别的重要工具，合理使用权限修饰符可以提高代码的安全性和可维护性。



代码示例

```java
/**
 * Test
 */
public class Test {

    public static void main(String[] args) {
        // 创建Animal对象并设置属性
        Animal animl1 = new Animal();
        animl1.name = "金蟾";
        animl1.setLeg(4); // 调用setLeg方法设置腿的数量

        // 打印动物的名字和腿的数量
        System.out.println("动物名称:" + animl1.name + " 动物腿数:" + animl1.getLeg());

        // 访问修饰符
        // public: 公共的，任何类都可以访问
        // private: 私有的，只有本类可以访问
        // protected: 受保护的，本类、同包类、子类可以访问
        // 默认（不写）：本类、同包类可以访问

        // 其他修饰符
        // static: 静态的，类变量、类方法
        // final: 最终的，常量、类、方法、变量
        // abstract: 抽象的，抽象类、抽象方法
        // transient: 瞬态的，不会被序列化的变量
        // volatile: 易变的，多线程操作共享变量
        // synchronized: 同步的，多线程操作共享变量
        // native: 本地的，调用本地方法
        // strictfp: 精确浮点，浮点运算更加精确
        // default: 默认的，接口方法
    }
}

class Animal {
    String name; // 名字
    int age;     // 年龄
    String color;// 颜色
    private int leg; // 腿的数量

    // 设置腿的数量
    public void setLeg(int l) {
        if (l >= 0 && l % 2 == 0) {
            leg = l;
        } else {
            System.out.println("请输入正确的腿数");
        }
    }

    // 获取腿的数量
    public int getLeg() {
        return leg;
    }

    // 动物觅食的方法
    public void eat() {
        System.out.println("动物觅食");
    }
}
```



如何体现封装性？

java 规定了四种访问权限修饰符，分别是 private ，缺省 ，protected ，public

我们可以用这四种权限去修饰类及类的成员，当这些成员被调用时体现可见性的大小



（类只能使用 public 和 缺省 修饰 类的内部成员可以使用四种修饰符）



使用频率

高 public private

低 缺省 protected





封装性的体现

场景1,私有化（pr1vate)类的属性，提供公共（public)的get和set方法，对此属性进行获取或修改

场景2:将类中不需要对外暴露的方法，设置为pr1vate

场景3,单例模式中构造器private的了，避免在类的外部创建实例。(放到static关键字后讲）





封装性的体现主要在于将对象的状态（属性）和行为（方法）捆绑在一起，并对对象的内部实现细节进行隐藏，仅通过有限的接口与外界通信。以下是封装性的几个具体体现和应用场景：

### 封装性的体现：
1. **隐藏内部实现细节**：
    - 通过将类的成员变量设置为私有（`private`），不允许外部直接访问。
    - 仅通过公共的访问方法（`public` getter/setter）来提供对属性的访问和修改。
2. **提供公共接口**：
    - 提供公共的方法（`public`）来允许外部代码以受控的方式访问和修改私有属性。
    - 通过这些公共接口，可以在修改内部实现时不影响外部代码。
3. **数据校验**：
    - 在setter方法中添加逻辑来校验赋给属性的值，确保数据的有效性和合理性。
4. **数据封装**：
    - 将相关属性和处理这些属性的方法封装在一起，构成一个独立的实体。
5. **实现细节的变化不影响外部**：
    - 可以在不影响使用该类的代码的情况下修改类的内部实现。
6. **提高代码的可读性和可维护性**：
    - 将属性和方法组织在同一个类中，使得代码结构更清晰，易于理解和维护。

### 应用场景：
1. **数据校验**：
    - 在用户注册时，通过封装确保用户提供的邮箱、密码等信息符合特定的格式和安全要求。
2. **对象状态管理**：
    - 在游戏中，通过封装管理角色的状态，如生命值、能量等，并通过方法来修改这些状态，而不是直接暴露这些属性。
3. **设备控制**：
    - 在硬件操作中，通过封装隐藏复杂的硬件访问细节，提供简单的接口来控制设备。
4. **业务逻辑抽象**：
    - 在业务系统中，通过封装将复杂的业务逻辑细节隐藏起来，对外提供简单的服务接口。
5. **数据缓存**：
    - 在需要缓存数据的场景中，通过封装实现数据的懒加载，即仅在需要时才从数据库或其他存储介质中加载数据。
6. **日志记录和审计**：
    - 在setter和getter方法中添加日志记录，以跟踪对象状态的变化，这对于调试和审计非常有用。
7. **保护敏感信息**：
    - 对于包含敏感信息的对象，如银行账户、个人身份信息等，通过封装确保这些信息不被未授权访问。
8. **接口与实现的分离**：
    - 在开发库或框架时，通过封装将接口与具体实现分离，使得实现可以在不影响使用者的情况下进行更改。
9. **代码重用**：
    - 在需要重用代码的场景中，通过封装可以轻松地将一个类的实现替换为另一个类，只要它们提供了相同的接口。
10. **解耦合**：
    - 在复杂的系统中，通过封装减少各个组件之间的依赖，提高系统的灵活性和可维护性。

封装性是面向对象设计的核心原则之一，它有助于构建松耦合、高内聚的系统，使得代码更加健壮、灵活和易于维护。



例子

```java
public class PersonTest {
    public static void main(String[] args) {
        //创建Person实例1
        Person person1 = new Person();
        // person1.age;
        person1.setAge(18);
    }
}
```



```java
public class Person {
    private int age;

    //设置age的属性

    public void setAge(int age){
        if(age>= 0 && age <= 150){
            this.age = age;
        }else{
            System.out.println("年龄不合法");
        }
    }

    //获取age的属性

    public int getAge(){
        return age;
    }
}
```





构造器

在Java中，构造器（Constructor）是一种特殊的方法，用于在创建新对象时初始化对象。构造器的名称必须与类名完全相同，并且没有返回类型，甚至连`void`类型的返回值也没有。构造器的主要目的是让数据成员（属性）在对象创建时就被初始化。

### 构造器的特点：
1. **名称**：构造器的名称必须与类名完全相同。
2. **返回类型**：构造器没有返回类型，连`void`也不行。
3. **调用**：在创建新对象时自动调用。
4. **重载**：可以有多个构造器，只要它们的参数列表不同（参数的数量或类型不同）。
5. **隐式调用**：如果未显式定义构造器，编译器会提供一个默认无参构造器。

### 构造器的作用：
1. **初始化对象**：在对象创建时给对象的属性赋初值。
2. **控制对象的创建**：通过重载构造器，可以控制对象的创建过程。
3. **提高封装性**：通过私有构造器和工厂方法，可以控制对象的创建和访问。

### 构造器的分类：
1. **无参构造器**（No-argument Constructor）：
    - 没有参数的构造器。
    - 如果没有显式定义任何构造器，编译器会提供一个默认的无参构造器。
2. **有参构造器**（Parameterized Constructor）：
    - 带有参数的构造器，用于在创建对象时初始化对象的属性。
3. **重载构造器**（Constructor Overloading）：
    - 一个类中可以有多个构造器，只要它们的参数列表不同。

### 构造器的继承：
+ 父类的构造器不能被子类继承，子类必须通过`super`关键字显式调用父类的构造器。

### 构造器的使用示例：
```java
public class Person {
    private String name;
    private int age;

    // 无参构造器
    public Person() {
        this.name = "Unknown";
        this.age = 0;
        System.out.println("Person created with default values.");
    }

    // 有参构造器
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Person created with name: " + name + " and age: " + age);
    }

    // Getter and Setter
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

public class TestConstructor {
    public static void main(String[] args) {
        Person person1 = new Person(); // 调用无参构造器
        Person person2 = new Person("Alice", 30); // 调用有参构造器
    }
}
```

在这个例子中，`Person`类有两个构造器：一个无参构造器和一个有参构造器。无参构造器提供了默认的初始化值，而有参构造器允许在创建对象时设置具体的属性值。

构造器是对象生命周期的起点，正确地使用构造器可以确保对象在创建时就处于有效和一致的状态。



每个类都有构造器

构造器的作用

+ 搭配 new 关键字，创建类的对象
+ 在创建对象的同时，可以给对象的相关属性赋值
+ 创建类以后，在没有显示提供任何构造器的情况下，系统会默认提供一个空参的构造器，且权限与类的权限相同
+ 一旦类中显示声明了构造器，那么系统将不再提供·空参的构造器
+ 在一个类中可以声明多个构造器，彼此直接可以构成重载





```java
public class StudentTest {
    public static void main(String[] args) {
        Student s = new Student("张三", 20, "男", "计算机");
        System.out.println(s.name + " " + s.age + " " + s.school + " " + s.major);

        Student s2 = new Student("李四", 21);
        System.out.println(s2.name + " " + s2.age );

        

    }
}
```





```java
public class Student {
    //构造器说明
    //1.构造器没有返回值
    //2.构造器的名称必须和类名相同
    //3.构造器的作用是完成对对象的初始化操作
    //4.如果你没有显式的定义类的构造器的话，则系统默认提供一个无参数的构造器
    //5.一旦你显式的定义了一个构造器，则系统就不再提供默认的无参数的构造器了
    //6.构造器也是可以重载的


     String name;
     int age;
     String school;
     String major;//主修课

    public Student(String n, int a) {
        name = n;
        age = a;
    }

    public Student(String n, int a, String s) {
        name = n;
        age = a;
        school = s;
    }

    public Student(String name, int age, String school, String major) {
        this.name = name;
        this.age = age;
        this.school = school;
        this.major = major;
    }

    
}
```





存款取款例子

```java
public class CustomerTest {
    public static void main(String[] args) {
        //创建Customer实例
        Customer customer = new Customer("Jane", "Smith");

        Account account = new Account(1001, 20000.0, 0.045);
        customer.setAccount(account);

        System.out.println("客户姓名：" + customer.getFirstName() + " " + customer.getLastName());

        //对客户的取钱存钱
        customer.getAccount().deposit(1000);
        customer.getAccount().deposit(2000);
        customer.getAccount().withdraw(5000);

        //输出客户信息
        System.out.println("客户姓名：" + customer.getFirstName() + " " + customer.getLastName());

    }
}
```





```java
public class Customer {
    private String firstName;
    private String lastName;
    private Account account;

    public Customer(String f,String l){
        firstName=f;
        lastName=l;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public Account getAccount() {
        return account;
    }

    public void setAccount(Account account) {
        this.account = account;
    }

}
```



```java
public class Account {
    private int id;
    private double balname;//余额
    private double annualInterestRate;//年利率

    public Account(int i,double b,double a){
        id=i;
        balname=b;
        annualInterestRate=a;
    }

    public int getId(){
        return id;

    }

    public void setBalname(double b){
        balname=b;
    }

    public void setId(int i){
        id=i;
    }

    public void setAnnualInterestRate(double a){
        annualInterestRate=a;
    }

    public double getAnnualInterestRate(){
        return annualInterestRate;
    }

    public void withdraw(double m){
        if(m>balname){
            System.out.println("余额不足");
        }else{
            balname=balname-m;
            System.out.println("取款成功");
        }
    }

    public void deposit(double m){
        balname+=m;
        System.out.println("存款成功");
    }

    



}
```

在Java中，匿名对象（Anonymous Object）是指没有显式名称的对象。这种对象通常是局部的，并且只在创建它的代码块中可见。匿名对象经常与接口或抽象类的匿名内部类一起使用，以实现特定的行为。

### 匿名对象的特点：
1. **局部作用域**：匿名对象只在创建它的代码块中有效。
2. **没有名称**：匿名对象没有名称，因此不能被引用。
3. **单次使用**：通常用于单次操作，如创建后立即调用其方法。
4. **与接口或抽象类一起使用**：经常用来直接实现接口或继承抽象类，而不需要创建一个具体的类。

### 匿名对象的使用场景：
1. **实现接口**：当需要一个接口的实例来临时实现某个功能时。
2. **继承抽象类**：当需要一个抽象类的实例来临时实现某些方法时。
3. **回调**：在需要提供回调函数时，尤其是当回调只需要使用一次时。
4. **事件监听器**：在为组件添加事件监听器时，经常使用匿名对象来实现`EventListener`接口。

### 匿名对象的示例：
```java
// 使用匿名对象实现Runnable接口来创建线程
Thread thread = new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Thread is running.");
    }
});

thread.start();

// 使用匿名对象作为方法参数
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        System.out.println("Button is clicked.");
    }
});
```

在第一个例子中，我们创建了一个`Thread`对象，其接收一个实现了`Runnable`接口的匿名对象作为参数。这个匿名对象重写了`run`方法，当线程启动时，会执行这个方法。

在第二个例子中，我们创建了一个按钮点击事件的监听器。我们传递了一个实现了`View.OnClickListener`接口的匿名对象给`setOnClickListener`方法。这个匿名对象重写了`onClick`方法，当按钮被点击时，会执行这个方法。

### 匿名对象的注意事项：
+ 匿名对象不能有构造器，因为它们没有名称。
+ 匿名对象不能被声明为`final`，因为它们没有名称，无法被引用。
+ 匿名对象通常用于实现一个接口或继承一个抽象类，并且实现的方式是匿名的、局部的。

匿名对象是Java中实现特定功能的一种简洁方式，它们使得代码更加紧凑，尤其是在处理回调和事件监听器时。然而，过度使用匿名对象可能会导致代码的可读性和可维护性降低，因此应该在适当的场合使用。



匿名对象没有对象名，往往只能使用一次，后续无法调用。

匿名对象常常作为实参传递给形参



'''

customer.setAcccount().deposit(100);



'''



类中属性 可以通过哪种方法赋值

+ 默认赋值 
+ 显示赋值 
+ 构造器中赋值 
+ 通过对象.方法赋值 
+ 通过对象.属性 的方式赋值



赋值的先后顺序

1 2 3 4/5



在Java中，类的属性（成员变量）可以通过以下几种方式进行赋值，并且它们的赋值顺序如下：

1. **直接在字段声明时赋值（Field Initialization）**：  
属性可以在声明时直接赋予初始值。

```java
public class Example {
    public int value = 10; // 声明时直接赋值
}
```

这种赋值方式最先执行，因为它是直接在字段声明时进行的。

2. **通过构造器赋值（Constructor Assignment）**：  
在类的构造器中对属性进行赋值。

```java
public class Example {
    private int value;
    public Example(int value) {
        this.value = value; // 通过构造器赋值
    }
}
```

构造器赋值在对象创建时执行，它在字段声明赋值之后执行，因为对象的内存空间被分配后，首先会执行字段的声明赋值，然后才执行构造器中的代码。

3. **通过代码块赋值（Instance Initializer Block）**：  
使用实例初始化块对属性进行赋值。

```java
public class Example {
    private int value;
    {
        value = 20; // 实例初始化块赋值
    }
}
```

实例初始化块在构造器执行之前，按照它们在代码中出现的顺序执行。

4. **通过静态代码块赋值（Static Initializer Block）**：  
使用静态初始化块对属性进行赋值。

```java
public class Example {
    private static int value;
    static {
        value = 30; // 静态初始化块赋值
    }
}
```

静态初始化块在类被加载到JVM时执行，且仅执行一次。它先于任何对象的创建和实例初始化块执行。

5. **通过setter方法赋值（Setter Method）**：  
通过公共的setter方法对属性进行赋值。

```java
public class Example {
    private int value;
    public void setValue(int value) {
        this.value = value; // 通过setter方法赋值
    }
}
```

setter方法赋值可以在对象创建后的任何时间点执行，具体取决于代码逻辑。

### 赋值顺序总结：
1. **静态字段声明赋值**：`static int value = 30;`
2. **静态代码块**：`static { value = 30; }`
3. **字段声明赋值**：`int value = 10;`
4. **实例代码块**：`{ value = 20; }`
5. **构造器**：在构造器中通过`this.value = value;`赋值
6. **setter方法**：在对象创建后通过`setValue`方法赋值

这个顺序展示了在Java中一个类的属性可能被赋值的不同阶段。静态初始化只在类加载时发生一次，而实例相关的赋值在每个对象创建时发生。setter方法则提供了一种灵活的途径，在对象的生命周期中随时可以改变属性值。







JavaBean是遵循特定编写规范的Java类，通常用于表示应用程序的数据。这个概念最早由Sun Microsystems公司提出，并成为了Java应用开发中一个广泛使用的组件技术。JavaBean可以是可视化组件，也可以是非可视化的，它们通常用于以下两个主要目的：

1. **封装数据**：JavaBean提供了一种封装数据和业务逻辑的方式，使得数据可以被不同部分的应用程序所使用。
2. **遵循标准**：JavaBean遵循特定的命名和属性管理约定，使得它们可以被各种开发工具和应用程序框架识别和操作。

### JavaBean的特点：
1. **可序列化**：JavaBean通常是可序列化的，这意味着它们可以被转化为字节流，方便在网络上传输或存储到文件中。
2. **属性访问方法**：JavaBean通过标准的getter和setter方法来访问私有属性。
3. **可选的构造器**：除了默认的无参构造器外，JavaBean可以提供其他构造器来初始化对象。
4. **事件处理**：可视化JavaBean可以有事件监听器和通知方法。
5. **可选的持久性**：JavaBean可以实现`java.io.Externalizable`接口来自定义序列化行为。
6. **设计模式**：JavaBean经常与设计模式如工厂模式、单例模式等结合使用。

### JavaBean的规范：
+ **属性访问**：属性通常通过`getPropertyName()`和`setPropertyName(value)`方法访问，其中`PropertyName`是属性名，首字母大写。
+ **布尔属性**：对于布尔类型的属性，通常使用`isPropertyName()`作为getter方法，`setPropertyName(value)`作为setter方法。
+ **构造器**：除了默认构造器外，可以提供带参数的构造器来初始化对象。
+ **序列化**：实现`java.io.Serializable`接口，使得对象可以被序列化和反序列化。
+ **可选的标签**：可以使用`java.beans`包中的类和接口来提供额外的功能，如属性更改事件和自定义器。

### JavaBean的简单示例：
```java
import java.io.Serializable;

public class UserBean implements Serializable {
    private String name;
    private int age;

    // 默认构造器
    public UserBean() {
    }

    // 带参数的构造器
    public UserBean(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 标准的getter和setter方法
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

在这个例子中，`UserBean`类有两个属性：`name`和`age`。它提供了标准的getter和setter方法来访问这些属性，并且实现了`Serializable`接口，使得`UserBean`对象可以被序列化。

JavaBean是Java EE规范的一部分，它们在Java应用开发中扮演着重要的角色，尤其是在MVC（模型-视图-控制器）架构中，JavaBean通常用作模型，负责存储数据和业务逻辑。



统一建模语言（Unified Modeling Language，UML）是一种标准的建模语言，用于软件工程中对软件系统的结构、行为和规则进行可视化。UML类图（Class Diagram）是UML中使用最广泛的一种图，用于展示系统的静态结构，即系统中的类、接口、枚举和它们之间的关系。

### UML类图的主要组成部分：
1. **类（Class）**：
    - 用矩形表示，矩形顶部提供类名，下方可以显示属性（attributes）和操作（operations）。
2. **属性（Attributes）**：
    - 类的内部结构，包括数据字段和常量，通常显示在类名下方。
3. **操作（Operations）**：
    - 类的行为，包括方法和构造函数，通常显示在属性下方。
4. **关系（Relationships）**：
    - 类与类之间的连接，包括依赖（Dependency）、关联（Association）、聚合（Aggregation）和组合（Composition）。
5. **接口（Interface）**：
    - 用一个带有曲线的矩形表示，内部可以包含操作签名。
6. **泛化（Generalization）**：
    - 表示继承关系，用一个带有空心箭头的直线连接子类和父类。
7. **实现（Realization）**：
    - 表示类实现了接口，用一个带有空心箭头的虚线连接类和接口。
8. **依赖（Dependency）**：
    - 表示一个类的变化可能影响到另一个类，用一条带箭头的虚线表示。
9. **关联（Association）**：
    - 表示两个类之间的结构关系，用一条实线表示。
10. **聚合（Aggregation）**：
    - 表示整体与部分的关系，但部分可以独立于整体存在，用一条带有菱形的实线表示。
11. **组合（Composition）**：
    - 表示整体与部分的关系，部分不能独立于整体存在，用一条带有实心菱形的实线表示。

### UML类图的表示方法：
+ **类名**：
    - 通常以大写字母开头，如`Classname`。
+ **属性和操作**：
    - 属性通常以`-`（私有）或`+`（公共）开头，操作以`+`（公共）或`-`（私有）开头。
    - 属性和操作可以有类型和名称，如`+visibility : Type`。
+ **可见性**：
    - `+`表示公共（public）。
    - `-`表示私有（private）。
    - `#`表示受保护（protected）。
    - `~`表示包级私有（package-private）。

### UML类图的作用：
1. **系统设计**：
    - 提供系统的静态视图，帮助开发者理解系统的结构。
2. **文档化**：
    - 作为项目文档的一部分，供团队成员和利益相关者参考。
3. **沟通工具**：
    - 帮助开发者和非技术人员之间就系统设计进行沟通。
4. **分析和规划**：
    - 在软件开发的早期阶段，用于识别和规划系统的需求。
5. **维护和扩展**：
    - 为现有系统的维护和扩展提供参考。

UML类图是一种强大的工具，可以帮助开发者以图形化的方式理解和设计复杂的系统结构。通过UML类图，开发者可以清晰地看到系统中的各个组件及其相互关系，这对于大型软件项目的成功至关重要。



# 复习


面向对象编程（OOP）是一种编程范式，它使用“对象”来设计应用程序，并将数据和方法封装在对象中。以下是面向对象编程中完成具体功能的操作的三步流程：

### 步骤1: 创建类，并设计类的内部成员（属性，方法）
在这一步中，你需要定义一个类，这个类将作为创建对象的蓝图。类的内部成员包括属性（也称为字段或变量）和方法（也称为函数或过程）。属性用于存储数据，而方法定义了对象可以执行的操作。

```java
class Phone {
    // 属性
    String brand;
    int memory;

    // 方法
    void call() {
        System.out.println("Making a call...");
    }

    void sendSMS(String message) {
        System.out.println("Sending SMS: " + message);
    }
}
```

### 步骤2: 创建类的对象
一旦类被定义，下一步就是创建类的实例，也就是对象。在Java中，这是通过使用`new`关键字完成的。

```java
Phone phoneP1 = new Phone();
```

这行代码在堆内存中为`Phone`类的一个新对象分配空间，并返回一个指向该对象的引用。

### 步骤3: 通过对象，调用其内部声明的属性或方法，完成相关的功能
创建对象后，你可以通过对象引用来访问其属性和方法，从而执行操作。

```java
phoneP1.brand = "Moonshot";
phoneP1.memory = 128;
phoneP1.call();
phoneP1.sendSMS("Hello, World!");
```

### 对象的内存解析
在Java中，对象的内存解析涉及到几个不同的内存区域：

+ **虚拟机栈（VM Stack）**：这是线程私有的内存区域，用于存储局部变量和部分结果，以及动态链接和方法出口等信息。每个方法执行时都会创建一个栈帧（Stack Frame），用于存储局部变量表、操作数栈、动态链接、方法出口等信息。
+ **堆（Heap）**：这是Java中最大的内存区域，也是垃圾收集器管理的主要区域。所有的对象实例和数组都是在这里分配的。
+ **方法区（Method Area）**：用于存储已被虚拟机加载的类信息、常量、静态变量等数据。
+ **程序计数器（Program Counter Register）**：这块内存区域很小，用于存储指向下一条指令的地址，即字节码行号指示器。
+ **本地方法栈（Native Method Stack）**：与虚拟机栈类似，但是用于支持本地方法的执行。

通过这些内存区域的协同工作，Java程序能够创建对象、调用方法，并管理内存。



权限修饰符 返回值类型 方法名(形参列表){  方法体 }



在面向对象编程（OOP）中，方法声明是定义类中方法的过程，这些方法定义了对象可以执行的操作。方法声明包括以下几个关键部分：

1. **访问修饰符**：定义了方法的可见性，例如`public`、`private`、`protected`等。
2. **返回类型**：方法执行后返回的数据类型。如果方法不返回任何值，则返回类型为`void`。
3. **方法名**：方法的名称，它应该是描述性的，以便于理解方法的功能。
4. **参数列表**：方法执行时需要的输入值，这些值在方法内部作为局部变量使用。参数列表包括参数类型和参数名，多个参数之间用逗号分隔。
5. **方法体**：方法的具体实现，即方法执行时所执行的代码块。
6. **异常**：方法可能抛出的异常列表。

下面是一个Java中方法声明的示例：

```java
public class Calculator {

    // 计算两个整数的和
    public int add(int num1, int num2) {
        return num1 + num2;
    }

    // 计算两个浮点数的差，可能抛出算术异常
    public double subtract(double num1, double num2) throws ArithmeticException {
        return num1 - num2;
    }

    // 显示欢迎信息，不返回任何值
    public void displayWelcomeMessage() {
        System.out.println("Welcome to the Calculator Application!");
    }
}
```

在这个例子中：

+ `public`是访问修饰符，表示这些方法可以被任何其他类访问。
+ `int`、`double`和`void`是返回类型。
+ `add`、`subtract`和`displayWelcomeMessage`是方法名。
+ `(int num1, int num2)`、`(double num1, double num2)`是参数列表。
+ 方法体包含了具体的执行代码。
+ `throws ArithmeticException`表示`subtract`方法可能会抛出`ArithmeticException`异常。

方法声明定义了方法的接口，即其他代码如何与方法交互，以及方法将执行什么操作。





调用方法时通过方法名与形参列表确定方法



方法重载（Method Overloading）是面向对象编程中的一个特性，它允许在同一个类中存在多个同名方法，只要这些方法的参数列表不同。参数列表不同可以是参数的类型不同、参数的数量不同，或者两者都不同。方法重载的主要目的是提供相同功能的多种版本，以适应不同的输入。

### 方法重载的规则：
1. **方法名相同**：重载的方法必须在同一个类中，并且方法名相同。
2. **参数列表不同**：参数的数量、类型或顺序必须至少有一个不同。
3. **返回类型不相关**：方法的返回类型不作为区分重载方法的因素。
4. **访问修饰符不相关**：方法的访问修饰符（如`public`、`private`等）也不影响方法重载。

### 方法重载的例子：
```java
public class Example {

    // 方法重载示例：根据参数数量不同
    public void display() {
        System.out.println("Display with no arguments");
    }

    public void display(int number) {
        System.out.println("Display with one argument: " + number);
    }

    public void display(String str) {
        System.out.println("Display with one argument: " + str);
    }

    // 方法重载示例：根据参数类型不同
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}
```

在这个例子中：

+ `display`方法被重载了三次，每次的参数列表都不同：无参数、一个`int`参数、一个`String`参数。
+ `add`方法也被重载了两次，每次接受的参数类型不同：两个`int`参数和两个`double`参数。

### 方法重载的优点：
1. **提高代码的可读性**：通过提供多个重载方法，可以使得代码更加直观和易于理解。
2. **增加代码的灵活性**：开发者可以根据需要调用不同参数的重载方法，使得代码更加灵活。
3. **减少错误**：通过明确区分不同参数的方法，可以减少调用错误的可能性。

方法重载是面向对象编程中一个非常有用的功能，它使得方法调用更加灵活和直观。





对象数组是数组的一种，它用于存储对象的引用。在面向对象编程中，对象数组允许你创建一个可以包含多个对象的数组，这些对象通常是同一个类或者同一个类的子类的实例。对象数组的声明、创建和使用与基本数据类型的数组类似，但是它们存储的是对象引用而不是实际的数据值。

### 声明对象数组
对象数组的声明需要指定对象的类型。例如，如果你有一个名为`Car`的类，你可以这样声明一个`Car`类型的对象数组：

```java
Car[] carArray;
```

### 创建对象数组
创建对象数组与创建基本数据类型数组类似，但是你需要使用`new`关键字来指定数组的大小，并初始化数组：

```java
carArray = new Car[3]; // 创建一个可以存储3个Car对象的数组
```

### 初始化对象数组
对象数组的每个元素都是一个引用，你需要为每个元素分配一个实际的对象：

```java
carArray[0] = new Car();
carArray[1] = new Car();
carArray[2] = new Car();
```

或者，你可以在声明和创建数组的同时进行初始化：

```java
Car[] carArray = {
    new Car(),
    new Car(),
    new Car()
};
```

### 使用对象数组
一旦对象数组被初始化，你就可以像使用普通数组一样使用它，通过索引来访问和操作数组中的每个对象：

```java
carArray[0].startEngine(); // 调用第一个Car对象的startEngine方法
carArray[1].stopEngine();  // 调用第二个Car对象的stopEngine方法
```

### 对象数组的特点
1. **灵活性**：对象数组可以存储任何与数组类型兼容的对象，包括继承自同一基类的子类对象。
2. **多态性**：在对象数组中，可以利用多态性存储不同子类的对象，并调用它们共有的方法。
3. **动态大小**：虽然数组的大小在创建时被固定，但是可以使用集合类（如`ArrayList`）来创建动态大小的对象数组。
4. **内存管理**：对象数组存储的是对象的引用，而不是对象本身。对象本身存储在堆内存中，而数组存储的是指向这些对象的引用。

对象数组是面向对象编程中处理多个对象时常用的数据结构，它提供了一种方便的方式来组织和管理对象集合。





Java 是一种强类型、面向对象的编程语言，它提供了一系列的关键字来支持其语言特性和功能。以下是一些常用的 Java 关键字：

1. **访问控制关键字**：
    - `public`：声明公共的类、接口、方法和变量，可以被任何其他类访问。
    - `protected`：声明受保护的成员，可以被同一包中的类以及所有子类访问。
    - `private`：声明私有成员，只能被声明它的类访问。
    - `default`（没有关键字）：当没有指定访问修饰符时，默认的访问级别，只能被同一包中的类访问。
2. **非访问控制关键字**：
    - `abstract`：声明抽象类或抽象方法，没有具体实现。
    - `final`：声明一个类、方法或变量不可被改变或覆盖。
    - `static`：声明静态成员，属于类而不是类的实例。
    - `transient`：声明一个字段在序列化时应被忽略。
    - `volatile`：声明一个变量在多个线程间共享时，总是从主内存中读取。
    - `synchronized`：用于同步方法或代码块，确保在同一时刻只有一个线程执行。
    - `strictfp`：用于声明严格模式的浮点数计算。
3. **程序控制关键字**：
    - `if`：条件语句，根据条件是否满足来执行不同的代码块。
    - `else`：与`if`配合使用，表示条件不满足时执行的代码块。
    - `switch`：多条件分支语句。
    - `case`：与`switch`配合使用，表示一个分支条件。
    - `default`：与`switch`配合使用，表示默认的分支条件。
    - `for`：用于循环，适用于已知循环次数的情况。
    - `while`：当条件满足时重复执行代码块。
    - `do`：至少执行一次代码块，然后检查条件是否满足以决定是否继续循环。
    - `break`：跳出最近的循环或`switch`语句。
    - `continue`：跳过当前循环的剩余部分，开始下一次循环。
4. **类和对象关键字**：
    - `class`：声明一个类。
    - `interface`：声明一个接口。
    - `extends`：表示一个类继承另一个类。
    - `implements`：表示一个类实现了一个或多个接口。
    - `this`：引用当前对象的上下文。
    - `super`：引用父类的上下文或父类的构造方法。
5. **异常处理关键字**：
    - `try`：开始一个异常处理块。
    - `catch`：捕获并处理`try`块中抛出的异常。
    - `finally`：无论是否捕获到异常，都会执行的代码块。
    - `throw`：抛出一个异常。
    - `throws`：声明一个方法可能抛出的异常。
6. **其他关键字**：
    - `boolean`、`byte`、`char`、`short`、`int`、`long`、`float`、`double`：基本数据类型关键字。
    - `void`：表示没有返回值的方法。
    - `null`：表示没有值。
    - `true`、`false`：布尔值。
7. **类型转换关键字**：
    - `instanceof`：检查一个对象是否是特定类的实例。

这些关键字是 Java 语言的基础，它们使得 Java 能够实现面向对象编程、异常处理、程序控制等核心功能。



面试：java封装性的体系



> java规定了四种选线修饰符，分别是private，缺省，protected，public我们可以使用四种权限修饰符来修饰类及类的内部成员。当这些成员被调用时，体现可见性的大小
>



> 场景1:私有化(private)类的属性，提供公共(public)的get和set方法，对此属性进行获取或修改  
场景2:将类中不需要对外暴露的方法，设置为private.  
场景3:单例模式中构造器private的了，避免在类的外部创建实例。(放到static关键字后讲)
>



理论:程序设计的原则之一

理论上

高内聚`:类的内部数据操作细节自己完成，不允许外部干涉;

（java程序通常以类的形态呈现，相关的功能封装到方法中。)

低耦合、:仅暴露少量的方法给外部使用，尽量方便外部调用。

(给相关的类、方法设置权限，把该隐藏的隐藏起来，该暴露的暴露出去)



类的成员之三:构造器

如何定义:权限修饰符 类名(形参列表){}

构造器的作用:① 搭配上new，用来创建对象 ② 初始化对象的成员变量







Java 的引用类型有哪几种(阿*校招)

类、数组、接口;枚举、注解、记录



面向对象，你解释一下，项目中哪些地方用到面向对象?(燕*金融)

“万事万物皆对象”



对象存在Java内存的哪块区域里面?

堆空间。

main方法的public能不能换成private?为什么?(凡*科技、顺*)

能。但是改以后就不能作为程序的入口了，就只是一个普通的方法。



构造方法和普通方法的区别(凡*科技、软*动力、中*软)

编写代码的角度:没有共同点。声明格式、作用都不同。

字节码文件的角度:构造器会以<init>()方法 的形态呈现;



2.构造器Constructor是否可被(重载)overload?(鸿*网络)

可以。



成员变量与局部变量的区别(艾*软件)

6个点。

变量赋值和构造方法加载的优先级问题(凡*科技、博*软件)

变量显式赋值先于构造器中的赋值。

如何证明?我看的字节码文件。



## 1. 关键字：this
### 1.1 this是什么？
+ 在Java中，this关键字不算难理解，它的作用和其词义很接近。
    - 它在方法（准确的说是实例方法或非static的方法）内部使用，表示调用该方法的对象
    - 它在构造器内部使用，表示该构造器正在初始化的对象。
+ this可以调用的结构：成员变量、方法和构造器

### 1.2 什么时候使用this
#### 1.2.1 实例方法或构造器中使用当前对象的成员
在实例方法或构造器中，如果使用当前类的成员变量或成员方法可以在其前面添加this，增强程序的可读性。不过，通常我们都习惯省略this。

但是，当形参与成员变量同名时，如果在方法内或构造器内需要使用成员变量，必须添加this来表明该变量是类的成员变量。即：我们可以用this来区分`成员变量`和`局部变量`。比如：

另外，使用this访问属性和方法时，如果在本类中未找到，会从父类中查找。这个在继承中会讲到。



在Java中，`this`关键字是一个特殊的引用，指向当前对象的实例。它在类的方法和构造函数中使用，主要有以下几个用途：

1. **区分实例变量和参数**：  
当方法或构造函数的参数与实例变量同名时，可以使用`this`来区分它们。例如：

```java
public class Person {
    private String name;

    public Person(String name) {
        this.name = name; // this.name指的是实例变量，name指的是参数
    }
}
```

2. **调用当前对象的方法**：  
可以使用`this`来调用当前对象的其他方法。例如：

```java
public class Calculator {
    public void add(int a, int b) {
        System.out.println(this.sum(a, b)); // 调用当前对象的sum方法
    }

    private int sum(int a, int b) {
        return a + b;
    }
}
```

3. **在构造函数中调用其他构造函数**：  
可以使用`this()`来调用同一类中的其他构造函数，这种调用必须是构造函数的第一行。例如：

```java
public class Rectangle {
    private int width;
    private int height;

    public Rectangle() {
        this(10, 20); // 调用带参数的构造函数
    }

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }
}
```

4. **返回当前对象**：  
在某些方法中，可以返回当前对象的引用，通常用于方法链。例如：

```java
public class Builder {
    private String value;

    public Builder setValue(String value) {
        this.value = value;
        return this; // 返回当前对象
    }
}
```

总结来说，`this`关键字在Java中用于引用当前对象的实例，帮助区分变量、调用方法、构造函数等，增强代码的可读性和可维护性。



this 可以调用的结构，成员方法，构造器





一般情况:我们通过对象a调用方法，可以在方法内调用当前对象a的属性或其他方法。此时，我们可以在属性和其他方法前

使用"this."，表示当前属性或方法所属的对象a。但是，一般情况下，我们都选择省略此"this."结构。



特殊情况:如果方法的形参与对象的属性同名了，我们必须使用"this."进行区分。使用this.修饰的变量即为属性(或成员变量)

没有使用this.修饰的变量，即为局部变量。







```java
public class User {
    private String name;
    private int age;

    // 无参数的构造函数
    public User() {
        // 模拟对象创建时，需要初始化50行代码。
        // 这里只是示例，所以没有写出50行代码
    }

    // 带一个参数name的构造函数
    public User(String name) {
        this(); // 调用无参数的构造函数
        this.name = name; // 设置name属性
    }

    // 带两个参数name和age的构造函数
    public User(String name, int age) {
        this(name); // 调用带一个参数的构造函数
        this.age = age; // 设置age属性
    }
}
```

代码说明：

1. **类定义**：定义了一个名为`User`的类，包含两个私有属性`name`和`age`。
2. **无参数的构造函数**：
    - `public User()`：这是一个无参数的构造函数，用于创建`User`对象时初始化对象。
    - 在这个构造函数中，可以执行一些初始化操作，比如设置默认值或者执行一些必要的初始化代码。这里的注释说明了这一点，但实际代码中并没有写出50行初始化代码。
3. **带一个参数的构造函数**：
    - `public User(String name)`：这是一个带有一个参数`name`的构造函数。
    - `this()`：在构造函数的第一行调用了无参数的构造函数，这样可以确保在设置`name`之前，对象的其他属性已经被初始化。
    - `this.name = name;`：使用`this`关键字来区分参数`name`和实例变量`name`，将传入的参数值赋给实例变量`name`。
4. **带两个参数的构造函数**：
    - `public User(String name, int age)`：这是一个带有两个参数`name`和`age`的构造函数。
    - `this(name)`：在构造函数的第一行调用了带有一个参数的构造函数，这样可以确保在设置`age`之前，对象的其他属性（包括`name`）已经被初始化。
    - `this.age = age;`：使用`this`关键字来区分参数`age`和实例变量`age`，将传入的参数值赋给实例变量`age`。

通过这种方式，`User`类提供了灵活的构造函数，可以根据需要创建具有不同属性值的`User`对象。



4.2 this调用构造器

格式:"this(形参列表)"

我们可以在类的构造器中，调用当前类中指定的其它构造器

要求:"this(形参列表)"必须声明在当前构造器的首行

结论:"this(形参列表)"在构造器中最多声明一个

如果一个类中声明了n个构造器，则最多有n-1个构造器可以声明有"this(形参列表)"的结构



# 继承性


代码层面:

> 自上而下:定义了一个类A，在定义另一个类B时，发现类B的功能与类A相似，考虑类B继承于类A  
自下而上:定义了类B,C，0等，发现B、C、0有类似的属性和方法，则可以考虑将相同的属性和方法进行抽取。  
封装到类A中，让类B、C、D继承于类A,同时，B、C、D中的相似的功能就可以刚除了。
>



有了继承，子类就获取了父类的所有属性和方法

私有权限不能继承



Java是一种面向对象的编程语言，继承性是面向对象编程的核心概念之一。继承性允许我们创建一个类（称为子类或派生类）来继承另一个类（称为父类或基类）的属性和方法。以下是Java继承性的几个关键点：

1. **代码重用**：继承性使得代码重用变得简单。子类可以继承父类的属性和方法，从而避免重复编写相同的代码。
2. **层次结构**：继承性允许创建类之间的层次结构。一个父类可以有多个子类，子类继承父类的特性，并可以添加自己的特性。
3. **多态性**：继承性是多态性的基础。多态性允许我们用父类类型的引用来引用子类的对象，使得同一个方法调用可以有不同的行为。
4. **访问控制**：在Java中，子类可以访问父类的公共（public）和受保护（protected）成员，但不能访问私有（private）成员。
5. **方法覆盖（Override）**：子类可以覆盖父类的方法，即提供一个新的实现。这要求子类的方法签名必须与父类中被覆盖的方法完全相同。
6. **构造方法**：子类不能继承父类的构造方法，但可以在其构造方法中通过`super()`调用父类的构造方法。
7. **super关键字**：`super`关键字用于访问父类的属性和方法，也用于在子类的构造方法中调用父类的构造方法。
8. **final类和方法**：如果一个类被声明为`final`，则不能被继承。如果一个方法被声明为`final`，则不能被覆盖。
9. **抽象类和接口**：Java中的抽象类和接口也是继承性的一部分。抽象类可以包含抽象方法，这些方法没有实现，必须由子类实现。接口定义了一组方法规范，任何实现该接口的类都必须实现这些方法。
10. **继承的传递性**：如果类B继承自类A，类C继承自类B，那么类C间接继承了类A的所有属性和方法。

继承性是Java编程中的一个重要特性，它提供了一种机制，允许开发者在现有代码的基础上构建新的功能，同时保持代码的清晰和可维护性。



```java
public class ExtendsTest {
    public static void main(String[] args) {
        Person p1 = new Person();
       
        p1.eat();
        student s1 = new student();
        s1.eat();
    }
}
```



```java
public class Person extends student{
    //java继承性

    String name;
    int age;

    // public void eat(){
    //     System.out.println("吃饭");
    // }

    // public void sleep(){
    //     System.out.println("睡觉");
    // }

    public void study(){
        System.out.println("学习");
    }


}
```



```java
public class student {
    
    String name;
    int age;

    //方法
    public void eat(){
        System.out.println("人吃饭");
    }

    public void sleep(){
        System.out.println("人睡觉");
    }

    public void study(){
        System.out.println("人学习");
    }

}
```



4.有了继承性以后:

子类就获取到了父类中声明的所有的属性和方法。

但是，由于封装性的影响，可能子类不能直接调用父类中声明的属性或方法

子类在继承父类以后，还可以扩展自己特有的功能(体现:增加特有的性、方法)

extends:延展、扩展、延伸

理解：子类和父类要区别于集合和子集

不要为了继承而继承，在继承前要判断是否存在 is a 的关系



语法示例  public class Student extends Person{ }







//超纲:获取s1所属类的父类

System.out.println(s1.getclass().getSuperclass());

//超纲:获取p1所属类的父类

System.out.println(p1.getclass().getSuperclass());

Java 中声明的类，如果没有显示声明其父类时，则默认继承于 java.lang.Object



java 继承时单继承 不支持继承多个父类（不能认义父）



其它：直接父类，间接父类

子父类的概念是相对的



**Java支持多层继承(继承体系)**

```java
class A{}
class B extends A{}
class C extends B{}
```

> 说明：
>
> + 子类和父类是一种相对的概念
> + 顶层父类是Object类。所有的类默认继承Object，作为父类。
>

**一个父类可以同时拥有多个子类**

```java
class A{}
class B extends A{}
class D extends A{}
class E extends A{}
```

**Java只支持单继承，不支持多重继承**

```java
public class A{}
class B extends A{}

//一个类只能有一个父类，不可以有多个直接父类。
class C extends B{} 	//ok
class C extends A,B...	//error
```

### 
继承性 练习**练习2：**

(1)定义一个ManKind类，包括

+ 成员变量int sex和int salary；
+ 方法void manOrWoman()：根据sex的值显示“man”(sex<font style="background-color:#f3bb2f;">1)或者“woman”(sex</font>0)；
+ 方法void employeed()：根据salary的值显示“no job”(salary==0)或者“ job”(salary!=0)。

(2)定义类Kids继承ManKind，并包括

+ 成员变量int yearsOld；
+ 方法printAge()打印yearsOld的值。

(3)定义类KidsTest，在类的main方法中实例化Kids的对象someKid，用该对象访问其父类的成员变量及方法。

```java
public class KindTest {
    public static void main(String[] args) {
        kinds kid = new kinds();

        kid.setSalary(100);
        kid.setSex(1);
        kid.setYearOld(12);

        kid.printAge();
    }
}
```



```java
public class Mankind{
    private int sex;
    private int salary;

    public Mankind() {

    }   


    public Mankind(int sex,int salary){
        this.sex=sex;
        this.salary=salary;

    }

    public int getSex(){
        return sex;
    }

    public void setSex(int sex){
        this.sex=sex;
    }

    public int getSalary(){
        return salary;
    }

    public void setSalary(int salary){
        this.salary=salary;
    }

    public void manWoman(){
        if(sex==1){
            System.out.println("Man");
        }else{
            System.out.println("Woman");
        }
    }

    public void employeed() {
        if(salary==0){
            System.out.println("no job");
        }else{
            System.out.println("job");
        }
    }


}
```



```java
public class kinds extends Mankind {
    private int yearOld;

    public kinds(){

    }

    public kinds(int yearOld){
        this.yearOld = yearOld;
    }

    public void setYearOld(int yearOld) {
        this.yearOld = yearOld;
    }

    public void setYearOld(int sex,int salary, int yearOld) {
        setSalary(salary);
        setSex(sex);
    }

    public int getYearOld() {
        return yearOld;
    }

    public void printAge(){
        System.out.println("I am " + yearOld + " years old.");
    }
    
}
```



求原著的底面积 体积

```java
public class CylinderTest {
    public static void main(String[] args) {
        Cylinder c = new Cylinder();
        c.setRadius(2);
        c.setLength(3.4);

        System.out.println("半径为" + c.getRadius() + "，高为" + c.getLength() + "的圆柱体体积为：" + c.getVolume(c.getRadius()));
    }
}
```

```java
public class Cylinder extends circle{
    private double length;

    public Cylinder() {
        length = 1;
    }

    public Cylinder(double length) {
        this.length = length;
    }

    public double getLength() {
        return length;
    }

    public void setLength(double length) {
        this.length = length;
    }

    //求体积
    public double getVolume(double radius) {
        return Math.PI * getRadius() * getRadius() * getLength();
    }

}
```

```java
public class circle {
    private int radius; 

    public circle() {
        this.radius = 1;
    }

    public circle(int radius) {
        this.radius = radius;
    }

    public int getRadius() {
        return radius;
    }

    public void setRadius(int radius) {
        this.radius = radius;
    }

    //计算圆的面积
    public double getArea() {
        return Math.PI * getRadius() * getRadius();
    }
    

    
}
```



> @Override使用说明：
>
> 写在方法上面，用来检测是不是满足重写方法的要求。这个注解就算不写，只要满足要求，也是正确的方法覆盖重写。建议保留，这样编译器可以帮助我们检查格式，另外也可以让阅读源代码的程序员清晰的知道这是一个重写的方法。
>

### 3.2 方法重写的要求
1. 子类重写的方法`必须`和父类被重写的方法具有相同的`方法名称`、`参数列表`。
2. 子类重写的方法的返回值类型`不能大于`父类被重写的方法的返回值类型。（例如：Student < Person）。

> 注意：如果返回值类型是基本数据类型和void，那么必须是相同
>

3. 子类重写的方法使用的访问权限`不能小于`父类被重写的方法的访问权限。（public > protected > 缺省 > private）

> 注意：① 父类私有方法不能重写   ② 跨包的父类缺省的方法也不能重写
>

4. 子类方法抛出的异常不能大于父类被重写方法的异常



此外，子类与父类中同名同参数的方法必须同时声明为非static的(即为重写)，或者同时声明为static的（不是重写）。因为static方法是属于类的，子类无法覆盖父类的方法。

### 3.3 小结：方法的重载与重写
方法的重载：方法名相同，形参列表不同。不看返回值类型。

方法的重写：见上面。

（1）同一个类中

```java
package com.atguigu.inherited.method;

public class TestOverload {
    public int max(int a, int b){
        return a > b ? a : b;
    }
    public double max(double a, double b){
        return a > b ? a : b;
    }
    public int max(int a, int b,int c){
        return max(max(a,b),c);
    }
}
```

（2）父子类中

```java
package com.atguigu.inherited.method;

public class TestOverloadOverride {
    public static void main(String[] args) {
        Son s = new Son();
        s.method(1);//只有一个形式的method方法

        Daughter d = new Daughter();
        d.method(1);
        d.method(1,2);//有两个形式的method方法
    }
}

class Father{
    public void method(int i){
        System.out.println("Father.method");
    }
}
class Son extends Father{
    public void method(int i){//重写
        System.out.println("Son.method");
    }
}
class Daughter extends Father{
    public void method(int i,int j){//重载
        System.out.println("Daughter.method");
    }
}
```



为什么需要方法重写？

子类在继承父类后，就获取了父类中申明的所有方法。但是父类可能不太适用于子类。子类需要对父类继承过来的方法进行覆盖，覆写操作。





方法重写（Method Overriding）是面向对象编程（OOP）中的一个概念，它指的是在派生类（子类）中重新定义基类（父类）中已有的方法。这样做的目的通常是为了改变原有方法的行为，或者根据子类的具体需求来提供特定的实现。

以下是方法重写的关键点：

1. **继承关系**：重写发生在具有继承关系的类之间，即子类重写了父类的方法。
2. **方法签名**：重写的方法必须具有与父类中被重写方法相同的方法签名，即相同的方法名和参数列表。
3. **访问级别**：子类中重写的方法不能拥有比父类方法更严格的访问级别。
4. **返回类型**：重写的方法返回类型必须与父类方法的返回类型相同或者更具体（协变返回类型）。
5. **异常**：重写的方法可以抛出父类方法声明的所有异常，或者不抛出任何异常，但不能抛出更广泛的异常类型。
6. **多态性**：方法重写是实现多态性的一种方式。多态性允许你通过父类的引用来调用子类的方法。
7. **@Override 注解**：在某些编程语言（如Java）中，可以使用`@Override`注解来明确指出一个方法是重写了父类的方法。如果方法没有正确重写父类的方法，编译器会报错。
8. **super关键字**：在子类的方法中，可以使用`super`关键字来调用父类中被重写的方法。
9. **构造方法不能被重写**：构造方法不能被重写，因为它们不参与多态性。
10. **静态方法和最终方法**：静态方法和被声明为`final`的方法不能被重写。

方法重写是面向对象编程中实现代码复用和扩展功能的重要机制，它允许开发者在不修改原有代码的情况下，通过扩展已有的类来增加新的行为。



子类不能重写父类 private 权限方法



### 3.2 方法重写的要求
1. 子类重写的方法`必须`和父类被重写的方法具有相同的`方法名称`、`参数列表`。
2. 子类重写的方法的返回值类型`不能大于`父类被重写的方法的返回值类型。（例如：Student < Person）。

> 注意：如果返回值类型是基本数据类型和void，那么必须是相同
>

3. 子类重写的方法使用的访问权限`不能小于`父类被重写的方法的访问权限。（public > protected > 缺省 > private）

> 注意：① 父类私有方法不能重写   ② 跨包的父类缺省的方法也不能重写
>

4. 子类方法抛出的异常不能大于父类被重写方法的异常



此外，子类与父类中同名同参数的方法必须同时声明为非static的(即为重写)，或者同时声明为static的（不是重写）。因为static方法是属于类的，子类无法覆盖父类的方法。

### 3.3 小结：方法的重载与重写
方法的重载：方法名相同，形参列表不同。不看返回值类型。

方法的重写：见上面。

（1）同一个类中

```java
package com.atguigu.inherited.method;

public class TestOverload {
    public int max(int a, int b){
        return a > b ? a : b;
    }
    public double max(double a, double b){
        return a > b ? a : b;
    }
    public int max(int a, int b,int c){
        return max(max(a,b),c);
    }
}
```

（2）父子类中

```java
package com.atguigu.inherited.method;

public class TestOverloadOverride {
    public static void main(String[] args) {
        Son s = new Son();
        s.method(1);//只有一个形式的method方法

        Daughter d = new Daughter();
        d.method(1);
        d.method(1,2);//有两个形式的method方法
    }
}

class Father{
    public void method(int i){
        System.out.println("Father.method");
    }
}
class Son extends Father{
    public void method(int i){//重写
        System.out.println("Son.method");
    }
}
class Daughter extends Father{
    public void method(int i,int j){//重载
        System.out.println("Daughter.method");
    }
}
```



## 5. 关键字：super
### 5.1 super的理解
在Java类中使用super来调用父类中的指定操作：

+ super可用于访问父类中定义的属性
+ super可用于调用父类中定义的成员方法
+ super可用于在子类构造器中调用父类的构造器

注意：

+ 尤其当子父类出现同名成员时，可以用super表明调用的是父类中的成员
+ super的追溯不仅限于直接父类
+ super和this的用法相像，this代表本类对象的引用，super代表父类的内存空间的标识



为什么需要 super？

子类继承父类以后，对父类方法进行了重写，那么在子类中，是否花裤对父类中被重写的类进行调用?（可以）

子类继承父类以后，发现子类和父类中定义了同名属性，是否可以区分子类中两个同名的属性？（可以）



使用 super 关键字即可做到

super 的理解： 父类的



### 5.2 super的使用场景
#### 5.2.1 子类中调用父类被重写的方法
+ 如果子类没有重写父类的方法，只要权限修饰符允许，在子类中完全可以直接调用父类的方法；
+ 如果子类重写了父类的方法，在子类中需要通过`super.`才能调用父类被重写的方法，否则默认调用的子类重写的方法

举例：

```java
package com.atguigu.inherited.method;

public class Phone {
    public void sendMessage(){
        System.out.println("发短信");
    }
    public void call(){
        System.out.println("打电话");
    }
    public void showNum(){
        System.out.println("来电显示号码");
    }
}

//smartphone：智能手机
public class SmartPhone extends Phone{
    //重写父类的来电显示功能的方法
    public void showNum(){
        //来电显示姓名和图片功能
        System.out.println("显示来电姓名");
        System.out.println("显示头像");

        //保留父类来电显示号码的功能
        super.showNum();//此处必须加super.，否则就是无限递归，那么就会栈内存溢出
    }
}
```

总结：

+ **方法前面没有super.和this.**
    - 先从子类找匹配方法，如果没有，再从直接父类找，再没有，继续往上追溯
+ **方法前面有this.**
    - 先从子类找匹配方法，如果没有，再从直接父类找，再没有，继续往上追溯
+ **方法前面有super.**
    - 从当前子类的直接父类找，如果没有，继续往上追溯

#### 5.2.2 子类中调用父类中同名的成员变量
+ 如果实例变量与局部变量重名，可以在实例变量前面加this.进行区别
+ 如果子类实例变量和父类实例变量重名，并且父类的该实例变量在子类仍然可见，在子类中要访问父类声明的实例变量需要在父类实例变量前加super.，否则默认访问的是子类自己声明的实例变量
+ 如果父子类实例变量没有重名，只要权限修饰符允许，在子类中完全可以直接访问父类中声明的实例变量，也可以用this.实例访问，也可以用super.实例变量访问

举例：

```java
class Father{
    int a = 10;
    int b = 11;
}
class Son extends Father{
    int a = 20;
    
    public void test(){
        //子类与父类的属性同名，子类对象中就有两个a
        System.out.println("子类的a：" + a);//20  先找局部变量找，没有再从本类成员变量找
        System.out.println("子类的a：" + this.a);//20   先从本类成员变量找
        System.out.println("父类的a：" + super.a);//10    直接从父类成员变量找
        
        //子类与父类的属性不同名，是同一个b
        System.out.println("b = " + b);//11  先找局部变量找，没有再从本类成员变量找，没有再从父类找
        System.out.println("b = " + this.b);//11   先从本类成员变量找，没有再从父类找
        System.out.println("b = " + super.b);//11  直接从父类局部变量找
    }
    
    public void method(int a, int b){
        //子类与父类的属性同名，子类对象中就有两个成员变量a，此时方法中还有一个局部变量a		
        System.out.println("局部变量的a：" + a);//30  先找局部变量
        System.out.println("子类的a：" + this.a);//20  先从本类成员变量找
        System.out.println("父类的a：" + super.a);//10  直接从父类成员变量找

        System.out.println("b = " + b);//13  先找局部变量
        System.out.println("b = " + this.b);//11  先从本类成员变量找
        System.out.println("b = " + super.b);//11  直接从父类局部变量找
    }
}
class Test{
    public static void main(String[] args){
        Son son = new Son();
        son.test();
        son.method(30,13);  
    }
}
```

总结：起点不同（就近原则）

+ **变量前面没有super.和this.**
    - 在构造器、代码块、方法中如果出现使用某个变量，先查看是否是当前块声明的`局部变量`，
    - 如果不是局部变量，先从当前执行代码的`本类去找成员变量`
    - 如果从当前执行代码的本类中没有找到，会往上找`父类声明的成员变量`（权限修饰符允许在子类中访问的）
+ **变量前面有this.** 
    - 通过this找成员变量时，先从当前执行代码的<font style="background-color:#f3bb2f;">本类去找成员变量</font>
    - 如果从当前执行代码的本类中没有找到，会往上找<font style="background-color:#f3bb2f;">父类声明的成员变量（</font>权限修饰符允许在子类中访问的）
+ **变量前面super.** 
    - 通过super找成员变量，直接从当前执行代码的直接父类去找成员变量（权限修饰符允许在子类中访问的）
    - 如果直接父类没有，就去父类的父类中找（权限修饰符允许在子类中访问的）

**<font style="color:red;">特别说明：应该避免子类声明和父类重名的成员变量</font>**

在阿里的开发规范等文档中都做出明确说明：

![](images/image-20211230110411580.png)

#### 5.2.3 子类构造器中调用父类构造器
① 子类继承父类时，不会继承父类的构造器。只能通过“super(形参列表)”的方式调用父类指定的构造器。

② 规定：“super(形参列表)”，必须声明在构造器的首行。

③ 我们前面讲过，在构造器的首行可以使用"this(形参列表)"，调用本类中重载的构造器，  
     结合②，结论：在构造器的首行，"this(形参列表)" 和 "super(形参列表)"只能二选一。

④ 如果在子类构造器的首行既没有显示调用"this(形参列表)"，也没有显式调用"super(形参列表)"，  
     则子类此构造器默认调用"super()"，即调用父类中空参的构造器。

⑤ 由③和④得到结论：子类的任何一个构造器中，要么会调用本类中重载的构造器，要么会调用父类的构造器。  
     只能是这两种情况之一。

⑥ 由⑤得到：一个类中声明有n个构造器，最多有n-1个构造器中使用了"this(形参列表)"，则剩下的那个一定使用"super(形参列表)"。

> 开发中常见错误：
>
> 如果子类构造器中既未显式调用父类或本类的构造器，且父类中又没有空参的构造器，则`编译出错`。
>

情景举例1：

```java
class A{

}
class B extends A{

}

class Test{
    public static void main(String[] args){
        B b = new B();
        //A类和B类都是默认有一个无参构造，B类的默认无参构造中还会默认调用A类的默认无参构造
        //但是因为都是默认的，没有打印语句，看不出来
    }
}
```

情景举例2：

```java
class A{
    A(){
        System.out.println("A类无参构造器");
    }
}
class B extends A{

}
class Test{
    public static void main(String[] args){
        B b = new B();
        //A类显示声明一个无参构造，
        //B类默认有一个无参构造，
        //B类的默认无参构造中会默认调用A类的无参构造
        //可以看到会输出“A类无参构造器"
    }
}
```

情景举例3：

```java
class A{
    A(){
        System.out.println("A类无参构造器");
    }
}
class B extends A{
    B(){
        System.out.println("B类无参构造器");
    }
}
class Test{
    public static void main(String[] args){
        B b = new B();
        //A类显示声明一个无参构造，
        //B类显示声明一个无参构造，        
        //B类的无参构造中虽然没有写super()，但是仍然会默认调用A类的无参构造
        //可以看到会输出“A类无参构造器"和"B类无参构造器")
    }
}
```

情景举例4：

```java
class A{
    A(){
        System.out.println("A类无参构造器");
    }
}
class B extends A{
    B(){
        super();
        System.out.println("B类无参构造器");
    }
}
class Test{
    public static void main(String[] args){
        B b = new B();
        //A类显示声明一个无参构造，
        //B类显示声明一个无参构造，        
        //B类的无参构造中明确写了super()，表示调用A类的无参构造
        //可以看到会输出“A类无参构造器"和"B类无参构造器")
    }
}
```

情景举例5：

```java
class A{
    A(int a){
        System.out.println("A类有参构造器");
    }
}
class B extends A{
    B(){
        System.out.println("B类无参构造器");
    }
}
class Test05{
    public static void main(String[] args){
        B b = new B();
        //A类显示声明一个有参构造，没有写无参构造，那么A类就没有无参构造了
        //B类显示声明一个无参构造，        
        //B类的无参构造没有写super(...)，表示默认调用A类的无参构造
        //编译报错，因为A类没有无参构造
    }
}
```

![](images/image-20200227141228450.png)

情景举例6：

```java
class A{
    A(int a){
        System.out.println("A类有参构造器");
    }
}
class B extends A{
    B(){
        super();
        System.out.println("B类无参构造器");
    }
}
class Test06{
    public static void main(String[] args){
        B b = new B();
        //A类显示声明一个有参构造，没有写无参构造，那么A类就没有无参构造了
        //B类显示声明一个无参构造，        
        //B类的无参构造明确写super()，表示调用A类的无参构造
        //编译报错，因为A类没有无参构造
    }
}
```

![](images/image-20200303183542807.png)

情景举例7：

```java
class A{
    A(int a){
        System.out.println("A类有参构造器");
    }
}
class B extends A{
    B(int a){
        super(a);
        System.out.println("B类有参构造器");
    }
}
class Test07{
    public static void main(String[] args){
        B b = new B(10);
        //A类显示声明一个有参构造，没有写无参构造，那么A类就没有无参构造了
        //B类显示声明一个有参构造，        
        //B类的有参构造明确写super(a)，表示调用A类的有参构造
        //会打印“A类有参构造器"和"B类有参构造器"
    }
}
```

情景举例8：

```java
class A{
    A(){
        System.out.println("A类无参构造器");
    }
    A(int a){
        System.out.println("A类有参构造器");
    }
}
class B extends A{
    B(){
        super();//可以省略，调用父类的无参构造
        System.out.println("B类无参构造器");
    }
    B(int a){
        super(a);//调用父类有参构造
        System.out.println("B类有参构造器");
    }
}
class Test8{
    public static void main(String[] args){
        B b1 = new B();
        B b2 = new B(10);
    }
}
```

### 5.3 小结：this与super
**1、this和super的意义**

this：当前对象

+ 在构造器和非静态代码块中，表示正在new的对象
+ 在实例方法中，表示调用当前方法的对象

super：引用父类声明的成员

**2、this和super的使用格式**

+ this
    - this.成员变量：表示当前对象的某个成员变量，而不是局部变量
    - this.成员方法：表示当前对象的某个成员方法，完全可以省略this.
    - this()或this(实参列表)：调用另一个构造器协助当前对象的实例化，只能在构造器首行，只会找本类的构造器，找不到就报错
+ super
    - super.成员变量：表示当前对象的某个成员变量，该成员变量在父类中声明的
    - super.成员方法：表示当前对象的某个成员方法，该成员方法在父类中声明的
    - super()或super(实参列表)：调用父类的构造器协助当前对象的实例化，只能在构造器首行，只会找直接父类的对应构造器，找不到就报错



super 使用例子

```java
public class Test{
    public static void main(String[] args){
        Student s = new Student();

        s.eat();
        s.sleep();
        s.study();

        s.show();

        
    }
}
```



```java
public class Student extends Person{
    
    String school;
    //方法
    public void eat(){
        System.out.println("学生吃饭.....");
    }

    public void sleep(){
        System.out.println("学生睡觉...........");
    }

    public void study(){
        System.out.println("学生认真学习");
    }

    public void show(){
        eat();
        //调用重写的方法

        this.eat();
        //调用本类的方法

        super.eat();
        //调用父类的方法
    }

    public void show1(){
        this.doSport();
        super.doSport();
    }

}
```

```java
public class Person {
    //属性

    String name;
    private int age;
    public void eat(){
        System.out.println("人吃饭");
    }
    public void sleep(){
        System.out.println("人睡觉");
    }
    public void doSport(){
        System.out.println("人运动");
    }
}
```



不加 super 即省略 this

现在本地找，后在父类找



3.1 super调用属性、方法

子类继承父类以后，我们就可以在子类的方法或构造器中，调用父类中声明的属性或方法。(满足封装性的前提下)

如何调用呢?需要使用"super."的结构，表示调用父类的属性或方法。

一般情况下，我们可以考虑省略"super."的结构。但是，如果出现子类重写了父类的方法或子父类中出现了同名的属性时

则必须使用"super."的声明，显式的调用父类被重写的方法或父类中声明的同名的属性。





Super 调用构造器

1. 子类继承父类时，不会继承父类的构造器。只能通过 "super(参数列表)" 的方式调用父类指定的构造器。
2. 规定："super(参数列表)" 必须声明在构造器的首行。
3. 我们前面讲过，在构造器的首行可以使用 "this(参数列表)"，调用本类中重载的构造器。
4. 结合②和③，结论：在构造器的首行，"this(参数列表)" 和 "super(参数列表)" 只能二选一。
5. 如果在子类构造器的首行既没有显示调用 "this(参数列表)"，也没有显式调用 "super(参数列表)"，则子类此构造器默认调用 "super()"，即调用父类中空参数的构造器。
6. 由④和⑤得到结论：子类的任何一个构造器中，要么会调用本类中重载的构造器，要么会调用父类的构造器，只能是这两种情况之一。
7. 由⑥得到：一个类中声明有n个构造器，最多有n-1个构造器中使用了 "this(参数列表)"，则剩下的那个一定使用了 "super(参数列表)"。
8. 我们在通过子类的构造器创建对象时，一定在调用子类构造器的过程中，直接或间接地调用到父类的构造器。
9. 也正因为调用过父类的构造器，我们才会将父类中声明的属性或方法加载到内存中，供子类对象使用。



以下是瞎写的代码

```java
public class Test{
    public static void main(String[] args){
        Student s = new Student();

        s.eat();
        s.sleep();
        s.study();

        System.out.println();

        s.show();

        System.out.println();

        Student s1 = new Student();
        s1.show();
        //调用构造器
        Student s2 = new Student("张三", 18, "男");
        s2.show();




    }
}
```

```java
public class Student extends Person{
    
    String school;
    //方法
    public void eat(){
        System.out.println("学生吃饭.....");
    }

    public void sleep(){
        System.out.println("学生睡觉...........");
    }

    public void study(){
        System.out.println("学生认真学习");
    }

    public void show(){
        eat();
        //调用重写的方法

        this.eat();
        //调用本类的方法

        super.eat();
        //调用父类的方法
    }

    public void show1(){
        this.doSport();
        super.doSport();
    }

    //super调用父类构造器例子
    public Student(){
        super("张三",18);
        System.out.println("Student无参构造器");

    }
    public Student(String name,int age){
        super(name,age);
        System.out.println("Student有2参构造器");
    }
    public Student(String name,int age,String school){
        super(name,age);
        this.school=school;
        System.out.println("Student有3参构造器");
    }


}
```

```java
public class Person {
    //属性

    String name;
    private int age;
    public void eat(){
        System.out.println("人吃饭");
    }
    public void sleep(){
        System.out.println("人睡觉");
    }
    public void doSport(){
        System.out.println("人运动");
    }

    //子类调用父类构造器例子
    public Person(String name,int age){
        this.name = name;
        this.age = age;
        System.out.println("父类1");
    }
    public Person(){
        this.name = "张三";
        this.age = 18;
        System.out.println("父类2");
    }

}
```

就近原则

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1730519278771-212d589a-8c19-42ba-8a86-768f16f519fb.png)





子类的实例化过程涉及到对象的创建和初始化，这个过程遵循特定的顺序和规则。以下是子类实例化过程的详细步骤：

1. **分配内存**：  
在实例化对象之前，Java虚拟机（JVM）首先为新对象分配内存空间。
2. **执行父类的构造器**：  
在子类的构造器执行之前，必须先执行父类的构造器。如果子类的构造器中没有显式地通过 `super` 调用父类的构造器，那么JVM会自动插入一个对父类无参构造器的调用（`super()`）。如果父类没有无参构造器，并且子类没有显式调用一个匹配的父类构造器，那么编译会失败。
3. **初始化父类的成员变量**：  
父类的构造器会初始化父类的成员变量。
4. **执行子类的构造器**：  
父类的构造器执行完毕后，开始执行子类的构造器。子类的构造器可以进一步初始化子类特有的成员变量，或者调用子类中重载的其他构造器（通过 `this` 关键字）。
5. **初始化子类的成员变量**：  
在子类构造器的主体中，子类的成员变量会被初始化。
6. **执行构造代码块**：  
如果有静态代码块（static blocks）和非静态代码块（instance initializers），它们会在成员变量初始化之后、构造器主体之前执行。
7. **执行构造器主体**：  
最后，执行构造器主体中的代码。
8. **对象创建完成**：  
一旦构造器执行完毕，对象就被认为是完全初始化了，可以被使用。

以下是一个简单的Java代码示例，展示了子类实例化的过程：

```java
class Parent {
    {
        // 父类的非静态代码块
        System.out.println("Parent's instance initializer");
    }

    public Parent() {
        // 父类的构造器
        System.out.println("Parent's constructor");
    }

    static {
        // 父类的静态代码块
        System.out.println("Parent's static initializer");
    }
}

class Child extends Parent {
    {
        // 子类的非静态代码块
        System.out.println("Child's instance initializer");
    }

    public Child() {
        // 子类的构造器
        System.out.println("Child's constructor");
    }

    static {
        // 子类的静态代码块
        System.out.println("Child's static initializer");
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Memory allocation for Child object");
        Child child = new Child();
    }
}
```

当运行 `Main` 类的 `main` 方法时，以下是执行的顺序：

1. 输出 "Memory allocation for Child object"（在 `main` 方法中）。
2. 输出 "Parent's static initializer"（父类的静态代码块）。
3. 输出 "Child's static initializer"（子类的静态代码块）。
4. 输出 "Parent's instance initializer"（父类的非静态代码块）。
5. 输出 "Parent's constructor"（父类的构造器）。
6. 输出 "Child's instance initializer"（子类的非静态代码块）。
7. 输出 "Child's constructor"（子类的构造器）。

这个顺序展示了从静态成员初始化到对象完全初始化的整个过程。



1，从结果的角度来看，显示为 类的继承性

当我们创建子类对象后，子类对象就获取了其父类中声明的所有的属性和方法，在权限允许的情况下，可以直接调用





2, 从过程的角度来看

当我们通过子类的构造器创建对象时，子类的构造器一定会直接或间接地调用其父类的构造器，而这个调用过程会一直向上追溯，直到调用了 `Object` 类中的构造器为止。同样地，子类的构造器也会直接或间接地调用其父类的父类的构造器，以此类推。正因为我们调用了子类所有的父类的构造器，所以我们会将这些父类中声明的属性和方法加载到内存中，供子类的对象使用。





## 7. 面向对象特征三：多态性
> 一千个读者眼中有一千个哈姆雷特。
>

### 7.1 多态的形式和体现
#### 7.1.1 对象的多态性
多态性，是面向对象中最重要的概念，在Java中的体现：**对象的多态性：父类的引用指向子类的对象**

格式：（父类类型：指子类继承的父类类型，或者实现的接口类型）

```java
父类类型 变量名 = 子类对象；
```

举例：

```java
Person p = new Student();

Object o = new Person();//Object类型的变量o，指向Person类型的对象

o = new Student(); //Object类型的变量o，指向Student类型的对象
```

对象的多态：在Java中，子类的对象可以替代父类的对象使用。所以，一个引用类型变量可能指向(引用)多种不同类型的对象

#### 7.1.2 多态的理解
Java引用变量有两个类型：`编译时类型`和`运行时类型`。编译时类型由`声明`该变量时使用的类型决定，运行时类型由`实际赋给该变量的对象`决定。简称：**编译 时，看左边；运行时，看右边。**

+ 若编译时类型和运行时类型不一致，就出现了对象的多态性(Polymorphism)
+ 多态情况下，“看左边”：看的是父类的引用（父类中不具备子类特有的方法）  
                    “看右边”：看的是子类的对象（实际运行的是子类重写父类的方法）

多态的使用前提：① 类的继承关系  ② 方法的重写



生活举例

>女朋友:我想养一个宠物。

>孩子:我想要一个玩具。

>老板:张秘书，安排一个技术科的同事，跟我一起下周出差。



#### 7.1.3 举例
```java
package com.atguigu.polymorphism.grammar;

public class Pet {
    private String nickname; //昵称

    public String getNickname() {
        return nickname;
    }

    public void setNickname(String nickname) {
        this.nickname = nickname;
    }

    public void eat(){
        System.out.println(nickname + "吃东西");
    }
}
```

```java
package com.atguigu.polymorphism.grammar;

public class Cat extends Pet {
    //子类重写父类的方法
    @Override
    public void eat() {
        System.out.println("猫咪" + getNickname() + "吃鱼仔");
    }

    //子类扩展的方法
    public void catchMouse() {
        System.out.println("抓老鼠");
    }
}
```

```java
package com.atguigu.polymorphism.grammar;

public class Dog extends Pet {
    //子类重写父类的方法
    @Override
    public void eat() {
        System.out.println("狗子" + getNickname() + "啃骨头");
    }

    //子类扩展的方法
    public void watchHouse() {
        System.out.println("看家");
    }
}
```

**1、方法内局部变量的赋值体现多态**

```java
package com.atguigu.polymorphism.grammar;

public class TestPet {
    public static void main(String[] args) {
        //多态引用
        Pet pet = new Dog();
        pet.setNickname("小白");

        //多态的表现形式
        /*
        编译时看父类：只能调用父类声明的方法，不能调用子类扩展的方法；
        运行时，看“子类”，如果子类重写了方法，一定是执行子类重写的方法体；
         */
        pet.eat();//运行时执行子类Dog重写的方法
//      pet.watchHouse();//不能调用Dog子类扩展的方法

        pet = new Cat();
        pet.setNickname("雪球");
        pet.eat();//运行时执行子类Cat重写的方法
    }
}
```

**2、方法的形参声明体现多态**

```java
package com.atguigu.polymorphism.grammar;

public class Person{
    private Pet pet;
    public void adopt(Pet pet) {//形参是父类类型，实参是子类对象
        this.pet = pet;
    }
    public void feed(){
        pet.eat();//pet实际引用的对象类型不同，执行的eat方法也不同
    }
}
```

```java
package com.atguigu.polymorphism.grammar;

public class TestPerson {
    public static void main(String[] args) {
        Person person = new Person();

        Dog dog = new Dog();
        dog.setNickname("小白");
        person.adopt(dog);//实参是dog子类对象，形参是父类Pet类型
        person.feed();

        Cat cat = new Cat();
        cat.setNickname("雪球");
        person.adopt(cat);//实参是cat子类对象，形参是父类Pet类型
        person.feed();
    }
}
```

**3、方法返回值类型体现多态**

```java
package com.atguigu.polymorphism.grammar;

public class PetShop {
    //返回值类型是父类类型，实际返回的是子类对象
    public Pet sale(String type){
        switch (type){
            case "Dog":
                return new Dog();
            case "Cat":
                return new Cat();
        }
        return null;
    }
}
```

```java
package com.atguigu.polymorphism.grammar;

public class TestPetShop {
    public static void main(String[] args) {
        PetShop shop = new PetShop();

        Pet dog = shop.sale("Dog");
        dog.setNickname("小白");
        dog.eat();

        Pet cat = shop.sale("Cat");
        cat.setNickname("雪球");
        cat.eat();
    }
}
```

### 7.2 为什么需要多态性(polymorphism)？
开发中，有时我们在设计一个数组、或一个成员变量、或一个方法的形参、返回值类型时，无法确定它具体的类型，只能确定它是某个系列的类型。

案例：

（1）声明一个Dog类，包含public void eat()方法，输出“狗啃骨头”

（2）声明一个Cat类，包含public void eat()方法，输出“猫吃鱼仔”

（3）声明一个Person类，功能如下：

+ 包含宠物属性
+ 包含领养宠物方法 public void adopt(宠物类型Pet)
+ 包含喂宠物吃东西的方法 public void feed()，实现为调用宠物对象.eat()方法

```java
public class Dog {
    public void eat(){
        System.out.println("狗啃骨头");
    }
}
```

```java
public class Cat {
    public void eat(){
        System.out.println("猫吃鱼仔");
    }
}
```

```java
public class Person {
    private Dog dog;

    //adopt：领养
    public void adopt(Dog dog){
        this.dog = dog;
    }

    //feed：喂食
    public void feed(){
        if(dog != null){
            dog.eat();
        }
    }
    /*
    问题：
    1、从养狗切换到养猫怎么办？   
        修改代码把Dog修改为养猫？
    2、或者有的人养狗，有的人养猫怎么办？  
    3、要是还有更多其他宠物类型怎么办？
    如果Java不支持多态，那么上面的问题将会非常麻烦，代码维护起来很难，扩展性很差。
    */
}
```

### 7.3 多态的好处和弊端
**好处**：变量引用的子类对象不同，执行的方法就不同，实现动态绑定。代码编写更灵活、功能更强大，可维护性和扩展性更好了。

**弊端**：一个引用类型变量如果声明为父类的类型，但实际引用的是子类对象，那么该变量就不能再访问子类中添加的属性和方法。

```java
Student m = new Student();
m.school = "pku"; 	//合法,Student类有school成员变量
Person e = new Student(); 
e.school = "pku";	//非法,Person类没有school成员变量

// 属性是在编译时确定的，编译时e为Person类型，没有school成员变量，因而编译错误。
```

> 开发中：
>
> 使用父类做方法的形参，是多态使用最多的场合。即使增加了新的子类，方法也无需改变，提高了扩展性，符合开闭原则。
>
> 【开闭原则OCP】
>
> + 对扩展开放，对修改关闭
> + 通俗解释：软件系统中的各种组件，如模块（Modules）、类（Classes）以及功能（Functions）等，应该在不修改现有代码的基础上，引入新功能
>

### 7.4 虚方法调用(Virtual Method Invocation)
在Java中虚方法是指在编译阶段不能确定方法的调用入口地址，在运行阶段才能确定的方法，即可能被重写的方法。

```java
Person e = new Student();
e.getInfo();	//调用Student类的getInfo()方法
```

子类中定义了与父类同名同参数的方法，在多态情况下，将此时父类的方法称为虚方法，父类根据赋给它的不同子类对象，动态调用属于子类的该方法。这样的方法调用在编译期是无法确定的。

举例：

![](images/image-20220324234208997.png)

前提：Person类中定义了welcome()方法，各个子类重写了welcome()。

![](images/image-20220324234214932.png)

执行：多态的情况下，调用对象的welcome()方法，实际执行的是子类重写的方法。

> 拓展：
>
> `静态链接（或早起绑定）`：当一个字节码文件被装载进JVM内部时，如果被调用的目标方法在编译期可知，且运行期保持不变时。这种情况下将调用方法的符号引用转换为直接引用的过程称之为静态链接。那么调用这样的方法，就称为非虚方法调用。比如调用静态方法、私有方法、final方法、父类构造器、本类重载构造器等。
>
> `动态链接（或晚期绑定）`：如果被调用的方法在编译期无法被确定下来，也就是说，只能够在程序运行期将调用方法的符号引用转换为直接引用，由于这种引用转换过程具备动态性，因此也就被称之为动态链接。调用这样的方法，就称为虚方法调用。比如调用重写的方法（针对父类）、实现的方法（针对接口）。
>

### 7.5 成员变量没有多态性
+ 若子类重写了父类方法，就意味着子类里定义的方法彻底覆盖了父类里的同名方法，系统将不可能把父类里的方法转移到子类中。
+ 对于实例变量则不存在这样的现象，即使子类里定义了与父类完全相同的实例变量，这个实例变量依然不可能覆盖父类中定义的实例变量

```java
package com.atguigu.polymorphism.grammar;

public class TestVariable {
    public static void main(String[] args) {
        Base b = new Sub();
        System.out.println(b.a);
        System.out.println(((Sub)b).a);

        Sub s = new Sub();
        System.out.println(s.a);
        System.out.println(((Base)s).a);
    }
}
class Base{
    int a = 1;
}
class Sub extends Base{
    int a = 2;
}
```

### 7.6 向上转型与向下转型
首先，一个对象在new的时候创建是哪个类型的对象，它从头至尾都不会变。即这个对象的运行时类型，本质的类型用于不会变。但是，把这个对象赋值给不同类型的变量时，这些变量的编译时类型却不同。

#### 7.6.1 为什么要类型转换
因为多态，就一定会有把子类对象赋值给父类变量的时候，这个时候，在`编译期间`，就会出现类型转换的现象。

但是，使用父类变量接收了子类对象之后，我们就`不能调用`子类拥有，而父类没有的方法了。这也是多态给我们带来的一点"小麻烦"。所以，想要调用子类特有的方法，必须做类型转换，使得`编译通过`。

+ **向上转型**：当左边的变量的类型（父类） > 右边对象/变量的类型（子类），我们就称为向上转型
    - 此时，编译时按照左边变量的类型处理，就只能调用父类中有的变量和方法，不能调用子类特有的变量和方法了
    - 但是，**运行时，仍然是对象本身的类型**，所以执行的方法是子类重写的方法体。
    - 此时，一定是安全的，而且也是自动完成的
+ **向下转型**：当左边的变量的类型（子类）<右边对象/变量的编译时类型（父类），我们就称为向下转型
    - 此时，编译时按照左边变量的类型处理，就可以调用子类特有的变量和方法了
    - 但是，**运行时，仍然是对象本身的类型**
    - 不是所有通过编译的向下转型都是正确的，可能会发生ClassCastException，为了安全，可以通过isInstanceof关键字进行判断

#### 7.6.2 如何向上或向下转型
向上转型：自动完成

向下转型：（子类类型）父类变量

```java
package com.atguigu.polymorphism.grammar;

public class ClassCastTest {
    public static void main(String[] args) {
        //没有类型转换
        Dog dog = new Dog();//dog的编译时类型和运行时类型都是Dog

        //向上转型
        Pet pet = new Dog();//pet的编译时类型是Pet，运行时类型是Dog
        pet.setNickname("小白");
        pet.eat();//可以调用父类Pet有声明的方法eat，但执行的是子类重写的eat方法体
//        pet.watchHouse();//不能调用父类没有的方法watchHouse

        Dog d = (Dog) pet;
        System.out.println("d.nickname = " + d.getNickname());
        d.eat();//可以调用eat方法
        d.watchHouse();//可以调用子类扩展的方法watchHouse

        Cat c = (Cat) pet;//编译通过，因为从语法检查来说，pet的编译时类型是Pet，Cat是Pet的子类，所以向下转型语法正确
        //这句代码运行报错ClassCastException，因为pet变量的运行时类型是Dog，Dog和Cat之间是没有继承关系的
    }
}
```





//多态性之前的场景:

Person p1=new Person();

Man m1= new Man();

//多态性:

Person p2 = new Man();

//声明人 new 了男人

子类的对象赋给父类的引用



多态性的应用:虚拟方法调用

在多态的场景下，调用方法时。

编译时，认为方法是左边声明的父类的类型的方法(即被重写的方法

执行式，实际执行的是子类重写父类的方法。



多态性前提

要有继承关系

要有方法的重写



多态性适用于方法不适用于属性





多态的弊端?

问题:Person p2=new Man();

针对于创建的对象，在内存中是否加载了Man类中声明的特有的属性和方法?加载了!

问题:能不能直接调用Man中加载的特有的属性和方法呢?不能





6.多态的好处与弊端

6.1 弊端:

在多态的场景下，我们创建了子类的对象，也加载了子类特有的属性和方法。但是由于声明为父类的引用

导致我们没有办法直接调用子类特有的属性和方法。

6.2 好处:

极大的减少了代码的冗余，不需要定义多个重载的方法。





#### 向下转型例子
多态性是面向对象编程的一个重要概念，它允许我们通过父类的引用来调用子类的对象。向下转型（Downcasting）是指将父类类型的引用转换为子类类型的引用。在Java中，向下转型之前通常需要进行类型检查，以确保转型是安全的。

以下是一个多态性向下转型的例子：

```java
class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}

class Dog extends Animal {
    public void makeSound() {
        System.out.println("Woof woof");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // 向上转型，多态
        myAnimal.makeSound(); // 输出 "Woof woof"

        // 向下转型
        if (myAnimal instanceof Dog) {
            Dog myDog = (Dog) myAnimal;
            myDog.makeSound(); // 输出 "Woof woof"
        }
    }
}
```

在这个例子中：

1. `Dog` 类继承自 `Animal` 类。
2. `Animal` 类有一个 `makeSound` 方法，而 `Dog` 类重写了这个方法。
3. 在 `main` 方法中，我们创建了一个 `Dog` 类型的对象，但是将其赋值给了一个 `Animal` 类型的引用 `myAnimal`。这是向上转型，因为子类对象可以被看作是父类类型。
4. 当我们调用 `myAnimal.makeSound()` 时，由于多态性，实际调用的是 `Dog` 类中的 `makeSound` 方法。
5. 然后我们进行了类型检查 `if (myAnimal instanceof Dog)`，以确保 `myAnimal` 引用的对象实际上是 `Dog` 类型或其子类型的实例。
6. 如果类型检查通过，我们将 `myAnimal` 向下转型为 `Dog` 类型，并调用 `Dog` 类的 `makeSound` 方法。

注意：向下转型之前必须进行类型检查，因为如果转型不成功，会抛出 `ClassCastException` 异常。`instanceof` 操作符用于检查一个对象是否是特定类的实例，这在向下转型前是一个安全的做法。



`instanceof` 是Java中的一个一元操作符，用于测试一个对象是否是一个特定类的实例，或者是否与特定类兼容。它返回一个布尔值：如果对象是指定类的实例或者是该类的子类的实例，则返回 `true`；否则返回 `false`。

以下是 `instanceof` 的一些使用细节和规则：

### 基本用法
```java
if (object instanceof ClassType) {
    // 如果object是ClassType或其子类的实例，则为true
}
```

+ `object` 是要检查的对象。
+ `ClassType` 是要检查的类类型。

### 示例
```java
class Animal {}
class Dog extends Animal {}

Animal myAnimal = new Dog();
boolean isDog = myAnimal instanceof Dog; // 返回true
```

在这个例子中，`myAnimal` 是 `Dog` 类的实例，`Dog` 是 `Animal` 类的子类，所以 `myAnimal` 也是 `Animal` 类的实例。因此，`myAnimal instanceof Dog` 返回 `true`。

### 多态和向下转型
`instanceof` 经常与多态和向下转型一起使用。在多态的情况下，可能有一个父类的引用指向子类的对象，`instanceof` 可以用来检查这个引用是否指向特定的子类，以便于进行安全的向下转型。

```java
if (myAnimal instanceof Dog) {
    Dog myDog = (Dog) myAnimal;
    // 现在可以安全地将myAnimal向下转型为Dog类型，并调用Dog类的方法
}
```

### 注意事项
+ `instanceof` 只能检测到类的继承层次结构，它不能检测接口的实现情况。如果需要检查一个类是否实现了特定的接口，可以使用 `Class` 类的 `isAssignableFrom` 方法。
+ `instanceof` 是在运行时检查的，所以它不会在编译时防止错误，而是在运行时提供类型安全。
+ 如果 `object` 是 `null`，`object instanceof ClassType` 的结果是 `false`，这不会引发空指针异常。

`instanceof` 是Java中处理多态和类型检查时的一个非常有用的工具，它帮助开发者在运行时确定对象的实际类型，并根据需要进行适当的类型转换。





#### 7.6.3 instanceof关键字
为了避免ClassCastException的发生，Java提供了 `instanceof` 关键字，给引用变量做类型的校验。如下代码格式：

```java
//检验对象a是否是数据类型A的对象，返回值为boolean型
对象a instanceof 数据类型A 
```

+ 说明：
    - 只要用instanceof判断返回true的，那么强转为该类型就一定是安全的，不会报ClassCastException异常。
    - 如果对象a属于类A的子类B，a instanceof A值也为true。
    - 要求对象a所属的类与类A必须是子类和父类的关系，否则编译错误。

代码：

```java
package com.atguigu.polymorphism.grammar;

public class TestInstanceof {
    public static void main(String[] args) {
        Pet[] pets = new Pet[2];
        pets[0] = new Dog();//多态引用
        pets[0].setNickname("小白");
        pets[1] = new Cat();//多态引用
        pets[1].setNickname("雪球");

        for (int i = 0; i < pets.length; i++) {
            pets[i].eat();

            if(pets[i] instanceof Dog){
                Dog dog = (Dog) pets[i];
                dog.watchHouse();
            }else if(pets[i] instanceof Cat){
                Cat cat = (Cat) pets[i];
                cat.catchMouse();
            }
        }
    }
}
```





强行转换例子

```java
class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}

class Dog extends Animal {
    public void watchDoor() {
        System.out.println("Dog is watching the door");
    }
}

class Cat extends Animal {
    public void catchMouse() {
        System.out.println("Cat is catching a mouse");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal;

        // 假设animal被赋值为Dog或Cat的对象
        animal = new Dog();
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;
            dog.watchDoor();
        } else if (animal instanceof Cat) {
            Cat cat = (Cat) animal;
            cat.catchMouse();
        }

        // 再次改变animal的类型
        animal = new Cat();
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;
            dog.watchDoor();
        } else if (animal instanceof Cat) {
            Cat cat = (Cat) animal;
            cat.catchMouse();
        }
    }
}
```

在这个示例中：

1. `Animal` 是一个基类，`Dog` 和 `Cat` 是继承自 `Animal` 的子类。
2. `Dog` 类有一个 `watchDoor` 方法，`Cat` 类有一个 `catchMouse` 方法。
3. 在 `main` 方法中，我们有一个 `Animal` 类型的引用 `animal`。
4. 我们使用 `instanceof` 操作符来检查 `animal` 是否是 `Dog` 或 `Cat` 的实例。
5. 如果 `animal` 是 `Dog` 的实例，我们将其向下转型为 `Dog` 类型，并调用 `watchDoor` 方法。
6. 如果 `animal` 不是 `Dog` 的实例，我们再检查它是否是 `Cat` 的实例，如果是，则将其向下转型为 `Cat` 类型，并调用 `catchMouse` 方法。

这样，根据 `animal` 的实际类型，我们可以调用相应的方法。











### 7.7 练习
**练习1：笔试&面试**

题目1：继承成员变量和继承方法的区别

```java
class Base {
    int count = 10;
    public void display() {
        System.out.println(this.count);
    }
}

class Sub extends Base {
    int count = 20;
    public void display() {
        System.out.println(this.count);
    }
}

public class FieldMethodTest {
    public static void main(String[] args){
        Sub s = new Sub();
        System.out.println(s.count);
        s.display();
        Base b = s;
        System.out.println(b == s);
        System.out.println(b.count);
        b.display();
    }
}

```

题目2：

```java
//考查多态的笔试题目：
public class InterviewTest1 {

    public static void main(String[] args) {
        Base base = new Sub();
        base.add(1, 2, 3);

//		Sub s = (Sub)base;
//		s.add(1,2,3);
    }
}

class Base {
    public void add(int a, int... arr) {
        System.out.println("base");
    }
}

class Sub extends Base {

    public void add(int a, int[] arr) {
        System.out.println("sub_1");
    }

//	public void add(int a, int b, int c) {
//		System.out.println("sub_2");
//	}

}

```

题目3：

```java
//getXxx()和setXxx()声明在哪个类中，内部操作的属性就是哪个类里的。
public class InterviewTest2 {
    public static void main(String[] args) {
        Father f = new Father();
        Son s = new Son();
        System.out.println(f.getInfo());//atguigu
        System.out.println(s.getInfo());//尚硅谷
        s.test();//尚硅谷  atguigu
        System.out.println("-----------------");
        s.setInfo("大硅谷");
        System.out.println(f.getInfo());//atguigu
        System.out.println(s.getInfo());//大硅谷
        s.test();//大硅谷  atguigu
    }
}

class Father {
    private String info = "atguigu";

    public void setInfo(String info) {
        this.info = info;
    }

    public String getInfo() {
        return info;
    }
}

class Son extends Father {
    private String info = "尚硅谷";
    
    public void setInfo(String info) {
        this.info = info;
    }

    public String getInfo() {
        return info;
    }
    
    public void test() {
        System.out.println(this.getInfo());
        System.out.println(super.getInfo());
    }
}
```

题目4：多态是编译时行为还是运行时行为？

```java
//证明如下：
class Animal  {
    protected void eat() {
        System.out.println("animal eat food");
    }
}

class Cat  extends Animal  {
    protected void eat() {
        System.out.println("cat eat fish");
    }
}

class Dog  extends Animal  {
    public void eat() {
        System.out.println("Dog eat bone");
    }
}

class Sheep  extends Animal  {
    public void eat() {
        System.out.println("Sheep eat grass");
    }
}

public class InterviewTest {
    public static Animal  getInstance(int key) {
        switch (key) {
        case 0:
            return new Cat ();
        case 1:
            return new Dog ();
        default:
            return new Sheep ();
        }

    }

    public static void main(String[] args) {
        int key = new Random().nextInt(3);
        System.out.println(key);

        Animal  animal = getInstance(key);
        animal.eat(); 
    }
}
```

**练习2：**

```java
class Person {
    protected String name="person";
    protected int age=50;
    public String getInfo() {
              return "Name: "+ name + "\n" +"age: "+ age;
    }
}
class Student extends Person {
    protected String school="pku";
    public String getInfo() {
                return  "Name: "+ name + "\nage: "+ age 
              + "\nschool: "+ school;
    }	
}
class Graduate extends Student{
    public String major="IT";
    public String getInfo()
    {
        return  "Name: "+ name + "\nage: "+ age 
              + "\nschool: "+ school+"\nmajor:"+major;
    }
}

```

建立InstanceTest 类，在类中定义方法method(Person e);  
在method中:  
(1)根据e的类型调用相应类的getInfo()方法。  
(2)根据e的类型执行：  
如果e为Person类的对象，输出：  
“a person”;  
如果e为Student类的对象，输出：  
“a student”  
“a person ”   
如果e为Graduate类的对象，输出：   
“a graduated student”  
“a student”  
“a person”

**练习3**：定义三个类，父类GeometricObject代表几何形状，子类Circle代表圆形，MyRectangle代表矩形。定义一个测试类GeometricTest，编写equalsArea方法测试两个对象的面积是否相等（注意方法的参数类型，利用动态绑定技术），编写displayGeometricObject方法显示对象的面积（注意方法的参数类型，利用动态绑定技术）。

##  Object 类


#### 默认的父类 
Java 中声明的类，如果没有显示的声明其父类时，则默认继承 java.lang.Object



任何一个Java类(除0bject类)都直接或间接的继承于0bject类

Object类称为java类的根父类



#### Object类中声明的结构(属性、方法等)就具有通用性
> 0bject类中没有声明属性

> 0bject类提供了一个空参的构造器

>重点关注:0bject类中声明的方法



#### 方法
重点方法 equals() toString()

了解方法 clone() finalsize()

目前不需要关注 getClass() hashCode()

notifyAll() wait() wait(xx) wait(xx,yy)



clone 复制的是内容不是地址，如果使用==判断结果为 false

其它：finalsize()调用时出现的划线表示为过时（JDK8 中可用，从 9 开始），不建议使用



#### 面试题 final finally finalize 的区别


<font style="background-color:#FCE75A;">在Java编程语言中，</font>`<font style="background-color:#FCE75A;">final</font>`<font style="background-color:#FCE75A;">、</font>`<font style="background-color:#FCE75A;">finally</font>`<font style="background-color:#FCE75A;">和</font>`<font style="background-color:#FCE75A;">finalize()</font>`<font style="background-color:#FCE75A;">是三个完全不同的概念，它们各自有不同的用途和含义：</font>

1. **<font style="background-color:#FCE75A;">final关键字</font>**<font style="background-color:#FCE75A;">：</font>
    - **<font style="background-color:#FCE75A;">变量</font>**<font style="background-color:#FCE75A;">：当用</font>`<font style="background-color:#FCE75A;">final</font>`<font style="background-color:#FCE75A;">修饰一个变量时，表示这个变量的值一旦被初始化后就不能被改变。例如，</font>`<font style="background-color:#FCE75A;">final int number = 10;</font>`<font style="background-color:#FCE75A;">，</font>`<font style="background-color:#FCE75A;">number</font>`<font style="background-color:#FCE75A;">的值就不能被修改。</font>
    - **<font style="background-color:#FCE75A;">方法</font>**<font style="background-color:#FCE75A;">：当用</font>`<font style="background-color:#FCE75A;">final</font>`<font style="background-color:#FCE75A;">修饰一个方法时，表示这个方法不能被子类重写。</font>
    - **<font style="background-color:#FCE75A;">类</font>**<font style="background-color:#FCE75A;">：当用</font>`<font style="background-color:#FCE75A;">final</font>`<font style="background-color:#FCE75A;">修饰一个类时，表示这个类不能被继承。</font>
2. **<font style="background-color:#FCE75A;">finally块</font>**<font style="background-color:#FCE75A;">：</font>
    - `<font style="background-color:#FCE75A;">finally</font>`<font style="background-color:#FCE75A;">是Java异常处理结构的一部分，与</font>`<font style="background-color:#FCE75A;">try</font>`<font style="background-color:#FCE75A;">和</font>`<font style="background-color:#FCE75A;">catch</font>`<font style="background-color:#FCE75A;">一起使用。它是一个代码块，位于</font>`<font style="background-color:#FCE75A;">try</font>`<font style="background-color:#FCE75A;">和</font>`<font style="background-color:#FCE75A;">catch</font>`<font style="background-color:#FCE75A;">块之后，用于执行清理工作，比如关闭文件流、释放数据库连接等。无论是否发生异常，</font>`<font style="background-color:#FCE75A;">finally</font>`<font style="background-color:#FCE75A;">块中的代码都会被执行。</font>
3. **<font style="background-color:#FCE75A;">finalize()方法</font>**<font style="background-color:#FCE75A;">：</font>
    - `<font style="background-color:#FCE75A;">finalize()</font>`<font style="background-color:#FCE75A;">是一个在</font>`<font style="background-color:#FCE75A;">java.lang.Object</font>`<font style="background-color:#FCE75A;">类中定义的方法，Java虚拟机（JVM）在对象被垃圾回收之前调用这个方法。这个方法可以被子类重写，用于在对象被回收前执行一些清理工作。然而，由于垃圾回收机制的不确定性，</font>`<font style="background-color:#FCE75A;">finalize()</font>`<font style="background-color:#FCE75A;">方法的调用时机是不可预测的，因此它的使用并不推荐，更推荐使用</font>`<font style="background-color:#FCE75A;">try-with-resources</font>`<font style="background-color:#FCE75A;">语句或自动资源管理来管理资源。</font>

<font style="background-color:#FCE75A;">总结来说，</font>`<font style="background-color:#FCE75A;">final</font>`<font style="background-color:#FCE75A;">用于声明不可变的对象、方法和类，</font>`<font style="background-color:#FCE75A;">finally</font>`<font style="background-color:#FCE75A;">用于异常处理中的资源清理，而</font>`<font style="background-color:#FCE75A;">finalize()</font>`<font style="background-color:#FCE75A;">是一个对象被垃圾回收前调用的方法，用于资源释放和清理工作。</font>

### 如何理解根父类
类 `java.lang.Object`是类层次结构的根类，即所有其它类的父类。每个类都使用 `Object` 作为超类。

+ Object类型的变量与除Object以外的任意引用数据类型的对象都存在多态引用

```java
method(Object obj){…} //可以接收任何类作为其参数

Person o = new Person();  
method(o);

```

+ 所有对象（包括数组）都实现这个类的方法。
+ 如果一个类没有特别指定父类，那么默认则继承自Object类。例如：

```java
public class Person {
    ...
}
//等价于：
public class Person extends Object {
    ...
}
```

### Object类的方法
根据JDK源代码及Object类的API文档，Object类当中包含的方法有11个。这里我们主要关注其中的6个：

#### 1、(重点)equals()


equals 的适用性：任何引用类型都能使用



**equals 重写的例子**

```java
public class UserTest {

    public static void main(String[] args) {
        User user = new User("adouzi", 18);
        User user2 = new User("adouzi", 18);

        System.out.println(user.equals(user2));
        // 输出结果为false

        /*
         * public boolean equals(Object obj) {
         * return (this == obj);
         * }
         */

        String str1 = new String("adouzi");
        String str2 = new String("adouzi");

        System.out.println(str1.equals(str2));
        // 输出结果为true

        /*
         * 
         * public boolean equals(Object anObject) {
         * if (this == anObject) {
         * return true;
         * }
         * return (anObject instanceof String aString)
         * && (!COMPACT_STRINGS || this.coder == aString.coder)
         * && StringLatin1.equals(value, aString.value);
         * }
         */

    }
}

class User {
    String name;
    int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

}
```

**我们使用 ctrl 键来看看 java.lang.Object 类中 equals()的定义**

```java
public boolean equals(Object obj) {
        return (this == obj);
}
```

`<font style="color:rgb(6, 6, 7);">this == obj</font>`<font style="color:rgb(6, 6, 7);">是一个比较操作，它检查当前对象的内存地址是否与传入参数对象的内存地址相同。如果相同，意味着它们是同一个对象，因此返回</font>`<font style="color:rgb(6, 6, 7);">true</font>`<font style="color:rgb(6, 6, 7);">；如果不同，意味着它们是不同的对象，因此返回</font>`<font style="color:rgb(6, 6, 7);">false</font>`<font style="color:rgb(6, 6, 7);">。</font>

<font style="color:rgb(6, 6, 7);"></font>

```java
String str1 = new String("adouzi");
String str2 = new String("adouzi");

System.out.println(str1.equals(str2));
         //输出结果为true
```

<font style="color:rgb(6, 6, 7);"></font>

```java
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        return (anObject instanceof String aString)
                && (!COMPACT_STRINGS || this.coder == aString.coder)
                && StringLatin1.equals(value, aString.value);
    }
```

 子类使用说明:

自定义的类在没有重写0bject中equals()方法的情况下，调用的就是0bject类中声明的equals()，比较两个对象的引用地址是否相同。(或比较两个对象是否指向了堆空间中的同一个对象实体)

对于像String、File、Date和包装类等，它们都重写了0bject类中的equals()方法，用于比较两个对象的实体内容是否相等。



重写 equals

```java
//重写equals方法
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj instanceof User) {
            User user = (User) obj;
            return this.name.equals(user.name);
        }
        return false;
        
    }
```

示例代码：

```java
public class UserTest {

    public static void main(String[] args) {
        User user = new User("adouzi", 18);
        User user2 = new User("adouzi", 18);

        System.out.println(user.equals(user2));
        // 输出结果为false
        //重写后输出结果为true

        /*
         * public boolean equals(Object obj) {
         * return (this == obj);
         * }
         */

        String str1 = new String("adouzi");
        String str2 = new String("adouzi");

        System.out.println(str1.equals(str2));
        // 输出结果为true

        /*
         * 
         * public boolean equals(Object anObject) {
         * if (this == anObject) {
         * return true;
         * }
         * return (anObject instanceof String aString)
         * && (!COMPACT_STRINGS || this.coder == aString.coder)
         * && StringLatin1.equals(value, aString.value);
         * }
         */

    }
}

class User {
    String name;
    int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    //重写equals方法
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj instanceof User) {
            User user = (User) obj;
            return this.name.equals(user.name);
        }
        return false;
        
    }

}
```

输出为 

> true
>
> true
>



在 idea 中能自动重写，使用 alt insert



开发中使用说明

在实际开发中，针对于自定义的类，常常会判断两个对象是否 equals() 而此时主要是判断两个对象的属性是否相等

所以我们要重写 equals()方法（推荐使用 idea 自动生成 手动实现比较麻烦）



**面试 区分== 和 equals()**

<font style="background-color:#FCE75A;">在Java中，</font>`<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;"> 和 </font>`<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 是两个用于比较对象的运算符和方法，但它们在比较对象时的行为和用途有所不同：</font>

1. `<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;">（双等号）：</font>
    - `<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;"> 是一个运算符，用于比较两个引用是否指向同一个对象（即它们是否具有相同的内存地址）。</font>
    - <font style="background-color:#FCE75A;">对于基本数据类型（如int、double等），</font>`<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;"> 比较的是值是否相等。</font>
    - <font style="background-color:#FCE75A;">对于对象引用，</font>`<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;"> 比较的是两个引用是否指向堆内存中的同一个对象实例。</font>
    - <font style="background-color:#FCE75A;">示例：</font>

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

System.out.println(s1 == s2); // true，因为s1和s2指向JVM字符串常量池中的同一个对象
System.out.println(s1 == s3); // false，因为s1指向字符串常量池中的对象，而s3指向堆中的新对象
```

2. `<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 方法：</font>
    - `<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 是一个方法，定义在</font>`<font style="background-color:#FCE75A;">Object</font>`<font style="background-color:#FCE75A;">类中，用于比较对象的内容是否相等。</font>
    - <font style="background-color:#FCE75A;">默认情况下，</font>`<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 方法的行为与</font>`<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;">相同，即比较对象的内存地址。</font>
    - <font style="background-color:#FCE75A;">但是，</font>`<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 方法可以被重写，以提供更复杂的比较逻辑，比如比较对象的属性值是否相等。</font>
    - <font style="background-color:#FCE75A;">对于字符串（</font>`<font style="background-color:#FCE75A;">String</font>`<font style="background-color:#FCE75A;">类）和其他一些类（如</font>`<font style="background-color:#FCE75A;">Integer</font>`<font style="background-color:#FCE75A;">、</font>`<font style="background-color:#FCE75A;">Double</font>`<font style="background-color:#FCE75A;">等），</font>`<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 方法已经被重写，以比较对象的内容。</font>
    - <font style="background-color:#FCE75A;">示例：</font>

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

System.out.println(s1.equals(s2)); // true，因为equals()比较的是字符串的内容
System.out.println(s1.equals(s3)); // true，因为equals()比较的是字符串的内容
```

<font style="background-color:#FCE75A;">区分</font>`<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;">和</font>`<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;">的关键点在于：</font>

+ `<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;"> 比较的是对象的引用是否相同，即是否指向内存中的同一个位置。</font>
+ `<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;"> 默认比较的是对象的引用，但可以被重写来比较对象的属性或状态是否相等。</font>

<font style="background-color:#FCE75A;">因此，当你需要比较两个对象是否逻辑上相等（即它们的属性值是否相同），你应该使用</font>`<font style="background-color:#FCE75A;">equals()</font>`<font style="background-color:#FCE75A;">方法。而当你需要检查两个引用是否指向同一个对象时，你应该使用</font>`<font style="background-color:#FCE75A;">==</font>`<font style="background-color:#FCE75A;">运算符。</font>





**= =：** 

+ 基本类型比较值:只要两个变量的值相等，即为true。

```java
int a=5; 
if(a==6){…}
```

+ 引用类型比较引用(是否指向同一个对象)：只有指向同一个对象时，==才返回true。

```java
Person p1=new Person();  	    
Person p2=new Person();
if (p1==p2){…}
```

    - 用“==”进行比较时，符号两边的`数据类型必须兼容`(可自动转换的基本数据类型除外)，否则编译出错

**equals()：**所有类都继承了Object，也就获得了equals()方法。还可以重写。

+ 只能比较引用类型，Object类源码中equals()的作用与“==”相同：比较是否指向同一个对象。	 
+ 格式:obj1.equals(obj2)
+ 特例：当用equals()方法进行比较时，对类File、String、Date及包装类（Wrapper Class）来说，是比较类型及内容而不考虑引用的是否是同一个对象；
    - 原因：在这些类中重写了Object类的equals()方法。
+ 当自定义使用equals()时，可以重写。用于比较两个对象的“内容”是否都相等
+ 重写equals()方法的原则
    - `对称性`：如果x.equals(y)返回是“true”，那么y.equals(x)也应该返回是“true”。
    - `自反性`：x.equals(x)必须返回是“true”。
    - `传递性`：如果x.equals(y)返回是“true”，而且y.equals(z)返回是“true”，那么z.equals(x)也应该返回是“true”。
    - `一致性`：如果x.equals(y)返回是“true”，只要x和y内容一直不变，不管你重复x.equals(y)多少次，返回都是“true”。
    - 任何情况下，x.equals(null)，永远返回是“false”；    x.equals(和x不同类型的对象)永远返回是“false”。
+ 重写举例：

```java
class User{
    private String host;
    private String username;
    private String password;
    public User(String host, String username, String password) {
        super();
        this.host = host;
        this.username = username;
        this.password = password;
    }
    public User() {
        super();
    }
    public String getHost() {
        return host;
    }
    public void setHost(String host) {
        this.host = host;
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
    @Override
    public String toString() {
        return "User [host=" + host + ", username=" + username + ", password=" + password + "]";
    }
    @Override
    public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        User other = (User) obj;
        if (host == null) {
            if (other.host != null)
                return false;
        } else if (!host.equals(other.host))
            return false;
        if (password == null) {
            if (other.password != null)
                return false;
        } else if (!password.equals(other.password))
            return false;
        if (username == null) {
            if (other.username != null)
                return false;
        } else if (!username.equals(other.username))
            return false;
        return true;
    }
    
}
```

**面试题：**==和equals的区别

> 从我面试的反馈，85%的求职者“理直气壮”的回答错误…
>

+ == 既可以比较基本类型也可以比较引用类型。对于基本类型就是比较值，对于引用类型就是比较内存地址
+ equals的话，它是属于java.lang.Object类里面的方法，如果该方法没有被重写过默认也是==;我们可以看到String等类的equals方法是被重写过的，而且String类在日常开发中用的比较多，久而久之，形成了equals是比较值的错误观点。
+ 具体要看自定义类里有没有重写Object的equals方法来判断。
+ 通常情况下，重写equals方法，会比较类中的相应属性是否都相等。

**练习1：**

```java
int it = 65;
float fl = 65.0f;
System.out.println(“65和65.0f是否相等？” + (it == fl)); //

char ch1 = 'A'; char ch2 = 12;
System.out.println("65和'A'是否相等？" + (it == ch1));//
System.out.println("12和ch2是否相等？" + (12 == ch2));//

String str1 = new String("hello");
String str2 = new String("hello");
System.out.println("str1和str2是否相等？"+ (str1 == str2));//

System.out.println("str1是否equals str2？"+(str1.equals(str2)));//

System.out.println(“hello” == new java.util.Date()); //

```

**练习2：**

编写Order类，有int型的orderId，String型的orderName，相应的getter()和setter()方法，两个参数的构造器，重写父类的equals()方法：public boolean equals(Object obj)，并判断测试类中创建的两个对象是否相等。

**练习3：**

请根据以下代码自行定义能满足需要的MyDate类,在MyDate类中覆盖equals方法，使其判断当两个MyDate类型对象的年月日都相同时，结果为true，否则为false。  public boolean equals(Object o)

```java
public class EqualsTest {
    public static void main(String[] args) {
        MyDate m1 = new MyDate(14, 3, 1976);
        MyDate m2 = new MyDate(14, 3, 1976);
        if (m1 == m2) {
            System.out.println("m1==m2");
        } else {
            System.out.println("m1!=m2"); // m1 != m2
        }

        if (m1.equals(m2)) {
            System.out.println("m1 is equal to m2");// m1 is equal to m2
        } else {
            System.out.println("m1 is not equal to m2");
        }
    }
}

```







#### 2、(重点)toString()


0bject类中tostring()的定义:

public string tostring(){

return getclass().getName()+ "@"+ Integer.toHexString(hashCode());

```java
public class ToStringTest {
    public static void main(String[] args) {
        User user = new User("张三", 20);
        System.out.println(user.toString());
    }
    
}

class User {
    String name;
    int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // @Override
    // public String toString() {
    //     return "User{name='" + name + "', age=" + age + "}";
    // }
}
```

> User@5caf905d
>



开发中的使用场景

>平时我们在调用System.out.println()打印对象引用变量时，其实就调用了对象的toString()

子类使用说明:

自定义的类，在没有重写0bject类的tostring()的情况下，默认返回的是当前对象的地址值。

像String、File、Date或包装类等0bject的子类，它们都重写了0bject类的toString()，在调用tostring()时返回当前对象的实体内容。

开发中使用说明:

>习惯上，开发中对于自定义的类在调用toString()时，也希望显示其对象的实体内容，而非地址值。这时候，就需要重写0bject

类中的tostring().





方法签名：public String toString()

① 默认情况下，toString()返回的是“对象的运行时类型 @ 对象的hashCode值的十六进制形式"

② 在进行String与其它类型数据的连接操作时，自动调用toString()方法

```java
Date now=new Date();
System.out.println(“now=”+now);  //相当于
System.out.println(“now=”+now.toString()); 
```

③ 如果我们直接System.out.println(对象)，默认会自动调用这个对象的toString()

> 因为Java的引用数据类型的变量中存储的实际上时对象的内存地址，但是Java对程序员隐藏内存地址信息，所以不能直接将内存地址显示出来，所以当你打印对象时，JVM帮你调用了对象的toString()。
>

④ 可以根据需要在用户自定义类型中重写toString()方法  
    如String 类重写了toString()方法，返回字符串的值。

```java
s1="hello";
System.out.println(s1);//相当于System.out.println(s1.toString());
```

例如自定义的Person类：

```java
public class Person {  
    private String name;
    private int age;

    @Override
    public String toString() {
        return "Person{" + "name='" + name + '\'' + ", age=" + age + '}';
    }
}
```

**练习**：定义两个类，父类GeometricObject代表几何形状，子类Circle代表圆形。

#### 3、clone()
```java
//Object类的clone()的使用
public class CloneTest {
    public static void main(String[] args) {
        Animal a1 = new Animal("花花");
        try {
            Animal a2 = (Animal) a1.clone();
            System.out.println("原始对象：" + a1);
            a2.setName("毛毛");
            System.out.println("clone之后的对象：" + a2);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}

class Animal implements Cloneable{
    private String name;

    public Animal() {
        super();
    }

    public Animal(String name) {
        super();
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Animal [name=" + name + "]";
    }
    
    @Override
    protected Object clone() throws CloneNotSupportedException {
        // TODO Auto-generated method stub
        return super.clone();
    }
    
}
```



#### 不那么重要的一些方法
#### 4、finalize()
+ 当对象被回收时，系统自动调用该对象的 finalize() 方法。（不是垃圾回收器调用的，是本类对象调用的）
    - 永远不要主动调用某个对象的finalize方法，应该交给垃圾回收机制调用。
+ 什么时候被回收：当某个对象没有任何引用时，JVM就认为这个对象是垃圾对象，就会在之后不确定的时间使用垃圾回收机制来销毁该对象，在销毁该对象前，会先调用 finalize()方法。 
+ 子类可以重写该方法，目的是在对象被清理之前执行必要的清理操作。比如，在方法内断开相关连接资源。
    - 如果重写该方法，让一个新的引用变量重新引用该对象，则会重新激活对象。
+ 在JDK 9中此方法已经被`标记为过时`的。

```java
public class FinalizeTest {
    public static void main(String[] args) {
        Person p = new Person("Peter", 12);
        System.out.println(p);
        p = null;//此时对象实体就是垃圾对象，等待被回收。但时间不确定。
        System.gc();//强制性释放空间
    }
}

class Person{
    private String name;
    private int age;

    public Person(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    //子类重写此方法，可在释放对象前进行某些操作
    @Override
    protected void finalize() throws Throwable {
        System.out.println("对象被释放--->" + this);
    }
    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
    
}
```

#### 5、getClass()
public final Class<?> getClass()：获取对象的运行时类型

> 因为Java有多态现象，所以一个引用数据类型的变量的编译时类型与运行时类型可能不一致，因此如果需要查看这个变量实际指向的对象的类型，需要用getClass()方法
>

```java
public static void main(String[] args) {
    Object obj = new Person();
    System.out.println(obj.getClass());//运行时类型
}
```

结果：

```java
class com.atguigu.java.Person
```

#### 6、hashCode()
public int hashCode()：返回每个对象的hash值。(后续在集合框架章节重点讲解)

```java
public static void main(String[] args) {
    System.out.println("AA".hashCode());//2080
    System.out.println("BB".hashCode());//2112
}
```

### 8.3 native关键字的理解
使用native关键字说明这个方法是原生函数，也就是这个方法是用`C/C++`等非Java语言实现的，并且`被编译成了DLL`，由Java去调用。

+ 本地方法是有方法体的，用c语言编写。由于本地方法的方法体源码没有对我们开源，所以我们看不到方法体
+ 在Java中定义一个native方法时，并不提供实现体。

**1. 为什么要用native方法**

Java使用起来非常方便，然而有些层次的任务用java实现起来不容易，或者我们对程序的效率很在意时，例如：Java需要与一些底层操作系统或某些硬件交换信息时的情况。native方法正是这样一种交流机制：它为我们提供了一个非常简洁的接口，而且我们无需去了解Java应用之外的繁琐的细节。

**2. native声明的方法，对于调用者，可以当做和其他Java方法一样使用**

native method的存在并不会对其他类调用这些本地方法产生任何影响，实际上调用这些方法的其他类甚至不知道它所调用的是一个本地方法。JVM将控制调用本地方法的所有细节。










