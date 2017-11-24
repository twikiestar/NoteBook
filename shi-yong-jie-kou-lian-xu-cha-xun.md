今天遇到了连续使用某个接口查询手机号运营商，在连续查询中可能需要花费大量的时间

导致超出了php.ini中脚本执行的最大时间限制

出现Maximum Execution Time Exceed 导致脚本终止

解决这个问题首先要给数据查询的地方设置缓冲，防止脚本超出最大内存，所以要在一次查询插入之间设置延时并且刷新浏览器，清除内存中的记录

在开始前设置脚本最大运行时间为不限时间

set \__ time _\_ limit\(0\);//设置脚本运行不限时间;

在SQL插入完成后执行以下代码

flush\(\);//把当前程序运行的数据返回给浏览器客户端

ob\_flush\(\);//刷新内存以便腾出空间继续执行查询



public function refreash\_user\_province\(\){

        //设置脚本超时时间为永不过期

        set\_time\_limit\(0\);

        // 查询已有手机号的用户执行归属地的查询与写入

        $mod =  M\('user'\);

        //所有记录了手机号码没有记录归属地的用户数组

        $phones = $mod-&gt;query\("SELECT id,mobile\_phone FROM \`weixin\_user\` where mobile\_phone !='' and mobile\_phone !=0 and phone\_location='' "\);

        foreach \($phones as $key =&gt; $value\) {

            $mobile = $value\['mobile\_phone'\];

                $info = get\_mobile\_area\($mobile\);//content返回一个省份与手机号的运营商

            if\(!$info\['province'\]\){

                $this-&gt;success\('数据刷新成功',U\('user\_show\_off/member\_maps'\) \);

            }else{

                $content=implode\("",$info\);

                $where\['id'\] = $value\['id'\];

                $data\['phone\_location'\] = $content;

                $mod-&gt;where\($where\)-&gt;save\($data\);

                /\*刷新缓冲区域\*/

                flush\(\);

                ob\_flush\(\);

                usleep\(50000\);//延迟执行500ms

            }

        }

        // echo"&lt;pre&gt;";

        // var\_dump\($info\);

    }





common.php//公共函数

	/\*

    \*查询手机号归属地函数

    \*/

    function get\_mobile\_area\($mobile\){

        $sms = array\('province'=&gt;'', 'supplier'=&gt;''\);    //初始化变量

        //根据淘宝的数据库调用返回值

        $url = "https://tcc.taobao.com/cc/json/mobile\_tel\_segment.htm?tel=".$mobile."&t=".time\(\);

        $ch = curl\_init\(\);

		curl\_setopt\($ch, CURLOPT\_URL,$url\);

		curl\_setopt\($ch, CURLOPT\_RETURNTRANSFER, 1\);

		curl\_setopt\($ch, CURLOPT\_SSL\_VERIFYPEER, FALSE\);

        curl\_setopt\($ch, CURLOPT\_SSL\_VERIFYHOST, FALSE\);

        curl\_setopt\($ch, CURLOPT\_POST, 1\);

        $file\_contents = mb\_convert\_encoding\( curl\_exec\($ch\) , 'UTF-8', 'GBK,UTF-8,ASCII'\); 

		curl\_close\($ch\);

		if\(mb\_substr\($file\_contents, "54", "2",'utf-8'\)=="内蒙"\){

					$sms\['province'\] = '内蒙古';

					$sms\['supplier'\] = mb\_substr\($file\_contents, "73", "4",'utf-8'\);

				}elseif\(mb\_substr\($file\_contents, "54", "2",'utf-8'\)=="黑龙"\){

					$sms\['province'\] = '黑龙江';

					$sms\['supplier'\] = mb\_substr\($file\_contents, "73", "4",'utf-8'\);

				}else{

			        $sms\['province'\] = mb\_substr\($file\_contents, "54", "2",'utf-8'\);  //截取字符串

			        $sms\['supplier'\] = mb\_substr\($file\_contents, "72", "4",'utf-8'\);

			    }

		// var\_dump\($file\_contents\);

		// var\_dump\($sms\);

        return $sms;

    }

