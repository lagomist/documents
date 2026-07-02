# Memorandum(备忘录)

---

## Markdown
链接：[Markdown语法](https://markdown.com.cn)

---

# Ubuntu

## 软件镜像源

[中科大](https://mirrors.ustc.edu.cn/) Ubuntu22.04 ARM源（ubuntu-ports）
```
# 默认注释了源码仓库，如有需要可自行取消注释
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy main main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-security main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-proposed main restricted universe multiverse
# deb-src https://mirrors.ustc.edu.cn/ubuntu-ports/ jammy-proposed main restricted universe multiverse
```

## 终端网络代理
` vim .bashrc `
```
PROXY() {
    export https_proxy="http://127.0.0.1:10808"
    export http_proxy="http://127.0.0.1:10808"
    export all_proxy="socks5://127.0.0.1:10808"
    export ALL_PROXY="socks5://127.0.0.1:10808"
    echo "set proxy to 127.0.0.1:10808"
}

UNPROXY() {
    unset http_proxy https_proxy all_proxy ALL_PROXY
    echo "Proxy unset"
}
```
使用  
` PROXY`  
终端命令加 `-E`,如:  
` sudo -E add-apt-repository --update ppa:ubuntu-toolchain-r/test `

---

## zip 解压缩
解压到当前目录  
` unzip xxx.zip `

解压到指定文件夹  
` unzip file.zip -d destination_folder `

压缩目录  
` zip -r xxx.zip dir `

---

## tar 解压缩
Tar选项：

* c – 创建压缩文件
* x – 解压文件
* v – 显示进度.
* f – 文件名.
* t – 查看压缩文件内容.
* j – 通过bzip2归档
* z – 通过gzip归档
* r – 在压缩文件中追加文件或目录
* W – 验证压缩文件

e.g.  
tar压缩:  
` tar -cvf code.tar /home/abc/code/ `

tar解压:  
` tar -xvf code.tar -C /home/abc/code `

## rar解压缩
使用unrar工具：
```bash
unrar x xxx.rar
```

---

## 根目录扩容

[参考链接](https://blog.csdn.net/YDJ18234492659/article/details/120887652)

查看磁盘信息：	`df -h`  

查看磁盘分区状态：	`fdisk -l`  

开始扩容：  

1. 进入磁盘： `parted /dev/xvdb`  
	`/dev/xvdb` 替换有空闲的磁盘  
2. 查看分区详情: `p` 
3. 对分区进行扩容:	`resizepart 1`
	`1` 替换为根目录挂载的分区 
4. 扩容大小  
	`-0`	将剩余所有空间都分给分区
5. 退出磁盘: `q`  
6. 查看根目录大小是否有变化:	`df -h`
7. 更新磁盘信息: `resize2fs /dev/xvdb`  
	`/dev/xvdb` 替换所扩容的磁盘

---

## 文件管理
列出文件夹中文件详细信息  
` ls -l `

查看文件类型  
` file name `

查看文件访问时间  
` stat name `

查看目录文件大小  
`du -sh `  
- s 合计目录下的文件大小
- h 格式化大小显示

查找文件  
`find [指定目录] [指定条件] [指定动作]`  
`find ./ -name "example.txt"`

查找库文件
`dpkg -S libxxx.a`

创建软链接
`ln -s 源地址 目标地址`

---

## 查看进程
终端中查看所有进程  
` ps -aux `

查看目标进程  
` ps -aux | grep xxx `

关闭目标进程  
` killall -9 <proc-name> ` 	相当于pidof+kill  
` pkill -9 <proc-name> ` 相当于pgrep+kill

---

## 安装,移除deb包
安装  
` sudo dpkg -i path_to_deb_file `

修复依赖项  
` sudo apt install -f `

自动处理依赖安装  
`sudo apt install -y --fix-broken path_to_deb_file`

移除  
` dpkg -r program_name `

---

## 查询已安装软件
使用 apt 命令  
` sudo apt list --installed | grep xxx `

使用 dpkg 命令  
` dpkg -l | grep xxx `

查看被依赖程序
`apt rdepends --installed xxx`

---

## 用户相关
### 用户组
1. 查看所属组  
`groups`  
2. 创建用户组  
`sudo groupadd docker`  
3. 加入用户组  
`sudo usermod -aG docker $USER`  

### 修改主机名
1. 查看当前主机名  
` hostnamectl `  
2. 修改主机名为HOST  
` sudo hostnamectl set-hostname HOST `

### 修改密码
`sudo passwd user`

### 修改用户名

推荐方式：
`usermod -l user1 -m user0 -d /home/user1`

* `-l user1`：将登录名从 `user0` 改为 `user1`
* `-d /home/user1`：设置新的家目录路径
* `-m`：**移动**原有家目录内容到新路径（若不加 `-m`，只改路径但不移动文件）

其他方式：
1. 转为root用户：`sudo su`  
2. 编辑修改所有原有用户名`vim /etc/passwd`	 
3. 编辑修所有原有改用户名`vim /etc/shadow`  
4. 编辑修所有原有改用户名`vim /etc/group`  
5. 执行以下命令，给目录重命名。 
`cd /home`  
`sudo mv old_user_name new_user_name`  
6. 编辑修改所有原有用户名`vim /etc/sudoers`  
7. 重启

### 图形界面登陆用户
`sudo vim /etc/lightdm/lightdm.conf`  
修改user：
```
[Seat:*]
Aautologin-guest=false
Aautologin-user=user
Aautologin-user-timeout=0
```

### WSL1登陆用户
WSL中编辑修改用户  
`vim /etc/wsl.conf`

---

## 相关功能路径
软件源路径  
`/etc/apt/sources.list`  
`/etc/apt/sources.list.d/*`  

CPU温度路径  
` /sys/class/thermal/thermal_zone0/temp`  

用户全局变量路径  
` ~/.profile `  
` ~/.bashrc  `

自动磁盘挂载路径  
`/etc/fstab`

---

## UFW 防火墙
查看防火墙状态  
` sudo ufw status `

允许应用端口访问  
` sudo ufw allow appname `

打开端口  
`sudo ufw allow port_number/protocol `
打开端口范围  
`sudo ufw allow port_1:port_2/protocol`

删除UFW规则  
直接删除  
`sudo ufw delete deny port_number`

or  
`sudo ufw delete allow port_number/protocol`

使用序号删除  
` sudo ufw status numbered `  
` sudo ufw delete 1 `

---

## SSH

1. 文件传输：

- file_path：需要替换为要上传文件的路径  
- orangepi：修改为开发板 linux 系统的用户名  
- 192.168.xx.xx: 为开发板的 IP 地址，请根据实际情况进行修改  
- /home/orangepi: 修改为开发板 linux 系统中的路径  

`scp file_path orangepi@192.168.xx.xx:/home/orangepi/`  

将文件从远程机器复制到本地机器  

`rsync username@ip_address:/home/username/filename .`  

将文件从本地机器复制到远程机器

`rsync filename username@ip_address:/home/username`  

2. 清除IP公钥信息：
```bash
ssh-keygen -R 192.168.31.33
```

---

## 系统镜像备份
使用dd命令将带镜像的SD中的镜像拷贝到新创建的目录中  
` sudo dd if=/dev/sda of=./image_backup.img count=8192 bs=1M conv=sync `

上图dd命令参数的含义：

- if=文件名：输入文件名，缺省为标准输入。即指定源文件。< if=/dev/sda >

- of=文件名：输出文件名，缺省为标准输出。即指定目的文件。<of=./image_backup.img>,这里的.img是镜像的格式，转成.img格式的文件后方便后续烧录镜像

- bs = bytes：同时设置读入/输出的块大小为bytes个字节，填1024k，表示1M大小。

- count = blocks：仅拷贝blocks个块，块大小等于ibs指定的字节数，设置的是8192，表示8192个bs，也就是8G。

- conv= sync：将每个输入块填充到ibs个字节，不足部分用空（NUL）字符补齐。

**(若备份的镜像仍无法正常运行，请将bs=1024k改为bs=1M并去掉conv参数)**

2. 运行时备份
```bash
# 原板执行
sudo sync
echo 3 | sudo tee /proc/sys/vm/drop_caches

# 然后在 PC 端拉取
ssh <USER>@<IP> "sudo dd if=/dev/mmcblk0 bs=4M status=progress" > backup.img
```

---

## 串口终端

使用`screen`命令连接串口

`sudo screen /dev/ttyUSB0 115200`

使用`minicom`命令连接串口

`sudo minicom -D /dev/ttyUSB0 -b 115200`

---

## snapd包管理工具

设置网络代理  
`sudo snap set system proxy.http="http://127.0.0.1:10809"`  
`sudo snap set system proxy.https="http://127.0.0.1:10809"`

取消网络代理  
`sudo snap set system proxy.http=""`  
`sudo snap set system proxy.https=""`

查看修改  
`snap changes`

清除进程  
`snap abort ID`

---

## python

1. 修改默认python

	查看当前系统默认python版本  
	`python --version`
	
	查看python3  
	`whereis python3`
	
	删除原有python2的软连接  
	`sudo rm /usr/bin/python`
	
	新建python3的软连接  
	`sudo ln -s /usr/bin/python3.5 /usr/bin/python`
	
	现在重新查看默认的python版本  
	`python --version`

2. 创建虚拟环境

```bash
python3 -m venv .venv
```

---

## 动态库配置
1. 设置优先使用当前目录下的动态库
   临时设置：`export LD_LIBRARY_PATH=./`
   用户持久设置：编辑`~/.bash_profile`添加上条配置

2. 添加进系统查找路径
```bash
sudo vim /etc/ld.so.conf
```
下面加一行 `/usr/local/target/lib`
执行后生效
```bash
sudo ldconfig
```
 
---
# Android

## 查看GPIO

```bash
cat /sys/kernel/debug/gpio
gpioinfo
```
