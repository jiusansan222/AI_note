---
title: python基础3——函数

date: 2022-7-1 10:59:20

updated: 2022-7-1 10:59:20

tags:

- python语言

categories:

- [编程语言, python, python快速入门]

---

## python基础3——函数

#### 一、定义函数

+ 一般函数语法
  
  + 关键词为`def`，后接函数名称和圆括号
  
  + 圆括号中定义参数
  
  + 结束函数时为 `return [表达式]`，可以同时返回多个值，此时会变成一个tuple

```python
def abs_my(x):
    if x > 0:
        return x
    else:
        return -x
```

+ 匿名函数
  
  + 使用 `lambda` 可以创建匿名函数。
  
  + 函数主体是一个表达式，而不是代码块
  
  + 语法：`lambda [arg1 [,arg2,.....argn]]:expression`

```python
sum = lambda arg1, arg2: arg1 + arg2

# 调用sum函数
print ("相加后的值为 : ", sum( 10, 20 ))
print ("相加后的值为 : ", sum( 20, 20 ))

# 输出
相加后的值为 :  30
相加后的值为 :  40


# 使用同样的代码来创建多个匿名函数
def myfunc(n):
  return lambda a : a * n

mydoubler = myfunc(2)
mytripler = myfunc(3)

print(mydoubler(11))
print(mytripler(11))

# 输出
22
33
```

#### 二、调用函数

+ 函数定义好后，可以在另一个函数里调用执行

+ python也内置了非常多有用的函数，可以直接调用，数据类型转换函数就是常用的一个内置函数

+ 在调用函数时，一定注意参数的传递是否正确（个数、类型），否则会出现`TypeError`的问题

#### 三、函数的参数

+ 可更改与不可更改对象
  
  + 可变类型： list,dict 等是可以修改的对象，传递这类对象时，被调用函数内部发生改变，原始参数也会改变
  
  + 不可变类型：strings, tuples, 和 numbers 是不可更改的对象，传递这类对象时，被调用函数内部发生改变，原始参数不会改变

+ 参数类型
  
  + 必需参数
    
    + 必须以正确的顺序传入函数。调用时的数量必须和声明时的一样。
  
  + 关键字参数
    
    + 使用关键字参数允许函数调用时参数的顺序与声明时不一致
  
  + 默认参数
    
    + 调用函数时，如果没有传递参数，则会使用默认参数。
  
  + 不定长参数
    
    + 需要一个函数能处理比当初声明时更多的参数时会用到不定长参数，它声明时不会命名。基本语法如下，
    + 加了星号 `*` 的参数会以元组(tuple)的形式导入，存放所有未命名的变量参数，一般写作`*Args`，星号也可以单独出现
    + 加了两个星号 `**` 的参数会以字典的形式导入，一般写作`**kw`。

```python
def printinfo( arg1, *vartuple ):
   "打印任何传入的参数"
   print ("输出: ")
   print (arg1)
   for var in vartuple:
      print (var)
   return

# 调用printinfo 函数
printinfo( 10 )
printinfo( 70, 60, 50 )

输出:
10
输出:
70
60
50
```
