### 类的特殊成员

####  __doc__

```
__doc__  表示类的描述信息
```
例子

```
class Foo:
    """ 描述类信息，这是用于看片的神奇 """

    def func(self):
        pass

print Foo.__doc__
#输出：类的描述信息
```
类的描述信息不能被继承

```
class Foo:
    '我是描述信息'
    pass

class Bar(Foo):
    pass
print(Bar.__doc__) #该属性无法继承给子类

该属性无法被继承
```
#### module/class

```
2. __module__ 和  __class__ 

　　__module__ 表示当前操作的对象在那个模块

　　__class__     表示当前操作的对象的类是什么

```

例子

```
#!/usr/bin/env python
# -*- coding:utf-8 -*-

class C:

    def __init__(self):
        self.name = 'zdk'

lib/aa.py
```

```


from lib.aa import C

obj = C()
print obj.__module__  # 输出 lib.aa，即：输出模块
print obj.__class__      # 输出 lib.aa.C，即：输出类


```

#### init

```
 __init__

　　构造方法，通过类创建对象时，自动触发执行。
```

例子

```
class Foo:

    def __init__(self, name):
        self.name = name
        self.age = 18


obj = Foo('zdk') # 自动执行类中的 __init__ 方法
```

#### 析构函数

```
 __del__

　　析构方法，当对象在内存中被释放时，自动触发执行。

注：此方法一般无须定义，因为Python是一门高级语言，程序员在使用时无需关心内存的分配和释放，因为此工作都是交给Python解释器来执行，所以，析构函数的调用是由解释器在进行垃圾回收时自动触发执行的。
```

#### call方法

对象后面加括号，触发执行。

注：构造方法的执行是由创建对象触发的，即：对象 = 类名() ；而对于 __call__ 方法的执行是由对象后加括号触发的，即：对象() 或者 类()()

```

class Foo:

    def __init__(self):
        pass
    
    def __call__(self, *args, **kwargs):

        print '__call__'


obj = Foo() # 执行 __init__
obj()       # 执行 __call__
```

#### dict

类或对象中的所有成员

上文中我们知道：类的普通字段属于对象；类中的静态字段和方法等属于类

```
class Province:

    country = 'China'

    def __init__(self, name, count):
        self.name = name
        self.count = count

    def func(self, *args, **kwargs):
        print 'func'

# 获取类的成员，即：静态字段、方法、
print Province.__dict__
# 输出：{'country': 'China', '__module__': '__main__', 'func': <function func at 0x10be30f50>, '__init__': <function __init__ at 0x10be30ed8>, '__doc__': None}

obj1 = Province('HeBei',10000)
print obj1.__dict__
# 获取 对象obj1 的成员
# 输出：{'count': 10000, 'name': 'HeBei'}

obj2 = Province('HeNan', 3888)
print obj2.__dict__
# 获取 对象obj1 的成员
# 输出：{'count': 3888, 'name': 'HeNan'}
```

#### str repr  format

如果一个类中定义了__str__方法，那么在打印 对象 时，默认输出该方法的返回值。

经典例题

```
#_*_coding:utf-8_*_
__author__ = 'Linhaifeng'
format_dict={
    'nat':'{obj.name}-{obj.addr}-{obj.type}',#学校名-学校地址-学校类型
    'tna':'{obj.type}:{obj.name}:{obj.addr}',#学校类型:学校名:学校地址
    'tan':'{obj.type}/{obj.addr}/{obj.name}',#学校类型/学校地址/学校名
}
class School:
    def __init__(self,name,addr,type):
        self.name=name
        self.addr=addr
        self.type=type

    def __repr__(self):
        return 'School(%s,%s)' %(self.name,self.addr)
    def __str__(self):
        return '(%s,%s)' %(self.name,self.addr)

    def __format__(self, format_spec):
        # if format_spec
        if not format_spec or format_spec not in format_dict:
            format_spec='nat'
        fmt=format_dict[format_spec]
        return fmt.format(obj=self)

s1=School('oldboy1','北京','私立')
print('from repr: ',repr(s1))
print('from str: ',str(s1))
print(s1)

'''
str函数或者print函数--->obj.__str__()
repr或者交互式解释器--->obj.__repr__()
如果__str__没有被定义,那么就会使用__repr__来代替输出
注意:这俩方法的返回值必须是字符串,否则抛出异常
'''
print(format(s1,'nat'))
print(format(s1,'tna'))
print(format(s1,'tan'))
print(format(s1,'asfdasdffd'))
```

format实例

```
date_dic={
    'ymd':'{0.year}:{0.month}:{0.day}',
    'dmy':'{0.day}/{0.month}/{0.year}',
    'mdy':'{0.month}-{0.day}-{0.year}',
}
class Date:
    def __init__(self,year,month,day):
        self.year=year
        self.month=month
        self.day=day

    def __format__(self, format_spec):
        if not format_spec or format_spec not in date_dic:
            format_spec='ymd'
        fmt=date_dic[format_spec]
        return fmt.format(self)

d1=Date(2016,12,29)
print(format(d1))
print('{:mdy}'.format(d1))  ?????

```
#### __getitem__、__setitem__、__delitem__

用于索引操作，如字典。以上分别表示获取、设置、删除数据

```
#!/usr/bin/env python
# -*- coding:utf-8 -*-
 
class Foo(object):
 
    def __getitem__(self, key):
        print '__getitem__',key
 
    def __setitem__(self, key, value):
        print '__setitem__',key,value
 
    def __delitem__(self, key):
        print '__delitem__',key
 
 
obj = Foo()
 
result = obj['k1']      # 自动触发执行 __getitem__
obj['k2'] = 'wupeiqi'   # 自动触发执行 __setitem__
del obj['k1']           # 自动触发执行 __delitem__
```

```
class Foo:
    def __init__(self,name):
        self.name=name

    def __getitem__(self, item):
        print(self.__dict__[item])

    def __setitem__(self, key, value):
        self.__dict__[key]=value
    def __delitem__(self, key):
        print('del obj[key]时,我执行')
        self.__dict__.pop(key)
    def __delattr__(self, item):
        print('del obj.key时,我执行')
        self.__dict__.pop(item)

f1=Foo('sb')
f1['age']=18
f1['age1']=19
del f1.age1
del f1['age']
f1['name']='alex'
print(f1.__dict__)
```

#### __getslice__、__setslice__、__delslice__

该三个方法用于分片操作，如：列表

```
#!/usr/bin/env python
# -*- coding:utf-8 -*-
 
class Foo(object):
 
    def __getslice__(self, i, j):
        print '__getslice__',i,j
 
    def __setslice__(self, i, j, sequence):
        print '__setslice__',i,j
 
    def __delslice__(self, i, j):
        print '__delslice__',i,j
 
obj = Foo()
 
obj[-1:1]                   # 自动触发执行 __getslice__
obj[0:1] = [11,22,33,44]    # 自动触发执行 __setslice__
del obj[0:2]                # 自动触发执行 __delslice__
```

#### __next__和__iter__实现迭代器协议

```
class Foo:
    def __init__(self,x):
        self.x=x

    def __iter__(self):
        return self

    def __next__(self):
        n=self.x
        self.x+=1
        return self.x

f=Foo(3)
for i in f:
    print(i)
```
简单实现range函数

```
class Range:
    def __init__(self,n,stop,step):
        self.n=n
        self.stop=stop
        self.step=step

    def __next__(self):
        if self.n >= self.stop:
            raise StopIteration
        x=self.n
        self.n+=self.step
        return x

    def __iter__(self):
        return self

for i in Range(1,7,3): #
    print(i)
```

#### ___enter__和__exit__

我们知道在操作文件对象的时候可以这么写

```


1 with open('a.txt') as f:
2 　　'代码块'

```

上述叫做上下文管理协议，即with语句，为了让一个对象兼容with语句，必须在这个对象的类中声明__enter__和__exit__方法

```
class Open:
    def __init__(self,name):
        self.name=name

    def __enter__(self):
        print('出现with语句,对象的__enter__被触发,有返回值则赋值给as声明的变量')
        # return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        print('with中代码块执行完毕时执行我啊')


with Open('a.txt') as f:
    print('=====>执行代码块')
    # print(f,f.name)

上下文管理协议
```

__exit__()中的三个参数分别代表异常类型，异常值和追溯信息,with语句中代码块出现异常，则with后的代码都无法执行

```
class Open:
    def __init__(self,name):
        self.name=name

    def __enter__(self):
        print('出现with语句,对象的__enter__被触发,有返回值则赋值给as声明的变量')

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('with中代码块执行完毕时执行我啊')
        print(exc_type)
        print(exc_val)
        print(exc_tb)



with Open('a.txt') as f:
    print('=====>执行代码块')
    raise AttributeError('***着火啦,救火啊***')
print('0'*100) #------------------------------->不会执行
```
如果__exit()返回值为True,那么异常会被清空，就好像啥都没发生一样，with后的语句正常执行

```
class Open:
    def __init__(self,name):
        self.name=name

    def __enter__(self):
        print('出现with语句,对象的__enter__被触发,有返回值则赋值给as声明的变量')

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('with中代码块执行完毕时执行我啊')
        print(exc_type)
        print(exc_val)
        print(exc_tb)
        return True



with Open('a.txt') as f:
    print('=====>执行代码块')
    raise AttributeError('***着火啦,救火啊***')
print('0'*100) #------------------------------->会执行
```
用途或者说好处：

1.使用with语句的目的就是把代码块放入with中执行，with结束后，自动完成清理工作，无须手动干预

2.在需要管理一些资源比如文件，网络连接和锁的编程环境中，可以在__exit__中定制自动释放资源的机制，你无须再去关系这个问题，这将大有用处

#### 描述符(__get__,__set__,__delete__)

简介
```
1 描述符是什么:描述符本质就是一个新式类,在这个新式类中,至少实现了__get__(),__set__(),__delete__()中的一个,这也被称为描述符协议
__get__():调用一个属性时,触发
__set__():为一个属性赋值时,触发
__delete__():采用del删除属性时,触发
```

描述符定义
```

class Foo: #在python3中Foo是新式类,它实现了三种方法,这个类就被称作一个描述符
    def __get__(self, instance, owner):
        pass
    def __set__(self, instance, value):
        pass
    def __delete__(self, instance):
        pass

定义一个描述符
```

这样来调用

```
#描述符Str
class Str:
    def __get__(self, instance, owner):
        print('Str调用')
    def __set__(self, instance, value):
        print('Str设置...')
    def __delete__(self, instance):
        print('Str删除...')

#描述符Int
class Int:
    def __get__(self, instance, owner):
        print('Int调用')
    def __set__(self, instance, value):
        print('Int设置...')
    def __delete__(self, instance):
        print('Int删除...')

class People:
    name=Str()
    age=Int()
    def __init__(self,name,age): #name被Str类代理,age被Int类代理,
        self.name=name
        self.age=age

#何地？：定义成另外一个类的类属性

#何时？：且看下列演示

p1=People('alex',18)

#描述符Str的使用
p1.name     ---->调用get
p1.name='egon'   ----->调用set
del p1.name      ------>调用del

#描述符Int的使用
p1.age    
p1.age=18
del p1.age

#我们来瞅瞅到底发生了什么
print(p1.__dict__)
print(People.__dict__)

#补充
print(type(p1) == People) #type(obj)其实是查看obj是由哪个类实例化来的
print(type(p1).__dict__ == People.__dict__)

描述符应用之何时?何地?
```
描述符分类

一 数据描述符:至少实现了__get__()和__set__()

```
1 class Foo:
2     def __set__(self, instance, value):
3         print('set')
4     def __get__(self, instance, owner):
5         print('get')
```

二 非数据描述符:没有实现__set__()

```
1 class Foo:
2     def __get__(self, instance, owner):
3         print('get')
```

#### ( __setattr__,__delattr__,__getattr__)
 
```
 class Foo:
    x=1
    def __init__(self,y):
        self.y=y

    def __getattr__(self, item):
        print('----> from getattr:你找的属性不存在')


    def __setattr__(self, key, value):
        print('----> from setattr')
        # self.key=value #这就无限递归了,你好好想想
        # self.__dict__[key]=value #应该使用它

    def __delattr__(self, item):
        print('----> from delattr')
        # del self.item #无限递归了
        self.__dict__.pop(item)

#__setattr__添加/修改属性会触发它的执行
f1=Foo(10)
print(f1.__dict__) # 因为你重写了__setattr__,凡是赋值操作都会触发它的运行,你啥都没写,就是根本没赋值,除非你直接操作属性字典,否则永远无法赋值
f1.z=3
print(f1.__dict__)

#__delattr__删除属性的时候会触发
f1.__dict__['a']=3#我们可以直接修改属性字典,来完成添加/修改属性的操作
del f1.a
print(f1.__dict__)

#__getattr__只有在使用点调用属性且属性不存在的时候才会触发
f1.xxxxxx

```
####  __getattribute__

第一
```
class Foo:
    def __init__(self,x):
        self.x=x

    def __getattr__(self, item):
        print('执行的是我')
        # return self.__dict__[item]

f1=Foo(10)
print(f1.x)
f1.xxxxxx #不存在的属性访问，触发__getattr__

```
第二

```
class Foo:
    def __init__(self,x):
        self.x=x

    def __getattribute__(self, item):
        print('不管是否存在,我都会执行')

f1=Foo(10)
f1.x
f1.xxxxxx

__getattribute__


```

第三都存在

```
#_*_coding:utf-8_*_
__author__ = 'Linhaifeng'

class Foo:
    def __init__(self,x):
        self.x=x

    def __getattr__(self, item):
        print('执行的是我')
        # return self.__dict__[item]
    def __getattribute__(self, item):
        print('不管是否存在,我都会执行')
        #raise AttributeError('哈哈')

f1=Foo(10)
f1.x
f1.xxxxxx

#当__getattribute__与__getattr__同时存在,只会执行__getattrbute__,除非__getattribute__在执行过程中抛出异常AttributeError

二者同时出现
```
#### 反射

python中的反射功能是由以下四个内置函数提供：hasattr、getattr、setattr、delattr，改四个函数分别用于对对象内部执行：检查是否含有某成员、获取成员、设置成员、删除成员。

python面向对象中的反射：通过字符串的形式操作对象相关的属性。python中的一切事物都是对象（都可以使用反射）

```
class BlackMedium:
    feature='Ugly'
    def __init__(self,name,addr):
        self.name=name
        self.addr=addr

    def sell_house(self):
        print('%s 黑中介卖房子啦,傻逼才买呢,但是谁能证明自己不傻逼' %self.name)
    def rent_house(self):
        print('%s 黑中介租房子啦,傻逼才租呢' %self.name)

b1=BlackMedium('万成置地','回龙观天露园')

#检测是否含有某属性
print(hasattr(b1,'name'))
print(hasattr(b1,'sell_house'))

#获取属性
n=getattr(b1,'name')
print(n)
func=getattr(b1,'rent_house')
func()

# getattr(b1,'aaaaaaaa') #报错
print(getattr(b1,'aaaaaaaa','不存在啊'))

#设置属性
setattr(b1,'sb',True)
setattr(b1,'show_name',lambda self:self.name+'sb')
print(b1.__dict__)
print(b1.show_name(b1))

#删除属性
delattr(b1,'addr')
delattr(b1,'show_name')
delattr(b1,'show_name111')#不存在,则报错

print(b1.__dict__)

四个方法的使用演示
```
或者类也是对象

```

class Foo(object):
 
    staticField = "old boy"
 
    def __init__(self):
        self.name = 'wupeiqi'
 
    def func(self):
        return 'func'
 
    @staticmethod
    def bar():
        return 'bar'
 
print getattr(Foo, 'staticField')
print getattr(Foo, 'func')
print getattr(Foo, 'bar')

```

导入当前模块,查看其方法

```

#!/usr/bin/env python
# -*- coding:utf-8 -*-

import sys


def s1():
    print 's1'


def s2():
    print 's2'


this_module = sys.modules[__name__]

hasattr(this_module, 's1')
getattr(this_module, 's2')

```

导入其他模块，利用反射查找该模块是否存在某个方法，并且执行某方法

```
module_test.py

#!/usr/bin/env python
# -*- coding:utf-8 -*-

def test():
    print('from the test')

```

```

#!/usr/bin/env python
# -*- coding:utf-8 -*-
 
"""
程序目录：
    module_test.py
    index.py
 
当前文件：
    index.py
"""

import module_test as obj

#obj.test()

print(hasattr(obj,'test'))

getattr(obj,'test')()  #执行test函数
```

为什么用反射之反射的好处

好处一：实现可插拔机制

有俩程序员，一个lili，一个是egon，lili在写程序的时候需要用到egon所写的类，但是egon去跟女朋友度蜜月去了，还没有完成他写的类，lili想到了反射，使用了反射机制lili可以继续完成自己的代码，等egon度蜜月回来后再继续完成类的定义并且去实现lili想要的功能。

总之反射的好处就是，可以事先定义好接口，接口只有在被完成后才会真正执行，这实现了即插即用，这其实是一种‘后期绑定’，什么意思？即你可以事先把主要的逻辑写好（只定义接口），然后后期再去实现接口的功能

```
例如提前写好了一个函数
class FtpClient:
    'ftp客户端,但是还么有实现具体的功能'
    def __init__(self,addr):
        print('正在连接服务器[%s]' %addr)
        self.addr=addr
```

其他人直接调用即可
```
#from module import FtpClient
f1=FtpClient('192.168.1.1')
if hasattr(f1,'get'):
    func_get=getattr(f1,'get')
    func_get()
else:
    print('---->不存在此方法')
    print('处理其他的逻辑')

不影响lili的代码编写
```

可通过字符串的形式导入模块

- 单层导入

```
 __import__('模块名')
```

- 多层导入

```
 __import__(' list.text.commons',fromlist=True) #如果不加上fromlist=True,只会导入list目录
 
```
