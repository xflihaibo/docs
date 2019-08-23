npm 是什么？ npx 是什么？ nvm 又是什么？ nrm 又是什么？你分的清吗

![](https://user-gold-cdn.xitu.io/2018/11/21/167359e08b98095d?w=600&h=326&f=jpeg&s=47246)

## npm

npm 的全称是 Node Package Manager 是 JavaScript 世界的包管理工具,并且是 Node.js 平台的默认包管理工具。通过 npm 可以安装、共享、分发代码,管理项目依赖关系。

#### 常用命令

```code
npm install 安装模块
npm uninstall 卸载模块
npm update 更新模块
npm outdated 检查模块是否已经过时
npm ls 查看安装的模块
npm init 在项目中引导创建一个package.json文件
npm help 查看某条命令的详细帮助
npm root 查看包的安装路径
npm config 管理npm的配置路径
npm cache 管理模块的缓存
npm start 启动模块
npm stop 停止模块
npm restart 重新启动模块
npm test 测试模块
npm version 查看模块版本
npm view 查看模块的注册信息
npm adduser  用户登录
npm publish 发布模块
npm access 在发布的包上设置访问级别
npm package.json的语法
```

#### npm 上传自己的包

```code
npm install AAA   //检查npm 是否存在
```

-   如果没有 新建一个 AAA 的文件夹

```code
cd  AAA>
npm init  -y
```

-   进入 package.json 文件

```code
 "name": "AAA", //必填项目名称
 "version": "0.0.1" //必填版本信息
 "main":'./dist/index.js'//暴露的文件地址名称
```

-   登录 npm

```code
 npm login //输入用户名、密码和邮箱
```

没有账号去(npm)[https://www.npmjs.com/]注册账号

-   更新 npm 包时，记得修改 package.json 文件夹中的 version 版本信息
-   执行

```code
 npm publish
```

-   利用 npm 撤销发布包

```code
 npm unpublish 包名
```

-   好的一个自定义的包就发布好了只需要在你需要用到的项目下 npm install AAA --save-dev 就可以加载到你的包了

## nvm

-   在开发中，有时候对 node 的版本有要求，有时候需要切换到指定的 node 版本来重现问题等。遇到这种需求的时候，我们需要能够灵活的切换 node 版本
-   nvm 就是为解决这个问题而产生的，他可以方便的在同一台设备上进行多个 node 版本之间切换

#### 常用命令

```code
npm  install   -g   nrm //安装
nvm install ## 安装指定版本，可模糊安装，如：安装v6.2.0，既可nvm install v6.2.0，又可nvm install 6.2
nvm uninstall ## 删除已安装的指定版本，语法与install类似
nvm use ## 切换使用指定的版本node
nvm ls ## 列出所有安装的版本
nvm ls-remote ## 列出所以远程服务器的版本（官方node version list）
nvm current ## 显示当前的版本
nvm alias ## 给不同的版本号添加别名
nvm unalias ## 删除已定义的别名
nvm reinstall-packages ## 在当前版本node环境下，重新全局安装指定版本号的npm包
```

-   nvm 不支持 Windows，但是有替代品，也就是 nvm-windows，

## n

-   n 是 node 一个模块，可以用来管理和切换 node 版本，其作者是 TJ Holowaychuk（出名的 Express 框架作者），使用非常之简单。

#### 常用命令

```code
npm install -g n
n //查看已安装版本
n latest  //安装最新版本并使用
n latest -d   //下载最新版但不使用，-d参数表示为仅下载
n stable  //安装最新稳定版本并使用
n <version>  //安装某个版本并使用，如$n 6.2.2
n rm <version ...> //删除某些版本
n ls    //查看可用版本
n --latest    //查看最新版本
n --stable    //查看最新稳定版
n -h    //查看帮助信息，更多命令在这里查看
```

-   这意味着，我们在使用 n 管理 node 版本前，首先需要一个 node 环境。我们或者用 Homebrew（mac） 来安装一个 node，或者从官网下载 pkg 来安装，总之我们得先自己装一个 node —— n 本身是没法给你装的。

## nrm 自由切换 npm 源

-   nrm(npm registry manager )是 npm 资源管理器，允许你快速切换 npm 源

#### 常用命令

```code
npm install -g nrm  nrm 安装
nrm ls  列出可用的源
nrm use taobao 选择国内淘宝的源
nrm test npm 测试速度
nrm add taobao http://192.168.10.127:8081/repository/npm-public/  添加源
nrm del  taobao删除对应的源
```

## npx

-   npm v5.2.0 引入的一条命令（npx），npx 会帮你执行依赖包里的二进制文件。引入这个命令的目的是为了提升开发者使用包内提供的命令行工具的体验
-   全局安装 parcel，但有时不同项目使用不同版本，不允许使用全局包，只能考虑下面一些方法
    使用 npm scripts，在 package.json 加一个 script ,将 node_modules 的可执行目录加到 PATH 中.指定可执行命令路径
-   当我们执行 npx parcel index.html 时，会自动去./node_modules/.bin 目录下搜索。

```code
old:
npm install -g create-react-app
create-react-app my-app
new:
npx create-react-app my-app
```
