---
title: python 相关知识点
date: 2019-09-15 23:02:17
tags:
 - python
 - it
 - web
categories:
 - Python
photos: https://www.python.org/static/img/python-logo-large.c36dccadd999.png?1576869008
---
# 变量
## 变量的命名格式：
        1.由数字、字母、下划线组成，不得含有其他特殊字符
        2.首字母不能为数字
        3.要注意区分大小写
        4.变量名不能为保留字(关键字)
        5.描述性单词命名你的变量，不能用中文、拼音
        6.驼峰式、下划线分割


# 数据运算
# 数据类型初识
### 数字
#### 整数 int(integer)
                整型  能表示的长度为-2^30-1~2^30-1.
                长整型
                in python3 已经不区分整型和长整型，统一叫整型。
#### 浮点数 float
#### 复数  x + yj  x是实部 y是虚部 x，y实际都是实数
#### 布尔值（bool）
        只有两种状态，分别是
            True    真
            False   假
        字符串
            salary.isdigit()
            计算机中，一切皆为对象
            世界万物，皆为对象，一切对象皆可分类 
#### 运算符
	算术运算符：+ - * / // % **
	赋值运算符：= += -= *= /= //= **= %=
	
	比较运算符：> < >= <= != ==
	逻辑运算符：and   or  not
	短路运算：当and第一个条件为False后面的就不会计算
			  当or 第一个条件为True后面的就不会计算
	优先级：()
	
	身份运算符：is    is not
	成员运算符：in    not in
	
	字符格式化输出
	 占位符 %s s = string
		   %d d = digit
		   %f f = float

# 循环loop
    有限循环，次数限制
    无限循环=死循环
    continue 结束本次循环，继续下一次循环（在多层中，指continue所在的一层的循环）
    break 跳出整个当前一层循环

for\
while\
break，continue

# 数据类型
## 整数
## 字符串
## 列表，元组
        查
            索引（下标），都是从0开始
            切片
            a.count('@value') 查某个元素的出现次数
            a.index('@value') 根据内容找其对应的位置
            'xxx' in a
        增加
            a.append(@object)
            a.insert(@index,'@content')
            a.extend 扩展
        修改
            a[index] = '@new value'
            a[start:end] = [1,2,3,4] (其中的数字代表第一二三...个值)
        删除
            a.remove('@value')
            a.pop(@index)
            del a ,del a[@index]
            a.clear()   清空
        排序
            a.sort()    （默认括号里面的参数reverse=False）从小到大排序
            a.sort(reverse = True)  从大到小排序
            a.reverse() 倒序
        身份判断
            type(a) is list
    购物车程序
## 集合（Set）
        不重复的
        无序的
        s.add() 添加元素，一个元素
        s.update()  更新，添加，多个元素
        s.remove() 删除元素，一个元素
        s.pop() 删除
        del s 删除整个集合
## 字典
        字典是python中唯一的映射类型，采用键值对应的形式存储的数据类型。
        注意：
            字典是无序存储的
            key必须是可哈希的
            可哈希表示key必须是不可变的类型，如：数字，字符串，元组。
    三级菜单

# 深浅拷贝
    1.浅拷贝：只拷贝第一层    import copy   copy.copy
    2.深拷贝：克隆整个整体    import copy   copy.deepcopy

# 函数：
    1.概念
    2.创建
    3.参数
    4.return
    5.作用域
        B-G-E-L


# 装饰器 （函数）
## 1.作用域
        B-G-E-L
## 2.高阶函数
    1.函数名可以作为参数
    2.函数名可以作为返回值
## 3.闭包




# 生成器
## 创建生成器的两种方式：
        1.（x*2 for x in range (10)） >>>>>>>>> generator object
        2.def f():
              yield 2
              print("ok")
              f() >>>>>>generator object
    
         yield from iterable本质上等于for item in iterable: yield item的缩写版

## 生成器的使用方法;
        1.next(f()) - - - - - - - - - - 计算出一个值
    
            注意：生成器再创建的时候已经决定了能计算出值个数，调用next的次数超过这个值时就会报StopIteration
    
            遍历所有元素可以通过for循环：
                for i in [1,2,3]:
                    print(i)
            for 循环内部做了三件事：
                1.调用对象的iter()方法，返回一个迭代器对象
    
                2.while:
                       try:
                           i = next(Iterator)
                       except StopIteration:
                           break
         2.send():
            f().send(None) # 等价于next(f())

# 迭代器
## 满足迭代器协议
        1.内部有next方法
        2.内部有iter()方法
        
        li=[1,2,3]:Iterable (内部有__iter__方法)>>>>>>>>>>>
        i = iter(li):List_Iterator
          
        next(i) - - - - - - - - - - 计算出一个值

***注意：生成器再创建的时候已经决定了能计算出值个数，调用next的次数超过这个值时就会报StopIteration***

            遍历所有元素可以通过for循环：
                for i in [1,2,3]:
                    print(i)
            for 循环内部做了三件事：
                1.调用对象的iter()方法，返回一个迭代器对象
    
                2.while:
                       try:
                           i = next(Iterator)
                       except StopIteration:
                           break
# 模块
# time
        time.time()
        time.sleep()
        time.strftime()
        time.striptime
        time.gmtime()   :UTC    结构化格式
        time.localtime()    :本地时间 结构化格式
# datetime
        datetime.datetime.now()
        
        print(time.clock()) #返回处理器时间,3.3开始已废弃 , 改成了time.process_time()测量处理器运算时间,不包括sleep时间,不稳定,mac上测不出来
        print(time.altzone)  #返回与utc时间的时间差,以秒计算\
        print(time.asctime()) #返回时间格式"Fri Aug 19 11:14:16 2016",
        print(time.localtime()) #返回本地时间 的struct time对象格式
        print(time.gmtime(time.time()-800000)) #返回utc时间的struc时间对象格式
    
        print(time.asctime(time.localtime())) #返回时间格式"Fri Aug 19 11:14:16 2016",
        print(time.ctime()) #返回Fri Aug 19 12:38:29 2016 格式, 同上
    
        日期字符串 转成  时间戳
        string_2_struct = time.strptime("2016/05/22","%Y/%m/%d") #将 日期字符串 转成 struct时间对象格式
        print(string_2_struct)
    
        struct_2_stamp = time.mktime(string_2_struct) #将struct时间对象转成时间戳
        print(struct_2_stamp)
    
        将时间戳转为字符串格式
        print(time.gmtime(time.time()-86640)) #将utc时间戳转换成struct_time格式
        print(time.strftime("%Y-%m-%d %H:%M:%S",time.gmtime()) ) #将utc struct_time格式转成指定的字符串格式
    
        时间加减
        import datetime
    
        print(datetime.datetime.now()) #返回 2016-08-19 12:47:03.941925
        print(datetime.date.fromtimestamp(time.time()) )  # 时间戳直接转成日期格式 2016-08-19
        print(datetime.datetime.now() )
        print(datetime.datetime.now() + datetime.timedelta(3)) #当前时间+3天
        print(datetime.datetime.now() + datetime.timedelta(-3)) #当前时间-3天
        print(datetime.datetime.now() + datetime.timedelta(hours=3)) #当前时间+3小时
        print(datetime.datetime.now() + datetime.timedelta(minutes=30)) #当前时间+30分
        c_time  = datetime.datetime.now()
        print(c_time.replace(minute=3,hour=2)) #时间替换
    
        %a	Locale’s abbreviated weekday name.
        %A	Locale’s full weekday name.
        %b	Locale’s abbreviated month name.
        %B	Locale’s full month name.
        %c	Locale’s appropriate date and time representation.
        %d	Day of the month as a decimal number [01,31].
        %H	Hour (24-hour clock) as a decimal number [00,23].
        %I	Hour (12-hour clock) as a decimal number [01,12].
        %j	Day of the year as a decimal number [001,366].
        %m	Month as a decimal number [01,12].
        %M	Minute as a decimal number [00,59].
        %p	Locale’s equivalent of either AM or PM.	(1)
        %S	Second as a decimal number [00,61].	(2)
        %U	Week number of the year (Sunday as the first day of the week) as a decimal number [00,53]. All days in a new year preceding the first Sunday are considered to be in week 0.	(3)
        %w	Weekday as a decimal number [0(Sunday),6].
        %W	Week number of the year (Monday as the first day of the week) as a decimal number [00,53]. All days in a new year preceding the first Monday are considered to be in week 0.	(3)
        %x	Locale’s appropriate date representation.
        %X	Locale’s appropriate time representation.
        %y	Year without century as a decimal number [00,99].
        %Y	Year with century as a decimal number.
        %z	Time zone offset indicating a positive or negative time difference from UTC/GMT of the form +HHMM or -HHMM, where H represents decimal hour digits and M represents decimal minute digits [-23:59, +23:59].
        %Z	Time zone name (no characters if no time zone exists).
        %%	A literal '%' character.

# random
        random.random()
        random.choice()
        random.randint()
        random.randrange()
        random.uniform()
        chr()数字按ASCII码转换成字母
# re
        findall():所有结果都返回到一个列表里
        search():返回匹配到的第一个对象（object），对象可以调用group()返回结果
        match() :只在字符串的开始,也返回匹配到的第一个对象（object），对象可以调用group()返回结果
        split() :
        sub()   :文字替换


# 正则表达式
## 匹配字符
### 元字符:
            .通配符
            ^
            $
            *   匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。
            +   匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
            ?   匹配前面的子表达式零次或一次。例如，"do(es)?" 可以匹配 "do" 、 "does" 中的 "does" 、 "doxy" 中的 "do" 。? 等价于 {0,1}。
            {}  限定符  限定符用来指定正则表达式的一个给定组件必须要出现多少次才能满足匹配
            []
            \
            ()
            |

# random,
# json
# pickle


# 面向对象



## 构造方法
### 特殊作用：
	在
		obj = 类名

### 如何创建类
	class 类名：
		pass

### 创建方法
	构造方法，__init__(self,arg)
		obj = 类('a1')
	普通方法
		obj= 类('xxx')
		obj.普通方法名()

## 面向对象三大特性之一：封装
	class Bar:
		def __init__(self,n,a):
			self.name = n
			self.age = a
			self.xue = 'o'
	
	b1 = Bar('mi',12)
	b2 = Bar('oric',8)

### 适用场景：
	如果多个函数中有一些相同的参数时，转换成面向对象
	
	    class DatabaseHelper:
	        def __init__(self,ip,port,username,pwd):
	            self.ip = ip
	            self.port = port
	            self.username = username
	            self.pwd =pwd
	        def add(self,content):
	            # 利用self中封装的用户名、密码等 连接数据
	            print('content')
	            # 关闭数据连接
	        def update(self,content):
	            # 利用self中封装的用户名、密码等 连接数据
	            print('content')
	            # 关闭数据连接
	        def delete(self,content):
	            # 利用self中封装的用户名、密码等 连接数据
	            print('content')
	            # 关闭数据连接
	        def get(self,content):
	            # 利用self中封装的用户名、密码等 连接数据
	            print('content')
	            # 关闭数据连接
	    s1 = DatabaseHelper('1.0.0.2',3306,'vk','nb')

## 面向对象三大特性之二：继承
	1.继承
		class 父类:
			pass
		class 子类(父类):
			pass
	
	2.重写
		防止执行父类中的方法
	
	3.self永远是执行该方法的调用者
	
	4.super(子类,self).父类中的方法()
	  父类名.父类中的方法()
	
	5.python中支持多继承
		a.左侧优先
		b.一条道走到黑
		c.同一个根时，根最后执行

## 面向对象三大特性之三：多态
	函数的参数需要声明类型（python不需要，java，C#，C++需要）
	python原生多态


# ====================面向对象中级====================

        class Foo:
            def __init__(self,name):
                # 普通字段
                self.name = name
            # 普通方法
            def show(self):
                print(self.name)
        obj = Foo('hu')
        obj.name
        obj.show()

## 类成员：
### 字段
		- 普通字段，保存在对象中，执行时，只能通过对象访问
		- 静态字段，保存在类中，执行时，可以通过对象访问，也可以通过类访问

### 方法
		- 普通方法，保存在类中，由对象调用 ，self-->对象
		- 静态方法，保存在类中，由类直接调用
		- 类方法，保存在类中，由类直接调用，cls-->当前类

### 应用场景
		如果对象中需要保存一些值，执行某个功能时，需要使用对象中的值 --> 普通方法
		不需要任何对象中的值 --> 静态方法

### 属性、特性
		- 不伦不类




​									
​									
中国的所有省份，用面向对象表示


        class Province:					
            # 静态字段，属于类			
            country = 'China'		
                                        
            def __init__(self,name):
                # 普通字段，属于对象	
                self.name = name	
                                        
        henan = Province("HeNan")	
        hebei = Province("HeBei")


​                                    
​        hebei.name						


​						


#### 一、成员修饰符
	公有成员
	私有成员	__

#### 二、特殊成员
	    __init__	类()自动执行
	    __call__	对象()  类() 自动执行
	    __int__		int(对象)
	    __str__		str(对象)
	
	    __add__
	
	    __dict__	# 讲对象中的封装的所有内容通过字典的形式返回
	    __getitem__	# 切片(slice类型)或者索引
	    __setitem__
	    __delitem__
	
	    __iter__	# 如果类中有__iter__方法，对象-->可迭代对象
	                # 对象，__iter__()的返回值：迭代器
	                # for 循环，迭代器,next
	                # for 循环，可迭代对象，对象，__iter__方法，迭代器，next
	                # 1、执行lioo对象的类ioo类的 __iter__方法，并获取其返回值
	                # 2、循环上一步中返回的对象


#### 三、metaclass，类的祖宗
        a.Python中一切事物皆是对象
        b.
            class Foo:
                pass
    
            obj = Foo()
            # obj是对象，Foo类
            # Foo类也是一个对象，type的对象
    
        c.
            类都是type类的对象	type(..)
            “对象“都是以类的对象 类()


#### 四、异常处理

	raise Exception('数据库处理错误。。。')

#### 五、反射

#### 六、单例模式



================================

        class Foo:
            def func(self):
                print(123)


================================

        def function(self):
            print('1258')
    
        Foo = type('Foo',(object,),{'func':function})
        # type('Foo',(object,),{'func':lambda x:125})	# 声明一个类
        Foo = type('Foo',(object,),{'func':lambda x:125})
        obj = Foo()
    
    # 声明了一个类



################################
