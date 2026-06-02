# docker
## docker容器工业化部署
docker就是用容器化技术给应用程序封装独立的运行环境，每个运行环境就是一个容器，运行容器的计算级被称为宿主机。
docker容器与虚拟机的最大区别是docker容器之间共用同一个系统内核，虚拟机包含一个操作系统的完整内核，所以docker比虚拟机更轻更小，启动速度更快
另外一个概念是镜像，镜像（大）是容器（小)的模板，镜像可以类比成是软件安装包，而容器就是安装好的软件
docker仓库就是存放分享镜像的地方，可以把镜像上传到dockers仓库里边，官方镜像仓库docker hub
docker是基于linux的容器化技术，windows和mac是虚拟了一个linux子系统来运行docker
官方镜像仓库docker hub


## 1. 安装docker

### ubantu系统服务器上运行docker
```bash
~$ curl -fsSL https://get.docker.com -o install-docker.sh
~$ sudo sh install-docker.sh
```
sudo是管理员权限，super user do

一键安装命令
```
sudo curl -fsSL https://get.docker.com| bash -s docker --mirror Aliyun
```
备用命令（每天自动从官网定时同步）
```
sudo curl -fsSL https://github.com/tech-shrimp/docker_installer/releases/download/latest/linux.sh| bash -s docker --mirror Aliyun
```
备用2（如果Github访问不了，可以使用Gitee的链接）
```
sudo curl -fsSL https://gitee.com/tech-shrimp/docker_installer/releases/download/latest/linux.sh| bash -s docker --mirror Aliyun
```
启动docker
```
sudo service docker start
```
### 在Windows下载运行docker
任务栏搜索功能，启用“适用于Linux的Windows子系统”+“虚拟机平台”

<img width="344" height="297" alt="windows功能" src="https://github.com/user-attachments/assets/12b1374b-68f8-4500-a0fd-87eb2b1e3f7c" />

管理员权限打开命令提示符，安装wsl2
```
wsl --set-default-version 2
wsl --update --web-download
```
等待wsl安装成功

<img width="431" height="59" alt="wsl2成功" src="https://github.com/user-attachments/assets/94c8f667-c32a-4ece-ab14-b79fbaed69c3" />




下载Windows版本安装包，进入此项目的Release
https://github.com/tech-shrimp/docker_installer/releases

下载Windows版本安装包

<img width="733" height="327" alt="windows安装包" src="https://github.com/user-attachments/assets/74356e35-0531-4992-b9c9-f77637501c78" />

官网下载桌面版可视化docker或者如果想自己指定安装目录，可以使用命令行的方式 参数 --installation-dir=D:\Docker 可以指定安装位置
```bash
start /w"" "Docker Desktop Installer.exe" intall --intallation-dir=D:\Docker
```
输入`docker --version`打印版本号则显示安装成功


##  2. docker命令

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


##  3. 拉镜像

### 方案一转存到阿里云
使用Github Action将国外的Docker镜像转存到阿里云仓库仓库，供国内服务器使用，免费芭蕉

- 支持DockerHub、gcr.io、k8s.io、ghcr.io等仓库
- 支持最大40GB的大型镜像
- 使用阿里云的官方线路，速度快
项目地址： https://github.com/tech-shrimp/docker_image_pusher

### 方案二镜像站
目前仅有很少的国内镜像站
不能保证镜像站充足，且要优先考虑
以下三个镜像站背靠扩大的开源项目，优先推荐

镜像加速地址

| 项目名称 | 项目地址 | 加速地址 |
|---------|---------|---------|
| 1面板 | https://github.com/1Panel-dev/1Panel/ | https://docker.1panel.live |
| 道云 | https://github.com/DaoCloud/public-image-mirror | https://docker.rm.daocloud.io |
| 耗子面板 | https://github.com/TheTN8/panel | https://hub.rat.dev |

容器配置文件

#### Linux配置镜像站
```
sudo vi /etc/docker/daemon.json
```
进入vi文本编辑器，配置linux下的镜像站

输入以下内容，最后按ESC，输入 :wq! 保存退出。
```
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://docker.1panel.live",
        "https://hub.rat.dev"
    ]
}
```
重启docker
```
sudo service docker restart
```
##### Windows/Mac配置站点
设置->Docker引擎->添加上换源的那一段，如下图
<img width="929" height="532" alt="win加速" src="https://github.com/user-attachments/assets/e63cd48e-5fc3-406a-a1c9-9225e7386cce" />

### 方案三离线镜像
使用Github Action下载docker离线镜像 https://github.com/wukongdaily/DockerTarBuilder

### 方案四使用一键脚本
```
bash -c "$(curl -sSLf https://xy.ggbond.org/xy/docker_pull.sh )" -s 
```
完整镜像名

### 方案五 使用Cloudflareworker自建镜像加速
https://github.com/cmliu/CF-Workers-docker.io

## 3.去哪里找镜像
https://docker.fxxk.dedyn.io/





