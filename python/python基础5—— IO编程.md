---
title: python基础5——IO编程

date: 2022-7-4 10:59:20

updated: 2022-7-4 10:59:20

tags:

- python语言

categories:

- [编程语言, python, python快速入门]

---

## python基础5—— IO编程

IO编程中，stream是一个很重要的概念。Input Stream是指数据从外界流向内存，Output Stream是指数据从内存流向外界。

#### 一、基本读写

+ 输入
  
  + 接收标准输入：`
    
    + input()`函数代表从标准输入读入一行文本，默认为键盘

+ 输出
  
  + `print()`函数
    
    + `str()`：返回一个用户易读的表达式
    
    + `repr()`：产生一个解释器易读的表示形式
    
    ```python
    >>> str('hello world')
    'hello world'
    >>> repr('hello world')
    "'hello world'"
    ```
  
  +  `str.format()`函数来格式化输出值
    
    + `print('{}'.format('XXX'))`，
    
    + 其中，括号及其里面的字符 (称作格式化字段) 将会被 format() 中的参数替换。
    
    + `{}`中可以记录数字，用于指定传入对象在format中的位置
    
    + 可选项`:`和格式标识符可以跟着字段名，允许对值进行更好的格式化。
    
    ```python
    # 保留小数点后三位
    >>> import math
    >>> print('常量 PI 的值近似为 {0:.3f}。'.format(math.pi))
    
    # 指定宽度
    >>> table = {'Google': 1, 'Runoob': 2, 'Taobao': 3}
    >>> for name, number in table.items():
    ...     print('{0:10} ==> {1:10d}'.format(name, number))
    ...
    Google     ==>          1
    Runoob     ==>          2
    Taobao     ==>          3
    ```

#### 二、文件读写

+ 打开文件
  
  + `f.open(filename, mode)`
    
    + `filename`：文件对象，带路径
    
    + `mode`：r读，w写，a追加，+读写，b以二进制方式打开
    
    + `encoding`参数:要读取非UTF-8编码的文本文件，需要传入`encoding`参数，如读取GBK编码的文件`f = open('gbk.txt', 'r', encoding='gbk')`
    
    + `errors`参数，表示如果遇到编码错误后如何处理。最简单的方式是直接忽略
  
  | 模式    | r   | r+  | w   | w+  | a   | a+  |
  |:-----:|:---:|:---:|:---:|:---:|:---:|:---:|
  | 读     | +   | +   |     | +   |     | +   |
  | 写     |     | +   | +   | +   | +   | +   |
  | 创建    |     |     | +   | +   | +   | +   |
  | 覆盖    |     |     | +   | +   |     |     |
  | 指针在开始 | +   | +   | +   | +   |     |     |
  | 指针在结尾 |     |     |     |     | +   | +   |
  
  + `f.close()`函数
    
    + 文件使用后必须关闭，因此需要调用`close`函数处理
    
    + :exclamation:`with`语句自动调用`close()`方法可以简化写法

```python
with open('/path/to/file', 'r') as f:
  print(f.read())
```

+ 读文件
  
  + `f.read()`：一次性读取文件的全部内容
  
  + `f.readline()`：每次读取一行内容，读到最后一行时，会返回一个空字符串
  
  + `f.readlines()`：一次读取所有内容并按行返回`list`

+ 写文件
  
  + `f.write(string)` 将 string 写入到文件中, 然后返回写入的字符数。

#### 三、序列化：

**<mark>pickle模块</mark>**

+ 序列化
  
  + 将程序中运行的对象信息保存到文件中去，永久存储。
  
  + 语法：`pickle.dump(obj, file, [,protocol])`
  
  ```python
  >>> import pickle
  >>> d = dict(name='Bob', age=20, score=88)
  >>> f = open('dump.txt', 'wb')
  >>> pickle.dump(d, f)
  >>> f.close()
  ```

+ 反序列化
  
  + 从文件中创建上一次程序保存的对象
  
  + 语法：`x = pickle.load(file)`
  
  ```python
  >>> f = open('dump.txt', 'rb')
  >>> d = pickle.load(f)
  >>> f.close()
  ```

**<mark>JSON</mark>**:在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如json，表示出来就是一个字符串

+ 序列化
  
  + python转json对象
  
  + 语法：`jdon.dump()`,会返回一个str，内容就是标准的json
  
  ```
  >>> import json
  >>> d = dict(name='Bob', age=20, score=88)
  >>> json.dumps(d)
  ```

+ 反序列化
  
  + JSON反序列化为Python对象
  
  + 语法：`json.load()`函数
  
  ```python
  >>> json_str = '{"age": 20, "score": 88, "name": "Bob"}'
  >>> json.loads(json_str)
  {'age': 20, 'score': 88, 'name': 'Bob'}
  ```
