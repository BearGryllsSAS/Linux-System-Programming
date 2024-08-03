# `Linux`系统编程

## 01P `Linux`命令基础习惯

1. `date`显示系统当前时间
```shell
[root@haibara OperatingSystem]# date
Sat Aug  3 19:21:15 CST 2024
```

2. `cat /etc/shells`查看当前可使用的`shell`
```shell
[root@haibara OperatingSystem]# cat /etc/shells
/bin/sh
/bin/bash
/usr/bin/sh
/usr/bin/bash
```

3. `echo $SHELL`查看当前使用的`shell`
```shell
[root@haibara OperatingSystem]# echo $SHELL
/bin/bash
```
3. 主键盘快捷键
```
上              Ctrl-p
下              Ctrl-n
左              Ctrl-b
右              Ctrl-f
Del             Ctrl-d      delete 光标后面的
Home            Ctrl-a      first letter
End             Ctrl-e      end
Backspace       Backspace   delete 光标前面的单个字符
清除整行        Ctrl-u 
删除光标到行末  Ctrl-k
显示上滚        Shift-PgUp
显示下滚        Shift-PgDn
增大终端字体    Ctrl-Shift-+
减小终端字体    Ctrl--
新打开一个终端  Ctrl-Alt-T
清屏 Ctrl-l 直接用 clear 也行
```

## 02P 类`Unix`系统目录

1. `pwd`查看当前所在目录
```shell
[root@haibara OperatingSystem]# pwd
/home/OperatingSystem
```

2. `Linux`系统目录
```
bin：存放二进制可执行文件
boot：存放开机启动程序
dev：存放设备文件：字符设备、块设备
home：存放普通用户
etc：用户信息和系统配置文件 passwd、group
lib：库文件：libc.so.6
root：管理员宿主目录（家目录）
usr：用户资源管理目录 unix software resource
```

3. 查看鼠标日志
```shell
[root@haibara OperatingSystem]# cd /dev/input/
[root@haibara input]# ls
by-id  by-path  event0  event1  event2  event3  event4  event5  event6 mice  mouse0  mouse1  mouse2
[root@haibara input]# cat mice 
����^C
```

## 03P 目录和文件操作 1

1. `cd -`返回上一个目录
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql OperatingSystem  TinyWebServer
[root@haibara home]# cd ~
[root@haibara ~]# cd -
/home
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
```

2. `Linux`系统文件类型
```
普通文件：-
目录文件：d
字符设备文件：c
块设备文件：b
软连接：l
管道文件：p
套接字：s
未知文件
```

3. `ls`列出当前文件夹下目录项
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
```

4. `ls -l`显示目录项详细信息
```shell
[root@haibara home]# ls -l
total 40
drwxr-xr-x  2 root root 4096 Aug  1 17:19 code
drwxr-xr-x  3 root root 4096 Jul  4 17:30 dfs
drwxr-xr-x  5 root root 4096 Jul  6 16:36 InternetChatRoom
drwxr-xr-x  9 root root 4096 Jul  6 16:39 linux_high_performance_servers
drwxr-xr-x  2 root root 4096 Jul 14 17:48 metting
drwxr-xr-x  3 root root 4096 Jun 30 18:05 minio
drwxr-xr-x  4 root root 4096 Jul  5 18:49 moyi
drwxr-xr-x  5 root root 4096 Jun 30 17:47 mysql
drwxr-xr-x  2 root root 4096 Aug  3 12:23 OperatingSystem
drwxr-xr-x 12 root root 4096 Jul  6 16:43 TinyWebServer
```

5. `ll`竖排显示目录项和详细信息，`ls -l`的缩写
```shell
[root@haibara home]# ll
total 40
drwxr-xr-x  2 root root 4096 Aug  1 17:19 code
drwxr-xr-x  3 root root 4096 Jul  4 17:30 dfs
drwxr-xr-x  5 root root 4096 Jul  6 16:36 InternetChatRoom
drwxr-xr-x  9 root root 4096 Jul  6 16:39 linux_high_performance_servers
drwxr-xr-x  2 root root 4096 Jul 14 17:48 metting
drwxr-xr-x  3 root root 4096 Jun 30 18:05 minio
drwxr-xr-x  4 root root 4096 Jul  5 18:49 moyi
drwxr-xr-x  5 root root 4096 Jun 30 17:47 mysql
drwxr-xr-x  2 root root 4096 Aug  3 12:23 OperatingSystem
drwxr-xr-x 12 root root 4096 Jul  6 16:43 TinyWebServer
```

6. `ls -l dirname`显示`dirname`中目录详细信息
```shell
[root@haibara home]# ls -l TinyWebServer/
total 109184
-rw-r--r-- 1 root root   6029119 Jul  6 16:39 2024_02_20_ServerLog
-rw-r--r-- 1 root root 100825534 Jul  6 16:41 2024_03_12_ServerLog
-rw-r--r-- 1 root root   1019200 Jul  6 16:40 2024_03_13_ServerLog
-rw-r--r-- 1 root root    824367 Jul  6 16:40 2024_03_14_ServerLog
-rw-r--r-- 1 root root    918557 Jul  6 16:41 2024_03_15_ServerLog
-rw-r--r-- 1 root root    851973 Jul  6 16:41 2024_03_16_ServerLog
-rw-r--r-- 1 root root    829551 Jul  6 16:41 2024_03_17_ServerLog
-rw-r--r-- 1 root root       141 Jul  6 16:41 2024_03_18_ServerLog
-rw-r--r-- 1 root root        47 Jul  6 16:41 2024_03_25_ServerLog
drwxr-xr-x 3 root root      4096 Jul  6 16:41 build
-rw-r--r-- 1 root root        24 Jul  6 16:41 build.sh
drwxr-xr-x 2 root root      4096 Jul  6 16:41 CGImysql
-rw-r--r-- 1 root root       919 Jul  6 16:41 CMakeLists.txt
-rw-r--r-- 1 root root      1636 Jul  6 16:41 config.cpp
-rw-r--r-- 1 root root       650 Jul  6 16:41 config.h
drwxr-xr-x 2 root root      4096 Jul  6 16:41 http
-rw-r--r-- 1 root root     11357 Jul  6 16:41 LICENSE
drwxr-xr-x 2 root root      4096 Jul  6 16:41 lock
drwxr-xr-x 2 root root      4096 Jul  6 16:41 log
-rw-r--r-- 1 root root       894 Jul  6 16:41 main.cpp
-rw-r--r-- 1 root root       311 Jul  6 16:41 makefile
-rw-r--r-- 1 root root     12184 Jul  6 16:41 README.md
drwxr-xr-x 2 root root      4096 Jul  6 16:42 root
-rw-r--r-- 1 root root    378512 Jul  6 16:41 server
drwxr-xr-x 3 root root      4096 Jul  6 16:43 test_pressure
drwxr-xr-x 2 root root      4096 Jul  6 16:43 threadpool
drwxr-xr-x 2 root root      4096 Jul  6 16:43 timer
-rw-r--r-- 1 root root     11000 Jul  6 16:43 webserver.cpp
-rw-r--r-- 1 root root      1967 Jul  6 16:43 webserver.h
```

7. `ls -dl dirname`显示`dirname`本身的详细信息
```shell
[root@haibara home]# ls -dl TinyWebServer/
drwxr-xr-x 12 root root 4096 Jul  6 16:43 TinyWebServer/
```

8. `ls -R`递归查看目录
```shell
[root@haibara home]# ls -R code/
code/:
A  B

code/A:
a.txt

code/B:
b.txt
```

9. `ls -Rl`递归展示详细信息
```shell
[root@haibara home]# ls -Rl code/
code/:
total 8
drwxr-xr-x 2 root root 4096 Aug  3 19:30 A
drwxr-xr-x 2 root root 4096 Aug  3 19:30 B

code/A:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:30 a.txt

code/B:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:30 b.txt
```

10. 文件权限说明
```shell
drwxr-xr-x | 3        | root |  root |  4096 |  Jul  6 16:41 |  build
-rw-r--r-- | 1        | root |  root |  24   |  Jul  6 16:41 |  build.sh
drwxr-xr-x | 2        | root |  root |  4096 |  Jul  6 16:41 |  CGImysql

文件权限     硬链接计数  所有者  所属组   大小    时间            文件名/文件夹名

权限具体展开
-rw-r—r—
1234567890
1 代表文件类型
234 代表所有者读写执行权限
567 代表同组用户读写执行权限
890 代表其他人读写执行权限
```

11. `which instruct`查看`instruct`命令所在目录位置
```shell
[root@haibara home]# which date
/usr/bin/date
```

12. 隐藏终端中的路径
```shell
vi ~./bash 打开使用的 shell 环境配置文件
末尾添加 PS1=$ 保存退出，重启终端即可
```
![隐藏终端中的路径](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408032314894.png)

13. `mkdir dirname`新建目录
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
[root@haibara home]# mkdir tempDir
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempDir  TinyWebServer
```

14. `rmdir dirname`删除空目录，非空目录删不掉
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempDir  TinyWebServer
[root@haibara home]# rmdir tempDir/
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
```

15. `touch filename`创建名为`name`的空文件
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
[root@haibara home]# touch tempFile
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempFile  TinyWebServer
```

16. `rm filename`删除文件
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempFile  TinyWebServer
[root@haibara home]# rm tempFile 
rm: remove regular empty file 'tempFile'? y
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
```

17. `rm -r dirname`递归删除目录
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
[root@haibara home]# rm -r code/
rm: descend into directory 'code/'? n
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
```

18. `rm -rf dirname`强制删除
```shell
[root@haibara home]# ls
code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
[root@haibara home]# rm -rf code/
[root@haibara home]# ls
dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
```

19. `mv file1 file2 location`将文件 1 和文件 2 移动到目标位置
```shell
[root@haibara OperatingSystem]# ls
a.txt  b.txt  tempDir
[root@haibara OperatingSystem]# mv a.txt b.txt tempDir/
[root@haibara OperatingSystem]# ls
tempDir
[root@haibara OperatingSystem]# ls tempDir/
a.txt  b.txt
```

20. `cp filename dirname`复制文件到目录
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir
[root@haibara OperatingSystem]# cp c.txt tempDir/
[root@haibara OperatingSystem]# ls -R
.:
c.txt  tempDir

./tempDir:
a.txt  b.txt  c.txt
```

21. `cp filename1 filename2`复制文件 1 并重命名为文件 2
```shell
[root@haibara tempDir]# ls
a.txt  b.txt  c.txt
[root@haibara tempDir]# cp a.txt a_copy.txt
[root@haibara tempDir]# ls
a_copy.txt  a.txt  b.txt  c.txt
```

22. `cp -a dirname1 dirname2`复制目录 1 及其下所有文件到目录 2
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# cp -a tempDir tempDirCopy1
[root@haibara OperatingSystem]# ls -R
.:
c.txt  tempDir  tempDirCopy1  tempDirCopy2

./tempDir:
a_copy.txt  a.txt  b.txt  c.txt

./tempDirCopy1:
tempDir

./tempDirCopy1/tempDir:
a_copy.txt  a.txt  b.txt  c.txt

./tempDirCopy2:
[root@haibara OperatingSystem]# ls -Rl
.:
total 12
-rw-r--r-- 1 root root    0 Aug  3 19:39 c.txt
drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
drwxr-xr-x 2 root root 4096 Aug  3 19:41 tempDirCopy2

./tempDir:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
-rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
-rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
-rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt

./tempDirCopy1:
total 4
drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir

./tempDirCopy1/tempDir:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
-rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
-rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
-rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt

./tempDirCopy2:
total 0

这里-a 和-r 的差别在于，-a 是完全复制，文件权限，改动时间什么的也完全相同。
```

23. `cp -r dirname1 dirname2`递归复制目录 1 到目录 2
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# cp -r tempDir tempDirCopy2
[root@haibara OperatingSystem]# ls -Rl
.:
total 12
-rw-r--r-- 1 root root    0 Aug  3 19:39 c.txt
drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2

./tempDir:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
-rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
-rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
-rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt

./tempDirCopy1:
total 4
drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir

./tempDirCopy1/tempDir:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
-rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
-rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
-rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt

./tempDirCopy2:
total 4
drwxr-xr-x 2 root root 4096 Aug  3 19:43 tempDir

./tempDirCopy2/tempDir:
total 0
-rw-r--r-- 1 root root 0 Aug  3 19:43 a_copy.txt
-rw-r--r-- 1 root root 0 Aug  3 19:43 a.txt
-rw-r--r-- 1 root root 0 Aug  3 19:43 b.txt
-rw-r--r-- 1 root root 0 Aug  3 19:43 c.txt

这里-a 和-r 的差别在于，-a 是完全复制，文件权限，改动时间什么的也完全相同。
```

## 04P 目录和文件操作2
1. `cat filename`查看文件内容
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# cat c.txt 
这是第一行
这是第二行
这是第三行
这是第四行
这是第五行
这是第六行
这是第七行
这是第八行
这是第九行
这是第十行
这是第十一行
这是第十二行
这是第十三行
```

2. `tac filename`逆转查看文件内容
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# tac c.txt 
这是第十三行
这是第十二行
这是第十一行
这是第十行
这是第九行
这是第八行
这是第七行
这是第六行
这是第五行
这是第四行
这是第三行
这是第二行
这是第一行
```

3. `cat`读取终端，就是回显
```shell
[root@haibara OperatingSystem]# cat
读取终端，回显
读取终端，回显
^C
```

4. `more filename`和`cat`差不多，但是对于大文件查看很强势。空格翻页，回车一行用`q`或者`Ctrl-c`退出
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# more c.txt 
这是第一行
这是第二行
这是第三行
这是第四行
这是第五行
这是第六行
这是第七行
这是第八行
这是第九行
这是第十行
这是第十一行
这是第十二行
这是第十三行
```

5. `less filename`也和`cat`差不多。会进入到另一个阅读界面，空格翻页，回车一行用`q`或者`Ctrl-c`退出
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# less c.txt 
```

6. `head -n filename`查看文件前`n`行，不加`-n`参数默认查看 10 行
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# head -5 c.txt 
这是第一行
这是第二行
这是第三行
这是第四行
这是第五行
```

7. `tail -n filename`查看文件后`n`行，默认查看 10 行，顺序显示
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# tail -5 c.txt 
这是第九行
这是第十行
这是第十一行
这是第十二行
这是第十三行
```

8. `tree`命令，查看当前目录结构树（需要自行下载`tree`）
```shell
[root@haibara OperatingSystem]# ls
c.txt  tempDir  tempDirCopy1  tempDirCopy2
[root@haibara OperatingSystem]# tree
.
├── c.txt
├── tempDir
│   ├── a_copy.txt
│   ├── a.txt
│   ├── b.txt
│   └── c.txt
├── tempDirCopy1
│   └── tempDir
│       ├── a_copy.txt
│       ├── a.txt
│       ├── b.txt
│       └── c.txt
└── tempDirCopy2
    └── tempDir
        ├── a_copy.txt
        ├── a.txt
        ├── b.txt
        └── c.txt

5 directories, 13 files
```

## 05P 软链接和硬链接

## 06P 创建修改用户和用户组

## 07P `find`命令1

## 08P 午后复习

## 09P `find`命令2

## 10P `grep`和`xargs`

## 11P `xargs`加强和`awk`说明

## 12P 软件包安装

## 13P 压缩命令`gzip`和`bzip2`

## 14P `rar`压缩和`zip`压缩

## 15P 其他命令

## 16P 总结

## 17P 复习

## 18P `vim`的三种工作模式

## 19P `vim`基本操作-跳转和删字符

## 20P `vim`基本操作-删除

## 21P `vim`基本操作-复制粘贴

## 22p `vim`基本操作-查找和替换

## 23P `vim`基本操作-其他

## 24P `vim`配置思路

## 25P `gcc`编译4步骤

## 26P `gcc`编译常用参数

## 27P 午后复习

## 28P 动态库和静态库理论对比

## 29P 静态库制作

## 30P 静态库使用及头文件对应

## 31P 动态库制作-生成与位置无关代码

## 32P 动态库制作-演示

## 33P 动态库加载错误原因及解决方式

## 34P 动态库加载错误原因及解决方式2

## 35P 扩展讲解-数据段合并

## 36P 总结

## 37P 复习

## 38P `gdb`调试基础指令

## 39P `gdb`调试其他指令

## 40P `gdb`常见错误说明

## 41P `makefile`基础规则

## 42P `makefile`的一个规则

## 43P 午后回顾

## 44P `makefile`两个函数和`clean`

## 45P `makefile`三个自动变量和模式规则

## 46P 习题和作业

## 47P 系统编程阶段说在前面的话

## 48P `open`函数

## 49P 总结

## 50P 复习

## 51P `makefile`作业

## 52P `read`和`write`实现`cp`

## 53P 系统调用和库函数比较-预读入缓输出

## 54P 文件描述符

## 55P 阻塞和非阻塞

## 56- cntl改文件属性

## 57P 午后回顾

## 58P `lseek`函数

## 59P 传入传出参数

## 60P 目录项和`inode`

## 61P `stat`函数

## 62p `lstat`和`stat`

## 63P 传出参数当返回值

## 64P `link`和`UNlink`隐式回收

## 65P 文件目录`rwx`权限差异

## 66P 目录操作函数

## 67P 总结

## 68P 复习

## 69P 递归遍历目录思路分析

## 70P 递归遍历目录代码预览

## 71P 递归遍历目录实现

## 72P 递归遍历目录总结

## 73P `dup`和`dup2`

## 74P `fcntl`实现`dup`描述符

## 75P 复习

## 76P 进程和程序以及`CPU`相关

## 77P 虚拟内存和物理内存映射关系

## 78P `pcb`进程控制块

## 79P 环境变量

## 80P `fork`函数原理

## 81P `fork`创建子进程

## 82P `getpid`和`getppid`

## 83P 循环创建多个子进程

## 84P 父子进程共享哪些内容

## 85P 父子进程共享

## 86P 总结

## 87P 复习

## 88P 父子进程`qdb`调试

## 89P `exec`函数族

## 90P `execlp`和`ececl`函数

## 91P `exec`函数族特性

## 92P 孤儿进程和僵尸进程

## 93P `wait`回收子进程

## 94P 获取子进程退出值和异常终止信号

## 95P `waitpid`回收子进程

## 96P 中午回顾

## 97P 错误解析

## 98P `waitpid`回收多个子进程

## 99P `wait`和`waitpid`总结

## 100P 进程间通信常见方式

## 101P 管道的特质

## 102P 管道的基本用法

## 103P 管道读写行为

## 104P 父子进程通信练习分析

## 105P 总结

## 106P 复习

## 107P 父子进程`lswc-l`

## 108P 兄弟进程间通信

## 109P 多个读写端操作管道和管道缓冲区大小

## 110P 命名管道`fifo`的创建和原理图

## 111P `fifo`实现非血缘关系进程间通信

## 112P 文件用于进程间通信

## 113P `mmap`函数原型

## 114P 复习

## 115P `mmap`建立映射区

## 116P `mmap`使用注意事项1

## 117P `mmap`使用注意事项2

## 118P `mmap`总结

## 119P 父子进程间`mmap`通信

## 120P 无血缘关系进程间`mmap`通信

## 121P `mmap`总结

## 122P `mmap`匿名映射区

## 123P 总结

## 124P 复习

## 125P 信号的概念和机制

## 126P 与信号相关的概念

## 127P 信号屏蔽字和未决信号集

## 128P 信号四要素和常规信号一览

## 129P `kill`函数和`kill`命令

## 130P `alarm`函数

## 131P `setitimer`函数

## 132P 午后回顾

## 133P 信号集操作函数

## 134P 信号操作函数使用原理分析

## 135P 信号集操作函数练习

## 136P `siqnal`实现信号捕捉

## 137P `sigaction`实现信号捕捉

## 138P 信号捕捉的特性

## 139P 内核实现信号捕捉简析

## 140P 借助信号捕捉回收子进程

## 141P 慢速系统调用中断

## 142P 总结

## 143P 复习子进程借助信号回收

## 144P 会话和进程组

## 145P 守护进程创建步骤分析

## 146P 守护进程创建

## 147P 线程概念

## 148P 三级映射

## 149P 线程共享和非共享

## 150P 中午复习

## 151P 创建线程

## 152P 循环创建多个子线程

## 153P 错误分析

## 154P 线程间全局变量共享

## 155P `pthread exit`退出

## 156P `pthread join`

## 157P `pthread join`作业

## 158P `pthread cancel`函数

## 159P 检查出错返回

## 160P 线程分离`pthread detach`

## 161P 进程和线程控制原语对比

## 162P 线程属性设置分离线程

## 163P 线程使用注意事项

## 164P 总结

## 165P 线程同步概念

## 166P 锁使用的注意事项

## 167P 借助互斥锁管理共享数据实现同步

## 168P 互斥锁使用技巧

## 169P `try`锁

## 170P 读写锁操作函数原型

## 171P 两种死锁

## 172P 读写锁原理

## 173P `rwlock`

## 174P 午后复习

## 175P 静态初始化条件变量和互斥量

## 176P 条件变量和相关函数`wait`

## 177P 条件变量的生产者消费者模型分析

## 178P 条件变量生产者消费者代码预览

## 179P 条件变量实现生产者消费者代码

## 180P 多个消费者使用`while`做

## 181P 条件变量`siqnal`注意事项

## 182P 信号量概念及其相关操作函数

## 183P 信号量实现的生产者消费者

## 184P 总结