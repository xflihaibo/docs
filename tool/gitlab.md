## 安装

```shell
[root@gitlab ~]# yum install -y curl policycoreutils-python openssh-server        #安装依赖
[root@gitlab ~]# wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el7/gitlab-ce-10.2.2-ce.0.el7.x86_64.rpm        #下载软件包
[root@gitlab ~]# rpm -ivh gitlab-ce-10.2.2-ce.0.el7.x86_64.rpm    #安装gitlab
```

```shell
[root@gitlab ~]# vim /etc/gitlab/gitlab.rb      #编辑配置文件
external_url 'http://192.168.1.21'        #改为自己的IP地址
[root@gitlab ~]# gitlab-ctl reconfigure    #重新加载配置文件
```

主要服务构成
nginx 静态 web 服务器
gitlab-workhorse 轻量级反向服务器
gitlab-shell 处理 git 命令修改 authorized keys 列表
logrotate 日志文件管理工具
postgresql 数据库
redis 缓存服务器

支持内置 HA 保证高并发也仍旧实现高可用行

开发管理
运维管理

admin area systeminof 产看系统状况

## 常用命令

```shell
sudo gitlab-ctl reconfigure :重启配置，并启动 gitlab 服务
sudo gitlab-ctl start :启动所有 gitlab s
sudo gitlab-ctl restart :重新启动 GitLab
sudo gitlab-ctl stop :停止所有 gitlab
sudo gitlab-ctl status: 查看服务状态
sudo gitlab-ctl tail :查看 Gitlab 日志
sudo vim /etc/gitlab/gitlab.rb :修改默认的配置文件
gitlab:check SANITIZE=true --trace :检查 gitlab gitlab-rake

```
