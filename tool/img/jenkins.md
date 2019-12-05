# JenKins

Jenkins 是一款开源 CI&CD 软件，用于自动化各种任务，包括构建、测试和部署软件

持续部署：一种软件开发实践，即团队开发成员经常集成他们的工作，通过每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。每次集成都通过自动化的构建（包括编译、发布、自动化测试）来验证，从而尽早地发现集成错误
持续集成：在持续集成的基础上，将集成后的代码部署到更贴近真实运行环境的「类生产环境」（production-like environments）中。比如，完成单元测试后，可以把代码部署到连接数据库的 Staging 环境中更多的测试。如果代码没有问题，可以继续手动部署到生产环境中。
持续交付：在持续交付的基础上，把部署到生产环境的过程自动化。

### 优化

降低风险
减少重复过程
任何时间、任何地点生成可部署的软件
增强项目的可见性

### Jenkins 和 Hudson

目前最流行的一款持续集成及自动化部署工具。
Jenkins 和 Hundson 之间的关系:2009 年，甲骨文收购了 Sun 并继承了 Hudson 代
码库。在 2011 年年初，甲骨文和开源社区之间的关系破裂，该项目被分成两个独立的

## 安装

首先要先下载 java 依赖包 和 git

```javascript
yum install java
yum install git
```

首先要先添加 Jenkins 源

```javascript
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
```

```javascript
yum install jenkins //完成之后直接使用 yum 命令安装 Jenkins
```

Jenkins 修改权限

```javascript
vim / etc / sysconfig / jenkins;
```

找到\$JENKINS_USER 改为 “root”:
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3350cc48faa?w=966&h=275&f=png&s=21929)
然后更改执行以下命令 Jenkins home，webroot 和日志的所有权：

```javascript
chown -R root:root /var/lib/jenkins
chown -R root:root /var/cache/jenkins
chown -R root:root /var/log/jenkins
```

## 启动

```javascript
service jenkins restart  //启动 jenkins
```

jenkins 启动成功
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f33aafb99dd0?w=971&h=50&f=png&s=6718)

### 应用

在本地浏览器输入你的 ip 地址加 默认端口 8080 就可以看到 jenkins 解锁页面啦
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f343fa6c8754?w=1671&h=579&f=png&s=57240)
要输入管理员密码
那么刚刚安装的时候忘记保存了也没关系
页面上有提示 那我们就 去指定的目录找吧
vim /var/lib/jenkins/secrets/initialAdminPassword
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f348f82c5659?w=675&h=98&f=png&s=10156)
就得到了密码串 复制到输入框执行一下步吧
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f34bb82e467c?w=992&h=562&f=png&s=65578)
选择安装推荐的插件即可
等待安装
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f351bcff65fb?w=1049&h=711&f=png&s=66424)
不用多说输入就好了 执行 保存并完成
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3544aaeefc2?w=997&h=440&f=png&s=26596)
下一步默认 就好了 开始使用 jenkins
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3564779ddaa?w=1002&h=287&f=png&s=21774)

## 应用

## 配置

### 全局安全配置

用户角色对 Jenkins 操作权限配置

### 全局工具配置

### 管理插件

jenkins 插件下载，功能扩展安装
