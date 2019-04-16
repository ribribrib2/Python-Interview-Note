# 第一章: 课程导读
## 标准库
- collections 
- re 
- random 
- struct 
- heapq 
- itertools 
- functools 
- OS.stat 
- tempfile 
- pickle 
- json 
- CSV 
- xml 
- tarfile 
- sys 
- threading 
- queue 
- inspect 
- httpserver 
- mmap 
- logging 
- concurrent.futures 
- multiprocessing

# 第二章：数据结构相关话题
## 如何在列表，字典集合中根据条件筛选数据?
![](http://qiniu.rearib.top/FtRmA2RS8l1OXPdmPDeW6o_etWDD)

![](http://qiniu.rearib.top/FvOSb5U_SxJuzMq6JLYw459UWDLn)

- 生成一个随机字符串
```
import random

l = [random.randint(-10, 10) for _ in range(10)]
ll = [x for x in l if x >= 0]
lll = filter(lambda x : x >= 0, l)  # python3返回一个生成器

d = {'student{}:'.format(i): random.randint(0, 100) for i in range(50)}
>>> d.items()
>>> dict_items([('student0:', 4), ('student1:', 13), ('student2:', 88), ('student3:', 28), ('student4:', 79))

print(dict(filter(lambda item: item[1] >= 90, d.items())))
```

## 如何为元组中的每个元素命名，提高程序可读性？
![](http://qiniu.rearib.top/FpC3se5_OnVJRuEovEMSs52AvQm8)

![](http://qiniu.rearib.top/FoBzHX3O6Pb70H5MqYxH0ec5V0oq)

- 方案1：定义一系列数值常量或枚举类型

![](http://qiniu.rearib.top/FuQMjUftryWfro9E_2HbI21hyTfk)

![](http://qiniu.rearib.top/FsoHU2CKwVkWq_VjdefiPXxJFnmq)

- 方案2：使用标准库中collections.namedtuple替代内置tuple

![](http://qiniu.rearib.top/FuPeF0ks5pBwwUdcNnc3pRkua9vW)

## 如何根据字典中值的大小，对字典中的项排序?
![](http://qiniu.rearib.top/FmSzJrXzN4ZBHuq1rrNMEgGjrkzR)

将字典中的各项转换为元组，使用内置函数sorted排序。

![](http://qiniu.rearib.top/FsUSwipbGsvOPCPkxMb2PfK_XfrO)

- 方案1：将字典中的项转化为（值，键）元组。（列表解析或 zip ）

列表解析
```
import random

d = {k : random.randint(0,100) for k in 'asdfjh'}
print(d)
t = list((v,k) for k,v in d.items())
print(sorted(t))

{'a': 82, 's': 70, 'd': 96, 'f': 21, 'j': 37, 'h': 59}
[(21, 'f'), (37, 'j'), (59, 'h'), (70, 's'), (82, 'a'), (96, 'd')]
```

使用zip:
![](http://qiniu.rearib.top/Fj4aE1choHPsj9DBjoZzRvYUjVe8)

- 方案2：传递sorted函数的key参数

```
d = {'a': 82, 's': 70, 'd': 96, 'f': 21, 'j': 37, 'h': 59}
print(d)
print(sorted(d.items(),key=lambda item:item[1], reverse=True))
```

![](http://qiniu.rearib.top/Fs1gdvbp3rvozZ7vwwqF1IbuXrdL)

![](http://qiniu.rearib.top/Fr1hTDNePoqg_QqanrseyrfOVhTt)


## 如何统计序列中元素的频度？
1.某随机序列[12，5，6，4，6，5，5，7]中，找到出现次数最高的3个元素，它们出现次数是多少？
- 方案1：将序列转换为字典{元素：频度}，根据字典中的值排序。

![](http://qiniu.rearib.top/FtR3ntJ0zDNE-PhEVJ3GE_WvHs5M)

如果字典很大,使用排序很浪费, 可以使用堆

![](http://qiniu.rearib.top/FlPLi9sKYSw1sy2KZHyEe51D8G-K)

- 方案2：使用标准库collections中的Counter对象。

![](http://qiniu.rearib.top/FiWfBZz7Ngh72zhqJ10c_C4l6I7l)

2.对某英文文章的单词，进行词频统计，找到出现次数最高的10个单词，它们出现次数是多少？

```
from collections import Counter
import re

f = open('1.txt','r',encoding='utf-8')
data = f.read()
print(data)
f.close()
d = re.split('\W+',data)
print(d)
c = Counter(d)
print(c.most_common(10))
```

## 如何快速找到多个字典的公共键（key）？
![](http://qiniu.rearib.top/Fh3XJ5PGXYL6bXHEXNpiQU9mIbYn)

- 解析判断

`random.simple`从序列或者集合中随机抽取K个不重复的元素形成新的序列，是属于不重复随机抽样

![](http://qiniu.rearib.top/Fgr9-xXpwPQjfmJClpOzaW_Vq2Tl)

![](http://qiniu.rearib.top/FtdIFOy52KXLS5kxSBJ3vdQYRS6Y)

- 集合的方式
![](http://qiniu.rearib.top/Fr3ORJAddotbppPRNrXPB_jEWKNn)

reduce函数:
```
from functools import reduce
print(reduce(lambda a,b: a+b, range(0,10)))
# a = a + b

>>> 45
```

![](http://qiniu.rearib.top/Fr2O8Dji_LlGAarOvu8CtBVrpPOR)

![](http://qiniu.rearib.top/FsJr_y2nAIypiIcjdv2DS9K48M-4)


## 如何让字典保持有序？
![](http://qiniu.rearib.top/FkisUkjIHFEUIYFBO7BMp7fgASUp)

- 使用标准库collections中的OrderedDict

1. 以OrderedDict替代内置字典Dict，依次将选手成绩存入OrderedDict。
2. shuffle 打乱顺序

![](http://qiniu.rearib.top/FpW28Kod_oxVTOnhIujxB2vWliLr)

3. 但是还是无法实现通过输入次序输出名字,对于可迭代对象无法切片或者索引,可以使用islice

![](http://qiniu.rearib.top/FkQJZbI69KFqUB3Hz9RzagXDF90O)

![](http://qiniu.rearib.top/Fi7XbZGQtpYNgA0Nl9sqvLezejrp)

这里的有序是指字典的保存按照插入的顺序, 使用islice切片是按插入顺序返回key,上面的实验在python3.5中实现, python3.6中的dict已经是一个有序字典

## 如何实现用户的历史记录功能（最多n条）？
![](http://qiniu.rearib.top/Fgh1BBwtm8GdTnHCFTxV90M1VMQR)

- 使用容量为n的队列存储历史记录

1. 使用标准库collections中的deque，它是一个双端循环队列。

![](http://qiniu.rearib.top/FlyUu9Xhcz4ElP2bhsVdeW5q9nzw)

2. 使用pickle模块将历史记录存储到硬盘，以便下次启动使用

![](http://qiniu.rearib.top/Flylcllxfo3eDzvvJ5gvtJFTXIbN)


# 第三章：迭代器与生成器相关话题
## 如何实现可迭代对象和迭代器对象?
![](http://qiniu.rearib.top/Fvw8pa-P-GjnY-nukc1T1UPiEdaA)

for循环拿到一个可迭代对象,会通过iter(l)返回一个迭代器, 然后不断调用next, 并最终处理StopIteration错误.

![](http://qiniu.rearib.top/FlPw_pmR2_lPv9AUTzpTUoSSR0i5)

源码
```
class Iterable(metaclass=ABCMeta):
    __slots__ = ()

    @abstractmethod
    def __iter__(self):
        while False:
            yield None
    @classmethod
    def __subclasshook__(cls, C):
        if cls is Iterable:
            return _check_methods(C, "__iter__")
        return NotImplemented

class Iterator(Iterable):
    __slots__ = ()

    @abstractmethod
    def __next__(self):
        'Return the next item from the iterator. When exhausted, raise StopIteration'
        raise StopIteration
    def __iter__(self):
        return self
    @classmethod
    def __subclasshook__(cls, C):
        if cls is Iterator:
            return _check_methods(C, '__iter__', '__next__')
        return NotImplemented
```

![](http://qiniu.rearib.top/FkuyLUK_v10HXo9u2W0eE1eIIHpe)

![](http://qiniu.rearib.top/FlFbzMxkq-UQ_oZKWpD7UyE04bWy)

首先输入城市生成可迭代对象, 开始for循环之前会调用可迭代对象的__iter__会返回一个迭代器, 对于迭代器调用__next__就会去获取天气.如果直接创建迭代器那么用完就没了, 如果创建可迭代对象那么会重新生成一个迭代器.

## 如何使用生成器函数实现可迭代对象?
![](http://qiniu.rearib.top/Fo3qaddVNIRV_o5FMCdcbeZepZBx)

- 将该类的\_\_iter\_\_方法实现成生成器函数,每次yield返回一个素数,

之前的循环是自己去维护的, 使用index, 如果自动维护则需要使用生成器

![](http://qiniu.rearib.top/FlqewA4o_c1BbjFzT8X-Z-Fh4VF_)

## 如何进行反向迭代以及如何实现反向迭代?
![](http://qiniu.rearib.top/FtBFGzBrjws40CJT6_b96Fonky5g)

![](http://qiniu.rearib.top/FtrqQXdI7W-ZWX0FDbo-B-5BM9cZ)

- 实现反向迭代协议的\_\_reversed\_\_ 方法,它返回一个反向迭代器,

![](http://qiniu.rearib.top/Fs_J8QJQFbDa09HcyPcsCGvFWIUS)

![](http://qiniu.rearib.top/Fq9WpOBIR0voLFkZWp3MjtW1dQO5)

我们用十进制描述浮点数,计算机使用二进制描述浮点数,所以有误差.

![](http://qiniu.rearib.top/Fn3HmYN_LUzJFg0Wm5AyatyPtrvQ)

![](http://qiniu.rearib.top/FjhChHs8QxdkF0mrQtW-gKEswatr)

## 如何对可迭代对象做切片操作?
![](http://qiniu.rearib.top/FnZJTLqKi1ie-8BqJktMgOnqfksL)

![](http://qiniu.rearib.top/Ft8ci8gvfIPsC2b8G67cQc5BBhe9)

- 使用itertools.islice,它能返回一个迭代对象切片的生成器.

![](http://qiniu.rearib.top/FmF3EmyQ4KwHfD_Q259ByE-wx1Yx)

## 如何在一个for语句中迭代多个可迭代对象?
![](http://qiniu.rearib.top/FpFyObXWznV9q5hnGTefT1Atuizx)

- 并行:使用内置函数zip,它能将多个可迭代对象合并,每次迭代返回一个元组.

![](http://qiniu.rearib.top/FjhzGUDnxBb11oRsjOijZjvzhuwo)

![](http://qiniu.rearib.top/Fueu1ALeG1Ve_oIKmTWjJwD4Vtqh)

![](http://qiniu.rearib.top/Fo7js3C-_vdU10uaDmm5zrflzPse)

- 串行:使用标准库中的itertools.chain,它能将多个可迭代对象连接

![](http://qiniu.rearib.top/Fp7JJXJR3WWYyyFJsNUwSsbXWVUP)

# 第四章：字符串处理相关话题
## 如何拆分含有多种分隔符的字符串
![](http://qiniu.rearib.top/FoKyuL8L7YPFGnszZqq7vpI7vSUE)

- 方法1：连续使用是str.split()方法，每次处理一种分隔符号。

![](http://qiniu.rearib.top/Fh3dPvkvSWUgzjyVWJwFlpz7eQFv)

对于二维列表可以使用extend, 对于map对象需要使用list才能输出数据

![](http://qiniu.rearib.top/Fjw4lN9jPJOiHJQ7dzHT2TYVWgZU)

对于二维列表也可以使用sum方法

![](http://qiniu.rearib.top/FnToujfYD4h1vQfL77jmJtbAYZEy)

最终函数实现:

![](http://qiniu.rearib.top/FkIvPu_02c9VmMYZy7gtlm3BbQTS)

![](http://qiniu.rearib.top/Fvoqb7Z3g_GVW_NuYWm95mW68BRo)

- 方法2：使用正则表达式的re.split()方法。（推荐）

![](http://qiniu.rearib.top/FuwXS6Q2uPcQ9lm3KvAjosEH6gio)

## 如何判断字符串a是否以字符串b开头或结尾？
![](http://qiniu.rearib.top/FlKxJGvushNw4Yd94vpLmReWEBkp)

- 使用str.startswith()和str.endswith()方法。（注意：多个匹配时参数使用元组）

![](http://qiniu.rearib.top/FhEbcYWShdb0e6Lt9pmIRK6yjgi7)

![](http://qiniu.rearib.top/FvUSQWKAcGDXHeplOEkiB4y4ZsNV)

![](http://qiniu.rearib.top/Fts03QKrldsTI3IQQ4uI2woVO3bh)

![](http://qiniu.rearib.top/FpAKlDb7JZZeG3u0i13WUSCV5ToR)

![](http://qiniu.rearib.top/FimyIvdfWI7Z6NefkA9UTlF-FS5I)

## 如何调整字符串中文本的格式？
![](http://qiniu.rearib.top/FneTNjoDlliobZY1xqZe4t42YL9O)

- 使用正则表达式re.sub()方法做字符串替换，利用正则表达式的捕获组，捕获每个部分内容，在替换字符串中调整各个捕获组的顺序。

![](http://qiniu.rearib.top/FtriSHAZo4dneZx0odPnd_SCtj3T)

![](http://qiniu.rearib.top/FsWPA9hx69D7M_P_mb-UfiaKH27J)

## 如何将多个小字符串拼接成一个大字符串？
![](http://qiniu.rearib.top/FmoUUF6D5GcXtMJtFZz9OjKYwh2Y)

- 方法一：迭代列表，连续使用'+' 操作依次拼接每一个字符串。

![](http://qiniu.rearib.top/FtLHsG2hrRnQkti1Rem0APr8hFXw)

![](http://qiniu.rearib.top/Fpp5m6_l60LOGcUoOSNbQhVSk43R)

![](http://qiniu.rearib.top/FqFdsgffQkYmh-gaNArXe0lMKc5E)

- 方法二: 使用strjoin()方法，更加快速的拼接列表中所有字符串，

![](http://qiniu.rearib.top/FsFIyy42afstioGP-b0__r8p_JWX)

![](http://qiniu.rearib.top/FtOpIKDUQ6drPILsKk7KUmsj_NwW)


## 如何对字符串进行左，右，居中对齐？
![](http://qiniu.rearib.top/FvTPx22ROAyBo-sI_EjTEjFW2VzS)

- 方法一：使用字符串的str.ljust(), str.rjust(),str.center()进行左,右,居中对齐。

![](http://qiniu.rearib.top/FsYnhJQl4K9CLWu5vG9S25M9_APi)

![](http://qiniu.rearib.top/FkQe5G5Duz9mN5Xv9bkUmQySIn8K)

- 方法二：使用format()方法，传递类似'<20','>20','^20'参数完成同样任务。

![](http://qiniu.rearib.top/FqzBpjX4zVs9jKH2PHBc7CkICspE)

![](http://qiniu.rearib.top/FptmdrPcBygoUQcdsFPgyBrQ_sMy)

## 如何去掉字符串中不需要的字符？
![](http://qiniu.rearib.top/Fm85NAozeJ5VLo_2Ez60IZE7Wpmi)

- 方法一:字符串strip(), lstrip(), rstrip()方法去掉字符串两端字符.(默认去掉空白字符\t\r..)

![](http://qiniu.rearib.top/Fvyc4Msx_bvT2Tn8IKNg5zFCdMVu)

- 方法二:删除单个固定位置的字符,可以使用切片+拼接的方式.

- 方法三:字符串的replace()方法或正则表达式re.sub()删除任意子串

![](http://qiniu.rearib.top/Fs7tWQPOZMcihRVkG2D_Y94nA7L2)

- 方法四:字符串的translate()方法,可以同时删除多种不同字符

![](http://qiniu.rearib.top/FlCyqaHclI7vucM1v92hNTBixeTx)

![](http://qiniu.rearib.top/FqMdBPVZCnuVVW8q6I88az8bB8Ek)

# 第五章：文件I/O操作相关话题
## 如何读写文本文件 ?
某文本文件编码格式已知(如UTF-8, GBK, BIG5),在python 2.x和python 3.x中分别如何读写该文件?

![](http://qiniu.rearib.top/FsT_KhC3HZilHymsDKe-0KzN0Bdm)

## 如何处理二进制文件?
wav是一种音频文件的格式,音频文件为二进制文件.
wav文件由头部信息和音频采样数据构成.前面为头部信息,包括声道数,采样频率,编码位宽等等,后面是音频采样数据.
使用python,分析一个wav文件头部信息,处理音频数据.

- Python使用struct处理二进制

![](http://qiniu.rearib.top/FnRb5UHxtgxJBHyBN9HysRMefX-R)


# 第六章：数据编码与处理相关话题
## CSV数据格式存储
![](http://qiniu.rearib.top/FicE4fhFhcE3RD-vTbVl91BeGgvh)

- 标准库中的CSV模块，使用其中reader和writer完成CSV文件读写。

![](http://qiniu.rearib.top/FoRcChWL9YD3HMB5BxrRfv_7q8xT)

![](http://qiniu.rearib.top/FmN_jCsjoCIQELP6phHGEgVMWoUZ)

![](http://qiniu.rearib.top/FkXKzlNuGw0zekX5fyz6wUEx7kkS)


# 第七章：类与对象相关话题
# 第八章：多线程与多进程相关话题
# 第九章：装饰器相关话题































