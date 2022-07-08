```yaml
title: python基础6——错误和异常

date: 2022-7-8 10:59:20

updated: 2022-7-8 10:59:20

tags:

- python语言

categories:

- [编程语言, python, python快速入门]
```

## python基础6——错误和异常

python内置一套异常处理机制，可以用来处理代码运行中出现的各种问题。如果发生异常而没有处理，程序就会停止。

异常处理的大致步骤是：定义（内置的无需再次定义）-> 捕捉

#### 一、异常定义

+ 内置
  
  + 在Python中，异常也是对象，可对它进行操作。BaseException是所有内置异常的基类
  
  + Python自动将所有异常名称放在内建命名空间中，所以程序不必导入exceptions模块即可使用异常。
  
  + 常见的错误类型
    
    + `ValueError`：当数据类型错误时产生的错误类
    
    + `KeyError`：当查询无效的字典key时产生的错误类
    
    + `FileNotFoundError`：当使用了不存在的文件时产生的错误类型

+ 用户自定义
  
  + 异常类也可以自行创建。这个类需要继承自 Exception 类，可以直接继承，或者间接继承
  
  + 例子
    
    ```python
    class MyError(Exception):
        def __init__(self, value):
            self.value = value
        def __str__(self):
            return repr(self.value)
    ```

#### 二、异常捕捉

+ `try 执行代码 /expect 异常时执行的代码`
  
  + 执行逻辑
    
    + 执行`try`部分，若无异常发生，则执行完`try`部分后结束
    
    + 执行`try`部分，若在某句发生异常，余下语句会被忽略
      
      + 异常类型与`expect`后的名称匹配，执行`expect`语句
      
      + 不匹配，则会传递给上层的`try`
  
  + 一个 try 可以包含多个except子句，分别来处理不同的特定的异常，但最多只有一个分支会被执行
  
  + 最后一个except子句可以忽略异常的名称，它将被当作通配符使用。可以使用这种方法打印一个错误信息，然后再次把异常抛出。
  
  ```python
  import sys
  
  try:
      f = open('myfile.txt')
      s = f.readline()
      i = int(s.strip())
  except OSError as err:
      print("OS error: {0}".format(err))
  except ValueError:
      print("Could not convert data to an integer.")
  except:
      print("Unexpected error:", sys.exc_info()[0])
      raise
  ```

+ `try 执行代码 /except 异常时执行的代码 /else 未发生异常时执行的代码`
  
  + 使用 else 子句可以避免一些意想不到，而 except 又无法捕获的异常

+ `try / finally` :清理行为
  
  + `finally`语句无论是否发生异常都将执行最后的代码。

#### 三、异常抛出

+ 程序中的异常不仅可以自动触发，还可以由开发人员使用`raise`语句和`assert`语句主动抛出。对于自定义异常只能由手动抛出。

+ `raise`语法
  
  + `raise [Exception [, args [, traceback]]]`
  
  + 参数：异常的实例或者是异常的类
  
  + 如果只想知道这是否抛出了一个异常，只要原样返回而并不处理，那么使用`raise` 即可，不需要参数。
  
  + 例子
    
    ```python
    x = 10
    if x > 5:
        raise Exception('x 不能大于 5。x 的值为: {}'.format(x))
    ```

+ `assert`语法：断言
  
  + `assert 表达式[,异常信息]`
  
  + 表达式的值为False时触发AssertionError异常，值为True时不做任何操作
  
  + 例子:
    
    ```
    assert n != 0, 'n is zero!'
    ```


