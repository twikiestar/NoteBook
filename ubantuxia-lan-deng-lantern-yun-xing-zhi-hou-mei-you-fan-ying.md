Linux -- Lantern 无法启动

问题：

```
  今天安装了Lantern之后，不能启动起来，一闪而过

  命令行里启动，包如下错误：
```

/.lantern/bin/lantern: error while loading shared libraries: libappindicator3.so.1: cannot open shared object file: No such file or directory

尝试 安装  apt-get install libappindicator3-1

结果：

```
 可以愉快的玩耍了
```



