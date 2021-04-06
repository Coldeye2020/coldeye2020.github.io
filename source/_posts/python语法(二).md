---
title: Python(一)Python中级语法
date: 2020-10-20 14:20:17
categories:
- Tech 
- Language
- Python
tags: [Python]
mathjax: false
urlname: python_grammar_intermediate
keywords: [Python, Grammar]
description:
---

{% note info %}

**说明**

+ 本文是在大三上学期看`廖雪峰Python`教程所做笔记，后并为勘误，如有错误，请谅解
+ 另外，本文并不是一份严谨可靠的Python教程，更多的是我学习Python`中级语法设计时的一些心得和感悟

{% endnote %}

<!--more-->

### 定义默认参数要牢记一点：默认参数必须指向不变对象！（最重要！！！）

```python
# 以下就是将默认参数指向可变对象的例子
def appenderror(L=[])
	L.append('Error')
    return L

# 我们传入参数正常使用时
In[0] >>> appenerror([1,2,3])
Out[0] >>> [1,2,3,'Error']

In[1] >>> appenerror(['S','K','G'])
Out[1] >>> ['S','K','G','Error']

# 但我们使用默认参数时
In[2] >>> appenerror()
Out[2] >>> ['Error']
# 似乎也没毛病

# 但是我们再次调用函数并使用默认参数时
In[3] >>> appenerror()
Out[3] >>> ['Error','Error']

# 显然得到的不是我们想要的答案
'''
	原因：这主要是由于Python的函数在使用默认参数时，是将默认参数先计算出来的，事实上，如果将默认参数指向可变对象，他也会创造出一个可变对象，对这个指向对象的任何操作都会影响到后续
'''

# 那我们要是就是想要使用列表作为默认参数呢？
'''
	可采用的方法: 引入 None 或者其他任何不可变对象，
'''
def appenderror(L=None)
	if L is None:
        L = []
	L.append('Error')
    return L
# 当然也可以吧L换做任何字符串常量，但最好还是使用None，经过判断语句之后再把其改为想要的数据类型
```

### 可变长参数的妙用

```python
# A函数 未使用可变长
def calc(numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

# A函数使用
calc([1,2,3,4,5])


# B函数 使用可变长参数(其中可变长部分传入的元素是以tuple的方式传入的)
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

# B函数使用
calc(1,2,3,4,5)

# 如果我们想用可迭代对象的元素当做可变长参数传入函数B
d = [1, 2, 3, 4, 5]
calc(*d)
```

### 关键字参数

```python
'''
	‘关键字参数’ 区别于 ‘参数名传参’ 的点在于
		1.关键字传参时是不会有提示的，即函数不会把参数名字给你，一般函数定义如下:
			def func(**kwarg):
			 	...
		  并且关键字传参时不限制数量的，你可以一直写下去，只有函数能够识别出来，如下例:
		  	func(name='小明', age=18, hometowm='湖北')
		  他是通过来生成一个dict，并根据你的输入产生键值对，来进行值的传递的
		  关键字参数的传递时是一定是要给出参数名的，这与参数名传参时可有可无不同（如果不给参数名则默认严格遵守位置传参的规则）
         2.位置参数（参数名传参）时是会有提示的，即函数不会把参数名字给你，这一点在好的文本编辑器上体现的比较明显      
     所以如果除开‘数量限制’和‘是否必须加上参数名’这两点来说的话，关键字参数真的和位置参数的（参数名传参的方式是很像了），几乎可以说是等同了
'''

# 请欣赏表演:
In [0]:	def pri(name='小红', age=12 ,**kw):
		print('name:', name, 'age', age)

In [1]:	c = {'name':'fuck', 'age':'就这？'}
     	pri(**c)
Out[1]: name: fuck age: 就这？
            
In [2]:	c = {'name':'fuck', 'age2':'sb'}
     	pri(**c)
Out[2]: name: fuck age: 12            

'''
	关键字参数的掠夺能力:
	容易看出的是:
		当把字典通过"**号表达式"作为一个个键值对传入后，他会先判别时候是属于未知参数，如果不都不是才会传递给关键字参数，这体现了关键字参数和未知参数通过“参数名传参的”关系。
'''            

'''
	让人又爱又恨的 ‘*号表达式’:
		在很多情况下，当我们调用含有关键字或者可变长参数的函数式，当我们想传入可迭代对象或者dict时，通常不是将其作为一个整体，而是想将其中的每一个元素传入函数，所以我们会使用 *表达式来拆分他们。
		1.  *可迭代对象 返回的是很多个单独的元素，但如果他们被作为不定长参数接收后，将会重新整合成一个tuple。
		2. **dict 返回的是很多个键值对，但形式不是标准的键值对，而是为‘key=value’，但如果他们作为关键字参数被接收后，将会重新整合为一个新的dict。
		3. *dict 返回一个由key组成的tuple。
		当然 ‘*号表达式’ 的作用绝不仅限于给函数传参时使用，但我绝不建议你不这样做，特别是对于新手来说。
'''

'''
	否定了位置传参可能的，命名关键字参数：
		可以进行位置传参也可以进行关键字传参的参数:必选参数（必须传入一个），默认参数（可以传入一个或零个）
		只能进行位置传参的参数:可变长参数（无限位置传参）
		只能进行关键字传参的参数:命名关键字参数（会有提示，也可以设置默认参数，但有限，并且如果没有设置默认则必须传入参数），关键字参数（无限关键字传参）
'''
# 在下例中: name为必选参数，age为默认参数，args为可变长参数，city为默认命名关键字参数（可以不传入），job为必选命名关键字参数（必须传入），kwargs为关键字参数（无限传参）
def person(name, age=12, *args, city='Beijing', job, **kwargs):
    print(name, age, args, city, job)
# 引入命名关键字参数带来的新操作
# 1.对于默认命名关键字参数: 如果你想设置一个可以选传的参数A，如果你简单的设置为默认位置参数，那么在前面通过位置传参的过程中，如果你不想给这个参数传参，则参数A之后的所有默认位置参数和“可变长参数”（特别是可变长，如果不把A用“位置传参”填上，你就永远无法把参数传到可变长那里）就都不可以进行位置传参了，除非用“位置传参”（如果你用关键字传参也不行，只能是位置传参）把这个参数A填上，这就与你想设置一个选传参数A的初心矛盾了。
# 如下例，第一个函数将可选参数age定义为默认位置参数，但显然，如果不给age进行位置传参，则永远无法给可变长参数args进行传参，第二个函数将可选参数age定义为默认命名关键字参数，这次，即是不给age传参，仍可以给args传参
def person(name, age=12, *args, city='beijing', job='guangzhou'):
    print(name, age, args, city, job)
>>>	person('xiaohong', '他是个傻子')    
xiaohong 他是个傻子 () beijing guangzhou

def person(name, *args, city='beijing', age=12, job='guangzhou'):
    print(name, age, args, city, job)
>>>	person('xiaohong', '他是个傻子')    
xiaohong 12 ('他是个傻子',) beijing guangzhou
    
# 2.pass，从现在的是用来看，似乎必选命名关键字参数能做的，必选位置参数都能做的，看似好像就是简单地把其传参方式减少了


'''
	如果看了上面关于‘*号表达式’的表述后，你产生了一些疑问，这是正常的。
	请看下面几个例子
'''

# 请欣赏表演:
In [0]:	def pri(name='小红', age=12 ,**kw):
		print('name:', name, 'age', age)

# 将dict作为参数名进行传参的例子
In [1]:	c = {'name':'fuck', 'age':'就这？'}
     	pri(**c)
Out[1]: name: fuck age: 就这？

# 将可迭代对象作为参数进行位置传参的例子
In [2]:	d = ('就这水平？', 12)
     	pri(*d)
Out[2]: name: 就这水平？ age: 12

# 用单‘*’星号表达式拆解dict
In [2]: pri(*c)
Out[2]: name: name age: age            

# 我们来观察一下，是位置参数的掠夺能力强还是的关键字参数能力的强
In [2]:	d = ('就这水平？', 12)
		pri( *d,**c)
Out[2]: TypeError: pri() got multiple values for argument 'name'
# 根据上面代码的结果，我们可以得知还是positional argument的掠夺能力更强一些，只要满足关键字，就会被位置参数夺去

```

### 混合传参

```python
'''
	虽说上面这些讨论可以初步看出python在函数传参时的一些规则，但是仍然十分的混乱，所以我们就直接来介绍一种极端情况下的例子，来看看python到底是如何进行参数分配的
'''

# 规则1:函数的参数定义时的顺序: 必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
>>> def f1(a, b, c=0, *args, **kw):
    	print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)
        

>>>	def f2(a, b, c=0, *, d, **kw):
    	print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)
        
        
>>> def f1(c=0, a, b, *args, **kw):
    	print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)
SyntaxError: non-default argument follows default argument        
        
# 规则2:调用函数传参时的顺序: 位置传参, 关键字(参数名)传参（不讲究顺序），例如
>>> f1(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {}

>>> f1(1, 2, 3, x=99, 'a', 'b')
SyntaxError: positional argument follows keyword argument

# 规则3:当使用位置传参时前面的参数叠满后，移至才会下一个参数（可能不是很好理解），请看下例
>>> f1(1, 3, 'a', 'b', x=99)
a = 1 b = 3 c = a args = ('b',) kw = {'x': 99}

# 规则4:表明某一个参数接受了两个或以上的传参时则会报错,并不会是更新为最后传递的参数
>>> f1(1, 2, 3, 'a', 'b', a=99)
TypeError: f1() got multiple values for argument 'a'

# 规则5:不同参数对传参的掠夺能力:必选参数 > 默认参数 > 可变参数 > 命名关键字参数 > 关键字参数
# 前面三个参数的大小关系主要是由其‘函数定义时就已经定好的参数位置关系’决定，关键字参数和可变参数的大小关系并不会影响什么，因为他们接受的传参类型完全不同，一个只能是value，一个必须是key=value。而后面关键字参数的掠夺能力与前三个参数的关系则很重要，如下例:
>>> f1(1, 2, 'b', a=99)
TypeError: f1() got multiple values for argument 'a'
```

### 字符串细节

```python
# 众所周知，Python把当做了字符串当做了一个tuple来处理
# 所以利用切片和迭代的性质可以非常快捷的处理字符串

'''
	切片小细节:
		请问下面代码的输出结果是什么?
'''

a = []

>>>	a[:-2]
[]
>>>	a[:-1]
[]

>>>	a[0:]
[]
>>>	a[1:]
[]
>>>	a[2:]
[]

>>>	a[2:1]
[]
>>>	a[2:-1]
[]
>>>	a[-2:1]
[]

'''
	根据以上代码得结果表明: 与索引不同的是，切片在超出范围的时候并不会报错，而是将满足要求的元素进行输出
	验证代码如下:
'''
b = [1,2,3,4]

>>>	b[-55:55]
[1, 2, 3, 4]

>>>	b[1:55]
[2, 3, 4]

>>>	b[-55:-1]
[1, 2, 3]

>>> b[-1:-5]
[]

>>> b[5:1]
[]

>>>	b[-1:-5:-1]
[4, 3, 2, 1]

>>>	b[5:-1:-1]
[4, 3, 2, 1]

# 根据上面几个例子打开可以归纳出切片的导出细则:
# 1.首先计算出第一,二个index所代表的位置
# 2.观察是否满足第三个value的正负号规则
# 3.如果不满足直接返回空list[]
# 4.如果满足，则计算切片是否超出list范围
# 5.如果超出则把超出的一边或者两边定义在list的边界上
# 6.如果未超出则按正常次序计算

'''
	question:
		利用切片操作，实现一个trim()函数，去除字符串首尾的空格，
'''

def trim(s):
    if s == '':
        return s
    while s[-1:] == ' ':
          s = s[:-1]
    while s[:1] == ' ':
          s = s[1:]
    return s

# 现在来解释一下，为什么要引入这个例子，因为:
# 你可能认为 s[-1:] 和 s[-1]是同一个东西，但是事实上，前者为切片，超出范围会自动限制在list边界处，后者为索引，超出范围会直接报错, 我们看一个更为容易理解的例子:
s = []

>>>	s[-1:]
[]
>>> s[-1]
Error
# 上例中对于lenth为0的list而言，s[-1:] 即代表s的全部即[]，而s[-1] 则会报错显示index超出了。

但事实上，上述问题才用的方法并不是值得推崇的，因为在利用切片赋值时会开辟内存空间，从而占用了大量不必要的内存，所以比较好的做法是先找到非' '元素的index，再通过切片一次性赋值
```

### list` , `tuple` , `dict` 一类的迭代原理 与 `zip` 的区别

```python
>>>	for x, y in [((1, 1), (2, 4)), (3, 9)]:
...    	print(x, y)
(1,1) (2,4)
3 9

'''
	对上述代码结果的解释:
		对于可迭代对象[((1, 1), (2, 4)), (3, 9)]而言,其第一个迭代元素为((1, 1), (2, 4))
												其第二个迭代元素为(3,9)
		所以将第一次迭代时, x = (1,1), y = (2, 4)
			 第二次迭代时, x = 3, y = 9
	但是对于generator 和 iterator的原理还有待考量
'''

# zip()函数
>>>	zip([1,2,3],[5,3,8])
# 他会生成一个迭代器，且每次的迭代元素是对应的元素组成的一个tuple
# 相当于他会生成一个[(1,5),(2,3),(3,8)]的可迭代对象
```

### 细究 `list` 生成式

```python
'''
	探究list生成式中，if放前面和放后面的区别
'''
>>>	L1 = ['Hello', 'World', 18, 'Apple', None]
>>> L1
['Hello', 'World', 18, 'Apple', None]

>>>	L2 = [s.lower() for s in L1 if isinstance(s,str)]
>>>	L2
['hello', 'world', 'apple']

>>>	L3 = [s.lower() if isinstance(s,str) else s for s in L1]
>>>	L3
['hello', 'world', 18, 'apple', None]

'''
	上例可知对于列表生成式而言，
		if放for前面: 和else连用形成一个类似三目运算符的效果，其返回的是一个值，并不能作为筛选依据，所以if放前面时，并不会改变生成list的元素个数
		if放for后面: 构成对for的迭代元素的筛选依据，其决定了迭代的元素s是否返回给生成式，所以不会影响到最终生成元素的值，而是对元素进行筛选，改变生成list的元素个数
'''
```

### `generator` 创建方式

```python
# 方式1，类似于列表生成式，但是要将列表生成式的[]，改为()
>>>	a = (i**2 for i in range(10))
>>>	for i in a:
...    print(i)
0
1
4
9
16
25
36
49
64
81
# 也可以通过调用next(a)来进行遍历操作
```

```python
# 方式2，通过 yield 可以将普通的函数转换为列表生成式
>>>	define a(max):
...		i, sum = 1, 0
...    	while(i <= max):
...			sum += i
...			yield sum
...			i += 1

>>>	b = a(5)
>>>	b
<generator object a at 0x0000027213B0CD68>
>>>	for i in b:
    	print(i)
1
3
6
10
15
```

```python
# 但是当我们使用函数来当生成器时，我们很难拿到return的值，事实上，默认生成器里面只有yield的值，如下
>>>	def fib_ge(max):
...	    n, a, b = 0, 0, 1
...	    while(n<max):
...	        yield b
...	        a, b = b, a+b
...	        n += 1
...	    return 'done'


>>>	for i in fib_ge(11):
...	    print(i)

1
1
2
3
5
8
13
21
34
55
89

# 如果想要得到函数的真正返回值，我们需要使用next函数。
>>>	def fib_ge(max):
...	    n, a, b = 0, 0, 1
...	    while(n<max):
...	        yield b
...	        a, b = b, a+b
...	        n += 1
...	    return 'done'

>>>	a = fib_ge(11)
>>>	while True:
...	    try:
...	        x = next(a)
...	        print(x)
...	    except StopIteration as e:
...	        print(e.value)
...	        break

1
1
2
3
5
8
13
21
34
55
89
done
```

> 还有一件事，使用generator的时候一定要把它先赋给某个变量，不然对generator调用next()函数永远都只会得到相同的初始值时

###  高阶函数

```python
'''
	介绍几个比较常用的python内置的高阶函数
'''

# 1. map()
'''
	用法: map(用于转换func,可迭代序列A)
	返回值: Iterator
	功能: 将A中的每一个元素都带入func中，得到的返回值作为返回的iterator对应的元素
'''

# 2. reduce()
'''
	用法: reduce(用于计算的func,可迭代序列B)
	返回值: 最后的结果
	功能: func必须接收两个变量，将B中的头两个元素带入func中得到的结果再与第三个一起作为变量传递给func，如此循环，直至到最后一个元素
'''

# 3. filter()
'''
	用法: filter(用于判断的func,可迭代序列C)
	返回值: Iterator
	功能:将C中的每一个元素都带入func中进行检验，返回值为True保留，为False则被丢弃，所有保留下来的元素成为iterator对应的元素
'''

# 4.sorted()
'''
	用法:sorted(待排序的list或者dict D, key=用于转换的func, reverse=True)
	返回值: Iterator
	功能:将D中的元素先通过func转换之后再进行排序.
	Example:
		sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
		['about', 'bob', 'Credit', 'Zoo']
'''
```

### 返回函数(闭包)

```python
# 闭包的关键点在于理解变量的作用域
'''
	下面是一些关于如何理解返回函数的例子:
		例子1 返回函数的定义
		例子2，3 使用返回函数时的常见错误(对变量作用域的误解)
		例子4，5 闭包的好处(4.当闭包执行完后，仍然能够保持住当前的运行环境(记忆性), 5.闭包可以根据外部作用域的局部变量来得到不同的结果(更灵活))
'''

# 例1: 闭包的基本定义:在函数中定义了函数，并且内函数调用了外部函数的变量
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum

>>>	a = lazy_sum(1,2,3,5)
>>>	a()
11





# 例2: 返回函数中使用可变变量时
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs

f1, f2, f3 = count()

>>>	f1()
9
>>>	f2()
9
>>>	f3()
9

'''
	解释为何会出现如下结果:
		官方解释: 返回的函数并没有立刻执行，而是直到调用了f()才执行
		我的理解: 在调取返回函数时,函数开始找参数，根据之前的规则我们知道函数肯定是从上往下挨个找的，当他里面没有定义i这个local变量时，就回去找他的下面一层（外函数）中是否有定义i，发现确实是有定义的，于是就返回该i的平方，此时i为3，故而都返回的是9
		奇怪之处: 在C语言里面，一般来说循环变量用完就会被扔掉了，Python为何可以找到呢？原因在于Python并没有规定循环变量的作用域，如果他在地面上使用，那么全局的i都会被改变，如果他在函数A里面使用，那么函数A的i变量就会被改变，如下例:
'''
def count():
    i = 1000
    for i in range(10):
        pass
    print(i)
    
>>>	count()
9

# 代码改进
def count():
    fs = []
    def f_2(j):			# 此处的j的作用域是函数f_2(),比起外函数count的j,f在被调用时会优先选择f_2()的j
        def f():
            return j*j
        return f
    for j in range(4) 	# 此处的j的作用域是整个函数count 
   		fs.append(f_2(j))	# 这是起决定性的一步，在函数f_2被调用的时候,f_2里面所用的变量就已经被计算出来了,此时返回的f，在之后的调用过程中的参数会取决于此时f_2中的所有参数
    return fs






# 例3: 在返回函数中是不能更改外部变量的
def foo(): 
    a = 1
    def bar(): 
        a = a + 1
        return a
    return bar

'''
	报错原因: 这是因为在执行代码 c = foo()时，python会导入全部的闭包函数体bar()来分析其的局部变量，python规则指定所有在赋值语句左面的变量都是局部变量，则在闭包bar()中，变量a在赋值符号"="的左面，被python认为是bar()中的局部变量。再接下来执行print c()时，程序运行至a = a + 1时，因为先前已经把a归为bar()中的局部变量，所以python会在bar()中去找在赋值语句右面的a的值，结果找不到，就会报错。解决的方法很简单
	1. 使用nonlocal或global的关键字
		
	2. 使用list等可变类型
'''

# 1
def foo(): 
	a = 1
    def bar(): 
        nonlocal a
        a += 1
        return a 
    return bar


# 2
def foo(): 
	a = [1]
    def bar(): 
        a[0] = a[0] + 1
        return a[0] 
    return bar






# 例4: 返回函数保持住当前的运行环境
origin = [0, 0] # 坐标系统原点 
legal_x = [0, 50] # x轴方向的合法坐标 
legal_y = [0, 50] # y轴方向的合法坐标 
def create(pos=origin): 
    def player(direction,step): 
  	# 这里应该首先判断参数direction,step的合法性，比如direction不能斜着走，step不能为负等 
    # 然后还要对新生成的x，y坐标的合法性进行判断处理，这里主要是想介绍闭包，就不详细写了。 
    	new_x = pos[0] + direction[0]*step 
		new_y = pos[1] + direction[1]*step 
		pos[0] = new_x 
		pos[1] = new_y # 注意！此处不能写成 pos = [new_x, new_y]，原因在上文有说过 
		return pos 
	return player 
  
player = create() # 创建棋子player，起点为原点 
print(player([1,0],10)) # 向x轴正方向移动10步 
print(player([0,1],20)) # 向y轴正方向移动20步 
print(player([-1,0],10)) # 向x轴负方向移动10步

[10, 0]
[10, 20]
[0, 20]

'''
	我来谈一下对返回函数记忆性的理解:
		在上述代码 ‘player = create()’ 执行时，执行了函数creat, creat()中player()外的变量全部被创造出来了,并放置在某一个未知空间(其实就只有两个变量，即变量pos和函数变量player),在调用player时候，因为是通过可变类型list进行传递的参数，所以是可以在返回函数执行过程中改变外部变量的值的，于是存在于未知空间的变量pos就这样被改来改去，并且每次调用player时，接受的也是这样的一个pos,于是通过这个pos变量，具有了记忆性，如果pos不能使list类型，则需要在中player中使用nonlocal关键字
'''


# 例5: 返回函数根据外部作用域的局部变量来得到不同的结果（灵活性）
def make_filter(keep): 
    def the_filter(file_name): 
        file = open(file_name) 
        lines = file.readlines() 
        file.close() 
        filter_doc = [i for i in lines if keep in i] 
        return filter_doc 
    return the_filter

# 显然当我们传递进去不同参数是,我们便可以进行不一样的功能
# 如果我们需要取得文件"result.txt"中含有"pass"关键字的行，则可以这样使用例子程序
filter = make_filter("pass")
filter_result = filter("result.txt")
```

### 聪明人才看得懂的例子

```python
'''
	请说出下面两个生成器的区别
'''

def _odd_iter():
    a = 3
    while True:
        yield a
        a += 2

def _not_divisible(n):
    return lambda x: x % n > 0

def primes():
    yield 2
    it = _odd_iter() # 初始序列
    while True:
        n = next(it) # 返回序列的第一个数
        yield n
        it = filter(_not_divisible(n), it) # 构造新序列

def primes_2():
    yield 2
    it = _odd_iter() # 初始序列
    while True:
        n = next(it) # 返回序列的第一个数
        yield n
        it = filter(lambda x: x % n > 0, it) # 构造新序列

pri = prime()
pri_2 = prime_2()
        
        
'''
	傻瓜才会看得程序运行顺序分析:
		对于Primes()这个生成器的对象pri而言,他的运行顺序为:
			第一次执行next(pri):
				1. 执行 yield 2
				2. 跳出
				
			第二次执行next(pri):
				1. 执行 it = _odd_iter(), 将生成一个‘从三开始，只含奇数’的迭代对象
				2. 进入 while()循环
				3. 第一次执行 next(it):
					1. return 3
					2. 跳出
				4. 将返回值‘3’赋给n
				5. yield n(3)
				6. 跳出
				
			第三次执行next(pri):
				1. 执行 it = filter(_not_divisible(n), it):
					1. 开辟一片内存，来调用_not_divisible(n):
						2. 传入参数n(3) # 因为这里是直接调用了函数，而并不是简简单单的函数名赋值，所以这个函数空间里面的所有参数(除了内函数lambda里面独有的参数)都已经被计算出来了,所以这里的n已经占据了函数空间的一片区域，并且不会改变(除非内函数里面引入nonlocal这种关键字),我将这片内存空间里面的这个变量称为n_1(这与传入的参数的内存空间是不一样的)
						3. 返回lambda表达式
					2. 将返回的对象，即lambda表达式传递给filter作为判断func # 此时由于，只是将匿名函数当一个变量传递给了filter，而没有去调用它，所以lambda表达式中的参数值n并不会确定下来
					3. 将迭代对象it传递给filter
					4. filter 函数返回一个迭代对象给新的it_1(我这么叫是为了区分之后的it序列), 因为filter已经执行了所以可以肯定filter里面的参数的必然已经确定下来了，即‘调用的判断规则 _not_divisible(3)’和‘参考的原始generator’ 已经确定，但原始的generator还没调用，所以仍然停在3这个位置
				2. 重新开始循环
				3. 执行 next(it_1):
					1. 首先是调用原始的generator 'it':
						1. a += 2
						2. yield a(5)
					2. 判断是否满足判断规则 ‘_not_divisible(3)’:
						1. 传入 it 生成的 5 到匿名函数中
						2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(3)中找到，即n=3
						3. 判断得出:不能整除3，所以返回5
				4. 执行 n = 5
				5. 执行 yield n(5)
				6. 跳出
				
			第四次执行next(pri):
				1.  执行 it_2 = filter(_not_divisible(5), it_1) # 这标注下标也只是为了区分其不同
				2.	重新开始循环	
				3. 执行 next(it_2):
					1. 首先是调用他的上一个的generator 'it_1':
						1. 调用'it_1'的generator 'it':
							1. a += 2
							2. yield a(7)
						2. 判断是否满足判断规则 ‘_not_divisible(3)’:
							1. 传入 it 生成的 7 到匿名函数中
							2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(3)中找到，即n=3
							3. 判断得出:不能整除3，所以返回7
					2. 判断是否满足判断规则 ‘_not_divisible(5)’:
						1. 传入 it 生成的 7 到匿名函数中
						2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(5)中找到，即n=5
						3. 判断得出:不能整除5，所以返回7
				4. 执行 n = 7
				5. 执行 yield n(7)
				6. 跳出


			第五次执行next(pri):
				1. 执行 it_3 = filter(_not_divisible(7), it_2) # 这标注下标也只是为了区分其不同
				2. 重新开始循环	
				3. 执行 next(it_3):
					1. 首先是调用他的上一个的generator 'it_2':
						1. 调用'it_2'的generator 'it_1':
							1. 调用'it_1'的上一个generator 'it':
								1. a += 2
								2. yield a(9)
							2. 判断是否满足判断规则 ‘_not_divisible(3)’:
								1. 传入 it 生成的 7 到匿名函数中
								2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(3)中找到，即n=3
							3. 判断得出:能整除3，所以再一次调用generator'it':
								1. a += 2
								2. yield a(11)
							4. 判断是否满足判断规则 ‘_not_divisible(3)’:
								1. 传入 it 生成的 7 到匿名函数中
								2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(3)中找到，即n=3
							5. 判断得出:不能整除3:
								1. a += 2
								2. yield a(11)
						2. 判断是否满足判断规则 ‘_not_divisible(5)’:
							1. 传入 it 生成的 11 到匿名函数中
							2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(5)中找到，即n=5
							3. 判断得出:不能整除5，所以返回11
					2. 判断是否满足判断规则 ‘_not_divisible(7)’:
						1. 传入 it 生成的 11 到匿名函数中
						2. 执行 lambda x: x % n > 0 # 这里lambda表达式的n会从_not_divisible(7)中找到，即n=7
						3. 判断得出:不能整除7，所以返回11
				4. n = 11
				5. 执行 yield n(11)
				6. 跳出
				
'''

'''
		如果对pri_2进行一波顺寻分析，会发现主要的不同在于,它的判断规则从 ‘_not_divisible(3)’, ‘_not_divisible(5)’, ‘_not_divisible(7)’ 分别变成了‘lambda x: x % n > 0’, ‘lambda x: x % n > 0’, ‘lambda x: x % n > 0’, 因为在每一次执行时,前者判断条件里面的n来源于已经创造的函数空间中的变量n, 即3,5,7。而后者因为并不是返回函数，且本身并没有定义n，所以会自动在外层函数中找n,最终找到了定义在prime_2()中的n值, 故而三个lambda表达式都是使用的一样的n值。
'''
```

### 装饰器

```python
# 装饰器主要用于增强函数的功能，本质上，decorator就是一个返回函数的高阶函数
'''
	下面将举几个例子来帮助理解装饰器的行为及其用法:
		例1: 基本使用
		例2: 带参数的decorator
		例3: 使用decorator的decorator(常用)
		例4: 提前执行func,并以变量作为返回值的装饰器(最常用)
'''

# 例1: 基本使用
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper

@log
def now():
    print('2020-12-2')

>>>	now()
call now():
2020-12-2

# 实际上在执行now()这一步可以拆分为两步:
#				1. now_1 = log(now)
#				2. now_1():
#					1. wrapper():
#						1. print('call %s():' % now.__name__)
#						2. return now()
#					2. now()



# 例2: 带参数的decorator
def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator

@log('excute')
def now():
    print('2020-12-2')

>>> now()
excute now()
2020-12-12

# 执行顺序分析:
# 1. now_1 = log('excute')(now):
#		1. text = 'excute'
#		2. now_1 = decorator(now)
# 2. now_1():
#		1. wrapper():
#			1. print('%s %s():' % ('excute', now.__name__))
#			2. return now()
#		2. now()




# 例3: 使用decorator的decorator(常用)
import functools

def log(text):
    def decorator_1(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator

# 其中@functools.wraps(func)使用这个装饰器是为了将函数在使用了@decorator这个装饰器之后,把 .__name__这一属性保持不变


# 如果不加上@functools.wraps(func)
@log
def now():
    print('2020-12-2')

    
>>> a = now
>>> a.__name__
'decorator_1'


# 加上@functools.wraps(func)这一语句后
@log
def now():
    print('2020-12-2')

>>> a = now    
>>> a.__name__
'now'



# 例4: 提前执行func,并以变量作为返回值的装饰器(最常用)
import time, functools

def metric(fn):
    @functools.wraps(fn)
    def decoretor(*args,**kwargs):
        t0 = time.time()
        back = fn(*args,**kwargs)
        delta_time = time.time() - t0
        print('%s executed in %s ms' % (fn.__name__, delta_time))
        return back
    return decoretor

# 可见返回的是变量back,使用这样的方法可以在执行decorator()的过程中就调用函数,并得到相关信息,而并不需要等到decorator都执行完了最后才调用函数
```

### 偏函数

```python
# 当我们大量使用某一个函数是，我们想要将某些参数固定下来，我们会引入偏函数的概念

# 例1: 手动创建偏函数
def int2(x, base=2)
	return int(x, base)

# 例2: 利用functools.partial()函数创建偏函数
int2 = functools.partial(int, base=2)

# 实际上functools.partial()接收三个参数, partial(func, *args, **keywords), 其中第一个为函数名，后面两个参数将分别作为位置传参和关键字传参传入到func中

# 如:
int2 = functools.partial(int, base=2) = int(base=2)
int2(*args,**kwargs) = int(*args,**kwargs,base=2)

max10 = functools.partial(max, 10)
max10(*args) = max(*args,10)
```

### 模块初步

#### 模块简介

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Michael Liao'

import sys

def test():
    args = sys.argv
    if len(args)==1:
        print('Hello, world!')
    elif len(args)==2:
        print('Hello, %s!' % args[1])
    else:
        print('Too many arguments!')

if __name__=='__main__':
    test()
```

```python
'''
	第1行和第2行是标准注释，第1行注释可以让这个hello.py文件直接在Unix/Linux/Mac上运行，第2行注释表示.py文件本身使用标准UTF-8编码；

	第4行是一个字符串，表示模块的文档注释，任何模块代码的第一个字符串都被视为模块的文档注释；

	第6行使用__author__变量把作者写进去，这样当你公开源代码后别人就可以瞻仰你的大名
	
	以上就是Python模块的标准文件模板，当然也可以全部删掉不写，但是，按标准办事肯定没错。
	
	
	
	后面开始就是真正的代码部分。
	
	第8行import sys导入内建的系统模块
	
	sys模块有一个argv变量，用list存储了命令行的所有参数。argv至少有一个元素，因为第一个参数永远是该.py文件的名称，例如：
	运行python3 hello.py获得的sys.argv就是['hello.py']
	运行python3 hello.py Michael获得的sys.argv就是['hello.py', 'Michael']
	
	最后两行:
		if __name__=='__main__':
   	 		test()
   	 	当我们在命令行运行hello模块文件时，Python解释器把一个特殊变量__name__置为__main__，而如果在其他地方导入该hello模块时，if判断将失败，因此，这种if测试可以让一个模块通过命令行运行时执行一些额外的代码，最常见的就是运行测试:
   	 	情况1: //直接运行hello.py，判定__name__ == __main__, 所以直接执行test()
   	 		$ python3 hello.py
			Hello, world!
			$ python hello.py Michael
			Hello, Michael!
		情况2: //导入hello模块时,虽然最后两行也被导入了,但是不同的是__name__ ！= __main__, 所以不执行test(), 如需执行则需要手动调用test()
			$ python3
			Python 3.4.3 (v3.4.3:9b73f1c3e601, Feb 23 2015, 02:52:03) 
			[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
			Type "help", "copyright", "credits" or "license" for more information.
			>>> import hello
			>>> hello.test()
			Hello, world!				
'''
```



#### 作用域(数据封装)

1. 特殊变量(魔法变量): `__xxx__` : `__author__`,`__name__`,`__doc__`
   	可以被直接引用，但是有特殊用途

2. 私有变量:`_xxx` 或者`__xxx` :
       不应该被直接引用
       一个下划线开头的实例变量名，比如`_name`，这样的实例变量外部是可以访问的，但是，按照约定俗成的规定，当你看到这样的变量时，意思就是，“虽然我可以被访问，但是，请把我视为私有变量，不要随意访问”。

   ​	双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。不能直接访问`__name`是因为Python解释器对外把`__name`变量改成了`_Student__name`，所以，仍然可以通过`_Student__name`来访问`__name`变量：

3. 公开变量: `xxx`

```python
# 常见错误
>>> bart = Student('Bart Simpson', 59)
>>> bart.get_name()
'Bart Simpson'
>>> bart.__name = 'New Name' # 设置__name变量！
>>> bart.__name
'New Name'

# 表面上看，外部代码“成功”地设置了__name变量，但实际上这个__name变量和class内部的__name变量不是一个变量！内部的__name变量已经被Python解释器自动改成了_Student__name，而外部代码给bart新增了一个__name变量。不信试试：

>>> bart.get_name() # get_name()内部返回self.__name
'Bart Simpson'

```

#### 这里有一个值得注意的但不知道放到哪里的实际案例

```python
class F:
    val = [1,2,3]
    val_2 = 3
    def __init__(self):
        pass

    
f1 = F()
f2 = F()

>>> f1.val.append(4) 
>>> f2.val
[1,2,3,4]       # 对f1实例中属性的操作，影响到了f2

>>> f1.val_2 += 1 
>>> f2.val_2	 # 对f1实例中属性的操作，没有影响到f2
3

>>> f3 = F()
>>> f3.val
[1,2,3,4]	#可以说对实例f1的操作，已经影响到了这个类

# 以上现象的本质原因是Python的可变和不可变数据类型所决定的，这是因为在实例化后，类变量是各个实例共享的对象，都指向同一个内存地址，起先f1.val_2和f2.val_2是指向同一个内存地址，f1.val和f2.val是指向同一内存地址，但f1.val_2和f2.val_2指向的是一个数字，而f1.val和f2.val指向的是一个列表，数字是一个不可变对象，列表是一个可变对象，所以在执行f1.val_2 += 2后，f1.val_2新创建了一个指向数字“7”的对象，而f2.val_2还是指向实例化时指向数字“5”的对象；而向列表中增加一个元素并不会创建一个新的对象，所以f1.val和f2.val依然指向同一个内存地址。
# 但这种现象仅限于对于 ‘类中已经定义好的可变类型变量’ 进行更改时会出现，而对于类中未定义, 而是在使用实例时新增加的属性，则不会有这种担心
```



#### 继承和多态

```python
# 和函数在选择参数时，从高楼层往低楼层找，这个原理是类似的。子类的方法和变量也会优先在该类中找，找不到之后才会到父类中找，并一层一层往下
```

##### 1 多继承

###### 1  MRO

```python
# MRO遵循以下规则：
# 	1. 本地优先级： 根据声明顺序从左往右查找
# 	2. 单调性： 所有子类中，也应满足其查找顺序
```

```python
# 生成MRO采用的是C3 算法，而C3算法中重点是一个merge函数，那先来看一个执行merge时步骤：
# 		1. 顺序遍历列表
#		2. 查找首元素满足以下条件，否则遍历下一个序列
#				1. 在其他序列也是首元素
#				2.	或者在其他序列里不存在
#		3. 从所有序列中移除此元素，合并到MRO序列中
#		4. 重复执行，直到所有序列为空或无法执行下去
```

```python
# 实例演示:
#
# 例1:
class B:
    pass
#	mro(B) = [B,O] 
#	[B,O]中的字母O表示的就是object



# 例2:
class B(A):
    pass
# 	mro(B) = [B] + merge(mro(A),[A])
#	mro(B) = [B] + merge([A,O],[A])
#	mro(B) = [B,A] + merge([O])
#	mro(B) = [B,A,O]




# 例3:
class A1:
    pass
class B1:
    pass
class C1(A1,B1):
	pass
# 	mro(C1) = [C1] + merge(mro(A1),mro(B1),[A1,B1])
# 	mro(C1) = [C1] + merge([A1,O],[B1,O],[A1,B1])
# 	mro(C1) = [C1] + merge([O],[B1,O],[B1])
# 	mro(C1) = [C1,A1,B1] + merge([O],[O])
# 	mro(C1) = [C1,A1,B1,O]

class C2(B1,A1):
    pass
# 	mro(C2) = [C2] + merge(mro(B1),mro(A1),[A1,B1])
# 	mro(C2) = [C2] + merge([B1,O],[A1,O],[B1,A1])
# 	mro(C2) = [C2] + merge([O],[A1,O],[A1])
# 	mro(C2) = [C2,B1,A1] + merge([O],[O])
# 	mro(C2) = [C2,B1,A1,O]



# 例4:
class A2:
    pass
class B2(A2):
    pass
class C1(A2,B2):
    pass
# 	mro(C1) = [C1] + merge(mro(A2),mro(B2),[A2,B2])
# 	mro(C1) = [C1] + merge([A2,O],( [B2] + merge(mro(A2),[A2]) ),[A2,B2])
# 	mro(C1) = [C1] + merge([A2,O],( [B2] + merge([A2,O],[A2]) ),[A2,B2])
# 	mro(C1) = [C1] + merge([A2,O],( [B2,A2] + merge([O]) ),[A2,B2])
# 	mro(C1) = [C1] + merge([A2,O],[B2,A2,O],[A2,B2])
# 	mro(C1) = [C1] + merge([A2,O],[B2,A2,O],[A2,B2])
#	mro(C1) = Error

class C2(B2,A2):
    pass
# 	mro(C2) = [C2] + merge(mro(B2),mro(A2),[B2,A2])
# 	mro(C2) = [C2] + merge([B2,A2,O],[A2,O],[B2,A2])
# 	mro(C2) = [C2,B2] + merge([A2,O],[A2,O],[A2])
# 	mro(C2) = [C2,B2,A2] + merge([O],[O])
# 	mro(C2) = [C2,B2,A2,O]

# 总结出大概就是子类要放在前面

# 其实在一个类中有一个__mro__属性，可显示出查找顺序，如下：
>>> C2.__mro__
(__main__.C2, __main__.B2, __main__.A2, object)
```

###### 2 MIXIN - 混入

```python
'''
	MIXIN是一种组合的表现，在python是通过多继承来实现组合。

	试想有这样一个场景，我们有一个文档类，文档分为word文档和excel文档，这些文档可以输出到显示器上，也可以输出到打印机上，我们用MIXIN的方式来实现，如下：
'''
class Document:
    def __init__(self,content):
        self.content = content
  
class Word(Document):
    def format(self):
        self.content = 'i am word,my content is {0}'.format(self.content)
  
class Excel(Document):
    def format(self):
        self.content = 'i am excel,my content is {0}'.format(self.content)

'''
	上边定义了三个类，Document类作为Word和Excel类的父类，两个子类分别实现了各自的format方法。这两种文档能输出到打印机和显示器上，所以接下来定义这两个类，如下：
'''        
        
class Monitor:
    def display(self):
        print('{0} on monitor'.format(self.content))
 
class Printer:
    def display(self):
        print('{0} on printer'.format(self.content))

        
'''
	Monitor和Printer类只继承object类，各自实现了输出功能。如果此时我们想把word文档输出到显示器上、word文档输出到打印机上，或者是想把excel文档输出到显示器、excel文档输出到打印机上，应该怎样实现呢？如下：
'''       
class WordWithMonitor(Monitor,Word):
    pass
 
class ExcelWithMonitor(Monitor,Excel):
    pass
 
class WordWithPrinter(Printer,Word):
    pass
 
class ExcelWithPrinter(Printer,Excel):
    pass

wwm = WordWithMonitor('mix in')
wwm.format()
wwm.display()

wwp = WordWithPrinter('mix in')
wwp.format()
wwp.display()
'''
	ExcelWithMonitor类和ExcelWithPrinter类实例化出来后效果和上边一样，这样通过继承不同的类组合就可以满足不同的要求，上边的Monitor类和Printer类我们叫做MINXIN类，这种类有以下特征：

	1. 此类一般只包含方法，不包含数据

	2. 此类不能单独实例化，比如上边的Monitor类和Printer，类中没有content这个变量，所以不能单独实例化

	3. 此类一般只继承object类，或继承具有MIXIN类特性的类

	在使用MINXIN这种方式时，一般会把MIXIN类写在继承列表的首位，如class WordWithMonitor(Monitor,Word):，这样能避免因其他类的同名方法覆盖MIXIN类的方法，可以通过__mro__属性来看一下类继承后的查找顺序，如下：
'''
>>> WordWithMonitor.__mro__
(__main__.WordWithMonitor,
 __main__.Monitor,
 __main__.Word,
 __main__.Document,
 object)
```





#### 获取对象信息(反射)

详细信息:https://zhaochj.github.io/2016/05/08/2016-05-08-%E5%8F%8D%E5%B0%84/

```python
# 1. 使用type()

# 变量
>>> type(123)
<class 'int'>
>>> type('str')
<class 'str'>
>>> type(None)
<type(None) 'NoneType'>

# 函数 和 自定义类的对象
>>> type(abs)
<class 'builtin_function_or_method'>
>>> type(a)
<class '__main__.Animal'>



# 2. 调用types模块

# check变量是否为函数
>>> import types
>>> def fn():
...     pass
...
>>> type(fn)==types.FunctionType
True
>>> type(abs)==types.BuiltinFunctionType
True
>>> type(lambda x: x)==types.LambdaType
True
>>> type((x for x in range(10)))==types.GeneratorType
True



# 3. 使用isinstance()

# 总是优先使用isinstance()判断类型，可以将指定类型及其子类“一网打尽”。
# 对于一个对象而言，他不仅属于他自己的类，还属于他继承的父类

# 并且还可以判断一个变量是否是某些类型中的一种(传入tuple):
>>> isinstance([1, 2, 3], (list, tuple))
True
>>> isinstance((1, 2, 3), (list, tuple))
True



# 4. 使用dir()

# dir()会返回一个包含对象或者类所有属性和方法字符串的list: (既可以传入类名，也可以传入实例化对象)
>>> dir(object)
['__class__',
 '__delattr__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__lt__',
 '__ne__',
 '__new__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__']

# 实际上 dir() 等价于 'object.__dir__',我们观察上面的结果可以看出对象是有__dir__这个attribute或者说是方法的(这里并不需要细究)

# 因为所有的类都会继承object(他是所有类的父类)，所以所有类都可以调用dir(),查看对象里面的属性和方法

# 类似的还有 str类 下的 'str.__len__()' 等价于 len() 
#					'object.__getatrribute__()' 等价于 getattr()
#					'object.__setattr__()' 等价于 setattr()

# 比较常用的用来查看对象属性或者方法的函数
dir(),getattr(),setattr(),hasattr()
# 使用示例
>>> class MyObject(object):
...     def __init__(self):
...         self.x = 9
...     def power(self):
...         return self.x * self.x
...
>>> obj = MyObject()

>>> hasattr(obj, 'x') # 有属性'x'吗？
True
>>> obj.x
9
>>> hasattr(obj, 'y') # 有属性'y'吗？
False
>>> setattr(obj, 'y', 19) # 设置一个属性'y'
>>> hasattr(obj, 'y') # 有属性'y'吗？
True
>>> getattr(obj, 'y') # 获取属性'y'
19
>>> obj.y # 获取属性'y'
19
# 可以传入一个default参数，如果属性不存在，就返回默认值：
>>> getattr(obj, 'z', 404) # 获取属性'z'，如果不存在，返回默认值404
404

```





#### 类方法

```python
# 类方法可以调用类变量但不能调用实例变量
# 类方法用@classmethod这个装饰器实现，如下：
class H:
    __val = 3

    def __init__(self,x):
        self.x = x

    @classmethod
    def get_val(cls):
        print(cls.__val)
        print(cls.x)
        
        
>>> h = H(7)
>>> H.get_val()
3
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-76-0e8ff847d82b> in <module>()
      1 h = H(7)
----> 2 H.get_val()

<ipython-input-75-c0204fe93832> in get_val(cls)
      8     def get_val(cls):
      9         print(cls.__val)
---> 10         print(cls.x)

AttributeError: type object 'H' has no attribute 'x'

    
>>> h.get_val()
3
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-77-6b7dc73f632b> in <module>()
----> 1 h.get_val()

<ipython-input-75-c0204fe93832> in get_val(cls)
      8     def get_val(cls):
      9         print(cls.__val)
---> 10         print(cls.x)

AttributeError: type object 'H' has no attribute 'x'

# 如上，在执行H.get_val()和h.get_val()后都输出了cls__val这个类私有变量的值，但在访问实例变量时抛出了AttributeError错误，说明类直接调用，如H.get_val()也可以通过实例调用，如h.get_val()，类方法可以访问类私有变量，类方法不可访问实例变量。所有实例在创造是就都共享的叫类变量,每个实例需要单独定义的变量叫实例变量
```

#### 静态方法

```python
# 静态方法既不能调用实例的变量也不能调用类变量
# 静态方法使用@staticmethod这个装饰器来实现，如下：
class I:
    __val = 3
    val = 4

    @staticmethod
    def print_val():
        print(123)
        print(val)
        print(__val)
>>> i = I()
>>> i.print_val()

123
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-78-9345bd892eed> in <module>()
      9         print(__val)
     10 i = I()
---> 11 i.print_val()

<ipython-input-78-9345bd892eed> in print_val()
      6     def print_val():
      7         print(123)
----> 8         print(val)
      9         print(__val)
     10 i = I()

NameError: name 'val' is not defined

```

#### 魔法方法

```python
'''
	1. 对象的创建与销毁:
			__new__ 创建对象
			__init__ 初始化对象
			__del__ 当销毁对象时调用
	2. 可视化对象:
			__repr__ 对应repr(object)这个函数，返回一个可以用来表示对象的可打印字符串
			__str__ 对应str(object)这个函数，返回一个字符串对象，适合用于print输出
			__bytes__ 对应bytes(object)这个函数，返回bytes对象
	3. 比较运算符重载
			__lt__ 小于
			__le__ 小于等于
			__eq__ 等于
			__ne__ 不等于
			__gt__ 大于
			__ge__ 大于等于
	4. bool() 和 len()函数
	5. hash() 与 可hash对象
	6. 可调用对象 和 类装饰器
	7. 类装饰器
	8. 单例(基于__call__)
'''
```

##### 对象的创建与销毁

```python
'''
	1. 对象的创建与销毁:
			__new__ 创建对象
			__init__ 初始化对象
			__del__ 当销毁对象时调用	
'''

class A:
    def __new__(cls):
        print('call __new__')
        return object.__new__(cls)
    
    def __init__(self):
        print('call __init__')
        
    def mothod(self):
        print('call mothod')
        
    def __del__(self):
        print('call __del__')
        

>>> a = A()
call __new__
call __init__
>>> a.mothod()
call mothod
>>> del a
call __del__
```

##### 可视化对象

```python
'''
	2. 可视化对象:
			__repr__ 对应repr(object)这个函数，返回一个可以用来表示对象的可打印字符串
			__str__ 对应str(object)这个函数，返回一个字符串对象，适合用于print输出
			__bytes__ 对应bytes(object)这个函数，返回bytes对象
'''
class B:
    def __init__(self,name):
        self.name = name
        
    def __repr__(self):
        return 'call __repr__ name is {0}'.format(self.name)
    
    def __str__(self):
        return 'call __str__ name is {0}'.format(self.name)
    
    def __bytes__(self):
        return 'call __bytes__ name is {0}'.format(self.name).encode('utf-8')

    
 b = B('zhaochj')
>>> b   
call __repr__ name is zhaochj
>>> print(b)
call __str__ name is zhaochj
>>> bytes(b)
b'call __bytes__ name is zhaochj'
```

##### 比较运算符重载

```python
'''
	3. 比较运算符重载
			__lt__ 小于
			__le__ 小于等于
			__eq__ 等于
			__ne__ 不等于
			__gt__ 大于
			__ge__ 大于等于
'''
'''
			类创建的对象里的‘属性’是可以通过运算符进行比较的
			但类本身是不能用运算符进行比较或者计算的
'''
class Person_1:
    def __init__(self,age):
        self.age = age
        
    def __lt__(self,other):
        print('call __lt__')
        return self.age < other.age
    
    def __le__(self,other):
        print('call __le__')
        return self.age <= other.age
    
    def __eq__(self,other):
        print('call __eq__')
        return self.age == other.age
    
    def __ne__(self,other):
        print('call __ne__')
        return self.age != other.age
    
    def __gt__(self,other):
        print('call __gt__')
        return self.age > other.age
    
    def __ge__(self,other):
        print('call __ge__')
        return self.age >= other.age

    
>>> p3 = Person_1('30')
>>> p4 = Person_1('20')
>>> p3 > p4
call __gt__
True
>>> P3 == P4
call __eq__
False
```

##### `bool()` 和 `len()` 函数

```python
'''
	4. bool() 和 len() 函数:
			__bool__ 决定bool()函数的执行
			__len__  决定len()函数的执行
			注:如果未标注__bool__方法,则会采用object中的__bool__,并调用__len__，根据返回值决定True or False
'''

# 观察bool函数的用法
list1 = []
str1 = ''
>>> bool(list1)
False
>>> bool(str1)
False

# 观察例1:
class Grok:
    def __init__(self,val):
        self.val = val
        
    def __bool__(self):
        print('call __bool__')
        return not self.val

>>> g = Grok('')
>>> bool(g)
call __bool__
True
>>> g = Grok('1')
>>> bool(g)
call __bool__
False

# 观察例2:
class Seq:
    def __init__(self,*args):
        self.val = args
        
    def __len__(self):
        print('call __len__')
        return len(self.val)

>>> s1 = Seq(1,2,3)
>>> s2 = Seq()
>>> len(s1)
call __len__
3
>>> len(s2)
call __len__
0
>>> bool(s1)
call __len__
True
>>> bool(s2)
call __len__
False

'''
	由上面两例可知, 
		1. bool函数主要是通过__bool__这个魔法方法来进行返回的,而len函数则是通过__len__这个魔法方法
		2. 我们还可知,当类内部未定义__bool__时,则自动采用object中的__bool__方法,此时会调用__len__这个魔法方法,并根据__len__方法的返回值来决定bool的返回值
'''

# 例3: (定义__bool__后，调用bool()观察是否还会调用__len__)
class Seq_1:
    def __init__(self,*args):
        self.val = args
        
    def __len__(self):
        print('call __len__')
        return len(self.val)
    
    def __bool__(self):
        print('call __bool__')
        return True

>>> s3 = Seq_1()
>>> bool(s3)
call __bool__
True

# 显然，符合逻辑，他并不会调用object中的__bool__方法，自然也不会调用__len__方法咯
```

##### hash()与可hash对象

```python
'''
	5.hash()与可hash对象:
			__hash__ 控制了
'''

class Hash:
    def __init__(self,val):
        self.val = val
        
    def __hash__(self):
        return 123
    
    
>>> h1 = Hash('zhaochj')
>>> hash(h1)
123

'''
	如果不再类中定义__hash__ 在执行hash()时则会自动调用object类中的__hash__
'''
class Hash_1:
    def __init__(self,val):
        self.val = val
 


>>> h1 = Hash('zhaochj')
>>> hash(h1)
123
```

##### 可调用对象

```python
'''
	6. 可调用对象:
			__call__ 决定根据类实例化的对象是否可以被调用,以及返回值
'''

# 在python中可以用callable函数查看一个对象是不是可调用，如下：
def fn():
    print('ha ha ha')
    
>>> callable(fn)
True

# 那一个实例化的对象呢?
class Fun:
    def __init__(self,name):
        self.name = name
        
>>> f = Fun('zhaochj')
>>> callable(f)
False
# 显然该对象是不可调用的


# 如何创造出一种可以调用的实例化对象呢?
class Fun_1:
    def __init__(self,name):
        self.name = name
        
    def __call__(self):
        print('my name is {0}'.format(self.name))

>>> f = Fun('zhaochj')
>>> callable(f)
True
>>> f()
my name is zhaochj

# 事实上,完全可以通过 __call__魔法方法 把f()看作真正的函数,可以接收参数,也可以返回值
```

##### 类装饰器(基于`__call__`)

```python
'''
	7. 类装饰器(基于可调用对象):
			__call__ 决定根据类实例化的对象是否可以被调用,以及返回值
			@ 修饰器符号:
					@class()
					def a():
						pass
					
					a() 等同于一下几步
						1. b = class()
						2. a = b(a)
						2. a() = class()(a)() 
'''
# 注意:在上例中 @class() 中的()一定不能省掉了,因为其本质还是利用了,可以接受函数作为参数的‘可调用对象’作为装饰器,即由类实例化的对象b

import functools
class InjectUser:
    def __init__(self,default_user):
        self.user = default_user
        
    def __call__(self,fn):
        @functools.wraps(fn)
        def wrap(*args,**kwargs):
            if 'user' not in kwargs.keys():
                kwargs['user'] = self.user
            return fn(*args,**kwargs)
        return wrap
        
@InjectUser('zhaochj')
def do_somthings(*args,**kwargs):
    print(kwargs.get('user'))
    
>>> do_somthings()
zhaochj
>>> do_somthings(user='就这水平')
就这水平

# 这完全等价于还没有加@装饰器时的一下语句
>>> InjectUser('zhaochj')(do_somthings(user='就这水平'))
就这水平
```

##### 单例(基于`__call__`)

```python
'''
	8. 利用__call__实现单例:
			__call__
'''

'''
	所谓单例，是指一个类的实例从始至终只能被创建一次。单例的实现有多种，这里以__call__方法来实现。
		即使之后再出现去用类创建实例,其本质也是第一个创建的实例对象
'''

class Single:
    __instance = None
    
    def __init__(self,cls):
        self.cls = cls
        
    def __call__(self,*args,**kwargs):
        if self.__instance is None:
            self.__instance = self.cls(*args,**kwargs)
        return self.__instance

@Single
class Grok1:
    pass

>>> grok1 = Grok1()
>>> id(grok1)
>>> grok2 = Grok1()
>>> id(grok2)


'''
	我们来仔细分析一下程序顺序:
			1. 执行 grok1 = Grok1() 语句:
					1. Grok1被修饰器Single修饰:
						Grok1' = Single(Grok1):
						1. 将Single类实例化为一个的对象(我们将其称之为A),self就是对象A
						2. cls 接收传入的参数，即Grok1这个类
						3. 使Grok1这个对象的‘cls’属性 指向 Grok1这个类
						4. 将 Grok1'(为了区分它与之Grok1类) 指向实例化的Single类对象
					2. Grok1():
						1. 因为Grok1'本质上已经是实例化的Single类对象,所以在调用Grok1'时本质上是在调用Signal类里面定义好的__call__()方法
						2. 执行__call__(): (因为Grok1'()没有参数,所以__call__也没有参数)
								1. 判断是否创建过实例,显示没有进入if执行语句:
										1. Grok1'.__instance = Grok1'.cls() = Grok1()
										2. 即,将Grok1()类实例化出一个对象Grok1'.__instance
								2. 将Grok1'.__instance,即一个Grok1类的实例化对象的返回
					3. 将grok1 指向这个返回的Grok1类的实例化对象
					
			2. 执行 grok2 = Grok1() 语句:
					1. 因为Grok1已经经过了执行grok1 = Grok1()时,被修饰器Single修饰的那一步，(修饰过程只有执行了一次就不会再执行了)，所以本质上Grok1还是上次创造出来的Grok1',即一个实例化的Single类对象而已。此时直接进入第2步
					2. Grok1():
						在这里,分析基本与第一次执行时一直,但是不同点就在于，此时Grok1'.__instance不为空而是指向一个Grok1类的实例化对象,可以这么说,其实就是grok1了,所以他不会再执行if语句里面的实例化过程了,而是直接返回这个实例化对象,即之前已经创建的grok1
					3. 将grok2 指向这个返回的Grok1类的实例化对象, 即grok1
'''			
```

#####  `with`语句

```python
'''
		9. with 语句与__enter__,__exit__方法
'''


'''
	有一些任务，可能事先需要设置，事后做清理工作。对于这种场景，Python的with语句提供了一种非常方便的处理方式。一个很好的例子是文件处理，你需要获取一个文件句柄，从文件中读取数据，然后关闭文件句柄。
	如果不使用with语句，代码是这样的：
'''
file = open("/tmp/foo.txt")
data = file.read()
file.close()

'这里有两个问题。一是可能忘记关闭文件句柄；二是文件读取数据发生异常，没有进行任何处理。下面是处理异常的加强版本：'
file = open("/tmp/foo.txt")
try:
    data = file.read()
finally:
    file.close()


'虽然这段代码运行良好，但是太冗长了。这时候就是with一展身手的时候了。除了有更优雅的语法，with还可以很好的处理上下文环境产生的异常。下面是with版本的代码：'
with open("/tmp/foo.txt") as file:
    data = file.read()

# 那with语法是怎么实现的呢？下边来看一个类：    
class Resource:
    def __init__(self):
        print("call __init__")
        
    def __enter__(self):
        print("call __enter__")
        print("self object at {0}".format(self))
        return self
    
    def __exit__(self,*args,**kwargs):
        print("call __exit__")
        
        
# 创造个实例并运行试试?
>>> with Resource() as res:
...     print("res object at {0}".format(res))
call __init__
call __enter__
self object at <__main__.Resource object at 0x7f5db448a6a0>
res object at <__main__.Resource object at 0x7f5db448a6a0>
call __exit__

# 这上边这个例子可知，只要一个类实现了__enter__和__exit__方法，那这个类就可以使用with语句。


# with语句的调用流程大致如下：
1. python解释器执行到with Resource() as res:语句时，其实是首先实例化了Resource类给对象res，接着执行了__enter__函数,打印了前三行
2. 执行print("res object at {0}".format(res))语句，这里的res是指向Resource类实例化对象，所以与self指向的对象相同，打印第四行
3. 再执行__exit__函数
```





#### 描述器

```python
'''
	一个类实现了__get__、__set__、__delete__三个方法，这个类就叫描述器
	以我现在的感觉来看,装饰器增强函数功能而存在的:(传入的参数是类或者函数)
		1. 普通装饰器,函数C接收的是函数A,返回的是函数B,通过函数B增强函数A的功能
		2. 类装饰器,类C接收的是函数A,返回的是可调用对象B,通过类的属性和方法来增强A的功能
				或者接受的是类A,返回的是可调用对象B,B可以实现实例化的功能,例如:单例
	而描述器则是为了限制类的属性而存在的:(传入的参数是属性名)
		1. 描述其,类C接受的是变量名字,返回对象,通过__get__、__set__、__delete__三个方法使得这个看起来这个对象表现和属性变量无异
	直接来看一个描述器的实现，如下：
'''

class Number:
    def __init__(self,name):
        self.name = name
        
    def __get__(self,instance,cls):
        print('call __get__')
        return instance.__dict__[self.name]
    
    def __set__(self,instance,value):
        print('call __set__')
        if isinstance(value,(int,float)):
            instance.__dict__[self.name] = value
        else:
            raise TypeError('execepted int or float')
            
    def __delete__(self,instance):
        del instance.__dic
        
        
class Point:
    x = Number('x')
    y = Number('y')
    
    def __init__(self,x,y):
        self.x = x
        self.y = y
'''
	这样就定义了一个描述器Number类，这个类的作用是描述实例化Point类时x和y变量的类型必须为整型或浮点型，如果不满足这两种类型中的一个，那抛出TypeError的异常。为了验证代码的调用关系，有意在Number类中加了一些print语句，在实例代码中应该把这语句去除。现在来实际实例化Point类试试：
'''

# 给类里面的对象赋值
>>> p1 = Point(2,8)
call __set__
call __set__

# 当执行p1 = Point(2,8)时发生了什么呢？
# 1.当python解释器解析到
class Point:
    x = Number('x')
    y = Number('y')
    
    def __init__(self,x,y):
        self.x = x
        self.y = y
# 代码块时，解释器会创建一个Point类对象，此对象中有x类变量，且此变量指向Number类的一个实例，有y类变量，且此变量指向Number类的另一个实例；解释器还会创建一个__init__函数，此函数接收两个参数。


# 2.当解释器执行到p1 = Point(2,8)时，Point类中的__init__构建函数被执行，执行以下两代码
self.x = x
self.y = y
# 解释器先执行self.x = x代码，这里的self.x是一个变量对象，等号后边的x是指向类变量x = Number('x')中的Number类实例，这时解释器会执行Number类中的__set__函数，把p1实例传递给instance这个形参，把2传递给value这个形参，执行此函数体的代码
def __set__(self,instance,value):
        print('call __set__')
        if isinstance(value,(int,float)):
            instance.__dict__[self.name] = value
        else:
            raise TypeError('execepted int or float')
# 首先打印出call __set__，再执行if语句，为True时把p1实例中__dict__这个特殊方法中key为x的值指向2；如果if语句的判断结果为False，那抛出异常。

# 接着解释器往下执行代码，开始执行构建函数中的self.y = y语句，这个过程与执行self.x = x语句一样。这样就完成了p1 = Point(2,8)这个语句的执行，其实质就是会去执行Number类的__set__函数
>>> P1.x
call __get__
2


# 当执行上边的p1.x时发生了什么？
# 执行p1.x是去调用Point类的实例变量x，从上边的分析可知，这个实例变量是指向Number('x')这个实例，这时解释器会执行Number类的__get__方法，会把p1这个实例名作为变量传递给instance这个形参，把p1的类名作为变量传递给cls，代码如下：
def __get__(self,instance,cls):
        print('call __get__')
        return instance.__dict__[self.name]
# 先打印出call __get__，然后取出p1实例中__dict__中key为x的值返回，这样就得到执行p1 = Point(2,8)语句时2这个数字。
# 总结起来，访问一个使用了描述器的类的实例属性时，其实质是访问了描述器的__get__函数。
# 其实访问p1.x和访问Point.x.__get__(p1,Point)的过程是一样的。


>>> P1.x = 10
call __set__

这和实例化Point类时,初始化赋值给x,的过程是一样的
```

代码改进(可以控制判断传入不同的类型)

```python
class TypeCheck:
    def __init__(self,name,expected_type):
        self.name = name
        self.expected_type = expected_type
        
    def __get__(self,instance,cls):
        if instance is not None:
            return instance.__dict__[self.name]
        return self
    
    def __set__(self,instance,value):
        if not isinstance(value,self.expected_type):
            raise TypeError('expected type {0}'.format(self.expected_type))
        instance.__dict__[self.name] = value
        
    def __delete__(self,instance):
        del instance.__dict__[self.name]

        
class Point:
    x = Number('x',int)
    y = Number('y',str)
    
    def __init__(self,x,y):
        self.x = x
        self.y = y       
```

#### 补充

##### super()方法

```python
# super 的一个最常见用法可以说是在子类中调用父类的初始化方法了。
class Animal(object):
    def __init__(self, name):
        self.name = name

    def greet(self):
        print('Hello, I am %s.' % self.name)


class Dog(Animal):
    def greet(self):
        super(Dog, self).greet()  #调用父类Animal的greet方法
        print('WangWang...')


d=Dog("xiaohuang")

d.greet()
```

运行结果如下:

```
Hello, I am xiaohuang.
WangWang...
```



### 面向对象高级编程

#### 动态绑定属性

```python
class Student(object):
    pass

s1 = Student()
s2 = Student()


# 给实例化的对象进行属性绑定:
s1.name = 'Michael'
print(s1.name)
'Michael'
# 但是其他实例化的对象并不会改变:
print(s2.name)
Error


# 若想要全部对象都可以使用该属性,则需要对类进行动态的属性绑定
Student.name = 'Michael'
'''
	这样所有的对象的name属性就都是Michael了，值得注意的是这与变量的查询机制有关，首先是对象里面是否定义了，如果没有则查询到本类，再是父类，超父类
'''
# 另外方法也可以看做是一种属性


```



####  对动态绑定属性的限制

#####  `__slots__`

```python
'''
	但是实际情况下,我们并不希望用户去随意的绑定属性，所以Python引入了__slots__属性对这一行为进行限制
'''


class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
    
    
>>> s = Student() # 创建新的实例
>>> s.name = 'Michael' # 绑定属性'name'
>>> s.age = 25 # 绑定属性'age'
>>> s.score = 99 # 绑定属性'score'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute 'score'
    
    
# 注意:__slots__定义的属性仅对当前类实例起作用，对继承的子类是不起作用的:
# 所以如果需要限制绑定属性,则在定义子类的时候也要引入__slots__,此时子类中的允许绑定的属性就是自身的__slots__加上父类的__slots__
# 如果只是单纯的想继承父类定义的__slots__,则只需要在定义子类时加上一行 __slots__ = ()即可
```

##### @property的实现与作用

```python
# 我们直接来看property源码吧
class Property(object):
    "Emulate PyProperty_Type() in Objects/descrobject.c"
    def __init__(self, fget=None, fset=None, fdel=None, doc=None):
        self.fget = fget
        self.fset = fset
        self.fdel = fdel
        self.__doc__ = doc

    def __get__(self, obj, objtype=None):
        if obj is None:
            return self
        if self.fget is None:
            raise AttributeError, "unreadable attribute"
        return self.fget(obj)

    def __set__(self, obj, value):
        if self.fset is None:
            raise AttributeError, "can't set attribute"
        self.fset(obj, value)

    def __delete__(self, obj):
        if self.fdel is None:
            raise AttributeError, "can't delete attribute"
        self.fdel(obj)

    def getter(self, fget):
        return type(self)(fget, self.fset, self.fdel, self.__doc__)

    def setter(self, fset):
        return type(self)(self.fget, fset, self.fdel, self.__doc__)

    def deleter(self, fdel):
        return type(self)(self.fget, self.fset, fdel, self.__doc__)

    
# 可以看出Property就是一个‘描述器’,其作用是让返回的对象表现的像是他传递进来之前的样子,可以直接赋值,可以直接调用,还可以删除,除此之外,他还可以接收函数作为参数,并增强函数的功能,显然他也是一个‘装饰器’

# 我们来看一个使用 @property 的实例:
class Spam(object):
    def __init__(self,val):
        self.__val = val

    @Property
    def val(self):
        return self.__val
    
    @val.setter
    def set_val(self,value):
        self.__val = value


# 1. 首先我们实例化这个Student,分析一下执行过程
>>> s1 = Student()

'''
	执行过程分析:
		1. 执行了__init__语句，将传入的参数的值传递给了实例变量self.__val,且该变量不可以直接通过s1.__val访问
		2. val被装饰器Property给装饰了,具体过程就不分析了,总之是返回了一个名为val的Property类对象,并将val取代之。这一步骤的主要意义在意将'self.val'与'val(self)'等价起来
		3. set_val被装饰器val.setter给装饰了,将val这个property对象的fset方法设置为Spam类中的set_val方法,因为__set__方法的存在,使得可以直接对val进行赋值,这个值将作为返回的执行函数参数的value值, self.fset(obj, value), 等价于 set_val(self,value)。这一步最关键的意义在于让'self.val=value'与set_val(self,value)等价起来
		4. 将实例化好的对象传递给s1
		此时 s1.val 等价于 Property.__get__.(self, s1) 等价于 s1.val(self) 等价于 self.__val
			s1.val = 10 等价于 Property.__set_.(self, s1, 10) 等价于 s1.set_val(self, 10) 等价于 self.__val = 10
'''

'''
	为何要大费周章搞这些?直接把__val设置为公有属性不就好了吗,何必这么麻烦?
		1.在val方法中动手脚可以很轻松的将传入的值联系上其他与之相关的变量,即一个属性变动后,其他与之相关的属性可以通过表达式进行修改,从而达到自动化更新所有属性的效果
		2.通过对是否调用@val.setter可以控制是否可以直接用赋值符号进行修改,即控制变量是'只读'还是'可读写'
		3.通过在val方法中的操作可以对传入的值进行简单的检查,从而判断是否需要传递给属性,还是说输入的参数有问题
		4.Property别人都跟你写好了,直接当装饰器和描述器用不就好了吗,何必去纠结麻不麻烦?比你自己实现这些功能麻烦?Property的主要作用感觉就是
				1. 允许直接调用对象,使得这个对象的调用会执行某一个特定函数
				2. 重载了'='为一个函数,左边为对象,右边为函数的参数
				3. 允许直接用del(我们一般不会设置这个)
'''
```

### IO编程

#### 文件读写

```python
# 读文件
# 要以读文件的模式打开一个文件对象，使用Python内置的open()函数，传入文件名和标示符：
>>> f = open('/Users/michael/test.txt', 'r')

# 如果文件打开成功，接下来，调用read()方法可以一次读取文件的全部内容，Python把内容读到内存，用一个str对象表示：
>>> f.read()
'Hello, world!'

# 最后一步是调用close()方法关闭文件。文件使用完毕后必须关闭，因为文件对象会占用操作系统的资源，并且操作系统同一时间能打开的文件数量也是有限的:
>>> f.close()

# 由于文件读写时都有可能产生IOError，一旦出错，后面的f.close()就不会调用。所以，为了保证无论是否出错都能正确地关闭文件，我们可以使用try ... finally来实现:
>>> try:
...    	f = open('/path/to/file', 'r')
...   	print(f.read())
...	finally:
...     if f:
...        	f.close()


# 但是每次都这么写实在太繁琐，所以，Python引入了with语句来自动帮我们调用close()方法:
with open('/path/to/file', 'r') as f:
    print(f.read())
 这和前面的try ... finally是一样的，但是代码更佳简洁，并且不必调用f.close()方法。

# 调用read()会一次性读取文件的全部内容，如果文件有10G，内存就爆了，所以，要保险起见，可以反复调用read(size)方法，每次最多读取size个字节的内容。另外，调用readline()可以每次读取一行内容，调用readlines()一次读取所有内容并按行返回list。因此，要根据需要决定怎么调用。

# 如果文件很小，read()一次性读取最方便；如果不能确定文件大小，反复调用read(size)比较保险；如果是配置文件，调用readlines()最方便
for line in f.readlines():
    print(line.strip()) # 把末尾的'\n'删掉
    
    
# file-like Object
# 像open()函数返回的这种有个read()方法的对象，在Python中统称为file-like Object。除了file外，还可以是内存的字节流，网络流，自定义流等等。file-like Object不要求从特定类继承，只要写个read()方法就行。
# StringIO就是在内存中创建的file-like Object，常用作临时缓冲。

```

