# docker
## docker容器工业化部署
docker就是用容器化技术给应用程序封装独立的运行环境，每个运行环境就是一个容器，运行容器的计算级被称为宿主机。
docker容器与虚拟机的最大区别是docker容器之间共用同一个系统内核，虚拟机包含一个操作系统的完整内核，所以docker比虚拟机更轻更小，启动速度更快。
另外一个概念是镜像，镜像（大）是容器（小)的模板，镜像可以类比成是软件安装包，而容器就是安装好的软件
docker仓库就是存放分享镜像的地方，可以把镜像上传到dockers仓库里边，官方镜像仓库docker hub
docker是基于linux的容器化技术，windows和mac是虚拟了一个linux子系统来运行docker
官方镜像仓库docker hub


## 🔗 1. 安装docker

### ubantu系统服务器上运行docker
```bash
~$ curl -fsSL https://get.docker.com -o install-docker.sh
~$ sudo sh install-docker.sh
```
sudo是管理员权限，super user do

### 在Windows下载运行docker
官网下载桌面版可视化docker或者命令行
```bash
start /w"" "Docker Desktop Installer.exe" intall --intallation-dir=D:\Docker
```
输入docker --version打印版本号则显示安装成功


## 🔗 2. 拉镜像

docker pull命令用来从镜像仓库下载镜像

### 基本用法
```bash
docker pull docker.io/library/nginx:lastest
```
简化后：
```bash
docker pull nginx
```

### pull命令详解
pull命令由4部分组成（两个/）：
- **docker.io** - 官方公共仓库地址，可省略官方地址
- **library** - 命名空间，也就是作者名字，可省略官方作者名字
- **nginx** - 要下载的软件
- **:lastest** - 软件的版本号，可指定某个版本（如1.28.0），也可不写表示最新版本

### 使用示例
```bash
docker pull docker.n8n.io/n8nio/n8n
```
下一个开源ai工作流工具n8n

### 功能特性
- 支持DockerHub、gcr.io、k8s.io、ghcr.io等仓库
- 支持最大40GB的大型镜像
- 使用阿里云的官方线路，速度快


## 🔗 3. 启动容器

待补充...
