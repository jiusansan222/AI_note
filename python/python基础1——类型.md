## python基础1——类型

  计算机是用于处理数值计算的机器，编程语言也需要能处理各种各样的数据。本节介绍python中基础的数据类型及相关方法。

#### 一、数字

+ **整数（int， long）**：包括正整数、0、负整数。
  
  + 可以有不同进制的写法，用不同的前缀来区分。
  
  + 可以进行+-*/的运算操作，运算结果总是精确的
  
  + 可以用`_`来区分比较大的数，方式如下所示（同样适用于浮点数）：

```python
1000 # 10进制整数
0xff # 16进制整数，以0x为前缀
1000000000 = 1_000_000_000
```

+ **浮点数（float）**：也就是小数。
  
  + 浮点：小数点可以出现在数的任何位置
  
  + 对于非常大或者非常小的浮点数，python会用科学计数法的形式进行标识
  
  + 同所有语言一样，浮点数运算可能存在四舍五入的误差
  
  + 任意两数相除，结果总是浮点数
  
  + 其他运算中，只要存在操作数是浮点数，结果也总是浮点数

```python
  >>> 4/2
  2.0
  >>> 1+2.0
  3.0
  >>> 2*3.0
  6.0
  >>> 3**2.0
  9.0
```

+ **复数（complex）**：复数由实数部分和虚数部分构成
  + 可以用 `a + bj`,或者 `complex(a,b)` 表示
  + 复数的实部 a 和虚部 b 都是浮点型。

#### 二、字符串

- 一系列由字母、数字、下划线组成的字符，在python中可以用单引号或者双引号标识，这两者并无区别。
+ 字符编码问题
  
  - 几种编码方式：
    
    - `ASCII`编码， `GB2312`编码：只能处理单一语言的编码问题，比如英文、中文等，多语言混合文本中会出现乱码问题
    
    - `Uniocde`字符集 ：统一编码，但占用存储空间大
    
    - `UTF-8`编码：可变长编码
    
    - 在计算机内存中统一使用`Unicode`编码，在保存到硬盘或者传输时，就会转换为`UTF-8`编码
  
  - python中，字符串的类型为`str`，但在传输过程中会变为`bytes`,这就是`x=b'ABC'` 与`x='ABC'`的区别

```python
>>> 'ABC'.encode('ascii')
b'ABC'
>>> 'ABC'.encode('utf-8')
b'ABC'
>>> 'ABC'.encode('GBK')
b'ABC'
>>> '你好'.encode('ascii')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)
>>> b'ABC'.decode('ascii')
'ABC'
```

- 在编写python文件时，如代码中含有中文是，就需要指定保存为UTF-8编码，因此通常会在文件开头写下这两行,第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

- 字符串格式化
  
  - 法一：用占位符`%`实现，也可以用来格式化输出
  
  - `format()`
  
  - f-string：字符串开头加f，字符串中的{XXX}自动被变量值替换，XXX是变量名

```python
>>> 'Age: %s. Gender: %s' % (25, True)
'Age: 25. Gender: True

>>> "{} {}".format(111, 'asd')
'111 asd'  

>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
```

- 在python中内置了许多函数以方便使用。
  
  * `len(S)`：返回字符串长度
  
  * `S.split(str，num)`：用指定的分隔符str分割字符串，返回列表
  
  * `S.join(str)`：连接字符串
  
  * `eval(S)`：执行一个字符串表达式，并返回表达式的值
  
  * `exec(S)`：执行存储在字符串或文件中的python语句
  
  * `S.find(str, beg, end)`和`S.index(str, beg, end)`：检索`S[beg, end]`中是否出现find，出现返回起始位置，不出现`find`返回-1,`index`报错
  
  * `S.isxxx()`系列：判断字符串组成类型

```python
>>> eval('1*3+2')
5  

>>> exec('print(123)')
123 

>>> 'Hello zs'.find('zs')
6
>>> 'Hello zs'.index('zs')
6
>>> 'Hello zs'.index('zs',0,5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: substring not found
>>> 'Hello zs'.find('zs',0,5)
-1
```

#### 三、列表list与元组tuple

+ 列表是一个有序的集合，可以包含不同的数据类型，可以随时删除和添加元素，用`[]`标识

+ 列表基本操作
  
  + `len(L)`：求列表的元素个数
  
  + `L[i]`：通过索引访问元素，注意不要越界，正数是正序，负数是逆序。直接赋值可以实现覆盖，使用`del`可以删除
  
  + `L.append(x)`：追加元素至列表末尾
  
  + `L.insert(i, x)`和`L.pop()`：追加元素至指定位置i，删除末尾元素或指定位置元素
  
  + `L.remove(x)`：根据值删除元素
  
  + 列表切割：[头下标:尾下标] 截取相应的列表，从左到右索引默认 0 开始，从右到左索引默认 -1 开始，下标可以为空表示取到头或尾。

+ 组织列表
  
  + L.sort()：对列表进行排序，永久性修改

```python
>>> classmates = ['Michael', 'Bob', 'Tracy']
>>> classmates
['Michael', 'Bob', 'Tracy']  


>>> classmates.sort()
>>> classmates
['Bob', 'Michael', 'Tracy']
```

+ 元组是一个有序集合，可以认为是一种特殊的列表，但初始化后不再能修改，用`()`标识

PS：`(1)`和`(1,)`不同，前者是数字，后者是元组，python为了消歧的规定

#### 四、字典dict

+ 字典是无序的对象集合，通过键来存取，用`{}`来标识

```python
>>> dict = {}
>>> dict['one'] = "This is one"
>>> dict[2] = "This is two"
>>> dict
{'one': 'This is one', 2: 'This is two'}
```
