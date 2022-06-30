---
title: python基础2——控制语句

date: 2022-6-30 10:59:20

updated: 2022-6-30 10:59:20

tags:

- python语言

categories:

- [编程语言, python, python快速入门]

---

## python基础2——控制语句

#### 一、条件控制语句if

+ 一般形式，也可以多层嵌套使用

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

+ python中没有switch语句，可以通过if elif来代替

#### 二、循环语句

+ while语句
  
  + 语法为`while(判断条件)`
  
  + 可以对while循环使用else语句，当while后的条件语句为false时，会执行else的语句块

```python
while <expr>:
    <statement(s)>
else:
    <additional_statement(s)>
```

+ for语句
  
  + 用于遍历任何的可迭代对象，比如字符串或列表

```python
sum = 0
for x in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:
    sum = sum + x
print(sum)
```

+ range()函数可以生成数字序列
  
  + `range(num)`生成从0开始小于num的整数
  
  + `range(num1, num2)`生成从num1开始，小于num2的整数
  
  + `range(num1, num2, stride)`指定步长stride，从num1开始生成，小于num2

+ break语句
  
  + 跳出 for 和 while 的循环体，用于提前结束循环

+ continue语句
  
  + 跳过当前的这次循环，直接开始下一次循环。

+ pass语句
  
  + 空语句，一般用作占位语句，是为了保持程序完整性
