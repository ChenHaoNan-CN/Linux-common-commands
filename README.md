

---

### 🐧 Linux 通用命令大全 · 速查表
| 场景 | 子场景 | 命令示例（含最常用选项） | 一句话备注 |
|---|---|---|---|
| **🏠 文件系统** | 路径跳转 | `cd -` | 快速切回上一次目录 |
| | 查看占用 | `du -sh * \| sort -h` | 当前目录磁盘占用 Top |
| | 剩余空间 | `df -h` | 人类可读格式 |
| | 挂载点 | `findmnt` | 树形展示所有挂载 |
| | 安全删除 | `shred -vz -n3 文件` | 覆写 3 次再清空 |
| **🔍 查找与定位** | 文件名 | `find /etc -type f -iname "*.conf"` | 忽略大小写 |
| | 内容检索 | `rg -i "关键字" /var/log` | ripgrep 比 grep 快 |
| | 毫秒定位 | `locate -ie bashrc` | 依赖 updatedb 索引 |
| | 打开次数 | `history \| awk '{print $2}' \| sort \| uniq -c \| sort -nr \| head` | 最常敲的命令 Top10 |
| **📄 文本处理** | 高亮分页 | `bat /etc/ssh/sshd_config` | 行号 + 语法高亮 |
| | 实时追加 | `tail -f /var/log/nginx/access.log` | 调试必备 |
| | 关键字染色 | `tail -f xxx.log \| grep --color=always -E "错误\|WARN"` | 多关键字高亮 |
| | 列切割 | `awk -F: '{print $1,$3}' /etc/passwd` | 打印用户名与 UID |
| | 去重排序 | `sort -u file` 或 `uniq -d file` | 重复行 / 唯一行 |
| | 差异对比 | `diff -u old.conf new.conf` | 统一上下文格式 |
| | 并排对比 | `sdiff -w 80 old new` | 终端 80 列并排 |
| **🗜️ 归档压缩** | 打包 | `tar czf etc.tar.gz /etc` | z = gzip |
| | 解压 | `tar xvf file.tar.xz -C /tmp` | 自动识别压缩算法 |
| | 分卷 | `tar czf - dir/ \| split -b 100M - backup.tar.gz.` | 每卷 100 MB |
| | 极速拷贝 | `rsync -aP /src/ /dst/` | 断点续传 + 进度条 |
| **👤 用户/权限** | 新增用户 | `sudo useradd -m -s /bin/zsh alice` | 自动建家目录 |
| | 改密码 | `sudo passwd alice` | 交互式 |
| | 免密 sudo | `sudo visudo` → `alice ALL=(ALL) NOPASSWD:ALL` | 谨慎使用 |
| | 文件授权 | `chmod 644 file` / `chmod +x script.sh` | 数字 / 符号双写法 |
| | 改属主 | `sudo chown -R www-data:www-data /var/www` | 递归 |
| | 特殊位 | `chmod g+s dir` | 目录下文件自动继承组 |
| **🔥 进程与性能** | 树形进程 | `htop` 或 `btm` | 比 top 更漂亮 |
| | 端口监听 | `ss -tulnp` | 替代 netstat |
| | 杀进程 | `pkill -f "关键字"` | 支持模糊匹配 |
| | 后台运行 | `nohup long.sh >out 2>&1 &` | 退出终端仍存活 |
| | 定时任务 | `crontab -e` → `*/10 * * * * /path/script` | 每 10 分钟 |
| | 系统负载 | `uptime` / `cat /proc/loadavg` | 1/5/15 分钟平均负载 |
| | CPU 温度 | `sensors` | 需 `lm_sensors` |
| | 内存排序 | `ps aux --sort=-%mem \| head` | 吃内存 Top |
| **🌐 网络** | 本机 IP | `ip -4 -br addr` | 无颜色简洁格式 |
| | 网关 | `ip route \| grep default` | 一键看网关 |
| | 测延迟 | `ping -c4 1.1.1.1` | 仅 4 次 |
| | 路由跟踪 | `mtr -r 8.8.8.8` | 动态 traceroute |
| | 下载 | `wget -c http://example.com/file.iso` | 断点续传 |
| | 多线程 | `aria2c -x16 -s16 URL` | 16 线程飙车 |
| | 端口扫描 | `nc -zv 192.168.1.1 22-443` | 纯 bash 自带 |
| | 临时传文件 | `python3 -m http.server 8080` | 当前目录变 HTTP |
| **🔗 软链接** | 创建 | `ln -sv /data/iso ~/iso` | 显示过程 |
| | 查看源 | `readlink -f /usr/bin/python` | 递归追踪到底 |
| **🕒 时间与定时** | 立即同步 | `sudo ntpd -qg` | 一次性矫正 |
| | 硬件时钟 | `sudo hwclock --systohc` | 系统时间写回 BIOS |
| | 倒计时 | `sleep 180 && notify-send "水开了"` | 桌面通知 |
| | 秒级时间戳 | `date +%s` | 10 位 Unix 时间 |
| **🖥️ 硬件信息** | CPU | `lscpu` | 型号/核心/线程 |
| | 内存 | `lsmem -o SIZE` | 物理条大小 |
| | PCI 设备 | `lspci -nnk \| grep -A3 VGA` | 显卡驱动 |
| | USB | `lsusb -tv` | 树形速度等级 |
| | 磁盘 | `lsblk -o NAME,SIZE,TYPE,ROTA` | 机械/固态一目了然 |
| **🛡️ 安全** | 生成随机密码 | `openssl rand -base64 12` | 12 位 |
| | 擦除磁盘 | `sudo dd if=/dev/zero of=/dev/sdX bs=4M status=progress` | 不可恢复 |
| | 防火墙 | `sudo ufw enable && sudo ufw default deny incoming` | 一键最小化 |
| | SELinux 状态 | `getenforce` | Enforcing / Permissive |
| **🧹 其他小技巧** | 清空终端 | `clear` 或快捷键 `Ctrl+l` | 保留回滚 |
| | 重复上条 | `!!` | 超级方便 |
| | 上条最后一个参数 | `!$` | 少敲很多字 |
| | 安全重启 | `sudo systemctl reboot -i` | 立即忽略 inhibitor |
| | 安全关机 | `sudo systemctl poweroff -i` | 同上 |

---

### 🎨 终端配色提示（可选）
```bash
# 让 man 页彩色
export MANPAGER="sh -c 'col -bx | bat -l man -p'"
# diff 高亮
alias diff='diff --color=auto'
# grep 高亮
alias grep='grep --color=auto'
```

---

### ⚡ 一行安装「通用瑞士军刀」
```bash
# Debian/Ubuntu
sudo apt install curl wget git vim nano htop btop rsync ripgrep fd-find bat exa tree psmisc lsof

# RHEL/CentOS
sudo dnf install curl wget git vim nano htop rsync ripgrep fd-find bat tree psmisc lsof
```

---

祝使用愉快，我的朋友
