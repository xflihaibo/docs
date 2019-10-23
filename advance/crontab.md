# crontab

Linux 定时任务 Crontab crond 是 linux 下用来周期性的执行某种任务或等待处理某些事件的一个守护进程，与 windows 下的计划任务类似，当安装完成操作系统后，默认会安装此服务 工具，并且会自动启动 crond 进程，crond 进程每分钟会定期检查是否有要执行的任务，如果有要执行的任务，则自动执行该任务。

## 格式

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
cat /var/spool/cron/root
var/log/cron 日志列表

//etc/crontab
PATH =/sbin:/bin:/usr/sbin:/usr/bin    //环境变量
```

## 例如

```shell
* * * * * echo 'hello world' > $1  //每分钟
*/2 * * * * echo 'hello world' > $1 //每两分钟
* 7,8,9 * * * echo 'hello world' > $1  //7、8、9点执行
* 7-9 * * * echo 'hello world' > $1  //7、8、9点执行
```
