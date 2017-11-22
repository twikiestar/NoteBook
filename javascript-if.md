Javascript IF语句



2017年10月13日

10:02





If语句 - 只有当指定条件为True时使用if的语句体来执行代码

If..else,,语句 -当条件为True时执行第一段语句体,条件为false时执行第二段语句体

If..elseif..else.. 语句 - 使用该语句来选择多个代码块之一条件为True的语句 ,若没有符合条件都为false时执行else语句体中的内容

Switch 语句 - 使用该语句来选择多个代码块之一符合条件的来执行\(与if…elseif..else类似,但是条理更清晰,在代码中更容易理解\)











If 语句:

If\(条件\)

{

	语句体\(当if的条件为true时执行的代码\)

}

Tips:使用小写的if.使用大写的IF会生成Javascript错误,此语句中没有使用..else..说名只有在指定条件为true时才会触发语句体



If..else..语句:

If\(条件\)

{

	语句体1\(当if的条件为true时执行的代码\)

}else{

	语句体2\(当if的条件为false时执行的代码\)

}

	



If..elseif..else..语句:

If\(条件\)

{

	语句体1\(当if的条件为true时执行的代码\)

}elseif\(条件2\){

	语句体2\(当满足条件2时执行的代码\)

}else{

	语句体2\(当以上条件都为false时执行的代码\)

	

}



在Javascript中哪些值可以作为if的条件呢?

1.布尔变量true/false

2.数字非0,非NaN/\(0或NaN\)

3.对象非null/\(null或undefined\)

4.字符串非空串\(''\)/空串\(''\)



对于字符串不需要写一大堆if\(str != null && str != undefined && str !=''\)只需要一句

If\(!str\){

	//执行代码体

}

就可以了



对于数字的非空判断,则需要考虑使用isNaN\(\)函数,NaN不和任何类型的数据相等,包括他本身,只能使用isNaN\(\)函数进行判断.对于数字类型,if\(a\)语句中的a为0时if\(a\)为假,非0时if\(a\)为真



关于Javascript if语句的优化写法

一.使用常见的三元运算符

If\(foo\)bar\(\);else baz\(\); ==&gt;foo?bar\(\):baz\(\);

If\(!foo\)bar\(\);else baz\(\);==&gt;foo?baz\(\):bar\(\);

If\(foo\) return bar\(\);else return baz\(\); ==&gt;return foo\(\)?bar\(\):baz\(\);



例子:

&lt;script&gt;

	Var i=9;

	Var ii=\(i&gt;8\)?100:9;

	Alert\(ii\);

&lt;/script&gt;

输出结果为:

100



二.使用and\(&&\)和or\(\|\|\)运算符

If \(foo\) bar\(\); ==&gt; foo && bar\(\);

If \(foo\) bar\(\); ==&gt; foo \|\| bar\(\);



三.省略大括号{}

If \(foo\) return bar\(\) ; else something\(\) ; ==&gt; {if \( foo\) return bar\(\) ; something \(\) }

这种写法仅仅优化了一个大括号,建议使用UglifyJS帮助解决





使用Javascript一个获取html元素属性的方法



Function getAttr\(el,attrName\){

Var attr = { 'for' : 'htmlFor' , 'class' : 'className'}\[attrName\] \|\| attrName;

};



If\(x==null\)简写

If\(x==null\)或if\(typeof \(x\) == 'undefined' \)可以简写为if\(!x\),未验证

反之if\(x\)表示x非空



判断对象是否存在

If\(document.form1,.softurl9\){

//判断是否存在softurl9,防止js出错

}



If\(document.getElementById\('softurl9'\)\){

//判断是否存在softurl9,防止js出错

}







