

### 查看、开启、关闭和永久关闭防火墙

1. **查看防火墙状态**：
   ```bash
   sudo ufw status
   ```
   这将显示当前防火墙规则的状态，包括是否启用和允许的规则。

2. **开启防火墙**：
   ```bash
   sudo ufw enable
   ```
   启用防火墙后，它将按照默认规则开始工作，通常会拒绝所有传入连接，但允许所有传出连接。

3. **关闭防火墙**：
   ```bash
   sudo ufw disable
   ```
   关闭防火墙后，所有传入和传出的连接将被允许，不再受到防火墙的限制。

4. **永久关闭防火墙**：
   - 停止 ufw 服务：
     ```bash
     sudo systemctl stop ufw
     ```
   - 禁用 ufw 服务的自动启动：
     ```bash
     sudo systemctl disable ufw
     ```
   - 重启系统，以确保防火墙不会在系统启动时重新启用。

### 在 Ubuntu 上安装 SSH

1. **更新软件包列表**：
   ```bash
   sudo apt update
   ```

2. **安装 OpenSSH 服务器**：
   ```bash
   sudo apt install openssh-server
   ```

3. **检查 SSH 服务状态**：
   ```bash
   sudo systemctl status ssh
   ```
   如果服务正在运行，你将看到 `active (running)` 的状态信息。

4. **配置防火墙**（如果启用了防火墙）：
   ```bash
   sudo ufw allow ssh
   ```

5. **获取服务器 IP 地址**：
   ```bash
   ip a
   ```

6. **使用 SSH 客户端连接到服务器**：
   在本地计算机上打开终端，并输入以下命令：
   ```bash
   ssh username@server_ip_address
   ```
   将 `username` 替换为你在服务器上的用户名，`server_ip_address` 替换为你的服务器 IP 地址。

7. **生成 SSH 密钥对**（可选，推荐）：
   在本地计算机上生成 SSH 密钥对：
   ```bash
   ssh-keygen -t rsa
   ```
   按提示操作，生成的公钥保存在 `~/.ssh/id_rsa.pub` 文件中。

8. **将公钥复制到远程服务器**：
   ```bash
   ssh-copy-id username@server_ip_address
   ```
