

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





## 
