# WSL1

## vim replace mode
1. 问题描述  

	在windows 10的WSL1环境中，使用vim启动时默认进入REPLACE模式

2. 解决办法  

	编辑 .vimrc  
	` vim ~/.vimrc`  
	加入一行配置  
	`nnoremap <esc>^[ <esc>^[`
	

---

# Ubuntu

## apt 更新出错
1. 问题描述  

更新软件时，提示以下信息
> E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)  
> E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?

2. 解决办法  

方案一：

`sudo killall apt apt-get`

如果提示没有apt进程：

> apt: no process found  
> apt-get: no process found

方案二：  
依次执行：
```
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock*
sudo dpkg --configure -a
sudo apt update
```
## ch34x串口问题
1. 问题描述
使用ch34x驱动连接单片机时，`dmesg | grep ttyUSB`出现以下日志
```
usb 3-1.4: ch341-uart converter now attached to ttyUSB0
usb 3-1.4: usbfs: interface 0 claimed by ch341 while 'brltty' sets config #1
ch341-uart ttyUSB0: ch341-uart converter now disconnected from ttyUSB0
```
2. 解决办法

删除`brltty`这个软件：
```bash
sudo apt purge brltty
```

---

# Ubuntu(arm64)

## PyQt5安装卡死
1. 问题描述  

	使用 `pip install pyqt5`安装时卡死：  
	preparing metadata pyproject toml  

2. 解决办法  
	
	因为pip源无编译好的aarch64的whl包，需要下载PyQt5和sip的源码包进行自动编译  
	一条指令编译安装pyqt5：  
	`pip install pyqt5 --config-settings --confirm-license= --verbose`
	
## 进入桌面出现崩溃报告

1. 问题描述  

	因为各种原因，系统程序启动时出现问题，如Xorg、lightdm等，每次启动都会出现报告

2. 解决办法  

	查看或删除崩溃报告文件  
	`/var/crash/*`  

	临时禁用崩溃报告： 
	`sudo service apport stop`  
	
	永久禁用崩溃报告： 编辑 `/etc/default/apport` 文件，	将`enabled=1` 改为 `enabled=0`