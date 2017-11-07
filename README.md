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

* 布尔型（仅包括True和False两种取值）

* 整型（整数，如42）

* 浮点型（小数，或用科学计数法表示的数字，例如1.0e8，它表示1乘以10的8次方）

* 字符串型（字符组成的序列）。

	1. type( thing )
	
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

1. Python序列结构：字符串、元组和列表。

2. Python容器：列表、元组、字典与集合。

3. 列表创建：使用[]或者list()

```
>>> another_empty_list = list()

>>> another_empty_list

[]
```

* 列表有顺序，允许列表中的值重复。

* 使用list()可以将其他数据类型转换成列表

字符串转换为列表：

```
print(list('cat'))

['c', 'a', 't']
```

元组转换为列表：
```
a_tuple = ('ready', 'file', 'aim')

print(list(a_tuple))
```

* 使用split()可以依据分隔符将字符串切割成若干个字串组成的列表

* 使用[offset]修改和获取元素

```
marxes = ['Groucho', 'Chico', 'Harpo']
marxes[2] = 'Wanda'
print(marxes[0], marxes[2])

Groucho Wanda
```
负偏移量代表从尾部开始计数。

指定的偏移量对于待访问列表必须有效，否则会报错。

* 包含列表的列表

```
small_birds = ['humminhbird', 'finch']

extinct_birds = ['dodo', 'passenger piggeon', 'Norwegian Blue']

carol_birds = [3, 'Frennch hens', 2, 'turtledoves']

all_birds = [small_birds, extinct_birds, 'macaw', carol_birds]

print(all_birds)

print(all_birds[0])

print(all_birds[1][0])


[['humminhbird', 'finch'], ['dodo', 'passenger piggeon', 'Norwegian Blue'], 'macaw', [3, 'Frennch hens', 2, 'turtledoves']]

['humminhbird', 'finch']

dodo
```

* 使用范围并使用切片提取元素 

```
marxes = ['Groucho', 'Chico', 'Harpo']

print(marxes[0:2])      #步长为1

print(marxes[0::2])     #步长为2

#利用切片实现列表逆序

print(marxes[ ::-1])


['Groucho', 'Chico']

['Groucho', 'Harpo']

['Harpo', 'Chico', 'Groucho']


```

* 使用append()添加元素至尾部

```
marxes = ['Groucho', 'Chico', 'Harpo']

marxes.append('Zeppo')

print(marxes)


['Groucho', 'Chico', 'Harpo', 'Zeppo']
```

* 使用extend()或者+=合并列表

```
marxes = ['Groucho', 'Chico', 'Harpo']

other = ['Gummo','Karl']

marxes.extend(other)        #使用marxes += other得到相同结果

print(marxes)

['Groucho', 'Chico', 'Harpo', 'Gummo', 'Karl']
```

* 使用insert()在指定位置插入元素

```
marxes = ['Groucho', 'Chico', 'Harpo']

marxes.insert(2, 'Gummo')       #制定偏移量为0，可以插入列表头部，如果超过尾部，则会插入到列表最后

print(marxes)

```

* 使用del删除指定位置的元素

`marxes = ['Groucho', 'Chico', 'Harpo']`

`del marxes[1]`

当列表中的一个元素被删除后，位于它后面的元素会自动往前移动填补，且列表的长度减1

* 使用remove()删除具有指定值的元素

`marxes = ['Groucho', 'Chico', 'Harpo']`

`marxes.remove('Harpo')`

* 使用pop()获取并删除指定位置的元素

如果指定了偏移量，则返回指定偏移量的值，否则默认为-1.

```

marxes = ['Groucho', 'Chico', 'Harpo']

marxes.pop()

print(marxes)

print(marxes.pop())


['Groucho', 'Chico']

Chico
```

* 使用index()查询具有特定元素的位置

```
marxes = ['Groucho', 'Chico', 'Harpo']

print(marxes.index('Chico'))

1
```

* 使用in判断值是否存在

```
marxes = ['Groucho', 'Chico', 'Harpo']

print('Chico' in marxes)

True
```

* 使用count()记录特定值出现的次数

```
marxes = ['Groucho', 'Chico', 'Harpo']

print(marxes.count('Chico'))
```

