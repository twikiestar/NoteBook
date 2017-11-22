2017年9月30日

13:47



PHP数据类型转换

PHP的数据类型转换属于强制转换，允许转换的PHP数据类型有：

•（int）、（integer）：转换成整形 

•（float）、（double）、（real）：转换成浮点型 

•（string）：转换成字符串 

•（bool）、（boolean）：转换成布尔类型 

•（array）：转换成数组 

•（object）：转换成对象 

PHP数据类型有三种转换方式：

•在要转换的变量之前加上用括号括起来的目标类型 

•使用3个具体类型的转换函数，intval\(\)、floatval\(\)、strval\(\) 

•使用通用类型转换函数settype\(mixed var,string type\) 

 第一种转换方式： \(int\)  \(bool\)  \(float\)  \(string\)  \(array\) \(object\)



1.&lt;?php    

2.$num1=3.14;    

3.$num2=\(int\)$num1;    

4.var\_dump\($num1\); //输出float\(3.14\)    

5.var\_dump\($num2\); //输出int\(3\)    

6.?&gt;   

第二种转换方式：  intval\(\)  floatval\(\)  strval\(\)



1.&lt;?php    

2.$str="123.9abc";    

3.$int=intval\($str\);     //转换后数值：123    

4.$float=floatval\($str\); //转换后数值：123.9    

5.$str=strval\($float\);   //转换后字符串："123.9"     

6.?&gt;   

第三种转换方式：  settype\(\);



1.&lt;?php    

2.$num4=12.8;    

3.$flg=settype\($num4,"int"\);    

4.var\_dump\($flg\);  //输出bool\(true\)    

5.var\_dump\($num4\); //输出int\(12\)    

6.?&gt; 

