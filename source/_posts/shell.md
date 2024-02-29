---
title: Shell
categories: '-计算机'
date: 2024-2-16
abbrlink: 84539df9
---
# Shell

## What is Shell

* a textual interface

*  they allow you to run programs, give them input, and inspect their output in a semi-structured way
* The most popular one: Bourne Again Shell, or Bash

## Basic 

```bash
wwwqeo@LAPTOP-QQDH3S15:~$ #this is called a prompt
#wwwqeo@LAPTOP-QQDH3S15 is the username

wwwqeo@LAPTOP-QQDH3S15:~$ date
Fri Jan  5 13:49:30 CST 2024

wwwqeo@LAPTOP-QQDH3S15:~$ echo $SHELL
/bin/bash
wwwqeo@LAPTOP-QQDH3S15:~$ echo $PATH
/home/wwwqeo/.local/bin:/usr/local/sbin
# echo means "print"
# the : seperate the listed directories in $PATH
# $PATH is the directory that bash search for the programme to run
wwwqeo@LAPTOP-QQDH3S15:~$ which echo
/usr/bin/echo
# returns the path of the program "echo"
```

## Navigating

```bash
wwwqeo@LAPTOP-QQDH3S15:~$ pwd #pwd: present work directory
/home/wwwqeo
wwwqeo@LAPTOP-QQDH3S15:~$ cd /home #cd: change directory
wwwqeo@LAPTOP-QQDH3S15:/home$ cd .. # .. is the parents dir. of pwd
wwwqeo@LAPTOP-QQDH3S15:/$ pwd
/ # / means the root directory
wwwqeo@LAPTOP-QQDH3S15:/$ cd . # . refers to pwd
wwwqeo@LAPTOP-QQDH3S15:/$ pwd
/

wwwqeo@LAPTOP-QQDH3S15:/$ ls
bin   dev  home  lib    lib64   lost+found  mnt  proc  run   snap  sys  usr
boot  etc  init  lib32  libx32  media       opt  root  sbin  srv   tmp  var
wwwqeo@LAPTOP-QQDH3S15:/$ ls --help #help of ls
Usage: ls [OPTION]... [FILE]...

wwwqeo@LAPTOP-QQDH3S15:/$  ls -l # -l use long listing format
total 2120
lrwxrwxrwx   1 root root       7 May  2  2023 bin -> usr/bin
drwxr-xr-x   2 root root    4096 Apr 18  2022 boot
drwxr-xr-x  16 root root    3540 Jan  5 13:48 dev
......
#权限      链接 所属人 所属群组 大小   修改日期    文件名 
#权限 permission eg. lrwxrwxrwx , drwxr-xr-x
#10个字符，第一位：文件类型，-文件，l链接文件，d目录，b和c都是指设备文件
#后面9位每三个rwx一组，依次是所属人、所属群组、其他所有者权限
#r~read,w~write,x~execute（可执行）,-~no permission
#链接 links:表示有多少文件名链接到这个节点（i-node)上

wwwqeo@LAPTOP-QQDH3S15:/$ man ls #open the manual of ls

wwwqeo@LAPTOP-QQDH3S15:/$ cd ~ # ~ means /home/usr (usr is the username)
wwwqeo@LAPTOP-QQDH3S15:~$ pwd
/home/wwwqeo
wwwqeo@LAPTOP-QQDH3S15:~$ mkdir the_missing_semester
#mkdir~make directory; rm~remove
wwwqeo@LAPTOP-QQDH3S15:~/the_missing_semester$ touch semester
#touch: create blanck file

```

## Connecting Programs

In the shell, programs have 2 primary "streams" (input & output).

```bash
# < input ; > output ; | pipe; >> append to the file
wwwqeo@LAPTOP-QQDH3S15:~/the_missing_semester$ echo hello > hello.txt
wwwqeo@LAPTOP-QQDH3S15:~/the_missing_semester$ cat hello.txt
hello #cat means concatenate 
wwwqeo@LAPTOP-QQDH3S15:~/the_missing_semester$ cat < hello.txt
hello
wwwqeo@LAPTOP-QQDH3S15:~/the_missing_semester$ cat < hello.txt > hello2.txt
wwwqeo@LAPTOP-QQDH3S15:~/the_missing_semester$ cat < hello2.txt
hello

#The | operator lets you “chain” programs such that the output of one is the input of another
wwwqeo@LAPTOP-QQDH3S15:~$ ls -l / | tail -n1
drwxr-xr-x  13 root root    4096 May  2  2023 var
#tail 是一个命令，用于显示文件的末尾行。
#-n1 是 tail 命令的选项，表示只显示最后一行。

wwwqeo@LAPTOP-QQDH3S15:~$ ls / |tee output.txt 
#将根目录下的文件名写入home下的output.txt中
#tee 用于从输入读取数据，并将其同时输出到标准输出和一个或多个文件中。
wwwqeo@LAPTOP-QQDH3S15:~$ ls -l / >> output.txt
#将根目录下的ls -l append到home下的output.txt中

wwwqeo@LAPTOP-QQDH3S15:~/anaconda3/lib$ ls | grep "utf" -i 
#用grep在lib的文件中搜索含"utf"的文件 
#基本语法：grep "pattern" file.txt，第二个参数可以利用pipe传入
#-i：忽略大小写。-v：只输出不匹配的行。-r：递归地搜索。-l：只输出包含匹配的文件名，而不输出匹配的行。-n：输出匹配的行以及行号。
libutf8proc.so
libutf8proc.so.2
libutf8proc.so.2.4.1
utf8_and_ascii.so
utf8_and_big5.so
...
```

## Root

```bash
#sudo "su"~super user
```



## Appendix

### words

execute 执行 concatenate链接

### Shebang

Shebang（也称为Hashbang）是在Unix和类Unix系统中用于指定脚本解释器的特殊注释行。它的作用是告诉操作系统应该使用哪个解释器来执行脚本文件。

Shebang 的格式通常是在脚本文件的第一行，以井号（#）和叹号（!）开头，后面紧跟着解释器的路径。例如，常见的Shebang 行是 `#!/bin/bash`，它指定了使用 Bash 解释器来执行脚本。

当你在终端中执行一个带有Shebang 的脚本时，操作系统会读取Shebang 行，并根据指定的解释器来执行脚本。这样，你就不需要手动指定解释器，操作系统会自动选择正确的解释器来运行脚本。

除了指定解释器的路径，Shebang 行还可以包含其他选项和参数，以便更精确地控制脚本的执行环境。

以下是一些常见的Shebang 行示例：

- `#!/bin/bash`：使用Bash解释器执行脚本。
- `#!/usr/bin/python`：使用Python解释器执行脚本。
- `#!/usr/bin/env ruby`：使用Ruby解释器执行脚本，`/usr/bin/env` 是一个用于在环境变量中查找解释器的常用工具。

使用Shebang 可以使脚本文件具有可执行权限，并且可以直接运行，而不需要显式地指定解释器。这使得脚本的使用更加方便和可移植。

### Common Commands

```
cd | Change Directory |
cp | CoPy | 
cat | CATenate | “衔接”，衔接文件并打印到规范输出设备上，cat常常用来显现文件的内容，类似于下的type指令。
diff | DIFFerence | 在最简略的情况下，比较给定的两个文件的不同。
grep | Gnu Regular Expression Print |全面查找正则表达式并把行打印出来）是一种强大的文本查找东西，它能运用正则表达式查找文本，并把匹配的行打印出来。
ls | LiSt | 
man | MANual | 
mkdir | MaKe DIRectory |
mv | MoVe | 对文件或目录重新命名，或许将文件从一个目录移到另一个目录中。
pwd | Print Working Directory | 以绝对路径的方法显现用户当前作业目录
rm | ReMove | 可以删去一个目录中的一个或多个文件或目录，也可以将某个目录及其下属的一切文件及其子目录均删去掉。关于链接文件，仅仅删去整个链接文件，而原有文件坚持不变。
rmdir | ReMove DIRectory | 用来删去空目录。
su | Substitute User | 切换当前用户身份到其他用户身份，改动时须输入所要改动的用户帐号与暗码。
sudo | SuperUser DO | 用来以其他身份来履行指令，预设的身份为root。
```



### Commands

```
作者：云叔
链接：https://www.zhihu.com/question/49073893/answer/2886417025
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

## 1. 目录缩写缩写 | 全称 | 阐明 | 
/bin | BINaries | 二进制可履行指令
/dev | DEVices | 特别设备文件
/etc | ETCetera | 系统管理和装备文件
/etc/fstab | FileSystem TABle | 文件/etc/fstab包含了静态文件系统信息，界说了存储设备和分区整合到整个系统的方法。mount 指令会读取这个文件，确认设备和分区的挂载选项。
/lib | LIBraries | 库文件
/mnt | MouNT | 系统提供这个目录是让用户临时挂载其他的文件系统。

/opt | OPTion | 第三方软件放置的目录。
/proc | PROCesses | 虚拟的目录，是系统内存的映射。可直接拜访这个目录来获取系统信息。
/sbin | Super BINaries, Superuser BINaries | 系统管理指令，这儿寄存的是系统管理员运用的管理程序
/srv | SeRVices | 是一些网络服务发动后，这些服务所需要取用的数据目录。常见的服务例如 WWW，FTP 等。
/sys | SYStem | 虚拟文件系统，主要记载与内核相关的信息，包含现在已加载的内核模块与内核检测到的硬件设备信息，同样不占硬盘容量。
/tmp | TeMPorary | 共用的临时文件存储点
/tty | teletypewriter | “电传打字机”，在类Unix里，键盘显现器，都是虚拟teletypewriter
/usr | Unix System/Software/Shared Resources | “Unix 操作系统软件资源” 所放置的目录，不是用户数据。 FHS 建议一切的软件开发者应该将他们的数据合理的放置到这个目录下的子目录，而不是自行新建该软件自己独立的目录。
/var | VARiable | 某些大文件的溢出区

## 2. 指令缩写缩写 | 全称 | 阐明|  
apt | Advanced Packaging Tool | 是Debian Linux发行版中的APT软件包管理东西。一般合作apt-get或许apt-updateawk | Aho Weiberger and Kernighan | Alfred Aho，Peter Weinberger, 和 Brian Kernighan 的Family Name的首字符。一种编程言语，用于在linux/unix下对文本和数据进行处理。
bash | Bourne Again SHell | 一种shellbg | BackGround | 用于将作业放到后台运转，使前台可以履行其他使命。该指令的运转效果与在指令后面添加符号&的效果是相同的，都是将其放到系统后台履行。
cal | CALendar | 用于显现当前日历，或许指定日期的日历。
cat | CATenate | “衔接”，衔接文件并打印到规范输出设备上，cat常常用来显现文件的内容，类似于下的type指令。
chgrp | CHange GRouP | 用来改动文件或目录所属的用户组。
chmod | CHange MODe | 用来改动文件或目录的权限。chown | CHange OWNer | 改动某个文件或目录的一切者和所属的组，该指令可以向某个用户授权，使该用户变成指定文件的一切者或许改动文件所属的组。
cd | Change Directory | 切换作业目录
cp | CoPy | 将一个或多个源文件或许目录复制到指定的意图文件或目录
dd | Data Description | 用于复制文件并对原文件的内容进行转换和格式化处理。
df | Disk Free | 用于显现磁盘分区上的可运用的磁盘空间。默许显现单位为KB。
du | Disk Usage | 查看运用空间的，但是与df指令不同的是Linux du指令是对文件和目录磁盘运用的空间的查看，还是和df指令有一些差异的。
diff | DIFFerence | 在最简略的情况下，比较给定的两个文件的不同。
dpkg | Debian PacKaGe | Debian Linux系统用来装置、创立和管理软件包的实用东西。
ed | EDitor | 单行纯文本编辑器，它有指令模式（command mode）和输入模式（input mode）两种作业模式。
emacs | Editor MACroS | 是由GNU安排的创始人Richard Stallman开发的一个功用强大的全屏文本编辑器，它支撑多种编程言语，具有许多优良的特性。(备注：vim大法好！！！)
env | ENVironment | 用于显现系统中已存在的环境变量，以及在界说的环境中履行指令。
exec | EXECute | 用于调用并履行指令的指令。
fsck | File System Consistency checK, or fuck | 用于查看而且企图修复文件系统中的错误。
gawk | Gnu Aho Weiberger and Kernighan |
grep | Gnu Regular Expression Print | （global search regular expression(RE) and print out the line，全面查找正则表达式并把行打印出来）是一种强大的文本查找东西，它能运用正则表达式查找文本，并把匹配的行打印出来。
grub | GRand Unified Bootloader | 多重引导程序grub的指令行shell东西。
ifconfig | InterFace CONFIGuration | 被用于装备和显现Linux内核中网络接口的网络参数。
init | INITialization | Linux下的进程初始化东西
insmod | INStall Module | 用于将给定的模块加载到内核中。
ln | LiNk | 用来为文件创件衔接，衔接类型分为硬衔接和符号衔接两种，默许的衔接类型是硬衔接。如果要创立符号衔接必须运用”-s”选项。
ls | LiSt | 显现方针列表
lsmod | LiSt Module | 用于显现现已加载到内核中的模块的状况信息。
man | MANual | Linux下的协助指令，通过man指令可以查看Linux中的指令协助、装备文件协助和编程协助等信息。一般戏称有问题找男人。。。
mkdir | MaKe DIRectory | 创立目录
mkfs | MaKe FileSystem | 用于在设备上（通常为硬盘）创立Linux文件系统。
mv | MoVe | 对文件或目录重新命名，或许将文件从一个目录移到另一个目录中。
nano | Nano’s ANOther editor | 是一个字符终端的文本编辑器，有点像DOS下的editor程序。
parted | PARTition EDitor | 是由GNU安排开发的一款功用强大的磁盘分区和分区大小调整东西，与fdisk不同，它支撑调整分区的大小。
passwd | PASSWorD | 用于设置用户的认证信息，包含用户暗码、暗码过期时间等。
ping | Packet InterNet Grouper | 用来测试主机之间网络的连通性。履行ping指令会运用ICMP传输协议，发出要求回应的信息，若远端主机的网络功用没有问题，就会回应该信息，因而得知该主机运作正常。
popd | POP from Directory | 删去目录栈中的记载；
pushd | PUSH to Directory | 是将目录参加指令堆叠中。
ps | Processes Status | 陈述当前系统的进程状况。可以搭配kill指令随时中断、删去不必要的程序。
pwd | Print Working Directory | 以绝对路径的方法显现用户当前作业目录
rcconf | Run Command CONFiguration | Debian Linux下的运转等级服务装备东西，用以设置在特定的运转等级下系统服务的发动装备。
rm | ReMove | 可以删去一个目录中的一个或多个文件或目录，也可以将某个目录及其下属的一切文件及其子目录均删去掉。关于链接文件，仅仅删去整个链接文件，而原有文件坚持不变。
rmdir | ReMove DIRectory | 用来删去空目录。
rmmod | ReMove MODule | 用于从当前运转的内核中移除指定的内核模块。
rpm | RPM/Redhat Package Manager | RPM软件包的管理东西。
sed | Stream EDitor | 一种流编辑器，它是文本处理中十分中的东西，可以完美的合作正则表达式运用，功用与众不同。
ssh | Secure SHell | openssh套件中的客户端衔接东西，可以给予ssh加密协议完成安全的长途登录服务器。
su | Substitute User | “替代用户”，切换当前用户身份到其他用户身份，改动时须输入所要改动的用户帐号与暗码。
sudo | SuperUser DO | 用来以其他身份来履行指令，预设的身份为root。
sync | SYNChronize | 用于强制被改动的内容马上写入磁盘，更新超块信息。
vim | vi Improved | 是UNIX操作系统和类UNIX操作系统中最通用的全屏幕纯文本编辑器。
Linux中的vi编辑器叫vim，它是vi的增强版（vi Improved），与vi编辑器彻底兼容，而且完成了许多增强功用。(备注：神相同的编辑器！！！)
yum | Yellow dog Updater, Modified | 在Fedora和RedHat以及SUSE中基于rpm的软件包管理器
## 3. 编程相关缩写缩写 | 全称 | 阐明 | — 
cc | C Compiler |
gcc | Gnu Compiler Collection | 作为一个软件集被你下载下来编译装置的时分
gcc | Gnu C Compiler | 作为一个软件被你调用来编译C程序的时分
g++ | Gnu c++ compiler | 其实g++仅仅调用gcc，然后衔接c++的库，而且作相应的一些编译设置而已
gcj | Gnu Compiler for Java |
gdb | Gnu DeBug |## 
## 4. 递归缩写缩写 | 全称 | 阐明 | — 
—GNU | Gnu is Not Unix |
PHP | PHP: Hypertext Preprocessor |
RPM | RPM Package Manager |
WINE | WINE Is Not an Emulator | Wine 是类UNIX系统下运转微软Windows程序的”兼容层”。在Wine中运转的Windows程序，就如同运转原生Linux程序相同，不会有模拟器那样的性能问题。
PNG | PNG’s Not GIF |
nano | Nano’s ANOther editor |
## 5. 其他缩写缩写 | 全称 | 阐明| — | 
tar | Tape Archive | “磁带档案卷”
tcl | Tool Command Language | Tcl（发音 tickle）是一种脚本言语。
tty | teletypewriter | “电传打字机”，在类Unix里，键盘显现器，都是虚拟的
teletypewritertzselect | Time Zone SELECT |
```



