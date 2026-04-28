

# AOP 面向切面编程


### AOP简介
#### 什么是AOP？
AOP（Aspect-Oriented Programming，面向切面编程）是一种编程范式，旨在通过分离横切关注点（cross-cutting concerns）来提高代码的模块化。横切关注点是指那些在多个模块中都会涉及的功能，如日志记录、安全检查、事务管理等。AOP通过将这些关注点从业务逻辑中分离出来，使得代码更加清晰、可维护。

#### 为什么需要AOP？
在传统的面向对象编程（OOP）中，横切关注点往往会散布在多个类中，导致代码重复和耦合度高。AOP通过将这些关注点集中管理，减少了代码的重复，提高了代码的可维护性和可读性。

#### AOP的核心概念
1. **切面（Aspect）**：切面是模块化的横切关注点。它可以看作是一个类，包含了横切关注点的具体实现。
2. **连接点（Join Point）**：连接点是程序执行的某个特定点，如方法调用或异常抛出。AOP框架允许在这些点上插入切面代码。
3. **通知（Advice）**：通知是切面在连接点上执行的代码。通知有多种类型，如前置通知、后置通知、环绕通知等。
4. **切入点（Pointcut）**：切入点定义了在哪些连接点上应用切面。它通常通过表达式来指定。
5. **织入（Weaving）**：织入是将切面代码应用到目标对象的过程。织入可以在编译时、类加载时或运行时进行。

#### AOP的实现方式
1. **编译时织入**：在编译阶段将切面代码织入到目标类中。这种方式需要特殊的编译器支持。
2. **类加载时织入**：在类加载阶段通过类加载器将切面代码织入到目标类中。
3. **运行时织入**：在运行时通过代理模式将切面代码织入到目标对象中。Spring AOP主要采用这种方式。

#### AOP的应用场景
1. **日志记录**：在方法调用前后记录日志。
2. **性能监控**：监控方法的执行时间。
3. **安全检查**：在方法调用前进行权限验证。
4. **事务管理**：在方法调用前后管理事务。



## 代理模式简介（不要求掌握）
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733073361441-72423443-fb10-4271-8d41-54d8ccc52a05.png)

#### 什么是代理模式？
代理模式（Proxy Pattern）是一种结构型设计模式，它为其他对象提供一种代理以控制对这个对象的访问。代理模式可以在不改变原始对象的情况下，通过代理对象来控制对原始对象的访问。

#### 代理模式的类型
1. **静态代理**：在编译时由程序员创建代理类，代理类和目标类实现相同的接口。
2. **动态代理**：在运行时由JDK或CGLIB库动态生成代理类，代理类和目标类实现相同的接口或继承自目标类。

#### 代理模式的应用场景
1. **远程代理**：为一个对象在不同地址空间提供局部代表。这样可以隐藏一个对象存在于不同地址空间的事实。
2. **虚拟代理**：根据需要创建开销很大的对象。通过代理对象来控制对实际对象的访问，只有在需要时才创建实际对象。
3. **保护代理**：控制对原始对象的访问。保护代理用于对象应该有不同的访问权限时。
4. **智能引用代理**：在访问对象时执行一些附加操作，如计算一个对象被引用的次数。

#### 代理模式的优点
1. **职责清晰**：真实角色实现实际的业务逻辑，不用关心其他非本职的事务，通过代理类完成一件事务，附带的结果就是编程简洁清晰。
2. **高扩展性**：真实角色专注于业务逻辑，代理类负责其他事务，符合开闭原则。
3. **智能化**：代理类可以在执行真实角色的操作时，附加其他操作，如日志记录、性能监控等。

#### 代理模式的示例代码
以下是一个简单的静态代理示例：

```java
// 接口
public interface Subject {
    void request();
}

// 真实对象
public class RealSubject implements Subject {
    @Override
    public void request() {
        System.out.println("RealSubject: Handling request.");
    }
}

// 代理对象
public class Proxy implements Subject {
    private RealSubject realSubject;

    @Override
    public void request() {
        if (realSubject == null) {
            realSubject = new RealSubject();
        }
        System.out.println("Proxy: Logging request.");
        realSubject.request();
    }
}

// 客户端代码
public class Client {
    public static void main(String[] args) {
        Subject proxy = new Proxy();
        proxy.request();
    }
}
```

在这个示例中，`Proxy`类控制对`RealSubject`对象的访问，并在调用`request`方法时添加了日志记录功能。



#### 两种动态代理方式区别
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733073985528-71b1f8ba-7696-433a-83e5-cd17723f0d66.png)

+ JDK原生动态代理 拜把子 不能继承（必须要有接口）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733074163319-070cc25d-8268-4c1a-8027-36421b500896.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733074250700-52c2a8ad-602f-4406-b07a-b7744c265a49.png)



+ Cglib（三方 Spring提供的） 认干爹 可以继承

> cglib是spring核心的一部份，使用的时候不用额外导包
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733074273102-7a884b5a-7f4a-4ea9-94cb-2a6560cf9329.png)





### AOP其实就是对动态代理的简化
AOP 面向切面编程 可以说是 OOP 面向对象编程的一种完善

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733074787549-cffd3c7f-b9c3-4013-b9e7-99856d34db6b.png)

一般用于非核心业务 如 日志 权限管理等

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733075226302-f8d15a1a-3604-4f52-90b4-eb1877db9d10.png)







#### 思维导图
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733075431305-07804fdc-e828-4332-a228-065ae9db25b1.png)



### AOP基于注解方式的实现细节


Spring AOP会自动选择使用动态代理或者cglib

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733128735101-921ec2ee-8154-453f-97d1-6eb90cb61909.png)

#### 流程图
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733128953791-dba28dee-d02b-4687-a677-406eccfbe186.png)



### 例子
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733129407651-d823eb62-d790-4a1d-9289-d4e5f965d230.png)

+ 加入日志功能（简单示例）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733129374598-d1fa7317-71c2-448a-9452-82d4a7e5570f.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733129453801-7d9cc8eb-b244-4de3-8587-449a5d3c2eb5.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733129507665-a8db2ac8-d86a-4ced-944b-daa006d3ddeb.png)

+ 示例

 1.定义四个方法

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733129747090-87653432-8088-40d5-bad8-597064ff40af.png)



> TODO：增强方法中获取信息
>
> 1.全部增强方法中，获取目标方法的信息（方法名，参数，访问修饰符，所属类的信息...）
>
> （JointPoint jointPoint）
>
> joinpoint 包含目标方法的信息
>
> 2.返回的结果 - @AfterReturning
>
> （Object result）result接收返回结果
>
> @AfterReturing(value = "execution(* com.impl.*.*((..))",returing = "形参")
>
> 3.异常的信息 - @AfterThrowing
>
> (Throwable t)t接收异常信息
>
> @AfterThrowing(value = "execution(* com..iml.*.*(..))",throwing="形参")
>

#### 获取目标信息
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733130229448-f8240301-13a7-4922-a6c0-f99883902669.png)

> 添加JoinPoint即连接点即可获取目标方法的信息
>

#### 返回结果
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733130267778-69723f09-4887-4678-abcc-009ae3214e94.png)

#### 异常
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733130450792-6f384816-f845-48a2-84d8-39a8c0898d40.png)





### 切点表达式语法
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733130698748-77ba76a0-30c4-4cca-af1a-0d357c47d764.png)





### Spring AOP 切点表达式语法


#### 什么是切点表达式？
切点表达式（Pointcut Expression）用于定义在哪些连接点（Join Point）上应用切面（Aspect）。它通过匹配方法签名、注解等方式来指定切入点。

#### 
#### 固定语法
`execution(1 2 3.4.5(6))`

1. **访问修饰符**
    - `public` / `private`
1. **方法的返回参数类型**
    - `String`、`int`、`void`
    - 如果不考虑访问修饰符和返回值，这两位整合成一起写 `*`
    - 如果要是不考虑，必须两个都不考虑，不能出现 `*String`
1. **包的位置**
    - 具体包：`com.atguigu.service.impl`
    - 单层模糊：`com.atguigu.service.*`
    - 多层模糊：`com..impl`
    - 细节：`..` 不能开头
    - 找所有 `impl` 包：`com..impl` 不能写 `..impl`，写成：`*..impl`
1. **类的名称**
    - 具体：`CalculatorPureImpl`
    - 模糊：`*`
    - 不分模糊：`*Impl`
1. **方法名**
    - 语法和类名一致
1. **形参数列表**
    - 没有参数：`()` 
    - 有具体参数：`(String)`、`(String, int)`
    - 模糊参数：`(..)` 有没有参数都可以，有多个也可以！
    - 不分模糊：
        * `(String..)` `String` 后面有没有无所谓
        * `(..int)` 最后一个参数是 `int`
        * `(String..int)`



### 切点表达式的提取和复用
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733131304935-eb60d03d-61eb-40b9-bfcb-90678f7ecae1.png)

#### 切点表达式的提取
在Spring AOP中，可以通过注解和配置文件来提取切点表达式，以便在多个切面中复用。以下是一些常见的提取方法：

1. **使用注解提取切点表达式**  
可以在切面类中定义一个方法，并使用`@Pointcut`注解来标记切点表达式。然后在其他通知方法中引用这个切点表达式。

```java
@Aspect
@Component
public class LoggingAspect {

    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceMethods() {
        // 切点表达式
    }

    @Before("serviceMethods()")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Before method: " + joinPoint.getSignature().getName());
    }

    @After("serviceMethods()")
    public void logAfter(JoinPoint joinPoint) {
        System.out.println("After method: " + joinPoint.getSignature().getName());
    }
}
```

1. **使用配置文件提取切点表达式**  
可以在Spring配置文件中定义切点表达式，并在切面类中引用。

```xml
<aop:config>
    <aop:pointcut id="serviceMethods" expression="execution(* com.example.service.*.*(..))"/>
    <aop:aspect ref="loggingAspect">
        <aop:before pointcut-ref="serviceMethods" method="logBefore"/>
        <aop:after pointcut-ref="serviceMethods" method="logAfter"/>
    </aop:aspect>
</aop:config>
```

#### 切点表达式的复用
通过提取切点表达式，可以在多个切面中复用相同的切点表达式，从而减少代码重复，提高代码的可维护性。

1. **在多个切面中复用切点表达式**  
可以在一个切面类中定义切点表达式，然后在其他切面类中引用。

```java
@Aspect
@Component
public class CommonPointcuts {

    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceMethods() {
        // 切点表达式
    }
}

@Aspect
@Component
public class LoggingAspect {

    @Before("com.example.aspect.CommonPointcuts.serviceMethods()")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Before method: " + joinPoint.getSignature().getName());
    }
}

@Aspect
@Component
public class SecurityAspect {

    @Before("com.example.aspect.CommonPointcuts.serviceMethods()")
    public void checkSecurity(JoinPoint joinPoint) {
        System.out.println("Checking security for method: " + joinPoint.getSignature().getName());
    }
}
```

在多个切面中复用相同的切点表达式，避免了重复定义，提高了代码的可维护性和可读性。



Spring AOP中的环绕通知（Around Advice）是一种非常强大的通知类型，它允许在目标方法执行前后进行自定义的行为，并且可以控制是否执行目标方法，甚至可以替换目标方法的返回值或抛出异常来结束执行。以下是环绕通知的一些关键点：

1. **功能强大**：环绕通知是最强大的一种通知类型，因为它可以包围一个连接点（如方法调用），允许在方法执行前后添加自定义逻辑。
2. **控制执行流程**：环绕通知可以在方法调用前后完成自定义的行为，并且可以选择是否继续执行连接点或直接返回它们自己的返回值或抛出异常来结束执行。
3. **使用**`ProceedingJoinPoint`：环绕通知的连接点参数类型必须是`ProceedingJoinPoint`，这是`JoinPoint`的子接口，它允许控制何时执行连接点。
4. **必须调用**`proceed()`**方法**：在环绕通知中，需要明确调用`ProceedingJoinPoint`的`proceed()`方法来执行被代理的方法。如果忘记这样做，就会导致通知被执行了，但目标方法没有被执行。
5. **返回值**：环绕通知的方法需要返回目标方法执行之后的结果，即调用`joinPoint.proceed();`的返回值，否则会出现空指针异常。
6. **异常处理**：环绕通知可以捕获并处理目标方法执行过程中抛出的异常，这为异常处理提供了更大的灵活性。
7. **示例代码**：

```java
@Around("execution(public int com.test.spring.aop.ArithmeticCalculator.*(..))")
public Object aroudMethod(ProceedingJoinPoint pjd) throws Throwable {
    Object result = null;
    // 执行目标方法之前的逻辑
    try {
        result = pjd.proceed(); // 调用目标方法
        // 执行目标方法之后的逻辑
    } catch (Throwable e) {
        // 异常处理逻辑
        throw e;
    }
    return result; // 返回目标方法的结果
}
```

在这个示例中，`aroudMethod`方法接受一个`ProceedingJoinPoint`对象作为参数，该对象包含了关于当前正在执行的方法的所有信息。通过`pjd.proceed()`，你可以让目标方法继续执行，然后在其前后执行自定义的逻辑。

环绕通知因其强大的控制能力和灵活性，在Spring AOP中被广泛使用，特别是在需要对方法执行进行精细控制的场景中。



在Spring AOP中，切面的优先级决定了多个切面在同一个连接点上执行的顺序。以下是关于Spring AOP切面优先级设定的介绍：

1. **切面优先级的影响**：当同一个目标方法上存在多个切面时，切面的优先级决定了这些切面的内外嵌套顺序。优先级高的切面会在外面，优先级低的切面会在里面。
2. **使用**`@Order`**注解**：可以通过在切面类上使用`@Order`注解来控制切面的优先级。`@Order`注解的值越小，表示优先级越高；值越大，表示优先级越低。`@Order`注解的默认值是`Integer.MAX_VALUE`，即最低优先级。
3. `@Order`**注解的使用示例**：

```java
@Aspect
@Component
@Order(1) // 优先级高
public class HighPriorityAspect {
    // 切面逻辑
}

@Aspect
@Component
@Order(2) // 优先级低
public class LowPriorityAspect {
    // 切面逻辑
}
```

在这个示例中，`HighPriorityAspect`的优先级高于`LowPriorityAspect`，因为它的`@Order`值更小。

1. **基于XML的AOP配置**：在XML配置中，也可以通过`order`属性来指定切面的优先级。例如：

```xml
<aop:aspect ref="highPriorityAspect" order="1">
    <!-- 切面配置 -->
</aop:aspect>
<aop:aspect ref="lowPriorityAspect" order="2">
    <!-- 切面配置 -->
</aop:aspect>
```

这里`highPriorityAspect`的优先级高于`lowPriorityAspect`。

1. **优先级对执行顺序的影响**：对于入操作（如Before和Around通知），优先级越高的切面会越早执行；对于出操作（如After、AfterReturning和AfterThrowing通知），优先级越低的切面会越早执行。

通过合理设置切面的优先级，可以控制不同切面在目标方法执行时的执行顺序，这对于复杂的业务逻辑和事务管理等场景尤为重要。



`值越小，优先级越高`



Spring AOP（面向切面编程）是一种编程范式，它允许开发者将横切关注点（如日志记录、事务管理、权限检查等）从业务逻辑中分离出来。CGLIB是Spring AOP中使用的一种字节码生成库，用于在运行时动态地扩展类和实现AOP代理。以下是CGLIB在Spring AOP中生效的一些场景：

1. **非接口代理**：
    - 当目标对象没有实现接口时，Spring AOP不能使用JDK动态代理，因为JDK动态代理只能代理实现了接口的类。在这种情况下，Spring AOP会使用CGLIB来创建目标对象的子类，并在子类中实现代理逻辑。
1. **方法覆盖**：
    - 如果目标对象的方法被覆盖（Override），并且你想要在不改变原始方法实现的情况下添加额外的行为，CGLIB可以用来创建一个子类，在子类中添加额外的逻辑。
1. **增强非public方法**：
    - JDK动态代理只能代理public方法，而CGLIB可以代理包括private、protected和package-private在内的所有方法。因此，如果需要对非public方法进行增强，CGLIB是必需的。
1. **实现方法拦截**：
    - CGLIB通过使用MethodInterceptor来实现方法拦截，可以在方法执行前后以及抛出异常时添加自定义逻辑。
1. **实现字段拦截**：
    - CGLIB也可以用来拦截字段的读写操作，通过创建字段的getter和setter方法的子类实现。
1. **实现混合代理**：
    - 在某些情况下，可能需要同时使用JDK动态代理和CGLIB代理。Spring AOP允许混合使用这两种代理，以适应不同的目标对象和增强需求。
1. **性能优化**：
    - 对于性能敏感的应用，CGLIB代理可能比JDK动态代理更优，因为CGLIB代理是为目标对象创建子类，而JDK动态代理是为目标接口创建代理类。在某些情况下，子类代理可能比接口代理更高效。
1. **实现复杂的AOP逻辑**：
    - CGLIB提供了更多的灵活性，可以用于实现更复杂的AOP逻辑，比如多个切面在同一方法上的不同顺序执行。

在Spring配置中，可以通过`proxy-target-class`属性来指定是否使用CGLIB代理。如果设置为`true`，则Spring AOP将使用CGLIB来创建代理，即使目标对象实现了接口。如果设置为`false`（默认值），Spring将首先尝试使用JDK动态代理，如果目标对象没有实现接口，则回退到CGLIB代理。



（了解）

使用XML配置AOP（面向切面编程）是Spring框架中一个重要的功能，它允许我们在不修改业务逻辑代码的情况下，为业务逻辑添加额外的行为，比如日志记录、事务管理等。以下是使用XML配置AOP的基本步骤：

1. **添加Spring和AOP依赖**：在项目的`pom.xml`中添加Spring框架和AOP相关的依赖，如`spring-context`和`aspectjweaver`。
2. **定义业务接口和实现类**：创建业务逻辑接口及其实现，例如一个服务类`MyService`和它的实现`MyServiceImpl`。
3. **定义切面类**：创建一个切面类，用于定义前置、后置、环绕等通知。例如，`MyAspect`类中包含一个前置通知`beforeAdvice`。
4. **配置XML**：在`applicationContext.xml`中配置切面和业务bean，以及AOP相关的标签。
    - **引入AOP命名空间**：在XML配置文件中添加`xmlns:aop`和相应的`schemaLocation`。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">
    <!-- bean definitions here -->
</beans>
```

    - **定义业务bean和切面bean**：将业务逻辑类和切面类作为bean定义在XML中。

```xml
<bean id="myService" class="com.example.demo.aop.MyServiceImpl"/>
<bean id="myAspect" class="com.example.demo.aop.MyAspect"/>
```

    - **配置AOP切面**：使用`<aop:config>`标签开始AOP配置，并使用`<aop:aspect>`标签配置切面。

```xml
<aop:config>
    <aop:aspect id="myAspect" ref="myAspect">
        <!-- 配置通知 -->
    </aop:aspect>
</aop:config>
```

    - **配置通知**：在`<aop:aspect>`标签内部使用对应的标签配置通知的类型，并建立通知方法和切入点方法的关联。

```xml
<aop:config>
    <aop:aspect id="myAspect" ref="myAspect">
        <aop:before method="beforeAdvice" pointcut="execution(* com.example.demo.aop.MyService.performAction(..))"/>
    </aop:aspect>
</aop:config>
```

其中`method`属性指定切面类中的通知方法，`pointcut`属性指定切入点表达式，表示对哪些方法增强。

1. **测试配置**：编写测试代码来验证AOP配置是否生效。

通过以上步骤，你可以在Spring应用中使用XML配置AOP，为业务逻辑添加额外的行为而无需修改业务代码本身。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733136862959-839dbcef-c3a4-45c3-88bd-22d5d7cf07cb.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733136879946-75cb47f4-ac6e-4405-842f-3bcd2fb4c5e2.png)



Spring AOP（面向切面编程）是Spring框架中的一个重要概念，它允许开发者在不修改业务逻辑代码的情况下，对程序中的某些部分进行横向切入，比如日志记录、事务管理、权限检查等。AOP通过代理模式实现，即在不改变原有对象的基础上，创建一个代理对象来扩展对象的行为。

在Spring中，AOP对获取bean的影响主要体现在以下几个方面：

1. **代理对象的创建**：
    - 当你使用Spring AOP时，Spring容器会为被代理的bean创建一个代理对象。这个代理对象可能是JDK动态代理对象（如果目标对象实现了接口），或者是CGLIB代理对象（如果目标对象没有实现接口）。
    - 这意味着当你从Spring容器中获取一个bean时，实际上可能获取到的是它的代理对象，而不是原始对象。
1. **获取bean的方式**：
    - 如果你直接通过`@Autowired`注解注入bean，Spring会自动处理代理，你不需要做任何额外的操作。
    - 如果你通过`ApplicationContext`的`getBean`方法获取bean，并且指定了bean的名称，Spring同样会返回代理对象。
1. **代理对象的行为**：
    - 代理对象会拦截对原始对象的方法调用，并在调用前后执行额外的逻辑（如日志、事务等）。
    - 这可能会导致方法调用的执行时间比直接调用原始对象更长，因为代理对象需要执行额外的逻辑。
1. **代理对象的透明性**：
    - 对于客户端代码来说，代理对象是透明的，即客户端代码不需要知道它正在与代理对象交互。
    - 这意味着客户端代码可以像调用原始对象一样调用代理对象，而不需要做任何特殊的处理。
1. **配置和性能**：
    - AOP的配置可能会增加Spring容器启动的时间，因为需要额外处理代理对象的创建。
    - 在某些情况下，AOP可能会对性能产生影响，尤其是在代理逻辑非常复杂或者被代理的方法调用非常频繁的情况下。
1. **事务管理**：
    - 在Spring中，事务管理通常是通过AOP实现的。这意味着当你使用`@Transactional`注解时，Spring会为相关的bean创建代理对象，以确保在方法执行前后正确地管理事务。
1. **调试和测试**：
    - 在调试和测试时，需要注意你操作的是代理对象还是原始对象。这可能会影响调试信息和测试结果。



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733137191877-a3d807c5-3e7f-4bdd-97d6-4559e1aae5f3.png)

> 如果使用AOP结束，目标有接口，必须使用接口类型接收IoC容器中代理组件
>

AOP是一种思想，为了解决散落在四处的非核心代码，提高项目的可维护性



# TX 声明式事务
tx是对aop的再次封装



在Spring框架中，编程式事务管理是指通过代码直接控制事务的边界。与声明式事务（使用注解或XML配置）相比，编程式事务提供了更细粒度的控制，但在代码中需要显式地管理事务的开启、提交和回滚。Spring提供了`PlatformTransactionManager`接口来支持编程式事务管理。

以下是编程式事务管理的基本步骤和代码示例：

### 1. 引入依赖
首先，确保你的项目中已经包含了Spring事务管理的相关依赖。

### 2. 配置事务管理器
你需要配置一个`PlatformTransactionManager`。在Spring Boot项目中，这通常是自动配置的。如果是XML配置，你需要定义事务管理器并设置事务属性。

### 3. 编程式事务管理
#### a. 手动管理事务
你可以通过`TransactionTemplate`或直接使用`PlatformTransactionManager`来手动管理事务。

**使用**`TransactionTemplate`**：**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.TransactionDefinition;
import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.DefaultTransactionDefinition;
import org.springframework.transaction.support.TransactionTemplate;

@Service
public class MyService {

    private final TransactionTemplate transactionTemplate;

    @Autowired
    public MyService(PlatformTransactionManager transactionManager) {
        this.transactionTemplate = new TransactionTemplate(transactionManager);
    }

    public void myTransactionalMethod() {
        transactionTemplate.execute(status -> {
            // 在这里执行业务逻辑
            // 如果发生异常，事务将自动回滚
            return null;
        });
    }
}
```

**使用**`PlatformTransactionManager`**：**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.TransactionDefinition;
import org.springframework.transaction.TransactionStatus;
import org.springframework.transaction.support.DefaultTransactionDefinition;

@Service
public class MyService {

    private final PlatformTransactionManager transactionManager;

    @Autowired
    public MyService(PlatformTransactionManager transactionManager) {
        this.transactionManager = transactionManager;
    }

    public void myTransactionalMethod() {
        TransactionDefinition definition = new DefaultTransactionDefinition();
        TransactionStatus status = transactionManager.getTransaction(definition);
        try {
            // 在这里执行业务逻辑
            transactionManager.commit(status);
        } catch (Exception e) {
            transactionManager.rollback(status);
            throw e;
        }
    }
}
```

#### b. 设置事务属性
你可以通过`TransactionDefinition`设置事务的传播行为、隔离级别、超时时间等属性。

```java
TransactionDefinition definition = new DefaultTransactionDefinition();
definition.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);
definition.setIsolationLevel(TransactionDefinition.ISOLATION_SERIALIZABLE);
definition.setTimeout(30); // 超时时间，单位为秒
```

### 4. 处理事务回滚
在编程式事务管理中，你需要手动捕获异常并决定是否回滚事务。

### 总结
编程式事务管理提供了对事务控制的细粒度操作，但相比声明式事务，它需要更多的代码，可能会增加出错的机会。在实际开发中，声明式事务因其简洁性和易用性更受欢迎，但在需要更复杂事务控制的场景下，编程式事务管理是一个有力的工具。



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733138230700-a05aa905-92f9-463d-a168-3e250f171973.png)



插拔式，增强了弹性







