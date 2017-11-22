2017年9月29日

13:18



数据库编码正常在网页输出的时候出现乱码的解决办法

在&lt;?php下一行

输入

header\("Content-type:text/html;charset=utf-8"\);

解决

