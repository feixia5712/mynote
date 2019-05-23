### 面向对象

#### 面向过程 VS 面向对象

##### 编程范式

编程是 程序 员 用特定的语法+数据结构+算法组成的代码来告诉计算机如何执行任务的过程 ， 一个程序是程序员为了得到一个任务结果而编写的一组指令的集合，正所谓条条大路通罗马，实现一个任务的方式有很多种不同的方式， 对这些不同的编程方式的特点进行归纳总结得出来的编程方式类别，即为编程范式。 不同的编程范式本质上代表对各种类型的任务采取的不同的解决问题的思路， 大多数语言只支持一种编程范式，当然也有些语言可以同时支持多种编程范式。 两种最重要的编程范式分别是面向过程编程和面向对象编程。

##### 面向过程编程(Procedural Programming)
Procedural programming uses a list of instructions to tell the computer what to do step-by-step.
面向过程编程依赖 - 你猜到了- procedures，一个procedure包含一组要被进行计算的步骤， 面向过程又被称为top-down languages， 就是程序从上到下一步步执行，一步步从上到下，从头到尾的解决问题 。基本设计思路就是程序一开始是要着手解决一个大的问题，然后把一个大问题分解成很多个小问题或子过程，这些子过程再执行的过程再继续分解直到小问题足够简单到可以在一个小步骤范围内解决。

##### 面向对象编程

OOP编程是利用“类”和“对象”来创建各种模型来实现对真实世界的描述，使用面向对象编程的原因一方面是因为它可以使程序的维护和扩展变得更简单，并且可以大大提高程序开发效率 ，另外，基于面向对象的程序可以使它人更加容易理解你的代码逻辑，从而使团队开发变得更从容。

面向对象的几个核心特性如下

###### Class 类
一个类即是对一类拥有相同属性的对象的抽象、蓝图、原型。在类中定义了这些对象的都具备的属性（variables(data)）、共同的方法

###### Object 对象
一个对象即是一个类的实例化后实例，一个类必须经过实例化后方可在程序中调用，一个类可以实例化多个对象，每个对象亦可以有不同的属性，就像人类是指所有人，每个人是指具体的对象，人与人之前有共性，亦有不同

###### Encapsulation 封装
在类中对数据的赋值、内部调用对外部用户是透明的，这使类变成了一个胶囊或容器，里面包含着类的数据和方法

###### Inheritance 继承
一个类可以派生出子类，在这个父类里定义的属性、方法自动被子类继承

###### Polymorphism 多态
多态是面向对象的重要特性,简单点说:“一个接口，多种实现”，指一个基类中派生出了不同的子类，且每个子类在继承了同样的方法名的同时又对父类的方法做了不同的实现，这就是同一种事物表现出的多种形态。
编程其实就是一个将具体世界进行抽象化的过程，多态就是抽象化的一种体现，把一系列具体事物的共同点抽象出来, 再通过这个抽象的事物, 与不同的具体事物进行对话。
对不同类的对象发出相同的消息将会有不同的行为。比如，你的老板让所有员工在九点钟开始工作, 他只要在九点钟的时候说：“开始工作”即可，而不需要对销售人员说：“开始销售工作”，对技术人员说：“开始技术工作”, 因为“员工”是一个抽象的事物, 只要是员工就可以开始工作，他知道这一点就行了。至于每个员工，当然会各司其职，做各自的工作。
多态允许将子类的对象当作父类的对象使用，某父类型的引用指向其子类型的对象,调用的方法是该子类型的方法。这里引用和调用方法的代码编译前就已经决定了,而引用所指向的对象可以在运行期间动态绑定

#### 创建类和对象

类就是一个模板，模板里可以包含多个函数，函数里实现一些功能

　　对象则是根据模板创建的实例，通过实例对象可以执行类中的函数
　　
![image](https://images0.cnblogs.com/blog2015/425762/201508/271420286872390.jpg)

class是关键字，表示类
创建对象，类名称后加括号即可

一个类的简单写法

```
# 创建类
class Foo:
     
    def Bar(self):
        print 'Bar'
 
    def Hello(self, name):
        print 'i am %s' %name
 
# 根据类Foo创建对象obj
obj = Foo()
obj.Bar()            #执行Bar方法
obj.Hello('zhangdk') #执行Hello方法　
```

#### 封装

封装，顾名思义就是将内容封装到某个地方，以后再去调用被封装在某处的内容。

所以，在使用面向对象的封装特性时，需要：

- 将内容封装到某处
- 从某处调用被封装的内容
- 

将内容封装到某处

![封装](https://images0.cnblogs.com/blog2015/425762/201508/271641407509817.jpg)

说明：
```
self 是一个形式参数，当执行 obj1 = Foo('wupeiqi', 18 ) 时，self 等于 obj1

 当执行 obj2 = Foo('alex', 78 ) 时，self 等于 obj2

所以，内容其实被封装到了对象 obj1 和 obj2 中，每个对象中都有 name 和 age 属性，在内存里类似于下图来保存。

```
如下

![image](https://images0.cnblogs.com/blog2015/425762/201508/271653303446704.jpg)

从某处调用被封装的内容

调用被封装的内容时，有两种情况：

- 通过对象直接调用
- 通过self间接调用

1、通过对象直接调用被封装的内容

上图展示了对象 obj1 和 obj2 在内存中保存的方式，根据保存格式可以如此调用被封装的内容：对象.属性名

```
class Foo:
 
    def __init__(self, name, age):
        self.name = name
        self.age = age
 
obj1 = Foo('wupeiqi', 18)
print obj1.name    # 直接调用obj1对象的name属性
print obj1.age     # 直接调用obj1对象的age属性
 
obj2 = Foo('alex', 73)
print obj2.name    # 直接调用obj2对象的name属性
print obj2.age     # 直接调用obj2对象的age属性
```

2 通过self间接调用被封装的内容
执行类中的方法时，需要通过self间接调用被封装的内容

```

class Foo:
  
    def __init__(self, name, age):
        self.name = name
        self.age = age
  
    def detail(self):
        print self.name
        print self.age
  
obj1 = Foo('wupeiqi', 18)
obj1.detail()  # Python默认会将obj1传给self参数，即：obj1.detail(obj1)，所以，此时方法内部的 self ＝ obj1，即：self.name 是 wupeiqi ；self.age 是 18
  
obj2 = Foo('alex', 73)
obj2.detail()  # Python默认会将obj2传给self参数，即：obj1.detail(obj2)，所以，此时方法内部的 self ＝ obj2，即：self.name 是 alex ； self.age 是 78
```

#### 继承

继承，面向对象中的继承和现实生活中的继承相同，即：子可以继承父的内容。

继承的简单实例

```
class Animal:

    def eat(self):
        print "%s 吃 " %self.name

    def drink(self):
        print "%s 喝 " %self.name

    def shit(self):
        print "%s 拉 " %self.name

    def pee(self):
        print "%s 撒 " %self.name


class Cat(Animal):

    def __init__(self, name):
        self.name = name
        self.breed ＝ '猫'

    def cry(self):
        print '喵喵叫'

class Dog(Animal):
    
    def __init__(self, name):
        self.name = name
        self.breed ＝ '狗'
        
    def cry(self):
        print '汪汪叫'
        

# ######### 执行 #########

c1 = Cat('小白家的小黑猫')
c1.eat()

c2 = Cat('小黑的小白猫')
c2.drink()

d1 = Dog('胖子家的小瘦狗')
d1.eat()
```
所以，对于面向对象的继承来说，其实就是将多个类共有的方法提取到父类中，子类仅需继承父类而不必一一实现每个方法。

![继承](https://images0.cnblogs.com/blog2015/425762/201508/272229566093488.jpg)

##### 多继承

查看继承

```
class ParentClass1: #定义父类
    pass

class ParentClass2: #定义父类
    pass

class SubClass1(ParentClass1): #单继承，基类是ParentClass1，派生类是SubClass
    pass

class SubClass2(ParentClass1,ParentClass2): #python支持多继承，用逗号分隔开多个继承的类
    pass
```

```
>>> SubClass1.__bases__ #__base__只查看从左到右继承的第一个子类，__bases__则是查看所有继承的父类
(<class '__main__.ParentClass1'>,)
>>> SubClass2.__bases__
(<class '__main__.ParentClass1'>, <class '__main__.ParentClass2'>)
```

##### 经典类与新式类

1.只有在python2中才分新式类和经典类，python3中统一都是新式类

2.在python2中，没有显式的继承object类的类，以及该类的子类，都是经典类

3.在python2中，显式地声明继承object的类，以及该类的子类，都是新式类

4.在python3中，无论是否继承object，都默认继承object，即python3中所有类均为新式类

提示：如果没有指定基类，python的类会默认继承object类，object是所有python类的基类，它提供了一些常见方法（如__str__）的实现。

```
>>> ParentClass1.__bases__
(<class 'object'>,)
>>> ParentClass2.__bases__
(<class 'object'>,)

```

类的继承会继承父类的数据属性和函数属性
子类会先从实例中找然后去类中找，然后再去父类中找...直到最顶级的父类。

```
class Foo:
    def f1(self):
        print('Foo.f1')

    def f2(self):
        print('Foo.f2')
        self.f1()

class Bar(Foo):
    def f1(self):
        print('Foo.f1')


b=Bar()
b.f2()
```

####多继承的顺序

经典类:(深度优先)

![经典类](https://images2017.cnblogs.com/blog/1036857/201801/1036857-20180119212411240-1564453560.png)

新式类:(广度有先)

![广度有先](https://images2017.cnblogs.com/blog/1036857/201801/1036857-20180119212426037-160472708.png)

实例：

```
class A(object):
    def test(self):
        print('from A')

class B(A):
    def test(self):
        print('from B')

class C(A):
    def test(self):
        print('from C')

class D(B):
    def test(self):
        print('from D')

class E(C):
    def test(self):
        print('from E')

class F(D,E):
    # def test(self):
    #     print('from F')
    pass
f1=F()
f1.test()
print(F.__mro__) #只有新式才有这个属性可以查看线性列表，经典类没有这个属性

#新式类继承顺序:F->D->B->E->C->A
#经典类继承顺序:F->D->B->A->E->C
#python3中统一都是新式类
#pyhon2中才分新式类与经典类

```

2 继承原理（python如何实现的继承）

python到底是如何实现继承的，对于你定义的每一个类，python会计算出一个方法解析顺序(MRO)列表，这个MRO列表就是一个简单的所有基类的线性顺序列表，例如

```
>>> F.mro() #等同于F.__mro__
[<class '__main__.F'>, <class '__main__.D'>, <class '__main__.B'>, <class '__main__.E'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```
 

为了实现继承,python会在MRO列表上从左到右开始查找基类,直到找到第一个匹配这个属性的类为止。
而这个MRO列表的构造是通过一个C3线性化算法来实现的。我们不去深究这个算法的数学原理,它实际上就是合并所有父类的MRO列表并遵循如下三条准则:
1.子类会先于父类被检查
2.多个父类会根据它们在列表中的顺序被检查
3.如果对下一个类存在两个合法的选择,选择第一个父类

#### 子类中调用父类的方法

两种方式：

- 直接指名道姓，即父类名.父类方法()

```
#_*_coding:utf-8_*_
__author__ = 'Linhaifeng'

class Vehicle: #定义交通工具类
     Country='China'
     def __init__(self,name,speed,load,power):
         self.name=name
         self.speed=speed
         self.load=load
         self.power=power

     def run(self):
         print('开动啦...')

class Subway(Vehicle): #地铁
    def __init__(self,name,speed,load,power,line):
        Vehicle.__init__(self,name,speed,load,power)
        self.line=line

    def run(self):
        print('地铁%s号线欢迎您' %self.line)
        Vehicle.run(self)

line13=Subway('中国地铁','180m/s','1000人/箱','电',13)
line13.run()
```

- 方法二：super()调用父类方法

```
class Vehicle: #定义交通工具类
     Country='China'
     def __init__(self,name,speed,load,power):
         self.name=name
         self.speed=speed
         self.load=load
         self.power=power

     def run(self):
         print('开动啦...')

class Subway(Vehicle): #地铁
    def __init__(self,name,speed,load,power,line):
        #super(Subway,self) 就相当于实例本身 在python3中super()等同于super(Subway,self)
        super().__init__(name,speed,load,power)
        self.line=line

    def run(self):
        print('地铁%s号线欢迎您' %self.line)
        super(Subway,self).run()

class Mobike(Vehicle):#摩拜单车
    pass

line13=Subway('中国地铁','180m/s','1000人/箱','电',13)
line13.run()
```

即使没有直接继承关系，super仍然会按照mro继续往后查找

```
#A没有继承B,但是A内super会基于C.mro()继续往后找
class A:
    def test(self):
        super().test()
class B:
    def test(self):
        print('from B')
class C(A,B):
    pass

c=C()
c.test() #打印结果:from B


print(C.mro())
#[<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>]
```

==指名道姓与super()的区别==

```
#指名道姓
class A:
    def __init__(self):
        print('A的构造方法')
class B(A):
    def __init__(self):
        print('B的构造方法')
        A.__init__(self)


class C(A):
    def __init__(self):
        print('C的构造方法')
        A.__init__(self)


class D(B,C):
    def __init__(self):
        print('D的构造方法')
        B.__init__(self)
        C.__init__(self)

    pass
f1=D() #A.__init__被重复调用
'''
D的构造方法
B的构造方法
A的构造方法
C的构造方法
A的构造方法
'''


#使用super()
class A:
    def __init__(self):
        print('A的构造方法')
class B(A):
    def __init__(self):
        print('B的构造方法')
        super(B,self).__init__()


class C(A):
    def __init__(self):
        print('C的构造方法')
        super(C,self).__init__()


class D(B,C):
    def __init__(self):
        print('D的构造方法')
        super(D,self).__init__()

f1=D() #super()会基于mro列表,往后找
'''
D的构造方法
B的构造方法
C的构造方法
A的构造方法
'''

```

==当你使用super()函数时,Python会在MRO列表上继续搜索下一个类。只要每个重定义的方法统一使用super()并只调用它一次,那么控制流最终会遍历完整个MRO列表,每个方法也只会被调用一次（注意注意注意：使用super调用的所有属性，都是从MRO列表当前的位置往后找，千万不要通过看代码去找继承关系，一定要看MRO列表）==


#### 派生

当然子类也可以添加自己新的属性或者在自己这里重新定义这些属性（不会影响到父类），需要注意的是，一旦重新定义了自己的属性且与父类重名，那么调用新增的属性时，就以自己为准了。

```
class Riven(Hero):
    camp='Noxus'
    def attack(self,enemy): #在自己这里定义新的attack,不再使用父类的attack,且不会影响父类
        print('from riven')
    def fly(self): #在自己这里定义新的
        print('%s is flying' %self.nickname)
```

在子类中，新建的重名的函数属性，在编辑函数内功能的时候，有可能需要重用父类中重名的那个函数功能，应该是用调用普通函数的方式，即：==类名.func()==，此时就与调用普通函数无异了，因此即便是self参数也要为其传值

```
class Riven(Hero):
    camp='Noxus'
    def __init__(self,nickname,aggressivity,life_value,skin):
        Hero.__init__(self,nickname,aggressivity,life_value) #调用父类功能
        self.skin=skin #新属性
    def attack(self,enemy): #在自己这里定义新的attack,不再使用父类的attack,且不会影响父类
        Hero.attack(self,enemy) #调用功能
        print('from riven')
    def fly(self): #在自己这里定义新的
        print('%s is flying' %self.nickname)

r1=Riven('锐雯雯',57,200,'比基尼')
r1.fly()
print(r1.skin)

```
xxxx

```
运行结果
锐雯雯 is flying
比基尼
```

#### 组合与重用

软件重用的重要方式除了继承之外还有另外一种方式，即：组合

组合指的是，在一个类中以另外一个类的对象作为数据属性，称为类的组合


```
>>> class Equip: #武器装备类
...     def fire(self):
...         print('release Fire skill')
... 
>>> class Riven: #英雄Riven的类,一个英雄需要有装备,因而需要组合Equip类
...     camp='Noxus'
...     def __init__(self,nickname):
...         self.nickname=nickname
...         self.equip=Equip() #用Equip类产生一个装备,赋值给实例的equip属性
... 
>>> r1=Riven('锐雯雯')
>>> r1.equip.fire() #可以使用组合的类产生的对象所持有的方法
release Fire skill
```
组合与继承都是有效地利用已有类的资源的重要方式。但是二者的概念和使用场景皆不同，

1.继承的方式

通过继承建立了派生类与基类之间的关系，它是一种'是'的关系，比如白马是马，人是动物。

当类之间有很多相同的功能，提取这些共同的功能做成基类，用继承比较好，比如老师是人，学生是人

2.组合的方式

用组合的方式建立了类与组合的类之间的关系，它是一种‘有’的关系,比如教授有生日，教授教python和linux课程，教授有学生s1、s2、s3...

#### 其他

类有两种属性：数据属性和函数属性

1. 类的数据属性是所有对象共享的,id都一样

2. 类的函数属性是绑定给对象用的,内存地址都不一样

