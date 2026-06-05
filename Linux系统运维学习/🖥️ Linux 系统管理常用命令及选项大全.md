## 🖥️ Linux 系统管理常用命令及选项大全

系统管理命令涉及**进程管理、用户管理、磁盘管理、网络管理、系统监控**等多个方面。以下是分类整理的常用命令及其核心选项：

---

## 一、进程管理

### 1. `ps` - 查看进程状态

```bash
ps aux                 # 显示所有进程（包括其他用户、无终端的进程）
ps -ef                 # 显示所有进程，完整格式
ps -u username         # 显示指定用户的进程
ps -p PID              # 显示指定PID的进程
ps -l                  # 长格式显示
ps -eLf                # 显示线程信息
ps --sort=-%cpu        # 按CPU使用率降序排序
ps --sort=-%mem        # 按内存使用率降序排序
```

**常用组合：**
```bash
ps -ef | grep nginx    # 查找nginx进程
ps aux --sort=-%cpu    # 查看CPU占用最高的进程
```

### 2. `top` - 实时监控进程

```bash
top                    # 启动top界面
top -d 5               # 设置刷新间隔为5秒
top -u username        # 只显示指定用户的进程
top -p 1234,5678       # 只监控指定PID的进程
top -b -n 3            # 批处理模式，输出3次后退出
```

**top内部命令：**
- `P`：按CPU使用率排序
- `M`：按内存使用率排序
- `k`：杀死进程
- `q`：退出

### 3. `htop` - 增强版top（需安装）

```bash
htop                   # 启动htop界面
htop -u username       # 只显示指定用户
htop -p PID            # 只监控指定PID
```

### 4. `kill` - 终止进程

```bash
kill PID               # 正常终止进程（发送TERM信号）
kill -9 PID            # 强制终止进程（KILL信号）
kill -l                # 列出所有信号名称
kill -HUP PID          # 重启进程（常用于服务重载配置）
killall process_name   # 按进程名终止所有匹配的进程
pkill process_name     # 按进程名终止进程（更灵活）
```

### 5. `jobs` - 查看后台任务

```bash
jobs                   # 列出所有后台任务
jobs -l                # 显示任务的PID
fg %1                  # 将任务1调回前台
bg %1                  # 将任务1放到后台运行
```

### 6. `nohup` - 不挂断运行

```bash
nohup command &        # 后台运行，退出终端后继续运行
nohup command > output.log 2>&1 &  # 后台运行并将输出重定向
```

---

## 二、用户和组管理

### 1. `useradd` / `adduser` - 创建用户

```bash
useradd username                     # 创建用户
useradd -m username                  # 创建用户并自动创建家目录
useradd -d /home/custom username     # 指定家目录
useradd -s /bin/bash username        # 指定登录shell
useradd -g groupname username        # 指定主组
useradd -G group1,group2 username    # 指定附加组
useradd -u 1001 username             # 指定UID
useradd -e 2025-12-31 username       # 指定账户过期日期
```

### 2. `usermod` - 修改用户

```bash
usermod -c "Full Name" username      # 添加注释（全名）
usermod -l newname username          # 修改用户名
usermod -L username                   # 锁定用户（禁止登录）
usermod -U username                   # 解锁用户
usermod -aG groupname username       # 将用户添加到附加组（-a必须和-G一起用）
usermod -s /bin/zsh username         # 修改登录shell
```

### 3. `userdel` - 删除用户

```bash
userdel username                     # 删除用户
userdel -r username                   # 删除用户及其家目录、邮件池
```

### 4. `groupadd` / `groupmod` / `groupdel` - 组管理

```bash
groupadd groupname                   # 创建组
groupadd -g 1005 groupname           # 指定GID创建组
groupmod -n newname oldname          # 修改组名
groupmod -g 2000 groupname           # 修改GID
groupdel groupname                   # 删除组
```

### 5. `passwd` - 密码管理

```bash
passwd                               # 修改当前用户密码
passwd username                       # 修改指定用户密码（root可操作）
passwd -l username                    # 锁定用户密码
passwd -u username                    # 解锁用户密码
passwd -d username                    # 删除用户密码（无需密码登录）
passwd -S username                    # 显示用户密码状态
```

### 6. `su` - 切换用户

```bash
su                                   # 切换到root用户（保留当前环境）
su -                                 # 切换到root用户（完全切换环境）
su - username                        # 切换到指定用户
```

### 7. `sudo` - 以其他用户身份执行

```bash
sudo command                         # 以root执行命令
sudo -u username command             # 以指定用户执行命令
sudo -l                               # 列出当前用户的sudo权限
sudo -i                               # 切换到root交互式shell
sudo -s                               # 以root启动shell
sudo -k                               # 使sudo密码缓存立即失效
```

---

## 三、磁盘和文件系统管理

### 1. `df` - 查看磁盘空间使用情况

```bash
df                                   # 查看磁盘分区使用情况
df -h                                # 以人类可读方式显示（GB, MB）
df -T                                # 显示文件系统类型
df -i                                # 显示inode使用情况
df -a                                # 显示所有文件系统
df -t ext4                           # 只显示ext4类型的文件系统
df /home                             # 查看指定目录所在分区的使用情况
```

### 2. `du` - 查看文件和目录大小

```bash
du -h                                # 人类可读方式显示
du -s                                # 只显示总计（不显示子目录）
du -sh *                             # 显示当前目录下所有文件和目录的总大小
du -ah                               # 显示所有文件（包括子目录）的大小
du --max-depth=1                     # 显示目录深度为1的大小
du -sh /home/*                       # 查看home下每个用户目录的大小
```

### 3. `mount` / `umount` - 挂载/卸载

```bash
mount                                # 查看所有已挂载的分区
mount /dev/sdb1 /mnt/data            # 挂载设备到指定目录
mount -t ntfs /dev/sdc1 /mnt/win     # 指定文件系统类型挂载
mount -o ro /dev/sdb1 /mnt/data      # 以只读方式挂载
mount -o remount,rw /                # 重新挂载为读写模式
umount /mnt/data                     # 卸载挂载点
umount -l /mnt/data                  # 懒惰卸载（设备空闲时卸载）
```

### 4. `fdisk` / `parted` - 磁盘分区

```bash
fdisk -l                             # 查看所有磁盘分区信息
fdisk /dev/sdb                       # 对/dev/sdb进行分区操作
parted -l                            # 查看分区表信息
```

### 5. `mkfs` - 创建文件系统

```bash
mkfs.ext4 /dev/sdb1                  # 格式化为ext4
mkfs.xfs /dev/sdb1                   # 格式化为xfs
mkfs.ntfs /dev/sdb1                  # 格式化为ntfs
mkfs -t ext4 /dev/sdb1               # 同上
```

### 6. `fsck` - 检查文件系统

```bash
fsck /dev/sdb1                       # 检查文件系统
fsck -f /dev/sdb1                    # 强制检查（即使看起来干净）
fsck -y /dev/sdb1                    # 对所有问题自动回答yes
fsck -C /dev/sdb1                    # 显示进度条
```

---

## 四、系统信息和监控

### 1. `uname` - 查看系统信息

```bash
uname -a                             # 显示所有系统信息
uname -r                             # 显示内核版本
uname -m                             # 显示硬件架构（x86_64, arm等）
uname -n                             # 显示主机名
uname -s                             # 显示内核名称
```

### 2. `free` - 查看内存使用

```bash
free                                 # 查看内存使用情况
free -h                              # 人类可读方式显示
free -m                              # 以MB为单位显示
free -g                              # 以GB为单位显示
free -s 5                            # 每5秒刷新一次
free -t                              # 显示总内存（包括swap）
```

### 3. `uptime` - 查看系统运行时间

```bash
uptime                               # 查看系统已运行时间、负载等
```

### 4. `dmesg` - 查看内核日志

```bash
dmesg                                # 查看内核环缓冲区消息
dmesg | tail -20                     # 查看最后20条内核消息
dmesg -T                             # 显示人类可读的时间戳
dmesg -w                             # 实时等待新消息
```

### 5. `lscpu` - 查看CPU信息

```bash
lscpu                                # 显示CPU架构信息
```

### 6. `lsblk` - 查看块设备信息

```bash
lsblk                                # 以树形结构显示所有块设备
lsblk -f                             # 显示文件系统信息
lsblk -m                             # 显示权限和所有者信息
```

### 7. `lspci` / `lsusb` - 查看硬件设备

```bash
lspci                                # 查看PCI设备
lspci -v                             # 详细显示
lsusb                                # 查看USB设备
lsusb -v                             # 详细显示USB设备
```

### 8. `dmidecode` - 查看硬件信息

```bash
dmidecode                            # 显示DMI/SMBIOS信息
dmidecode -t memory                  # 查看内存信息
dmidecode -t processor                # 查看处理器信息
dmidecode -t bios                    # 查看BIOS信息
```

---

## 五、网络管理

### 1. `ifconfig` / `ip` - 网络接口配置

```bash
ifconfig                             # 查看所有网络接口（已淘汰，但仍可用）
ifconfig eth0                        # 查看指定接口
ifconfig eth0 up/down                 # 启用/禁用接口

ip addr                              # 查看IP地址（推荐）
ip link                              # 查看链路层信息
ip route                             # 查看路由表
ip addr add 192.168.1.100/24 dev eth0 # 添加IP地址
ip link set eth0 up/down              # 启用/禁用接口
```

### 2. `ping` - 测试网络连通性

```bash
ping baidu.com                       # 持续ping
ping -c 5 baidu.com                  # ping 5次后停止
ping -i 2 baidu.com                  # 间隔2秒发送一次
ping -s 1000 baidu.com               # 发送1000字节的数据包
ping -f baidu.com                    # 洪水ping（需要root）
```

### 3. `netstat` / `ss` - 查看网络连接

```bash
netstat -tln                         # 显示TCP监听端口
netstat -uln                         # 显示UDP监听端口
netstat -an                          # 显示所有连接
netstat -r                            # 显示路由表
netstat -i                            # 显示网络接口统计

ss -tln                              # 显示TCP监听端口（更快）
ss -uln                              # 显示UDP监听端口
ss -s                                # 显示socket统计信息
```

### 4. `curl` / `wget` - 下载和HTTP请求

```bash
curl http://example.com               # 获取网页内容
curl -o file.html http://example.com  # 保存到文件
curl -I http://example.com            # 只获取HTTP头
curl -X POST -d "key=value" http://api # POST请求

wget http://example.com/file.zip      # 下载文件
wget -c http://example.com/file.zip   # 断点续传
wget -r http://example.com            # 递归下载
wget -O newname.zip http://example.com/file.zip # 保存为指定名称
```

### 5. `ssh` - 远程登录

```bash
ssh user@hostname                    # 远程登录
ssh -p 2222 user@hostname            # 指定端口
ssh -i key.pem user@hostname         # 使用密钥登录
ssh -X user@hostname                 # 启用X11转发
ssh -L 8080:localhost:80 user@hostname # 本地端口转发
```

### 6. `scp` - 远程复制文件

```bash
scp file.txt user@hostname:/home/    # 本地文件复制到远程
scp user@hostname:/home/file.txt .   # 远程文件复制到本地
scp -r dir/ user@hostname:/home/     # 递归复制目录
scp -P 2222 file.txt user@hostname:/home/ # 指定端口
```

### 7. `traceroute` / `mtr` - 路由跟踪

```bash
traceroute baidu.com                 # 跟踪路由路径
mtr baidu.com                        # 结合ping和traceroute
```

---

## 六、系统服务管理

### 1. `systemctl` - Systemd 服务管理（主流发行版）

```bash
systemctl start service_name         # 启动服务
systemctl stop service_name          # 停止服务
systemctl restart service_name       # 重启服务
systemctl reload service_name        # 重新加载配置
systemctl status service_name        # 查看服务状态
systemctl enable service_name        # 设置开机自启
systemctl disable service_name       # 禁用开机自启
systemctl is-enabled service_name    # 查看是否开机自启
systemctl list-units --type=service  # 列出所有服务
systemctl daemon-reload              # 重新加载systemd配置
```

### 2. `service` - SysVinit 服务管理（旧系统）

```bash
service service_name start           # 启动服务
service service_name stop            # 停止服务
service service_name restart         # 重启服务
service service_name status          # 查看状态
```

### 3. `journalctl` - 查看系统日志

```bash
journalctl                           # 查看所有日志
journalctl -u service_name           # 查看指定服务的日志
journalctl -f                        # 实时跟踪日志
journalctl --since "2025-01-01"      # 查看指定时间后的日志
journalctl --until "2025-01-02"      # 查看指定时间前的日志
journalctl -p err                     # 查看错误级别日志
journalctl -n 100                     # 查看最后100条日志
```

---

## 七、计划任务

### 1. `crontab` - 定时任务

```bash
crontab -l                           # 列出当前用户的定时任务
crontab -e                           # 编辑定时任务
crontab -r                           # 删除所有定时任务
crontab -u username -l               # 查看指定用户的定时任务（root可用）
```

**crontab格式：**
```
* * * * * command_to_execute
│ │ │ │ │
│ │ │ │ └── 星期几 (0-7, 0或7代表周日)
│ │ │ └──── 月份 (1-12)
│ │ └────── 日期 (1-31)
│ └──────── 小时 (0-23)
└────────── 分钟 (0-59)
```

### 2. `at` - 一次性任务

```bash
at 10:00                             # 设置任务在10:00执行
at now + 1 hour                      # 1小时后执行
atq                                  # 查看等待的任务
atrm job_id                          # 删除任务
```

---

## 八、系统关机/重启

```bash
shutdown -h now                      # 立即关机
shutdown -h 10                       # 10分钟后关机
shutdown -r now                      # 立即重启
shutdown -c                          # 取消已计划的关机

reboot                               # 重启
halt                                 # 停止系统
poweroff                             # 关机
init 0                               # 关机
init 6                               # 重启
```

---

## 九、查看系统信息综合命令

```bash
# 系统版本
cat /etc/os-release                  # 查看发行版信息
lsb_release -a                       # 查看LSB信息

# 内核和系统
hostname                             # 查看主机名
hostnamectl                          # 查看系统信息（systemd）

# 运行时间
uptime                               # 查看运行时间和负载

# 系统限制
ulimit -a                            # 查看系统资源限制
```

---

## 🎯 常用组合技巧

```bash
# 查找占用CPU最高的进程
ps aux --sort=-%cpu | head -10

# 查找占用内存最高的进程
ps aux --sort=-%mem | head -10

# 实时监控特定进程
watch -n 1 'ps -p PID -o pid,ppid,cmd,%cpu,%mem'

# 查看某个用户的进程
ps -u username -o pid,cmd,%cpu,%mem --sort=-%cpu

# 查看系统负载
uptime && top -b -n 1 | head -10

# 查看网络连接数
netstat -an | grep ESTABLISHED | wc -l

# 查看所有开放端口
ss -tuln
```

---

这些系统管理命令覆盖了日常运维的大部分场景。想深入了解某个命令的详细用法，可以随时用 `man 命令名` 查看完整手册！