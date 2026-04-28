在 Linux 服务器运维中，Swap（交换分区/文件）是物理内存的重要“备用资源”，但有时会遇到“Swap 已配置却始终未使用”的情况。本文结合实际操作场景，详细拆解 Swap 未使用问题的排查思路、原因定位及解决方法，适用于各类 Linux 发行版（如 Ubuntu、CentOS、Debian 等）。



## 一、问题背景：线上业务频繁卡死


----------------问题背景--------------





笔者线上服务经常卡死，线上业务很慢甚至直接报错，SSH超时，后续审查发现连日志都无了，完全没有故障时期的记录，这时候笔者怀疑是内存爆了



笔者尝试通过增大swap解决问题，这时候发现不对劲了，swap完全没用起来！！！



----------------真実はいつも一つ-------------

那么就尝试从swap开始排查趴



以笔者的阿里云 Ubuntu 24 企业版服务器为例，用户通过命令查看 Swap 状态时，发现以下现象：

1. 执行 `swapon --show` 显示 Swap 已配置（3GB 交换文件 `/www/swap`），但 `USED` 始终为 0B：

```bash
root@iZ2vcgkv4smamnzeaxirjpZ:~# swapon --show
NAME      TYPE SIZE USED PRIO
/www/swap file   3G   0B   -2
```

2. 执行 `free -h` 查看内存占用，物理内存（1.6Gi）已用 769Mi，可用 843Mi，Swap 仍未触发使用：

```bash
root@iZ2vcgkv4smamnzeaxirjpZ:~# free -h
              total        used        free      shared  buff/cache   available
Mem:           1.6Gi       769Mi        68Mi        13Mi       961Mi       843Mi
Swap:          3.0Gi          0B       3.0Gi
```

3. 初步怀疑 Swap 功能异常，但不确定问题根源。



## 二、排查第一步：明确 Swap 未使用的“正常/异常”边界
在开始复杂排查前，需先判断 Swap 未使用是“系统正常调度”还是“功能故障”，避免无效操作。

### 1. 核心逻辑：Linux 优先使用物理内存，Swap 是“备用资源”
Linux 内存管理的核心策略是**“优先用尽物理内存，再启用 Swap”**，原因是 Swap 依赖磁盘 I/O，速度远慢于物理内存，频繁使用会影响性能。因此：

+ 若物理内存“可用空间（available）”充足（如本例中 843Mi），系统不会主动使用 Swap，属于**正常现象**；
+ 仅当物理内存接近耗尽（available 低于 100Mi），但 Swap 仍未使用时，才需进一步排查。

### 2. 验证物理内存是否“需要用”Swap
通过 `top` 或 `htop` 查看进程内存占用，确认是否有进程导致物理内存紧张：

```bash
root@iZ2vcgkv4smamnzeaxirjpZ:~# top
```

+ 若输出中 `%MEM` 列无高占用进程（如单个进程内存占比未超过 50%），物理内存仍有充足剩余，无需干预；
+ 若物理内存已接近满载（available 仅剩几十 MB），Swap 仍未使用，进入下一步排查。



## 三、排查第二步：分场景定位 Swap 未使用的核心原因
根据第一步的判断，若确认物理内存紧张但 Swap 未使用，需按以下场景逐步定位问题。

### 场景 1：Swap 未启用（表面配置，实际未挂载）
若 `swapon --show` 无输出，或 `free -h` 显示 Swap 总大小为 0，说明 Swap 未启用，需检查：

1. 查看 `/etc/fstab` 确认 Swap 开机自动挂载配置：

```bash
root@iZ2vcgkv4smamnzeaxirjpZ:~# cat /etc/fstab | grep swap
/www/swap    swap    swap    defaults    0 0
```

    - 若输出无 Swap 配置，需手动添加（见下文“解决方法”）；
    - 若有配置但未生效，执行 `sudo swapon /www/swap` 手动启用，再用 `swapon --show` 验证。
2. 检查 Swap 文件/分区是否存在：

```bash
# 检查 Swap 文件
ls -l /www/swap
# 检查 Swap 分区（若用分区而非文件）
lsblk | grep swap
```

    - 若文件/分区不存在，需重新创建 Swap（见下文“补充：创建 Swap 文件步骤”）。



### 场景 2：Swap 已启用，但 Swappiness 参数导致“极端排斥使用”
若 `swapon --show` 显示 Swap 已启用，但物理内存紧张时仍未使用，需重点检查 **Swappiness 内核参数**——该参数控制系统使用 Swap 的“倾向”，取值 0-100：

+ `swappiness=0`：仅当物理内存完全耗尽（连内核预留内存都不足）时，才被迫使用 Swap，优先“杀进程（OOM）”释放内存；
+ `swappiness=60`（默认值）：物理内存占用到一定比例时，逐步使用 Swap，平衡性能与稳定性；
+ `swappiness=100`：积极使用 Swap，物理内存占用较少时就触发。

#### 操作步骤：
1. 查看当前 Swappiness 配置：

```bash
root@iZ2vcgkv4smamnzeaxirjpZ:~# cat /proc/sys/vm/swappiness
0
```

本例中 Swappiness 为 0，这是 Swap 未使用的**核心原因**——系统极端排斥使用 Swap，即使物理内存紧张也优先杀进程。

2. 验证参数影响：  
若 Swappiness 为 0，即使通过 `stress` 工具模拟内存满载（如占用 1.8Gi 内存，超过物理内存 1.6Gi），Swap 仍可能不触发，或仅在进程被杀死前短暂使用。



## 四、解决方法：调整 Swappiness 参数，让 Swap 正常工作
针对 Swappiness 为 0 的问题，需将参数调整为合理值（推荐 30-50），让系统在物理内存紧张时主动使用 Swap，避免频繁 OOM 杀进程。

### 1. 临时调整（立即生效，重启后失效）
适合快速测试参数效果，执行命令：

```bash
# 将 Swappiness 设为 30
sudo sysctl -w vm.swappiness=30

# 验证调整结果
cat /proc/sys/vm/swappiness  # 输出应为 30
```

### 2. 永久调整（重启后仍生效）
临时调整会在服务器重启后失效，需将配置写入系统文件：

```bash
# 将 swappiness=30 追加到 /etc/sysctl.conf（系统级配置文件）
echo 'vm.swappiness=30' | sudo tee -a /etc/sysctl.conf

# 或者 （推荐）
vi /etc/sysctl.conf
# 将vm.swappiness=30写入对应位置

# 让配置立即生效（无需重启）
sudo sysctl -p
```

### 3. 验证调整效果
调整后：

```bash
root@iZ2vcgkv4smamnzeaxirjpZ:~# swapon --show
NAME      TYPE SIZE   USED PRIO
/www/swap file   3G 959.2M   -2
```

![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1759561501565-dbc37e52-dfb8-4cfe-b1bf-37f8d72252e0.png)

搞定~

## 五、补充：Swap 文件创建步骤（适用于未配置 Swap 的场景）
若服务器未配置 Swap，需手动创建交换文件，步骤如下（以创建 3GB Swap 为例）：

1. 创建 Swap 文件（路径 `/www/swap`）：

```bash
# 用 fallocate 快速创建 3GB 文件（若 fallocate 不可用，改用 dd if=/dev/zero of=/www/swap bs=1M count=3072）
sudo fallocate -l 3G /www/swap
```

2. 设置文件权限（仅 root 可读写，避免安全风险）：

```bash
sudo chmod 600 /www/swap
```

3. 格式化 Swap 文件：

```bash
sudo mkswap /www/swap
```

4. 启用 Swap 文件：

```bash
sudo swapon /www/swap
```

5. 配置开机自动挂载（添加到 `/etc/fstab`）：

```bash
echo '/www/swap swap swap defaults 0 0' | sudo tee -a /etc/fstab
```

6. 验证：

```bash
swapon --show  # 应显示 /www/swap，USED 初始为 0B
```



## 
