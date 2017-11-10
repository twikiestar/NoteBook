# Redis 启动

1直接启动Redis 进入redis 根目录 执行

./Redis-server



2.通过指定配置文件启动

./redis-server  \[空格\] /etc/redisconf/xxx.conf  \[回车\]



\#如果更改了端口，使用redis-cli客户端连接的时候，也需要指定端口。

redis-cli -p 6666



使用redis启动脚本设置开机启动

* `#!/bin/sh`
* `#`
* `# Simple Redis init.d script conceived to work on Linux systems`
* `# as it does use of the /proc filesystem.`
* `#redis服务器监听的端口`
* `REDISPORT=6379`
* `#服务端所处位置`
* `EXEC=`
* `/usr/local/bin/redis-server`
* `#客户端位置`
* `CLIEXEC=`
* `/usr/local/bin/redis-cli`
* `#redis的PID文件位置，需要修改`
* `PIDFILE=`
* `/var/run/redis_`
* `${REDISPORT}.pid`
* `#redis的配置文件位置，需将${REDISPORT}修改为文件名`
* `CONF=`
* `"/etc/redis/${REDISPORT}.conf"`
* `case`
* `"$1"`
* `in`
* `start)`
* `if`
* `[ -f $PIDFILE ]`
* `then`
* `echo`
* `"$PIDFILE exists, process is already running or crashed"`
* `else`
* `echo`
* `"Starting Redis server..."`
* `$EXEC $CONF`
* `fi`
* `;;`
* `stop)`
* `if`
* `[ ! -f $PIDFILE ]`
* `then`
* `echo`
* `"$PIDFILE does not exist, process is not running"`
* `else`
* `PID=$(`
* `cat`
* `$PIDFILE)`
* `echo`
* `"Stopping ..."`
* `$CLIEXEC -p $REDISPORT`
* `shutdown`
* `while`
* `[ -x`
* `/proc/`
* `${PID} ]`
* `do`
* `echo`
* `"Waiting for Redis to shutdown ..."`
* `sleep`
* `1`
* `done`
* `echo`
* `"Redis stopped"`
* `fi`
* `;;`
* `*)`
* `echo`
* `"Please use start or stop as first argument"`
* `;;`

* `esac`

 根据启动脚本，将修改好的配置文件复制到指定目录下，用root用户进行操作：

`mkdir /etc/redis`

`cp redis.conf /etc/redis/6379.conf`

将启动脚本复制到/etc/init.d目录下，本例将启动脚本命名为redisd（通常都以d结尾表示是后台自启动服务）。

`cp redis_init_script /etc/init.d/redisd`

设置为开机自启动，直接配置开启自启动 chkconfig redisd on 发现错误： service redisd does not support chkconfig

解决办法，在启动脚本开头添加如下注释来修改运行级别：

`#!/bin/sh`

`# chkconfig:   2345 90 10`

 再设置即可

`#设置为开机自启动服务器`

`chkconfig redisd on`

`#打开服务`

`service redisd start`

`#关闭服务`

`service redisd stop`

