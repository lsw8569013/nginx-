
清空命令行：reset

文件操作：
显示列表
ls -l 

ls -la 所有

ls -l ja* 通配符查找

创建文件

touch today.c

复制文件

cp src.txt dest.txt

cp -i src.txt dest.txt 询问

cp src.txt . 复制到当前目录

cp -R 目录 dest 复制整个目录到指定路径

cp c_?1 ../  通配符复制到上级目录


删除文件

rm file

删除目录
rm -rf 目录

查看文件类型：
file 文件

查看文件内容：
cat file

cat -n file 显示行号

查看文件最后10行

tail -n 10 file

查看文件最开始的10行

head -n 10 file


创建用户
useradd -m jack 创建用户的同时，创建了home目录

userdel -r jack 删除用户

创建组

groupadd androidgroup

分配用户到组

usermod -G androidgroup jack

文件权限

r读 w写 x执行

drwxr-xr-x

d rwx r-x r-x

d目录

1.文件所属用户具备的权限（root对该文件具备读写执行权限）

2.文件所属用户的所属组具备的权限（读、执行）

3.系统的其他用户具备的权限（读、执行）


rwx必须是固定顺序

权限		二进制		八进制
---			000			0

--x			001			1

-w-			010			2

-wx			011			3

r--			100			4

r-x			101			5

rw-			110			6

rwx			111			7

修改文件权限

chmod 644 file

给用户加上执行权限

chmod u+x file

改变创建目录的默认权限
umask 026

777-026

改变文件的所属

chown user.group file

chown user file

chown .group file

----------------------shell脚本

输出
echo 

#!/bin/bash           

 2 NDK=10
 
 3 text="i love shell"
 
 4 
 5 #命令的执行结果的输出作为变量的值
 
 6 text1=`date`
 
 7 text2=$(who)
 
 8 
 9 echo $NDK
 
10 echo $text

11 echo "$text very much"

12 echo "\$NDK"

13 echo $text1

14 echo $text2




 

