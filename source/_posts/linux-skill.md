---
title: Linux SKill(Linux技巧)
date: 2019-09-15 23:04:16
tags:
 - linux
 - ubuntu
 - debian
 - centos
categories:
 - Linux
 - Shell
photos: https://pic3.zhimg.com/v2-dc98064e8bc40d83d91362d4ce1dd9d3_1440w.jpg
---

## 1. apt

- 静默更新

```shell
apt-get update -qq
```

- 静默下载安装

```shell
apt-get install -q -y vim
```

- 处理安装时的错误

```shell
apt-get intall -f
```

## 2. aptitude

当遇到大量依赖包无法处理时。使用aptitude处理

其具有强大是依赖处理问题

**使用方式**

```
aptitude
	update  更新源
	install 安装软件包
	remove  卸载软件包
	purge   卸载软件包并删除配置文件
	search  搜索软件包
	show    显示软件包的详细信息
	
```

## 3. 利用cat添加文本文件

```shell
root@localhost:~# cat > /etc/profile.d/env.sh
export EDITOR=vim     [Enter ， Ctrl+C]
^C
root@localhost:~# cat /etc/profile.d/env.sh
export EDITOR=vim
```

## 4. apt卸载文件时，出现的问题

> 在卸载之前安装的mysql 或者 mariadb后，再次安装mysql或者mariadb时，如果现在安装的版本地低于之前的安装，要删除/etc/mysql和/usr/lib/mysql 中的文件，否则会出现错误导致安装不上
>
> ```shell
> 建议在每次利用包管理卸载时，使用 purge 参数，可以彻底移出 安装包相关文件
> 
> apt remove --purge [PackageName]
> apt-get purge [PackageName]
> apt-get autoremove --purge
> ```

## 5. Ubuntu 输入正确密码却无法进入桌面

> 查询网上，得出解决方案
>
> ```shell
> 原因：用户主目录中的.Xauthority的所有者变成了root，导致用户没有.Xauthority权限startx无法读入display信息
> -rw-------  1 root   root         466 8月  19 09:54 .Xauthority
> 
> # sudo chown ts:ts /home/ts/.Xauthority
> 
> -rw-------  1 ts   ts         466 8月  19 09:54 .Xauthority
> ```
>
> 更改所有者解决

## 6. 获取Ubuntu本地IP地址

- 通用
```shell
tmpip=$(ip a | grep inet | sed -e 's/^.*inet//g' | sed -e '1,2 d' | sed -e '$d');echo ${tmpip%%/*}
```
- Ubuntu 16.04
```shell
ifconfig eno1 | grep inet | sed -e s/^.*addr:// | sed -e s/B.*$// | sed -e '$d'
```
- Ubuntu 18.04
```shell
ifconfig eno1 | grep inet | sed -e s/^.*inet// | sed -e s/netmask.*$// | sed -e '$d'
```

## 7. 修改/etc/sudoers 文件格式错误，导致无法使用sudo

- 解决方式一
```shell
su -
登录到root账户修改/etc/sudoers到原来状态
[前提：设置过root密码]
```
- 解决方式二
```shell
重启机器在开机准备进入系统时按Shift键进入到grub恢复模式，然后在root环境下修改/etc/sudoers文件到原来状态，然后重启机器
```

## 8. LVM修改卷组名后忘记修改fstab，导致重启失败

> 由于修改卷组名后，/etc/fstab未做对应得修改使系统重启时无法挂载逻辑卷
> 系统不停的扫描导致重启失败

- 解决方式

1. 重启机器在开机准备进入系统时按Shift键进入到高级启动模式，按e键，修改grub启动文件将对应得卷组名改正
2. 再进入恢复模式进root账户修改/etc/fstab文件和其他启动相关的文件

## 9. Linux apt安装弹窗设置干扰自动化安装
```shell
sudo debconf-set-selections <<< '弹窗相关的设置信息'
```

Example：

- LDAP

```shell
debconf-set-selections <<< 'slapd slapd/internal/adminpw password mypass'
debconf-set-selections <<< 'slapd slapd/internal/generated_adminpw password mypass'
debconf-set-selections <<< 'slapd slapd/password1 password mypass'
debconf-set-selections <<< 'slapd slapd/password2 password mypass'
```

- MySQL

```shell
debconf-set-selections <<< 'mysql-server-5.7 mysql-server/root_password password mypass'
debconf-set-selections <<< 'mysql-server-5.7 mysql-server/root_password_again password mypass'
```

## 10. vim快捷注释方法

批量插入字符快捷键：
```markdown
Ctrl+v进入VISUAL BLOCK（可视块）模式，按 j （向下选取列）或者 k （向上选取列），再按Shift + i 进入编辑模式然后输入你想要插入的字符（任意字符），再按两次Esc就可以实现批量插入字符，不仅仅实现批量注释而已。  
```
批量删除字符快捷键：
```markdown
 Ctrl+v进入VISUAL BLOCK（可视块）模式，按 j （向下选取列）或者 k （向上选取列），直接（不用进入编辑模式）按 x 或者 d 就可以直接删去，再按Esc退出
```

## 11. mariadb普通用户无法登录的问题

```markdown
是由于mariadb在10版本后mysql库的user表中plugin字段默认为unix_socket所导致的将其改为mysql_native_password则解决
```
```sql
use mysql; 
update user set plugin='mysql_native_password' where User='root';
```

## 12. Docker修改镜像默认存储位置
```shell
sudo vim /etc/docker/daemon.json
```
在其中加入下列内容，注意：内容格式是json格式
```json
"graph": "/home/$Path"   # $Path表示路径
```

## 13. ln,find,du,sed命令使用简介

每次想创建软链都会忘了ln -s的前后参数规则，每次都要百度或Google搜一下，实在是烦死了，所以这次干脆记在博客上吧，算是个备忘了
```shell
ln -s a文件路径 b文件路径
```
> 其中a文件代表你要链接的文件或文件夹路径，也即被链接文件或文件夹路径
> 其中b文件代表将要创建链接的文件，其指向a文件（文件夹）。好比C语言中的指针

### find命令

```shell
使用方法： 
find   path   -option   [-print ]   [ -exec  -ok  command ]  {} \;

######  根据文件名查找 #######
find / -name filename 再根目录里面搜索文件名为filename的文件
find /home -name "*.txt"
find /home -iname "*.txt"  # 忽略大小写


######  根据文件类型查找 #######
find . -type 类型参数
f 普通文件
l 符号连接 
d 目录 
c 字符设备 
b 块设备 
s 套接字 
p Fifo


######  根据目录深度查找 #######
find . -maxdepth 3 -type f  # 最大深度为3
find . -mindepth 2 -type f  # 最小深度为2

#########   根据文件的权限或者大小名字类型进行查找 ###########

find . -type f -size (+|-)文件大小 # +表示大于 -表示小于 
b —— 块（512字节） 
c —— 字节 
w —— 字（2字节） 
k —— 千字节 
M —— 兆字节 
G —— 吉字节


#########   按照时间查找  ############

-atime（+|-）n  # 此选项代表查找出n天以前被读取过的文件。
-mtime（+|-）n  # 此选项代表查找出n天以前文件内容发生改变的文件。
-ctime（+|-）n  # 此选项代表查找出n天以前的文件的属性发生改变的文件。
-newer file  # 此选项代表查找出所有比file新的文件。
-newer file1 ! –newer file2  # 此选项代表查找比file1文件时间新但是没有file2时间新的文件。

# 注意：   
#  n为数字，如果前面没有+或者-号，代表的是查找出n天以前的，但是只是一天之内的范围内发生变化的文件。
#  如果n前面有+号，则代表查找距离n天之前的发生变化的文件。如果是减号，则代表查找距离n天之内的所有发生变化的文件。
#  -newer file1 ! –newer file2中的!是逻辑非运算符

#########   按照用户/权限查找  ############

-user 用户名：根据文件的属主名查找文件。
-group 组名：根据文件的属组名查找文件。
-uid n：根据文件属主的UID进行查找文件。
-gid n：根据文件属组的GID进行查找文件。
-nouser：查询文件属主在/etc/passwd文件中不存在的文件。
-nogroup：查询文件属组在/etc/group文件中不存在的文件
-perm 777： 查询权限为777的文件

来自: http://man.linuxde.net/find

########  查找时指定多个条件   ############

-o：逻辑或，两个条件只要满足一个即可。
-a：逻辑与，两个条件必须同时满足。

find  /etc -size +2M -a -size -10M


#########  对查找结果进行处理  #############
-exec  shell命令  {}  \;
-ok  shell命令  {}  \;
其中-exec就是代表要执行shell命令，后面加的是shell指令，再后面的“{}”表示的是要对前面查询到的结果进行查询，最后的“\；”表示命令结束。需要注意的是“{}”和“\”之间是要有空格的。而-ok选项与-exec的唯一区别就是它在执行shell命令的时候会事先进行询问，-print选项是将结果显示在标准输入上

find /home -name  “*.txt” -ok ls -l {} \;
find /home -name  “*.txt” -ok rm {} \;
```



### du

```shell
du dirname # 显示dirname下所有目录及其子目录的大小
-s ： 如果后面是目录，只显示一层
-h : 以能显示的最大单位显示
```


**初识正则表达式**

```shell
^ : 匹配开头
$ : 匹配结尾
[] ： 范围匹配
[a-z] : 匹配有小写字母
[A-Z] : 匹配所有大写字母
[0-9] : 匹配所有数字
. ： 匹配单个字符
* ： 表示*前面的内容出现0次或多次
+ ： 表示+前面的内容出现1次或多次
? ： 表示？前面的内容出现0次或1次

cat a.txt |grep hat$ # 匹配以hat结尾的行
cat a.txt |grep ^hat # 匹配以hat开头的行
cat a.txt | grep -E "[0-9]*"  # 匹配有0到多个数字的行
cat a.txt | grep -E "[0-9]+"  # 匹配有至少有1个数字的行
cat a.txt | grep -E "[0-9]？"  # 匹配有0到1个数字的行
```


### sed : 流编辑器，一次处理一行内容

#### 复制代码

```sh
sed [-nefr] [动作] [文件]
```
#### 选项与参数：

```shell
-n ：使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN 的数据一般都会被列出到终端上。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行(或者动作)才会被列出来
-e ：直接在命令列模式上进行 sed 的动作编辑
-f ：直接将 sed 的动作写在一个文件内， -f filename 则可以运行 filename 内的 sed 动作
-r ：sed 的动作支持的是延伸型正规表示法的语法。(默认是基础正规表示法语法)
-i ：直接修改读取的文件内容，而不是输出到终端。
```

*动作说明： [n1[,n2]]*

	动作：n1, n2 ：不一定存在，一般代表选择进行动作的行数，比如，如果我的动作是需要在 10 到 20 行之间进行的，则10,20[动作行为]

#### 动作：

```shell
#a ：新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)
#c ：取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
#d ：删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
	sed  "3d"  file  #  删除第三行
	sed  "1,3d"  # 删除前三行
	sed  "1d;3d;5d"  # 删除1、3、5行
	sed  "/^$/d" #删除空行   
	sed  "/abc/d" #删除所有含有abc的行
	sed  "/abc/，/def/d" #删除abc 和 def 之间的行，包括其自身
	sed  "1，/def/d" #删除第一行到 def 之间的行，包括其自身
	sed  "/abc/，+3d " # 删除含有abc的行之后，在删除3行
	sed  "/abc/，～3d" #从含有abc的行开始，共删除3行
	sed  "1~2d"  # 从第1行开始，每2行删除一行， 删除奇数行
	sed  "2~2d"  # 从第2行开始，每2行删除一行， 删除奇数行
	sed  "\$d"  # 删除最后一行
	sed  "/dd\|cc/d"  删除有dd或者cc的行
	
#i ：插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)；
#p ：列印，亦即将某个选择的数据印出。通常 p 会与参数 sed -n 一起运行
	
	sed -n  "3p"  file  #  显示第三行
	sed -n  "1,3p"  # 显示前三行
	sed -n  "2,+3p"  # 显示第二行，及后面的三行
	sed -n  "\$p"  # 显示最后一行
	sed -n "1p;3p;5p"  # 只显示文件1、3、5行
	sed -n  "$="  # 显示文件行数

#s ：替换，可以直接进行取代的工作。通常这个 s 的动作可以搭配正规表示法，例如 1,20s/old/new/g
	
	's/old/new/g'  
	
	sed  "s/\(all\)/bb/"
	sed -r "s/(all)/bb/"
```
## 14. 执行apt时,出现E: 无法获得锁 /var/lib/apt/lists/lock - open的问题

```shell
apt-get update
```
出现
```shell
E: 无法获得锁 /var/lib/apt/lists/lock - open
```
一般来说是你的用户权限不够所致，可以sudo解决，或直接使用root账户执行。

如果还是无法解决可尝试下面方式解决；

解决方法 

```shell
rm -rf /var/lib/apt/lists/lock
```
