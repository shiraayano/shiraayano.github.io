#### 笔者在使用idea中发现代码提示几乎不可用，出现提示缓慢等问题

- 找到idea的安装目录
![image](https://github.com/user-attachments/assets/13672396-cf64-4729-b325-a2e4aac4c77b)
    - 目录下有 `idea.properties`文件

- 添加以下配置（按照自己电脑配置量力而行哦 配置够的话无脑加大）
```java
-Xms4096m
-Xmx20480m
-XX:ReservedCodeCacheSize=2048m
-XX:+IgnoreUnrecognizedVMOptions
-XX:+UseG1GC
-XX:SoftRefLRUPolicyMSPerMB=50
-XX:CICompilerCount=2
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-ea
-Dsun.io.useCanonCaches=false
-Djdk.http.auth.tunneling.disabledSchemes=""
-Djdk.attach.allowAttachSelf=true
-Djdk.module.illegalAccess.silent=true
-Dkotlinx.coroutines.debug=off
```

![image](https://github.com/user-attachments/assets/a5207c17-b941-4054-be83-5c9afbbbef20)

---

#### 现在代码提示秒出
![image](https://github.com/user-attachments/assets/eb4c594c-fe62-4c42-abde-1e3e9b30fea1)

