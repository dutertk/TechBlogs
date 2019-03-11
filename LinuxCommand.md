#Linux常用命令
命令格式： 命令  【-选项】  【参数】   
如 ls     -a      /usr   
###su命令   
作用：切换用户身份   
英文：<font color="red">s</font>witch<font color="red">u</font>ser   
语法：su &nbsp; [选项] &nbsp; 用户名   
举例：su &nbsp; - &nbsp; dutertk   
-表示用户的环境变量一起切换   
###文件处理命令   
主要为CRUD   
<font size="4em">1. **cd**</font>   
英文：<font color="red">C</font>hange<font color="red">D</font>irectory   
作用：切换目录
语法：cd &nbsp; [目录]

- /切换到根目录  
- ..回到上一级目录
- .当前目录
- 显示并打开到上一次操作的目录
- ~当前用户的宿主目录   

<font size="4em">2. **ls**</font>   
英文：<font color="red">l</font>i<font color="red">s</font>t   
作用：显示目录文件
语法：ls &nbsp; [文件或者目录]   

- -a &nbsp; 显示所有文件
- -l &nbsp; 显示详细信息
- -R(recursive) &nbsp;递归显示当前目录下所有目录
- -r &nbsp; 逆序排序；
- -t &nbsp; 按修改时间排序   
  其中ll 相当于  ls &nbsp;-l  

<font size="4em">3. **touch**</font>  
作用：创建空文件或者更新已存在的文件的时间   
语法：touch &nbsp; 文件名
举例：touch &nbsp; a.txt &nbsp; b.txt &nbsp;  
touch {a.txt, b.txt}

<font size="4em">4. **cp**</font>  
英文：<font color="red">c</font>o<font color="red">p</font>y   
作用：复制文件或者目录  
语法：cp &nbsp;-[rp]&nbsp;源文件或者目录 &nbsp; 目的目录  
-r &nbsp; -R 递归处理，复制目录，即拷贝子文件夹  
-p &nbsp; 保留文件属性

<font size="4em">5. **rm**</font>  
英文：<font color="red">r</font>e<font color="red">m</font>ove   
作用：删除文件  
语法：rm &nbsp;-[rf]&nbsp;文件或者目录   
-r &nbsp; 删除目录及其下的所有文件  
-f &nbsp; 强制删除文件或者目录  


<font size="4em">6. **tail**</font>  
英文：<font color="red">tail</font>   
作用：查看文件的后几行  
语法：tail &nbsp;-[nf] &nbsp;文件名  
-n &nbsp; 行数  
-f &nbsp; 动态显示文件内容（即文件的实时内容）  
举例：tail &nbsp; -f &nbsp;-n &nbsp;100

<font size="4em">7. **find**</font>  
英文：<font color="red">find</font>   
作用：查找文件或者目录  
语法：find &nbsp;路径 &nbsp;匹配条件  

- -name 按照名称查找   
  举例：find&nbsp;/etc&nbsp;-name&nbsp;"init"
- -size 按照文件大小查找  
  以block为单位，一个block是512B，1K是2个block  +大于 &nbsp; -小于  
  举例：find&nbsp;/etc&nbsp;-size&nbsp;-204800

<font size="4em">8. **tar**</font>  
英文：<font color="red">tar</font>   
作用：文件或者目录打（解）包  
语法：tar&nbsp;[-zcf]&nbsp;压缩后文件名&nbsp;文件或者目录

- -c&nbsp;创建一个压缩文件（create）
- -x&nbsp;解开一个压缩文件（extract）
- -z&nbsp;以gzip命令压缩/解压缩  

举例：tar&nbsp;-zcf&nbsp;dir1.tar.gz&nbsp;dir1   
**注：**这里理解一下打包和压缩的意思：**打包**是指将一大堆文件或目录什么的变成一个总的文件，**压缩**则是将一个大的文件通过一些压缩算法变成一个小文件。为什么要区分这两个概念呢？这源于Linux中的很多压缩程序只能针对一个文件进行压缩，这样当你想要压缩一大堆文件时，你就得先借助另外的工具将这一大堆文件先打成一个包，然后再就原来的压缩程序进行压缩。  

<font size="4em">9. **shutdown**</font>  
英文：<font color="red">shutdown</font>   
作用：关机  
语法：shutdown&nbsp;[选项]&nbsp;时间

- -c&nbsp;取消前一个关机命令
- -h&nbsp;关机
- -r&nbsp;重启  

举例：shutdown&nbsp;-h&nbsp;now  
　　　reboot -h now

### 