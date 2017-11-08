# [redis的三种启动方式](http://www.cnblogs.com/pqchao/p/6549510.html)

redis的启动方式  
1.直接启动  
  进入redis根目录，执行命令:  
  \#加上‘&’号使redis以后台程序方式运行

| `./redis-server&` |
| :--- |


 2.通过指定配置文件启动  
  可以为redis服务启动指定配置文件，例如配置为/etc/redis/6379.conf  
  进入redis根目录，输入命令：

`./redis-server/etc/redis/6379.conf`

  \#如果更改了端口，使用\`redis-cli\`客户端连接时，也需要指定端口，例如：

redis-cli -p 6380

3.使用redis启动脚本设置开机自启动  
  启动脚本 redis\_init\_script 位于位于Redis的 /utils/ 目录下，redis\_init\_script脚本代码如下：

`#!/bin/sh`

`#`

`# Simple Redis init.d script conceived to work on Linux systems`

`# as it does use of the /proc filesystem.`

`#redis服务器监听的端口`

`REDISPORT=6379`

`#服务端所处位置`

`EXEC=/usr/local/bin/redis-server`

`#客户端位置`

`CLIEXEC=/usr/local/bin/redis-cli`

`#redis的PID文件位置，需要修改`

`PIDFILE=/var/run/redis_${REDISPORT}.pid`

`#redis的配置文件位置，需将${REDISPORT}修改为文件名`

`CONF="/etc/redis/${REDISPORT}.conf"`

`case"$1"in`

`start)`

`if[ -f $PIDFILE ]`

`then`

`echo"$PIDFILE exists, process is already running or crashed"`

`else`

`echo"Starting Redis server..."`

`$EXEC $CONF`

`fi`

`;;`

`stop)`

`if[ ! -f $PIDFILE ]`

`then`

`echo"$PIDFILE does not exist, process is not running"`

`else`

`PID=$(cat $ PIDFILE)`

`echo "Stopping ..."`

`$CLIEXEC -p $REDISPORT`

`shutdown`

`while [ -x /proc/${PID} ]`

`do`

`echo "Waiting for Redis to shutdown ..."`

`sleep 1`

`done`

`echo "Redis stopped"`

`fi`

`;;`

`*)`

`echo "Please use start or stop as first argument"`

`;;`

`esac`

 根据启动脚本，将修改好的配置文件复制到指定目录下，用root用户进行操作：

`mkdir /etc/redis`

`cp redis.conf/etc/redis/6379.conf`

 将启动脚本复制到/etc/init.d目录下，本例将启动脚本命名为redisd（通常都以d结尾表示是后台自启动服务）。

`cp redis_init_script/etc/init.d/redisd`

设置为开机自启动，直接配置开启自启动 chkconfig redisd on 发现错误： service redisd does not support chkconfig

解决办法，在启动脚本开头添加如下注释来修改运行级别：

\#!/bin/sh

\# chkconfig:   2345 90 10



 再设置即可

\#设置为开机自启动服务器

chkconfig redisd on

\#打开服务

service redisd start  
\#关闭服务

service redisd stop

