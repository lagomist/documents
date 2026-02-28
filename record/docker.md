# docker

Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从 Apache2.0 协议开源。

---

# 安装

## 下载安装

参考文档：[dockerdocs](https://docs.docker.com/engine/install/ubuntu/)

更新 apt 包索引。  
`sudo apt update`  

安装最新版本的 Docker Engine-Community 和 containerd  
`sudo apt install docker-ce docker-ce-cli containerd.io`

添加用户到docker组  
`sudo usermod -aG docker $USER`

## 网络配置

设置docker pull代理：

1. 创建 dockerd 相关的 systemd 目录，这个目录下的配置将覆盖 dockerd 的默认配置
```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
```

2. 新建配置文件 `/etc/systemd/system/docker.service.d/http-proxy.conf`，写入以下环境变量

```ini
[Service]
Environment="HTTP_PROXY=http://127.0.0.1:10808"
Environment="HTTPS_PROXY=http://127.0.0.1:10808"
```

3. 重新加载配置文件，重启 dockerd
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

4. 检查确认环境变量已经正确配置：
```bash
sudo systemctl show --property=Environment docker
```

---

# 命令大全

## 容器生命周期管理
- run
- start/ stop/ restart
- kill
- rm
- pause/ unpause
- create
- exec
	
## 容器操作
- ps
- inspect
- top
- attach
- events
- logs
- wait
- export
- port
- stats

## 容器rootfs命令
- commit
- cp
- diff

## 镜像仓库
- login
- pull
- push
- search

## 本地镜像管理
- images
- rmi
- tag
- build
- history
- save
- load
- import
- info|version
- info
- version

---

# 容器

## 启动容器
以下命令使用 ubuntu 镜像启动一个容器，参数为以命令行模式进入该容器：

`docker run -it --privileged
 --hostname 主机名 --name 容器名 -v <本地目录路径>:<容器侧挂载点> ubuntu bash`  

参数说明：

- -i: 交互式操作。
- -t: 终端。
- -d: 后台运行。
- --privileged 提高容器权限
- -v: 目录挂载
- --network： 网络名。
- --hostname： 容器主机名。
- --name： 容器名。
- ubuntu: ubuntu 镜像。
- /bin/bash：放在镜像名后的是命令，这里我们希望有个交互式 Shell，可用bash或忽略  

要退出终端，直接输入 exit 或 Ctrl+D

## 停止容器
停止容器的命令如下：
`docker stop <容器 ID>`

停止的容器可以通过 docker restart 重启：

`docker restart <容器 ID>`

## 进入容器
在使用 -d 参数时，容器启动后会进入后台。此时想要进入容器，可以通过以下指令进入：

`docker attach <容器 ID>`

`docker exec`：此命令会退出容器终端，但不会导致容器的停止。

## 删除容器
删除容器使用 `docker rm` 命令：

`docker rm -f CONTAINER_ID`

删除所有容器  
`docker rm $(docker ps -a -q)`

## 导出容器

如果要导出本地某个容器，可以使用 `docker export` 命令。

`docker export CONTAINER_ID > container.tar`

## 导入容器快照

可以使用 `docker import` 从容器快照文件中再导入为镜像，以下实例将快照文件 container.tar 导入到镜像 image:v1:

`docker import container.tar image:v1`

- image ：创建的镜像的命名
- v1 ：TAG标签

---

# 镜像

## 列出镜像列表
我们可以使用 docker images 来列出本地主机上的镜像。

`docker images`

- REPOSITORY：表示镜像的仓库源
- TAG：镜像的标签
- IMAGE ID：镜像ID
- CREATED：镜像创建时间
- SIZE：镜像大小

## 获取新镜像

可以使用 docker pull 命令来下载新镜像

`docker pull ubuntu:13.10`

## 查找镜像

我们可以从 Docker Hub 网站来搜索镜像，[Docker Hub]( https://hub.docker.com/)

也使用 `docker search` 命令来搜索镜像

## 拖取镜像

使用命令 `docker pull` 来下载镜像。例如：  
`docker pull httpd`

## 删除镜像

镜像删除使用 docker rmi 命令，比如我们删除 hello-world 镜像：  
`docker rmi hello-world`

删除所有镜像  
`docker rmi $(docker images -q)`

## 更新镜像

可以通过命令 `docker commit` 来提交容器副本。例如：  

`docker commit -m="has update" -a="runoob" e218edb10161`

各个参数说明：

- -m: 提交的描述信息
- -a: 指定镜像作者
- e218edb10161：容器 ID
- runoob/ubuntu:v2: 指定要创建的目标镜像名

## 构建镜像

我们使用命令 `docker build` ，从零开始来创建一个新的镜像。为此，我们需要创建一个 `Dockerfile` 文件，其中包含一组指令来告诉 Docker 如何构建我们的镜像。  
例如：
`docker build -t runoob/centos:6.7 .`

参数说明：

- -t ：指定要创建的目标镜像名
- . ：Dockerfile 文件所在目录，可以指定Dockerfile 的绝对路径

## 设置镜像标签

我们可以使用 docker tag 命令，为镜像添加一个新的标签。  
例如：  
`docker tag 860c279d2fec runoob/centos:dev`

---

# 常用操作

## 查看系统内存

`docker system df`

## 容器里网络代理
编辑 `~/.bashrc`添加以下内容
```bash
PROXY() {
    export https_proxy="http://172.17.0.1:10808"
    export http_proxy="http://172.17.0.1:10808"
    export all_proxy="socks5://172.17.0.1:10808"
    export ALL_PROXY="socks5://172.17.0.1:10808"
    echo "set proxy to 172.17.0.1:10808"
}

UNPROXY() {
    unset http_proxy https_proxy all_proxy ALL_PROXY
    echo "Proxy unset"
}

```
## 设置语言环境
编辑 `~/.bashrc`添加以下内容
```bash
export LANG=C.UTF-8
export LC_ALL=C.UTF-8
```