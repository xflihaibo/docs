# electron

<div align="center">
  <img src="./advance/img/electron/electron.jpeg" width="300" alt="logo" align="center">
</div>

[Electron](https://electronjs.org/) 是由 Github 开发,使用 JavaScript, HTML 和 CSS 构建跨平台的桌面应用,原理是 electron 通过将 chromium 和 node.js 合并到同一个运行时环境中，并将其打包为 Mac，Windows 和 Linux 系统下的应用来实现这一目的。

## 开始

自动重启工具 nodemoon supervisor

```shall
nodemoon --watch main.js --exec 'electrion .'
 "electron-dev": "concurrently \"npm run start-test\" \"wait-on http://192.168.102.86:3900 && electron .\"",
```

webview 单独有一个进程渲染
可以通过设置 nodeintraction 访问本地电脑资源
可以把自己开发的脚本信息嵌入到网页中
注入样式 html 代码等

delog
选择文件。保存文件 文本提示

## 进程

![electron](./img/electron/ele03.png)

### 主进程- Main Process

1.  可以使用和系统对接的 Electron API-创建菜单,上传文件等
2.  创建渲染进程- Renderer Process
3.  全面支持 Node.js
4.  一个程序只有一个主进程，作为整个程序的入口点

### 渲染进程- Renderer Process

1.  可以有多个,每个对应一个窗口
2.  每个都是一个单独的进程
3.  全面支持 Node.js 和 DOM API
4.  可以使用一部分 Electron 提供的 API

### 主进程(ipcMain)与渲染进程通信(ipcRenderer)

```javascript
//主进程
ipcMain.on('open-data', (event, data) => {
  console.log(data);
  event.sender.send('send-file');
});

//渲染进程
//发送消息
ipcRenderer.send('open-data');
//监听消息
ipcRenderer.on('send-file', (event, data) => {
  console.log(data);
});
```

## 调试

### 主进程调试

![electron](./img/electron/elemain01.png)
![electron](./img/electron/elemain02.png)
![electron](./img/electron/elemain03.jpeg)
![electron](./img/electron/elemain04.png)
![electron](./img/electron/elemain05.jpeg)
![electron](./img/electron/elemain06.png)

#### 渲染进程

![electron](./img/electron/eleipc01.png)
![electron](./img/electron/eleipc03.png)
![electron](./img/electron/eleipc02.png)

## 主进程(ipcMain)与渲染进程(ipcRenderer) 模块

shell
screen
clipborad :剪切
crashReporter :崩溃报告
nativeImage: 图片

## 主进程(ipcMain)

app
BrowserWindow
webContents：控制渲染网页
ipcMain
dialog
Menu
MenuItem
net ：http
protocol：
session
Tray：通知栏区域图标
systemPerferences：获取偏好设置
globalhortcut：定义快捷键
contentTracing：收集跟踪性能瓶颈
powerSaveBlocker:阻止系统进入睡眠模式
powerMonitor：监听电源更改
autoUpdater：自动更新

## 渲染进程(ipcRenderer) 模块

ipcRenderer
desktopCapturer:捕获桌面声音视频
romote：获取主进程模块
webFrame:渲染网页

## 模块

devtron 开发调试工具
electrion-is-dev ：判断开发环境生产环境
fs-extra: fs 文件操作
wait-on

electron-shared miniblink :优化打包体积

node-auto-launch：开机自启动

```javascript
let NodeAutoLaunch = require('node-auto-launch');
let electronAuto = new NodeAutoLaunch({
  name: 'appName'
  path:'/Applications/appname.app'
});
electronAuto.enabled()
```

electron-store:本地持久化

```javascript
const Store = require('electron-store');

const store = new Store();

store.set('unicorn', '🦄');
console.log(store.get('unicorn'));
//=> '🦄'

// Use dot-notation to access nested properties
store.set('foo.bar', true);
console.log(store.get('foo'));
//=> {bar: true}

store.delete('unicorn');
console.log(store.get('unicorn'));
//=> undefined
```

electron-updater （--save）自动更新检测
electron-builder 打包 难度： 🌟🌟🌟
electron-forge :打包 难度：🌟🌟
electron-is-dev 检查当前(生产 开发)环境

```javascript
const isDev = require('electron-is-dev');

if (isDev) {
  console.log('Running in development');
} else {
  console.log('Running in production');
}
```

[崩溃日志报告](https://electronjs.org/docs/api/crash-reporter#%E5%B4%A9%E6%BA%83%E6%97%A5%E5%BF%97%E6%8A%A5%E5%91%8A)

electron-log 日志

```javascript
const log = require('electron-log');

log.info('Hello, log');
log.warn('Some problem appears');
electron-log支持的日志级别有：error, warn, info, verbose, debug, silly
```

```json
"build": {
    "productName":"xxxx",//项目名 这也是生成的exe文件的前缀名
    "appId": "com.xxx.xxxxx",//包名
    "copyright":"xxxx",//版权  信息
     "compression": "store", // "store" | "normal"| "maximum" 打包压缩情况(store 相对较快)，store 39749kb, maximum 39186kb
    "directories": { // 输出文件夹
      "output": "build"
    },
    "publish": [
      {
        "provider": "generic",
        "url": "http://127.0.0.1:3000/xxx/"
      }
    ],
    "extraResources":  { // 拷贝dll等静态文件到指定位置
        "from": "./app-update.yml",
        "to": "./b.txt"
    },
    "publish": [
        {
          "provider": "generic", // 服务器提供商 也可以是GitHub等等
          "url": "http://xxxxx/" // 服务器地址
        }
      ],
     "asar": true,//asar打包
    "files": [
      "**/*",
      "!docs${/*}",
      "!node_modules/@paulcbetts/cld/deps/cld${/*}"
    ],
    "mac": {
      "category": "public.app-category.productivity",
      "artifactName": "${productName}-${version}-${arch}.${ext}"
    },
    "linux": {
      "category": "Chat;GNOME;GTK;Network;InstantMessaging",
      "packageCategory": "GNOME;GTK;Network;InstantMessaging",
      "description": "etrial Desktop Client for Linux",
      "target": [
        "deb",
        "zip",
        "AppImage",
        "snap"
      ],
      "maintainer": "Akash Nimare <akash@etrial.com>",
      "artifactName": "${productName}-${version}-${arch}.${ext}"
    },
    "deb": {
      "synopsis": "etrial Desktop App",
      "afterInstall": "./scripts/debian-add-repo.sh",
      "afterRemove": "./scripts/debian-uninstaller.sh"
    },
    "snap": {
      "synopsis": "etrial Desktop App"
    },
    "dmg": {
      "background": "hardware/build/appdmg.png",
      "icon": "hardware/build/icon.icns", //路径
      "iconSize": 100,
      "contents": [
        {
          "x": 380,
          "y": 280,
          "type": "link",
          "path": "/Applications"
        },
        {
          "x": 110,
          "y": 280,
          "type": "file"
        }
      ],
      "window": {
        "width": 500,
        "height": 500
      }
    },
    "win": {
      "target": [
        {
          "target": "nsis-web",  //我们要的目标安装包
          "arch": [//// 这个意思是打出来32 bit + 64 bit的包，但是要注意：这样打包出来的安装包体积比较大，所以建议直接打32的安装包
            "x64",
            "ia32"
          ]
        }
      ],
      "icon": "hardware/build/icon.ico", //图标路径
      "artifactName": "${productName}-Web-Setup-${version}.${ext}",
      "publisherName": "XXXX Labs, Inc."
    },
    "nsis": {
      "perMachine": false,//是否开启安装时权限限制（此电脑或当前用户）
      "oneClick": false, // 是否一键安装
      "allowElevation": true, // 允许请求提升。 如果为false，则用户必须使用提升的权限重新启动安装程序。
      "allowToChangeInstallationDirectory": true, // 允许修改安装目录
     "installerIcon": "./build/icons/aaa.ico",// 安装图标
    "uninstallerIcon": "./build/icons/bbb.ico",//卸载图标
    "installerHeaderIcon": "./build/icons/aaa.ico", // 安装时头部图标
    "createDesktopShortcut": true, // 创建桌面图标
    "createStartMenuShortcut": true,// 创建开始菜单图标
    "shortcutName": "xxxx", // 图标名称
    "include": "build/script/installer.nsh", // 包含的自定义nsis脚本 这个对于构建需求严格得安装过程相当有用。
    "script" : "build/script/installer.nsh", // NSIS脚本的路径，用于自定义安装程序。 默认为build / installer.nsi
    }
  }
```

## 打包参数

```shell
 --mac, -m, -o, --macos   Build for macOS,                              [array]
  --linux, -l              Build for Linux                               [array]
  --win, -w, --windows     Build for Windows                             [array]
  --x64                    Build for x64 (64位安装包)                     [boolean]
  --ia32                   Build for ia32(32位安装包)                     [boolean]
  --armv7l                 Build for armv7l                              [boolean]
  --arm64                  Build for arm64                               [boolean]
  --dir                    Build unpacked dir. Useful to test.           [boolean]
  --prepackaged, --pd      预打包应用程序的路径（以可分发的格式打包）
  --projectDir, --project  项目目录的路径。 默认为当前工作目录。
  --config, -c             配置文件路径。 默认为`electron-builder.yml`（或`js`，或`js5`)
```

github- settings->Developer settings-》Personal access tokens=〉Generate new token-》 勾选 repo= Generate token

本地配置 git
export GH_TOKEN=39cd1f807461123618e9d2dea2c596d514128eeb

## 开发串口工具

由于开发串口工具问题较多，所以先总结罗列一些开发流程之前准备的的事情

第一步全局安装
python2.7 (必须) 我的是 2.7.16 版本

```shell
npm i -g node-gyp //可以对Native模块进行重编译。
    or
npm i -g node-pro-gyp 可以对Native模块进行重编译。
npm i -g production windows-build-tools  //编译本机节点模块
```

## node

```javascript
node.js add-on
node-ffi  集成c++
WinRT  蓝牙 usb 预览文件
Applescript
shell
lazyLoad 懒加载
https://developers.google.com/web/updates
视频捕捉
desltopCapturey
webRtc





```

## 项目开发依赖

```shell
npm install --save-dev electron-rebuild 先下载electron-rebuild

# 每次运行"npm install"时，也运行这条命令
./node_modules/.bin/electron-rebuild

# 在windows下如果上述命令遇到了问题，尝试这个：
.\node_modules\.bin\electron-rebuild.cmd
```

## 相关问题链接

1.  (参考链接)[https://blog.csdn.net/naisi2422553065/article/details/90475830]
2.  (参考链接)[http://electronjs.org/docs/tutorial/using-native-node-modules]

## 最小化托盘 window 关闭 用 window.close 事件

## windows 打包引用路径有问题呢

## build 文件名称问题-window 打包报错

## 获取文件路径最好使用 path 拼接，否则 window 打包后报错

## electron-build 在 window 打包 router 失效 配置成多页面

## 推送需要设置 gh_token

## window 开发 打包 32 位系统 可以适配 64 位

npm install --arh=ia32 --platfrom=win32 electron

## electron-build 打包

1.  build.productName:'名称'
2.  react 模板需要在 build 中设置"extends": null,打包忽略 build

## build files 可以做打包体积优化

```json
[
  "!**/node_modules/*/{CHANGELOG.md,README.md,README,readme.md,readme}",
  "!**/node_modules/_/{test,**tests**,tests,powered-test,example,examples}",
  "!**/node_modules/_.d.ts",
  "!**/node_modules/.bin"
]
```

主监控异常上报

```javascript
process.on('uncaughtException', function() {
  //do somethings
});

process.crash(); //模拟崩溃
```
