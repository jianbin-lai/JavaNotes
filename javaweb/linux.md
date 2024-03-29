#### Linux操作系统

##### 目录结构

![](https://www.ydlclass.com/doc21xnv/assets/1658378236166.0e7875fa.png)

1. root，存放root用户的相关文件
2. home，存放普通用户的相关文件
3. bin，存放常用命令的目录，如vi，su
4. sbin，要具有一定权限才可以使用命令
5. mnt，默认挂载光驱和软驱的目录
6. etc，存放配置的相关文件
7. var，存放经常变化的文件，如网络连接的sock文件 、日志
8. boot，存放引导系统启动的相关文件
9. usr，安装一个软件的默认目录，相当于windows下的program files
10. proc，这个目录是一个虚拟的目录，它是系统内存的映射，访问这个目录来获取系统信息
11. srv ，service缩写。该目录存放一些服务启动之后需要提取的数据
12. sys，这是linux2.6内核的一个很大的变化，该目录下安装了2.6内核中新出现的一个文件系统
13. tmp，这个目录是用来存放一些临时文件的
14. del，类似于windows的设备管理器，把所有的硬件用文件的形式存储
15. media，系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将外部的存储挂载在/mnt/上，然后进入该目录就可以查看里面的内容了。
16. opt，这是给主机额外安装软件所摆放，如安装oracle数据库就可放到该目录下默认为空。

Linux中所有内容都是以文件的形式保存和管理，即：一切皆文件。普通文件是文件；目录(在win下称为文件夹)是文件；硬件设备(键盘、硬盘、打印机，网卡)是文件；套接字(socket)、网络通信等资源也都是文件。

##### 虚拟机网络配置	

桥接模式：桥接模式就是将【主机网卡】与【虚拟机虚拟的网卡】利用虚拟网桥进行通信。在桥接的作用下，类似于把【物理主机虚拟为一个交换机】，所有桥接设置的【虚拟机】连接到这个交换机的一个接口上，物理主机也同样插在这个交换机当中，所以所有桥接下的网卡与网卡都是交换模式的，相互可以访问而不干扰。在桥接模式下，虚拟机ip地址需要与主机在同一个网段，如果需要联网，则网关与DNS需要与主机网卡一致

NAT地址转换：作用主要是做网络地址转换，我们可以使用内部的局域网络，访问公共网络。

- 物理机会产生一张虚拟网卡（VMnet8）、这张网卡和虚拟机的网卡的ip地址统一有dhcp管理发放。
- 上网时，通过nat设备进行网络地址转化，从而使得所有的网卡均可上网。

Host-only(仅主机模式)：Host-Only模式将虚拟机与外网隔开，使得虚拟机成为一个独立的系统，只与主机相互通讯

##### shell简介

shell既是一个应用程序，也叫壳程序，提供一个界面，使用户可以通过shell访问操作系统内核。

版本：

- sh（Bourne Shell）（交换式的命令解释器和命令编程语言）： 是UNIX最初使用的 shell，而且在每种 UNIX 上都可以使用 。在shell编程方面做的很优秀，但是在处理与用户的交互方面做得不如其他几种shell。
- bash（Bourne Again Shell）：Linux默认，是Bourne Shell的扩展。完全兼容Bourne Shell，并在他基础上增加了很多特性如命令补全、命令历史等。有灵活和强大的编辑接口，同时有很友好的用户界面。

命令类型

- 内置命令

  【内部命令】实际上是shell程序的一部分，其中包含的是一些比较简单的linux系统命令，这些命令由shell程序识别并在shell程序内部完成运行，通常**在linux系统加载运行时shell就被加载并驻留在系统内存中**。内部命令是写在bashy源码里面的，其执行速度比外部命令快，因为解析内部命令shell不需要创建子进程。比如：cd，echo等 。

- 外部命令

  【外部命令】是linux系统中的实用程序部分，因为实用程序的功能通常都比较强大，所以其包含的程序量也会很大，**在系统加载时并不随系统一起被加载到内存中，而是在需要时才将其调用内存**。通常外部命令的实体并**不包含在shell中，但是其命令执行过程是由shell程序控制的**。shell程序管理外部命令执行的路径查找、加载存放，并控制命令的执行。外部命令是在bash之外额外安装的，通常放在/bin、 /usr/bin、 /sbin、 /usr/sbin 等目录下。可通过“echo $PATH”命令查看外部命令的存储路径，比如：ls、vi等。

#### linux命令详解

##### 易忘常用命令

1. 上下翻页  shift + pgdn |  pgup
2. 行首与行尾：shift + home |   end
3. 从上倒下搜索关键词   /linux  从下倒上搜索关键词   ?linux     
4. N定位到上一个搜索的关键词，n定位下一个

##### 目录相关命令

1. pwd（绝对路径
2. ls（目录下文件  简化ll）
3. 创建多级目录  mkdir -p a/b
4. 删除目录  rmdir -p a/b
5. 复制目录或文件 cp -r src des
6. 移动文件或重命名   mv  src  des
7. 递归删除文件及目录  rm -rf   ydlclass

##### 文件相关命令

1. 创建文件   touch  文件名
2. 输出字符或变量或将内容存储到文件   echo hell  --> echo linux >> ydlclass.txt(追加) -> encho linux > ydlclass.txt(覆盖)
3. 查看文件内容   cat [] 文件名  选项：-b列行号空白行不算   -n 空白行算
4. 查看文件内容  more 文件
   1. 空格键（space）：向下翻一页
   2. enter：向下翻一行
   3. q：退出more，不在显示文件内容
   4. ctrl+f：向下滚动一屏
   5. ctrl+b：返回上一频
5. 查看文件头n行  head -n 文件名
6. 查看文件末几行  tail -n(-f 修改) 文件名
7. 统计指定文本行数、字数、字节数    wc   -l  -w  -c
8. 查看文件的具体存储信息和时间等信息  stat 文件名
9. 查看文件类型  file 文件名

##### 安装软件和资源下载

yum：yum（yellowdog updater modified）是一个RPM系统的自动更新和软件包安装/卸载器。它可以自动计算依赖和找出想要安装的软件包。

![](https://www.ydlclass.com/doc21xnv/assets/image-20220729151414923.0312b716.png)

安装：yum install vim -y

卸载：yum remove vim -y

下载网络文件：wget  [] 地址

1. -b：background后台下载
2. -P：directory-prefix下载到指定目录
3. -O：下载并以指定的文件名保存

##### vim编辑器

![](https://www.ydlclass.com/doc21xnv/assets/1658888100676.67f1fd66.png)	

命令模式

光标移动

1. 跳转文件的首行   gg
2. 跳转文件的第n行  n+gg

3. 跳转文件的尾行  G


删除、复制、黏贴

| 操作类型 | 操作键      | 功能                     |
| ---- | -------- | ---------------------- |
| 删除   | x或Del    | 删除光标处的单个字符             |
|      | dw       | 删除至一个单词的末尾             |
|      | d2wgg    | 删除两个字符                 |
|      | dd       | 删除当前光标所在行              |
|      | n+dd     | 删除从光标所在行开始的n行内容        |
|      | d^       | 删除当前光标之前到行首的所有字符（不含光标） |
|      | d$       | 从当前光标删除到行尾（包含光标）       |
| 复制   | yy       | 复制当前行整行的内容到剪贴板         |
|      | nyy(3yy) | 复制从光标所在行开始的n行内容        |
| 粘贴   | p        | 粘贴                     |
| 替换   | r+字符     | 输入r+字符，替换所在位置字符        |
|      | R+字符     | 连续替换多个字符               |

可视模式：可进行批量文本的选择

1. v 进入可视模式
2. 移动光标位置
3. 输入y复制文本
4. 输入p粘贴

撤销编辑及保存退出

|      |                     |      |
| ---- | ------------------- | ---- |
| 操作键  | 功能                  |      |
| u    | 撤销最后执行的命令,多次输入，多次撤销 |      |
| U    | 撤销对整行的命令            |      |
| ZZ   | 保存当前的文件内容并退出vi编辑器   |      |

末行模式

| 功能       | 命令               | 备注         |
| -------- | ---------------- | ---------- |
| 保存文件     | :w               | 保存修改的内容    |
|          | :w /root/newfile | 另存为其他文件    |
| 退出vi     | :q               | 未修改退出      |
|          | :q!              | 放弃修改并退出    |
| 保存文件退出vi | :wq              | 保存修改的内容并退出 |
| 行号显示     | :set nu          | 在编辑器中显示行号  |
|          | :set nonu        | 取消编辑器中显示行号 |

##### 文本处理文件

grep： grep [参数] 查找内容 源文件     在文件内搜索字符串匹配的行并输出

参数：

- -c：count只输出匹配行的计数
- -n：输出匹配的行和行号

sed：很好的文本文件处理工具，他是以【行】为单位进行处理，可以将数据行进行替换、删除、新增、刷选等特定工作。

- -n∶使用安静(silent)模式。在一般 sed 的用法中，所有来自被处理和未被处理的数据都会显示在控制台。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行才会被列出来。
- -i∶直接修改读取的档案内容，而不是由控制台输出。

常用命令：

- a∶新增， 在下一行插入

- c∶替换， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！

- d∶删除，因为是删除啊，所以 d 后面通常不接任何咚咚；

- i∶插入， 在上一行插入

- p∶展示，列出最终的结果。

- s∶替换，可以直接进行取代的工作哩！sed    's/要替换的字符串/新的字符串/g' 

  刷新某行记录、删除特定行、插入一行或多行字符串、替换



