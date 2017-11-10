如何在linux下安装Yii框架



2017年9月29日

13:23





1.获取Composer

https://laravel-china.org/composer

在laravel中国社区获取composer

以及更改composer的中国镜像可以大幅度加快下载框架的速度

			安装 Composer\#

			注意：composer不能在root下使用，如果安装框架，要提前把创建的文件夹改成777权限并且把文件属主改成执行composer下的用户

			Linux/Mac：\#

			wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer

			chmod a+x /usr/local/bin/composer



			&lt;--------------------------下面是关于安装composer的选项----------------------------&gt;

			如遇权限不足，可添加 sudo。

			使用 Composer 镜像加速有两种选项：

    选项一：全局配置，这样所有项目都能惠及（推荐）；

    选项二：单独项目配置；

选项一、全局配置（推荐）

$ composer config -g repo.packagist composer https://packagist.laravel-china.org

选项二、单独使用

如果仅限当前工程使用镜像，去掉 -g 即可，如下：

$ composer config repo.packagist composer https://packagist.laravel-china.org

取消镜像

composer config -g --unset repos.packagist

遇到问题？\#

composer 命令后面加上 -vvv （是3个v）可以打印出调错信息，命令如下：

$ composer -vvv create-project laravel/laravel blog

$ composer -vvv require psr/log

如果自己解决不了，或发现 BUG，可以在 @扣丁禅师 的 GitHub 上 创建 Issue。

注意提问时请带上 -vvv 的输出，并且要求叙述清晰，第一次提问的同学请阅读 关于提问的智慧。

常见问题\#

    已存在 composer.lock 文件，先删除，再运行 composer install 重新生成。

        原因：composer.lock 缓存了之前的配置信息，从而导致新的镜像配置无效。

    使用 laravel new 命令创建工程， 这个命令会从 这里 下一个zip包，里面自带了 composer.lock，和上面原因一样，也无法使用镜像加速，解决方法：

        方法一（推荐）：

        不使用 laravel new，直接用 composer create-project laravel/laravel xxx 新建工程。

        方法二：

        运行 laravel new xxx，当看见屏幕出现 - Installing doctrine/inflector 时，Ctrl + C 终止命令，cd xxx 进入，删除 composer.lock，再运行 composer install。

注：在laravel社区下载的composer 如果完全根据代码执行 composer.phar 文件会存在/usr/local/bin/下一个叫做composer不带后缀的文件就是composer.phar

 在执行代码的时候：

 	php composer.phar global require "fxp/composer-asset-plugin:^1.2.0"

 	要改成绝对路径才能使用\(文件名保持一致性\)：

 	 	php /usr/local/bin/composer global require "fxp/composer-asset-plugin:^1.2.0"

			&lt;--------------------------上面是关于安装composer 可能会出现的问题----------------------------&gt;



安装完Composer，运行下面的命令来安装Composer Asset插件:



php /usr/local/bin/composer global require "fxp/composer-asset-plugin:^1.2.0"



现在选择的应用程序模板之一，开始安装 Yii 2.0。应用程序模板是一个包含Yii写的骨架Web应用程序包。



    安装基本的应用程序模板，运行下面的命令：



    php /usr/local/bin/composer create-project yiisoft/yii2-app-basic basic 2.0.12



    安装高级的应用程序模板，运行下面的命令：



    php /usr/local/bin/composer create-project yiisoft/yii2-app-advanced advanced 2.0.12



请注意，您可能会被提示安装过程中输入你的 GitHub 的用户名和密码。这是正常的。只要输入它们并继续。

&lt;---------------------------------------以下是安装yii2框架的注意事项--------------------------------&gt;

出现Could not fetch https://api.github.com/repos/RobinHerbots/Inputmask/contents/bower.json?ref=4.x, please create a GitHub OAuth token to go over the API rate limit

Head to https://github.com/settings/tokens/new?scopes=repo&description=Composer+on+localhost.localdomain+2017-09-15+1141

to retrieve a token. It will be stored in "/home/composer/.composer/auth.json" for future use by Composer.

请去github网站获取token然后输入保存token继续安装



