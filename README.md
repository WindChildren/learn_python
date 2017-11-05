# learn_python
python学习笔记

## 第一章
 1. 环境输出
 `>>>len("python")`
`6`
在python shell 下是交互环境，默认自己支持输出。
`print(len("python"))`
模块中，需要用print 语句输出结果。
 2. 基本元素
Python里所有数据都是以对象形式存在的。
内置数据类型包括：
布尔型（仅包括True和False两种取值）

整型（整数，如42）

浮点型（小数，或用科学计数法表示的数字，例如1.0e8，它表示1乘以10的8次方）

字符串型（字符组成的序列）。
	1.  type( thing )
	`print(type(3))`
	得到输出
	`<class 'float'>`
	2.  命名规范
	变量名只能是小写字母、大写字母、数字和下划线。关键字不能作为变量名。
	3. 整数
	数字前加一个负号可以定义一个负数，可以进行连续运算：
	`>>>5  + 9  - 2 + 1 - 6 `
	`17`
	* / 用来执行浮点数除法
	* // 用来执行整数除法
	百分号 % 在Python在两个数字之间代表求模运算，得到余数
	* 使用下面方法可以同时得到余数和商
	`>>>divmod(9, 5)`
	`(1,4)`
	4. 基数
	整数默认为十进制数，可以在数字前添加前缀，显示地指定其他基数。
	* 0b 或 0B 代表二进制
	* 0o 或 0O 代表八进制
	* 0x 或 0X 代表十六进制
	5. 类型转换
	使用int()函数将其他数据类型转换为整数，小数点后的会被舍去，无法将与数字无关的数据转换为整型。
	
	使用str()将数据类型转换为字符串。
	
	在使用不同数字类型进行计算的时候，python会自动进行类型转换。
	
	Python可以处理超大型数据而不会报错。
	6. 数学函数
	7. 使用引号创建
	可以使用连续三个单引号或者双引号创建字符串，三元引号多用于创建多行的字符串。
	
	```
	>>>poem = ''' There was a Young Lady of Norway,
	... Who casually sat in a doorway;'''
	```
	8. 基本方法和符号的使用
	* 使用\转义
	字符前面添加\会使该字符的意义发生改变，如：\n, 有时会用到 \' 和 \" 来表示单、双引号。
	
	`>>>testimony = "\" I did nothing! \" he said. \" Not that either! Or the other thing.\" "` 
	
	`>>>print(testimony)`
	
	`" I did nothing! " he said. "Not that either! Or the other thing." `
	
	如需要输出一个\,连续输入两个\\即可
	* 使用+拼接
	* 使用*复制
	
	`start = 'Na' * 4` 
	
	`print(start)`
	
	`Na Na Na Na`
	* 使用[]提取字符
	
	`>>>letters = 'abcdefghijklmnopqrstuvwxyz'`
	
	`letters[0]`
	
	`'a'`
	* 使用[start：end：step]分片
	从start提取到end - 1, 每step个字符提取一个
	* 使用len()获得长度
	* 使用split()分割
	
	`tools = 'get gloves, get mask, give cat vitamins, call ambulance'`
	
	`print(tools.split(','))`
	
	`['get gloves', ' get mask', ' give cat vitamins', ' call ambulance']`
	
	若不指定分隔符，split()默认使用空白字符——换行符、空格、制表符
	* 使用join()合并
	`tools_list = ['get gloves', ' get mask', ' give cat vitamins', ' call ambulance']`
	`print(','.join(tools_list))`
	`get gloves, get mask, give cat vitamins, call ambulance`
	其他字符函数详见标准文档[1] : (https://docs.python.org/3/library/stdtypes.html#string-methods)
	## 第二章
	