

添加php.intl插件



2017年9月29日

13:20



给源码包安装的linux加载php intl模块

安装ICU模块

wget http://download.icu-project.org/files/icu4c/52.1/icu4c-52\_1-src.tgztar -xvf tar xf icu4c-52\_1-src.tgz  

cd icu/source/

./runConfigureICU Linux  

make

make install



给php添加intl服务

转到php7.0.7下源码包ext目录

cd /soft/php-7.0.7/ext/intl

/usr/local/php/bin/phpize

./configure --with-php-config=\[php安装路径\]+/php/bin/php-config  --enable-intl

make

make install

