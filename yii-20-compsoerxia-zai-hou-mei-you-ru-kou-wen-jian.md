2017年9月29日

13:22



yii2.0 解决一开始安装web/目录下没有入口index.php

如题：

对于一些刚使用Yii2的同学可能刚下载advanced 版 在frontend/web/ 下找不到index.php

解决：

在advanced目录下有个 init.bat 文件

双击运行，会出现一个dos窗口 输入 0（开发模式） 或 1（产品模式）

按回车

再输入 yes 回车

这样就能生成入口文件了.

