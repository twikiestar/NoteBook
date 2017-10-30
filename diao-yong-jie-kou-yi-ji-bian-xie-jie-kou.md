2017年10月21日

13:34



http://localhost/openUser.php?act=get\_user\_list&type=json



这里openUser.php相当于一个接口,其中get\_user\_list 是一个API\(获取用户列表\),返回数据格式为JSON数据



PHP GET 方式访问

$file\_contents = File\_get\_content\('

http://localhost/openUser.php?act=get\_user\_list&type=json

'\)



POST 方式访问\(需要开启PHP curl 模块支持\)

$url = 'http://localhost/openUser.php?act=get\_user\_list&type=json';

$ch = curl\_init\(\);

Curl\_setopt\($ch,CURLPOPT\_URL,$url\);

Curl\_setopt\($ch,CURLOPT\_RETURNTRANSFER,1\);

Curl\_setopt\($ch,CURLOPT\_CONNECTTIMEOUT,10\);

Curl\_setopt\($ch,CURLOPT\_POST,1\);//启用POST提交方式

$file\_content = curl\_exec\($ch\);

Curl\_close\($ch\);



一个简单的API例子

&lt;?php

	$output  =array\(\);

	$a = @$\_GET\['a'\] ? $\_GET\['a'\]:'';

	$uid = @$\_GET\['uid'\]?$\_GET\['uid'\]:0;

	

	If\(empty\($a\)\){

		$output =array\('data'=&gt;NULL,'info'=&gt;'没有数据啊','code'=&gt;-201\);

		Exit\(json\_encode\($output\)\);

	}

	//走接口

	If\($a == 'get\_users'\){

	//检查用户

		If\($uid == 0\){

			$output = array\('data'=&gt;NULL,'info'=&gt;'THE UID IS NULL','code'=&gt;-401\);

			Exit\(json\_encode\($output\)\);

		}

	}

	

	//假设$mysql 是数据库

	

	$mysql = array\(

		

	\)

	

?&gt;





