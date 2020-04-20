# homebrew

## 安装方式

```shell
/usr/bin/ruby -e "\$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" //安装
/usr/bin/ruby -e "\$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)" //卸载
```

## 修改权限 root

```javascript
# 查看所属用户：
ls -al `which brew`
# 改变用户：
sudo chown root:wheel `which brew`
```

### 添加第三方仓库

brew install git 安装 git
brew reinstall git: 重新覆盖安装包
brew uninstall git 卸载 git
brew search git: 搜索 git
brew list :列出已安装的软件
brew update :更新 brew
brew home :用浏览器打开 brew 的官方网站
brew info git: 显示软件信息
brew deps 显示包依赖
brew upgarde 更新所有
brew upgarde git: 更新指定包
brew cleanup :清理不需要的版本极其安装包缓存
brew cleanup git: 清理指定包的旧版本
brew cleanup -n 查看可清理的旧版本包，不执行实际操作
brew doctor: 检查有没有问题
