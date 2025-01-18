SSM整合通常指的是Spring + Spring MVC + MyBatis的整合，是Java Web开发中常用的技术组合。

1. **Spring Framework**: 提供了依赖注入（DI）和面向切面编程（AOP）等特性，能够简化Java应用的开发。
2. **Spring MVC**: 是基于Spring的Web框架，提供了MVC模式的实现，用于构建Web应用程序。
3. **MyBatis**: 是一个优秀的持久层框架，通过XML或注解方式配置SQL映射，可以很方便地操作数据库。

整合SSM的步骤一般如下：

### 1. 配置Spring
+ 配置Spring的核心配置文件（如`applicationContext.xml`），包括数据源配置、事务管理等。

### 2. 配置Spring MVC
+ 配置Spring MVC的`DispatcherServlet`，配置视图解析器、处理器映射等。

### 3. 配置MyBatis
+ 配置MyBatis的`SqlSessionFactory`，设置数据源、mapper文件位置等。

### 4. 编写业务逻辑和持久层代码
+ 在Spring中配置Service层和DAO层的Bean，编写业务逻辑和数据访问代码。

### 5. 编写Controller
+ 使用Spring MVC编写Controller处理用户请求，调用Service层完成业务逻辑。

### 6. 编写Mapper接口和XML文件
+ 编写MyBatis的Mapper接口和对应的XML文件，定义SQL语句和映射关系。



### 示例
### 1. **项目结构**
```plain
src/main/java
├── com.example.config
│   ├── AppConfig.java         # Spring核心配置
│   ├── WebConfig.java         # Spring MVC配置
│   └── MyBatisConfig.java     # MyBatis配置
├── com.example.controller
│   └── UserController.java    # Controller层
├── com.example.service
│   └── UserService.java       # Service接口
│   └── UserServiceImpl.java   # Service实现
├── com.example.mapper
│   └── UserMapper.java        # MyBatis Mapper接口
└── com.example.model
    └── User.java              # 数据模型类
```

### 2. **Spring核心配置 (**`**AppConfig.java**`**)**
```java
package com.example.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.annotation.EnableTransactionManagement;

import javax.sql.DataSource;
import org.apache.commons.dbcp2.BasicDataSource;

@Configuration
@ComponentScan(basePackages = "com.example")
@EnableTransactionManagement
public class AppConfig {

    @Bean
    public DataSource dataSource() {
        BasicDataSource dataSource = new BasicDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/mydb");
        dataSource.setUsername("root");
        dataSource.setPassword("password");
        return dataSource;
    }

    @Bean
    public DataSourceTransactionManager transactionManager(DataSource dataSource) {
        return new DataSourceTransactionManager(dataSource);
    }
}
```

### 3. **Spring MVC配置 (**`**WebConfig.java**`**)**
```java
package com.example.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.ViewResolver;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
import org.springframework.web.servlet.view.InternalResourceViewResolver;

@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Bean
    public ViewResolver viewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        return resolver;
    }
}
```

### 4. **MyBatis配置 (**`**MyBatisConfig.java**`**)**
```java
package com.example.config;

import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.annotation.MapperScan;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;

@Configuration
@MapperScan("com.example.mapper")
public class MyBatisConfig {

    @Bean
    public SqlSessionFactory sqlSessionFactory(DataSource dataSource) throws Exception {
        SqlSessionFactoryBean sessionFactory = new SqlSessionFactoryBean();
        sessionFactory.setDataSource(dataSource);
        return sessionFactory.getObject();
    }
}
```

### 5. **业务逻辑层 (**`**UserService.java**`** 和 **`**UserServiceImpl.java**`**)**
```java
package com.example.service;

public interface UserService {
    User getUserById(int id);
}

package com.example.service;

import com.example.mapper.UserMapper;
import com.example.model.User;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserServiceImpl implements UserService {

    @Autowired
    private UserMapper userMapper;

    @Override
    public User getUserById(int id) {
        return userMapper.findUserById(id);
    }
}
```

### 6. **Controller层 (**`**UserController.java**`**)**
```java
package com.example.controller;

import com.example.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/user")
    public String getUser(@RequestParam("id") int id, Model model) {
        model.addAttribute("user", userService.getUserById(id));
        return "user";
    }
}
```

### 7. **Mapper接口 (**`**UserMapper.java**`**)**
```java
package com.example.mapper;

import com.example.model.User;
import org.apache.ibatis.annotations.Select;

public interface UserMapper {
    @Select("SELECT * FROM users WHERE id = #{id}")
    User findUserById(int id);
}
```

### 8. **数据模型 (**`**User.java**`**)**
```java
package com.example.model;

public class User {
    private int id;
    private String name;
    private String email;

    // Getters and Setters
}
```

### 9. **配置Servlet初始化**
```java
package com.example.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

public class MyWebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class<?>[]{AppConfig.class, MyBatisConfig.class};
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class<?>[]{WebConfig.class};
    }

    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
}
```

### 
