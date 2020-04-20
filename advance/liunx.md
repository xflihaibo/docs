# linux

<div align="center">
  <img src="./advance/img/liunx.jpg" width="150" alt="logo" align="center">
</div>

Linux：是一种自由和开放源码的类 UNIX 操作系统。该操作系统的内核由林纳斯·托瓦兹在 1991 年 10 月 5 日首次发布，在加上用户空间的应用程序之后，成为 Linux 操作系统

## liunx 常用命令

1.  netstat -ntpl 查看进程
1.  ss –an –p | grep 8080 查看进程
1.  lsof -i:80 查看进程
1.  cat /etc/passwd 查看用户列表
1.  kill -9 pid 强制杀死进程
1.  killall nginx 杀死 nginx 所有的进程
1.  nginx –t 查看是否生效
1.  nginx -s reload: 重新启动
1.  ssh 启动 sudo service ssh start
1.  tar -cvf vitest.zip vitest 压缩
1.  tar -xvf vitest.zip 解压缩
1.  systemctl start firewalld 开启防火墙
1.  systemctl stop firewalld 关闭防火墙
1.  systemctl status firewalld 查看防火墙状态
1.  firewall-cmd –list-all 查看所有的信息
1.  Chmod 600 ubuntu02_key 修改私钥权限
1.  ps -ef | grep nginx 查看 nginx 的进程
1.  sudo passwd 设置 root 用户密码
1.  su root 切换用户
1.  /etc/profile //环境变量配置文件
1.  ssh root@192.168.50.14 -P 8090
1.  复制文件：scp width.html roottest@192.168.50.141:home/newtest
1.  复制目录：scp -r filename roottest@192.168.50.141:home/newtest
1.  ssh roottest@192.168.50.141
1.  service jenkins restart 启动 jenkins 进程
1.  service nginx restar 启动 nginx 进程
1.  yum uninstall nginx 卸载
1.  curl 127.0.0.1; 访问网络
1.  Exit：退出
1.  hostname hb 更改主机用户名
1.  where is nginx 查找文件位置
1.  which nginx (别名)查找文件位置
1.  find /etc -name init.d 查找文件
1.  find /etc -name init.\* (多个)查找文件
1.  find /etc -name init.? （一个）查找文件
1.  find /etc -iname init.T 忽略大小写
1.  find /etc -atime 5 //文件访问时间
1.  find /etc -ctime 5 //改变文件属性
1.  find /etc -mtime 5 //修改时间
1.  find /etc -size -100k //文件小于 100k 的
1.  find /etc -size +100k //文件大于 100k 的
1.  find /etc -size 100k //文件等于 100k 的
1.  main ls 查看帮助

### 配置免密登录

-   注如果 scp ssh 失败：
-   sudo ps -e |grep ssh“–>回车–>有 sshd,说明 ssh 服务已经启动，如果没有启动，输入”sudo service ssh start“–>回车–>ssh 服务就会启动 如果没有下载 apt-get install openssh-server 并且

*   ssh-keygen –t rsa –C ‘name’ -f 'wenjianming_key’
    > -   -t 选择加密算法
    > -   -C 名字
    > -   -f 生成密钥名字
    > -   rsa 加密方式
    > -   wenjianming_key.pub >> authorized_keys //把公钥追加 authorized_keys
    > -   > 覆盖
    > -   > > 追加
    > -   Exit：退出
*   ssh 登录：ssh -i pri-key root@192.168.50.134

### 拷贝公钥

```shell
ssh-copy-id <ip地址>
```

```bash
    known_hosts: 存放其他服务器生成的指纹
    config 配置
            Host evil-cloud
            User root
            Host yideng
            HostName 192.168.50.142
            port 22
            IdentityFile ~/.ssh/new
            IdentitiesOnly yes
            Protocol 2
            Compression yes
            ServerAliveInterval 60
            ServerAliveCountMax 20
            LogLevel INFO
    ssh yideng  可直接登录
```

## 文件夹作用

```shell
/bin: /usr/bin: 可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等。
/boot：放置linux系统启动时用到的一些文件。/boot/vmlinuz 为 linux 的内核文件，以及 /boot/gurb。建议单独分区，分区大小100M即可
/dev：存放linux系统下的设备文件，访问该目录下某个文件，相当于访问某个设备，常用的是挂载光驱 mount /dev/cdrom /mnt。
/etc：系统配置文件存放的目录，不建议在此目录下存放可执行文件，重要的配置文件有 /etc/inittab、/etc/fstab、/etc/init.d、/etc/X11、/etc/sysconfig、/etc/xinetd.d修改配置文件之前记得备份。
注：/etc/X11 存放与 x windows 有关的设置。
/home：系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下，~表示当前用户的家目录，~edu 表示用户 edu 的家目录。建议单独分区，并设置较大的磁盘空间，方便用户存放数据
/lib: /usr/lib: /usr/local/lib：系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助，比较重要的目录为 /lib/modules。
/lost+fount：系统异常产生错误时，会将一些遗失的片段放置于此目录下，通常这个目录会自动出现在装置目录下。如加载硬盘于 /disk 中，此目录下就会自动产生目录 /disk/lost+found
/mnt: /media：光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，也不一定，可以选择任意位置进行挂载。
/opt：给主机额外安装软件所摆放的目录。如：FC4使用的Fedora 社群开发软件，如果想要自行安装新的 KDE 桌面软件，可以将该软件安装在该目录下。以前的 Linux 系统中，习惯放置在 /usr/local 目录下
/proc：此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的目录有 /proc/cpuinfo、/proc/interrupts、/proc/dma、/proc/ioports、/proc/net/* 等。
/root：系统管理员root的家目录，系统第一个启动的分区为 /，所以最好将 /root和 /放置在一个分区下。
/sbin: /usr/sbin: /usr/local/sbin：放置系统管理员使用的可执行命令，如fdisk、shutdown、mount 等。与 /bin 不同的是，这几个目录是给系统管理员 root使用的命令，一般用户只能"查看"而不能设置和使用。
/tmp：一般用户或正在执行的程序临时存放文件的目录,任何人都可以访问,重要数据不可放置在此目录下
/srv：服务启动之后需要访问的数据目录，如 www 服务需要访问的网页数据存放在 /srv/www 内。
/usr：应用程序存放目录，/usr/bin 存放应用程序，/usr/share 存放共享数据，/usr/lib 存放不能直接运行的，却是许多程序运行所必需的一些函数库文件。/usr/local: 存放软件升级包。/usr/share/doc: 系统说明文件存放目录。/usr/share/man: 程序说明文件存放目录，使用 man ls 时会查询 /usr/share/man/man1/ls.1.gz 的内容建议单独分区，设置较大的磁盘空间
/var：放置系统执行过程中经常变化的文件，如随时更改的日志文件 /var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下。建议单独分区，设置较大的磁盘空间
```

## 权限问题

ls -a 查看文件
chmod -R u+x tiral 给文件赋予所有者的执行权限
chmod -R u-x tiral 给文件减去所有者的执行权限
chmod -R u=rwx tiral 给文件赋予所有者的读写执行权限
chmod 755 trial

chown user1 trial 给文件赋予所有者的 fuzhi
chgrp user1 trial

权限试用者

1.  u:所有者
2.  g:所有组
3.  o:其他人

    权限

r:读 4。（cat more head tail）

5.  w:写 2. echo vi
6.  x:执行 1

<!-- > useradd user1
> pasword user1 -->

## shell 命令

![](./img/shell.png)

1.  /bin/bash -x first_shell.sh //执行 shell 文件 调试错误
2.  /bin/bnsh -n first_shell.sh //执行 shell 文件 调试错误

### shell 编程常见的系统变量解析

1.  \$0   当前程序的名称
2.  \$n   当前程序的第 n 个参数,n=1,2,3,...9
3.  \$\*   当前程序的所有参数 ( 不包括程序本身 )
4.  \$#   当前程序的参数个数 ( 不包括程序本身 )
5.  \$?   命令或程序执行完后的状态，一般返回 0 表示执行成功。
6.  \$UID   当前用户的 ID
7.  \$PWD 当前所在的目录

```shell
Var="1234"
readonly Var //使用 readonly 命令可以将变量定义为只读变量
unset Var  //使用 unset 命令可以删除变量
echo ${#Var}  #获取字符串长度 输出 4
echo ${Var:2:3} # 输出34 //提取子字符串

nameone=(1 2 3 4);
${array_name[n]} //数组元素值的一般格式
${array_name[@]} //获取数组中的所有元素
length=${#array_name[@]} //取得数组元素的个数
length=${#array_name[*]} // 或者
lengthn=${#array_name[n]}// 取得数组单个元素的长度
```

### 注释

1.  以 # 开头的行就是注释，会被解释器忽略
2.  多行注释

```shell
:<<EOF
注释内容...
EOF

:<<'
注释内容...
'
```

#### 创建目录

```shell
#!/bin/bash
DIR=$1
echo -e '\033 [32m-------------------\033[0m'




if ( ! -d $DIR ); then
    mkdir -p $DIR
    echo "the $DIR create success!!"
else
    echo "the $DIR is exist"
    exit
fi
```

#### 创建文件

```shell
#!/bin/bash
FILE=$1

if [ ! -f $FILE ]; then
    touch $FILE
    echo "the $FILE create success!!"
else
    echo "the $FILE is exist"
    exit
fi
```

## 算术运算符

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

```shell
+   加法  `expr $a + $b` 结果为 30。
-   减法  `expr $a - $b` 结果为 -10。
*   乘法  `expr $a \* $b` 结果为  200。
/   除法  `expr $b / $a` 结果为 2。
%   取余  `expr $b % $a` 结果为 0。
=   赋值  a=$b 将把变量 b 的值赋给 a。
==  相等。用于比较两个数字，相同则返回 true。 [ $a == $b ] 返回 false。
!=  不相等。用于比较两个数字，不相同则返回 true。

-eq 检测两个数是否相等，相等返回 true。    [ $a -eq $b ] 返回 false。
-ne 检测两个数是否不相等，不相等返回 true。  [ $a -ne $b ] 返回 true。
-gt 检测左边的数是否大于右边的，如果是，则返回 true。 [ $a -gt $b ] 返回 false。
-lt 检测左边的数是否小于右边的，如果是，则返回 true。 [ $a -lt $b ] 返回 true。
-ge 检测左边的数是否大于等于右边的，如果是，则返回 true。   [ $a -ge $b ] 返回 false。
-le 检测左边的数是否小于等于右边的，如果是，则返回 true。   [ $a -le $b ] 返回 true。

!   非运算，表达式为 true 则返回 false，否则返回 true。  [ ! false ] 返回 true。
-o  或运算，有一个表达式为 true 则返回 true。  [ $a -lt 20 -o $b -gt 100 ] 返回 true。
-a  与运算，两个表达式都为 true 才返回 true。  [ $a -lt 20 -a $b -gt 100 ] 返回 false。
&&  逻辑的 AND [[ $a -lt 100 && $b -gt 100 ]] 返回 false
||  逻辑的 OR  [[ $a -lt 100 || $b -gt 100 ]] 返回 true
```

## 文件测试运算符

```shell
=   检测两个字符串是否相等，相等返回 true。  [ $a = $b ] 返回 false。
!=  检测两个字符串是否相等，不相等返回 true。 [ $a != $b ] 返回 true。
-z  检测字符串长度是否为0，为0返回 true。  [ -z $a ] 返回 false。
-n  检测字符串长度是否为0，不为0返回 true。 [ -n "$a" ] 返回 true。
$   检测字符串是否为空，不为空返回 true。   [ $a ] 返回 true。
-b file 检测文件是否是块设备文件，如果是，则返回 true。  [ -b $file ] 返回 false。
-c file 检测文件是否是字符设备文件，如果是，则返回 true。 [ -c $file ] 返回 false。
-d file 检测文件是否是目录，如果是，则返回 true。 [ -d $file ] 返回 false。
-f file 检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。    [ -f $file ] 返回 true。
-g file 检测文件是否设置了 SGID 位，如果是，则返回 true。  [ -g $file ] 返回 false。
-k file 检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。  [ -k $file ] 返回 false。
-p file 检测文件是否是有名管道，如果是，则返回 true。   [ -p $file ] 返回 false。
-u file 检测文件是否设置了 SUID 位，如果是，则返回 true。  [ -u $file ] 返回 false。
-r file 检测文件是否可读，如果是，则返回 true。  [ -r $file ] 返回 true。
-w file 检测文件是否可写，如果是，则返回 true。  [ -w $file ] 返回 true。
-x file 检测文件是否可执行，如果是，则返回 true。 [ -x $file ] 返回 true。
-s file 检测文件是否为空（文件大小是否大于0），不为空返回 true。 [ -s $file ] 返回 true。
-e file 检测文件（包括目录）是否存在，如果是，则返回 true。    [ -e $file ] 返回 true。
```

## Shell 函数

```shell
#!/bin/bash

demoFun(){
    echo "这是我的第一个 shell 函数!"
}
echo "-----函数开始执行-----"
demoFun
echo "-----函数执行完毕-----"
funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"
```
