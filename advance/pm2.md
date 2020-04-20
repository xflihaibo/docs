-V, --version output the version number
-v --version print pm2 version
-s --silent hide all messages
--ext <extensions> watch only this file extensions
-n --name <name> set a name for the process in the process list
-m --mini-list display a compacted list without formatting
--interpreter <interpreter> set a specific interpreter to use for executing app, default: node
--interpreter-args <arguments> set arguments to pass to the interpreter (alias of --node-args)
--node-args <node_args> space delimited arguments to pass to node
-o --output <path> specify log file for stdout
-e --error <path> specify log file for stderr
-l --log [path] specify log file which gathers both stdout and stderr
--log-type <type> specify log output style (raw by default, json optional)
--log-date-format <date format> add custom prefix timestamp to logs
--time enable time logging
--disable-logs disable all logs storage
--env <environment_name> specify which set of environment variables from ecosystem file must be injected
-a --update-env force an update of the environment with restart/reload (-a <=> apply)
-f --force force actions
-i --instances <number> launch [number] instances (for networked app)(load balanced)
--parallel <number> number of parallel actions (for restart/reload)
--shutdown-with-message shutdown an application with process.send('shutdown') instead of process.kill(pid, SIGINT)
-p --pid <pid> specify pid file
-k --kill-timeout <delay> delay before sending final SIGKILL signal to process
--listen-timeout <delay> listen timeout on application reload
--max-memory-restart <memory> Restart the app if an amount of memory is exceeded (in bytes)
--restart-delay <delay> specify a delay between restarts (in milliseconds)
--exp-backoff-restart-delay <delay> specify a delay between restarts (in milliseconds)
-x --execute-command execute a program using fork system
--max-restarts [count] only restart the script COUNT times
-u --user <username> define user when generating startup script
--uid <uid> run target script with <uid> rights
--gid <gid> run target script with <gid> rights
--namespace <ns> start application within specified namespace
--cwd <path> run target script as <username>
--hp <home path> define home path when generating startup script
--wait-ip override systemd script to wait for full internet connectivity to launch pm2
--service-name <name> define service name when generating startup script
-c --cron <cron_pattern> restart a running process based on a cron pattern
-w --write write configuration in local folder
--no-daemon run pm2 daemon in the foreground if it doesn't exist already
--source-map-support force source map support
--only <application-name> with json declaration, allow to only act on one application
--disable-source-map-support force source map support
--wait-ready ask pm2 to wait for ready event from your app
--merge-logs merge logs from different instances but keep error and out separated
--watch [paths] watch application folder for changes (default: )
--ignore-watch <folders|files> List of paths to ignore (name or regex)
--watch-delay <delay> specify a restart delay after changing files (--watch-delay 4 (in sec) or 4000ms)
--no-color skip colors
--no-vizion start an app without vizion feature (versioning control)
--no-autorestart start an app without automatic restart
--no-treekill Only kill the main process, not detached children
--no-pmx start an app without pmx
--no-automation start an app without pmx
--trace enable transaction tracing with km
--disable-trace disable transaction tracing with km
--attach attach logging after your start/restart/stop/reload
--v8 enable v8 data collecting
--event-loop-inspector enable event-loop-inspector dump in pmx
--deep-monitoring enable all monitoring tools (equivalent to --v8 --event-loop-inspector --trace)
-h, --help output usage information

Commands:

    start [options] [name|namespace|file|ecosystem|id...]    start and daemonize an app
    trigger <proc_name> <action_name> [params]               trigger process action
    deploy <file|environment>                                deploy your json
    startOrRestart <json>                                    start or restart JSON file
    startOrReload <json>                                     start or gracefully reload JSON file
    pid [app_name]                                           return pid of [app_name] or all
    create                                                   return pid of [app_name] or all
    startOrGracefulReload <json>                             start or gracefully reload JSON file
    stop [options] <id|name|namespace|all|json|stdin...>     stop a process
    restart [options] <id|name|namespace|all|json|stdin...>  restart a process
    scale <app_name> <number>                                scale up/down a process in cluster mode depending on total_number param
    profile:mem [time]                                       Sample PM2 heap memory
    profile:cpu [time]                                       Profile PM2 cpu
    reload <name|all>                                        reload processes (note that its for app using HTTP/HTTPS)
    id <name>                                                get process id by name
    inspect <name>                                           inspect a process
    delete|del <name|id|script|all|json|stdin...>            stop and delete a process from pm2 process list
    sendSignal <signal> <pm2_id|name>                        send a system signal to the target process
    ping                                                     ping pm2 daemon - if not up it will launch it
    updatePM2                                                update in-memory PM2 with local PM2
    update                                                   (alias) update in-memory PM2 with local PM2
    install|module:install [options] <module|git:/>          install or update a module and run it forever
    module:update <module|git:/>                             update a module and run it forever
    module:generate [app_name]                               Generate a sample module in current folder
    uninstall|module:uninstall <module>                      stop and uninstall a module
    package [target]                                         Check & Package TAR type module
    publish|module:publish [options] [folder]                Publish the module you are currently on
    set [key] [value]                                        sets the specified config <key> <value>
    multiset <value>                                         multiset eg "key1 val1 key2 val2
    get [key]                                                get value for <key>
    conf [key] [value]                                       get / set module config values
    config <key> [value]                                     get / set module config values
    unset <key>                                              clears the specified config <key>
    report                                                   give a full pm2 report for https://github.com/Unitech/pm2/issues
    link [options] [secret] [public] [name]                  link with the pm2 monitoring dashboard
    unlink                                                   unlink with the pm2 monitoring dashboard
    monitor [name]                                           monitor target process
    unmonitor [name]                                         unmonitor target process
    open                                                     open the pm2 monitoring dashboard
    plus|register [options] [command] [option]               enable pm2 plus
    login                                                    Login to pm2 plus
    logout                                                   Logout from pm2 plus
    dump|save [options]                                      dump all processes for resurrecting them later
    cleardump                                                Create empty dump file
    send <pm_id> <line>                                      send stdin to <pm_id>
    attach <pm_id> [comman]                                  attach stdin/stdout to application identified by <pm_id>
    resurrect                                                resurrect previously dumped processes
    unstartup [platform]                                     disable the pm2 startup hook
    startup [platform]                                       enable the pm2 startup hook
    logrotate                                                copy default logrotate configuration
    ecosystem|init [mode]                                    generate a process conf file. (mode = null or simple)
    reset <name|id|all>                                      reset counters for process
    describe <name|id>                                       describe all parameters of a process
    desc <name|id>                                           (alias) describe all parameters of a process
    info <name|id>                                           (alias) describe all parameters of a process
    show <name|id>                                           (alias) describe all parameters of a process
    env <id>                                                 list all environment variables of a process id
    list|ls                                                  list all processes
    l                                                        (alias) list all processes
    ps                                                       (alias) list all processes
    status                                                   (alias) list all processes
    jlist                                                    list all processes in JSON format
    sysmonit                                                 start system monitoring daemon
    slist|sysinfos [options]                                 list system infos in JSON
    prettylist                                               print json in a prettified JSON
    monit                                                    launch termcaps monitoring
    imonit                                                   launch legacy termcaps monitoring
    dashboard|dash                                           launch dashboard with monitoring and logs
    flush [api]                                              flush logs
    reloadLogs                                               reload all logs
    logs [options] [id|name]                                 stream logs file. Default stream all logs
    kill                                                     kill daemon
    pull <name> [commit_id]                                  updates repository for a given app
    forward <name>                                           updates repository to the next commit for a given app
    backward <name>                                          downgrades repository to the previous commit for a given app
    deepUpdate                                               performs a deep update of PM2
    serve|expose [options] [path] [port]                     serve a directory over http via port
    autoinstall
    examples                                                 display pm2 usage examples

### 常用命令

$ pm2 logs 显示所有进程日志
$ pm2 stop all 停止所有进程
$ pm2 restart all 重启所有进程
$ pm2 reload all 0 秒停机重载进程 (用于 NETWORKED 进程)
$ pm2 stop 0 停止指定的进程
$ pm2 restart 0 重启指定的进程
$ pm2 startup 产生 init 脚本 保持进程活着
$ pm2 web 运行健壮的 computer API endpoint (http://localhost:9615)
$ pm2 delete 0 杀死指定的进程
$ pm2 delete all 杀死全部进程
$ pm2 list 查看有哪些进程
$ pm2 descripe app_name | app_id 查看某个进程的信息
运行进程的不同方式：
$ pm2 start app.js -i max 根据有效 CPU 数目启动最大进程数目
$ pm2 start app.js -i 3 启动 3 个进程
$ pm2 start app.js -x 用 fork 模式启动 app.js 而不是使用 cluster
$ pm2 start app.js -x -- -a 23 用 fork 模式启动 app.js 并且传递参数 (-a 23)
$ pm2 start app.js --name serverone 启动一个进程并把它命名为 serverone
$ pm2 stop serverone 停止 serverone 进程
$ pm2 start app.json 启动进程, 在 app.json 里设置选项
$ pm2 start app.js -i max -- -a 23 在--之后给 app.js 传递参数
$ pm2 start app.js -i max -e err.log -o out.log 启动 并 生成一个配置文件
$ pm2 monit 查看当前通过 pm2 运行的进程的状态
\$ pm2 start app.js --max-memory-restart 100M 内存超过使用上限自动重启

### 配置文件

```shell
{
    "apps": {
        "name": "express_project",       // 项目名
        "script": "app.js",              // 执行文件
        "cwd": "./",                     // 根目录
        "args": "",                      // 传递给脚本的参数
        "interpreter": "",               // 指定的脚本解释器
        "interpreter_args": "",          // 传递给解释器的参数
        "watch": true,                   // 是否监听文件变动然后重启
        "ignore_watch": [                // 不用监听的文件
            "node_modules",
            "public"
        ],
        "exec_mode": "cluster_mode",     // 应用启动模式，支持 fork 和 cluster 模式
        "instances": "max",              // 应用启动实例个数，仅在 cluster 模式有效 默认为 fork
        "error_file": "./logs/app-err.log",         // 错误日志文件
        "out_file": "./logs/app-out.log",           // 正常日志文件
        "merge_logs": true,                         // 设置追加日志而不是新建日志
        "log_date_format": "YYYY-MM-DD HH:mm:ss",   // 指定日志文件的时间格式
        "min_uptime": "60s",                        // 应用运行少于时间被认为是异常启动
        "max_restarts": 30,                         // 最大异常重启次数
        "autorestart": true,                        // 默认为 true, 发生异常的情况下自动重启
        "restart_delay": "60"                       // 异常重启情况下，延时重启时间
        "env": {
           "NODE_ENV": "production",                // 环境参数，当前指定为生产环境
           "REMOTE_ADDR": ""
        },
        "env_dev": {
            "NODE_ENV": "development",              // 环境参数，当前指定为开发环境
            "REMOTE_ADDR": ""
        },
        "env_test": {                               // 环境参数，当前指定为测试环境
            "NODE_ENV": "test",
            "REMOTE_ADDR": ""
        }
    }
}

```
