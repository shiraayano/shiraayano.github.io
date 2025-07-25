

### **在 Linux 上结合虚拟环境设置开机自启**
#### **步骤 1：创建虚拟环境并安装依赖**
1. 创建虚拟环境：

```bash
python3 -m venv /path/to/venv
```

2. 激活虚拟环境：

```bash
source /path/to/venv/bin/activate
```

3. 安装项目依赖：

```bash
pip install -r /path/to/your/project/requirements.txt
```

```php
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

#### **步骤 2：创建 **`systemd`** 服务文件**
1. 创建服务文件：

```bash
sudo nano /etc/systemd/system/myapp.service
```

2. 编辑服务文件，内容如下：

```properties
[Unit]
Description=My Python Application
After=network.target

[Service]
ExecStart=/path/to/venv/bin/python3 /path/to/your/project/main.py
WorkingDirectory=/path/to/your/project
Environment="PATH=/path/to/venv/bin"
Restart=always
User=your_username

[Install]
WantedBy=multi-user.target
```

    - 替换 `/path/to/venv` 为你的虚拟环境路径。
    - 替换 `/path/to/your/project` 为你的项目路径。
    - 替换 `your_username` 为你的用户名。

#### **步骤 3：启用并启动服务**
1. 启动服务：

```bash
sudo systemctl start myapp.service
```

2. 设置开机自启：

```bash
sudo systemctl enable myapp.service
```

3. 检查服务状态：

```bash
sudo systemctl status myapp.service
```

### **在 Windows 上结合虚拟环境设置开机自启**
#### **方法 1：使用任务计划程序**
1. **创建批处理文件**：
    - 创建一个 `.bat` 文件，例如 `start_app.bat`，内容如下：

```plain
@echo off
REM 设置工作目录
cd /d C:\path\to\your\project 
REM 激活虚拟环境
call C:\path\to\venv\Scripts\activate.bat
REM 运行 Python 应用
python C:\path\to\your\project\main.py
```

    - 替换 `C:\path\to\venv` 为你的虚拟环境路径。
    - 替换 `C:\path\to\your\project\main.py` 为你的 Python 脚本路径。
2. **打开任务计划程序**：
    - 搜索图像搜索“任务计划程序”并打开。
3. **创建基本任务**：
    - 点击“创建基本任务...”，输入名称和描述，点击“下一步”。
    - 选择“当计算机启动时”作为触发器，点击“下一步”。
    - 选择“启动程序”，点击“浏览”并选择你刚才创建的 `start_app.bat` 文件，点击“下一步”。
    - 确认设置后点击“完成”。

#### **方法 2：使用 **`pythonw.exe`** 和快捷方式（无窗口）**
1. 创建一个快捷方式：
    - 右键桌面或文件夹空白处，选择“新建” -> “快捷方式”。
    - 在“输入对象位置”中输入：

```plain
C:\path\to\venv\Scripts\pythonw.exe C:\path\to\your\project\main.py
```

        * 替换 `C:\path\to\venv` 为你的虚拟环境路径。
        * 替换 `C:\path\to\your\project\main.py` 为你的 Python 脚本路径。
    - 点击“下一步”，输入快捷方式名称，点击“完成”。
2. 将快捷方式移到启动文件夹：
    - 打开“启动”文件夹（图像搜索“启动”并进入）。
    - 将创建的快捷方式复制并粘贴到该文件夹中。

### **注意事项**
+ **路径问题**：确保所有路径使用绝对路径，避免相对路径导致找不到文件。
+ **权限问题**：在 Linux 上，`systemd` 需要管理员权限；在 Windows 上，任务计划程序可能需要管理员权限。
+ **虚拟环境激活**：在 Windows 上，虚拟环境通过 `activate.bat` 激活；在 Linux 上，通过 `source /path/to/venv/bin/activate` 激活。



