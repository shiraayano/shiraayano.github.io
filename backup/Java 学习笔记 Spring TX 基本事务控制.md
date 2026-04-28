![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733161893932-20a5e9a6-9647-48f8-9deb-5e6043bcd90d.png)



### Spring TX 基本事务控制
#### 什么是事务？
事务（Transaction）是指一组操作的集合，这些操作要么全部成功，要么全部失败。事务的主要特性包括原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）和持久性（Durability），简称ACID特性。

#### 为什么需要事务？
在数据库操作中，事务可以确保数据的一致性和完整性。例如，在银行转账操作中，事务可以确保从一个账户扣款和向另一个账户存款这两个操作要么同时成功，要么同时失败，避免出现资金丢失或重复的问题。

#### Spring中的事务管理
Spring提供了强大的事务管理功能，支持声明式事务和编程式事务两种方式。声明式事务通过注解或XML配置来管理事务，而编程式事务则通过编写代码来管理事务。

#### 声明式事务管理
声明式事务管理是Spring推荐的事务管理方式，主要通过注解来实现。

1. **引入依赖**  
在项目的`pom.xml`文件中添加Spring事务管理相关的依赖：

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-tx</artifactId>
    <version>5.3.10</version>
</dependency>
```

1. **启用事务管理**  
在Spring配置类中启用事务管理：

```java
@Configuration
@EnableTransactionManagement
public class AppConfig {
    @Bean
    public PlatformTransactionManager transactionManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
}
```

1. **使用注解管理事务**  
在需要事务管理的方法上使用`@Transactional`注解：

```java
@Service
public class MyService {

    @Autowired
    private MyRepository myRepository;

    @Transactional
    public void performTransaction() {
        myRepository.save(new Entity());
        // 其他数据库操作
    }
}
```

#### 编程式事务管理
编程式事务管理通过编写代码来管理事务，适用于需要精细控制事务的场景。

1. **获取事务管理器**

```java
@Autowired
private PlatformTransactionManager transactionManager;
```

1. **编写事务管理代码**

```java
public void performTransaction() {
    TransactionStatus status = transactionManager.getTransaction(new DefaultTransactionDefinition());
    try {
        // 数据库操作
        transactionManager.commit(status);
    } catch (Exception e) {
        transactionManager.rollback(status);
        throw e;
    }
}
```

#### 事务传播行为
Spring事务管理支持多种事务传播行为，如`REQUIRED`、`REQUIRES_NEW`、`NESTED`等。可以通过`@Transactional`注解的`propagation`属性来设置事务的传播行为：

```java
@Transactional(propagation = Propagation.REQUIRED)
public void performTransaction() {
    // 事务操作
}
```



### Spring 事务属性
在Spring中，`@Transactional`注解用于声明事务。通过设置不同的属性，可以控制事务的行为。以下是一些常用的事务属性：

1. **propagation**（传播行为）
    - 定义事务的传播行为，即当前事务方法被另一个事务方法调用时，事务如何传播。
    - 常见的传播行为包括：
        * `REQUIRED`：默认值，支持当前事务，如果没有则创建一个新事务。
        * `REQUIRES_NEW`：总是创建一个新事务，如果当前存在事务，则挂起当前事务。
        * `SUPPORTS`：支持当前事务，如果没有事务，则以非事务方式执行。
        * `NOT_SUPPORTED`：以非事务方式执行，如果当前存在事务，则挂起当前事务。
        * `MANDATORY`：支持当前事务，如果没有事务，则抛出异常。
        * `NEVER`：以非事务方式执行，如果当前存在事务，则抛出异常。
        * `NESTED`：如果当前存在事务，则在嵌套事务内执行，否则创建一个新事务。
1. **isolation**（隔离级别）
    - 定义事务的隔离级别，以防止多个事务之间的数据干扰。（推荐设置第二隔离级别）
    - 常见的隔离级别包括：
        * `DEFAULT`：使用数据库默认的隔离级别。
        * `READ_UNCOMMITTED`：最低的隔离级别，允许读取未提交的数据，可能会导致脏读、不可重复读和幻读。
        * `READ_COMMITTED`：允许读取已提交的数据，防止脏读，但可能会导致不可重复读和幻读。
        * `REPEATABLE_READ`：防止脏读和不可重复读，但可能会导致幻读。
        * `SERIALIZABLE`：最高的隔离级别，防止脏读、不可重复读和幻读，但性能较低。
1. **timeout**（超时时间）

```java
@Transactional(timeout = 30)
public void performTransaction() {
    // 事务操作
}
```

    - 定义事务的超时时间（以秒为单位）。如果事务在指定时间内没有完成，则自动回滚。
1. **readOnly**（只读）

```java
@Transactional(readOnly = true)
public void performReadOnlyTransaction() {
    // 只读事务操作
}
```

    - 指定事务是否为只读事务。只读事务可以优化性能，适用于只执行查询操作的方法。
1. **rollbackFor**（回滚规则）

```java
@Transactional(rollbackFor = Exception.class)
public void performTransaction() throws Exception {
    // 事务操作
}
```

    - 指定哪些异常会导致事务回滚。可以指定一个或多个异常类。
1. **noRollbackFor**（不回滚规则）

```java
@Transactional(noRollbackFor = IllegalArgumentException.class)
public void performTransaction() {
    // 事务操作
}
```

    - 指定哪些异常不会导致事务回滚。可以指定一个或多个异常类。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733162225890-8c4eefc8-0a5b-4330-a7d7-55639c7bf0da.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733162367837-4954afdd-57ca-4724-9c61-164a985c4d8e.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733162634176-440095e7-427d-4381-8bb4-4ae742e9951a.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733162504697-b6766b0f-b560-4001-8096-1e5316e9d74d.png)



### 事务传播行为
事务传播行为（Transaction Propagation Behavior）定义了当一个事务方法被另一个事务方法调用时，事务如何传播。Spring提供了多种传播行为，以满足不同的事务管理需求。以下是常见的事务传播行为：

1. **REQUIRED**
    - **描述**：如果当前存在事务，则加入该事务；如果当前没有事务，则创建一个新事务。
    - **应用场景**：这是默认的传播行为，适用于大多数情况。
    - （如果父方法有事务，我就加入，没有就新建自己独立）
2. **REQUIRES_NEW**
    - **描述**：总是创建一个新事务。如果当前存在事务，则挂起当前事务。
    - **应用场景**：适用于需要独立事务的情况，例如记录日志操作。
    - （不管父方法是否有事务，我都是新建事务，都是独立的）
3. **SUPPORTS**
    - **描述**：如果当前存在事务，则加入该事务；如果当前没有事务，则以非事务方式执行。
    - **应用场景**：适用于既可以在事务中执行，也可以在非事务中执行的操作。
4. **NOT_SUPPORTED**
    - **描述**：以非事务方式执行，如果当前存在事务，则挂起当前事务。
    - **应用场景**：适用于不需要事务的操作，例如读取配置文件。
5. **MANDATORY**
    - **描述**：如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。
    - **应用场景**：适用于必须在事务中执行的操作。
6. **NEVER**
    - **描述**：以非事务方式执行，如果当前存在事务，则抛出异常。
    - **应用场景**：适用于不允许在事务中执行的操作。
7. **NESTED**
    - **描述**：如果当前存在事务，则在嵌套事务内执行；如果当前没有事务，则创建一个新事务。
    - **应用场景**：适用于需要嵌套事务的情况，例如批量处理操作。

#### 示例代码
以下是一个使用`@Transactional`注解设置事务传播行为的示例：

java

```plain
@Service
public class MyService {

    @Transactional(propagation = Propagation.REQUIRED)
    public void requiredTransaction() {
        // 事务操作
    }

    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void requiresNewTransaction() {
        // 事务操作
    }

    @Transactional(propagation = Propagation.SUPPORTS)
    public void supportsTransaction() {
        // 事务操作
    }

    @Transactional(propagation = Propagation.NOT_SUPPORTED)
    public void notSupportedTransaction() {
        // 事务操作
    }

    @Transactional(propagation = Propagation.MANDATORY)
    public void mandatoryTransaction() {
        // 事务操作
    }

    @Transactional(propagation = Propagation.NEVER)
    public void neverTransaction() {
        // 事务操作
    }

    @Transactional(propagation = Propagation.NESTED)
    public void nestedTransaction() {
        // 事务操作
    }
}
```

传播行为：父方法调用子方法时，子方法是否要加到父方法中，或者是新建

