SpringMVC内部工作流程

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736452608640-aab129c3-e24b-4923-b71b-ed65a3dfb7d4.png)

SpringMVC 的内部工作流程可以分为以下几个步骤：

1. **用户请求**：用户通过浏览器发送一个 HTTP 请求到服务器。
2. **DispatcherServlet**：请求首先到达 DispatcherServlet，这是 SpringMVC 的核心组件。它负责将请求分发到相应的处理器。
3. **HandlerMapping**：DispatcherServlet 调用 HandlerMapping 来确定哪个 Controller 处理这个请求。HandlerMapping 根据请求的 URL 找到合适的 Controller。
4. **Controller**：找到合适的 Controller 后，DispatcherServlet 将请求转发给这个 Controller。Controller 处理请求，调用业务逻辑（Model），并返回视图名和模型数据。
5. **Model**：Controller 调用 Model 来处理数据，并将结果返回给视图。Model 包含应用程序的数据和业务逻辑。
6. **ViewResolver**：DispatcherServlet 调用 ViewResolver 将视图名解析为实际的视图对象。ViewResolver 根据视图名找到相应的视图模板，并将模型数据传递给视图。
7. **View**：视图对象生成最终的 HTML 页面，并将其返回给用户。视图负责将模型数据展示给用户，通常是 JSP、Thymeleaf 等模板引擎生成的 HTML 页面。
8. **响应用户**：最终生成的 HTML 页面通过 HTTP 响应返回给用户的浏览器，用户可以看到处理后的结果。



#### 下面是一个 springmvc 的例子
![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736513872125-e82a4653-07ee-4dd9-99ab-dbd679b0411c.png)

作为父工程，我们先删除 src，再编辑它的依赖

#####  导入springmvc需要的依赖
        web servlet

        ioc spring-context

        mvc spring-webmvc



```plain

```

```plain
<!--
    导入springmvc需要的依赖
        web servlet
        ioc spring-context
        mvc spring-webmvc
-->
<properties>
    <spring.version>6.0.6</spring.version>
    <servlet.api>9.1.0</servlet.api>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>

<dependencies>
    <!-- springioc相关依赖  -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>

    <!-- web相关依赖  -->
    <!-- 在 pom.xml 中引入 Jakarta EE Web API 的依赖 -->
    <!--
        在 Spring Web MVC 6 中，Servlet API 迁移到了 Jakarta EE API，因此在配置 DispatcherServlet 时需要使用
         Jakarta EE 提供的相应类库和命名空间。错误信息 “‘org.springframework.web.servlet.DispatcherServlet’
         is not assignable to ‘javax.servlet.Servlet,jakarta.servlet.Servlet’” 表明你使用了旧版本的
         Servlet API，没有更新到 Jakarta EE 规范。
    -->
    <dependency>
        <groupId>jakarta.platform</groupId>
        <artifactId>jakarta.jakartaee-web-api</artifactId>
        <version>${servlet.api}</version>
        <scope>provided</scope>
    </dependency>

    <!-- springwebmvc相关依赖  -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>

</dependencies>
```

（完整的配置文件）

```plain
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.eu.adouzi</groupId>
    <artifactId>ssm-springmvc-part</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>pom</packaging>


    <!--
        导入springmvc需要的依赖
            web servlet
            ioc spring-context
            mvc spring-webmvc
    -->
    <properties>
        <spring.version>6.0.6</spring.version>
        <servlet.api>9.1.0</servlet.api>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- springioc相关依赖  -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>

        <!-- web相关依赖  -->
        <!-- 在 pom.xml 中引入 Jakarta EE Web API 的依赖 -->
        <!--
            在 Spring Web MVC 6 中，Servlet API 迁移到了 Jakarta EE API，因此在配置 DispatcherServlet 时需要使用
             Jakarta EE 提供的相应类库和命名空间。错误信息 “‘org.springframework.web.servlet.DispatcherServlet’
             is not assignable to ‘javax.servlet.Servlet,jakarta.servlet.Servlet’” 表明你使用了旧版本的
             Servlet API，没有更新到 Jakarta EE 规范。
        -->
        <dependency>
            <groupId>jakarta.platform</groupId>
            <artifactId>jakarta.jakartaee-web-api</artifactId>
            <version>${servlet.api}</version>
            <scope>provided</scope>
        </dependency>

        <!-- springwebmvc相关依赖  -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>${spring.version}</version>
        </dependency>

    </dependencies>

</project>
```

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736513850891-69a9931f-e18d-4019-a744-36249ae189fa.png)

新建一个模块，使用插件将它转化成 web 工程

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736514117217-9b32ba54-a23a-4b52-b044-effd69ecbf78.png)

新建类HelloControll

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736514547007-b24e621f-d7ab-47f8-a8c4-14d69efb0a66.png)

```plain
package org.eu.adouzi.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
 * Hello 控制器
 *
 * @author shiraayano
 * @date 2025/01/10 21:01
 */
@Controller
public class HelloController {
    /**
     * 你好
     *
     * @return {@link String}
     */
    //定义handler
    //handler -> spring/hello return "hello"
    @RequestMapping("springmvc/hello")//对外访问的地址 也是到handler注册的注解
    @ResponseBody//直接然会字符串给前端,不找字符解析器
    public String hello() {
        System.out.println("hello handler method is running...");
        return "hello";
        //hello会返回给前端
    }
}
```



创建 config 包，在包下创建配置类 MvcConfig

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736514930820-ee1b21b6-556d-40d5-b7ec-36c467121bc8.png)

```plain
package org.eu.adouzi.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter;
import org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping;

/**
 * MVC 配置
 *
 * @author shiraayano
 * @date 2025/01/10 21:15
 * 
 * 将controller扫描到spring容器中
 * 将handlerMapping handlerAdapter 扫描到spring容器中
 */

@Configuration
@ComponentScan("org.eu.adouzi.controller")
public class MvcConfig {
    @Bean
    public RequestMappingHandlerMapping handlerMapping(){
        return new RequestMappingHandlerMapping();
    }
    @Bean
    public RequestMappingHandlerAdapter handlerAdapter(){
        return new RequestMappingHandlerAdapter();
    }
    
    
}
```

SpringMVC 对外提供有接口是替代 web.xml 

创建**SpringMvcInit 类**

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736515493408-80da3022-a05f-4b66-86a6-05c8da6f1ba1.png)

生成实现方法

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736515661340-fa980c20-09b3-4603-8bdb-be332c03655a.png)

```plain
package org.eu.adouzi.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

/**
 * Spring MVC 初始化
 *
 * @author shiraayano
 * @date 2025/01/10 21:27
 */
public class SpringMvcInit extends AbstractAnnotationConfigDispatcherServletInitializer {

    /**
     * 获取根配置类
     *
     * @return {@link Class<?>[]}
     */
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    /**
     * 获取 Servlet 配置类
     *
     * @return {@link Class<?>[]}
     */
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[0];
    }

    /**
     * 获取 Servlet 映射
     *
     * @return {@link String[]}
     */
    @Override
    protected String[] getServletMappings() {
        return new String[0];
    }
}
```

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736516052667-c44644f9-01be-4536-a466-064eb0b35a1c.png)

```plain
package org.eu.adouzi.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

/**
 * Spring MVC 初始化
 *
 * @author shiraayano
 * @date 2025/01/10 21:27
 */
public class SpringMvcInit extends AbstractAnnotationConfigDispatcherServletInitializer {

    /**
     * 获取根配置类
     *
     * @return {@link Class<?>[]}
     */

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    /**
     * 获取 Servlet 配置类
     *
     * @return {@link Class<?>[]}
     */
    //设置我们项目对应的配置类
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[] {MvcConfig.class};
    }

    /**
     * 获取 Servlet 映射
     *
     * @return {@link String[]}
     */
    //配置springmvc内部自带的servlet的访问地址
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};//允许全部
    }
}
```



编辑运行调试配置，添加 tomcat

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736516643459-7095c39e-f00a-4c32-b1ce-b5e7f7179066.png)

部署项目

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736516706748-33fded43-eca8-4b97-81a6-a6d45ab27d40.png)

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736516751125-153473c1-31b1-44d4-bcbb-e9b724d3f312.png)





运行...报错

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736517776402-74938984-6011-46de-8b0e-ce125b6b61a8.png)

看起来像是 jdk 版本高了

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1736518118677-14b58319-e861-4134-aa73-e7b0762d60b3.png)







总结

1.正常申明 Controller 方法

```plain
package org.eu.adouzi.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
 * Hello 控制器
 *
 * @author shiraayano
 * @date 2025/01/10 21:01
 */
@Controller
public class HelloController {
    /**
     * 你好
     *
     * @return {@link String}
     */
    //定义handler
    //handler -> spring/hello return "hello"
    @RequestMapping("springmvc/hello")//对外访问的地址 也是到handler注册的注解
    @ResponseBody//直接然会字符串给前端,不找字符解析器
    public String HelloController() {
        System.out.println("hello handler method is running...");
        return "hello";
        //hello会返回给前端
    }
}
```

2.写一个配置类，指定 HandlerMapping 和 HandlerAdapter，以及将 Handler 对应的 Controller 放入 ioc 容器

```plain
package org.eu.adouzi.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter;
import org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping;

/**
 * MVC 配置
 *
 * @author shiraayano
 * @date 2025/01/10 21:15
 *
 * 将controller扫描到spring容器中
 * 将handlerMapping handlerAdapter 扫描到spring容器中
 */

@Configuration
@ComponentScan("org.eu.adouzi.controller")
public class MvcConfig {
    @Bean
    public RequestMappingHandlerMapping handlerMapping(){
        return new RequestMappingHandlerMapping();
    }
    @Bean
    public RequestMappingHandlerAdapter handlerAdapter(){
        return new RequestMappingHandlerAdapter();
    }
    

}
```

3.按照 springmvc 的约定固定写一个类去继承 AbstractAnnotationConfigDispatcherServletInitializer

(只要继承这个类，项目启动的时候就会被加载)

```plain
package org.eu.adouzi.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

/**
 * Spring MVC 初始化
 *
 * @author shiraayano
 * @date 2025/01/10 21:27
 */
public class SpringMvcInit extends AbstractAnnotationConfigDispatcherServletInitializer {

    /**
     * 获取根配置类
     *
     * @return {@link Class<?>[]}
     */

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }

    /**
     * 获取 Servlet 配置类
     *
     * @return {@link Class<?>[]}
     */
    //设置我们项目对应的配置类
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[] {MvcConfig.class};
    }

    /**
     * 获取 Servlet 映射
     *
     * @return {@link String[]}
     */
    //配置springmvc内部自带的servlet的访问地址 （设置拦截路径）
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};//拦截全部
    }
}
```

