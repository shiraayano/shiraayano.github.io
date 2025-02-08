# Tools：Ollama 、Conda、 Open-WebUI
## Ollama
### 使用 open-webui 前我们需要先安装 Ollama
### 以下是 Ollama 的一些基本命令：
> 安装完 Ollama 之后可以直接跳到 conda 部分食用
>

### 模型管理
**创建模型**：从 Modelfile 创建模型。

+ `ollama create mymodel -f ./Modelfile`

**拉取模型**：从模型库中下载模型，也可用于更新本地模型。

+ `ollama pull <model-name>`
+ **列出模型**：查看本地所有可用的模型。

复制

```plain
ollama list
ollama ls
```

**删除模型**：删除本地指定的模型。

+ `ollama rm <model-name>`

**复制模型**：复制一个模型到另一个位置或给定名称的地方。

+ `ollama cp <old_model> <new_model>`

**显示模型信息**：查看特定模型的详细信息。

+ `ollama show <model_name>`

### 模型运行与交互
**运行模型**：运行一个已安装的模型。

+ `ollama run <model-name>`

**停止模型**：停止一个正在运行的模型。

+ `ollama stop <model-name>`
+ **多行输入**：对于多行输入，可以用 `"""` 包裹文本。

复制

```plain
>>> """Hello,
... world!
... """
```

**多模态模型**：支持图片输入的多模态模型。

+ `ollama run llava "What's in this image? /path/to/image.png"`

**使用启动参数传入 prompt**：

+ `ollama run llama3 "Summarize this file: $(cat README.md)"`

### 其他命令
**列出正在运行的模型**：显示当前正在运行的模型列表。

+ `ollama ps`

**启动 Ollama 服务**：在不运行桌面应用程序的情况下启动 Ollama。

+ `ollama serve`
+ **查看版本信息**：显示当前 Ollama 工具的版本信息。

复制

```plain
ollama -v
ollama --version
```

**推送模型到注册表**：将本地模型推送到模型注册表。

+ `ollama push <model-name>`



### 热门模型
+ **DeepSeek-R1**：综合性能出色。
+ **Qwen 2.5**：代码能力较强，适合编程相关任务。
+ **LLaMA 3.2**：英文处理能力优秀，支持128K上下文，适合长文本处理和角色扮演。
+ **Gemma 2**：谷歌模型，性能出色，角色扮演无限制。
+ **Command-R**：角色扮演能力出色，但显存占用较高。

### 特殊功能模型
+ **Embedding 模型**：支持长期记忆功能。
+ **Vision 模型**：具备图片理解能力。
+ **Tools 模型**：支持工具使用能力，可与其他应用集成。

### 官方资源
+ [Ollama GitHub](https://github.com/ollama/ollama)

## Open-WebUI
### 安装与使用
1. **创建 Python 环境**：

bash复制

```bash
conda create -n open-webui python=3.11
conda activate open-webui
```

2. **安装 Open-WebUI**：

bash复制

```bash
pip install open-webui
```

3. **启动服务**：

bash复制

```bash
open-webui serve
```

访问 `localhost:8080` 使用网页界面。

### 更新
bash复制

```bash
pip install --upgrade open-webui
```

### 官方资源
+ [Open-WebUI GitHub](https://github.com/open-webui/open-webui)





## Conda




```bash
conda env list
```

+ **创建新环境**：



```bash
conda create -n <env_name> python=<python_version>
```

+ **激活环境**：



```bash
conda activate <env_name>
```

+ **退出当前环境**：



```bash
conda deactivate
```

+ **删除环境**：



```bash
conda env remove -n <env_name>
```

+ **安装包**：



```bash
conda install <package_name>
```

+ **更新包**：



```bash
conda update <package_name>
```

+ **更新所有包**：



```bash
conda update --all
```

+ **查看已安装的包**：



```bash
conda list
```





