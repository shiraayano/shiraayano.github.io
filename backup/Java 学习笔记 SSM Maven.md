---

# SSM 学习路线
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732592789529-bd202c5e-aa1b-49a6-a86f-0eae2faad248.png)

**课程笔记**：  
[https://www.wolai.com/fbnhGx8eE9JfZugFpbCWmC](https://www.wolai.com/fbnhGx8eE9JfZugFpbCWmC)

---

## Maven简介
### 什么是Maven？
Maven 是一个基于 Java 的项目管理和构建工具，通过项目对象模型（POM, Project Object Model）描述项目的构建过程，涵盖编译、测试、打包等阶段，提供了丰富的插件和依赖机制，实现对 Java 项目的自动化管理。

### 为什么需要Maven？
在 Java 开发中，处理大量依赖库和复杂的构建过程十分耗时。Maven 提供了一种约定大于配置的规范化管理方式，简化项目构建，提升效率和可维护性。

### Maven的核心功能
1. **依赖管理**：通过中央仓库和本地仓库获取第三方库，方便版本控制。
2. **自动化构建**：内置生命周期，提供多种插件支持打包、测试、部署等任务。
3. **规范化项目结构**：统一项目结构，方便团队协作。
4. **代码质量管理**：支持代码质量分析和测试覆盖率检查。

### Maven的基本使用
1. **安装与配置**：
    - 下载 Maven：[Maven 官网](https://maven.apache.org/index.html)
    - 配置系统环境变量，将 Maven 添加到 `PATH` 中。
2. **项目结构**： Maven 推荐以下目录结构：

```plain
myproject/
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   └── resources
    └── test
        ├── java
        └── resources
```

3. **生命周期**： Maven 包括三个生命周期：
    - **clean**：清理项目。
    - **default**：核心生命周期，涵盖编译到部署。
    - **site**：生成项目文档。
4. **依赖管理**： 在 `pom.xml` 文件中声明依赖：

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

---

### 配置环境变量
下载 [Maven](https://maven.apache.org/download.cgi)，配置以下步骤：

1. 添加 Maven 的 bin 目录到系统 `PATH`。
2. 验证配置：在命令行运行 `mvn -v`，显示版本信息即成功。

**示例截图**：  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732592202124-781729dd-0028-48c5-a20b-bacb7ed17ea6.png)  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732592262220-b60f52ae-00b9-4b95-8d4b-b548a3932f6f.png)  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732592184877-7869738e-300a-44f9-89c3-268b16e1559f.png)

---

### 配置 Maven
需要修改 `maven/conf/settings.xml` 文件，主要配置以下三项：

#### 1. 配置本地仓库地址
```xml
<!-- 在 conf/settings.xml 的 55 行附近 -->
<localRepository>D:\repository</localRepository>
```

**示例截图**：  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732608090048-3789daa7-dc92-4f07-8672-66161671070e.png)

#### 2. 配置国内阿里镜像
```xml
<!-- 在 mirrors 节点下添加中央仓库镜像（160 行附近） -->
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```

**示例截图**：  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732608205979-592b430b-6948-40e5-8674-9f1b49e5fb6b.png)

#### 3. 配置 JDK 17 项目构建
```xml
<!-- 在 profiles 节点下添加 JDK 配置（268 行附近） -->
<profile>
    <id>jdk-17</id>
    <activation>
        <activeByDefault>true</activeByDefault>
        <jdk>17</jdk>
    </activation>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <maven.compiler.compilerVersion>17</maven.compiler.compilerVersion>
    </properties>
</profile>
```

**示例截图**：  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732608273473-2c87e491-a11b-4044-9c4a-43da89b52aec.png)

---

### 建议使用自定义 Maven 配置
在 IDEA 中：

1. 选择菜单 **文件 - 构建工具 - Maven**。
2. 手动设置 Maven 的自定义路径。

**示例截图**：  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732608480318-7b52eeb1-c021-465e-8684-e0c0dca36091.png)  
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732608601611-08b25a56-0180-41db-8183-b087dc4e0027.png)






## 基于IDEA的Maven工程创建

###  梳理Maven工程GAVP属性

Maven工程相对之前的工程，多出一组GAVP属性。GAV需要在创建项目时指定，P有默认值，后期可通过配置文件修改。以下是GAVP属性的详细说明：

Maven中的GAVP是指 **GroupId**、**ArtifactId**、**Version**、**Packaging** 等四个属性的缩写。其中前三个是必要的，而Packaging为可选项。这些属性用于为每个项目在Maven仓库中创建一个唯一标识，方便管理和引用。

#### GAV规则：
1. **GroupId 格式**：  
   格式为 `com.{公司/BU}.业务线.[子业务线]`，最多4级。  
   - 示例：`com.taobao.tddl`，`com.alibaba.sourcing.multilang`，`com.atguigu.java`。

2. **ArtifactId 格式**：  
   语义清晰不重复，通常为产品线名-模块名。  
   - 示例：`tc-client`，`uic-api`，`tair-tool`，`bookstore`。

3. **Version 格式**：  
   推荐格式为 `主版本号.次版本号.修订号`（如：1.0.0）。  
   - 主版本号：不兼容的API修改或重大功能增加。  
   - 次版本号：向下兼容的功能新增。  
   - 修订号：Bug修复或兼容性增强。  
   - 示例：初始版本→`1.0.0`，Bug修复→`1.0.1`，功能调整→`1.1.1`。

4. **Packaging 定义规则**：  
   - `jar`（默认值）：普通Java工程，打包为`.jar`文件。  
   - `war`：Java Web工程，打包为`.war`文件。  
   - `pom`：父工程，不生成打包文件。

---

### 使用IDEA构建Maven JavaSE工程

#### 注意：
省略了 `<version>`，默认值为 `<version>1.0-SNAPSHOT</version>`，后期可随意修改。

![JavaSE工程示例](https://secure2.wostatic.cn/static/oDo2HDrVXHoKqfqRdqLKuV/image.png)

---

### 使用IDEA构建Maven JavaEE工程

#### 1. 手动创建
1. 创建一个JavaSE Maven工程。
2. 手动添加Web项目结构文件，注意结构和命名必须固定，否则无法识别。

![Web项目结构](https://secure2.wostatic.cn/static/2iYsG44sjYayNqY7t9WtrZ/image.png)

3. 修改 `pom.xml` 文件，新增 `<packaging>` 标签，定义打包方式为 `war`：
   ```xml
   <groupId>com.atguigu</groupId>
   <artifactId>maven_parent</artifactId>
   <version>1.0-SNAPSHOT</version>
   <packaging>war</packaging>
   ```
4. 刷新和校验，确认 `webapp` 文件夹出现小蓝点，表示成功。

![校验成功](https://secure2.wostatic.cn/static/CEhMC5eswYp2GhyYQwnry/image.png)

#### 2. 插件方式创建
1. 安装插件 `JBLJavaToWeb`：  
   依次选择 `File > Settings > Plugins > Marketplace`，搜索并安装。

![插件安装](https://secure2.wostatic.cn/static/dfWTRgLdpDLHj7triTW9nM/image.png)

2. 创建一个JavaSE Maven工程。
3. 右键项目，使用插件快速补全Web项目结构。

![插件补全](https://secure2.wostatic.cn/static/vdNw6jnGT7r7CXUji3j7ah/image.png)

---

### Maven工程项目结构说明

Maven提供一种标准化的项目结构，便于管理依赖、构建、测试和发布。以下是Maven Web程序的文件结构及说明：

```plaintext
|-- pom.xml                               # Maven 项目管理文件
|-- src
    |-- main                              # 项目主要代码
    |   |-- java                          # Java 源代码目录
    |   |   `-- com/example/myapp         # 开发者代码主目录
    |   |       |-- controller            # 存放 Controller 层代码
    |   |       |-- service               # 存放 Service 层代码
    |   |       |-- dao                   # 存放 DAO 层代码
    |   |       `-- model                 # 存放数据模型
    |   |-- resources                     # 存放配置文件和静态资源
    |   |   |-- log4j.properties          # 日志配置文件
    |   |   |-- spring-mybatis.xml        # Spring Mybatis 配置文件
    |   |   `-- static                    # 静态资源目录
    |   |       |-- css                   # 存放 CSS 文件
    |   |       |-- js                    # 存放 JavaScript 文件
    |   |       `-- images                # 存放图片资源
    |   `-- webapp                        # Web相关配置和资源
    |       |-- WEB-INF                   # 存放Web配置文件
    |       |   |-- web.xml               # Web应用部署描述文件
    |       |   `-- classes               # 编译后的class文件
    |       `-- index.html                # Web应用入口页面
    `-- test                              # 项目测试代码
        |-- java                          # 单元测试代码
        `-- resources                     # 测试资源文件
```

#### 说明：
- **pom.xml**：项目管理文件，描述依赖和构建配置。
- **src/main/java**：Java源代码目录。
- **src/main/resources**：资源文件目录，如配置文件和静态资源。
- **src/main/webapp/WEB-INF**：Web配置文件目录。
- **src/test/java**：测试代码目录。
- **src/test/resources**：测试资源文件目录。

---

### 示例截图

#### 手动创建示例
![手动示图1](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732609463167-e4830330-2d38-4530-b35c-9db483209ef3.png)

#### 插件补全示例
![插件补全示例](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732609984318-e5d59520-30fd-4312-9ad0-7ef64e3c0ffa.png)

#### 其他操作
- **新建模块**
  ![new module](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610094573-fa1bac7e-f591-4ff1-848a-16ea0b608c37.png)
- **右键插件快速生成**
  ![右键插件生成](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610176623-a7c820c0-b090-493e-b11d-91c5ea7128bc.png)





## 基于IDEA的Maven工程创建
### 梳理Maven工程GAVP属性
```plain
> Maven工程相对之前的工程，多出一组gavp属性，gav需要我们在创建项目的时指定，p有默认值，后期通过配置文件修改。既然要填写的属性，我们先行了解下这组属性的含义!

Maven 中的 GAVP 是指 GroupId、ArtifactId、Version、Packaging 等四个属性的缩写，其中前三个是必要的，而 Packaging 属性为可选项。这四个属性主要为每个项目在maven仓库总做一个标识，类似人的《姓-名》。有了具体标识，方便maven软件对项目进行管理和互相引用！

**GAV遵循一下规则：**

  1） **GroupID 格式**：com.{公司/BU }.业务线.[子业务线]，最多 4 级。

    说明：{公司/BU} 例如：alibaba/taobao/tmall/aliexpress 等 BU 一级；子业务线可选。

    正例：com.taobao.tddl 或 com.alibaba.sourcing.multilang  com.atguigu.java

  2） **ArtifactID 格式**：产品线名-模块名。语义不重复不遗漏，先到仓库中心去查证一下。

    正例：tc-client / uic-api / tair-tool / bookstore

  3） **Version版本号格式推荐**：主版本号.次版本号.修订号 1.0.0

    1） 主版本号：当做了不兼容的 API 修改，或者增加了能改变产品方向的新功能。

    2） 次版本号：当做了向下兼容的功能性新增（新增类、接口等）。

    3） 修订号：修复 bug，没有修改方法签名的功能加强，保持 API 兼容性。

    例如： 初始→1.0.0  修改bug → 1.0.1  功能调整 → 1.1.1等

**Packaging定义规则：**

  指示将项目打包为什么类型的文件，idea根据packaging值，识别maven项目类型！

  packaging 属性为 jar（默认值），代表普通的Java工程，打包以后是.jar结尾的文件。

  packaging 属性为 war，代表Java的web工程，打包以后.war结尾的文件。

  packaging 属性为 pom，代表不会打包，用来做继承的父工程。
```

### Idea构建Maven JavaSE工程
```plain
注意：此处省略了version，直接给了一个默认值<version>1.0-SNAPSHOT</version>

自己后期可以在项目中随意修改！

![](https://secure2.wostatic.cn/static/oDo2HDrVXHoKqfqRdqLKuV/image.png?auth_key=1732609482-vFAW9GZ7TjCnWxbpk4Rqna-0-39e01048607660175a5858866353701c)
```

###  Idea构建Maven JavaEE工程
```plain
1. 手动创建
    1. 创建一个javasemaven工程
    2. 手动添加web项目结构文件

        注意：结构和命名固定

        ![](https://secure2.wostatic.cn/static/2iYsG44sjYayNqY7t9WtrZ/image.png?auth_key=1732609483-siJyahspe1LfNfbHos8iEq-0-ec978c156bc204fff657817f000d5145)
    3. 修改pom.xml文件打包方式

        修改位置：项目下/pom.xml
```

```plain
<groupId>com.atguigu</groupId>

<artifactId>maven_parent</artifactId>

<version>1.0-SNAPSHOT</version>

<!-- 新增一列打包方式packaging -->
<packaging>war</packaging>

```

```plain
    4. 刷新和校验

        ![](https://secure2.wostatic.cn/static/CEhMC5eswYp2GhyYQwnry/image.png?auth_key=1732609483-g1Yi2fioUX91MYHfTndY91-0-5cc2d18696caa67a58e9e00184267388)

        ![](https://secure2.wostatic.cn/static/haCWoNhTmZaQEzd3T8GmRu/image.png?auth_key=1732609482-smkhNoQuaKbgEszRfR7EyN-0-ee82c6c23942826809de44cd3f1bde21)

        项目的webapp文件夹出现小蓝点，代表成功！！
2. 插件方式创建
    1. 安装插件JBLJavaToWeb

        file / settings / plugins / marketplace

        ![](https://secure2.wostatic.cn/static/dfWTRgLdpDLHj7triTW9nM/image.png?auth_key=1732609482-t4zZvdLNbchfrxGaHShGH8-0-d452ad5cf0237b88a95f22180613c361)
    2. 创建一个javasemaven工程
    3. 右键、使用插件快速补全web项目

        ![](https://secure2.wostatic.cn/static/vdNw6jnGT7r7CXUji3j7ah/image.png?auth_key=1732609482-uimzhRbUK8hugjqHxzQd1Q-0-ac42aad9c902113970c3147652dead3b)
```

### Maven工程项目结构说明
```plain
Maven 是一个强大的构建工具，它提供一种标准化的项目结构，可以帮助开发者更容易地管理项目的依赖、构建、测试和发布等任务。以下是 Maven Web 程序的文件结构及每个文件的作用：
```

```plain
|-- pom.xml                               # Maven 项目管理文件 
|-- src
    |-- main                              # 项目主要代码
    |   |-- java                          # Java 源代码目录
    |   |   `-- com/example/myapp         # 开发者代码主目录
    |   |       |-- controller            # 存放 Controller 层代码的目录
    |   |       |-- service               # 存放 Service 层代码的目录
    |   |       |-- dao                   # 存放 DAO 层代码的目录
    |   |       `-- model                 # 存放数据模型的目录
    |   |-- resources                     # 资源目录，存放配置文件、静态资源等
    |   |   |-- log4j.properties          # 日志配置文件
    |   |   |-- spring-mybatis.xml        # Spring Mybatis 配置文件
    |   |   `-- static                    # 存放静态资源的目录
    |   |       |-- css                   # 存放 CSS 文件的目录
    |   |       |-- js                    # 存放 JavaScript 文件的目录
    |   |       `-- images                # 存放图片资源的目录
    |   `-- webapp                        # 存放 WEB 相关配置和资源
    |       |-- WEB-INF                   # 存放 WEB 应用配置文件
    |       |   |-- web.xml               # Web 应用的部署描述文件
    |       |   `-- classes               # 存放编译后的 class 文件
    |       `-- index.html                # Web 应用入口页面
    `-- test                              # 项目测试代码
        |-- java                          # 单元测试目录
        `-- resources                     # 测试资源目录
```

```plain
- pom.xml：Maven 项目管理文件，用于描述项目的依赖和构建配置等信息。
- src/main/java：存放项目的 Java 源代码。
- src/main/resources：存放项目的资源文件，如配置文件、静态资源等。
- src/main/webapp/WEB-INF：存放 Web 应用的配置文件。
- src/main/webapp/index.html：Web 应用的入口页面。
- src/test/java：存放项目的测试代码。
- src/test/resources：存放测试相关的资源文件，如测试配置文件等。
```



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732609463167-e4830330-2d38-4530-b35c-9db483209ef3.png)



手动示图1



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732609984318-e5d59520-30fd-4312-9ad0-7ef64e3c0ffa.png)



插件例图

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610094573-fa1bac7e-f591-4ff1-848a-16ea0b608c37.png)

new module

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610144372-c71e3cdd-02f1-4580-aab7-592717ab9f0e.png)

右键 JBLJavaToWeb

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610176623-a7c820c0-b090-493e-b11d-91c5ea7128bc.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610217761-9ccaa41d-3e33-4ad1-b97b-8984b3fe01fc.png)

### Idea构建Maven JavaSE工程
```plain
注意：此处省略了version，直接给了一个默认值<version>1.0-SNAPSHOT</version>

自己后期可以在项目中随意修改！

![](https://secure2.wostatic.cn/static/oDo2HDrVXHoKqfqRdqLKuV/image.png?auth_key=1732609482-vFAW9GZ7TjCnWxbpk4Rqna-0-39e01048607660175a5858866353701c)
```

### Idea构建Maven JavaEE工程
```plain
1. 手动创建
    1. 创建一个javasemaven工程
    2. 手动添加web项目结构文件

        注意：结构和命名固定（必须按照结构来，否则无法识别）

        ![](https://secure2.wostatic.cn/static/2iYsG44sjYayNqY7t9WtrZ/image.png?auth_key=1732609483-siJyahspe1LfNfbHos8iEq-0-ec978c156bc204fff657817f000d5145)
    3. 修改pom.xml文件打包方式

        修改位置：项目下/pom.xml
```

```plain
<groupId>com.atguigu</groupId>

<artifactId>maven_parent</artifactId>

<version>1.0-SNAPSHOT</version>

<!-- 新增一列打包方式packaging -->
<packaging>war</packaging>

```

```plain
    4. 刷新和校验

        ![](https://secure2.wostatic.cn/static/CEhMC5eswYp2GhyYQwnry/image.png?auth_key=1732609483-g1Yi2fioUX91MYHfTndY91-0-5cc2d18696caa67a58e9e00184267388)

        ![](https://secure2.wostatic.cn/static/haCWoNhTmZaQEzd3T8GmRu/image.png?auth_key=1732609482-smkhNoQuaKbgEszRfR7EyN-0-ee82c6c23942826809de44cd3f1bde21)

        项目的webapp文件夹出现小蓝点，代表成功！！


2. 插件方式创建
    1. 安装插件JBLJavaToWeb

        file / settings / plugins / marketplace

        ![](https://secure2.wostatic.cn/static/dfWTRgLdpDLHj7triTW9nM/image.png?auth_key=1732609482-t4zZvdLNbchfrxGaHShGH8-0-d452ad5cf0237b88a95f22180613c361)
    2. 创建一个javasemaven工程
    3. 右键、使用插件快速补全web项目

        ![](https://secure2.wostatic.cn/static/vdNw6jnGT7r7CXUji3j7ah/image.png?auth_key=1732609482-uimzhRbUK8hugjqHxzQd1Q-0-ac42aad9c902113970c3147652dead3b)
```



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732609675222-6ab415d0-9cb9-41d2-a577-65f06eb597da.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732609712818-781c6e84-5754-4bd3-aa8f-87469a77da1a.png)

### Maven工程项目结构说明
```plain
Maven 是一个强大的构建工具，它提供一种标准化的项目结构，可以帮助开发者更容易地管理项目的依赖、构建、测试和发布等任务。以下是 Maven Web 程序的文件结构及每个文件的作用：
```

```plain
|-- pom.xml                               # Maven 项目管理文件 
|-- src
    |-- main                              # 项目主要代码
    |   |-- java                          # Java 源代码目录
    |   |   `-- com/example/myapp         # 开发者代码主目录
    |   |       |-- controller            # 存放 Controller 层代码的目录
    |   |       |-- service               # 存放 Service 层代码的目录
    |   |       |-- dao                   # 存放 DAO 层代码的目录
    |   |       `-- model                 # 存放数据模型的目录
    |   |-- resources                     # 资源目录，存放配置文件、静态资源等
    |   |   |-- log4j.properties          # 日志配置文件
    |   |   |-- spring-mybatis.xml        # Spring Mybatis 配置文件
    |   |   `-- static                    # 存放静态资源的目录
    |   |       |-- css                   # 存放 CSS 文件的目录
    |   |       |-- js                    # 存放 JavaScript 文件的目录
    |   |       `-- images                # 存放图片资源的目录
    |   `-- webapp                        # 存放 WEB 相关配置和资源
    |       |-- WEB-INF                   # 存放 WEB 应用配置文件
    |       |   |-- web.xml               # Web 应用的部署描述文件
    |       |   `-- classes               # 存放编译后的 class 文件
    |       `-- index.html                # Web 应用入口页面
    `-- test                              # 项目测试代码
        |-- java                          # 单元测试目录
        `-- resources                     # 测试资源目录
```

```plain
- pom.xml：Maven 项目管理文件，用于描述项目的依赖和构建配置等信息。
- src/main/java：存放项目的 Java 源代码。
- src/main/resources：存放项目的资源文件，如配置文件、静态资源等。
- src/main/webapp/WEB-INF：存放 Web 应用的配置文件。
- src/main/webapp/index.html：Web 应用的入口页面。
- src/test/java：存放项目的测试代码。
- src/test/resources：存放测试相关的资源文件，如测试配置文件等。
```



---------------------



pom.xml放项目配置，依赖

scr放项目源文件

 -main放主体代码

  -java 放java代码

  -resources 放除了源代码以外的配置文件

  -webapp 放静态页面和配置文件

 -test放测试代码（例如单元测试）



------------------



## Maven核心功能依赖和构建管理
![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610644717-db73d881-63d5-4d2c-915f-52b01c73bb76.png)



> 可以申明变量来管理版本号

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610918225-90a78bd9-d2a7-427c-8e7e-2c5a5c423be1.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610929718-72293aee-98f9-4be1-a94b-3982d404b654.png)

> 导入第三方依赖方式

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610769332-82f08d67-cf8e-43db-8b4d-5615ef7fa984.png)

> 使用maven search插件



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610703915-a1af42d3-d265-4001-8e6c-60eb5c6e53bc.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610722507-3ac0d060-9603-4688-994a-2554d98f5a29.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732610738545-53f6c994-9c3b-4e8a-b374-689797154d18.png)



> 可以限制依赖的范围

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732611087922-b6a87192-8899-4afa-a82f-736f64b4a0ba.png)



> 还有runtime main test不用，只在运行时候使用
provided main test用 打包运行时不用



> 总结:他是一种锦上添花的手段,如果你掌握不好,你就默认值,全部生效,你就一定不会错!!

### 3.1 依赖管理和配置
```plain
Maven 依赖管理是 Maven 软件中最重要的功能之一。Maven 的依赖管理能够帮助开发人员自动解决软件包依赖问题，使得开发人员能够轻松地将其他开发人员开发的模块或第三方框架集成到自己的应用程序或模块中，避免出现版本冲突和依赖缺失等问题。

我们通过定义 POM 文件，Maven 能够自动解析项目的依赖关系，并通过 Maven **仓库自动**下载和管理依赖，从而避免了手动下载和管理依赖的繁琐工作和可能引发的版本冲突问题。

重点: 编写pom.xml文件!

maven项目信息属性配置和读取：
```

```plain
<!-- 模型版本 -->
<modelVersion>4.0.0</modelVersion>
<!-- 公司或者组织的唯一标志，并且配置时生成的路径也是由此生成， 如com.companyname.project-group，maven会将该项目打成的jar包放本地路径：/com/companyname/project-group -->
<groupId>com.companyname.project-group</groupId>
<!-- 项目的唯一ID，一个groupId下面可能多个项目，就是靠artifactId来区分的 -->
<artifactId>project</artifactId>
<!-- 版本号 -->
<version>1.0.0</version>

<!--打包方式
    默认：jar
    jar指的是普通的java项目打包方式！ 项目打成jar包！
    war指的是web项目打包方式！项目打成war包！
    pom不会讲项目打包！这个项目作为父工程，被其他工程聚合或者继承！后面会讲解两个概念
-->
<packaging>jar/pom/war</packaging>
```

```plain
依赖管理和添加：

<!-- 
   通过编写依赖jar包的gav必要属性，引入第三方依赖！
   scope属性是可选的，可以指定依赖生效范围！
   依赖信息查询方式：
      1. maven仓库信息官网 https://mvnrepository.com/
      2. mavensearch插件搜索
 -->
<dependencies>
    <!-- 引入具体的依赖包 -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
        <!--
            生效范围
            - compile ：main目录 test目录  打包打包 [默认]
            - provided：main目录 test目录  Servlet
            - runtime： 打包运行           MySQL
            - test:    test目录           junit
         -->
        <scope>runtime</scope>
    </dependency>

</dependencies>
```


> 依赖版本提取和维护:


```plain
<!--声明版本-->
<properties>
  <!--命名随便,内部制定版本号即可！-->
  <junit.version>4.11</junit.version>
  <!-- 也可以通过 maven规定的固定的key，配置maven的参数！如下配置编码格式！-->
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
</properties>

<dependencies>
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <!--引用properties声明版本 -->
    <version>${junit.version}</version>
  </dependency>
</dependencies>
```

### 依赖传递和冲突
（依赖传递：只要导入依赖，就会自动导入依赖的依赖）


**依赖传递**指的是当一个模块或库 A 依赖于另一个模块或库 B，而 B 又依赖于模块或库 C，那么 A 会间接依赖于 C。这种依赖传递结构可以形成一个依赖树。当我们引入一个库或框架时，构建工具（如 Maven、Gradle）会自动解析和加载其所有的直接和间接依赖，确保这些依赖都可用。

依赖传递的作用是：

1. 减少重复依赖：当多个项目依赖同一个库时，Maven 可以自动下载并且只下载一次该库。这样可以减少项目的构建时间和磁盘空间。
2. 自动管理依赖: Maven 可以自动管理依赖项，使用依赖传递，简化了依赖项的管理，使项目构建更加可靠和一致。
3. 确保依赖版本正确性：通过依赖传递的依赖，之间都不会存在版本兼容性问题，确实依赖的版本正确性！

依赖传递演示：

  项目中，需要导入jackson相关的依赖，通过之前导入经验，jackson需要导入三个依赖，分别为：

  ![](https://secure2.wostatic.cn/static/463a23mzkd1mo97Fm1rhpS/image.png?auth_key=1732592594-rAeM7NhvMmpTpTcN42iqKi-0-d77f2cacf1426ec412d397ff45ca25ad)

  通过查看网站介绍的依赖传递特性：data-bind中，依赖其他两个依赖

  ![](https://secure2.wostatic.cn/static/m8TKvDS5fj34z334a6jPxz/image.png?auth_key=1732592594-c1jkjA6dyHhSiSnbZxL7oX-0-ec4f70629a9917b14bb06d3c173eea1b)

  最佳导入：直接可以导入data-bind，自动依赖传递需要的依赖


```plain
<!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.0</version>
</dependency>
```

```plain
依赖冲突演示：

当直接引用或者间接引用出现了相同的jar包! 这时呢，一个项目就会出现相同的重复jar包，这就算作冲突！依赖冲突避免出现重复依赖，并且终止依赖传递！

![](https://secure2.wostatic.cn/static/4C2G8BJGLJ4pzmWoGs1Woi/image.png?auth_key=1732592594-aywSDt68LEywdKCrr2agfB-0-2ded7a59f35fe247f588f5387a098646)

maven自动解决依赖冲突问题能力，会按照自己的原则，进行重复依赖选择。同时也提供了手动解决的冲突的方式，不过不推荐！

解决依赖冲突（如何选择重复依赖）方式：
  1. 自动选择原则
      - 短路优先原则（谁短谁优先，路径短）（第一原则）

          A—>B—>C—>D—>E—>X(version 0.0.1)

          A—>F—>X(version 0.0.2)

          则A依赖于X(version 0.0.2)。
      - 依赖路径长度相同情况下，则“先声明优先”（第二原则）

          A—>E—>X(version 0.0.1)

          A—>F—>X(version 0.0.2)

          在<depencies></depencies>中，先声明的，路径相同，会优先选择！

小思考:
```

```plain
前提：
   A 1.1 -> B 1.1 -> C 1.1 
   F 2.2 -> B 2.2 
   
pom声明：
   F 2.2
   A 1.1 
   
   B 2.2 
```

### 依赖导入失败场景和解决方案
```plain
在使用 Maven 构建项目时，可能会发生依赖项下载错误的情况，主要原因有以下几种：

1. 下载依赖时出现网络故障或仓库服务器宕机等原因，导致无法连接至 Maven 仓库，从而无法下载依赖。
2. 依赖项的版本号或配置文件中的版本号错误，或者依赖项没有正确定义，导致 Maven 下载的依赖项与实际需要的不一致，从而引发错误。
3. 本地 Maven 仓库或缓存被污染或损坏，导致 Maven 无法正确地使用现有的依赖项，并且也无法重新下载！

解决方案：

1. 检查网络连接和 Maven 仓库服务器状态。
2. 确保依赖项的版本号与项目对应的版本号匹配，并检查 POM 文件中的依赖项是否正确。
3. 清除本地 Maven 仓库缓存（lastUpdated 文件），因为只要存在lastupdated缓存文件，刷新也不会重新下载。本地仓库中，根据依赖的gav属性依次向下查找文件夹，最终删除内部的文件，刷新重新下载即可！

    例如： pom.xml依赖
```

```plain
<dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>druid</artifactId>
  <version>1.2.8</version>
</dependency>
```

```plain
    文件：

    ![](https://secure2.wostatic.cn/static/6mSDgf4nkaRLAu16dqSJk7/image.png?auth_key=1732592595-5HC5QVnSytTqtW2eUzSKut-0-8f549144f6aa52e2517b8228b6110ab9)

    脚本使用：

    
```

```plain
使用记事本打开
set REPOSITORY_PATH=D:\repository  改成你本地仓库地址即可！
点击运行脚本，即可自动清理本地错误缓存文件！！
```




> 本地仓库被污染

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732611847612-dea420b1-0c4f-40e6-b9c8-01aa4fcd0798.png)

> 如果本地仓库存在lastupdated就不会访问网络仓库  
一般是更新中止造成的  
这时候我们可以按照路径寻找，然后删除该文件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732611977290-819350ef-b1fc-4d97-874b-03cf0862fdb1.png)



+ 可以使用懒人脚本一键删除lastupdated

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732612074981-eac529dd-161e-4bdf-9e72-cb460da3b3b6.png)



### 扩展构建管理和插件配置
```plain
**构建概念:**

项目构建是指将源代码、依赖库和资源文件等转换成可执行或可部署的应用程序的过程，在这个过程中包括编译源代码、链接依赖库、打包和部署等多个步骤。

![](https://secure2.wostatic.cn/static/hDM25DDDzZrYFzhfiwTWVk/image.png?auth_key=1732609472-thEMj3S37cLQEisv8DGyKM-0-74da0cd55eba316b71eaabd6d0cf9486)

**主动触发场景：**

- 重新编译 : 编译不充分, 部分文件没有被编译!
- 打包 : 独立部署到外部服务器软件,打包部署
- 部署本地或者私服仓库 : maven工程加入到本地或者私服仓库,供其他工程使用

**命令方式构建:**

语法: mvn 构建命令  构建命令....
```

| 命令 | 描述 |
| --- | --- |
| mvn clean | 清理编译或打包后的项目结构,删除target文件夹 |
| mvn compile | 编译项目，生成target文件 |
| mvn test | 执行测试源码 (测试) |
| mvn site | 生成一个项目依赖信息的展示页面 |
| mvn package | 打包项目，生成war / jar 文件 |
| mvn install | 打包后上传到maven本地仓库(本地部署) |
| mvn deploy | 只打包，上传到maven私服仓库(私服部署)（需要共享给他人时） |


注意

+ 命令指向需要我们进入到项目的根目录 pom文件的目录
+ 步数必须是jar包形式



```plain
**可视化方式构建:**

![](https://secure2.wostatic.cn/static/85Cv2rhHoFN4C9JgJzVdho/image.png?auth_key=1732609472-r9qUvv4SPSTzf1RbeVEQyM-0-046732a4ddabf0ade0e07aef8c926467)

**构建命令周期:**

构建生命周期可以理解成是一组固定构建命令的有序集合，触发周期后的命令，会自动触发周期前的命令！也是一种简化构建的思路!

- 清理周期：主要是对项目编译生成文件进行清理

    包含命令：clean
- 默认周期：定义了真正构件时所需要执行的所有步骤，它是生命周期中最核心的部分

    包含命令：compile - test - package - install / deploy
- 报告周期

    包含命令：site

    打包: mvn clean package 本地仓库: mvn clean install

**最佳使用方案:**
```

```latex
打包: mvn clean package
重新编译: mvn clean compile
本地部署: mvn clean install 
```

```plain
**周期，命令和插件:**

周期→包含若干命令→包含若干插件!

使用周期命令构建，简化构建过程！

最终进行构建的是插件！

插件配置:
```

```plain
<build>
   <!-- jdk17 和 war包版本插件不匹配 -->
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.2</version>
        </plugin>
    </plugins>
</build>
```









> mvn compile   
编译好后

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732612545601-b06e1e8d-9250-421b-9042-67847bddc8a4.png)



> mvn install

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732612620141-4d56e45a-707f-4b10-86f5-6c0c960cf4f3.png)



> mvn clean compile test package install （部署操作）



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732612996901-bfd775b3-899b-4292-9651-821c29a761fd.png)

> mvn clean install（这样就可以）  
会自动触发compile test package



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732612746166-f1067f7c-21d4-4339-8a56-f5d3a04e6d30.png)



> 命令有周期   
maven将命令分成了三个周期   
最终干活的是插件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732613104760-d39b3c89-9037-4ab9-821a-9c239e3d2fec.png)

> 我们其实是使用命令调用插件

> 遇到插件版本过低时可以自定义导入插件

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732613247692-a85e9ac6-2fc2-49ea-8af0-dd5b124aca37.png)


## Maven继承和聚合特性
### Maven工程继承关系
#### 依赖冲突时

> 思路一 直接在父工程引入依赖

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636324870-2e18ea47-d186-4e6d-9095-9da81034ada0.png)



> 思路二 父工程不引入依赖 只做依赖声明

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636614291-9eae4f26-e7bb-4309-9f59-8356231c0de2.png)


- 父工程不打包也不写代码

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636772645-daf728d9-4c7f-4fce-9a92-dc5edc161a1d.png)

 - 新建子工程

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636809429-661b018f-c743-4bca-a748-7020f16c1418.png)



![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636835079-c505d11e-5dc5-4b9f-8722-7500a2d04532.png)

 - 子工程中pom文件多了parent

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636872905-1751b1be-080c-4773-a228-242700283e44.png)



 - 在父工程中声明版本管理

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732636995047-93265983-6462-4334-a4f4-a12cee059db1.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732637109103-c139f1b2-36fa-43d5-a802-c1f3c989bc73.png)



 - 在子工程中需要写

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732637148624-d70b56f4-4309-404f-b443-82d5f84268e3.png)

 - 不用写版本






1. 继承概念

    Maven 继承是指在 Maven 的项目中，让一个项目从另一个项目中继承配置信息的机制。继承可以让我们在多个项目中共享同一配置信息，简化项目的管理和维护工作。

    ![](https://secure2.wostatic.cn/static/ooGfu99ezNBaguhLkwT4Z4/image.png?auth_key=1732611338-aoA4cR1kH2n6Tgx2MESFZs-0-ce62f218ceaa31b9d51ec0784c5ac640)
2. 继承作用

    作用：在父工程中统一管理项目中的依赖信息,进行统一版本管理!

    它的背景是：

    - 对一个比较大型的项目进行了模块拆分。
    - 一个 project 下面，创建了很多个 module。
    - 每一个 module 都需要配置自己的依赖信息。

    它背后的需求是：

    - 多个模块要使用同一个框架，它们应该是同一个版本，所以整个项目中使用的框架版本需要统一管理。
    - 使用框架时所需要的 jar 包组合（或者说依赖信息组合）需要经过长期摸索和反复调试，最终确定一个可用组合。这个耗费很大精力总结出来的方案不应该在新的项目中重新摸索。

    通过在父工程中为整个项目维护依赖信息的组合既保证了整个项目使用规范、准确的 jar 包；又能够将以往的经验沉淀下来，节约时间和精力。
3. 继承语法
    - 父工程


```plain
<groupId>com.atguigu.maven</groupId>
<artifactId>pro03-maven-parent</artifactId>
<version>1.0-SNAPSHOT</version>
<!-- 当前工程作为父工程，它要去管理子工程，所以打包方式必须是 pom -->
<packaging>pom</packaging>

```


    - 子工程


```plain
<!-- 使用parent标签指定当前工程的父工程 -->
<parent>
  <!-- 父工程的坐标 -->
  <groupId>com.atguigu.maven</groupId>
  <artifactId>pro03-maven-parent</artifactId>
  <version>1.0-SNAPSHOT</version>
</parent>

<!-- 子工程的坐标 -->
<!-- 如果子工程坐标中的groupId和version与父工程一致，那么可以省略 -->
<!-- <groupId>com.atguigu.maven</groupId> -->
<artifactId>pro04-maven-module</artifactId>
<!-- <version>1.0-SNAPSHOT</version> -->
```


4. 父工程依赖统一管理
    - 父工程声明版本


```plain
<!-- 使用dependencyManagement标签配置对依赖的管理 -->
<!-- 被管理的依赖并没有真正被引入到工程 -->
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>4.0.0.RELEASE</version>
    </dependency>
  </dependencies>
</dependencyManagement>
```


    - 子工程引用版本


```plain
<!-- 子工程引用父工程中的依赖信息时，可以把版本号去掉。  -->
<!-- 把版本号去掉就表示子工程中这个依赖的版本由父工程决定。 -->
<!-- 具体来说是由父工程的dependencyManagement来决定。 -->
<dependencies>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-beans</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-expression</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aop</artifactId>
  </dependency>
</dependencies>
```

###  Maven工程聚合关系


![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732637219490-5c444114-75a2-4214-990e-4cc005dbec1c.png)



在创建子工程时自带继承和聚合

一般情况下继承和聚合时同时存在

我们可以通过修改配置文件单独配置

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732637372787-fe07cce0-e54e-4298-ab10-a502811dc226.png)



```plain
1. 聚合概念

    Maven 聚合是指将多个项目组织到一个父级项目中，通过触发父工程的构建,统一按顺序触发子工程构建的过程!!
2. 聚合作用
    1. 统一管理子项目构建：通过聚合，可以将多个子项目组织在一起，方便管理和维护。
    2. 优化构建顺序：通过聚合，可以对多个项目进行顺序控制，避免出现构建依赖混乱导致构建失败的情况。
3. 聚合语法

    父项目中包含的子项目列表。
```

```plain
<project>
  <groupId>com.example</groupId>
  <artifactId>parent-project</artifactId>
  <packaging>pom</packaging>
  <version>1.0.0</version>
  <modules>
    <module>child-project1</module>
    <module>child-project2</module>
  </modules>
</project>
```

```plain
4. 聚合演示

    通过触发父工程构建命令、引发所有子模块构建！产生反应堆！

    ![](https://secure2.wostatic.cn/static/weyQ7odFa3amf3NTtCgyjQ/image.png?auth_key=1732610488-sVyt3LW3B9qEnmdLQGgQBa-0-97274a203dde13729b0462f204b80169)
```

## 实战 创建项目例子



+ 父工程配置![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732637887317-7f8aa0a6-a348-4464-87d7-fcc640d00a84.png)
+ 子工程![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732637989125-b0a10b2c-392e-40a3-84f4-60ac00ca72c5.png)![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638247736-ccd889ce-eaa7-4fbc-9de9-a3896ceaa3a6.png)
+ ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638688047-0da41f4d-5db0-4033-9357-5296ee136db8.png)
+ 子工程![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638297767-63f806d9-6a55-4720-b310-f1280a002fc7.png)![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638247736-ccd889ce-eaa7-4fbc-9de9-a3896ceaa3a6.png)
+ ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638744367-2772419d-d58d-4119-a89e-0023ee4ab85a.png)
+ 子工程![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638328765-14b280e5-2e73-494a-bb41-a855e0365742.png)
+ ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638247736-ccd889ce-eaa7-4fbc-9de9-a3896ceaa3a6.png)![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638247736-ccd889ce-eaa7-4fbc-9de9-a3896ceaa3a6.png)
+ ![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638771249-5ed01710-40e0-4909-acc4-217f53f33ae5.png)



+ 父工程

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638385154-d4edde6b-7825-4a5c-a22d-54ca621c67be.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638586636-46647ba7-1bc2-48bd-bc85-4cff1498dfcd.png)

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638636500-b8410b94-b3e8-4f3a-a4b8-955794e0535e.png)



+ 最后 install

![](https://cdn.nlark.com/yuque/0/2024/png/49455411/1732638875419-dba35d6a-acbf-4360-893c-b911e6a9528d.png)






