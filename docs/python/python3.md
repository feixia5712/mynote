### python基础之数据类型与变量

#### 变量

1 什么是变量之声明变量

```
#变量名=变量值
age=18
gender1='male' 
gender2='female'
```

2 为什么要有变量
变量作用：“变”=>变化，“量”=>计量/保存状态
程序的运行本质是一系列状态的变化，变量的目的就是用来保存状态，变量值的变化就构成了程序运行的不同结果。

***
3 变量值之数据类型与对象

程序中需要处理的状态很多，于是有了不同类型的变量值，x='egon',变量值'egon'存放与内存中，绑定一个名字x，变量值即我们要存储的数据。

在python中所有数据都是围绕对象这个概念来构建的，对象包含一些基本的数据类型：数字，字符串，列表，元组，字典等
程序中存储的所有数据都是对象，
一个对象（如a=1）有：
　　一个身份（id）
　　一个类型(type)
　　一个值(通过变量名a来查看)
1 对象的类型也称为对象的类别，python为每个类型都定制了属于该类型特有的方法，极大地方便了开发者对数据的处理
2 创建某个特定类型的对象也称为创建了该类型的一个实例，工厂函数的概念来源于此

***
4 可变对象与不可变对象
实例被创建后，身份和类型是不可变的，
如果值是不可以被修改的，则是不可变对象
如果值是可以被修改的，则是可变对象

***
5 容器对象
某个对象包含对其他对象的引用，则称为容器或集合
***

6 对象的属性和方法
属性就是对象的值，方法就是调用时将在对象本身上执行某些操作的函数，使用.运算符可以访问对象的属性和方法，如

a=3+4j

a.real
b=[1,2,3]

b.append(4)

7 身份比较，类型比较，值比较

x=1

y=1

x is y #x与y是同一个对象，is比较的是id，即身份
type(x) is type(y) #对象的类型本身也是一个对象，所以可以用is比较两个对象的类型的身份
x == y #==比较的是两个对象的值是否相等

***
7 变量的命名规范

8 变量的赋值操作

与c语言的区别在于变量赋值操作无返回值

链式赋值：y＝x＝a＝1

多元赋值：x,y=1,2 x,y=y,x

增量赋值：x+=1

***
#### 数据类型

1 什么是数据类型以及数据类型分类

python中的数据类型

python使用对象模型来存储数据，每一个数据类型都有一个内置的类，每新建一个数据，实际就是在初始化生成一个对象，即所有数据都是对象

对象三个特性

身份：内存地址，可以用id()获取

类型：决定了该对象可以保存什么类型值，可执行何种操作，需遵循什么规则，可用type()获取

值：对象保存的真实数据

注：我们在定义数据类型，只需这样：x＝1，内部生成1这一内存对象会自动触发，我们无需关心
这里的字符串、数字、列表等都是数据类型（用来描述某种状态或者特性）除此之外还有很多其他数据，处理不同的数据就需要定义不同的数据类型

标准类型 | 其他类型
---|---
数字 | 类型type
字符串 | NUll
列表 | 文件
元祖 | 集合
字典 |函数/方法
 x    |类
 x    |模块

#### 标准数据类型

数字

定义：a＝1

特性：

1.只能存放一个值

2.一经定义，不可更改

3.直接访问

分类：整型，长整型，布尔，浮点，复数

#### 整形

Python的整型相当于C中的long型,Python中的整数可以用十进制,八进制,十六进制表示。
python2.*与python3.*关于整型的区别

python2.*
在32位机器上，整数的位数为32位，取值范围为-2**31～2**31-1，即-2147483648～2147483647

在64位系统上，整数的位数为64位，取值范围为-2**63～2**63-1，即-9223372036854775808～9223372036854775807
python3.*整形长度无限制

长整型long

python2.*：
跟C语言不同，Python的长整型没有指定位宽，也就是说Python没有限制长整型数值的大小，

但是实际上由于机器内存有限，所以我们使用的长整型数值不可能无限大。
在使用过程中，我们如何区分长整型和整型数值呢？

通常的做法是在数字尾部加上一个大写字母L或小写字母l以表示该整数是长整型的，例如：

a = 9223372036854775808L

注意，自从Python2起，如果发生溢出，Python会自动将整型数据转换为长整型，
所以如今在长整型数据后面不加字母L也不会导致严重后果了。

python3.*
长整型，整型统一归为整型

```
python2.7
>>> a=9223372036854775807
>>> a
9223372036854775807
>>> a+=1
>>> a
9223372036854775808L

python3.5
>>> a=9223372036854775807
>>> a
9223372036854775807
>>> a+=1
>>> a
9223372036854775808

```

布尔值bool

True 和False

1和0

浮点数float

Python的浮点数就是数学中的小数，类似C语言中的double。
在运算中，整数与浮点数运算的结果是浮点数
浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，
一个浮点数的小数点位置是可变的，比如，1.23*109和12.3*108是相等的。
浮点数可以用数学写法，如1.23，3.14，-9.01，等等。但是对于很大或很小的浮点数，
就必须用科学计数法表示，把10用e替代，1.23*109就是1.23e9，或者12.3e8，0.000012
可以写成1.2e-5，等等。
整数和浮点数在计算机内部存储的方式是不同的，整数运算永远是精确的而浮点数运算则可能会有
四舍五入的误差。

复数

数字相关内建函数

[内建函数相关](https://images2015.cnblogs.com/blog/1036857/201610/1036857-20161007202627379-994345539.png)

#### 字符串

```
定义：它是一个有序的字符的集合，用于存储和表示基本的文本信息，‘’或“”或‘’‘ ’‘’中间包含的内容称之为字符串
特性：
1.只能存放一个值
2.不可变
3.按照从左到右的顺序定义字符集合，下标从0开始顺序访问，有序
补充：
　　1.字符串的单引号和双引号都无法取消特殊字符的含义，如果想让引号内所有字符均取消特殊意义，在引号前面加r，如name＝r'l\thf'
　　2.unicode字符串与r连用必需在r前面，如name＝ur'l\thf'

```
字符串创建

```
a='hello world'

```
常用操作

```
移除空白
分割
长度
索引
切片

```
字符工程函数str

```

class str(object):
    """
    str(object='') -> str
    str(bytes_or_buffer[, encoding[, errors]]) -> str

    Create a new string object from the given object. If encoding or
    errors is specified, then the object must expose a data buffer
    that will be decoded using the given encoding and error handler.
    Otherwise, returns the result of object.__str__() (if defined)
    or repr(object).
    encoding defaults to sys.getdefaultencoding().
    errors defaults to 'strict'.
    """
    def capitalize(self): # real signature unknown; restored from __doc__
        """
        首字母变大写
        S.capitalize() -> str

        Return a capitalized version of S, i.e. make the first character
        have upper case and the rest lower case.
        """
        return ""

    def casefold(self): # real signature unknown; restored from __doc__
        """
        S.casefold() -> str

        Return a version of S suitable for caseless comparisons.
        """
        return ""

    def center(self, width, fillchar=None): # real signature unknown; restored from __doc__
        """
        原来字符居中，不够用空格补全
        S.center(width[, fillchar]) -> str

        Return S centered in a string of length width. Padding is
        done using the specified fill character (default is a space)
        """
        return ""

    def count(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
         从一个范围内的统计某str出现次数
        S.count(sub[, start[, end]]) -> int

        Return the number of non-overlapping occurrences of substring sub in
        string S[start:end].  Optional arguments start and end are
        interpreted as in slice notation.
        """
        return 0

    def encode(self, encoding='utf-8', errors='strict'): # real signature unknown; restored from __doc__
        """
        encode(encoding='utf-8',errors='strict')
        以encoding指定编码格式编码，如果出错默认报一个ValueError，除非errors指定的是
        ignore或replace

        S.encode(encoding='utf-8', errors='strict') -> bytes

        Encode S using the codec registered for encoding. Default encoding
        is 'utf-8'. errors may be given to set a different error
        handling scheme. Default is 'strict' meaning that encoding errors raise
        a UnicodeEncodeError. Other possible values are 'ignore', 'replace' and
        'xmlcharrefreplace' as well as any other name registered with
        codecs.register_error that can handle UnicodeEncodeErrors.
        """
        return b""

    def endswith(self, suffix, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.endswith(suffix[, start[, end]]) -> bool

        Return True if S ends with the specified suffix, False otherwise.
        With optional start, test S beginning at that position.
        With optional end, stop comparing S at that position.
        suffix can also be a tuple of strings to try.
        """
        return False

    def expandtabs(self, tabsize=8): # real signature unknown; restored from __doc__
        """
        将字符串中包含的\t转换成tabsize个空格
        S.expandtabs(tabsize=8) -> str

        Return a copy of S where all tab characters are expanded using spaces.
        If tabsize is not given, a tab size of 8 characters is assumed.
        """
        return ""

    def find(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.find(sub[, start[, end]]) -> int

        Return the lowest index in S where substring sub is found,
        such that sub is contained within S[start:end].  Optional
        arguments start and end are interpreted as in slice notation.

        Return -1 on failure.
        """
        return 0

    def format(self, *args, **kwargs): # known special case of str.format
        """
        格式化输出
        三种形式：
        形式一.
        >>> print('{0}{1}{0}'.format('a','b'))
        aba

        形式二：（必须一一对应）
        >>> print('{}{}{}'.format('a','b'))
        Traceback (most recent call last):
          File "<input>", line 1, in <module>
        IndexError: tuple index out of range
        >>> print('{}{}'.format('a','b'))
        ab

        形式三：
        >>> print('{name} {age}'.format(age=12,name='lhf'))
        lhf 12

        S.format(*args, **kwargs) -> str

        Return a formatted version of S, using substitutions from args and kwargs.
        The substitutions are identified by braces ('{' and '}').
        """
        pass

    def format_map(self, mapping): # real signature unknown; restored from __doc__
        """
        与format区别
        '{name}'.format(**dict(name='alex'))
        '{name}'.format_map(dict(name='alex'))

        S.format_map(mapping) -> str

        Return a formatted version of S, using substitutions from mapping.
        The substitutions are identified by braces ('{' and '}').
        """
        return ""

    def index(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.index(sub[, start[, end]]) -> int

        Like S.find() but raise ValueError when the substring is not found.
        """
        return 0

    def isalnum(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是字母或数字才返回True

        S.isalnum() -> bool

        Return True if all characters in S are alphanumeric
        and there is at least one character in S, False otherwise.
        """
        return False

    def isalpha(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是字母才返回True
        S.isalpha() -> bool

        Return True if all characters in S are alphabetic
        and there is at least one character in S, False otherwise.
        """
        return False

    def isdecimal(self): # real signature unknown; restored from __doc__
        """
        S.isdecimal() -> bool

        Return True if there are only decimal characters in S,
        False otherwise.
        """
        return False

    def isdigit(self): # real signature unknown; restored from __doc__
        """
        S.isdigit() -> bool

        Return True if all characters in S are digits
        and there is at least one character in S, False otherwise.
        """
        return False

    def isidentifier(self): # real signature unknown; restored from __doc__
        """
        字符串为关键字返回True

        S.isidentifier() -> bool

        Return True if S is a valid identifier according
        to the language definition.

        Use keyword.iskeyword() to test for reserved identifiers
        such as "def" and "class".
        """
        return False

    def islower(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是小写字母才返回True
        S.islower() -> bool

        Return True if all cased characters in S are lowercase and there is
        at least one cased character in S, False otherwise.
        """
        return False

    def isnumeric(self): # real signature unknown; restored from __doc__
        """
        S.isnumeric() -> bool

        Return True if there are only numeric characters in S,
        False otherwise.
        """
        return False

    def isprintable(self): # real signature unknown; restored from __doc__
        """
        S.isprintable() -> bool

        Return True if all characters in S are considered
        printable in repr() or S is empty, False otherwise.
        """
        return False

    def isspace(self): # real signature unknown; restored from __doc__
        """
        至少一个字符，且都是空格才返回True
        S.isspace() -> bool

        Return True if all characters in S are whitespace
        and there is at least one character in S, False otherwise.
        """
        return False

    def istitle(self): # real signature unknown; restored from __doc__
        """
        >>> a='Hello'
        >>> a.istitle()
        True
        >>> a='HellP'
        >>> a.istitle()
        False

        S.istitle() -> bool

        Return True if S is a titlecased string and there is at least one
        character in S, i.e. upper- and titlecase characters may only
        follow uncased characters and lowercase characters only cased ones.
        Return False otherwise.
        """
        return False

    def isupper(self): # real signature unknown; restored from __doc__
        """
        S.isupper() -> bool

        Return True if all cased characters in S are uppercase and there is
        at least one cased character in S, False otherwise.
        """
        return False

    def join(self, iterable): # real signature unknown; restored from __doc__
        """
        #对序列进行操作（分别使用' '与':'作为分隔符）
        >>> seq1 = ['hello','good','boy','doiido']
        >>> print ' '.join(seq1)
        hello good boy doiido
        >>> print ':'.join(seq1)
        hello:good:boy:doiido


        #对字符串进行操作

        >>> seq2 = "hello good boy doiido"
        >>> print ':'.join(seq2)
        h:e:l:l:o: :g:o:o:d: :b:o:y: :d:o:i:i:d:o


        #对元组进行操作

        >>> seq3 = ('hello','good','boy','doiido')
        >>> print ':'.join(seq3)
        hello:good:boy:doiido


        #对字典进行操作

        >>> seq4 = {'hello':1,'good':2,'boy':3,'doiido':4}
        >>> print ':'.join(seq4)
        boy:good:doiido:hello


        #合并目录

        >>> import os
        >>> os.path.join('/hello/','good/boy/','doiido')
        '/hello/good/boy/doiido'


        S.join(iterable) -> str

        Return a string which is the concatenation of the strings in the
        iterable.  The separator between elements is S.
        """
        return ""

    def ljust(self, width, fillchar=None): # real signature unknown; restored from __doc__
        """
        S.ljust(width[, fillchar]) -> str

        Return S left-justified in a Unicode string of length width. Padding is
        done using the specified fill character (default is a space).
        """
        return ""

    def lower(self): # real signature unknown; restored from __doc__
        """
        S.lower() -> str

        Return a copy of the string S converted to lowercase.
        """
        return ""

    def lstrip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.lstrip([chars]) -> str

        Return a copy of the string S with leading whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return ""

    def maketrans(self, *args, **kwargs): # real signature unknown
        """
        Return a translation table usable for str.translate().

        If there is only one argument, it must be a dictionary mapping Unicode
        ordinals (integers) or characters to Unicode ordinals, strings or None.
        Character keys will be then converted to ordinals.
        If there are two arguments, they must be strings of equal length, and
        in the resulting dictionary, each character in x will be mapped to the
        character at the same position in y. If there is a third argument, it
        must be a string, whose characters will be mapped to None in the result.
        """
        pass

    def partition(self, sep): # real signature unknown; restored from __doc__
        """
        以sep为分割，将S分成head,sep,tail三部分

        S.partition(sep) -> (head, sep, tail)

        Search for the separator sep in S, and return the part before it,
        the separator itself, and the part after it.  If the separator is not
        found, return S and two empty strings.
        """
        pass

    def replace(self, old, new, count=None): # real signature unknown; restored from __doc__
        """
        S.replace(old, new[, count]) -> str

        Return a copy of S with all occurrences of substring
        old replaced by new.  If the optional argument count is
        given, only the first count occurrences are replaced.
        """
        return ""

    def rfind(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.rfind(sub[, start[, end]]) -> int

        Return the highest index in S where substring sub is found,
        such that sub is contained within S[start:end].  Optional
        arguments start and end are interpreted as in slice notation.

        Return -1 on failure.
        """
        return 0

    def rindex(self, sub, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.rindex(sub[, start[, end]]) -> int

        Like S.rfind() but raise ValueError when the substring is not found.
        """
        return 0

    def rjust(self, width, fillchar=None): # real signature unknown; restored from __doc__
        """
        S.rjust(width[, fillchar]) -> str

        Return S right-justified in a string of length width. Padding is
        done using the specified fill character (default is a space).
        """
        return ""

    def rpartition(self, sep): # real signature unknown; restored from __doc__
        """
        S.rpartition(sep) -> (head, sep, tail)

        Search for the separator sep in S, starting at the end of S, and return
        the part before it, the separator itself, and the part after it.  If the
        separator is not found, return two empty strings and S.
        """
        pass

    def rsplit(self, sep=None, maxsplit=-1): # real signature unknown; restored from __doc__
        """
        S.rsplit(sep=None, maxsplit=-1) -> list of strings

        Return a list of the words in S, using sep as the
        delimiter string, starting at the end of the string and
        working to the front.  If maxsplit is given, at most maxsplit
        splits are done. If sep is not specified, any whitespace string
        is a separator.
        """
        return []

    def rstrip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.rstrip([chars]) -> str

        Return a copy of the string S with trailing whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return ""

    def split(self, sep=None, maxsplit=-1): # real signature unknown; restored from __doc__
        """
        以sep为分割，将S切分成列表，与partition的区别在于切分结果不包含sep，
        如果一个字符串中包含多个sep那么maxsplit为最多切分成几部分
        >>> a='a,b c\nd\te'
        >>> a.split()
        ['a,b', 'c', 'd', 'e']
        S.split(sep=None, maxsplit=-1) -> list of strings

        Return a list of the words in S, using sep as the
        delimiter string.  If maxsplit is given, at most maxsplit
        splits are done. If sep is not specified or is None, any
        whitespace string is a separator and empty strings are
        removed from the result.
        """
        return []

    def splitlines(self, keepends=None): # real signature unknown; restored from __doc__
        """
        Python splitlines() 按照行('\r', '\r\n', \n')分隔，
        返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如        果为 True，则保留换行符。
        >>> x
        'adsfasdf\nsadf\nasdf\nadf'
        >>> x.splitlines()
        ['adsfasdf', 'sadf', 'asdf', 'adf']
        >>> x.splitlines(True)
        ['adsfasdf\n', 'sadf\n', 'asdf\n', 'adf']

        S.splitlines([keepends]) -> list of strings

        Return a list of the lines in S, breaking at line boundaries.
        Line breaks are not included in the resulting list unless keepends
        is given and true.
        """
        return []

    def startswith(self, prefix, start=None, end=None): # real signature unknown; restored from __doc__
        """
        S.startswith(prefix[, start[, end]]) -> bool

        Return True if S starts with the specified prefix, False otherwise.
        With optional start, test S beginning at that position.
        With optional end, stop comparing S at that position.
        prefix can also be a tuple of strings to try.
        """
        return False

    def strip(self, chars=None): # real signature unknown; restored from __doc__
        """
        S.strip([chars]) -> str

        Return a copy of the string S with leading and trailing
        whitespace removed.
        If chars is given and not None, remove characters in chars instead.
        """
        return ""

    def swapcase(self): # real signature unknown; restored from __doc__
        """
        大小写反转
        S.swapcase() -> str

        Return a copy of S with uppercase characters converted to lowercase
        and vice versa.
        """
        return ""

    def title(self): # real signature unknown; restored from __doc__
        """
        S.title() -> str

        Return a titlecased version of S, i.e. words start with title case
        characters, all remaining cased characters have lower case.
        """
        return ""

    def translate(self, table): # real signature unknown; restored from __doc__
    maketrans() 方法用于创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。
    注：两个字符串的长度必须相同，为一一对应的关系，然后使用translate进行按照规则转换
        """
        table=str.maketrans('alex','big SB')

        a='hello abc'
        print(a.translate(table))

        S.translate(table) -> str

        Return a copy of the string S in which each character has been mapped
        through the given translation table. The table must implement
        lookup/indexing via __getitem__, for instance a dictionary or list,
        mapping Unicode ordinals to Unicode ordinals, strings, or None. If
        this operation raises LookupError, the character is left untouched.
        Characters mapped to None are deleted.
        """
        return ""

    def upper(self): # real signature unknown; restored from __doc__
        """
        S.upper() -> str

        Return a copy of S converted to uppercase.
        """
        return ""

    def zfill(self, width): # real signature unknown; restored from __doc__
        """
        原来字符右对齐，不够用0补齐
        
        S.zfill(width) -> str

        Pad a numeric string S with zeros on the left, to fill a field
        of the specified width. The string S is never truncated.
        """
        return ""

    def __add__(self, *args, **kwargs): # real signature unknown
        """ Return self+value. """
        pass

    def __contains__(self, *args, **kwargs): # real signature unknown
        """ Return key in self. """
        pass

    def __eq__(self, *args, **kwargs): # real signature unknown
        """ Return self==value. """
        pass

    def __format__(self, format_spec): # real signature unknown; restored from __doc__
        """
        S.__format__(format_spec) -> str

        Return a formatted version of S as described by format_spec.
        """
        return ""

    def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass

    def __getitem__(self, *args, **kwargs): # real signature unknown
        """ Return self[key]. """
        pass

    def __getnewargs__(self, *args, **kwargs): # real signature unknown
        pass

    def __ge__(self, *args, **kwargs): # real signature unknown
        """ Return self>=value. """
        pass

    def __gt__(self, *args, **kwargs): # real signature unknown
        """ Return self>value. """
        pass

    def __hash__(self, *args, **kwargs): # real signature unknown
        """ Return hash(self). """
        pass

    def __init__(self, value='', encoding=None, errors='strict'): # known special case of str.__init__
        """
        str(object='') -> str
        str(bytes_or_buffer[, encoding[, errors]]) -> str

        Create a new string object from the given object. If encoding or
        errors is specified, then the object must expose a data buffer
        that will be decoded using the given encoding and error handler.
        Otherwise, returns the result of object.__str__() (if defined)
        or repr(object).
        encoding defaults to sys.getdefaultencoding().
        errors defaults to 'strict'.
        # (copied from class doc)
        """
        pass

    def __iter__(self, *args, **kwargs): # real signature unknown
        """ Implement iter(self). """
        pass

    def __len__(self, *args, **kwargs): # real signature unknown
        """ Return len(self). """
        pass

    def __le__(self, *args, **kwargs): # real signature unknown
        """ Return self<=value. """
        pass

    def __lt__(self, *args, **kwargs): # real signature unknown
        """ Return self<value. """
        pass

    def __mod__(self, *args, **kwargs): # real signature unknown
        """ Return self%value. """
        pass

    def __mul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value.n """
        pass

    @staticmethod # known case of __new__
    def __new__(*args, **kwargs): # real signature unknown
        """ Create and return a new object.  See help(type) for accurate signature. """
        pass

    def __ne__(self, *args, **kwargs): # real signature unknown
        """ Return self!=value. """
        pass

    def __repr__(self, *args, **kwargs): # real signature unknown
        """ Return repr(self). """
        pass

    def __rmod__(self, *args, **kwargs): # real signature unknown
        """ Return value%self. """
        pass

    def __rmul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value. """
        pass

    def __sizeof__(self): # real signature unknown; restored from __doc__
        """ S.__sizeof__() -> size of S in memory, in bytes """
        pass

    def __str__(self, *args, **kwargs): # real signature unknown
        """ Return str(self). """
        pass

```
#### 列表

定义：[]内以逗号分隔，按照索引，存放各种数据类型，每个位置代表一个元素
特性：
1.可存放多个值

2.可修改指定索引位置对应的值，可变

3.按照从左到右的顺序定义列表元素，下标从0开始顺序访问，有序

列表的创建

三种方式

```
list_test=['jjj',12,'ok']
或
list_test=list('abc')
或
list_test=list(['jjj',12,'ok'])

```
常见操作

索引
切片
追加
删除
长度
切片
循环
包含

常用方法


```
class list(object):
    """
    list() -> new empty list
    list(iterable) -> new list initialized from iterable's items
    """
    def append(self, p_object): # real signature unknown; restored from __doc__
        """ L.append(object) -> None -- append object to end """
        pass

    def clear(self): # real signature unknown; restored from __doc__
        """ L.clear() -> None -- remove all items from L """
        pass

    def copy(self): # real signature unknown; restored from __doc__
        """ L.copy() -> list -- a shallow copy of L """
        return []

    def count(self, value): # real signature unknown; restored from __doc__
        """ L.count(value) -> integer -- return number of occurrences of value """
        return 0

    def extend(self, iterable): # real signature unknown; restored from __doc__
        """ L.extend(iterable) -> None -- extend list by appending elements from the iterable """
        pass

    def index(self, value, start=None, stop=None): # real signature unknown; restored from __doc__
        """
        L.index(value, [start, [stop]]) -> integer -- return first index of value.
        Raises ValueError if the value is not present.
        """
        return 0

    def insert(self, index, p_object): # real signature unknown; restored from __doc__
        """ L.insert(index, object) -- insert object before index """
        pass

    def pop(self, index=None): # real signature unknown; restored from __doc__
        """
        L.pop([index]) -> item -- remove and return item at index (default last).
        Raises IndexError if list is empty or index is out of range.
        """
        pass

    def remove(self, value): # real signature unknown; restored from __doc__
        """
        L.remove(value) -> None -- remove first occurrence of value.
        Raises ValueError if the value is not present.
        """
        pass

    def reverse(self): # real signature unknown; restored from __doc__
        """ L.reverse() -- reverse *IN PLACE* """
        pass

    def sort(self, key=None, reverse=False): # real signature unknown; restored from __doc__
        """ L.sort(key=None, reverse=False) -> None -- stable sort *IN PLACE* """
        pass

    def __add__(self, *args, **kwargs): # real signature unknown
        """ Return self+value. """
        pass

    def __contains__(self, *args, **kwargs): # real signature unknown
        """ Return key in self. """
        pass

    def __delitem__(self, *args, **kwargs): # real signature unknown
        """ Delete self[key]. """
        pass

    def __eq__(self, *args, **kwargs): # real signature unknown
        """ Return self==value. """
        pass

    def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass

    def __getitem__(self, y): # real signature unknown; restored from __doc__
        """ x.__getitem__(y) <==> x[y] """
        pass

    def __ge__(self, *args, **kwargs): # real signature unknown
        """ Return self>=value. """
        pass

    def __gt__(self, *args, **kwargs): # real signature unknown
        """ Return self>value. """
        pass

    def __iadd__(self, *args, **kwargs): # real signature unknown
        """ Implement self+=value. """
        pass

    def __imul__(self, *args, **kwargs): # real signature unknown
        """ Implement self*=value. """
        pass

    def __init__(self, seq=()): # known special case of list.__init__
        """
        list() -> new empty list
        list(iterable) -> new list initialized from iterable's items
        # (copied from class doc)
        """
        pass

    def __iter__(self, *args, **kwargs): # real signature unknown
        """ Implement iter(self). """
        pass

    def __len__(self, *args, **kwargs): # real signature unknown
        """ Return len(self). """
        pass

    def __le__(self, *args, **kwargs): # real signature unknown
        """ Return self<=value. """
        pass

    def __lt__(self, *args, **kwargs): # real signature unknown
        """ Return self<value. """
        pass

    def __mul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value.n """
        pass

    @staticmethod # known case of __new__
    def __new__(*args, **kwargs): # real signature unknown
        """ Create and return a new object.  See help(type) for accurate signature. """
        pass

    def __ne__(self, *args, **kwargs): # real signature unknown
        """ Return self!=value. """
        pass

    def __repr__(self, *args, **kwargs): # real signature unknown
        """ Return repr(self). """
        pass

    def __reversed__(self): # real signature unknown; restored from __doc__
        """ L.__reversed__() -- return a reverse iterator over the list """
        pass

    def __rmul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value. """
        pass

    def __setitem__(self, *args, **kwargs): # real signature unknown
        """ Set self[key] to value. """
        pass

    def __sizeof__(self): # real signature unknown; restored from __doc__
        """ L.__sizeof__() -- size of L in memory, in bytes """
        pass

    __hash__ = None

查看

```
#### 元祖

```
定义：与列表类似，只不过［］改成（）
特性：
1.可存放多个值
2.不可变
3.按照从左到右的顺序定义元组元素，下标从0开始顺序访问，有序

```
创建元祖

```
ages = (11, 22, 33, 44, 55)
或
ages = tuple((11, 22, 33, 44, 55))

```
常用操作

索引
切片
循环
长度
包含

常用方法

```
class tuple(object):
    """
    tuple() -> empty tuple
    tuple(iterable) -> tuple initialized from iterable's items
    
    If the argument is a tuple, the return value is the same object.
    """
    def count(self, value): # real signature unknown; restored from __doc__
        """ T.count(value) -> integer -- return number of occurrences of value """
        return 0

    def index(self, value, start=None, stop=None): # real signature unknown; restored from __doc__
        """
        T.index(value, [start, [stop]]) -> integer -- return first index of value.
        Raises ValueError if the value is not present.
        """
        return 0

    def __add__(self, *args, **kwargs): # real signature unknown
        """ Return self+value. """
        pass

    def __contains__(self, *args, **kwargs): # real signature unknown
        """ Return key in self. """
        pass

    def __eq__(self, *args, **kwargs): # real signature unknown
        """ Return self==value. """
        pass

    def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass

    def __getitem__(self, *args, **kwargs): # real signature unknown
        """ Return self[key]. """
        pass

    def __getnewargs__(self, *args, **kwargs): # real signature unknown
        pass

    def __ge__(self, *args, **kwargs): # real signature unknown
        """ Return self>=value. """
        pass

    def __gt__(self, *args, **kwargs): # real signature unknown
        """ Return self>value. """
        pass

    def __hash__(self, *args, **kwargs): # real signature unknown
        """ Return hash(self). """
        pass

    def __init__(self, seq=()): # known special case of tuple.__init__
        """
        tuple() -> empty tuple
        tuple(iterable) -> tuple initialized from iterable's items
        
        If the argument is a tuple, the return value is the same object.
        # (copied from class doc)
        """
        pass

    def __iter__(self, *args, **kwargs): # real signature unknown
        """ Implement iter(self). """
        pass

    def __len__(self, *args, **kwargs): # real signature unknown
        """ Return len(self). """
        pass

    def __le__(self, *args, **kwargs): # real signature unknown
        """ Return self<=value. """
        pass

    def __lt__(self, *args, **kwargs): # real signature unknown
        """ Return self<value. """
        pass

    def __mul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value.n """
        pass

    @staticmethod # known case of __new__
    def __new__(*args, **kwargs): # real signature unknown
        """ Create and return a new object.  See help(type) for accurate signature. """
        pass

    def __ne__(self, *args, **kwargs): # real signature unknown
        """ Return self!=value. """
        pass

    def __repr__(self, *args, **kwargs): # real signature unknown
        """ Return repr(self). """
        pass

    def __rmul__(self, *args, **kwargs): # real signature unknown
        """ Return self*value. """
        pass

```
#### 字典

```
定义：｛key1:value1,key2:value2｝,key-value结构，key必须可hash
特性：
1.可存放多个值
2.可修改指定key对应的值，可变
3.无序

```
字典的创建

```
person = {"name": "sb", 'age': 18}
或
person = dict(name='sb', age=18)
person = dict({"name": "sb", 'age': 18})
person = dict((['name','sb'],['age',18]))
{}.fromkeys(seq,100) #不指定100默认为None
注意：
>>> dic={}.fromkeys(['k1','k2'],[])
>>> dic
{'k1': [], 'k2': []}
>>> dic['k1'].append(1)
>>> dic
{'k1': [1], 'k2': [1]} 

```
字典常用操作

索引
新增
删除
键、值、键值对
循环
长度

字典工厂函数dict()

```
class dict(object):
    """
    dict() -> new empty dictionary
    dict(mapping) -> new dictionary initialized from a mapping object's
        (key, value) pairs
    dict(iterable) -> new dictionary initialized as if via:
        d = {}
        for k, v in iterable:
            d[k] = v
    dict(**kwargs) -> new dictionary initialized with the name=value pairs
        in the keyword argument list.  For example:  dict(one=1, two=2)
    """
    def clear(self): # real signature unknown; restored from __doc__
        """ D.clear() -> None.  Remove all items from D. """
        pass

    def copy(self): # real signature unknown; restored from __doc__
        """ D.copy() -> a shallow copy of D """
        pass

    @staticmethod # known case
    def fromkeys(*args, **kwargs): # real signature unknown
        """ Returns a new dict with keys from iterable and values equal to value. """
        pass

    def get(self, k, d=None): # real signature unknown; restored from __doc__
        """ D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None. """
        pass

    def items(self): # real signature unknown; restored from __doc__
        """ D.items() -> a set-like object providing a view on D's items """
        pass

    def keys(self): # real signature unknown; restored from __doc__
        """ D.keys() -> a set-like object providing a view on D's keys """
        pass

    def pop(self, k, d=None): # real signature unknown; restored from __doc__
        """
        D.pop(k[,d]) -> v, remove specified key and return the corresponding value.
        If key is not found, d is returned if given, otherwise KeyError is raised
        """
        pass

    def popitem(self): # real signature unknown; restored from __doc__
        """
        D.popitem() -> (k, v), remove and return some (key, value) pair as a
        2-tuple; but raise KeyError if D is empty.
        """
        pass

    def setdefault(self, k, d=None): # real signature unknown; restored from __doc__
        """ D.setdefault(k[,d]) -> D.get(k,d), also set D[k]=d if k not in D """
        pass

    def update(self, E=None, **F): # known special case of dict.update
        """
        D.update([E, ]**F) -> None.  Update D from dict/iterable E and F.
        If E is present and has a .keys() method, then does:  for k in E: D[k] = E[k]
        If E is present and lacks a .keys() method, then does:  for k, v in E: D[k] = v
        In either case, this is followed by: for k in F:  D[k] = F[k]
        """
        pass

    def values(self): # real signature unknown; restored from __doc__
        """ D.values() -> an object providing a view on D's values """
        pass

    def __contains__(self, *args, **kwargs): # real signature unknown
        """ True if D has a key k, else False. """
        pass

    def __delitem__(self, *args, **kwargs): # real signature unknown
        """ Delete self[key]. """
        pass

    def __eq__(self, *args, **kwargs): # real signature unknown
        """ Return self==value. """
        pass

    def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass

    def __getitem__(self, y): # real signature unknown; restored from __doc__
        """ x.__getitem__(y) <==> x[y] """
        pass

    def __ge__(self, *args, **kwargs): # real signature unknown
        """ Return self>=value. """
        pass

    def __gt__(self, *args, **kwargs): # real signature unknown
        """ Return self>value. """
        pass

    def __init__(self, seq=None, **kwargs): # known special case of dict.__init__
        """
        dict() -> new empty dictionary
        dict(mapping) -> new dictionary initialized from a mapping object's
            (key, value) pairs
        dict(iterable) -> new dictionary initialized as if via:
            d = {}
            for k, v in iterable:
                d[k] = v
        dict(**kwargs) -> new dictionary initialized with the name=value pairs
            in the keyword argument list.  For example:  dict(one=1, two=2)
        # (copied from class doc)
        """
        pass

    def __iter__(self, *args, **kwargs): # real signature unknown
        """ Implement iter(self). """
        pass

    def __len__(self, *args, **kwargs): # real signature unknown
        """ Return len(self). """
        pass

    def __le__(self, *args, **kwargs): # real signature unknown
        """ Return self<=value. """
        pass

    def __lt__(self, *args, **kwargs): # real signature unknown
        """ Return self<value. """
        pass

    @staticmethod # known case of __new__
    def __new__(*args, **kwargs): # real signature unknown
        """ Create and return a new object.  See help(type) for accurate signature. """
        pass

    def __ne__(self, *args, **kwargs): # real signature unknown
        """ Return self!=value. """
        pass

    def __repr__(self, *args, **kwargs): # real signature unknown
        """ Return repr(self). """
        pass

    def __setitem__(self, *args, **kwargs): # real signature unknown
        """ Set self[key] to value. """
        pass

    def __sizeof__(self): # real signature unknown; restored from __doc__
        """ D.__sizeof__() -> size of D in memory, in bytes """
        pass

    __hash__ = None

```

#### 集合

```
{1,2,3,1}
或
定义可变集合set
>>> set_test=set('hello')
>>> set_test
{'l', 'o', 'e', 'h'}
改为不可变集合frozenset
>>> f_set_test=frozenset(set_test)
>>> f_set_test
frozenset({'l', 'e', 'h', 'o'})

```
常用操作

```
　 in
not in
＝＝
！＝
<,<=
>,>=
|,|=:合集
&.&=:交集
－,－=:差集
^,^=:对称差分

```
方法如下

```
class set(object):
    """
    set() -> new empty set object
    set(iterable) -> new set object
    
    Build an unordered collection of unique elements.
    """
    def add(self, *args, **kwargs): # real signature unknown
        """
        Add an element to a set.
        
        This has no effect if the element is already present.
        """
        pass

    def clear(self, *args, **kwargs): # real signature unknown
        """ Remove all elements from this set. """
        pass

    def copy(self, *args, **kwargs): # real signature unknown
        """ Return a shallow copy of a set. """
        pass

    def difference(self, *args, **kwargs): # real signature unknown
        """
        相当于s1-s2
        
        Return the difference of two or more sets as a new set.
        
        (i.e. all elements that are in this set but not the others.)
        """
        pass

    def difference_update(self, *args, **kwargs): # real signature unknown
        """ Remove all elements of another set from this set. """
        pass

    def discard(self, *args, **kwargs): # real signature unknown
        """
        与remove功能相同，删除元素不存在时不会抛出异常
        
        Remove an element from a set if it is a member.
        
        If the element is not a member, do nothing.
        """
        pass

    def intersection(self, *args, **kwargs): # real signature unknown
        """
        相当于s1&s2
        
        Return the intersection of two sets as a new set.
        
        (i.e. all elements that are in both sets.)
        """
        pass

    def intersection_update(self, *args, **kwargs): # real signature unknown
        """ Update a set with the intersection of itself and another. """
        pass

    def isdisjoint(self, *args, **kwargs): # real signature unknown
        """ Return True if two sets have a null intersection. """
        pass

    def issubset(self, *args, **kwargs): # real signature unknown
        """ 
        相当于s1<=s2
        
        Report whether another set contains this set. """
        pass

    def issuperset(self, *args, **kwargs): # real signature unknown
        """
        相当于s1>=s2
        
         Report whether this set contains another set. """
        pass

    def pop(self, *args, **kwargs): # real signature unknown
        """
        Remove and return an arbitrary set element.
        Raises KeyError if the set is empty.
        """
        pass

    def remove(self, *args, **kwargs): # real signature unknown
        """
        Remove an element from a set; it must be a member.
        
        If the element is not a member, raise a KeyError.
        """
        pass

    def symmetric_difference(self, *args, **kwargs): # real signature unknown
        """
        相当于s1^s2
        
        Return the symmetric difference of two sets as a new set.
        
        (i.e. all elements that are in exactly one of the sets.)
        """
        pass

    def symmetric_difference_update(self, *args, **kwargs): # real signature unknown
        """ Update a set with the symmetric difference of itself and another. """
        pass

    def union(self, *args, **kwargs): # real signature unknown
        """
        相当于s1|s2
        
        Return the union of sets as a new set.
        
        (i.e. all elements that are in either set.)
        """
        pass

    def update(self, *args, **kwargs): # real signature unknown
        """ Update a set with the union of itself and others. """
        pass

    def __and__(self, *args, **kwargs): # real signature unknown
        """ Return self&value. """
        pass

    def __contains__(self, y): # real signature unknown; restored from __doc__
        """ x.__contains__(y) <==> y in x. """
        pass

    def __eq__(self, *args, **kwargs): # real signature unknown
        """ Return self==value. """
        pass

    def __getattribute__(self, *args, **kwargs): # real signature unknown
        """ Return getattr(self, name). """
        pass

    def __ge__(self, *args, **kwargs): # real signature unknown
        """ Return self>=value. """
        pass

    def __gt__(self, *args, **kwargs): # real signature unknown
        """ Return self>value. """
        pass

    def __iand__(self, *args, **kwargs): # real signature unknown
        """ Return self&=value. """
        pass

    def __init__(self, seq=()): # known special case of set.__init__
        """
        set() -> new empty set object
        set(iterable) -> new set object
        
        Build an unordered collection of unique elements.
        # (copied from class doc)
        """
        pass

    def __ior__(self, *args, **kwargs): # real signature unknown
        """ Return self|=value. """
        pass

    def __isub__(self, *args, **kwargs): # real signature unknown
        """ Return self-=value. """
        pass

    def __iter__(self, *args, **kwargs): # real signature unknown
        """ Implement iter(self). """
        pass

    def __ixor__(self, *args, **kwargs): # real signature unknown
        """ Return self^=value. """
        pass

    def __len__(self, *args, **kwargs): # real signature unknown
        """ Return len(self). """
        pass

    def __le__(self, *args, **kwargs): # real signature unknown
        """ Return self<=value. """
        pass

    def __lt__(self, *args, **kwargs): # real signature unknown
        """ Return self<value. """
        pass

    @staticmethod # known case of __new__
    def __new__(*args, **kwargs): # real signature unknown
        """ Create and return a new object.  See help(type) for accurate signature. """
        pass

    def __ne__(self, *args, **kwargs): # real signature unknown
        """ Return self!=value. """
        pass

    def __or__(self, *args, **kwargs): # real signature unknown
        """ Return self|value. """
        pass

    def __rand__(self, *args, **kwargs): # real signature unknown
        """ Return value&self. """
        pass

    def __reduce__(self, *args, **kwargs): # real signature unknown
        """ Return state information for pickling. """
        pass

    def __repr__(self, *args, **kwargs): # real signature unknown
        """ Return repr(self). """
        pass

    def __ror__(self, *args, **kwargs): # real signature unknown
        """ Return value|self. """
        pass

    def __rsub__(self, *args, **kwargs): # real signature unknown
        """ Return value-self. """
        pass

    def __rxor__(self, *args, **kwargs): # real signature unknown
        """ Return value^self. """
        pass

    def __sizeof__(self): # real signature unknown; restored from __doc__
        """ S.__sizeof__() -> size of S in memory, in bytes """
        pass

    def __sub__(self, *args, **kwargs): # real signature unknown
        """ Return self-value. """
        pass

    def __xor__(self, *args, **kwargs): # real signature unknown
        """ Return self^value. """
        pass

    __hash__ = None

```

#### byte类型

```
定义：存8bit整数，数据基于网络传输或内存变量存储到硬盘时需要转成bytes类型,字符串前置b代表为bytes类型
>>> x
'hello sb'
>>> x.encode('gb2312')
b'hello sb'

```
#### 数据类型转换内置表
[内置转换表](https://images2015.cnblogs.com/blog/1036857/201610/1036857-20161011101326368-808569007.png)

#### 运算符
