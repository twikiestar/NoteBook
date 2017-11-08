一台IIS服务器被攻击之后，恢复备份，网页上的验证码全都无法显示

检查php GD2正常

清空Cookie以及网站缓存

问题依旧

运行了一个utf-8脚本修正文档是否自带BOM导致验证码不显示的错误

实际上这是一个文件编码错误，并不是网页代码出现错误

在本地通过管理员模式cmd运行以下php脚本解决：

注意以utf-8无BOM模式下开发！！

﻿&lt;?php 

/\*清除rom\*/

if\(isset\($\_GET\['dir'\]\)\){ 

    $basedir=$\_GET\['dir'\]; 

}else{ 

    $basedir = '.'; 

}   

$auto = 1;   

checkdir\($basedir\); 

function checkdir\($basedir\){ 

    if\($dh = opendir\($basedir\)\){ 

        while\(\($file = readdir\($dh\)\) !== false\){ 

            if\($file != '.' && $file != '..'\){ 

                if\(!is\_dir\($basedir."/".$file\)\){ 

                    echo "filename: $basedir/$file ".checkBOM\("$basedir/$file"\)." &lt;br&gt;"; 

                }else{ 

                    $dirname = $basedir."/".$file; 

                    checkdir\($dirname\); 

                } 

            } 

        }//end while 

    closedir\($dh\); 

    }//end if\($dh 

}//end function 

function checkBOM\($filename\){ 

    global $auto; 

    $contents = file\_get\_contents\($filename\); 

    $charset\[1\] = substr\($contents, 0, 1\);   

    $charset\[2\] = substr\($contents, 1, 1\);   

    $charset\[3\] = substr\($contents, 2, 1\);   

    if\(ord\($charset\[1\]\) == 239 && ord\($charset\[2\]\) == 187 && ord\($charset\[3\]\) == 191\){ 

        if\($auto == 1\){ 

            $rest = substr\($contents, 3\); 

            rewrite \($filename, $rest\); 

            return "&lt;font color=red&gt;BOM found, automatically removed.&lt;/font&gt;"; 

        }else{ 

            return \("&lt;font color=red&gt;BOM found.&lt;/font&gt;"\); 

        } 

    }   

    else return \("BOM Not Found."\); 

}//end function 

function rewrite\($filename, $data\){ 

    $filenum = fopen\($filename, "w"\); 

    flock\($filenum, LOCK\_EX\); 

    fwrite\($filenum, $data\); 

    fclose\($filenum\); 

}

?&gt;



