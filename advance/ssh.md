# ssh

## 本机

第一步打开本地命令行，输入" ssh-keygen -t rsa -C 'test' -f 'test@email.com' " 一路回车生成密钥文件

![ssh](./img/ssh/13.jpeg)

找到当前用户下的 ”.ssh“ 隐藏文件

![ssh](./img/ssh/11.jpeg)

然后把 ”test@email.com“ 拷贝到 “.ssh”文件夹下

![ssh](./img/ssh/12.jpeg)

用 vim 打开 .ssh 文件夹下的 config 文件（如果没有文件就新建)

![ssh](./img/ssh/02.jpeg)

输入以下的信息 Host: 是你的远程服务器地址， IdentityFile ：是你的私钥文件地址

![ssh](./img/ssh/03.jpeg)

## scp 拷贝

使用”scp“ 把公钥拷贝到你指定的服务器上根目录下的“.ssh” 文件 至此本地配置结束 ✌️

![ssh](./img/ssh/05.jpeg)

## 远程服务器

第一次登录远程服务器 输入‘yes’，然后在输入密码即可
![ssh](./img/ssh/15.jpeg)

登录成功

![ssh](./img/ssh/14.jpeg)

找到根目录下的".ssh" 文件

![ssh](./img/ssh/08.jpeg)

把 公钥 使用“ >> ”追加到 “authorized_keys” 文件里（如果没有文件就新建)

![ssh](./img/ssh/04.jpeg)

## 成功

尝试 "ssh root@112.74.18.XXX" 发现不用输入密码㊙ ️ 就可以直接登录到远程服务器上，到此配置成功 ✌️

![ssh](./img/ssh/01.jpeg)
