#初识Python

python的语法总体来说比较简单优雅

## 创建简单的列表

​	`movies = ["The Holy Grail" , "The Life of Brian", "The Meaning of Life"]`

**python中的变量并不用声明数据类型**

**Python中对列表的处理：**

* `movies.append(i)`
* `movies.insert(i,"")`
* `movies.remove(i)`
* `print(movies[i])`
* `movies[i] = " "`

## 列表的嵌套，如何输出列表中的数据

`for`循环

```python
movies = ["The holllyGrail",1975,"Therry Jones & Terry Gilliam",91,["Graham Chapman",["Michael Palin","John Cleese","Tery Graillam"]]]

```

```python
for each_item in movies:
  if isinstance(each_item,list):
    for vested_item in each_item:
      print(vested_item)
  else:
    print(each_item)
```

 `while`循环类似

# 创建自己的模块

## 创建函数

> 上面的问题看似得到了解决,然而当里表的数据再一次嵌套时，我们的代码也需要随之改变，复杂度会很高，代码的重复度也会很高，因此我们需要一个函数来帮助我们在实现功能的同事，不需要对代码进行改动

> `version1.0`

``````python
def print_lol(the_list):
  for each_item in the_list:
    if isinstance(each_item,list):
      print_lol(each_item)
    else:
      print(each_item)
      
``````

> 通过一个上面的递归函数，我们解决了列表的嵌套输出问题，当列表有多层嵌套时，我们不需要在改动我们的代码

## 新的需求

> 如果我希望在输出时通过输出可以看出列表之间的嵌套关系，又该如何？

> 增加函数的参数控制
>
> 通过一个level参数，输出时用`tab`键来显示列表之间的层次

> `version1.1`

```python
def print_lol(the_list,level):
  for each_item in the_list:
    if isinstance(each_item,list):
      print_lol(each_item,level + 1)
    else:
      for tab_stop in range(level):
        print("\t",end='')
      print(each_item)
```

> 新版本的的`print_lol()`提供了嵌套显示的功能，但是在你发布之后，调用`version1.0`函数的用户却不能再正常使用

> 解决方法：赋予`level`一个默认值为0，即`level = 0`

> `version1.2`

```python
def print_lol(the_list,level = 0):
  for each_item in the_list:
    if isinstance(each_item,list):
      print_lol(each_item,level + 1)
    else:
      for tab_stop in range(level):
        print("\t",end='')
      print(each_item)
```

>虽然现在所有的人调用它都能work了，但是所有的显示都必须缩进了。那么那些不想缩进显示的用户又该如何？

> How to do?
>
> 再增加一个参数用于控制是否开启`tab`缩进显示

> `version2.0`

```python
def print_lol(the_list,indent = False,level = 0):
  for each_item in the_list:
    if isinstance(each_item,list):
      print_lol(each_item,indent,level + 1)
    else:
      if indent:
      	for tab_stop in range(level):
        	print("\t",end='')
      print(each_item)
```

> 至此，`print_lol()`函数可以满足大多数用户的需要

# 其他一些小事情 :happy:

## 注释

> Python中的注释可以是"#" `````

## 发布自己的代码

1.创建自己的文件夹，将`Python`文件复制到其中

2.在文件夹中创建一个`setup.py` 文件



```python
from distutils.core import setup

setup(
  name         = "",
  version      = "1.0.0",
  py_modules   = [''],
  autoor       = 'hfpython',
  author_email = 'xxxxxx.com',
  url          = 'https://www.ddddd.com'
  description  = 'A simple printer of nested lists' 
  
)
```

3.构建一个发布文件

`python3 setup.py sdist`

4.将发布安装到你的`Python`本地副本中

`sudo python3 setup.py install`

# 思考

> 1.通过对`Python`的学习，主要学习了`Python`对列表的处理
>
> 2.通过对函数模块的学习，我们除了代码的实现本身之外，我们更应该思考的是如何设计我们的模块，代码的可用性，复用性，以及版本更新时兼容性的控制，怎样使代码更加易用。当我们设计一个复杂的系统时，这些考量都是十分必要且重要的，可以帮助我们节省成本，减少错误的发生。:smiley:





