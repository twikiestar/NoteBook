执行shell脚本的时候出现bad interpreter

我当时是再用window系统，通过winSCP获取的框架CMD脚本，然后通过编辑器sublime修改之后更新给linux下出现了这段错误

找了资料之后发现windows会把文件属性默认改为dos文件，然后shell脚本出现编译错误

查询资料之后得知

需要在linux下使用vim

：set ff 查看当前文件属性

如果属性为dos说明文件被windows修改了

：set ff=unix 强制修改为unix文件属性

ok问题解决

