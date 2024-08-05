# `Linux`系统编程

## 01P `Linux`命令基础习惯

1. `date`显示系统当前时间
> ```shell
> [root@haibara OperatingSystem]# date
> Sat Aug  3 19:21:15 CST 2024
> ```

2. `cat /etc/shells`查看当前可使用的`shell`
> ```shell
> [root@haibara OperatingSystem]# cat /etc/shells
> /bin/sh
> /bin/bash
> /usr/bin/sh
> /usr/bin/bash
> ```

3. `echo $SHELL`查看当前使用的`shell`
> ```shell
> [root@haibara OperatingSystem]# echo $SHELL
> /bin/bash
> ```
4. 主键盘快捷键
> ```
> 上              Ctrl-p
> 下              Ctrl-n
> 左              Ctrl-b
> 右              Ctrl-f
> Del             Ctrl-d      delete 光标后面的
> Home            Ctrl-a      first letter
> End             Ctrl-e      end
> Backspace       Backspace   delete 光标前面的单个字符
> 清除整行        Ctrl-u 
> 删除光标到行末  Ctrl-k
> 显示上滚        Shift-PgUp
> 显示下滚        Shift-PgDn
> 增大终端字体    Ctrl-Shift-+
> 减小终端字体    Ctrl--
> 新打开一个终端  Ctrl-Alt-T
> 清屏 Ctrl-l 直接用 clear 也行
> ```

## 02P 类`Unix`系统目录

1. `pwd`查看当前所在目录
> ```shell
> [root@haibara OperatingSystem]# pwd
> /home/OperatingSystem
> ```

2. `Linux`系统目录
> ```
> bin：存放二进制可执行文件
> boot：存放开机启动程序
> dev：存放设备文件：字符设备、块设备
> home：存放普通用户
> etc：用户信息和系统配置文件 passwd、group
> lib：库文件：libc.so.6
> root：管理员宿主目录（家目录）
> usr：用户资源管理目录 unix software resource
> ```

3. 查看鼠标日志
> ```shell
> [root@haibara OperatingSystem]# cd /dev/input/
> [root@haibara input]# ls
> by-id  by-path  event0  event1  event2  event3  event4  event5  event6 mice  mouse0  mouse1  mouse2
> [root@haibara input]# cat mice 
> ����^C
> ```

## 03P 目录和文件操作 1

1. `cd -`返回上一个目录
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql OperatingSystem  TinyWebServer
> [root@haibara home]# cd ~
> [root@haibara ~]# cd -
> /home
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> ```

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
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> ```

4. `ls -l`显示目录项详细信息
> ```shell
> [root@haibara home]# ls -l
> total 40
> drwxr-xr-x  2 root root 4096 Aug  1 17:19 code
> drwxr-xr-x  3 root root 4096 Jul  4 17:30 dfs
> drwxr-xr-x  5 root root 4096 Jul  6 16:36 InternetChatRoom
> drwxr-xr-x  9 root root 4096 Jul  6 16:39 linux_high_performance_servers
> drwxr-xr-x  2 root root 4096 Jul 14 17:48 metting
> drwxr-xr-x  3 root root 4096 Jun 30 18:05 minio
> drwxr-xr-x  4 root root 4096 Jul  5 18:49 moyi
> drwxr-xr-x  5 root root 4096 Jun 30 17:47 mysql
> drwxr-xr-x  2 root root 4096 Aug  3 12:23 OperatingSystem
> drwxr-xr-x 12 root root 4096 Jul  6 16:43 TinyWebServer
> ```

5. `ll`竖排显示目录项和详细信息，`ls -l`的缩写
> ```shell
> [root@haibara home]# ll
> total 40
> drwxr-xr-x  2 root root 4096 Aug  1 17:19 code
> drwxr-xr-x  3 root root 4096 Jul  4 17:30 dfs
> drwxr-xr-x  5 root root 4096 Jul  6 16:36 InternetChatRoom
> drwxr-xr-x  9 root root 4096 Jul  6 16:39 linux_high_performance_servers
> drwxr-xr-x  2 root root 4096 Jul 14 17:48 metting
> drwxr-xr-x  3 root root 4096 Jun 30 18:05 minio
> drwxr-xr-x  4 root root 4096 Jul  5 18:49 moyi
> drwxr-xr-x  5 root root 4096 Jun 30 17:47 mysql
> drwxr-xr-x  2 root root 4096 Aug  3 12:23 OperatingSystem
> drwxr-xr-x 12 root root 4096 Jul  6 16:43 TinyWebServer
> ```

6. `ls -l dirname`显示`dirname`中目录详细信息
> ```shell
> [root@haibara home]# ls -l TinyWebServer/
> total 109184
> -rw-r--r-- 1 root root   6029119 Jul  6 16:39 2024_02_20_ServerLog
> -rw-r--r-- 1 root root 100825534 Jul  6 16:41 2024_03_12_ServerLog
> -rw-r--r-- 1 root root   1019200 Jul  6 16:40 2024_03_13_ServerLog
> -rw-r--r-- 1 root root    824367 Jul  6 16:40 2024_03_14_ServerLog
> -rw-r--r-- 1 root root    918557 Jul  6 16:41 2024_03_15_ServerLog
> -rw-r--r-- 1 root root    851973 Jul  6 16:41 2024_03_16_ServerLog
> -rw-r--r-- 1 root root    829551 Jul  6 16:41 2024_03_17_ServerLog
> -rw-r--r-- 1 root root       141 Jul  6 16:41 2024_03_18_ServerLog
> -rw-r--r-- 1 root root        47 Jul  6 16:41 2024_03_25_ServerLog
> drwxr-xr-x 3 root root      4096 Jul  6 16:41 build
> -rw-r--r-- 1 root root        24 Jul  6 16:41 build.sh
> drwxr-xr-x 2 root root      4096 Jul  6 16:41 CGImysql
> -rw-r--r-- 1 root root       919 Jul  6 16:41 CMakeLists.txt
> -rw-r--r-- 1 root root      1636 Jul  6 16:41 config.cpp
> -rw-r--r-- 1 root root       650 Jul  6 16:41 config.h
> drwxr-xr-x 2 root root      4096 Jul  6 16:41 http
> -rw-r--r-- 1 root root     11357 Jul  6 16:41 LICENSE
> drwxr-xr-x 2 root root      4096 Jul  6 16:41 lock
> drwxr-xr-x 2 root root      4096 Jul  6 16:41 log
> -rw-r--r-- 1 root root       894 Jul  6 16:41 main.cpp
> -rw-r--r-- 1 root root       311 Jul  6 16:41 makefile
> -rw-r--r-- 1 root root     12184 Jul  6 16:41 README.md
> drwxr-xr-x 2 root root      4096 Jul  6 16:42 root
> -rw-r--r-- 1 root root    378512 Jul  6 16:41 server
> drwxr-xr-x 3 root root      4096 Jul  6 16:43 test_pressure
> drwxr-xr-x 2 root root      4096 Jul  6 16:43 threadpool
> drwxr-xr-x 2 root root      4096 Jul  6 16:43 timer
> -rw-r--r-- 1 root root     11000 Jul  6 16:43 webserver.cpp
> -rw-r--r-- 1 root root      1967 Jul  6 16:43 webserver.h
> ```

7. `ls -dl dirname`显示`dirname`本身的详细信息
> ```shell
> [root@haibara home]# ls -dl TinyWebServer/
> drwxr-xr-x 12 root root 4096 Jul  6 16:43 TinyWebServer/
> ```

8. `ls -R`递归查看目录
> ```shell
> [root@haibara home]# ls -R code/
> code/:
> A  B
> 
> code/A:
> a.txt
> 
> code/B:
> b.txt
> ```

9. `ls -Rl`递归展示详细信息
> ```shell
> [root@haibara home]# ls -Rl code/
> code/:
> total 8
> drwxr-xr-x 2 root root 4096 Aug  3 19:30 A
> drwxr-xr-x 2 root root 4096 Aug  3 19:30 B
> 
> code/A:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:30 a.txt
> 
> code/B:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:30 b.txt
> ```

10. 文件权限说明
> ```shell
> drwxr-xr-x | 3        | root |  root |  4096 |  Jul  6 16:41 |  build
> -rw-r--r-- | 1        | root |  root |  24   |  Jul  6 16:41 |  build.sh
> drwxr-xr-x | 2        | root |  root |  4096 |  Jul  6 16:41 |  CGImysql
> 
> 文件权限     硬链接计数  所有者  所属组   大小    时间            文件名/文件夹名
> 
> 权限具体展开
> -rw-r—r—
> 1234567890
> 1 代表文件类型
> 234 代表所有者读写执行权限
> 567 代表同组用户读写执行权限
> 890 代表其他人读写执行权限
> ```
> 
> 11. `which instruct`查看`instruct`命令所在目录位置
> ```shell
> [root@haibara home]# which date
> /usr/bin/date
> ```

12. 隐藏终端中的路径
> ```shell
> vi ~./bash 打开使用的 shell 环境配置文件
> 末尾添加 PS1=$ 保存退出，重启终端即可
> ```
> ![隐藏终端中的路径](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408032314894.png)

13. `mkdir dirname`新建目录
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> [root@haibara home]# mkdir tempDir
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempDir  TinyWebServer
> ```

14. `rmdir dirname`删除空目录，非空目录删不掉
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempDir  TinyWebServer
> [root@haibara home]# rmdir tempDir/
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> ```

15. `touch filename`创建名为`name`的空文件
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> [root@haibara home]# touch tempFile
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempFile  TinyWebServer
> ```

16. `rm filename`删除文件
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  tempFile  TinyWebServer
> [root@haibara home]# rm tempFile 
> rm: remove regular empty file 'tempFile'? y
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> ```

17. `rm -r dirname`递归删除目录
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> [root@haibara home]# rm -r code/
> rm: descend into directory 'code/'? n
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> ```

18. `rm -rf dirname`强制删除
> ```shell
> [root@haibara home]# ls
> code  dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> [root@haibara home]# rm -rf code/
> [root@haibara home]# ls
> dfs  InternetChatRoom  linux_high_performance_servers  metting  minio  moyi  mysql  OperatingSystem  TinyWebServer
> ```

19. `mv file1 file2 location`将文件 1 和文件 2 移动到目标位置
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  tempDir
> [root@haibara OperatingSystem]# mv a.txt b.txt tempDir/
> [root@haibara OperatingSystem]# ls
> tempDir
> [root@haibara OperatingSystem]# ls tempDir/
> a.txt  b.txt
> ```

20. `cp filename dirname`复制文件到目录
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir
> [root@haibara OperatingSystem]# cp c.txt tempDir/
> [root@haibara OperatingSystem]# ls -R
> .:
> c.txt  tempDir
> 
> ./tempDir:
> a.txt  b.txt  c.txt
> ```

21. `cp filename1 filename2`复制文件 1 并重命名为文件 2
> ```shell
> [root@haibara tempDir]# ls
> a.txt  b.txt  c.txt
> [root@haibara tempDir]# cp a.txt a_copy.txt
> [root@haibara tempDir]# ls
> a_copy.txt  a.txt  b.txt  c.txt
> ```

22. `cp -a dirname1 dirname2`复制目录 1 及其下所有文件到目录 2
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# cp -a tempDir tempDirCopy1
> [root@haibara OperatingSystem]# ls -R
> .:
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> 
> ./tempDir:
> a_copy.txt  a.txt  b.txt  c.txt
> 
> ./tempDirCopy1:
> tempDir
> 
> ./tempDirCopy1/tempDir:
> a_copy.txt  a.txt  b.txt  c.txt
> 
> ./tempDirCopy2:
> [root@haibara OperatingSystem]# ls -Rl
> .:
> total 12
> -rw-r--r-- 1 root root    0 Aug  3 19:39 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 2 root root 4096 Aug  3 19:41 tempDirCopy2
> 
> ./tempDir:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt
> 
> ./tempDirCopy1:
> total 4
> drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
> 
> ./tempDirCopy1/tempDir:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt
> 
> ./tempDirCopy2:
> total 0
> 
> 这里-a 和-r 的差别在于，-a 是完全复制，文件权限，改动时间什么的也完全相同。
> ```

23. `cp -r dirname1 dirname2`递归复制目录 1 到目录 2
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# cp -r tempDir tempDirCopy2
> [root@haibara OperatingSystem]# ls -Rl
> .:
> total 12
> -rw-r--r-- 1 root root    0 Aug  3 19:39 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> 
> ./tempDir:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt
> 
> ./tempDirCopy1:
> total 4
> drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
> 
> ./tempDirCopy1/tempDir:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:40 a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:38 a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:39 b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 c.txt
> 
> ./tempDirCopy2:
> total 4
> drwxr-xr-x 2 root root 4096 Aug  3 19:43 tempDir
> 
> ./tempDirCopy2/tempDir:
> total 0
> -rw-r--r-- 1 root root 0 Aug  3 19:43 a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 c.txt
> 
> 这里-a 和-r 的差别在于，-a 是完全复制，文件权限，改动时间什么的也完全相同。
> ```

## 04P 目录和文件操作2
1. `cat filename`查看文件内容
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# cat c.txt 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> ```
> 
> 2. `tac filename`逆转查看文件内容
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tac c.txt 
> 这是第十三行
> 这是第十二行
> 这是第十一行
> 这是第十行
> 这是第九行
> 这是第八行
> 这是第七行
> 这是第六行
> 这是第五行
> 这是第四行
> 这是第三行
> 这是第二行
> 这是第一行
> ```

3. `cat`读取终端，就是回显
> ```shell
> [root@haibara OperatingSystem]# cat
> 读取终端，回显
> 读取终端，回显
> ^C
> ```

4. `more filename`和`cat`差不多，但是对于大文件查看很强势。空格翻页，回车一行用`q`或者`Ctrl-c`退出
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# more c.txt 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> ```

5. `less filename`也和`cat`差不多。会进入到另一个阅读界面，空格翻页，回车一行用`q`或者`Ctrl-c`退出
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# less c.txt 
> ```

6. `head -n filename`查看文件前`n`行，不加`-n`参数默认查看 10 行
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# head -5 c.txt 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> ```

7. `tail -n filename`查看文件后`n`行，默认查看 10 行，顺序显示
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tail -5 c.txt 
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> ```

8. `tree`命令，查看当前目录结构树（需要自行下载`tree`）
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tree
> .
> ├── c.txt
> ├── tempDir
> │   ├── a_copy.txt
> │   ├── a.txt
> │   ├── b.txt
> │   └── c.txt
> ├── tempDirCopy1
> │   └── tempDir
> │       ├── a_copy.txt
> │       ├── a.txt
> │       ├── b.txt
> │       └── c.txt
> └── tempDirCopy2
>     └── tempDir
>         ├── a_copy.txt
>         ├── a.txt
>         ├── b.txt
>         └── c.txt
> 
> 5 directories, 13 files
> ```

## 05P 软链接和硬链接

1. `ln -s file file.s`创建一个软链接
> ```shell
> > [root@haibara OperatingSystem]# ls
> > c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# ln -s c.txt c.txt.s
> [root@haibara OperatingSystem]# ls
> c.txt  c.txt.s  tempDir  tempDirCopy1  tempDirCopy2
> ```
> 软链接就像`Windows`下的快捷方式
> ```shell
> [root@haibara OperatingSystem]# cat c.txt.s 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> [root@haibara OperatingSystem]# cat c.txt
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> ```
> 软链接的大小是文件路径的大小
> ```shell
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 root root  217 Aug  3 19:45 c.txt
> lrwxrwxrwx 1 root root    5 Aug  3 19:51 c.txt.s -> c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:40 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```
> `Linux`下的软链接行为和`Windows`下的快捷方式差不多，但是如果是用相对路径创建的软链接，在软链接移动之后就会失效，无法访问。这一点和`Windows`快捷方式不同，`Windows`快捷方式随便放哪里都行。
> 
> 失效的软链接
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  c.txt.s  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# mv c.txt.s tempDir
> [root@haibara OperatingSystem]# ls tempDir
> a_copy.txt  a.txt  b.txt  c.txt.s
> ```
> 所以，创建软链接最好使用绝对路径，移动后，绝对路径创建的软链接不会失效
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# ln -s /home/OperatingSystem/c.txt c.txt.s
> [root@haibara OperatingSystem]# ls
> c.txt  c.txt.s  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# mv c.txt.s tempDir
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# ls tempDir
> a_copy.txt  a.txt  b.txt  c.txt.s
> [root@haibara OperatingSystem]# cat tempDir/c.txt.s 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> [root@haibara OperatingSystem]# ll -a tempDir
> total 8
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 .
> drwxr-xr-x 5 root root 4096 Aug  3 19:54 ..
> -rw-r--r-- 1 root root    0 Aug  3 19:40 a_copy.txt
> -rw-r--r-- 1 root root    0 Aug  3 19:38 a.txt
> -rw-r--r-- 1 root root    0 Aug  3 19:39 b.txt
> lrwxrwxrwx 1 root root   27 Aug  3 19:54 c.txt.s -> /home/OperatingSystem/c.txt
> ```
> 注意，软链接的权限指的是这个软链接本身的权限，不是软链接指向文件的权限

2. `ln file file.h`创建一个硬链接
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# ln c.txt c.txt.s
> [root@haibara OperatingSystem]# ll -a
> total 28
> drwxr-xr-x   5 root root 4096 Aug  3 19:55 .
> drwxr-xr-x. 11 root root 4096 Aug  3 19:38 ..
> -rw-r--r--   2 root root  217 Aug  3 19:45 c.txt
> -rw-r--r--   2 root root  217 Aug  3 19:45 c.txt.s
> drwxr-xr-x   2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x   3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x   3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```
> 创建硬链接后，文件的硬链接计数 +1
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# ln c.txt c.txt.s
> [root@haibara OperatingSystem]# ll -a
> total 28
> drwxr-xr-x   5 root root 4096 Aug  3 19:55 .
> drwxr-xr-x. 11 root root 4096 Aug  3 19:38 ..
> -rw-r--r--   2 root root  217 Aug  3 19:45 c.txt
> -rw-r--r--   2 root root  217 Aug  3 19:45 c.txt.s
> drwxr-xr-x   2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x   3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x   3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```
> 再创建一个硬链接
> ```shell
> [root@haibara OperatingSystem]# ln c.txt.s c.txt2.s
> [root@haibara OperatingSystem]# ll -a
> total 32
> drwxr-xr-x   5 root root 4096 Aug  3 19:56 .
> drwxr-xr-x. 11 root root 4096 Aug  3 19:38 ..
> -rw-r--r--   3 root root  217 Aug  3 19:45 c.txt
> -rw-r--r--   3 root root  217 Aug  3 19:45 
> -rw-r--r--   3 root root  217 Aug  3 19:45 c.txt.s
> drwxr-xr-x   2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x   3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x   3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```
> 这里对于`c.txt`，有 2 个硬链接`c.txt.s`和`c.txt2.s`，无论更改哪个硬链接或者文件本身，这三个文件的变化同步
> ```shell
> [root@haibara OperatingSystem]# cat c.txt
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> [root@haibara OperatingSystem]# cat c.txt.s 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> [root@haibara OperatingSystem]# cat c.txt2.s 
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> [root@haibara OperatingSystem]# vim c.txt2.s 
> [root@haibara OperatingSystem]# cat c.txt
> 这是第一行
> 这是第二行
> 这是第三行
> 这是第四行
> 这是第五行
> 这是第六行
> 这是第七行
> 这是第八行
> 这是第九行
> 这是第十行
> 这是第十一行
> 这是第十二行
> 这是第十三行
> 这是第十四行
> ```
> 产生这种同步变化的原因
> 
> ![Inode](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040105869.png)
> 
> 可以看到文件和硬链接的`Inode`是相同的，每个文件都有唯一的`Inode`，直观理解起来就像洗佳佳里面的引用，对于同一个文件，无论有多少引用，在访问时，都是这个文件，所以修改就是同步的。
> 
> 当删除一个硬链接时，文件的硬链接计数 -1，当这个计数减为 0 时，才会删除这个文件
> ```shell
> [root@haibara OperatingSystem]# ll
> total 24
> -rw-r--r-- 3 root root  236 Aug  3 19:57 c.txt
> -rw-r--r-- 3 root root  236 Aug  3 19:57 c.txt2.s
> -rw-r--r-- 3 root root  236 Aug  3 19:57 c.txt.s
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> [root@haibara OperatingSystem]# rm c.txt2.s 
> rm: remove regular file 'c.txt2.s'? y 
> [root@haibara OperatingSystem]# ll
> total 20
> -rw-r--r-- 2 root root  236 Aug  3 19:57 c.txt
> -rw-r--r-- 2 root root  236 Aug  3 19:57 c.txt.s
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```
> 即使删除硬链接指向的文件，也只会让硬链接计数-1


## 06P 创建修改用户和用户组

1. `whoami`查看当前用户
> ```shell
> [root@haibara OperatingSystem]# whoami
> root
> ```

2. `chmod`修改权限操作

> 第一种，文字设定法
> ```
> chmod [who] [+|-|=] [mode] filename
> 
> 操作对象 who 可以是下述字母中的任一个或者它们的组合
> u 表示”用户(user)”，即文件或目录的所有者
> g 表示”同组(group)用户”，即与文件所有者有相同组 ID 的所有用户
> o 表示”其他(others)用户”
> a 表示”所有(all)用户”，它是系统默认值
> 
> 操作符号可以是：
> + 添加某个权限
> - 取消某个权限
> = 赋予给定权限并取消其他所有权限（如果有的话）
> ```
> 如下所示，给`c.txt`文件添加执行权限
> ```shell
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 root root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> [root@haibara OperatingSystem]# chmod u+x c.txt 
> [root@haibara OperatingSystem]# ll
> total 16
> -rwxr--r-- 1 root root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```
> 
> 第二种，数字设定法
> ```
> chmod 操作码 filename 直接用操作码修改文件权限
> 对于 file2 的权限
> -rw-rw-r—
> 421421421
> 三个组的权限都用二进制编号，比如要设置当前用户对文件的读写和执行权限，则当前用户的操作权
> 限为 4（读）+ 2（写）+ 1（执行） = 7
> 用户组和其他用户的权限设置也是一样的
> ```
> 
> 对于`c.txt`的权限`-rw-r--r--`我们设置如下：
> 
> 所有者 `rw-` = 6
> 
> 所有者所在组 `rw-` = 6
> 
> 其他用户 `r--` = 4
> 
> 操作码就是 644
> 
> ```shell
> [root@haibara OperatingSystem]# ll
> total 16
> -rwxr--r-- 1 root root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> [root@haibara OperatingSystem]# chmod 644 c.txt 
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 root root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```

3. `sudo adduser newusername`添加新用户
> ```shell
> [root@haibara OperatingSystem]# adduser tempUser
> ```

4. `chown username filename`修改文件所有者
> ```shell
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 root root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> [root@haibara OperatingSystem]# chown tempUser c.txt 
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 tempUser root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root     root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root     root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root     root 4096 Aug  3 19:43 tempDirCopy2
> ```

5. `su username`切换当前用户为`username`
> ```shell
> [root@haibara OperatingSystem]# su root
> [root@haibara OperatingSystem]# su tempUser
> [tempUser@haibara OperatingSystem]$ su root
> Password: 
> ```

6. `sudo groupadd groupname`添加新的用户组
> ```shell
> [root@haibara OperatingSystem]# groupadd tempGroup
> ```

7. `sudo chgrp groupname filename`修改文件所属用户组
> ```shell
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 tempUser root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root     root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root     root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root     root 4096 Aug  3 19:43 tempDirCopy2
> [root@haibara OperatingSystem]# chgrp tempGroup c.txt 
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 tempUser tempGroup  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root     root      4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root     root      4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root     root      4096 Aug  3 19:43 tempDirCopy2
> ```

8. `sudo chown username:groupname filename`同时修改文件所属用户和用户组
> ```shell
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 tempUser tempGroup  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root     root      4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root     root      4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root     root      4096 Aug  3 19:43 tempDirCopy2
> [root@haibara OperatingSystem]# chown root:root c.txt 
> [root@haibara OperatingSystem]# ll
> total 16
> -rw-r--r-- 1 root root  236 Aug  3 19:57 c.txt
> drwxr-xr-x 2 root root 4096 Aug  3 19:54 tempDir
> drwxr-xr-x 3 root root 4096 Aug  3 19:42 tempDirCopy1
> drwxr-xr-x 3 root root 4096 Aug  3 19:43 tempDirCopy2
> ```

9. `sudo userdel username`删除用户
> ```shell
> [root@haibara OperatingSystem]# userdel  tempUser 
> ```

10. `sudo groupdel groupname`删除用户组
> ```shell
> [root@haibara OperatingSystem]# groupdel tempGroup 
> ```

## 07P `find`命令1

1. `find`命令：找文件

> `-type`按文件类型搜索 `d/p/s/c/b/l/`
> ```shell
> [root@haibara OperatingSystem]# find ./ -type d
> ./
> ./tempDirCopy1
> ./tempDirCopy1/tempDir
> ./tempDirCopy2
> ./tempDirCopy2/tempDir
> ./tempDir
> ```
> 
> `-name`按文件名搜索
> ```shell
> [root@haibara OperatingSystem]# find ./ -name '*.txt'
> ./tempDirCopy1/tempDir/a.txt
> ./tempDirCopy1/tempDir/b.txt
> ./tempDirCopy1/tempDir/c.txt
> ./tempDirCopy1/tempDir/a_copy.txt
> ./tempDirCopy2/tempDir/a.txt
> ./tempDirCopy2/tempDir/b.txt
> ./tempDirCopy2/tempDir/c.txt
> ./tempDirCopy2/tempDir/a_copy.txt
> ./tempDir/a.txt
> ./tempDir/b.txt
> ./tempDir/a_copy.txt
> ./c.txt
> ```
> 
> `-maxdepth`指定搜索深度，应作为第一个参数出现
> ```shell
> [root@haibara OperatingSystem]# find ./ -maxdepth 1 -name '*.txt'
> ./c.txt
> [root@haibara OperatingSystem]# find ./ -maxdepth 2 -name '*.txt'
> ./tempDir/a.txt
> ./tempDir/b.txt
> ./tempDir/a_copy.txt
> ./c.txt
> ```
> 
> `-size`按文件大小搜索，单位：`k、M、G`
> ```shell
> [root@haibara OperatingSystem]# cd /bin/
> [root@haibara bin]# find ./ -size +10M -size -20M
> ./runc
> [root@haibara bin]# ll ./runc
> -rwxr-xr-x 1 root root 13773648 May 23 04:15 ./runc
> ```
> 这里要注意，两个`size`一个都不能少，还有就是文件大小单位对大小写敏感
> 
> 按照时间搜索    `-atime、mtime、ctime`天    `-amin、mmin、cmin`分钟
> ```
> a 表示最近访问时间
> m 表示最近更改时间，指更改文件属性一类的
> c 表示最近改动时间，指更改文件内容
> ```

## 08P 午后复习

## 09P `find`命令2

> 1. `-exec`：将`find`搜索的结果集执行某一指定命令
> ```shell
> [root@haibara OperatingSystem]# find ./ -name '*.txt' -exec ls -l {} \;
> -rw-r--r-- 1 root root 0 Aug  3 19:38 ./tempDirCopy1/tempDir/a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:39 ./tempDirCopy1/tempDir/b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 ./tempDirCopy1/tempDir/c.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 ./tempDirCopy1/tempDir/a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 ./tempDirCopy2/tempDir/a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 ./tempDirCopy2/tempDir/b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 ./tempDirCopy2/tempDir/c.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:43 ./tempDirCopy2/tempDir/a_copy.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:38 ./tempDir/a.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:39 ./tempDir/b.txt
> -rw-r--r-- 1 root root 0 Aug  3 19:40 ./tempDir/a_copy.txt
> -rw-r--r-- 1 root root 236 Aug  3 19:57 ./c.txt
> ```

2. `-ok`: 以交互式的方式 将`find`搜索的结果集执行某一指定命令
> ```shell
> [root@haibara OperatingSystem]# find ./ -maxdepth 2 -name '*.txt' -ok ls -l {} \;
> < ls ... ./tempDir/a.txt > ? y
> -rw-r--r-- 1 root root 0 Aug  3 19:38 ./tempDir/a.txt
> < ls ... ./tempDir/b.txt > ? y
> -rw-r--r-- 1 root root 0 Aug  3 19:39 ./tempDir/b.txt
> < ls ... ./tempDir/a_copy.txt > ? y
> -rw-r--r-- 1 root root 0 Aug  3 19:40 ./tempDir/a_copy.txt
> < ls ... ./c.txt > ? y
> -rw-r--r-- 1 root root 236 Aug  3 19:57 ./c.txt
> ```

## 10P `grep`和`xargs`

> 1. `grep`命令：找文件内容
> ```shell
> [root@haibara OperatingSystem]# grep -r '第四行' ./ -n
> ./tempDir/c.txt:4:这是第四行
> ./c.txt:4:这是第四行
> [root@haibara OperatingSystem]# grep -r '第四行' ./ 
> ./tempDir/c.txt:这是第四行
> ./c.txt:这是第四行
> ```
> `-n`参数：显示行号

2. `ps`监控后台进程工作情况，默认只显示当前可以和用户交互的进程
> ```shell
> [root@haibara OperatingSystem]# ps
>     PID TTY          TIME CMD
>    1898 pts/0    01:07:38 minio
>  412692 pts/0    00:00:00 bash
>  413654 pts/0    00:00:00 su
>  413655 pts/0    00:00:00 bash
>  413679 pts/0    00:00:00 su
>  413708 pts/0    00:00:00 su
>  413711 pts/0    00:00:00 bash
>  440616 pts/0    00:00:00 su
>  440617 pts/0    00:00:00 bash
>  440918 pts/0    00:00:00 ps
> ```

3. `ps aux | grep 'cupsd'` 检索进程结果集
> ```shell
> [root@haibara OperatingSystem]# ps aux | grep kernel
> root      440923  0.0  0.0  12144  1176 pts/0    S+   20:24   0:00 grep --color=auto kernel
> ```
> 使用`grep`搜索进程，有一条结果是搜索进程本身

4. `find … | xargs ls -l`
> ```shell
> [root@haibara OperatingSystem]# ls
> c.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# find ./ -maxdepth 1 -name '*.txt'| xargs ls -l
> -rw-r--r-- 1 root root 236 Aug  3 19:57 ./c.txt
> [root@haibara OperatingSystem]# find ./ -maxdepth 2 -name '*.txt'| xargs ls -l
> -rw-r--r-- 1 root root 236 Aug  3 19:57 ./c.txt
> -rw-r--r-- 1 root root   0 Aug  3 19:40 ./tempDir/a_copy.txt
> -rw-r--r-- 1 root root   0 Aug  3 19:38 ./tempDir/a.txt
> -rw-r--r-- 1 root root   0 Aug  3 19:39 ./tempDir/b.txt
> -rw-r--r-- 1 root root 236 Aug  3 20:23 ./tempDir/c.txt
> ```
> 对`find`操作的结果集进行操作等价于`find … -exec ls -l {} \；`两者差别在于当结果集合很大的时候，`xargs`会对结果进行分段处理，所以性能好些，但`xargs`也有缺陷，`xargs`默认用空格来分割结果集，当文件名有空格的时候，会因为文件名被切割失效
> 
> `-xargs`：将`find`搜索的结果集执行某一指定命令，当结果集数量过大时，可以分片映射

5. 创建名字带空格的文件方法

>    ![创建名字带空格的文件方法](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040142528.png)


6. `xargs`缺陷演示

>    ![xargs 缺陷演示](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040143116.png)


## 11P `xargs`加强和`awk`说明

## 12P 软件包安装

1. `sudo yum install softname`安装软件
> ```shell
> [root@haibara OperatingSystem]# yum install tree
> Last metadata expiration check: 1:10:25 ago on Sat 03 Aug 2024 07:39:02 PM CST.
> Package tree-1.7.0-15.0.1.an8.x86_64 is already installed.
> Dependencies resolved.
> Nothing to do.
> Complete!
> ```

2. `sudo yum update`更新软件列表

3. 更换软件源：系统设置->软件和更新->下载自…    
    换软件源过后要更新软件列表

4. `sudo yum remove softname` 卸载软件

5. 使用安装包进行软件安装

>    ![使用安装包进行软件安装](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040153341.png)


## 13P 压缩命令`gzip`和`bzip2`

> 两者都是配合`tar`打包命令使用这两个压缩的缺陷都是只能对单个文件进行压缩，一来不能压目录，二来不能打包
> 
> 第一种压缩方式：`gzip`
> 
> `tar zcvf` 要生成的压缩包名 压缩材料，这里压缩包名一般以`.tar.gz`结尾
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tar zcvf sum.tar.gz a.txt b.txt c.txt d.txt 
> a.txt
> b.txt
> c.txt
> d.txt
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> ```
> 上述命令实际上执行了两步，一个是`gzip`进行压缩`gzip filename`
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# gzip a.txt 
> [root@haibara OperatingSystem]# ls
> a.txt.gz  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> ```
> 解压`gunzip zipfile`
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# gunzip a.txt.gz 
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> ```
> 
> 另一个是打包命令`tar file… tarname`
> 
> 所以`tar zcvf`是两条指令的结合版本，对`zcvf`进行解释
> ```
> z:zip，压缩
> c:create，创建
> v:vision，显示压缩过程，可以去掉，直接用 zcf，但这样不显示压缩过程
> f:file，文件
> ```
> 
> `file filename`查看文件来源
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  a.txt.tar.gz  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# file a.txt.tar.gz 
> a.txt.tar.gz: POSIX tar archive (GNU)
> [root@haibara OperatingSystem]# ls
> a.txt  a.txt.tar.gz  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# file sum.tar.gz 
> sum.tar.gz: gzip compressed data, last modified: Sat Aug  3 14:23:11 2024, from Unix, original size 10240
> ```
> 
> 第二种压缩方式：使用`bzip2`方式压缩
> 
> `tar jcvf` 要生成的压缩包名 压缩材料
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tar -jcvf sum2.tar.gz a.txt b.txt c.txt d.txt 
> a.txt
> b.txt
> c.txt
> d.txt
> [root@haibara OperatingSystem]# file sum2.tar.gz 
> sum2.tar.gz: bzip2 compressed data, block size = 900k
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum2.tar.gz  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> ```
> 
> 解压：将压缩命令中的`c --> x`
> 
> `tar zxvf`压缩材料 使用`gzip`解压
> 
> `tar jxvf`压缩材料 使用`bzip2`解压
> ```shell
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum2.tar.gz  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tar -zxvf sum.tar.gz 
> a.txt
> b.txt
> c.txt
> d.txt
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum2.tar.gz  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> [root@haibara OperatingSystem]# tar -jxvf sum2.tar.gz
> a.txt
> b.txt
> c.txt
> d.txt
> [root@haibara OperatingSystem]# ls
> a.txt  b.txt  c.txt  d.txt  sum2.tar.gz  sum.tar.gz  tempDir  tempDirCopy1  tempDirCopy2
> ```

## 14P `rar`压缩和`zip`压缩

1. `rar`压缩

> 需要安装`rar`
> 
> ![安装 rar](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040210089.png)
> 
> `rar a -r newdir dir`打包，把`dir`压缩成`newdir.rar`，如果压缩材料里没有目录，`-r`参数可以省去
> 
> ![rar 压缩](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040210066.png)
> 
> `unrar x newdir.rar`解压`rar`文件
> 
> ![解压 rar 文件](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040233198.png)

2. `zip`压缩：`zip -r dir.zip dir`

> ![zip 压缩](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040232017.png)
>
> `zip`解压`unzip dir.zip`
>
> ![zip 解压](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408040230128.png)
> `zip`文件在`Windows`和`Linux`下通用

## 15P 其他命令

1. `who`查看当前在线上的用户情况
```shell
[root@haibara OperatingSystem]# who
root     tty1         2024-07-05 21:54
root     pts/0        2024-08-05 18:36 (171.105.33.155)
root     pts/1        2024-08-05 19:21 (171.105.33.155)
```


2. `whoami`查看当前用户，不带有进程
```shell
[root@haibara OperatingSystem]# whoami
root
```

3. `ps aux | grep 条件` 结果至少有一个，就是当前查询进程
```shell
[root@haibara OperatingSystem]# ps aux | grep kernel
root      520588  0.0  0.0  12216  1188 pts/1    S+   19:22   0:00 grep --color=auto kernel
```

4. `jobs`查看操作系统当前运行了哪些用户作业
```shell
[root@haibara OperatingSystem]# cat
123  
123
^C
[root@haibara OperatingSystem]# cat &
[1] 523028
[root@haibara OperatingSystem]# jobs
[1]+  Stopped                 cat
[root@haibara OperatingSystem]# 
```

5. `kill`杀死进程

在一个会话窗口中编写这样的代码，执行，此时`main.app`程序会阻塞
```shell
[root@haibara OperatingSystem]# ls
main.app  main.cpp
[root@haibara OperatingSystem]# cat main.cpp
#include <iostream>
using namespace std;

void myPrint(int i)
{
    if (i % 2 == 1) 
    {
        cout << "this turn i = " << i << endl;
    }
}

void fun2()
{
    cout << "in fun2 start" << endl;
    cout << "in fun2 end" << endl;
}

void fun1()
{
    cout << "in fun1 start" << endl;
    fun2();
    cout << "in fun1 end" << endl;
}

int main()
{
    cout << "in main start" << endl;

    for (int i = 0; i < 10; i++)
    {
        myPrint(i);
    }
    
    fun1();

    fun2();
    
    cout << "in main end" << endl;

    while (true);

    return 0;
}
[root@haibara OperatingSystem]# ./main.app 
in main start
this turn i = 1
this turn i = 3
this turn i = 5
this turn i = 7
this turn i = 9
in fun1 start
in fun2 start
in fun2 end
in fun1 end
in fun2 start
in fun2 end
in main end
```

在另一个会话窗口中，查看进程`id`丙用`kill`杀死该进程
```shell
[root@haibara OperatingSystem]# ps aux | grep main.app
root      523062 99.6  0.1  13856  1884 pts/0    R+   21:44   0:56 ./main.app
root      523121  0.0  0.0  12216  1184 pts/4    R+   21:45   0:00 grep --color=auto main.app
[root@haibara OperatingSystem]# kill 523062
```

此时`main.app`程序被杀死
```shell
[root@haibara OperatingSystem]# ./main.app 
in main start
this turn i = 1
this turn i = 3
this turn i = 5
this turn i = 7
this turn i = 9
in fun1 start
in fun2 start
in fun2 end
in fun1 end
in fun2 start
in fun2 end
in main end
Terminated
[root@haibara OperatingSystem]# 
```

6. `env`环境变量
```shell
[root@haibara OperatingSystem]# env
LS_COLORS=rs=0:di=38;5;33:ln=38;5;51:mh=00:pi=40;38;5;11:so=38;5;13:do=38;5;5:bd=48;5;232;38;5;11:cd=48;5;232;38;5;3:or=48;5;232;38;5;9:mi=01;05;37;41:su=48;5;196;38;5;15:sg=48;5;11;38;5;16:ca=48;5;196;38;5;226:tw=48;5;10;38;5;16:ow=48;5;10;38;5;21:st=48;5;21;38;5;15:ex=38;5;40:*.tar=38;5;9:*.tgz=38;5;9:*.arc=38;5;9:*.arj=38;5;9:*.taz=38;5;9:*.lha=38;5;9:*.lz4=38;5;9:*.lzh=38;5;9:*.lzma=38;5;9:*.tlz=38;5;9:*.txz=38;5;9:*.tzo=38;5;9:*.t7z=38;5;9:*.zip=38;5;9:*.z=38;5;9:*.dz=38;5;9:*.gz=38;5;9:*.lrz=38;5;9:*.lz=38;5;9:*.lzo=38;5;9:*.xz=38;5;9:*.zst=38;5;9:*.tzst=38;5;9:*.bz2=38;5;9:*.bz=38;5;9:*.tbz=38;5;9:*.tbz2=38;5;9:*.tz=38;5;9:*.deb=38;5;9:*.rpm=38;5;9:*.jar=38;5;9:*.war=38;5;9:*.ear=38;5;9:*.sar=38;5;9:*.rar=38;5;9:*.alz=38;5;9:*.ace=38;5;9:*.zoo=38;5;9:*.cpio=38;5;9:*.7z=38;5;9:*.rz=38;5;9:*.cab=38;5;9:*.wim=38;5;9:*.swm=38;5;9:*.dwm=38;5;9:*.esd=38;5;9:*.jpg=38;5;13:*.jpeg=38;5;13:*.mjpg=38;5;13:*.mjpeg=38;5;13:*.gif=38;5;13:*.bmp=38;5;13:*.pbm=38;5;13:*.pgm=38;5;13:*.ppm=38;5;13:*.tga=38;5;13:*.xbm=38;5;13:*.xpm=38;5;13:*.tif=38;5;13:*.tiff=38;5;13:*.png=38;5;13:*.svg=38;5;13:*.svgz=38;5;13:*.mng=38;5;13:*.pcx=38;5;13:*.mov=38;5;13:*.mpg=38;5;13:*.mpeg=38;5;13:*.m2v=38;5;13:*.mkv=38;5;13:*.webm=38;5;13:*.ogm=38;5;13:*.mp4=38;5;13:*.m4v=38;5;13:*.mp4v=38;5;13:*.vob=38;5;13:*.qt=38;5;13:*.nuv=38;5;13:*.wmv=38;5;13:*.asf=38;5;13:*.rm=38;5;13:*.rmvb=38;5;13:*.flc=38;5;13:*.avi=38;5;13:*.fli=38;5;13:*.flv=38;5;13:*.gl=38;5;13:*.dl=38;5;13:*.xcf=38;5;13:*.xwd=38;5;13:*.yuv=38;5;13:*.cgm=38;5;13:*.emf=38;5;13:*.ogv=38;5;13:*.ogx=38;5;13:*.aac=38;5;45:*.au=38;5;45:*.flac=38;5;45:*.m4a=38;5;45:*.mid=38;5;45:*.midi=38;5;45:*.mka=38;5;45:*.mp3=38;5;45:*.mpc=38;5;45:*.ogg=38;5;45:*.ra=38;5;45:*.wav=38;5;45:*.oga=38;5;45:*.opus=38;5;45:*.spx=38;5;45:*.xspf=38;5;45:
SSH_CONNECTION=171.105.33.155 5409 172.28.119.15 22
LANG=en_US.UTF-8
HISTCONTROL=ignoredups
HOSTNAME=haibara
S_COLORS=auto
which_declare=declare -f
XDG_SESSION_ID=30
USER=root
PWD=/home/OperatingSystem
HOME=/root
SSH_CLIENT=171.105.33.155 5409 22
SSH_TTY=/dev/pts/1
MAIL=/var/spool/mail/root
TERM=xterm-256color
SHELL=/bin/bash
SHLVL=1
LOGNAME=root
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/0/bus
XDG_RUNTIME_DIR=/run/user/0
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
HISTSIZE=1000
LESSOPEN=||/usr/bin/lesspipe.sh %s
BASH_FUNC_which%%=() {  ( alias;
 eval ${which_declare} ) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot $@
}
OLDPWD=/root
_=/usr/bin/env
```

7. `top`文字版任务管理器
```shell
[root@haibara OperatingSystem]# top
top - 19:23:20 up 30 days, 21:29,  3 users,  load average: 0.00, 0.02, 0.00
Tasks: 119 total,   1 running, 118 sleeping,   0 stopped,   0 zombie
%Cpu(s):  3.2 us,  0.0 sy,  0.0 ni, 96.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1697.2 total,    341.0 free,    785.6 used,    570.6 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    759.0 avail Mem 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                                                                                  
      1 root      20   0  238876   9520   6352 S   0.0   0.5   0:30.70 systemd                                                                                                  
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.30 kthreadd                                                                                                 
      3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp                                                                                                   
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_par_gp                                                                                               
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 slub_flushwq                                                                                             
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_highpri                                                                              
      9 root      20   0       0      0      0 I   0.0   0.0   0:14.18 kworker/u4:0-events_unbound                                                                              
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 mm_percpu_wq                                                                                             
     11 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_tasks_rude_                                                                                          
     12 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_tasks_trace                                                                                          
     13 root      20   0       0      0      0 S   0.0   0.0   0:03.33 ksoftirqd/0                                                                                              
     14 root      20   0       0      0      0 I   0.0   0.0   5:07.34 rcu_sched                                                                                                
     15 root      rt   0       0      0      0 S   0.0   0.0   0:00.05 migration/0                                                                                              
     16 root      rt   0       0      0      0 S   0.0   0.0   0:00.40 watchdog/0                                                                                               
     17 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/0                                                                                                  
     18 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/1                                                                                                  
     19 root      rt   0       0      0      0 S   0.0   0.0   0:00.03 watchdog/1                                                                                               
     20 root      rt   0       0      0      0 S   0.0   0.0   0:00.20 migration/1                                                                                              
     21 root      20   0       0      0      0 S   0.0   0.0   0:03.29 ksoftirqd/1                                                                                              
     23 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/1:0H-events_highpri                                                                              
     25 root      20   0       0      0      0 I   0.0   0.0   0:14.49 kworker/u4:1-events_unbound                                                                              
     26 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kdevtmpfs                                                                                                
     27 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 netns                                                                                                    
     28 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kauditd                                                                                                  
     29 root      20   0       0      0      0 S   0.0   0.0   0:00.66 khungtaskd                                                                                               
     30 root      20   0       0      0      0 S   0.0   0.0   0:00.00 oom_reaper                                                                                               
     31 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 writeback                                                                                                
     32 root      20   0       0      0      0 S   0.0   0.0   0:00.09 kcompactd0                                                                                               
     33 root      25   5       0      0      0 S   0.0   0.0   0:00.00 ksmd                                                                                                     
     34 root      39  19       0      0      0 S   0.0   0.0   0:12.48 khugepaged                                                                                               
     35 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 crypto                                                                                                   
     36 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kintegrityd                                                                                              
     37 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kblockd                                                                                                  
     38 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 blkcg_punt_bio                                                                                           
     39 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 tpm_dev_wq                                                                                               
     40 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 md                                                                                                       
     41 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 edac-poller                                                                                              
     42 root      rt   0       0      0      0 S   0.0   0.0   0:00.00 watchdogd                                                                                                
     44 root       0 -20       0      0      0 I   0.0   0.0   0:05.35 kworker/0:1H-kblockd                                                                                     
     61 root      20   0       0      0      0 S   0.0   0.0   0:08.11 kswapd0                                                                                                  
    109 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kthrotld                                                                                                 
    111 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 acpi_thermal_pm                      
```

8. `sudo passwd uusername`设置用户密码

   ![设置用户密码](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408052154009.png)


9. `sudo su`切换`root`用户

   ![切换 root 用户](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408052154303.png)


10. `ifconfig`查看网卡信息
```shell
[root@haibara OperatingSystem]# ifconfig
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:5ff:fe4d:f30d  prefixlen 64  scopeid 0x20<link>
        ether 02:42:05:4d:f3:0d  txqueuelen 0  (Ethernet)
        RX packets 224499  bytes 213254057 (203.3 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 210559  bytes 99637835 (95.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.28.119.15  netmask 255.255.240.0  broadcast 172.28.127.255
        inet6 fe80::216:3eff:fe06:7205  prefixlen 64  scopeid 0x20<link>
        ether 00:16:3e:06:72:05  txqueuelen 1000  (Ethernet)
        RX packets 4516631  bytes 3880003027 (3.6 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 2678622  bytes 1105683323 (1.0 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth8f7e0d8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::a8be:c8ff:feb0:c587  prefixlen 64  scopeid 0x20<link>
        ether aa:be:c8:b0:c5:87  txqueuelen 0  (Ethernet)
        RX packets 5473  bytes 684137 (668.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7130  bytes 652161 (636.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth96f5668: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::24d6:4aff:feb6:1416  prefixlen 64  scopeid 0x20<link>
        ether 26:d6:4a:b6:14:16  txqueuelen 0  (Ethernet)
        RX packets 106647  bytes 22815626 (21.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 115395  bytes 91810696 (87.5 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethaf6078f: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::3c84:c8ff:fe83:c0ad  prefixlen 64  scopeid 0x20<link>
        ether 3e:84:c8:83:c0:ad  txqueuelen 0  (Ethernet)
        RX packets 95156  bytes 191008598 (182.1 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 77376  bytes 5973480 (5.6 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

11. `man name`系统参考手册查看`name`
```shell
[root@haibara OperatingSystem]# man fork
```

12. `man n name`在系统手册第`n`章查看`name`
```shell
[root@haibara OperatingSystem]# man 2 fork
```

13. `alias 别名='指令'`给命令起别名
```shell
[root@haibara OperatingSystem]# alias pg='ps aux | grep'
[root@haibara OperatingSystem]# pg kernal
root      520659  0.0  0.0  12216  1188 pts/1    S+   19:24   0:00 grep --color=auto kernal
```

## 16P 总结
```
Linux 系统： “所见皆文件”

Linux 系统目录：
bin：存放二进制可执行文件
boot：存放开机启动程序
dev：存放设备文件： 字符设备、块设备
home：存放普通用户
etc：用户信息和系统配置文件 passwd、group
lib：库文件：libc.so.6
root：管理员宿主目录（家目录）
usr：用户资源管理目录
Linux 系统文件类型： 7/8 种
普通文件：-
目录文件：d
字符设备文件：c
块设备文件：b
软连接：l
管道文件：p
套接字：s
未知文件。

软连接：快捷方式
为保证软连接可以任意搬移， 创建时务必对源文件使用 绝对路径。

硬链接：
ln file file.hard
操作系统给每一个文件赋予唯一的 inode，当有相同 inode 的文件存在时，彼此同步。
删除时，只将硬链接计数减一。减为 0 时，inode 被释放。

创建用户：
sudo adduser 新用户名 --- useradd

修改文件所属用户：
sudo chown 新用户名 待修改文件。
sudo chown wangwu a.c

删除用户：
sudo deluser 用户名

创建用户组：
sudo addgroup 新组名

修改文件所属用户组：
sudo chgrp 新用户组名 待修改文件。
sudo chgrp g88 a.c

删除组：
sudo delgroup 用户组名

使用 chown 一次修改所有者和所属组：
sudo chown 所有者：所属组 待操作文件。

find 命令：找文件
-type 按文件类型搜索 d/p/s/c/b/l/ f:文件
-name 按文件名搜索
find ./ -name "*file*.jpg"
-maxdepth 指定搜索深度。应作为第一个参数出现。
find ./ -maxdepth 1 -name "*file*.jpg"
-size 按文件大小搜索. 单位：k、M、G
find /home/itcast -size +20M -size -50M
-atime、mtime、ctime 天 amin、mmin、cmin 分钟。

-exec：将 find 搜索的结果集执行某一指定命令。
find /usr/ -name '*tmp*' -exec ls -ld {} \;
-ok: 以交互式的方式 将 find 搜索的结果集执行某一指定命令

-xargs：将 find 搜索的结果集执行某一指定命令。 当结果集数量过大时，可以分片映射。
find /usr/ -name '*tmp*' | xargs ls -ld 
-print0：
find /usr/ -name '*tmp*' -print0 | xargs -0 ls -ld 

grep 命令：找文件内容
grep -r 'copy' ./ -n
-n 参数：:显示行号

ps aux | grep 'cupsd' -- 检索进程结果集。

软件安装：
1. 联网
2. 更新软件资源列表到本地。 sudo apt-get update
3. 安装 sudo apt-get install 软件名
4. 卸载 sudo apt-get remove 软件名
5. 使用软件包（.deb） 安装： sudo dpkg -i 安装包名。

tar 压缩：
1. tar -zcvf 要生成的压缩包名 压缩材料。
tar zcvf test.tar.gz file1 dir2 使用 gzip 方式压缩。
tar jcvf test.tar.gz file1 dir2 使用 bzip2 方式压缩。

tar 解压：
将 压缩命令中的 c --> x
tar zxvf test.tar.gz 使用 gzip 方式解压缩。
tar jxvf test.tar.gz 使用 bzip2 方式解压缩。

rar 压缩：
rar a -r 压缩包名（带.rar 后缀） 压缩材料。
rar a -r testrar.rar stdio.h test2.mp3

rar 解压：
unrar x 压缩包名（带.rar 后缀）

zip 压缩：
zip -r 压缩包名（带.zip 后缀） 压缩材料。
zip -r testzip.zip dir stdio.h test2.mp3

zip 解压：
unzip 压缩包名（带.zip 后缀）
unzip testzip.zip

创建一个目录，大小默认是 4096k
```

## 17P 复习

## 18P `vim`的三种工作模式

![vim 的三种工作模式](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408052159828.png)

## 19P `vim`基本操作-跳转和删字符
```
i 进入编辑模式，光标前插入字符
a 进入编辑模式，光标后插入字符
o 进入编辑模式，光标所在行的下一行插入
I 进入编辑模式，光标所在行的行首插入
A 进入编辑模式，光标所在行的行末插入字符
O 进入编辑模式，光标所在行的上一行插入字符

s 删除光标所在字符并进入编辑模式
S 删除光标所在行并进入编辑模式
x 删除光标所在字符，工作模式不变
dw 删除光标所在单词，要求光标在首字母上，如果不在首字母，只会删除当前位置到单词末，工作模式不变
D 删除光标所在位置到行末，工作模式不变
0(数字) 光标移到行首，工作模式不变
$ 光标移到行尾，工作模式不变
d0 删除光标所在位置到行首，工作模式不变
d$ 删除光标所在位置到行末，工作模式不变

命令模式下的光标移动
h 左移
j 下移
k 上移
l 右移

命令模式下行跳转
line-G 缺点是没有回显

末行模式下行跳转
:line-回车

跳转首行
gg （命令模式）
跳转末行
G （命令模式）

自动缩进
在这之前要进行 vimrc 修改，不然自动缩进是 8 个空格
ubuntu 的 vimrc 位置在/etc/vim/vimrc
在文件末尾添加三行：
set tabstop=4 //设置制表符宽度为 4
set softtabstop=4 // 设置软制表符宽度为 4
set shiftwidth=4 // 设置缩进空格数为 4
```

## 20P `vim`基本操作-删除
```
替换单个字符：
r 命令模式下替换光标选中字符

一段删除，即删除指定区域：
光标选中要删除的首字符，按 v 进入可视模式，再使用 hjkl 移动到要删除的末尾，按 d 删除

删除整行：
dd，剪切光标所在行
n+dd，剪切从光标开始的 n 行
```

## 21P `vim`基本操作-复制粘贴
```
yy 复制光标所在行

p 向后粘贴剪切板内容，如果复制整行，这里是粘贴在光标所在位置的下一行

P 向前粘贴剪切板内容，如果是整行，这里是粘贴在光标所在位置的上一行

p 和 P 粘贴会出现换行，主要原因是复制整行时，会把行末的换行符也复制下来。

n-yy 复制光标所在位置的 n 行，包括光标所在行
```

## 22p `vim`基本操作-查找和替换
```
查找
/+findname 命令模式下查找
按回车键启动查找后，按 n，会自动找下一个，N 跳到上一个
查找光标所在单词
光标在目标单词上时，*或者#查找下一个，这里不要求光标必须在首字母上

替换：末行模式下进行
单行替换
光标置于待替换行， :s /待替换词/替换词
全文替换
:%s /待替换词/替换词 这个默认替换每行的首个，一行有多个目标词时，后面的不会变
:%s /待替换词/替换词/g 真正意义上的全局替换
区域替换
:24,35s /待替换词/替换词/g 替换 24-35 行之间的目标词
末行模式下历史命令
Ctrl-p 上一条命令
Ctrl-n 下一条命令
```

## 23P `vim`基本操作-其他
```
命令模式下
u 撤销操作
Ctrl-r 反撤销

分屏，末行模式下
:sp 水平分屏
:vsp 竖直分屏
分屏命令+filename，分屏并打开这个文件
分屏后屏幕切换，Ctrl-w-w
使用:q 退出光标所在窗口
使用:qall 退出所有窗口

从 vim 中跳转 manpage，命令模式下
将光标放在待查看单词上，按 K，默认看第一卷
n+K，查看第 n 卷

查看宏定义：命令模式
光标放在待查看词上，[+d 即可查看

vim 下使用 shell 命令：末行模式
:! + 命令
操作后，会切换至终端显示结果，出现如下画面，按 Enter 后回到 vim 界面
```

## 24P `vim`配置思路
```
两个 vim 配置文件
1. /etc/vim/vimrc
2. ~/.vimrc
其中，第二个配置文件会优先加载，属于用户配置
```

## 25P `gcc`编译 4 步骤

![gcc 编译4步骤](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408052208615.png)


## 26P `gcc`编译常用参数

当头文件和源码不在一个目录下时，需要指定头文件

下面是头文件和源码在同一个目录下
```shell
[root@haibara OperatingSystem]# vim hello.h
[root@haibara OperatingSystem]# vim hello.c
[root@haibara OperatingSystem]# gcc hello.c -o hello.out
[root@haibara OperatingSystem]# ls
HeadDir  hello.out  hello.c  hello.h
[root@haibara OperatingSystem]# ./hello.out
hello world
```
将`hello.h`放入新建的文件夹`headDir`之后，编译会失败
```shell
[root@haibara OperatingSystem]# tree
.
├── HeadDir
│   └── hello.h
└── hello.c

1 directory, 2 files
[root@haibara OperatingSystem]# g++ main.cpp -o main.out
g++: error: main.cpp: No such file or directory
g++: fatal error: no input files
compilation terminated.
```
`-I`参数指定头文件所在位置，位置可以在编译文件前，也可以在后面
```shell
[root@haibara OperatingSystem]# tree
.
├── HeadDir
│   └── hello.h
└── hello.c

1 directory, 2 files
[root@haibara OperatingSystem]# gcc hello.c -o hello.out -I ./HeadDir/
[root@haibara OperatingSystem]# ls
HeadDir  hello.out  hello.c
[root@haibara OperatingSystem]# ./hello.out
hello world
```
部分参数如下
```
-I 指定头文件所在目录位置
-c 只做预处理，编译，汇编。得到二进制文件
-g 编译时添加调试文件，用于 gdb 调试
-Wall 显示所有警告信息
-D 向程序中“动态”注册宏定义
-l 指定动态库库名
-L 指定动态库路径
```

## 27P 午后复习

## 28P 动态库和静态库理论对比

![动态库和静态库理论对比](https://moyi-image.oss-cn-guangzhou.aliyuncs.com/img02/202408052215276.png)

## 29P 静态库制作

静态库名字以`lib`开头，以`.a`结尾
例如：`libmylib.a`

静态库生成指令
`ar rcs libmylib.a file1.o`

步骤一：写好源代码
```shell
[root@haibara OperatingSystem]# ls
add.c  mul.c  sub.c
[root@haibara OperatingSystem]# cat add.c 
int add(int a, int b) 
{
    return a + b;
}
[root@haibara OperatingSystem]# cat sub.c 
int sub(int a, int b)
{
    return a - b;
}
[root@haibara OperatingSystem]# cat mul.c 
int mul(int a, int b)
{
    return a * b;
}
```

步骤二：编译源代码生成`.o`文件
```shell
[root@haibara OperatingSystem]# ls
add.c  main.c  mul.c  sub.c
[root@haibara OperatingSystem]# gcc -c add.c -o add.o
[root@haibara OperatingSystem]# gcc -c sub.c -o sub.o
[root@haibara OperatingSystem]# gcc -c mul.c -o mul.o
[root@haibara OperatingSystem]# ls
add.c  add.o  main.c  mul.c  mul.o  sub.c  sub.o
```

步骤三：制作静态库`ar rcs libname.a file1.o file2.o …`
```shell
[root@haibara OperatingSystem]# ls
add.c  add.o  main.c  mul.c  mul.o  sub.c  sub.o
[root@haibara OperatingSystem]# ar rsc libmath.a add.o sub.o mul.o
[root@haibara OperatingSystem]# ls
add.c  add.o  libmath.a  main.c  mul.c  mul.o  sub.c  sub.o
```

静态库的使用：`gcc main.c lib 库名.a -o main.out`
```shell
[root@haibara OperatingSystem]# ls
add.c  add.o  libmath.a  main.app  main.c  mul.c  mul.o  sub.c  sub.o
[root@haibara OperatingSystem]# gcc main.c libmath.a -o main.out
main.c: In function ‘main’:
main.c:7:36: warning: implicit declaration of function ‘add’ [-Wimplicit-function-declaration]
     printf("%d + %d = %d\n", a, b, add(a, b));
                                    ^~~
main.c:8:36: warning: implicit declaration of function ‘sub’ [-Wimplicit-function-declaration]
     printf("%d - %d = %d\n", a, b, sub(a, b));
                                    ^~~
main.c:9:36: warning: implicit declaration of function ‘mul’ [-Wimplicit-function-declaration]
     printf("%d * %d = %d\n", a, b, mul(a, b));
                                    ^~~
[root@haibara OperatingSystem]# ./main.out
10 + 20 = 30
10 - 20 = -10
10 * 20 = 200
```
上面代码中，`main.c`直接使用了`mymath`库中的`add sub mul`函数，所以在编译时要导入静态库编译时出现了函数未定义的警告，可以忽略，让系统生成默认的定义


`main.c`只有 216，然而`main.out`有 18264，所以静态库使用时，是直接编译到文件里的
```shell
[root@haibara OperatingSystem]# ll -a main.c main.out 
-rwxr-xr-x 1 root root 18264 Aug  5 19:46 main.out
-rw-r--r-- 1 root root   216 Aug  5 19:46 main.c
```

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