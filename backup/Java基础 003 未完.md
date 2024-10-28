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

