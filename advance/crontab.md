# crontab

Linux 定时任务 Crontab crond 是 linux 下用来周期性的执行某种任务或等待处理某些事件的一个守护进程，与 windows 下的计划任务类似，当安装完成操作系统后，默认会安装此服务 工具，并且会自动启动 crond 进程，crond 进程每分钟会定期检查是否有要执行的任务，如果有要执行的任务，则自动执行该任务。

## at 一次执行定时命令

chkconfig --list | grep atd at 服务是否安装
service atd restar 启动服务
service atd status 查看状态

### at 访问控制

1. 如果系统中有 /etc/at.allow 文件，那么只有写入/etc/at.allow 文件（白名单）中的用户可以使用 at 命令， /etc/at.deny 文件会被忽略
2. 如果系统中没有/etc/at.allow 文件，只有/etc/at.deny 文件，那么写入/etc/at.deny 文件（黑名单）中的用户不能使用 at 命令 root 除外
3. 如果系统中两个文件都不存在，那么只有 root 用户可以使用 at 命令

### at 格式

at -m : 当 at 工作完成后，无论是否命令输出，都用 email 通知执行 at 命令的用户
at -c : 工作号，显示 at 工作的内容

atq :查询 已经有的命令

时间

-   HH：MM 02:30
    HH:MM YYYY-MM-DD 02:30 9012-12-23
    HH:MM [am|pm][month][date] 02:30 july 24
    HH:MM [am|pm]+[minuter| hours|days|weeks] now+5 minutes

## crontab 循环执行定时命令

chkconfig --list | grep cron crontab 服务是否安装
service crond restar 启动服务
service crond status 查看状态
chkconfig crond on

### crontab 访问控制

1. 如果系统中有 /etc/cron.allow 文件，那么只有写入/etc/cron.allow 文件（白名单）中的用户可以使用 cron 命令， /etc/cron.deny 文件会被忽略
2. 如果系统中没有/etc/cron.allow 文件，只有/etc/cron.deny 文件，那么写入/etc/cron.deny 文件（黑名单）中的用户不能使用 cron 命令 root 除外
3. 如果系统中两个文件都不存在，那么只有 root 用户可以使用 cron 命令

## crontab 格式

{minute} {hour} {day-of-month} {month} {day-of-week} {full-path-to-shell-script}

1.  minute: 区间为 0 – 59
1.  hour: 区间为 0 – 23
1.  day-of-month: 区间为 0 – 31
1.  month: 区间为 1 – 12. 1 是 1 月. 12 是 12 月.
1.  Day-of-week: 区间为 0 – 7. 周日可以是 0 或 7.

```shell
yum clean call. //  清空缓存
yum update // 拉去最新版本信息
yum install -y cronie crontabs  //下载
yum list cronie && systemctl status crond 检查安装是否完毕及启动
yum list crontabs && which crontab && crontab -l 检查crontab 工具是否安装

crontab -e //编辑任务
systemctl restart cront。//重启任务
crontab -l  //查看任务列表
crontab -r //删除任务列表
cat /var/spool/cron/root
var/log/cron 日志列表

etc/crontab 系统配置文件

PATH =/sbin:/bin:/usr/sbin:/usr/bin    //环境变量
```

|    项目    |         含义         |         范围          |
| :--------: | :------------------: | :-------------------: |
| 第一个“\*” | 一小时当中的第几分钟 |         0-59          |
| 第二个“\*” |   一天中的第几小时   |         0-23          |
| 第三个“\*” |   一个月中的第几天   |         0-31          |
| 第四个“\*” |    一年中的第几月    |         1-12          |
| 第五个“\*” |    一周中的星期几    | 0-7 （0，7 代表周日） |

| 特殊符号 |                                       含义                                        |
| :------: | :-------------------------------------------------------------------------------: |
|    \*    |                代表任何时间，比如第一个 “\* “就代码每分钟都要执行                 |
|    ，    | 代表不联系时间 比如 0 8，12，16 \* \* \* 命令” 每天 8 点 12 点 16 点 执行一次命令 |
|    -     |      代表连续的范围 比如 0 5 \* \* \* 1-6 命令“ 周一到周六 5 点 0 分执行命令      |
|   \*/n   |           代表每隔多久执行一次 “\*/10 \* \* \* \*命令” 每隔 10 分钟执行           |

## 例如

```shell
* * * * * echo 'hello world' > $1  //每分钟
*/10 * * * * echo 'hello world' > $1 //每十分钟
* 7,8,9 * * * echo 'hello world' > $1  //7、8、9点执行
* 7-9 * * * echo 'hello world' > $1  //7、8、9点执行
```

1 6 个选项不能为空
2 脚本写绝对路径
3 天 和 星期 不能同时写
4 年 和秒 不能处理

## 系统的定时任务

etc/anacrontab 系统配置文件

anacron 系统关机错过定时任务 可以在系统开机之后在执行

检测周期
anacron 会使用 一天 七天 一个月 作为检测周期
在系统 /var/spool/anacron 目录存在 cron.{daily,weeekly,monthly}文件，用于记录 cron 的时间
和当前时间比较 如果两个时间差值超过了 anacron 的指定时间，证明 anacron 任务执行了
