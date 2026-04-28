## 如何处理 Vocaloid 声库的注册表数据

在使用 Vocaloid 编辑器时，有时我们需要将不同版本的声库数据迁移或更新注册表路径。以下是两种常见的 CMD 脚本，分别用于处理声库数据的路径替换和数据迁移。

## 我这有俩脚本，按需选择，记得用管理员运行。

### 处理 V3 声库路径替换

这个脚本的功能是将 V3 声库的注册表数据从旧路径转换到 V5 编辑器所需的新路径。它适用于将 V3 声库的数据复制并更新到 V5 编辑器的注册表路径中。

```cmd
@echo off && reg export "HKLM\SOFTWARE\WOW6432Node\VCLDASGN3\DATABASE\VOICE3" "%TEMP%\v3data.reg" /y && powershell -Command "(Get-Content '%TEMP%\v3data.reg') -replace 'VCLDASGN3\\DATABASE\\VOICE3', 'VOCALOID4\\DATABASE' | Set-Content '%TEMP%\v3data_modified.reg'" && reg import "%TEMP%\v3data_modified.reg" && del "%TEMP%\v3data.reg" && del "%TEMP%\v3data_modified.reg" && echo V3 声库注册表数据已成功复制到 V5 编辑器路径中！ && pause
```

#### 功能说明：
1. **导出 V3 声库的注册表数据**：从 `HKLM\SOFTWARE\WOW6432Node\VCLDASGN3\DATABASE\VOICE3` 导出数据到 `%TEMP%\v3data.reg` 文件。
2. **使用 PowerShell 修改文件内容**：
   - 读取 `%TEMP%\v3data.reg` 文件内容。
   - 将注册表路径中的 `VCLDASGN3\DATABASE\VOICE3` 替换为 `VOCALOID4\DATABASE`。
   - 将修改后的内容写入 `%TEMP%\v3data_modified.reg` 文件。
3. **导入修改后的注册表数据**：从 `%TEMP%\v3data_modified.reg` 导入数据到注册表中。
4. **删除临时文件**：删除 `%TEMP%\v3data.reg` 和 `%TEMP%\v3data_modified.reg` 文件。
5. **显示操作成功信息**。

这个脚本特别适合需要更新 V3 声库注册表路径以便在 V5 编辑器中使用的情况。

### 导出和导入 V3 和 V4 声库数据

这个脚本用于导出和导入 V3 和 V4 声库的注册表数据，适用于需要将声库数据从一个路径迁移到另一个路径的场景，但不涉及路径替换。

```cmd
@echo off && reg export "HKLM\SOFTWARE\WOW6432Node\VCLDASGN3\DATABASE\VOICE3" "%TEMP%\v3data.reg" /y && reg import "%TEMP%\v3data.reg" && del "%TEMP%\v3data.reg" && reg export "HKLM\SOFTWARE\WOW6432Node\POCALOID4\DATABASE" "%TEMP%\v4data.reg" /y && reg import "%TEMP%\v4data.reg" && del "%TEMP%\v4data.reg" && echo 注册表路径更新成功! && pause
```

#### 功能说明：
1. **导出 V3 声库的注册表数据**：从 `HKLM\SOFTWARE\WOW6432Node\VCLDASGN3\DATABASE\VOICE3` 导出数据到 `%TEMP%\v3data.reg` 文件。
2. **导入 V3 数据**：将 `%TEMP%\v3data.reg` 的数据导入到注册表。
3. **删除临时文件**：删除 `%TEMP%\v3data.reg` 文件。
4. **导出 V4 声库的注册表数据**：从 `HKLM\SOFTWARE\WOW6432Node\POCALOID4\DATABASE` 导出数据到 `%TEMP%\v4data.reg` 文件。
5. **导入 V4 数据**：将 `%TEMP%\v4data.reg` 的数据导入到注册表。
6. **删除临时文件**：删除 `%TEMP%\v4data.reg` 文件。
7. **显示操作成功信息**。

这个脚本适用于直接导出和导入声库数据的需求，适合在多个编辑器之间迁移数据。

![image](https://github.com/user-attachments/assets/58f3871f-1f06-436b-b4e0-1415511219d0)

![image](https://github.com/user-attachments/assets/3cc8f331-f162-4e62-855c-55f8ecddc01c)

![image](https://github.com/user-attachments/assets/b3b69b28-45ea-47a1-b9be-ed15dca53b07)

![image](https://github.com/user-attachments/assets/6df7edcc-33e9-4f78-8805-794c2202c9da)

### 参考

参考 [Bilibili https://www.bilibili.com/read/cv16192226/](https://www.bilibili.com/read/cv16192226/) 