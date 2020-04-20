# jenkins

### 前期准备

-   liunx 基本命令
-   git 基本命令
-   nginx
-   jenkins
-   [jenkins 清华大学镜像源](https://mirrors.tuna.tsinghua.edu.cn/jenkins/)
-   [jenkins 清华大学插件镜像源](https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json)

##### 工具

-   github 账号和项目
-   git
-   centos 服务器

#### 坐稳啦！ 要发车啦！

### 首先登录你远程服务器地址

输入远程服务器地址

```javascript
ssh 用户名@远程服务器 ip 地址
```

首次登录有提示信息 输入 yes 就好了
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f30502d70a54?w=637&h=118&f=png&s=13698)
登录成功！
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f30832dd10fa?w=638&h=167&f=png&s=12217)

### 安装 nginx

```javascript
nginx - v; //输入查看
```

说明服务器没有安装 nginx
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f30ae24d32aa?w=522&h=71&f=png&s=4963)

```javascript
yum install nginx //输入下载
or
yum install epel-release //如果上一步安装失败
yum install nginx //再次下载
```

```javascript
y; //回车
```

![](https://user-gold-cdn.xitu.io/2018/6/30/1644f30e66d34475?w=586&h=109&f=png&s=5899)

安装完毕！
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f31196252b84?w=925&h=184&f=png&s=18252)

```javascript
nginx - v;
```

![](https://user-gold-cdn.xitu.io/2018/6/30/1644f315b0bfd017?w=412&h=55&f=png&s=3942)
nginx 已经安装完毕

### 修改 nginx 配置

```javascript
nginx - t; //查看配置文件地址
cd / etc / nginx;
ls; //可以看到 nginx.conf 配置文件
```

![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3186732c44b?w=1292&h=135&f=png&s=20262)

```javascript
vim nginx.conf
or
yum install vim //如果没有可以安装vim 再次执行上步
```

### vim 编辑器用法

```javascript
i; //编辑器底部出现 insert 后 你可以编辑配置文件了；
```

![](https://user-gold-cdn.xitu.io/2018/6/30/1644f31eb45a526d?w=1460&h=155&f=png&s=17204)

修改配置 user 改成 root (服务器用户名 我的是 root)
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f320b0802e2a?w=1116&h=160&f=png&s=15799)

这是默认静态资源文件存放的地址
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f322dddc81c9?w=1109&h=527&f=png&s=36091)

```javascript
esc //退出编辑模式
:+ wq //保存退出
nginx -t 查看配置文件是否报错
```

配置显示成功
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3250a3714fe?w=888&h=114&f=png&s=14013)

### 创建项目

```javascript
cd /root
mkdir www
cd www
vim index.html //创建 index.html 文件
```

输入以下内容（hello world）
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f328a38e34a9?w=734&h=276&f=png&s=21180)

保存退出

```javascript
nginx; // 启动nginx server
```

然后在本地浏览器输入你的 ip 地址加/index.html 就能看到大大的 hello world ! 服务器配置 server 结束
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f32ac8bc60aa?w=543&h=172&f=png&s=6504)

## 配置 Jenkins

### 安装

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

### 配置

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

```javascript
service jenkins restart  //启动 jenkins
```

jenkins 启动成功
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f33aafb99dd0?w=971&h=50&f=png&s=6718)

### 启动 Jenkins

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

### 创建任务

开始配置第一个 jenkins 任务
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3588c088f86?w=1055&h=670&f=png&s=43760)
创建一个自由风格的 输入名称 点击确定就好了
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f35be9dd095a?w=1688&h=751&f=png&s=94717)

###### 项目结构

```javascript
admin;
html;
home.html;
js;
home_page.js;
css;
home.css;
```

![](https://user-gold-cdn.xitu.io/2018/6/30/1644f360debbb307?w=1199&h=449&f=png&s=46820)
填写描述、填写你的 git URL 地址
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f362ebdf0628?w=1738&h=934&f=png&s=84535)
在构建中选择“执行 shell” 输入以下命令

```javascript
rm -rf test.tar.gz
tar czvf test.tar.gz *
mv -f test.tar.gz /root/www
cd /root/www
tar -xzvf test.tar.gz
rm -rf test.tar.gz
```

![](https://user-gold-cdn.xitu.io/2018/6/30/1644f3657e5063ba?w=1498&h=572&f=png&s=40919)
点击保存、回到工程项目下 点击立即构建 等待执行完成(成功)
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f368047ed7d2?w=855&h=474&f=png&s=54549)
在本地浏览器输入你的 ip 地址加/html/home.html 就能看到构建的项目了
![](https://user-gold-cdn.xitu.io/2018/6/30/1644f36a658918a5?w=967&h=213&f=png&s=15334)
尝试在 git 上修改文件保存后 执行立即构建 成功后， 然后在本地浏览器刷新 发现代码已经修改

### 主从模式

master -Slave

配置 Slave 然后设置项目编译节点

### 角色和用户管理

Role-based Authorization Strategy 插件

### 下载插件加速

mirrors
update-center
nvm wrapper ：和本地运行 npm script 一样，我们要想在 jenkins 里面执行 npm 命令，先要在 jenkins 里面配置 node 的环境，可以通过配置环境变量的方式引入 node，也可以通过安装插件的方式，这里使用了插件的方式，安装一下 nvm wrapper 这个插件

### 邮件通知

Email Extension Plugin 插件

### 参数化构建

Extended Choice Parameter 插件
Git Parameter git 参数化构建插件

<tbale>
<tr> <th colspan="5"> Overall(全局) </th> <th colspan="6"> Slave(节点) </th> <th colspan="8">  Job(任务  </th> <th colspan="4">  View(视图)   </th></tr>

<tr><td>  Administer   </td><td>    Read     </td><td> RunScripts </td><td> UploadPlugins </td><td> ConfigureUpdateCenter </td><td> Create </td><td> Update </td><td> View </td><td> Delete </td><td> ManageDomains </td><td> Configure </td><td> Delete </td><td> Create </td><td> Disconnect </td><td> Connect Build </td><td> Create </td><td> Delete </td><td> Configure </td><td> Read </td><td> Discover </td><td> Build </td><td> Workspace </td><td> Cancel </td><td> Create </td><td> Delete </td><td> Configure </td><td> Read </td><tr>

<tr><td> 管理员(最大)  </td><td>    阅读     </td><td>  运行脚本  </td><td>升级插件</td><td> 配置升级中心 </td><td> 创建 </td><td> 更新 </td><td> 查看 </td><td> 删除 </td><td> 管理域 </td><td> 配置 </td><td> 删除 </td><td> 创建 </td><td> 断开连接 </td><td> 连接 </td><td> 构建 </td><td> 创建 </td><td> 删除 </td><td> 配置 </td><td> 阅读 </td><td> 重定向 </td><td> 构建 </td><td> 查看工作区 </td><td> 取消构建 </td><td> 创建 </td><td> 删除 </td><td> 配置 </td><td> 阅读 </td></tr>

</tabel>

插件名称
Folders： (https://plugins.jenkins.io/cloudbees-folder),这个插件支持用户使用目录管理项目，目录支持嵌套，并且支持目录中创建视图
OWASP Markup Formatter ： OWASP 标记格式化程序插件,使用 OWASP Java HTML Sanitizer ，可以在项目描述等中输入安全的 HTML 标记
Build Timeout ： 构建超时,此插件允许构建在指定的时间过后自动终止
Credentials Binding： 证书绑定
Timestamper ：将时间戳添加到控制台输出
Workspace Cleanup： (https://plugins.jenkins.io/ws-cleanup),这个插件支持在构建前后 删除或者部分删除 workspace
Ant ：向 Jenkins 添加 Apache Ant 支持
Gradle： 这个插件允许 Jenkins 直接调用 Gradle 构建脚本
Pipeline： 管道,一套插件可让您协调自动化
Pipeline: GitHub Groovy Libraries ：允许从 GitHub 动态加载 Pipeline Groovy 库
Pipeline: Stage View 查看每一步的执行结果
GitHub Branch Source ：GitHub 组织文件夹插件
Git： (https://plugins.jenkins.io/git),支持使用 Github、GitLab、Gerrit 等系统管理代码仓库
Subversion： (https://plugins.jenkins.io/subversion),支持 Subversion 系统管理源代码
SSH Slaves ：SSH 登录到一个远程服务器以执行必要的脚本
Matrix Authorization Strategy： 矩阵授权策略插件,提供基于矩阵的安全授权策略（全局和每个项目）
PAM Authentication ：为 Jenkins 添加 Unix 可插入身份验证模块（PAM）支持
LDAP ：(https://plugins.jenkins.io/ldap),这个插件允许使用 LDAP 对用户进行认证，LDAP 服务器可以为 Active Directory 或者 OpenLDAP
Email Extension： 这个插件是 Jenkins 的电子邮件发布者的替代品。它允许配置电子邮件通知的各个方面：发送电子邮件时，应该收到谁以及电子邮件说明的内容
Mailer ：发邮件服务
Localization: Chinese (Simplified) 本地化构建
