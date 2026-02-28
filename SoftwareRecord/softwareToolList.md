# 软件工具

## Qv2ray

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 网络代理客户端，实现VPN和网络加速 |
| 说明 | Ubuntu QT图形界面使用 |

**二.安装**

1.安装snapd：`sudo apt install snapd`  
2.安装qv2ray，两个方式：  
2.1.安装snap-store：`sudo snap install snap-store`  
    然后使用图形界面搜索`qv2ray` 并安装
2.2.终端直接安装：`sudo snap install qv2ray`

**三.用法**

启动软件  
订阅地址：[购买订阅](https://jxdy.top/#/dashboard)  
订阅配置更新，设置入站代理端口后，即可连接使用  

---

## uGet

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 多链路下载工具 |
| 说明 | 图形界面使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install uget aria2`  

**三.用法**

安装完毕后在应用中心找到`uGet`双击启动
在`settings ` 中的插件选择`aria2`即可

---

## ghostwriter

**一.描述**

| 描述 | 内容          |
|----|-------------|
| 功能 | Markdown编辑器 |
| 说明 | 图形界面使用      |图形界面使用      |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install ghostwriter`

**三.用法**

安装完毕后在应用中心找到`ghostwriter`双击启动

**四.体验**

主题多样，观赏性好。但在Ubuntu-xfce环境下中文输入有问题，勉强能用。

---

## ReText

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | Markdown编辑器 |
| 说明 | 图形界面使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install retext`

**三.用法**

安装完毕后在应用中心找到`ReText`双击启动

**四.体验**

编辑和预览独立性强，基于Qt与python,平台支持广泛，但界面简单，没有目录支持。

---

## Zettlr

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | Markdown编辑器 |
| 说明 | 图形界面使用 |

**二.安装**
[Zettlr官网](https://www.zettlr.com/)
访问下载安装包，在终端中打开安装包目录
`sudo dpkg -i Zettlr-3.0.5-arm64.deb`  
`Zettlr-3.0.5-arm64` 切换为具体的安装包

**三.用法**

安装完毕后在应用中心找到`Zettlr`双击启动

**四.体验**

是一款非常适合撰写专业文本的 MarkDown 编辑器，Zettlr 特有的文献引用、聚焦模式、热图搜索、代码高亮、组织结构几大特色都可以让 MarkDown 从编辑器变身生产力工具。
支持目录导航，功能齐全，比上面两款Markdown编辑器好用。

---

## GoldenDict

**一.描述**

| 描述 | 内容 |
| --- | --- |
| 功能 | 翻译软件 |
| 说明 | 图形界面使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install goldendict`

**三.用法**

安装完毕后在应用中心找到`goldendict`双击启动

**四.体验**

免费开源、个性化强。

---

## arp-scan

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 可用于局域网下的网络主机扫描 |
| 说明 | Ubuntu终端使用 |

**二.安装**

 ` sudo apt install  arp-scan `
 
**三.用法**

扫描设备  
` sudo arp-scan -I wlan0 --localnet `

` wlan0 ` 替换成目标网口

---

## FileZilla

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 可用于局域网下基于FTP协议的文件传输 |
| 说明 | 图形界面使用 |

**二.安装**

`sudo apt install filezilla`
 
**三.用法**

安装完毕后在应用中心找到`FileZilla`双击启动
**注意：** 传输二进制文件时可能会被转换类型，修改传输类型为二进制解决

---

## cutecom

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 串口调试工具 |
| 说明 | 图形界面使用 |

**二.安装**

`sudo apt install cutecom`
 
**三.用法**

安装完毕后在应用中心找到`cutecom`双击启动  

---

## qrcp

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 局域网文件传输工具 |
| 说明 | 命令行使用，创建本地http服务，实现与移动设备的文件传输 |

**二.安装**

github：[下载](https://github.com/claudiodangelis/qrcp)  
支持windows、linux各个架构  

**三.用法**

打开终端命令行：  
1. 配置  

	`qrcp --help` 查看用法  
	`qrcp config` 配置软件  
2. 发送  
	
	`qrcp MyDocument.pdf` 发送一个文件  
	`qrcp MyDocument.pdf IMG0001.jpg` 发送多个文件  
	`qrcp Documents/` 发送整个文件夹  
	`qrcp --zip LongVideo.avi` 发送前压缩  
3. 接收  

	`qrcp receive` 接收文件  
	`qrcp receive --output=/tmp/dir` 指定路径接收  

---

## KDiskMark

**一.描述**

| 描述 | 内容         |
|----|------------|
| 功能 | 开源磁盘性能测试工具 |
| 说明 | Qt图形界面使用   |

**二.安装**

github：[KDiskMark](https://github.com/JonMagon/KDiskMark)  
Ubuntu ARM64 安装：
```bash
sudo add-apt-repository ppa:jonmagon/kdiskmark
sudo apt update
sudo apt install kdiskmark
```
删除软件源：
```bash
sudo add-apt-repository --remove ppa:jonmagon/kdiskmark
```

**三.用法**

安装完毕后在应用中心找到`KDiskMark`双击启动  
	
---

# 开发工具

## mosquitto
                                                                         
**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | MQTT服务器 实现消息代理 |
| 说明 | Ubuntu终端使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install mosquitto`

**三.用法**

1.配置：  
在/etc/mosquitto/conf.d目录下，添加配置文件`myconfig.conf` ：  
` sudo vim /etc/mosquitto/conf.d/myconfig.conf `

粘入下面这些配置：  

```
# 添加监听端口（很重要，否则只能本机访问）
listener 1883
# 关闭匿名访问，客户端必须使用用户名
allow_anonymous false
# 指定 用户名-密码 文件
password_file /etc/mosquitto/pwfile

```
2.添加账户及密码：  
` sudo mosquitto_passwd -c /etc/mosquitto/pwfile 用户名 `

3.打开防火墙端口：  
` sudo ufw allow 1883/tcp `

4.启动：  
该应用由systemctl服务管理，可开机自启动  
重启mosquitto  
` sudo service mosquitto restart `

查看mosquitto运行状态  
` sudo service mosquitto status `

### mosquitto-clients
安装：  
`sudo apt-get install mosquitto-clients`

订阅主题  
`mosquitto_sub -h 服务器地址 -t "topic/" -u 用户名 -P 密码 -i “client_id”`

发布主题  
`mosquitto_pub -h 服务器地址 -t "topic/" -u 用户名 -P 密码 -m "消息"`

---

## CasaOS

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 开源家庭云系统 |
| 说明 | 服务应用 |

**二.安装**

1. 安装Docker  
`sudo curl -sSL https://get.docker.com | sh`  
2. 安装CasaOS  
`curl -fsSL https://get.casaos.io | sudo bash`

**三.用法**

安装完成后，脚本会启动服务，并监听在 80 端口上。在浏览器上输入 `http://IP地址` 进行访问

卸载：`casaos-uninstall`

---

## vsftpd

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 开源FTP服务器 可用于文件传输 |
| 说明 | 服务应用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install vsftpd`

**三.用法**

服务器配置：  

1. 配置  
	编辑修改`sudo vim /etc/vsftpd.conf`  ，注意参数后不要有空格！
```
write_enable=YES  
connect_from_port_20=NO
# port模式的数据端口  
ftp_data_port=10090
# pasv模式的端口范围  
pasv_enable=Yes
pasv_min_port=10090
pasv_max_port=10100
# 配置ftp服务器的上传下载文件所在的目录  
local_root=/home/username/ftp/
```

2. 重启FTP服务器  
	`sudo service vsftpd restart` 

3. 打开UFW端口  
	`sudo ufw allow 21/tcp`  
	`sudo ufw allow 10090:10100/tcp`

客户端配置：  

1. 连接服务器  

	安装FTP客户端  
	`sudo apt install ftp`
	
	连接服务器  
	`ftp server_addr`
2. 传输文件

	列出本地目录文件  
	`！ls`  
	切换本地目录  
	`lcd /local/path/`  
	
	列出远程服务器目录内容  
	`ls`  
	下载文件  
	`get filename`  
	上传文件  
	`put filename`  
	退出客户端  
	`quit`

**四.体验**

操作简单，开源简洁，可用于小型开发板

---

## x11vnc

**一.描述**

| 描述 | 内容               |
|----|------------------|
| 功能 | VNC远程桌面服务器       |
| 说明 | 服务应用，无连接显示器，容易卡顿 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install x11vnc`

**三.用法**

设置密码  
`sudo x11vnc -storepasswd`  

创建systemd服务文件  
`sudo vim /etc/systemd/system/x11vnc.service`
粘贴以下内容(修改USERNAME)  
```
[Unit]
Description=Start x11vnc at startup.
After=multi-user.target

[Service]
Type=simple
ExecStart=/usr/bin/x11vnc -auth guess -forever -noxdamage -repeat -rfbauth /home/USERNAME/.vnc/passwd -rfbport 5900 -shared
 
[Install]
WantedBy=multi-user.target
```

启动服务  
`sudo systemctl enable x11vnc.service`  
`sudo systemctl start x11vnc.service`

服务配置  
修改分辨率  
`sudo vim /etc/X11/xorg.conf`

文件内容（修改分辨率：1920 1080）  
```
Section "Device"
        Identifier "Configured Video Device"
EndSection
Section "Monitor"
        Identifier "Configured Monitor"
EndSection
Section "Screen"
        Identifier "Default Screen"
        Monitor "Configured Monitor"
        Device "Configured Video Device"
        SubSection "Display"
                   Depth 24
                   Virtual 1920 1080
        EndSubSection
EndSection
```

**四.体验**

配置简单，平台兼容好，但有延迟较高，容易出bug,如有拖影等缺点。

---

## NoMachine

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 跨平台的远程桌面控制软件 |
| 说明 | 图形界面使用，包含服务端和客户端 |

**二.安装**

[官网地址](https://www.nomachine.com/)

**三.用法**

安装完毕后在应用中心找到`NoMachine`或 `NoMachine Service`启动  

**四.体验**

开源免费的远程桌面软件，支持各种环境、架构，使用体验比较流畅，比VNC软件的显示效果要好不少。服务端不连接显示器，容易卡顿，需要额外设置。

---

## QT

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 跨平台的GUI开发框架 |
| 说明 | 图形界面使用 |

**二.安装**

[官方下载](https://download.qt.io/official_releases/qt/)

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install qtbase5-dev qtbase5-dev-tools qtchooser qt5-qmake qtcreator`

- qtbase5-dev: 提供了C++类库以及开发Qt程序所需的基础工具，包括Qt核心、网络、数据库访问、事件处理等功能。
- qtbase5-dev-tools: 包含了一些开发工具，如Qt Designer和Qt Linguist等，这些工具用于创建用户界面和翻译Qt应用程序。
- qtchooser: 是一个图形化工具，用于选择Qt运行环境。
- qt5-qmake: 是Qt5的构建工具，用于编译和链接Qt应用程序。
- qtcreator: 是一个跨平台的集成开发环境(IDE)，专门为Qt开发人员设计，提供了代码编辑、调试、测试等一系列开发工具。
- qtbase5-examples: 提供了Qt库的示例代码，方便开发者学习和使用。
- qtbase5-doc-html: 包含了Qt库的官方文档，以HTML格式提供。

**三.用法**

安装完毕后在应用中心找到`Qt Creator`双击启动  

**四.体验**

直接使用软件库安装，简单方便，但无法选择版本，体验与windows环境无差别。

---

## miniconda

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 小巧的python环境管理工具 |
| 说明 | 终端、IDE使用 |

**二.安装**

官网下载安装包：[miniconda](https://docs.conda.io/projects/miniconda/en/latest/)

打开终端运行  
`bash ./Miniconda3-latest-Linux-aarch64.sh`

同意许可，和指定安装目录等

**三.用法**

激活环境变量  
`source .bashrc`

取消自动激活  
`conda config --set auto_activate_base false`

**四.体验**

精简版的conda,python包和环境管理工具，创建虚拟环境很好用

---

# 娱乐软件

## Fceux

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | FC游戏模拟器 运行.nes游戏 |
| 说明 | Ubuntu 图形界面使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install fceux`

**三.用法**

安装完毕后在应用中心找到**Fceux**双击启动  
或者是在终端输入命令：` fceux `启动模拟器  
点击file->open rom打开已经下载好的nes游戏

---

## Game Conqueror

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 游戏内存修改器 |
| 说明 | Ubuntu 图形界面使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install gameconqueror`

**三.用法**

安装完毕后在应用中心找到**Game Conqueror**双击启动  
使用方式与CE类似

---

## DeSmuME

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | nds游戏模拟器 运行.nds游戏 |
| 说明 | 安装后有两个启动器（Gtk，Gtk-Glade）Gtk-Glade为增强版，CPU占用高，运行没问题建议使用Gtk |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
`sudo apt install desmume`

**三.用法**

安装完毕后在应用中心找到**DeSmuME**双击启动  

---

## NetHack

**一.描述**

| 描述 | 内容 |
| ------- | ------- |
| 功能 | 有名的RPG游戏 |
| 说明 | 图形界面或控制台使用 |

**二.安装**

打开终端（CTRL+ALT+T）：  
`sudo apt update`  
控制台 字符模式 
`sudo apt install nethack-console`  
或图形界面 贴图模式  
`sudo apt install nethack-qt`

**三.用法**

安装完毕后在应用中心找到`nethack`双击启动  

或者控制台输入`nethack`启动  

**四.体验**

悠久的来历，复古的风格，难度较高。

---
