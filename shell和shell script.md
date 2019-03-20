# shell和shell script

## Shell

1. ### 认识shell

​    管理整个计算机硬件的其实是操作系统的内核（kernel）,这个内核是需要被保护的，所以一般用户只能通过shell来跟内核通信，以达到所想要的工作。程序从用户接口得到输入信息，shell将用户程序及其输入翻译成操作系统内核能够识别的指令，并且操作系统内核执行完将返回的输出通过shell再呈现给用户。

2. ### shell变量的显示与设置

​    利用echo这个命令来显示变量，但是变量前面必须加上字符“$”才行。当然也可以使用echo “  ”  >> filename 来创建一个新的文件。

变量的设置规则：

- 变量与变量内容以一个等号来连接，如下所以：

myname=dutertk

- 等号两边不能直接接空格符，如果必须用空格，需要使用单引号或者双引号包括

myname="duter tk"

- 双引号的特殊字符如“$”等，可以保有原本的特性，如下

var="lang is $LANG" 则echo $var输出的是lang is en_US

- 可用转义字符“\”将特殊符号变成一般字符
- 取消变量的方法为使用“unset 变量名称”的命令

3. ### 变量的有效范围

如果在跑程序的时候，有父进程与子进程的不同程序关系时，则“变量”可否被引用于**export**有关。被export后的变量，称它为环境变量。环境变量可以被子进程所引用，这是因为内存配置的原因：

- 当启动一个shell，操作系统会分配一记忆块给shell使用，此内存内的变量可以让子进程使用；
- 若在父进程利用export功能，可以让自定义变量的内容写到上述的记忆块当中（环境变量）；
- 当加载另一个shell时，子shell可以将父shell的环境变量所在的记忆块导入自己的环境变量块当中。

4. ### 变量键盘读取、数组与声明

- **read**

  read [-pt] variable

-p : 后面可以接提示符

-t ：等待的秒数

example：read  -p "Please input your name:" -t 30 named

提示用户30秒内输入自己的名字

- **declare**

  declare [-aixr] variable

-a : 将后面名为variable的变量定义为数组类型

-i ：将后面名为variable的变量定义为整数类型

-x ：定义为环境变量

-r ：定义为readonly类型，该变量不能更改，不能重设

- **array**

  数组的设置方式：var[index]=content

## Shell Script

1. ### 定义

利用shell的功能写的一个程序，使用纯文本文件，将一些shell的语法与命令写在里面，搭配正则表达式、管道命令等，达到想要的处理目的。

**注意事项：**

1. 命令的执行是从上到下、从左而右的分析与执行；
2. 命令中的空白会被忽略；
3. 如果读取到一个Enter符号，就尝试开始执行该行命令；
4. 如果某一行内容太多，则可以使用"\[Enter]"来扩展到下一行；
5. “#”可以作为批注；

**良好的编写习惯：**

- 记录script的功能
- script的版本信息
- script的作者与联络方式
- script的历史记录
- script内较特殊的命令，使用“绝对路径”的方式来执行
- script执行时需要的环境变量预先声明与设置

2. ### 简单范例

```shell
#!/bin/bash
# Program:
#  User inputs his first name and last name. Program shows his full name.
# History:
# 2019/03/20  dutertk   firstcreate
PATH=/bin:/sbin:/usr/bin:/usr/sbin:~/bin
export PATH
read -p "Please input your first name: " firstname
read -p "Please input your last name: " lastname 
echo -e "\nYour full name is: $firstname $lastname"
```

3. ### 执行方式区别

- 使用直接执行的方式来执行script

不管使用绝对路径还是相对路径，还是使用bash或者sh来执行脚本时，该script都会使用一个新的bash环境来执行脚本内的命令。也就是说使用这种执行方式时，其实script是在子进程的bash内执行的。

- 使用source来执行脚本：在父进程中执行



