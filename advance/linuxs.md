whilinuxs.md

```shell
ls :罗列文件列表
    -a :显示所有文件，包括隐藏文件
    -l :显示详细信息
    -d :查看目录属性
    -h :人性化显示文件大小
    -i :显示incode

mkdir 创建文件
    -p: 递归创建文件

cd  切换目录
    cd ~  :进入当前用户的家目录
    cd .. :进入上一次目录
    cd -  :进入上次目录
cp 切换目录
     -r :复制目录
     -p :连带文件属性
     -d :如果源文件是连接文件 则复制链接属性
     -a :相当于 -pdr
mv


查询命令

locate 在后台数据库中按文件名搜索，搜索速度更快
    /var/lib/mlocate 存储文件名与数据库数据
    updatedb :更新创建的文件名存入数据库中
    /etc/updatedb.conf: 配置文件
        PRUNE_BIND_MOUNTS='yes' 开启搜索限制
        PRUNEFS=    搜索时，不搜索的文件系统
        PRUNENAMES=      搜索时，不搜索的文件类型
        PRINEPATHS=     搜索时，不搜索的文件路径

搜索

which
whereis 查询命令的配置文件
    -b :查找可执行的文件
    -m :只查找帮助文件

whoami
whatis ls
whatis cd 确定是否是shell内部命令


find /root -iname install.log 不区分大小写
find /root -name "*[cd]"
find /root -nouser 没有所有者文件， sys proc 没有属于正常。外来文件
find /var/log  -mtime +10 10天前
find /var/log  -mtime -10 10天内
find . -size 25k 查找文件大小是25K的文件
find . -size +25K 查找文件大小是大于25K的文件
find /etc -size +20k -a size -50k 查找etc/ 目录下 大于20k并且小于50k 的文件
find /etc -size +20k -a size -50k -exec ls lh {}\; 查找etc/ 目录下 大于20k并且小于50k 的文件,并显示详细信息

grep  在文件当中匹配符合条件的字符串
    -i 忽略大小写
    -v 排除指定字符串

man 帮助命令
man ls ls帮助信息
man  -f  相当 whatis
man  -k   相当 apropos
    man 的级别
    1: 查看命令帮助
    2: 查看可被内核调用的函数的帮助
    3: 查看函数和函数库的帮助
    4: 查看特殊文件的帮助
    5: 查看配置文件的帮助
    6: 查看游戏的帮助
    7: 查看其他杂项的帮助
    8: 查看系统管理员可用命令的帮助
    9: 查看和内核相关文件的帮助



apropos ls 含有ls关键字的帮助信息
ls --help 查看ls帮助信息
help cd 获取内部命令

info 帮助信息
    -回车 进入子帮助页面
    -u :进入上层页面
    -n :进入下一个帮助小节
    -p : 进入上一个帮助小节
    -q : 退出

压缩

    .zip 格式压缩
    zip  压缩文件名 源文件
    zip -r 压缩文件名 源目录
    uzip  解压文件名
    .gz 格式压缩
    gzip 源文件
    gzip -c 源文件 压缩文件
    gzip -r 目录
    gzip -d 解压文件
    gunzip 解压文件
     .bz2 格式压缩
    bzip2 源文件 压缩.bz2格式 不保留源文件
    bzip2 -k 源文件 压缩之后保留源文件
    bzip2 -d 解压文件
    bunzip2 解压文件
    .tar.bz2 格式

    tar  -jcv -f filename.tar.bz2 被压缩的文件或目录
    tar -jxv -f filename.tar.bz2 -C 欲解压到的目录

    .tar.gz
    tar -zcvf 压缩名 源文件 压缩
    tar -zxvf 压缩包名称    解压
    .tar 格式
    tar -cvf filename.tar xxx 打包
    tar -xvf filename.tar  解压x

解压包
tar -cvf 压缩
tar -xvf 解压
先打包后压缩





关机
shutdown -r now
shutdown -r 05:30 &
shutdown -c
halt
init 0
poweroff


reboot
init 6


w 用户名
命令输出
    USER:登陆的用户名
    TTY: 登陆终端
    FROM:ip地址登录
    LOGIN@:登陆时间
    IDLE:用户闲置时间
    JCPU:指的是和改终端连接的所有占用时间
    PCPU:当前进程所占用的时间
    WHAT:当前正在运行的命令
who 用户名称
    命令输出
    -:用户名
    -: 登陆终端
    -:ip登录时间
last
    last默认读取/var/log/wtmp文件数据
     命令输出
    -:用户名
    -:登陆终端
    -:登陆ip
    -:登录时间
    -:退出时间
lastlog
    lastlog默认读取/var/log/lastlog文件数据
     命令输出
    -:用户名
    -:登陆终端
    -:登陆ip
    -:最后一次登录时间
history 历史命令
    -c:清空历史命令
    -w:把缓存中的历史命令写入历史命令保存文件 ～/.bash_history

alias ls='ls --color=never' 添加别名
alias   查看别名
unalias 删除别名
    1. 第一顺位 用绝对路径或相对路径执行的命令
    2. 第二顺位 执行别名
    3. 第三顺位 执行bash的内部命令
    4. 第三顺位 按照$PATH环境变量定义的目录查找顺序找到的第一个命令

输出重定向

命令 >> 文件 2>&1 以追加的方式，把正确输出和错误的输出都保存到同一个文件中
命令 &>>文件 以追加的方式，把正确输出和错误的输出都保存到同一个文件中
命令 >>文件1 2>>文件2 ：把正确的追加到文件1中 把错误的追加到文件2中

wc 输入重定向
    -c 统计字节数
    -w 统计单词数
    -l 统计行数

```

### shell

```shell
\a 输出警告
\b 退格键 向左侧删除
\n 换行符
\r 回车键
\t tap键
\v 垂直制表符
\0nnn 八进制
\xhh  十六进制

```

```shell
echo -e "\e[1;31m hello world \e[0m"
echo -e "\e[1;32m hello world \e[0m"
echo -e "\e[1;33m hello world \e[0m"
echo -e "\e[1;34m hello world \e[0m"
echo -e "\e[1;35m hello world \e[0m"
echo -e "\e[1;36m hello world \e[0m"
echo -e "\e[1;37m hello world \e[0m"
echo -e "\e[1;30m hello world \e[0m"
```

```shell
30m 黑色
31m 红色
32m 绿色
33m 黄色
34m 蓝色
35m 洋红
36m 青色
37m 白色
```

## 脚本执行

方式一
chmod 755 hello.sh
./hello.sh
方式二
bash hello.sh

vim
ctrl+c

设置环境变量

export HD='hello Docker'

echo $PATH  查看系统环境变量
PATH = "$PATH":/root/sh 增加 PATH 变量的值
ps1 环境变量

locale 当前语言
-LANG 定义系统主语系变量
-LC_ALL 罗列支持的语言
echo \$LANG 当前语言
locale -a | more 罗列支持的语言
cat /etc/sysconfig/i18n

```shell
$n :问数字 ¥0代表命令把本身 $1-$9 代表第一到第九个参数
$_ :代表命令行中的所有参数，\$_ 把所有的参数看成一个整体
$@ :这个变量也代表命令行中所有参数，不过$@把每个参数区分中
\$# :这个变量代表命令行素所有的参数

‘’：单引号 在单引号中所有的特殊符号，如"\$" 和 "`" 都没有特殊含义 "": 双引号 在双引号中特殊符号都没有特殊含义 但是 "\$" 和 "`"和“\”例外 拥有 “调用变量的值”，“引用命令”，“转义符”的特殊含义
``: 反引号 在反引号扩起来的内容是系统命令，在 Bash 中会优先执行它，和$()作用一样，不过推荐用 $(),
$(): 和反引号一样，用来引用系统命令
#: 在shell脚本中，#开头的行代表注释
$: 用于调用变量的值，如需要调用 name 的值时，需要用$name的方式
\ : 转义符号 跟在\之后的特殊符号将失去特殊含义，变为普通自负 \$ 将输出 $ 符号 ，而不做变量引用


$? 最后一个命令的返回状态，如果这个变量的值为0，证明上一个命令的正确执行；如果这个变量的值为非0，则证明上一个命令的不正确了
$$ 当前进程号
$! 后台运行的进程号 pid


```

read 接收键盘输入
选项
-p 提示信息；在等待 read 输入时，输出提示信息
-t 秒数 read 命令会一直等待用户输入，使用此项可以指定等待时间
-n 字符数 read 命令只接受指定的字符数
-s 隐藏输入数据 使用密码

declare 声明变量类型
-:给变量设定类型属性
+:取消变量的类型属性
-a:将变量类型声明为数组型
-i:将变量类型声明为整数型
-x:将变量类型声明为环境变量
-r:将变量类型声明为制度变量
-p:显示指定变量的被声明的类型
declare -x test=123 和 export 作用相似，但其实是 declare 命令的作用
declare -i cc=$aa+$bb
dd=$(expr $aa + $bb) :注意‘+’号左右两侧必须有空格
dd=$(( $aa + $bb))
dd=$[ $aa + \$bb]
move[0]=zp
move[1]=tp
declare -a move[2]=live
echo move
echo move[2]
echo move[*]

###node

ls -al /usr/bin/node
sudo ln -s /usr/bin/nodejs /usr/bin/node

wget https://nodejs.org/dist/v9.8.0/node-v9.8.0-linux-x64.tar.xz
tar -xvf node-v9.8.0-linux-x64.tar
cd node-v9.8.0-linux-x64
ln -s /opt/nodejs/node-v9.8.0-linux-x64/bin/node /usr/local/bin/node
ln -s /opt/nodejs/node-v9.8.0-linux-x64/bin/npm /usr/local/bin/npm
