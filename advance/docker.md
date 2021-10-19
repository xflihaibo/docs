# docker

-   [Docker](https://www.docker.com/) 是一个开源的引擎，可以轻松的为任何应用创建一个轻量级的、可移植的、自给自足的容器。开发者在笔记本上编译测试通过的容器可以批量地在生产环境中部署，包括 VMs（虚拟机）、bare metal、OpenStack 集群和其他的基础应用平台。

### Docker 通常用于如下场景：

1.  web 应用的自动化打包和发布；
2.  自动化测试和持续集成、发布；
3.  在服务型环境中部署和调整数据库或其他的后台应用；
4.  从头编译或者扩展现有的 OpenShift 或 Cloud Foundry 平台来搭建自己的 PaaS 环境。

### 底层技术支持

1.Namespaces :做隔离 pid net ipc mnt uts
2.Control groups :做资源限制
3.Union file systems: Container 和 image 的分层

#### 安装 docker 启动

```bash
yum -y install docker-io
 systemctl start docker ||  service docker start //启动
 yum -y install docker-io

docker info //查看信息
docker version //查看版本

decker run --detach centos ping www.baidu.com  //后台运行doker容器

systemctl start docker #启动
systemctl restart docker #重启
systemctl stop docker #停止
systemctl status docker #查看状态
systemctl enable docker #自启动
systemctl disable docker #禁止自启动

http://dockone.io/article/104
```

## docker-Image

https://hub.docker.com/explore/

-   文件和 meta data 的集合
    分层的，并且每一层都可以添加改变，删除文件 成为一个新的 image
    不同的 image 可以共享相同的 layer
    Image 本身是 read-only

## Container

1 通过 Image 创建
2 在 Image layer 之上建立一个 container layer（可读写）
3 类比面向对象：类和实例
4Image 负责 app 的存储和分发 Container 负责运行 app

```code
docker container ls 列举本地运行的程序
docker container ls -a 列举本地所有的程序
docker run -it  hello-world 交互运行

docker  container cp cb4acb4acb4a:/u.txt u.txt 复制docker 文件到指定目录
```

## docker-machine

-   docker-machine 是 Docker 官方提供的一个工具，它可以帮助我们在远程的机器上安装 Docker，或者在虚拟机 host 上直接安装虚拟机并在虚拟机中安装 Docker。我们还可以通过 docker-machine 命令来管理这些虚拟机和 Docker。下面是来自 Docker Machine 官方文档的一张图，很形象哦！

-   Docker Machine 的目的是简化 Docker 的安装和远程管理。从本文的内容我们也可以看到，Docker Machine 确实为我们使用和管理 Docker 带来了很多的便利。至于有待提高的方面，现在 Docker Machine 会安装最新版本的 Docker，笔者觉得如果能够支持指定安装 Docker 的版本就好了！

*   安装 docker-machine

```code
https://github.com/docker/machine/releases
curl -L https://github.com/docker/machine/releases/download/v0.16.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
    chmod +x /tmp/docker-machine &&
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine

docker-machine version //查看版本

http://m.elecfans.com/article/624284.html

docker-machine create [OPTIONS] [arg...] //创建虚拟机
docker-machine rm [OPTIONS] [arg...] //移除虚拟机
docker-machine ssh [arg...] //登录虚拟机
docker-machine env [OPTIONS] [arg...] //docker客户端配置环境变量
docker-machine inspect //检查机子信息
docker-machine ls [OPTIONS] [arg...]. //查看虚拟机列表
docker-machine status [arg...]  //一个虚拟机名称 //查看虚拟机状态
docker-machine start [arg...]  //一个或多个虚拟机名称.//启动虚拟机
docker-machine stop [arg...]  //一个或多个虚拟机名称 //停止虚拟机
docker-machine restart [arg...]  //一个或多个虚拟机名称 //重启虚拟机
```

## Docker Engine

-   人们提到 Docker，一般而言，大家说的是 Docker Engine

```code
Docker Engine 由三个部分组成：
Docker 进程（Docker Daemon）
REST API：指定了和进程交互的接口
CLI(command line interface)：通过 REST API 和 daemon 通信，诸如：docker run <image>, docker ps...
Docker Machine 是一种提供管理主机的 工具。常规，你会安装 Docker Machine 在你的本地机器上。
Docker Machine 有自己的命令client：docker-machine
Docker Engine 则有client：docker
```

Docker Machine 来安装 Docker Engine 在一个或者多个虚拟系统上，这些虚拟系统可以是本地的（比如 Virtualbox 里），也可以是远程的（云）

#### 配置 docker 国内代理

```code
mkdir -p /etc/docker
//写入 国内代理地址
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://fwvjnv59.mirror.aliyuncs.com"]
}
```

#### 重启程序 docker

```code
systemctl daemon-reload
systemctl restart docker
```

#### image 镜像

-   Docker 把应用程序及其依赖，打包在 image 文件里面。只有通过这个文件，才能生成 Docker 容器
-   image 文件可以看作是容器的模板
-   Docker 根据 image 文件生成容器的实例 container 容器
-   同一个 image 文件，可以生成多个同时运行的容器实例
-   一个 image 文件往往通过继承另一个 image 文件，加上一些个性化设置而生成

```code
docker search ubuntu //查找镜像
docker pull  docker.io/ubuntu //拉取镜像
docker rmi    docker.io/ubuntu //删除镜像
docker image ls //查看本地镜像mi
docker run hello-world //运行镜像实例
docker run ubuntu  /bin/echo "hello" 运行实例 并且打印 hello
```

#### Dockerfile

> Dockerfile 文件模版

```code
FROM node             //继承的镜像
COPY ./app /app     //拷贝镜像
WORKDIR /app     //当前工作目录
RUN npm install    //安装依赖
EXPROSE 3000    //暴露端口号
ENV   //设置变量  容器内部可以获取到参数
ARG     //设置变量  可以在命令行加参数覆盖
CMD //容器默认启动执行
```

### 常用命令

```shell
docker attach xxx(container id)
docker container run -d(--detach) -p 90:80 nginx
docker container stop 2bbd 停止容器运行
docker container start  2bb 启动容器
docker container rm $(docker container ps -aq) 删除容器
docker container logs 2bb 查看日志
docker container logs 2bbd -- follow(-f) 持续查看日志
docker container kill  2bbd6 停止容器运行（暴力）
docker container run ubuntu sh
docker container run  -it ubuntu /bin/bash  运行容器并且进入容器
docker exec -it xxx sh 进入容器内部
docker exec -it xxx bash  进入容器内部
docker pull image nginx
docker image save nginx:latest -o mynginx.image
docker image load -i ./mynginx.image
docker tag  镜像id 新镜像名称：版本
docker cp 文件名称 容器id:容器内部路径  把文件拷贝到容器内部
docker container cp 8335:/u.txt u.txt  拷贝docker 容器的文件
docker image prune -a  清理无容器使用的镜像
docker container ps //获取运行的容器
docker container ps -a //获取所有的容器
docker container ps -l 最新
eixt 退出docker 容器
```

数据卷：将宿主机的一个目录映射到容器的一个目录中，可以在宿主机中操作目录中的文件，那么容器内部的文件，也会一起修改

```bash
docker volume create 数据卷名称 //创建数据卷
#创建数据卷之后，默认会存放在一个目录下 /var/lib/docker/volume/数据卷名称/data
docker volume inspect 数据卷名称  //查看数据卷信息
docker volume ls
docker volume rm  数据卷名称
doceke run -v 数据卷名称:容器内部路径 容器id //当映射数据卷时，如果不存在，docker 会自动创建(会把容器内部同步一下)
doceke run -v 路径:容器内部路径 容器id //直接制定一个路径作为数据卷存放位置
docker container run -d(--detach) -p 90:80 nginx -v 数据卷名称:容器内部路径
```

### docker-compose

之前运行一个镜像需要添加大量参数，可以通过 docker-compose 编写这些参数，同时可以批量管理容器
需要 docker-compose.yml 文件管理维护

#### docker-compose.yml 模版

```yml
varsion: '3.1'
services:
    mysql: # 服务名称
        restart: 'always' #跟容器一起启动
        image: daocloud.io/library/mysql:5.7.5-m15 # 指定镜像路径
        container_name: mysql # 指定容器名称
        ports:
            - 3306:3306 #端口号
        envitoment:
            MYSQL_ROOT_PASSWORD: root # mysql 指定的root 登录密码
        volumes:
            - /opt/docker_mysql/data:/var/lib/mysql #映射数据卷
```

#### docker-compose 命令

```shell
docker-compose up  -d     #基于docker-compose.yml启动
docker-compose down # 删除
docker-compose start/stop/restart #启动/停止/重启
docker-compose ps   # 查看
docker-compose logs -f # 日志
docker-compose up -d  # 日志
docker-compose build # 重新构建自定义镜像
```

#### docker-compose 配置自定义 Dockerfile

```yml
varsion: '3.1'
services:
    mynginx: # 服务名称
        restart: 'always' #跟容器一起启动
        build:
            context: ../ #指定dockerfile 文件所在路径
            dockerfile: Dockerfile #指定指定dockerfile文件名称
        image: mynginx:1.0.0
        container_name: mynginx # 指定容器名称
        ports:
            - 8080:8080 #端口号
        envitoment:
            TZ: Asia/Shanghai
        volumes:
            - /opt/docker_mysql/data:/var/lib/mysql #映射数据卷
```

### Dockerfile

```
from daocloud.io/library/nginx:1.12.0-alpine
copy
```

# podman

[Podman](https://podman.io/)  是一个开源的容器运行时项目，可在大多数  Linux  平台上使用。Podman  提供与  Docker  非常相似的功能。正如前面提到的那样，它不需要在你的系统上运行任何守护进程，并且它也可以在没有  root  权限的情况下运行。
