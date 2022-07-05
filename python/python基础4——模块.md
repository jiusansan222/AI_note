---
title: python基础4——模块

date: 2022-7-3 10:59:20

updated: 2022-7-3 10:59:20

tags:

- python语言

categories:

- [编程语言, python, python快速入门]

---

## python基础4——模块

#### 一、模块

+ 模块是一个包含定义的函数和变量的文件，其后缀名是.py。也就是说，一个python文件就是一个模块。

+ `import`语句
  
  + 语句的一般写法如下，当python解释器扫描到import语句后，会按照一定的路径进行扫描。扫描顺序与python的搜索路径有关
    
    ```python
    import moudule1,[[module2],[module3],...]
    ```
  
  + python的搜索路径：搜索路径是由一系列目录名组成的，可以通过以下代码获取。`sys.path`会获取到一个目录列表，第一项是空串，代表当前目录。当import模块时，python解释器会依次从目录中搜索所引入的模块。
  
  ```python
  >>> import sys
  >>> sys.path
  ['', 'D:\\software\\Anaconda3\\envs\\python_learn\\python38.zip', 'D:\\software\\Anaconda3\\envs\\python_learn\\DLLs', 'D:\\software\\Anaconda3\\envs\\python_learn\\lib', 'D:\\software
  \\Anaconda3\\envs\\python_learn', 'D:\\software\\Anaconda3\\envs\\python_learn\\lib\\site-packages']
  ```

+ `from ... import ...`语句
  
  +  from 语句可以从模块中导入一个指定的部分到当前命名空间中
  
  + 这个声明不会把整个模块导入到当前的命名空间中，它只会将指定的函数引入进来。
  
  + `from ... import *`可以导入一个模块中的所有项目。

+ 深入模块
  
  + `__name__`属性:该属性可以使该程序块仅在该模块自身运行时执行，在被引入时不执行。
  
  + `dir()`函数：内置的函数 dir() 可以找到模块内定义的所有名称。以一个字符串列表的形式返回
  
  ```python
  >>> import sys
  >>> dir(sys)
  ['__breakpointhook__', '__displayhook__', '__doc__', '__excepthook__', '__interactivehook__', '__loader__', '__name__', '__package__', '__spec__', '__stderr__', '__stdin__', '__stdout_
  _', '__unraisablehook__', '_base_executable', '_clear_type_cache', '_current_frames', '_debugmallocstats', '_enablelegacywindowsfsencoding', '_framework', '_getframe', '_git', '_home',
   '_xoptions', 'addaudithook', 'api_version', 'argv', 'audit', 'base_exec_prefix', 'base_prefix', 'breakpointhook', 'builtin_module_names', 'byteorder', 'call_tracing', 'callstats', 'co
  pyright', 'displayhook', 'dllhandle', 'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix', 'executable', 'exit', 'flags', 'float_info', 'float_repr_style', 'get_asyncgen_hoo
  ks', 'get_coroutine_origin_tracking_depth', 'getallocatedblocks', 'getcheckinterval', 'getdefaultencoding', 'getfilesystemencodeerrors', 'getfilesystemencoding', 'getprofile', 'getrecu
  rsionlimit', 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettrace', 'getwindowsversion', 'hash_info', 'hexversion', 'implementation', 'int_info', 'intern', 'is_finalizing', 'maxs
  ize', 'maxunicode', 'meta_path', 'modules', 'path', 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'ps1', 'ps2', 'pycache_prefix', 'set_asyncgen_hooks', 'set_coroutine_orig
  in_tracking_depth', 'setcheckinterval', 'setprofile', 'setrecursionlimit', 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout', 'thread_info', 'unraisablehook', 'version', 've
  rsion_info', 'warnoptions', 'winver']
  ```
  
  + 标准模块：Python 自带一些标准模块库，比如sys

+ 使用模块的好处
  
  + 提高代码的可维护性
  
  + 代码不必从0开始编写，可以通过引用模块来完成

#### 二、包

+ 包是管理组织模块的一种形式，采用"点模块名称"，比如A.B表示A包中的子模块B

+ 下面表示了一种可能的包结构，是一个多级层次的包结构。每一个包目录下面都会有一个`__init__.py`的文件，该文件可以为空，也可以写一些初始化代码

```python
sound/                          顶层包
      __init__.py               初始化 sound 包
      formats/                  文件格式转换子包
              __init__.py
              wavread.py
              ...
      effects/                  子包
              __init__.py
              echo.py
              main.py
              ...
      filters/                  子包
              __init__.py
              equalizer.py              ...
```

+ 包同样是通过`import`语句来导入，比如`import sound.effects.echo`，这时会导入子模块sound.effects.echo，访问时也必须用全名sound.effects.echo

+ 通过`from ... import ...`也可以访问，比如`from sound.effects import echo`可以导入子包sound.effects.echo，访问时只需叫echo即可

+ `__init__.py`：
  
  + `__all__`列表变量：通过指定该列表变量，可以在使用`from ... import * `导入包时，只导入指定内容
  + `__path__`：目录列表

+ 路径问题:sparkling_heart:
  
  路径的查找中的当前路径都是针对入口模块的，即主模块`"__main__"`
  
  + 绝对路径导入：从sys.path中各个路径中按顺序查找包或模块
  
  ```python
  import subeffect.surround
  import sound.filters.equalizer
  import sound.formats.wavread
  ```
  
  + 相对路径导入：导入当前包（本代码文件）上下级的包，使用’.'作为标记。一个点表示当前路径，二个点表示上一层路径。
    + `from . import module_name`导入和自己同目录下的模块。
    + `from .package_name import module_name`导入和自己同目录的包的模块。
    + `from .. import module_name`导入上级目录的模块。
    + `from ..package_name import module_name`导入位于上级目录下的包的模块。
    + 每多一个点就多往上一层目录
    + 入口文件最好不用相对导入，比较麻烦
  
  ```python
  from . import echo
  from .. import filters
  from ..formats import wavreader
  ```
  
  + 当所导入的包与当前模块包不在同一个文件夹下时，用`sys.path.append()`添加目录
  
  ```python
  import sys
  sys.path.append(<TARGET_PARENT_PATH>)
  import <FILE_STEM>
  ```
