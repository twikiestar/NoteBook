XAMPP 服务器端配置



2017年6月30日

18:41



xampp配置



 XAMPP 的安装过程仅 4 个步骤



 步骤 1：下载



XAMPP 的 Linux 版 1.7.4, 2011年 1月 26日



tar xvfz xampp-linux-devel-1.7.4.tar.gz -C /opt 



 步骤 2：安装



将下载的压缩文件释放到 /opt：



tar xvfz xampp-linux-1.7.4.tar.gz -C /opt



XAMPP 被安装在 /opt/lampp 目录下。



 步骤 3：开始运行



使用下面的命令开始运行 XAMPP：



/opt/lampp/lampp start



高级的启动与停止参数



参数 描述



start 启动 XAMPP。



stop 停止 XAMPP。



restart 重新启动 XAMPP。



startapache 只启动 Apache。



startssl 启动 Apache 的 SSL 支持。该命令将持续激活 SSL 支持，例如：执行该命令后，如果您关闭并重新启动 XAMPP，SSL 仍将处于激活状态。



startmysql 只启动 MySQL 数据库。



startftp 启动 ProFTPD 服务器。通过 FTP，您可以上传文件到您的网络服务器中（用户名“nobody”，密码“lampp”）。该命令将持续激活 ProFTPD，例如：执行该命令后，如果您关闭并重新启动 XAMPP，FTP 仍将处于激活状态。



stopapache 停止 Apache。



stopssl 停止 Apache 的 SSL 支持。该命令将持续停止 SSL 支持，例如：执行该命令后，如果您关闭并重新启动 XAMPP，SSL 仍将处于停止状态。



stopmysql 停止 MySQL 数据库。



stopftp 停止 ProFTPD 服务器。该命令将持续停止 ProFTPD，例如：执行该命令后，如果您关闭并重新启动 XAMPP，FTP 仍将处于停止状态。



security 启动一个小型安全检查程序。



例如：想启用带 SSL 支持的 Apache，只需输入如下命令（以 root 身份）：



/opt/lampp/lampp startssl



现在您可以通过 SSL 形式的 https://localhost 访问 Apache 服务器了。



重要的文件和目录



文件/目录 用途



/opt/lampp/bin/ XAMPP 命令库。例如 /opt/lampp/bin/mysql 可执行 MySQL 监视器。



/opt/lampp/htdocs/ Apache 文档根目录。



/opt/lampp/etc/httpd.conf Apache 配制文件。



/opt/lampp/etc/my.cnf MySQL 配制文件。



/opt/lampp/etc/php.ini PHP 配制文件。



/opt/lampp/etc/proftpd.conf ProFTPD 配制文件。（从 0.9.5 版开始）



/opt/lampp/phpmyadmin/config.inc.php phpMyAdmin 配制文件。



想停止 XAMPP，只需输入如下命令：



/opt/lampp/lampp stop



想卸载 XAMPP，只需输入如下命令：



rm -rf /opt/lampp



ln -s /opt/lampp/lampp S99lampp // 自动启动XAMPP



ln -s /opt/lampp/lampp K01lampp // 停止自动启动



如果你想分步启动，可以输入命令：vi /etc/rc.d/rc.local



/opt/lampp/lampp startapcahe



/opt/lampp/lampp startmysql



/opt/lampp/lampp startssl



/opt/lampp/lampp startproftpd



/opt/lampp/lampp start 表示全部启动



7. 如何允许或者禁止root通过SSH登陆\(Fun-FreeBSD\)？



修改sshd\_config配置文件，更改其中的条目PermitRootLogin no&line;yes 就可以了。



\(不知道在那里修改\)



8、 xampp 更新



    下载更新包后解压，终端机中输入：xampp-upgrade/start



--------------------------------------------------------------------------------



附注：



程序在那里？



在典型的Unix系统里并没有所谓的系统设定或管理接口，而仅有所谓的设定档案，下表是包含在XAMPP中的相关软件设定档案概要。



重要档案和目录



/opt/lampp/bin/



XAMPP指令的家目录。例如 /opt/lampp/bin/mysql 用来执行MySQL。      命令行



/opt/lampp/htdocs/



Apache 文件根目录。



/opt/lampp/etc/httpd.conf



Apache设定档案。



/opt/lampp/etc/my.cnf



MySQL设定档案。



/opt/lampp/etc/php.ini



PHP设定档案。



/opt/lampp/etc/proftpd.conf



ProFTPD设定档案。\(从 0.9.5版后才有\)



/opt/lampp/phpmyadmin/config.inc.php



phpMyAdmin设定档案。



备份



做为系统安全保障的一部分，及时、全面的备份是一项必不可少的工作。数据库以及各软件的配置文件、日志等，经常会使管理员晕头转向，一不小心就会漏掉一项。而XAMPP则让这一工作变得非常简单，输入下面的命令就可一步完成：



/opt/lampp/lampp backup \*\*\*\*



命令后面跟着的是MySQL 的 root 用户的密码。命令执行后会看到下面的内容：



Backing up databases...



Backing up configuration, log and htdocs files...



Calculating checksums...



Building final backup file...



Backup finished.



Take care of /opt/lampp/backup/xampp-backup-19-02-06.sh



恢复



恢复以前的备份，只需以 root 用户身份运行下面的命令：



\# sh /opt/lampp/backup/xampp-backup-19-02-06.sh \*\*\*\*



命令后面跟着的是MySQL 的 root 用户的密码，这时用户将看到如下信息：



Checking integrity of files...



Restoring configuration, log and htdocs files...



Checking versions...



Installed: XAMPP 1.5.1



Backup from: XAMPP 1.5.1



Restoring MySQL databases...



Restoring MySQL user databases...



Backup complete. Have fun!



You may need to restart XAMPP to complete the restore.



恢复完后，需要重新启动XAMPP，才能使恢复的数据可用。



图形化管理



gksu /opt/lampp/share/xampp-control-panel/xampp-control-panel



修改权限



sudo chmod -R 777 /home/htdocs



映射



添加alias，默认的网站目录是/opt/lampp/htdocs，需要sudo权限，不是很方便，我自己重新选择一个目录，然后sudo gedit /opt/lampp/etc/httpd.conf 修改，查找字符串 /opt/lampp/htdocs，替换2处，然后在最后添加Alias /xampp /opt/lampp/htdocs/xampp，这样访问localhost/xampp就能访问xampp的面板了



错误日志？？？



tail /opt/lampp/log/error\_log



sudo chmod －R a＋rw /opt/lampp/htdocs



MySQL 管理员（root）没有密码。



MySQL 可通过网络访问。



ProFTPD 使用“lampp”作为用户名“nobody”的密码。



PhpMyAdmin 可以通过网络访问。



示例程序可以通过网络访问。



MySQL 和 Apache 在同一个用户名（nobody）下运行。



/opt/lampp/lampp security



小记：添加映射到 /home/xing/。。。   总是失败access forbiden 看来是个人文件夹受保护，或者又是哪个权限问题！！！ 



