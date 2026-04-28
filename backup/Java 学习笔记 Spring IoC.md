
# Spring 框架学习笔记

## 什么是框架？
框架是一种应用程序内部预设了常见问题解决方案的工具。开发者可以直接调用框架的方法以简化开发。

- 有 **jar 包**，可以自定义配置的工具即为框架。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732697745048-dd7b0e88-a5fa-45f3-b6c5-8264e4b7af60.png)

## Spring 核心功能
Spring 作为组件管理框架，具有以下核心功能：
1. **IoC（控制反转）**
   - Spring 充当组件管理者，将组件的创建、管理和存储职责交由容器负责。
   - Spring IoC 容器是复杂容器，与普通容器（如数组、集合）和 Servlet 容器类似，但更具灵活性。
   - ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732699521922-5cd03343-7895-45db-86f7-f00a93788410.png)

2. **DI（依赖注入）**
   - 通过依赖注入，容器动态提供对象所需的依赖，而非硬编码依赖。
   - 只有交由 Spring 管理的组件才能享受其家族的其他功能（如 AOP、事务管理）。
   - ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732699610183-2a1d9876-3501-46ce-bff1-c06053403703.png)

## Spring 核心模块
### 1. 核心容器（Core Container）
- 包含核心模块、上下文模块、Bean 工厂和 SpEL（Spring 表达式语言）。
    - **核心模块**：提供 DI 功能。
    - **上下文模块**：框架式对象访问方式。
    - **Bean 工厂**：用于创建和管理 Bean 对象。
    - **SpEL**：支持在 XML 和注解中使用表达式。

### 2. 数据访问与集成
- **JDBC 模块**：简化数据库访问，提供统一异常处理和事务管理。
- **ORM 模块**：支持 Hibernate、JPA、MyBatis 等。
- **事务管理**：支持声明式和编程式事务管理。

### 3. Web 模块
- **Spring MVC**：基于 MVC 模式，简化 Web 应用开发。
    - **控制器**：处理用户请求。
    - **视图解析器**：渲染视图（如 JSP、Thymeleaf）。
    - **数据绑定和验证**：自动绑定请求参数并进行验证。

### 4. Spring Boot
- **自动配置**：根据依赖自动配置应用。
- **嵌入式服务器**：支持嵌入式 Tomcat、Jetty 等。
- **Spring Initializr**：快速创建 Spring Boot 项目。

### 5. Spring Cloud
- **服务发现**：使用 Eureka 或 Consul。
- **配置管理**：使用 Spring Cloud Config。
- **断路器**：使用 Hystrix 增强容错能力。

### 6. 安全模块
- **Spring Security**：支持认证和授权。
    - **认证**：表单登录、OAuth2 等。
    - **授权**：基于角色和权限控制。

### 7. 测试模块
- 提供对 Spring 应用的单元测试和集成测试支持。
    - **Mock 对象**：与 Mockito 集成。
    - **测试上下文**：加载 Spring 上下文进行测试。

### 容器配置
为了适应现代开发环境，推荐使用 **配置类 + 注解** 的方式。
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732699300270-323cb31a-b61a-4c00-b2d2-b132b10c09ed.png)

## Spring 的优点
1. **降低耦合度**：通过 DI 动态注入依赖，减少组件间硬编码耦合。
2. **提高可测试性**：方便使用 Mock 对象进行单元测试。
3. **增强灵活性**：通过配置文件或注解动态调整依赖关系。
4. **模块化设计**：可按需选择模块使用。
5. **统一管理**：集中管理组件及依赖关系，提高一致性。
6. **丰富生态系统**：大量扩展与社区支持。
7. **简化配置**：Spring Boot 提供默认配置，专注业务逻辑。

## 组件管理
- **组件** 是可以复用的 Java 对象。
- **组件一定是对象**，但对象不一定是组件。

Spring 的 IoC 容器允许开发者通过配置文件或注解定义组件，并自动管理它们的生命周期和依赖关系。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732698601280-165cf778-adde-4026-8208-2112b397005c.png)

---
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732699900372-bd3497f2-9a9f-4527-a112-abc0421b61d9.png)

第一步 **编写配置信息**

第二步 **实例化IoC对象**

第三步 **通过IoC容器获取组件**





# IoC配置


### 一 XML文件的方式



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732699992368-57991bef-e662-4068-a7a8-0c1b457aac48.png)

- 一个bean就是一个组件



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732704383919-f5a66dc0-93bf-4ec8-8ebf-1da2584dedba.png)



- 使用父工程管理依赖

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732704751872-3959077e-8b83-4e13-98cc-7f94dc0b567c.png)



> 在resources中创建配置文件  
建议使用此方式一键创建   
New - XML Configuration - Spring Config



- 无参构造函数例子

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732705098483-5607519a-e5ec-400f-8982-8b09b7041963.png)



- 静态工厂类例子（必须是静态工厂才可以用此方法）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732705198781-3cebcdef-de05-4182-9392-31f3af0c1b77.png)



- 非静态工厂（需要两步）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732705350812-38ac15ac-a56c-4951-bf0f-025c02311079.png)



# DI 的配置
>有两种注入方式  
 1.基于构造函数的依赖注入  
 2.基于Setter的依赖注入  

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732705526603-f8077aac-deec-43f5-9b2b-166e9cc80cb8.png)





引用和被引用的容器必须在IoC容器中



有参构造函数 可以在bean标签中传参

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732705914712-94f76a2d-b5c1-492d-8265-fa90f11380ca.png)

多个构造参数注入三种方式

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732706239225-ad91bbb4-b9c8-448f-82e4-ee17d3a21ca6.png)

> 顺序 name index   
推荐使用 name





> 另外 声明顺序无所谓

> SpringIoC是一个高级容器   
内部会有缓存操作，线创建对象，再进行赋值

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732706033143-43c3e7f9-db89-4762-b864-43ac727b1b12.png)





# 基于 Setter 注入（重要）
> name->属性名 setter方法的 去set和首字母小写的值!调用set方法的
setMovieFinder ->movieFinder   
value |ref 二选一   
value="直接属性值”ref =”其他bean的Id"   

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732706464337-869396f2-40be-4504-a4ea-85d2d6527a15.png)



#### IoC 容器的创建和使用

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732707453581-e9612ca3-23a4-4f14-8b48-17656ff7f79b.png)

#### 如何创建 ioc 并读取配置文件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732707770837-c404edc0-7817-4aea-b6d4-c620a771d8ff.png)





#### 在 ioc 容器中获取组件 bean

- 获取值的三种方式

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732707924132-d37a99d0-1213-414d-9fe1-f481f5285b89.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732708106253-32712ff8-f0ce-404f-be01-a7bf8a799044.png)



- 组件（bean ）周期方法

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732708513808-037f0060-42bd-4428-a2fb-1fd4b7a17cb1.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732708755374-083888a8-d12d-4d03-9899-16de58bb32b1.png)



- 拓展作用域配置

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732708976941-fbb508ef-e256-4204-964d-eb6bb2f68e21.png)

> 单例 一个 bean 标签（scope = 单例）对应一个 beandefinition 对应一个 组件对象   
多例 对应多个组件对象



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732709135803-dc4dd506-e74a-4e4b-9541-bc24b9ff8744.png)



> 例子 单例

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732709384412-cfbf8320-c736-4327-9139-63978e980a43.png)

> 单例输出 true

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732709419045-bb91f285-d551-4d1e-8dba-a896cb96c991.png)



> 多例

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732709344264-c0f6d035-2d3c-4ccf-882f-ad4c47fa9bf9.png)

> 此时输出 false

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732709451828-96478ef3-7140-4a17-bd0d-539234763bf9.png)





#### 拓展 spring-ioc factorybean

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732716937618-2b8ccbb9-8278-4a62-8a1d-0488d10567f5.png)

#### factorybean 介绍

##### 应用场景



> 创建一个 factorybean   
1 实现 factorybean 接口 <返回值泛型>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732717245220-c98f683c-a274-4ba2-9399-57fd24bc5d4e.png)



> 配置到 ioc 容器内

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732717386471-a67d8a0e-875d-4fd9-9818-d2d98e01ab0b.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732717409487-89a948a3-4545-44e4-8141-2059d725bf57.png)

> 输出

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732717419912-4656b403-31f4-47c4-9030-c3fa726f2280.png)



- beanfactory 和 factorybean 区别

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732717566373-e3356c47-793d-46f3-92bb-a0d5eff09a51.png)





## 使用注解方式管路组件 （bean）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732879543946-1a2cc921-675b-4b7e-8373-a52a2c9652bf.png)



#### 注解

1. **@Component**：这是一个通用的注解，用于标记一个类为Spring的组件。它可以用于任何层次的组件。

```java
@Component
public class MyComponent {
    // 组件逻辑
}
```

2. **@Controller**：用于标记控制器组件，通常用于Web层。

```java
@Controller
public class MyController {
    // 控制器逻辑
}
```

3. **@Service**：用于标记服务层组件，通常用于业务逻辑层。

```java
@Service
public class MyService {
    // 服务逻辑
}
```

4. **@Repository**：用于标记持久层组件，通常用于数据访问层。

```java
@Repository
public class MyRepository {
    // 数据访问逻辑
}
```

5. **@Autowired**：用于自动装配Bean，可以标记在字段、构造器或方法上。

```java
@Autowired
private MyService myService;
```

6. **@Configuration** 和 **@Bean**：用于Java配置类中，定义和配置Bean。

```java
@Configuration
public class AppConfig {
    @Bean
    public MyComponent myComponent() {
        return new MyComponent();
    }
}
```



注意：添加ioc注解，默认组件名默认为类的首字母小写

+ 示例 扫描包

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732883721678-3aa92871-f6aa-45ea-b15d-549f0fea7db1.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732883739418-5957125d-f36a-486f-9869-c5d3b6ffbe4a.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732883698739-3cfea2f6-8120-414d-b4dc-861227dbd6f6.png)

 - 排除包下的某些注解

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732883848246-595a388b-4418-4a9b-9c50-61b4f67a4278.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732884315476-af92d8e2-79e7-40c9-8ec3-24183132a9c0.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732884282644-71ca079d-614f-48f6-87c4-69588dfa1b30.png)

+ 指定包，指定注解

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732884411558-8fb4cd2c-f4ce-45eb-832d-8667ba3e77f7.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732884449158-242b3ccb-148d-42ae-ac3c-06bd80a06fac.png)



### ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732884580193-326ea060-adf9-464d-8cda-054d22d75723.png)


+ 添加注释
+ 指定包



### 示例
+ 配置周期方法

周期方法命名随意，但必须是 public void 没有形参

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732885200996-a7364899-d055-4de0-b576-c3ec5ce06ad4.png)

+ 扫描包

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732885255568-b55a3eeb-44c0-44eb-b946-bc98e2194d83.png)

+ 测试

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732885345547-e7f84128-943f-40a8-a3e2-ff0e56f999d6.png)

+ 输出

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732885379066-15c6169f-056a-4607-af4f-8a0b72062142.png)



自动注解装配

1. **@Autowired**：这是最常用的自动装配注解。它可以用于构造器、方法或字段上，Spring会自动根据类型匹配Bean。

```java
@Autowired
private MyService myService;
```

2. **@Qualifier**：当有多个相同类型的Bean时，可以使用@Qualifier指定需要注入的Bean的名称。

```java
@Autowired
@Qualifier("specificBeanName")
private MyService myService;
```

3. **@Primary**：当有多个相同类型的Bean时，可以使用@Primary标记一个Bean为首选Bean。

```java
@Primary
@Bean
public MyService myPrimaryService() {
    return new MyServiceImpl();
}
```

4. **@Resource**：这是Java标准的注解，类似于@Autowired，但可以通过名称或类型进行注入。

```java
@Resource(name = "myService")
private MyService myService;
```

5. **@Inject**：这是来自JSR-330的注解，功能类似于@Autowired。

```java
@Inject
private MyService myService;
```





**佛系装配** 是一种在 Spring 框架中使用的自动装配技术，旨在简化配置和提高开发效率。以下是其主要特点：

+ **自动装配**：通过注解（如 @Autowired），Spring 可以自动满足 bean 之间的依赖，减少显式配置。
+ **类型匹配**：默认按类型（byType）从容器中匹配一个 bean 注入，支持成员变量、构造器和方法上的注解。
+ **避免异常**：可以通过设置 @Autowired 的 required 属性为 false 来避免没有匹配类型的 bean 时抛出异常。
+ **解决歧义**：使用 @Primary 或 @Qualifier 注解来解决多个 bean 匹配时的歧义问题。

这种方法能够显著减少配置文件的复杂度，使开发过程更加高效和简洁。



> 不太建议使用佛系装配
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732885965496-1408e2aa-ee7b-4efc-b078-7189d1cce4e1.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886042062-0e463c92-27c2-4a84-acf1-65212a1d6775.png)



> JSR注解
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886104352-dedd3a31-234d-4d32-9990-0d12762ed2b9.png)

Resource注解

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886130506-282db529-836e-466d-964a-4f1df6cee327.png)



### 赋值方法
+ 直接赋值
+ 注解赋值（一般用于读写配置信息）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886310750-cf402ed8-e74e-471a-9b66-886797e21830.png)





引入使用@value

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886419410-4c0c76d4-41a5-4213-88ba-de8949decd3b.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886475814-dcb91475-d654-4b4b-8c71-7132f28a886d.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886511229-b1628f70-7bee-4e9f-8c4c-e9bcdbd5a1da.png)



> 总结
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732886875381-c9e99d39-2023-4fcb-aac8-3a8ac06e6e85.png)

使用注解配置依然会使用到xml文件，没有摆脱xml解析效率低的问题·

1.注解的扫描配置

2.引入外部的文件

3.引入第三方的bean也仍然需要xml文件

--- 



使用@Autowirted需要先使用@Repository

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732887082200-ba61145d-fb97-4924-871d-2dceed982d7b.png)



### 配置类（完全注解开发）
配置类可以完全替代xml，解决解析效率问题

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732887643523-cfcade39-3b2e-4b17-9c94-911cf3482a01.png)



description ： java的配置类、替代xml文件

1. 包扫描注解配置
2. 引用外部配置文件
3. 声明第三方以来的bean组件

步骤：

1. 添加@Configuration 代表是配置类
2. 实现上面的三个功能注解

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888067065-59a1a961-9795-466f-826b-757475d0cd6b.png)



示例：

注意：在刷新的时候才进行ioc和di的注入

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888177901-43687530-6814-47cf-84c3-2a0c2fad5aff.png)



@Bean 定义组件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888382058-913f5233-30c4-46ee-b5bb-582de1884bf6.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888398597-1b574555-440d-4245-8d55-98239b4dfec8.png)



取名字@Bean(name="",initMethod)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888511332-89dec761-ff93-4384-bf0d-9e67ddbcc78c.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888574792-b5798321-21df-4565-ba12-d9ed3de4a7a2.png)



### 引用其它ioc容器

两种方式，推荐二 
直接调用bean方法即可   
直接形参变量引入，要求必须有对应的组件，如果有多个，形参名 = 组件id标识即可

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888705179-1b08c244-687f-46e4-aaae-49d8ff57a034.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732888778563-83118290-78b7-42fc-ab19-1212e24e7caf.png)

@Import 注解使用

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732896948973-a338e5c7-624e-4b24-a9e7-a701e6a451f9.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732896967930-4f9800e5-8dd7-4d95-bf66-b09e8df1c279.png)

配置类

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733045585172-f6cdb14a-ceeb-40d0-a3c6-fb8dc3be52ab.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733045633962-708fea14-e363-4b63-a80d-ceff20dd8a82.png)



#### 搭建测试环境

### 4.6 整合Spring5-Test5搭建测试环境
1. 整合测试环境作用 好处1：不需要自己创建IOC容器对象了 好处2：任何需要的bean都可以在测试类中直接享受自动装配
2. 导入相关依赖

```plain
<!--junit5测试-->
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.3.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-test</artifactId>
    <version>6.0.6</version>
    <scope>test</scope>
</dependency>
```

1. 整合测试注解使用

```plain
//@SpringJUnitConfig(locations = {"classpath:spring-context.xml"})  //指定配置文件xml
@SpringJUnitConfig(value = {BeanConfig.class})  //指定配置类
public class Junit5IntegrationTest {
    
    @Autowired
    private User user;
    
    @Test
    public void testJunit5() {
        System.out.println(user);
    }
}
```



- 例子
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733048740073-3f713050-6c21-4ffb-88cc-422a95b3c445.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733048664031-1a1fe64b-4052-40c6-8eea-5fba445ce598.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733048705338-1b432af7-b667-4882-ac2d-245ca8c5da72.png)








# 废稿
#### 写了干脆放出来


### 配置maven
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274268833-f65eef69-5cde-4034-941d-5a1745661735.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274252090-8d745512-c7aa-4865-8166-22a05e710834.png)



#### 配置出问题时需要做两件事
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274348317-24fd4837-e9be-40dd-9d4d-add079eb3373.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274386514-476cb2e7-a38d-4ca7-81b8-9b648c8f67dc.png)

最后清除缓存

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274418402-7081d38d-32a6-4498-82a3-37288ef132c2.png)



+ 其它

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274519022-3d5959e5-5d3b-4952-a7b6-48703b60df11.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274542772-95ccc229-a121-4fbc-984b-8934312e77ce.png)





### 创建项目
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732273595343-22b10dee-595f-429d-95c8-4052a946837f.png)

选择必要的选项（目前默认即可）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732273616020-9b1fdd80-83a6-465f-b72a-27a2d45012d0.png)

（可以删除没有的东西）

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732273681115-70397c70-070b-4247-8e19-953cac57d859.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732273853634-8ccfee71-1d20-4ec1-ba4e-04d436476509.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732273916713-5176adfd-6e89-4cca-a1d9-b1f911b4d68a.png)

Spring启动的默认组件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732273992019-c37a1e50-7c65-44db-81c7-f678387e6939.png)

安装组件 一键生成默认值

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274117598-9a3b4a96-936d-4eed-9c0f-7b0413f65b52.png)



给容器添加自己的组件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274207743-53f2a0c4-110c-4c99-af17-a8a82e57f2ac.png)

### 从容器中获取组件
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274669567-f633a478-2c3a-4dc9-8109-ee77259c4360.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732274697736-9e1e2fba-7f4d-49b8-9e48-2769ed3a1484.png)



@Bean

将组件放到容器中

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732276572386-b5f99b9f-891f-461b-9c95-dacc1fd3679b.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732276791912-a13d43c3-4a7a-435f-96bf-af81f7d8381b.png)



小结:

从容器中获取组件，

1)、组件不存在，抛异常:NoSuchBeanDefinitionException

2)组件不唯一，抛异常:NoUniqueBeanDefinitionException

3)、组件唯一存在，正确返回。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732276850578-dee3a424-ea8e-452a-b039-452ecb12fb55.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732276863207-a8a4f73f-c98f-4b2d-b759-7ce48ad429ee.png)





![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732276929438-f71e466e-0077-44ee-a3a6-5eb8c35eb7d2.png)



组件是单实例的

组件创建：容器启动时就会创建

单实例特性：所有组件默认是单例的，使用时从容器中调用






