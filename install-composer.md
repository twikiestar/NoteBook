Linux下全局安装composer方法



2017年9月29日

13:13









//下载composer

curl -sS https://getcomposer.org/installer \| php

//将composer.phar文件移动到bin目录以便全局使用composer命令

mv composer.phar /usr/local/bin/composer

//切换国内源

composer config -g repo.packagist composer https://packagist.phpcomposer.com



使用国内镜像

composer config -g repo.packagist composer https://packagist.phpcomposer.com

安装 Composer\#

Linux/Mac：\#



wget https://dl.laravel-china.org/composer.phar -O /usr/local/bin/composer

chmod a+x /usr/local/bin/composer



如遇权限不足，可添加 sudo。

Windows：\#



    直接下载 composer.phar，地址：https://dl.laravel-china.org/composer.phar

    把下载的 composer.phar 放到 PHP 安装目录

    新建 composer.bat, 添加如下内容，并保存：



@php "%~dp0composer.phar" %\*



查看当前版本\#



$ composer -V



升级版本\#



$ composer selfupdate



    注意 selfupdate 升级命令会连接官方服务器，速度很慢。建议直接下载我们的 composer.phar 镜像，每天都会更新到最新。

