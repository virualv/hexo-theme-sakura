---
title: shell 学习指北
date: 2019-09-15 23:16:52
tags:
 - shell
 - bash
 - linux
categories: Shell
photos: https://www.w3cschool.cn/attachments/image/20170622/1498119961561899.png
---
# shell入门

### 1. 第一个 hello world ！脚本

```shell
#！/bin/sh
echo "hello world !"
```

### 变量

*变量命名规则和C、Java、python等语言一致*
1. 要是只能是字母或下划线开头
2. 不能以数字开头
3. 变量名可以使用数字、字母、下划线，且只能能包含这三种

- 使用变量
```shell
#!/bin/sh
a = 13
echo $a

```

```shell
#!/bin/sh
a = 13
echo ${a}

name = "alex"
echo $name
```

**注意：尽量用${}这种方式，如 ${skill}script,没有{}，则变成$skillscrpit,这是个未赋值的变量**

- 只读变量 
```shell
#!/bin/sh
url="www.baidu.com"
readonly url
url="www.google.com"
```
*提示信息*
```shell
3.sh: 4: 3.sh: url: is read only
```

- 删除变量
```shell
unset [变量名]

#!/bin/sh
url="www.baidu.com"
unset url
echo $url
```

#### 变量类型
1. 局部变量
2. 环境变量
3. shell变量

### 字符串

#### 单引号
- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用
```shell
str='this is string'
```
#### 双引号

```shell
string="shell"
str="this is ${string}"
```
```shell
name='kitbar'
str="hello, I'm "$name"! \n "
```
**双引号的优点：**

- 双引号里可以有变量
- 双引号里可以出现转义字符

#### 查找子字符串

```shell
string="kitbar is great site"
echo `expr index "$string" ba`
```

```bash
4
```

# shell入门

### 1. 第一个 hello world ！脚本

```shell
#！/bin/sh
echo "hello world !"
```

### 变量

*变量命名规则和C、Java、python等语言一致*
1. 要是只能是字母或下划线开头
2. 不能以数字开头
3. 变量名可以使用数字、字母、下划线，且只能能包含这三种

- 使用变量
```shell
#!/bin/sh
a = 13
echo $a

```

```shell
#!/bin/sh
a = 13
echo ${a}

name = "alex"
echo $name
```

**注意：尽量用${}这种方式，如 ${skill}script,没有{}，则变成$skillscrpit,这是个未赋值的变量**

- 只读变量 
```shell
#!/bin/sh
url="www.baidu.com"
readonly url
url="www.google.com"
```
*提示信息*
```shell
3.sh: 4: 3.sh: url: is read only
```

- 删除变量
```shell
unset [变量名]

#!/bin/sh
url="www.baidu.com"
unset url
echo $url
```

### 字符串
#### 单引号
- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用
```shell
str='this is string'
```
#### 双引号数组

#### 定义数值

```shell
arr_name=(value0,value1,value2,value3,value4)
或
arr_name[0]=value0
arr_name[1]=value1
arr_name[2]=value2
arr_name[2]=value3
arr_name[2]=value4
```

#### 读取数值

```shell
${arr_name[n]}	// n代表下标

value=${arr_name[n]}
```

#### 获取所有元素

```shell
echo ${arr_name[@]}
```

#### 获取数组的长度

```shell
length=${#arr_name[@]}
或
length=${#arr_name[*]}
或
length=${#arr_name[n]}
```

### shell 注释

#### 单行注释

```shell
#
# 注释
# author： huangzy
str="sid"
```

#### 多行注释

```shell
:<<EOF
注释内容
EOF

或者

:<<!
注释内容
!

或者

:<<@
注释内容
@
```

## Shell传递参数

```shell
$0	// 执行的文件名
$1	// 第一个参数
$2	// 第二个参数
```

```shell
$#	// 传递到脚本的参数个数
$*	[只做了解，主要用$@]// 以一个单字符串显示所有向脚本传递的参数
	// "$*" 则会显示所有参数"$1 $2...$n"
$$	// 脚本运行的当前进程ID号
$!	// 后台运行的最后一个进程的ID号
$@	// 与$*相同，但是使用时加引号，并在引号中返回每个参数
	// "$@" 则显示参数"$1" "$2"..."$n"
$-	// 显示shell使用的当前选项，与set命令功能相同
$?	// 显示最后命令的退出状态
```

## 运算符

- 算术运算符

- 关系运算符

- 布尔运算符

- 字符串运算符

- 文件测试运算符

通过expr来支持运算

```shell
#!/bin/sh
val = `expr 2+2`
echo "两数和为：$val"
```

```
+
-
*
/
%
=
==
!=
```

**注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b]是错误的，必须写成 [ $a == $b ]**

****

```shelll
-eq	检测两个数是否相等，相等返回 true。
-ne 检测两个数是否不相等，不相等返回 true。
-gt 检测左边的数是否大于右边的，如果是，则返回 true。
-lt 检测左边的数是否小于右边的，如果是，则返回 true。
-ge 检测左边的数是否大于等于右边的，如果是，则返回 true。
-le 检测左边的数是否小于等于右边的，如果是，则返回 true。
```

### echo 命令

```shell
命令格式
echo string
```

1. 显示普通字符串

    ```shell
    echo "It is a test"
    ```

2. 显示转义字符

   ```shell
   echo "\"It is a test\""
   ```


3. 显示变量

   ```shell
   name="xiaoming"
   echo "who is $name"
   ```

4. 显示换行

   ```shell
   echo -e "OK！ \n"  
   echo "It is a test"
   
   echo -e "OK！ \c"  # -e 开启转义 \c 不换行
   echo "It is a test"
   ```

5. 不换行显示

   ```shell
   echo -n "ok"
   ```

6. 不转义字符

   ```shell
   echo '$name\"\n'	# 单引号内不进行任何转义
   ```

7. 显示执行结果

   ```shell
   echo `date`
   echo `cal`
   ```

### printf 命令

使用语法

```shell
printf  format-string  [arguments...]
# format-string 为格式控制字符
# arguments 为参数列表
```

```shell
%s %c %d %f 都是格式替代符

%-10s指一个宽度为10个字符（-表示左对齐，没有则是右对齐）
%-4.2f指格式化为float类型的小数，其中.2表示保留2位小数
```

**格式只指定了一个参数，但多出的参数仍然会按照该格式输出，format-string 被重用**

*如果没有 arguments，那么 %s 用NULL代替，%d 用 0 代替，%f用0.000000代替，%c则直接是空代替*

#### 转义的字符

| \a    | 警告字符，通常为ASCII的BEL字符                               |
| ----- | ------------------------------------------------------------ |
| \b    | 后退                                                         |
| \c    | 抑制（不显示）输出结果中任何结尾的换行字符（只在%b格式指示符控制下的参数字符串中有效），而且，任何留在参数里的字符、任何接下来的参数以及任何留在格式字符串中的字符，都被忽略 |
| \f    | 换页（formfeed）                                             |
| \n    | 换行                                                         |
| \r    | 回车（Carriage return）                                      |
| \t    | 水平制表符                                                   |
| \v    | 垂直制表符                                                   |
| \\    | 一个字面上的反斜杠字符                                       |
| \ddd  | 表示1到3位数八进制值的字符。仅在格式字符串中有效             |
| \0ddd | 表示1到3位的八进制值字符                                     |

### test命令

**一般用在if判断里**

```shell
#!/bin/sh
cd ~/tmp
if test -d ./11.sh
then
	echo "is dir"
else
	echo "is not dir"
fi
```

```shell
-eq | -ne | -gt | -ge | -lt | -le
实际判断规则与运算符中介绍一致
```

#### 文件测试

```shell
-e 文件名	如果文件存在则为真
-r 文件名	如果文件存在且可读则为真
-w 文件名	如果文件存在且可写则为真
-x 文件名	如果文件存在且可执行则为真
-s 文件名	如果文件存在且至少有一个字符则为真
-d 文件名	如果文件存在且为目录则为真
-f 文件名	如果文件存在且为普通文件则为真
-c 文件名	如果文件存在且为字符型特殊文件则为真
-b 文件名	如果文件存在且为块特殊文件则为真
! test -e 文件名 如果文件不存在则为真    [对第一种情况取反]
```

### 流程控制

#### if else

```shell
if condition
then
	cmd1
	cmd2
fi
```
```shell
if condition
then
	cmd1
	cmd2
	cmd3
else
	cmd1
	cmd2
fi
```
#### if elif else
```shell
if condition
then
	cmd1
	cmd2
	cmd3
elif condition
then
	cmd1
	cmd2
	cmd3
else
	cmd1
	cmd2
fi
```

#### for 循环

```shell
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

#### while循环

```shell
while 条件:
do
	command
done
```

#### until循环

```shell
until condition
do
	command
done
```

#### case循环

```shell
case i in
opt1)
	command1
    command2
    ...$#	传递到脚本的参数个数
$*	以一个单字符串显示所有向脚本传递的参数
$$	脚本运行的当前进程ID号
$!	后台运行的最后一个进程的ID号
$@	与$*相同，但是使用时加引号，并在引号中返回每个参数。
$-	显示Shell使用的当前选项，与set命令功能相同。
$?	显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误
    ;;
opt2)
	command1
	command2
	...
	;;
esac
```

**注意:case的语法和C family语言差别很大，它需要一个esac（就是case反过来）作为结束标记，每个case分支用右圆括号，用两个分号表示break。**

#### break  continue

> 和C、Java一样，break是退出整个循环，continue是退出单次循环

### 函数

| $#   | 传递到脚本的参数个数                                        |
| ---- | ----------------------------------------------------------- |
| $*   | 以一个单字符串显示所有向脚本传递的参数                      |
| $$   | 脚本运行的当前进程ID号                                      |
| $!   | 后台运行的最后一个进程的ID号                                |
| $@   | 与$*相同，但是使用时加引号，并在引号中返回每个参数。        |
| $-   | 显示Shell使用的当前if选项，与set命令功能相同。              |
| $?   | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误 |

### 输入、输出重定向

```shell
command > file		# 输出重定向到file
command < file		# 输入重定向到file
command >> file		# 输出追加到file里
n > file			# 将文件描述符为n的文件重定向到file
n >> file			# 将文件描述符为n
n >& m				# 将输出文件 m 和 n 合并。
n <& m				# 将输入文件 m 和 n 合并。
<< tag
```

**注意：文件描述符 0 通常是标准输入（STDIN），1 是标准输出（STDOUT），2 是标准错误输出（STDERR）**