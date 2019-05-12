### 函数

#### 数学定义的函数与python中的函数
初中数学函数定义：一般的，在一个变化过程中，如果有两个变量x和y，并且对于x的每一个确定的值，y都有唯一确定的值与其对应，那么我们就把x称为自变量，把y称为因变量，y是x的函数。自变量x的取值范围叫做这个函数的定义域

例如y=2*x

python中的函数定义

```
python中函数定义方法：
 
def test(x):
    "The function definitions"
    x+=1
    return x
     
def:定义函数的关键字
test：函数名
（）：内可定义形参
"":文档描述（非必要，但是强烈建议为你的函数添加描述信息）
x+=1：泛指代码块或程序处理逻辑
return：定义返回值


调用运行：可以带参数也可以不带
函数名()

```
函数式编程就是：先定义一个数学函数(数学建模)，然后按照这个数学模型用编程语言去实现它。至于具体如何实现和这么做的好处，且看后续的函数式编程。

#### 函数使用的好处
总结使用函数的好处：

1.代码重用

2.保持一致性，易维护

3.可扩展性

#### 函数与过程

过程定义：过程就是简单特殊没有返回值的函数

这么看来我们在讨论为何使用函数的的时候引入的函数，都没有返回值，没有返回值就是过程，没错，但是在python中有比较神奇的事情

```
def fun():
    msg='hekko'
    return msg

def fun1():
   return 0
def fun2():
    return 0,10,'yyyy'

t=fun()
t1=fun1()
t2=fun2()
print (t)
print (t1)
print (t2)
```
结果

```
hekko
0
(0, 10, 'yyyy')  --元祖
```
总结：

返回值数=0(也就是没有返回值):返回None

返回值数=1(只返回一个值):返回object

返回值数>1(返回多个值):返回tuple

函数的参数

普通参数

默认参数

动态参数

```
普通参数

# ######### 定义函数 ######### 

# name 叫做函数func的形式参数，简称：形参
def func(name):
    print name

# ######### 执行函数 ######### 
#  'wupeiqi' 叫做函数func的实际参数，简称：实参
func('wupeiqi')

普通参数
```

==默认参数必须放在参数列表最后==
```
默认参数
def func(name, age = 18):
    
    print "%s:%s" %(name,age)

# 指定参数
func('wupeiqi', 19)
# 使用默认参数
func('alex')

注：默认参数需要放在参数列表最后

```
动态参数
```
def func(*args):

    print args


# 执行方式一
func(11,33,4,4454,5)

# 执行方式二
li = [11,2,2,3,3,4,54]
func(*li)


----------------------
def func(**kwargs):

    print args
# 执行方式一
func(name＝'wupeiqi',age=18)

# 执行方式二
li = {'name':'wupeiqi', age:18, 'gender':'male'}
func(**li)


```
一般写法
```
def func(*args, **kwargs):

    print args
    print kwargs

```

#### 局部变量与全局变量

在子程序中定义的变量称为局部变量，在程序的一开始定义的变量称为全局变量。

全局变量作用域是整个程序，局部变量作用域是定义该变量的子程序。

当全局变量与局部变量同名时：

在定义局部变量的子程序内，局部变量起作用；在其它地方全局变量起作用。

#### ==前向引用之'函数即变量==  ------>理解

函数调用函数的时候,只要被调用的函数已经被被定义，就可以进行调用

```
第一种

def action():
    print ('in the action')
    logger()

def logger():
    print ('rrrr')

action()   可以

第二种


def logger():
    print ('rrrr')
    
def action():
    print ('in the action')
    logger()

action()   可以

第三种
def action():
    print ('in the action')
    logger()

action()   不可以会报错

```
#### 嵌套函数和作用域

嵌套函数作用域以上级为准


#### 匿名函数

lambda表达式

```
学习条件运算时，对于简单的 if else 语句，可以使用三元运算来表示，即：


# 普通条件语句
if 1 == 1:
    name = 'wupeiqi'
else:
    name = 'alex'
  
# 三元运算
name = 'wupeiqi' if 1 == 1 else 'alex'
对于简单的函数，也存在一种简便的表示方式，即：lambda表达式

# ###################### 普通函数 ######################
# 定义函数（普通方式）
def func(arg):
    return arg + 1
  
# 执行函数
result = func(123)
  
# ###################### lambda ######################
  
# 定义函数（lambda表达式）
my_lambda = lambda arg : arg + 1
  
# 执行函数
result = my_lambda(123)
lambda存在意义就是对简单函数的简洁表示
```

内置函数

map

遍历序列，对序列中每个元素进行操作，最终获取新的序列

[map图](https://images2015.cnblogs.com/blog/425762/201511/425762-20151114164016869-1553913346.png)

```
li = [11, 22, 33]

new_list = map(lambda a: a + 100, li)
```
filter

对于序列中的元素进行筛选，最终获取符合条件的序列

[filter图](https://images2015.cnblogs.com/blog/425762/201511/425762-20151114164107884-344713622.png)

```
li = [11, 22, 33]

new_list = filter(lambda arg: arg > 22, li)

#filter第一个参数为空，将获取原来序列
```

reduce

reduce在python2中可以直接使用，但是在python3中需要导入模块

```
from functools import reduce
li = [11, 22, 33]

result = reduce(lambda arg1, arg2: arg1 + arg2, li)

# reduce的第一个参数，函数必须要有两个参数
# reduce的第二个参数，要循环的序列
# reduce的第三个参数，初始值
```

内置函数

[内置函数图](https://images2015.cnblogs.com/blog/1036857/201611/1036857-20161129121211131-1892084999.png)

常用内置函数用法简介

max/min

==max(iterable, key, default) 求迭代器的最大值，其中iterable 为迭代器，max会for i in … 遍历一遍这个迭代器，然后将迭代器的每一个返回值当做参数传给key=func 中的func(一般用lambda表达式定义) ，然后将func的执行结果传给key，然后以key为标准进行大小的判断。最后的输出是输出迭代器的结果==

```
字典的运算：最小值，最大值，排序
salaries={
    'egon':3000,
    'alex':100000000,
    'wupeiqi':10000,
    'yuanhao':2000
}

迭代字典，取得是key，因而比较的是key的最大和最小值
>>> max(salaries)
'yuanhao'
>>> min(salaries)
'alex'

可以取values，来比较
>>> max(salaries.values())
100000000
>>> min(salaries.values())
2000
但通常我们都是想取出，工资最高的那个人名，即比较的是salaries的值，得到的是键
>>> max(salaries,key=lambda k:salary[k])
'alex'
>>> min(salaries,key=lambda k:salary[k])
'yuanhao'
```
#### all()　　

接受一个迭代器，如果迭代器的所有元素都为真，那么返回True，否则返回False

```
>>> tmp_1 = ['python',123]
>>> all(tmp_1)
True
>>> tmp_2 = []
>>> all(tmp_2)
True
>>> tmp_3 = [0]
>>> all(tmp_3)
False
```

#### any()　　
 
 接受一个迭代器，如果迭代器里有一个元素为真，那么返回True,否则返回False
 
#### bin()
 
#### oct()
 
#### hex() 
 
 三个函数功能为：将十进制数分别转换为2/8/16进制。
 
#### bytes()　　

将一个字符串转换成字节类型
 
```
 >>> s = bytes(a, encoding='utf-8')
>>> s
b'\xe7\x8e\x8b'
```
 
#### challable()　　

判断对象是否可以被调用，能被调用的对象就是一个callables对象，比如函数和带有__call__()的实例

```
>>> callable(max)
True
>>> callable([1, 2, 3])
False
>>> callable(None)
False
>>> callable('str')
False
```

#### dir()　　

不带参数时返回当前范围内的变量，方法和定义的类型列表，带参数时返回参数的属性，方法列表


```
>>> dir()
['__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__', 'li', 'li1', 'li2', 'li_1']
>>> dir(list)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']

```

#### enumerate()　　
 
 返回一个可以枚举的对象，该对象的next()方法将返回一个元组
 
```
 >>> test = ['a', 'b', 'c']
>>> for k,v in enumerate(test):
    print(k,v)
 
# 输出结果：
(0,a)
(1,b)
(2,c)

```
 
#### format()　　

格式化输出字符串

三种形式

```
t = [11, 22, 33, 44]

print ("{},{}".format(t[0],t[1]))

print ("{1},{0}".format(t[0],t[1]))

print('{name} {age}'.format(age=t[0],name=t[1]))
```

#### isinstance()　　

检查对象是否是类的对象，返回True或False

```
 isinstance(obj, cls)
 检查obj是否是类cls的对象, 返回True 或 False
class Foo(object):
     pass
 obj = Foo()
 isinstance(obj, Foo)

```
#### issubclass()　　
 
 检查一个类是否是另一个类的子类。返回True或False

#### sorted()

首先讲解与list.sort()区别

主要的区别在于，list.sort()是对已经存在的列表进行操作，进而可以改变进行操作的列表。而内建函数sorted返回的是一个新的list，==而不是在原来的基础上进行的操作.==

```
sorted('可迭代序列',key=func,reverse)
其中key=func的原理跟max一样

>>>l=[('a', 1), ('b', 2), ('c', 6), ('d', 4), ('e', 3)]
>>>sorted(l, key=lambda x:x[0])
Out[39]: [('a', 1), ('b', 2), ('c', 6), ('d', 4), ('e', 3)]
>>>sorted(l, key=lambda x:x[0], reverse=True)
Out[40]: [('e', 3), ('d', 4), ('c', 6), ('b', 2), ('a', 1)]
>>>sorted(l, key=lambda x:x[1])
Out[41]: [('a', 1), ('b', 2), ('e', 3), ('d', 4), ('c', 6)]
>>>sorted(l, key=lambda x:x[1], reverse=True)
Out[42]: [('c', 6), ('d', 4), ('e', 3), ('b', 2), ('a', 1)]


```

#### zip()　　
 
 将对象逐一配对
 
```
 list_1 = [1,2,3]
list_2 = ['a','b','c']
s = zip(list_1,list_2)
print(list(s))
 
运行结果：
 
[(1, 'a'), (2, 'b'), (3, 'c')]

```

zip()是Python的一个内建函数，它接受一系列可迭代的对象作为参数，将对象中对应的元素按顺序组合成一个tuple，每个tuple中包含的是原有序列中对应序号位置的元素，然后返回由这些tuples组成的list。若传入参数的长度不等，则返回list的长度和参数中长度最短的对象相同。在所有参数长度相同的情况下，zip()与map()类似，没有参数的情况下zip()返回一个空list。

利用*号操作符，可以将list unzip（解压成单独的序列）


```
#反解
c=[(1, 'A'), (2, 'B'), (3, 'C')]
s1,s2=zip(*c)
print (list(s1))
print (list(s2))

输出结果
[1, 2, 3]
['A', 'B', 'C']

```
