### MyBatis简介
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733233179374-fc012a6d-44f5-4310-b6a6-480a8a6c318f.png)

mybatis就是一层封装

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733234269306-4ff84d50-58a0-4548-a832-7b4aaf6bbbdf.png)

作用：简化数据库操作的

运行效率 JDBC>MyBatis>Hibernate

这些都是对于JDBC的封装，封装的越多，效率越低

功能强大性能优异

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733233032178-433c21bc-a7a7-4d0f-a925-d726c7f37178.png)

#### 什么是MyBatis？
MyBatis是一个优秀的持久层框架，它支持自定义SQL、存储过程以及高级映射。MyBatis消除了几乎所有的JDBC代码以及设置参数和获取结果集的工作。MyBatis可以通过简单的XML或注解来配置和映射原始类型、接口和Java POJO（Plain Old Java Objects，普通老式Java对象）为数据库中的记录.

#### MyBatis的特点
1. **简化数据库访问**：MyBatis通过XML或注解配置，简化了数据库访问操作，减少了代码量。
2. **灵活的SQL**：支持自定义SQL语句，开发者可以完全控制SQL的执行。
3. **高级映射**：支持复杂的映射关系，包括一对一、一对多、多对多等。
4. **动态SQL**：支持动态SQL语句，可以根据条件生成不同的SQL。
5. **缓存机制**：内置一级缓存和二级缓存，提高了查询性能。

#### MyBatis的基本使用
1. **引入依赖**  
在项目的`pom.xml`文件中添加MyBatis相关的依赖：

```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.17</version>
</dependency>
```

1. **配置SqlSessionFactory**  
使用XML配置文件来配置SqlSessionFactory：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "https://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```

1. **定义Mapper接口**  
创建一个Mapper接口，并在接口方法上使用注解或XML配置SQL语句：

```java
public interface BlogMapper {
    @Select("SELECT * FROM blog WHERE id = #{id}")
    Blog selectBlog(int id);
}
```

1. **使用MyBatis**  
在代码中使用SqlSessionFactory获取SqlSession，并调用Mapper接口的方法：

```java
try (SqlSession session = sqlSessionFactory.openSession()) {
    BlogMapper mapper = session.getMapper(BlogMapper.class);
    Blog blog = mapper.selectBlog(101);
}
```

#### MyBatis的应用场景
1. **企业级应用开发**：MyBatis适用于各种规模的企业级应用开发，特别是需要灵活控制SQL的场景。
2. **复杂查询**：MyBatis支持复杂的查询和映射关系，适用于需要复杂查询的应用。
3. **高性能需求**：MyBatis内置缓存机制，适用于对性能有较高要求的应用。
4. 轻量级



#### 示例
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232394657-c951c621-c45c-4fc7-bd53-15c5c04de449.png)

##### 新建一个父工程
+ 导入依赖
    - 需要导入mybatis
    - mysql驱动
    - junit5测试

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232138453-76ee08a8-e897-47a4-ba76-e5e2eb90d72e.png)

##### 新建moudle
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232252596-6dc654e4-2484-4f6f-88c5-eebb4abf2542.png)



##### --
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232441799-937e16d5-9e3a-430a-a19c-692ecf5e2614.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232503194-85c40bc0-dcb5-4612-a6e0-b64880ae8e05.png)

注意：mapper接口不能重载，因为它是根据方法名识别的

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232726052-a09e011f-82b2-4cc1-b814-bfcd0d1768d4.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733232928185-d56cb21d-9dfe-4725-b2b1-819765313d90.png)





#### ibatis方式
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733233865980-b66ec490-7e1e-46da-8515-dcd3a493ac2b.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733233293744-fe226828-967c-4bad-9d12-01dcc2b96f3b.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733233600302-37b22422-33e3-401a-9702-b23c8041959f.png)



我们可以声明接口来保证我们写的正确

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733233962724-6afa2c22-f427-4418-a340-90ccdb814771.png)





### MyBatis中的#{}和${}的区别
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733320817082-0537e525-bbf7-4373-8103-6184cb044505.png)

在MyBatis中，`#{} `和`${}`是用于在SQL语句中插入参数的两种方式，它们有不同的用途和行为。

#### 1. `#{} `（占位符 + 赋值   id=? ?=赋值） 推荐使用
+ **用途**：用于安全地插入参数，防止SQL注入。
+ **行为**：MyBatis会将`#{} `中的参数替换为一个占位符（如`?`），并使用PreparedStatement来设置参数值。
+ 只能替代值的位置，不能替代容器名（标签，列名，sql 关键字）
+ **示例**：

```xml
<select id="selectUser" parameterType="int" resultType="User">
    SELECT * FROM users WHERE id = #{id}
</select>

```

在这个示例中，`#{id}`会被替换为一个占位符`?`，并在执行SQL时将参数值设置为`id`的值。

#### 2. `${}`（字符串拼接）
+ **用途**：用于直接插入参数值，不进行预编译，适用于动态生成SQL语句的场景。
+ **行为**：MyBatis会将`${}`中的参数直接替换为参数值，不进行任何转义或预编译。
+ **示例**：

```xml
<select id="selectUser" parameterType="String" resultType="User">
    SELECT * FROM users WHERE name = '${name}'
</select>

```

在这个示例中，`${name}`会被直接替换为参数`name`的值。如果`name`的值是`John`，则生成的SQL语句为`SELECT * FROM users WHERE name = 'John'`。

#### 区别总结
1. **安全性**：`#{} `使用PreparedStatement，防止SQL注入；`${}`直接插入参数值，存在SQL注入风险。
2. **性能**：`#{} `使用预编译SQL，性能较好；`${}`每次执行都会重新解析SQL，性能较差。
3. **用途**：`#{} `适用于传递参数值；`${}`适用于动态生成SQL语句。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733321245049-f6876139-df3c-4f0c-9dda-21881bb991b6.png)



#### 简单类型传入
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733321353682-ec15276b-efbd-4dd1-a667-8644be7e0597.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733321420123-4ecdc790-8b6b-4b1d-99d0-c77ca3a47adf.png)

key 值随便写，一般情况推荐使用参数名

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733321544305-23f1ef32-5b03-4d89-b6eb-f4872673c23b.png)

#### 单个实例对象传入
key=属性名即可

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733321583765-fda45596-89b8-4372-8db5-c734efbc72ac.png)

写传入对象的属性

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733321657815-47e4862f-1734-46bf-b482-945b0e1edd2d.png)



#### 传入多个简单类型数据如何取值
推荐使用注解

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733322412695-89891707-0dad-4513-9b59-1a8c12fe7fd2.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733322420276-ee56270e-a47f-40be-8e32-ea044eeaf64b.png)

#### 传入 map
key=map 的 key 即可

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733322576240-cfbe1dc5-aaa5-4529-a16b-dd61e9b1c21f.png)







可以去官网查看文档 mybatis.org

#### 事务管理器
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733320081154-11ef6b3d-3b2a-4740-abee-9885ab0b2a92.png)

使用 JDBC 就会自动开启管理事务，有事务相关的管理

使用 MANAGED 这个配置基本啥也不干

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733320179732-fb4d2bce-b8da-4438-83e2-94c71949cf9d.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733320247514-4e040481-517e-4171-baa4-085890f34e7d.png)

一般我们不使用 mybatis 的连接池，我们使用第三方的

性能好



开启日志输出

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733320431240-7cb3cf3f-7a2f-427d-a7a5-25ab53d84e72.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733320450495-bf994b48-f4c0-4bfb-b153-e7353a61e26d.png)



  



### 单个简单类型和定义别名
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733322841767-dc37966b-7c6c-43d5-abc3-916684604ac0.png)

可以写全名或者简写

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733322977387-96f5addb-a603-42c0-b0af-521af11c250a.png)

> mybatis 给我们提供了 72 种类别名，如果没有我们可以自己定义或写类的全限定符号
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323032510-69d4a133-11d2-4c6d-a26c-976b2e6be4cf.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323076298-2ac12bcc-e3cf-4889-a06a-796695148995.png)

> 写别名
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323152273-8dcf1704-b02f-4158-9abc-364fde1bdabd.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323219283-56b72104-aac8-48e0-b9c3-02e17a221039.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323314679-44d06783-2435-4a1c-aad4-bb9396728054.png)

#### 单个简单类型
单个简单类型指的是Java中的基本数据类型及其包装类，如`int`、`Integer`、`String`、`boolean`、`Boolean`等。这些类型在MyBatis中可以直接作为参数和返回值使用。

**示例**：

```xml
<select id="selectUserName" parameterType="int" resultType="String">
    SELECT name FROM users WHERE id = #{id}
</select>

```

`parameterType`指定了参数类型为`int`，`resultType`指定了返回值类型为`String`。

#### 定义别名
MyBatis允许为Java类定义别名，以简化配置文件中的类型声明。别名可以通过`<typeAlias>`标签在MyBatis配置文件中定义，也可以通过注解方式定义。

**XML配置方式**：

```xml
<typeAliases>
    <typeAlias alias="User" type="com.example.model.User"/>
</typeAliases>

```

`User`是`com.example.model.User`类的别名。在Mapper文件中，可以使用别名代替全限定类名。

**注解方式**：

```java
@Alias("User")
public class User {
    private int id;
    private String name;
    // getters and setters
}
```

`@Alias("User")`注解为`User`类定义了别名。在Mapper文件中，可以使用别名代替全限定类名。

**使用别名的示例**：

```xml
<select id="selectUser" parameterType="int" resultType="User">
    SELECT * FROM users WHERE id = #{id}
</select>

```

`resultType`使用了别名`User`，MyBatis会将查询结果映射到`User`类的实例中。



#### 单个实体类型输出
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323515946-7c0601a7-d82d-4954-a64e-b35c90c1bcd5.png)

开启驼峰式自动映射

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323476878-957681a7-0d93-4b95-b0d9-f6b909e01dc9.png)





#### 返回 map
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323544503-8a2c937b-43d1-4335-81e3-c1cdc60ae350.png)

列名 -> key

map

结果 -> 值



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323732927-3e0cee0b-d11a-49ab-8ea8-03764c7d99bf.png)



#### 返回集合类型
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323693741-0da123ef-e065-4c0e-a314-af3e75499d86.png)

切记：返回值是集合 resultType 不需要指定集合类型，只需要指定泛型即可

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733323831900-9bfc1441-994e-43c7-b9f5-e4a1464f4b54.png)

底层是使用集合去查的，所以我们只需要指定泛型

#### 返回主键值
##### 自增长主键
主键回显 获取插入数据的主键

1.自增长逐渐回显 mysql out_increment

int inserEmp(Employee employee);

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733326780850-f34fb1c5-30c1-4c82-bb76-bbc521b19766.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733327530103-b02dda16-cecc-4d5b-8881-c51439a3671e.png)





##### 非自增长主键维护
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733327664174-9ce7abfb-c86a-4923-8119-6071cdec4bda.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733327776979-75237730-e5d5-4fab-b126-9347f5db93c9.png)

> 自己维护主键
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733327964355-d9657c83-9f1f-451f-a2da-85c0641c47bc.png)

> 非自增长的主键交给mybatis维护
>

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733328189925-b93ae6bd-f841-4bc2-9172-2ba159cdb51a.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733328218149-b7760fa5-3a44-4df6-aef6-0336eb88b134.png)

### MyBatis自定义映射关系和ResultMap
#### 什么是自定义映射关系？
在MyBatis中，自定义映射关系是指将数据库查询结果映射到Java对象的过程。MyBatis允许开发者通过XML配置或注解的方式，自定义查询结果与Java对象属性之间的映射关系。这种映射关系可以处理复杂的查询结果，如一对一、一对多、多对多等。

#### 什么是ResultMap？
ResultMap是MyBatis中用于定义自定义映射关系的核心组件。通过ResultMap，可以将查询结果中的列与Java对象的属性进行映射，从而实现复杂的映射关系。

#### ResultMap的基本使用
1. **定义ResultMap**  
在MyBatis的XML配置文件中定义ResultMap：

```xml
<resultMap id="userResultMap" type="com.example.model.User">
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <result property="email" column="user_email"/>
</resultMap>
```

在这个示例中，`userResultMap`定义了一个ResultMap，将查询结果中的`user_id`、`user_name`和`user_email`列分别映射到`User`对象的`id`、`name`和`email`属性。

1. **使用ResultMap**  
在Mapper文件中使用ResultMap：

```xml
<select id="selectUser" resultMap="userResultMap">
    SELECT user_id, user_name, user_email FROM users WHERE user_id = #{id}
</select>
```

在这个示例中，`selectUser`查询使用了`userResultMap`，将查询结果映射到`User`对象。

#### 复杂映射关系
1. **一对一映射**  
一对一映射是指一个对象包含另一个对象的情况。例如，用户对象包含地址对象：

```xml
<resultMap id="userResultMap" type="com.example.model.User">
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <association property="address" javaType="com.example.model.Address">
        <id property="id" column="address_id"/>
        <result property="street" column="address_street"/>
        <result property="city" column="address_city"/>
    </association>
</resultMap>
```

1. **一对多映射**  
一对多映射是指一个对象包含多个子对象的情况。例如，用户对象包含多个订单对象：

```xml
<resultMap id="userResultMap" type="com.example.model.User">
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <collection property="orders" ofType="com.example.model.Order">
        <id property="id" column="order_id"/>
        <result property="amount" column="order_amount"/>
        <result property="date" column="order_date"/>
    </collection>
</resultMap>
```

1. **多对多映射**  
多对多映射是指一个对象包含多个子对象，每个子对象又包含多个父对象的情况。例如，学生对象包含多个课程对象，课程对象也包含多个学生对象：

```xml
<resultMap id="studentResultMap" type="com.example.model.Student">
    <id property="id" column="student_id"/>
    <result property="name" column="student_name"/>
    <collection property="courses" ofType="com.example.model.Course">
        <id property="id" column="course_id"/>
        <result property="name" column="course_name"/>
    </collection>
</resultMap>
```

通过ResultMap，MyBatis可以灵活地处理各种复杂的映射关系，满足不同的业务需求。



### 列名和属性不一致的解决方案
在MyBatis中，当数据库列名和Java属性名不一致时，可以通过以下几种方案来解决映射问题：

#### 方案1：使用别名
通过在SQL查询中使用别名，将数据库列名映射到Java属性名。

```xml
<select id="selectTeacher" parameterType="int" resultType="Teacher">
    SELECT t.id AS tId, t.name AS tName FROM teacher WHERE t.id = #{tId}
</select>
```

在这个示例中，`t.id`被映射为`tId`，`t.name`被映射为`tName`。

#### 方案2：开启驼峰式映射
通过在MyBatis配置文件中开启驼峰式映射，将下划线命名的数据库列名自动映射为驼峰命名的Java属性名。

```xml
<settings>
    <setting name="mapUnderscoreToCamelCase" value="true"/>
</settings>
```

在这个示例中，数据库列名`tid`会自动映射为Java属性名`tId`。

#### 方案3：使用ResultMap自定义映射
通过ResultMap自定义映射关系，可以精确控制数据库列名和Java属性名的映射。`resultType`和`resultMap`二选一使用。

```xml
<!-- 声明ResultMap标签，自定义映射规则 -->
<resultMap id="teacherResultMap" type="Teacher">
    <id property="tId" column="id"/>
    <result property="tName" column="name"/>
</resultMap>

<!-- 使用ResultMap -->
<select id="queryById" resultMap="teacherResultMap">
    SELECT * FROM teacher WHERE id = #{tId}
</select>
```

在这个示例中，`teacherResultMap`定义了自定义映射规则，将数据库列`id`映射为Java属性`tId`，将数据库列`name`映射为Java属性`tName`。

#### 深层次对象结构映射
对于深层次的对象结构和多表查询，可以通过ResultMap进行复杂映射。

```xml
<resultMap id="orderResultMap" type="Order">
    <id property="orderId" column="order_id"/>
    <result property="orderName" column="order_name"/>
    <association property="orderItem" javaType="OrderItem">
        <id property="itemId" column="item_id"/>
        <result property="orderId" column="order_id"/>
        <result property="itemName" column="item_name"/>
    </association>
</resultMap>

<select id="selectOrder" resultMap="orderResultMap">
    SELECT o.order_id, o.order_name, i.item_id, i.order_id, i.item_name
    FROM orders o
    JOIN order_items i ON o.order_id = i.order_id
    WHERE o.order_id = #{orderId}
</select>
```

在这个示例中，`orderResultMap`定义了复杂的映射关系，将`Order`对象和`OrderItem`对象的属性与数据库列进行映射。



ResultMap标签，自定义映射关系，可以多层次，也可以单层次







#### 通过注解生成对应的方法
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733330245067-fd9e61f3-3b52-4fdf-a732-b39d337553f9.png)



*

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733330586788-30ee06fb-a71c-43c0-8714-e945f29b0bcf.png)



### MyBatis多表映射
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733330986656-bc939188-af3d-4af2-b197-4df689f782ba.png)

在MyBatis中，多表映射是指将多个数据库表的数据映射到Java对象中。多表映射通常用于处理复杂的查询结果，如一对一、一对多、多对多等关系。以下是一些常见的多表映射方式：

#### 一对一映射
一对一映射是指一个对象包含另一个对象的情况。例如，用户对象包含地址对象。

**示例**：

```xml
<resultMap id="userResultMap" type="com.example.model.User">
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <association property="address" javaType="com.example.model.Address">
        <id property="id" column="address_id"/>
        <result property="street" column="address_street"/>
        <result property="city" column="address_city"/>
    </association>
</resultMap>

<select id="selectUser" resultMap="userResultMap">
    SELECT u.user_id, u.user_name, a.address_id, a.address_street, a.address_city
    FROM users u
    JOIN addresses a ON u.address_id = a.address_id
    WHERE u.user_id = #{userId}
</select>
```

在这个示例中，`userResultMap`定义了用户和地址之间的一对一映射关系。

#### 一对多映射
一对多映射是指一个对象包含多个子对象的情况。例如，用户对象包含多个订单对象。

**示例**：

```xml
<resultMap id="userResultMap" type="com.example.model.User">
    <id property="id" column="user_id"/>
    <result property="name" column="user_name"/>
    <collection property="orders" ofType="com.example.model.Order">
        <id property="id" column="order_id"/>
        <result property="amount" column="order_amount"/>
        <result property="date" column="order_date"/>
    </collection>
</resultMap>

<select id="selectUser" resultMap="userResultMap">
    SELECT u.user_id, u.user_name, o.order_id, o.order_amount, o.order_date
    FROM users u
    JOIN orders o ON u.user_id = o.user_id
    WHERE u.user_id = #{userId}
</select>
```

在这个示例中，`userResultMap`定义了用户和订单之间的一对多映射关系。

#### 多对多映射
多对多映射是指一个对象包含多个子对象，每个子对象又包含多个父对象的情况。例如，学生对象包含多个课程对象，课程对象也包含多个学生对象。



##### 总结
对一 属性中包含对象方法

对多 属性中包含对象集合



**示例**：

```xml
<resultMap id="studentResultMap" type="com.example.model.Student">
    <id property="id" column="student_id"/>
    <result property="name" column="student_name"/>
    <collection property="courses" ofType="com.example.model.Course">
        <id property="id" column="course_id"/>
        <result property="name" column="course_name"/>
    </collection>
</resultMap>

<select id="selectStudent" resultMap="studentResultMap">
    SELECT s.student_id, s.student_name, c.course_id, c.course_name
    FROM students s
    JOIN student_courses sc ON s.student_id = sc.student_id
    JOIN courses c ON sc.course_id = c.course_id
    WHERE s.student_id = #{studentId}
</select>
```

在这个示例中，`studentResultMap`定义了学生和课程之间的多对多映射关系。

通过ResultMap，MyBatis可以灵活地处理各种复杂的映射关系，满足不同的业务需求.







![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733399694662-770e4e6b-ef5d-48a7-b243-f95f048093bd.png)只有双表查，没有多表查

若有多张表可以拆成双表

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733399948490-8faa932f-3e82-48a8-8e3f-65660db7f486.png)

### MyBatis动态语句
MyBatis动态语句允许开发者根据不同的条件动态生成SQL语句，从而提高查询的灵活性和可维护性。MyBatis提供了一系列的动态SQL标签，如`<if>`、`<choose>`、`<when>`、`<otherwise>`、`<trim>`、`<where>`、`<set>`和`<foreach>`，这些标签可以在Mapper XML文件中使用。

#### 常用动态SQL标签
1. `<if>`**标签**
    - 用于根据条件动态生成SQL片段。
    - 示例：

```xml
<select id="findUserById" parameterType="int" resultType="User">
    SELECT * FROM users
    <where>
        <if test="id != null">
            id = #{id}
        </if>
    </where>
</select>
```

1. `<choose>`**、**`<when>`**和**`<otherwise>`**标签**
    - 类似于Java中的`switch`语句，用于根据不同的条件生成不同的SQL片段。
    - 示例：

```xml
<select id="findUser" parameterType="map" resultType="User">
    SELECT * FROM users
    <where>
        <choose>
            <when test="id != null">
                id = #{id}
            </when>
            <when test="name != null">
                name = #{name}
            </when>
            <otherwise>
                1 = 1
            </otherwise>
        </choose>
    </where>
</select>
```

1. `<trim>`**标签**
    - 用于去除SQL片段的前后多余字符，如逗号、AND、OR等。
    - 示例：

```xml
<update id="updateUser" parameterType="User">
    UPDATE users
    <set>
        <trim suffixOverrides=",">
            <if test="name != null">name = #{name},</if>
            <if test="email != null">email = #{email},</if>
        </trim>
    </set>
    WHERE id = #{id}
</update>
```

1. `<where>`**标签**
    - 用于自动处理WHERE子句的AND/OR逻辑，避免SQL语句中出现多余的AND/OR。
    - 示例：

```xml
<select id="findUserByConditions" parameterType="map" resultType="User">
    SELECT * FROM users
    <where>
        <if test="id != null">id = #{id}</if>
        <if test="name != null">AND name = #{name}</if>
    </where>
</select>
```

1. `<set>`**标签**
    - 用于动态生成UPDATE语句中的SET子句，自动去除多余的逗号。
    - 示例：

```xml
<update id="updateUser" parameterType="User">
    UPDATE users
    <set>
        <if test="name != null">name = #{name},</if>
        <if test="email != null">email = #{email},</if>
    </set>
    WHERE id = #{id}
</update>
```

1. `<foreach>`**标签**
    - 用于遍历集合生成SQL片段，常用于IN查询和批量操作。
    - 示例：

```xml
<select id="findUsersByIds" parameterType="list" resultType="User">
    SELECT * FROM users
    WHERE id IN
    <foreach item="id" collection="list" open="(" separator="," close=")">
        #{id}
    </foreach>
</select>
```



### MyBatis动态SQL语句的使用
在MyBatis中，可以通过动态SQL语句来根据不同的条件生成不同的SQL查询。以下是如何使用动态SQL语句来实现条件查询的示例：

#### 示例方法
```java
List<Employee> query(@Param("name") String name, @Param("salary") Double salary);
```

如果传入属性，就判断相等；如果不传入，则不加对应的条件。

#### 动态SQL语句
使用`<where>`标签和`<if>`标签来实现动态SQL语句：

```xml
<select id="query" resultType="Employee">
    SELECT * FROM employee
    <where>
        <if test="name != null">
            emp_name = #{name}
        </if>
        <if test="salary != null and salary &gt; 100">
            AND emp_salary = #{salary}
        </if>
    </where>
</select>
```

#### 解释
1. `<where>`**标签的作用**：
    - 自动添加`WHERE`关键字：如果`<where>`标签内部有任何一个`<if>`条件满足，则自动添加`WHERE`关键字；如果不满足，则去掉`WHERE`。
    - 自动去掉多余的`AND`和`OR`关键字：`<where>`标签会自动处理多余的`AND`和`OR`关键字，确保生成的SQL语句是正确的。
1. `<if>`**标签的作用**：
    - 判断传入的参数，最终是否添加语句。
    - `test`属性内部做比较运算，如果结果为`true`，则将标签内的SQL语句进行拼接；如果为`false`，则不拼接标签内部语句。

#### 注意事项
+ **大于和小于符号**：不推荐直接写符号，可以使用HTML实体符号，如`&gt;`（大于）和`&lt;`（小于）。
+ **避免错误的SQL语句**：确保`<if>`标签内部的条件判断正确，避免生成错误的SQL语句。例如，如果第一个条件不满足，而第二个条件满足，则会生成错误的SQL语句`WHERE AND emp_salary = #{salary}`。

通过使用动态SQL语句，可以根据不同的条件生成灵活的查询语句，提高查询的灵活性和可维护性。



### MyBatis中的动态SQL标签
MyBatis提供了一系列动态SQL标签，用于根据不同的条件动态生成SQL语句。以下是一些常用的动态SQL标签及其用法：

#### 1. `<set>`标签
+ **用途**：用于动态生成`UPDATE`语句中的`SET`子句，自动去除多余的逗号。
+ **示例**：

```xml
<update id="updateUser" parameterType="User">
    UPDATE users
    <set>
        <if test="name != null">name = #{name},</if>
        <if test="email != null">email = #{email},</if>
    </set>
    WHERE id = #{id}
</update>
```

在这个示例中，`<set>`标签会根据条件动态生成`SET`子句，并自动去除多余的逗号。

#### 2. `<trim>`标签
+ **用途**：用于去除SQL片段的前后多余字符，如逗号、AND、OR等。
+ **属性**：
    - `prefix`：在生成的SQL片段前添加的字符串。
    - `suffix`：在生成的SQL片段后添加的字符串。
    - `prefixOverrides`：去除生成的SQL片段前的指定字符。
    - `suffixOverrides`：去除生成的SQL片段后的指定字符。
+ **示例**：

```xml
<update id="updateUser" parameterType="User">
    UPDATE users
    <trim prefix="SET" suffixOverrides=",">
        <if test="name != null">name = #{name},</if>
        <if test="email != null">email = #{email},</if>
    </trim>
    WHERE id = #{id}
</update>
```

在这个示例中，`<trim>`标签会在生成的SQL片段前添加`SET`，并去除多余的逗号。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733402384573-e266a84c-43ae-4ac6-90d2-62c83e36a8b6.png)

#### 3. `<choose>`、`<when>`和`<otherwise>`标签
+ **用途**：类似于Java中的`switch`语句，用于根据不同的条件生成不同的SQL片段。
+ **示例**：

```xml
<select id="findUser" parameterType="map" resultType="User">
    SELECT * FROM users
    <where>
        <choose>
            <when test="id != null">
                id = #{id}
            </when>
            <when test="name != null">
                name = #{name}
            </when>
            <otherwise>
                1 = 1
            </otherwise>
        </choose>
    </where>
</select>
```

在这个示例中，`<choose>`标签会根据不同的条件生成不同的SQL片段。

它和if的区别，这个只能一个满足，if可以多个

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733402505620-960980fa-a998-44b0-be98-c4fc9d99b304.png)

#### 4. `<foreach>`标签
+ **用途**：用于遍历集合生成SQL片段，常用于IN查询和批量操作。
+ **属性**：
    - `item`：集合中每个元素的别名。
    - `collection`：要遍历的集合。
    - `open`：在生成的SQL片段前添加的字符串。
    - `separator`：在生成的SQL片段之间添加的分隔符。
    - `close`：在生成的SQL片段后添加的字符串。
+ **示例**：

```xml
<select id="findUsersByIds" parameterType="list" resultType="User">
    SELECT * FROM users
    WHERE id IN
    <foreach item="id" collection="list" open="(" separator="," close=")">
        #{id}
    </foreach>
</select>
```

在这个示例中，`<foreach>`标签会遍历集合`list`，生成`IN`查询的SQL片段。



在数据库url后面加?allowMultiQueries=true允许多语句执行

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733403775364-ec20c015-607c-4806-8db5-8cda7295b1c6.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733403799449-dcc319af-88a1-4a79-b442-fb6d8c8d0e3a.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733403814251-660d1e7f-857f-4d63-bab5-350334333d7c.png)

update把整体的更新语句都遍历一遍，注意，要先允许多语句执行



### MyBatis中的SQL片段
在MyBatis中，SQL片段（SQL Fragments）是一种用于重用SQL代码的机制。通过定义和引用SQL片段，可以避免重复编写相同的SQL代码，提高代码的可维护性和可读性。SQL片段通常使用`<sql>`和`<include>`标签来定义和引用。

#### 定义SQL片段
使用`<sql>`标签定义一个SQL片段。`<sql>`标签通常放在Mapper XML文件的顶部。

```xml
<sql id="userColumns">
    user_id, user_name, user_email
</sql>
```

在这个示例中，定义了一个名为`userColumns`的SQL片段，包含了用户表的三个列名。

#### 引用SQL片段
使用`<include>`标签引用一个SQL片段。`<include>`标签可以放在任何需要引用SQL片段的地方。

```xml
<select id="selectUser" resultType="User">
    SELECT <include refid="userColumns"/>
    FROM users
    WHERE user_id = #{id}
</select>
```

在这个示例中，使用`<include>`标签引用了`userColumns` SQL片段，从而避免了重复编写列名。

#### 动态SQL片段
SQL片段也可以包含动态SQL标签，如`<if>`、`<choose>`等，从而实现更复杂的SQL重用。

```xml
<sql id="dynamicUserColumns">
    user_id,
    <if test="includeName">
        user_name,
    </if>
    user_email
</sql>

<select id="selectUser" resultType="User">
    SELECT <include refid="dynamicUserColumns"/>
    FROM users
    WHERE user_id = #{id}
</select>
```

在这个示例中，`dynamicUserColumns` SQL片段包含了一个动态SQL标签`<if>`，根据条件决定是否包含`user_name`列。



### MyBatis Mapper按包批量扫描
在MyBatis中，Mapper按包批量扫描是一种简化配置的方式，通过指定包路径，自动扫描并注册Mapper接口。这样可以避免手动一个一个地配置Mapper接口，提高开发效率。

#### 配置步骤
建议使用第二种，上下创建相同结构的配置文件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733404302179-8bc75a00-aac7-4a1b-b4df-e154e307f5d3.png)

注意，创建的时候要写斜杠，不然就是一个文件夹

编译产物

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733404460236-c00cfa51-a83a-4fc1-b506-fa72ff8b2e21.png)

1. **引入依赖**  
在项目的`pom.xml`文件中添加MyBatis和Spring Boot相关的依赖：

```xml
<dependencies>
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>2.2.0</version>
    </dependency>
</dependencies>
```

1. **配置Mapper扫描**  
在Spring Boot配置类中使用`@MapperScan`注解，指定Mapper接口所在的包路径：

```java
@SpringBootApplication
@MapperScan("com.example.mapper")
public class MyBatisApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyBatisApplication.class, args);
    }
}
```

1. **定义Mapper接口**  
在指定的包路径下定义Mapper接口，并使用MyBatis的注解或XML文件配置SQL语句：

```java
@Mapper
public interface UserMapper {
    @Select("SELECT * FROM users WHERE id = #{id}")
    User selectUser(int id);
}
```

1. **使用Mapper接口**  
在Service类中注入Mapper接口，并调用其方法：

```java
@Service
public class UserService {
    @Autowired
    private UserMapper userMapper;

    public User getUserById(int id) {
        return userMapper.selectUser(id);
    }
}
```

通过以上配置，Spring Boot会自动扫描`com.example.mapper`包下的所有Mapper接口，并将其注册为Spring Bean，从而简化了Mapper接口的配置过程。



### MyBatis插件机制
MyBatis插件机制允许开发者通过编写插件来拦截和修改MyBatis的核心行为，如SQL执行、参数处理和结果映射等。插件机制使得MyBatis具有很高的可扩展性，能够满足各种复杂的业务需求。

#### 插件的基本原理
MyBatis插件通过实现`Interceptor`接口，并使用`@Intercepts`和`@Signature`注解来定义拦截点。拦截点可以是MyBatis的四种核心对象的方法：

1. **Executor**：执行器，负责SQL语句的执行。
2. **ParameterHandler**：参数处理器，负责SQL参数的处理。
3. **ResultSetHandler**：结果集处理器，负责结果集的处理。
4. **StatementHandler**：语句处理器，负责SQL语句的预处理。

#### 插件的实现步骤
1. **实现**`Interceptor`**接口**

```java
@Intercepts({
    @Signature(type = Executor.class, method = "update", args = {MappedStatement.class, Object.class}),
    @Signature(type = Executor.class, method = "query", args = {MappedStatement.class, Object.class, RowBounds.class, ResultHandler.class})
})
public class MyPlugin implements Interceptor {
    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        // 在这里编写拦截逻辑
        return invocation.proceed();
    }

    @Override
    public Object plugin(Object target) {
        return Plugin.wrap(target, this);
    }

    @Override
    public void setProperties(Properties properties) {
        // 设置插件属性
    }
}
```

1. **注册插件**  
在MyBatis配置文件中注册插件：

```xml
<plugins>
    <plugin interceptor="com.example.MyPlugin">
        <property name="someProperty" value="value"/>
    </plugin>
</plugins>
```

### PageHelper分页插件
PageHelper是一个MyBatis的分页插件，能够简化分页查询的实现。它通过拦截SQL语句，在执行查询前后自动添加分页逻辑，从而实现分页功能。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733404730214-d70f6a26-2a4d-457b-aa61-65b993e0f301.png)

#### PageHelper的使用步骤
1. **引入依赖**  
在项目的`pom.xml`文件中添加PageHelper的依赖：

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.13</version>
</dependency>
```

1. **配置PageHelper**  
在Spring Boot配置类中配置PageHelper：

```java
@Configuration
public class MyBatisConfig {
    @Bean
    public PageHelper pageHelper() {
        PageHelper pageHelper = new PageHelper();
        Properties properties = new Properties();
        properties.setProperty("helperDialect", "mysql");
        properties.setProperty("reasonable", "true");
        properties.setProperty("supportMethodsArguments", "true");
        properties.setProperty("params", "count=countSql");
        pageHelper.setProperties(properties);
        return pageHelper;
    }
}
```

1. **使用PageHelper进行分页查询**  
在Service层或Mapper接口中使用PageHelper进行分页查询：

```java
@Service
public class UserService {
    @Autowired
    private UserMapper userMapper;

    public PageInfo<User> getUsers(int pageNum, int pageSize) {
        PageHelper.startPage(pageNum, pageSize);
        List<User> users = userMapper.selectAll();
        return new PageInfo<>(users);
    }
}
```

通过以上配置和代码，PageHelper会自动拦截SQL语句，并在执行查询前后添加分页逻辑，从而实现分页功能。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733405051043-965c7ce5-10ce-43f4-9364-1969e288ccb5.png)

注意：正常编写语句即可，切记不要写分号结尾



### MyBatis的ORM介绍和逆向工程
#### 什么是ORM？
ORM（Object-Relational Mapping，面向对象关系映射）是一种技术，用于在面向对象编程语言（如Java、C#）和关系数据库之间建立映射关系。ORM通过将数据库中的表映射为编程语言中的类，将表中的记录映射为类的实例，从而简化了数据库操作，使开发者可以使用面向对象的方式来操作数据库。

#### ORM的优点
1. **提高开发效率**：通过自动生成SQL语句，减少了手动编写SQL的工作量。
2. **增强可维护性**：通过面向对象的方式操作数据库，使代码更加清晰、易于维护。
3. **减少错误**：通过自动生成SQL语句，减少了手动编写SQL时可能出现的错误。
4. **跨数据库支持**：ORM框架通常支持多种数据库，使得应用程序可以更容易地切换数据库。

#### 常见的ORM框架
1. **Hibernate**：一个流行的Java ORM框架，提供了强大的映射功能和丰富的配置选项。
2. **MyBatis**：一个半自动化的ORM框架，允许开发者手动编写SQL语句，同时提供了自动映射功能。
3. **Entity Framework**：一个用于.NET的ORM框架，提供了强大的数据库操作功能。

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733405878730-10493609-0f23-499b-8495-34c2829ed2e7.png)

### MyBatis逆向工程
#### 什么是逆向工程？
逆向工程（Reverse Engineering）是一种技术，通过分析现有的系统或代码，生成相应的设计文档或模型。在数据库开发中，逆向工程通常指的是从现有的数据库结构生成相应的代码，如实体类、Mapper接口等。

#### MyBatis逆向工程
MyBatis提供了逆向工程工具，可以根据数据库表结构自动生成相应的实体类、Mapper接口和XML配置文件，从而简化开发过程。

#### 使用MyBatis逆向工程的步骤
1. **引入依赖**  
在项目的`pom.xml`文件中添加MyBatis逆向工程相关的依赖：

```xml
<dependency>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-core</artifactId>
    <version>1.4.0</version>
</dependency>
```

1. **配置逆向工程**  
创建一个逆向工程配置文件`generatorConfig.xml`，配置数据库连接信息和生成代码的路径：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
    PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
    "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <context id="MySQLTables" targetRuntime="MyBatis3">
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        connectionURL="jdbc:mysql://localhost:3306/mydatabase"
                        userId="root"
                        password="password"/>
        <javaModelGenerator targetPackage="com.example.model" targetProject="src/main/java"/>
        <sqlMapGenerator targetPackage="mapper" targetProject="src/main/resources"/>
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.example.mapper" targetProject="src/main/java"/>
        <table tableName="users"/>
    </context>
</generatorConfiguration>
```

1. **运行逆向工程**  
使用MyBatis Generator插件运行逆向工程，生成相应的代码：

```shell
mvn mybatis-generator:generate
```

通过以上步骤，MyBatis逆向工程工具会根据数据库表结构自动生成相应的实体类、Mapper接口和XML配置文件，从而简化开发过程.



#### 我们可以直接在idea中安装逆向插件
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733406194344-26d7bf3c-856b-4b61-adcf-3951e3d00e6f.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733406411721-231441b5-baf7-4d71-91e8-6d944a7dd1e3.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733406286848-673ad9f8-bbcd-460f-927d-887901840c4e.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733406429822-b9fff3ad-de0a-4d6d-b442-8e56aede94b6.png)

自动生成的

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733406373740-a8beaf0b-43b6-4a41-9471-b7e12fe7ddfa.png)





![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1733405951223-0695d6bf-67c4-4f37-bcdc-5981e40ec480.png)

半自动，单表自动生成mapper接口和xml文件配置

