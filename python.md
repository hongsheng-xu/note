# python

# python之禅

1. 如果有两个解决方案一个简单一个复杂,都行之有效,选择简单的解决方案以便后人维护
2. 现实是复杂的,有时候没有简单地解决方案,就选择最简单的可行的解决方案
3. 编写有益的注释
4. 不要企图编写完美无缺的代码.先编写行之有效的代码,再决定对其做进一步改进还是转去编写新的代码

# 代码规范

[pep0008英文](https://www.python.org/dev/peps/pep-0008/): [https://www.python.org/dev/peps/pep-0008/](https://www.python.org/dev/peps/pep-0008/)

谷歌中文: [https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/python_style_rules/](https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/python_style_rules/)

# 注释

## 单行注释

```python
#这是单行注释
# 这是单行注释,建议#后跟个空格
print("")  # 当一行代码很短,注释也很短常把注释放到代码后面,且注释和代码之间至少两个空格
```

## 多行注释

```python
""""
这是多行注释
""""
```

## todo注释

```python
# TODO(作者/邮件) 待执行项说明
```

*tips:在单行注释的#后面添加TODO关键字，能够高亮显示注释，并且能通过Project窗口快捷访问，在搭建框架时使用。TODO后面可以添加开发人员的名字，待框架完成后回来实现细节。*

# 算术运算

## 运算符

```python
+ # 加法
- # 减法
* # 乘法或用于字符串进行重复,例如:"str"*2="strstr"
/ # 除法
% # 取余
// # 取整除, 例如9//2=4
** # 求幂,例如2**3=8

# 同c一样
+=
-=
*=
/=
//= # 取整赋值
%= 
**= # 求幂赋值
```

## 优先级

| 优先级  | 运算符     |
| ------- | ---------- |
| 1(最高) | **         |
| 2       | * /  //  % |
| 3(最低) | + -        |

 *可以使用小括号`()`改变优先级,同级运算符运算次序从左至右*

# 变量与数据类型

## 声明

```python
变量 = 值 # 例如name = "zhangsan",这个变量是字符串的引用
```

*tips: 可以通过python的内置函数`id(变量)`*来查看该变量的内存地址

## 引用

**python中变量和数据是分开存储的,变量中记录数据的地址叫做引用**

**如果一个变量已经被定义,当对其重新赋值其实是修改了它的引用指向了新的地址**

```python
# 举例
a=1
id(1) == id(a)  # True
b=1
id(a) == id(b)  # True

```

## 类型

```python
# 常用的数据类型,python是自动类型推导
# 数字类型:int,float,bool,复数
# 非数字类型:字符串,元组,字典,列表
```

## 类型检测

```python
type(变量) # 获取变量的类型
```

## 标识符命名

1. 只能由字母 数字 下划线组成
2. 不能以数字开头
3. 不能与关键字重名

![变量命名规则](https://images-1300732204.cos.ap-chengdu.myqcloud.com/image-20211023121509542.png)

## 整数

### 常用方法

```python
str(变量) # 将数字转成字符串
int(变量) # 将变量转整数
```

**tips: python2中有long类型,python3中没有long类型,long存储的比int长,但python3中将int和long整合到一起**

### 运算

```python
# 数字类型变量之间可以直接运算
# bool类型的变量在参与运算时true为1,false为0
```

## 浮点数

```python
float(变量) # 将变量转浮点数
```
## 字符串

**字符串可以使用单引号`‘`或双引号`"`包裹**

```python
# 取值
字符串[下标]
字符串.index(value)  # 求子字符串在字符串中的索引

# 大小写转换
字符串.title # 英文单词首字母大写
字符串.upper # 字符串转大写
字符串.lower # 字符串转小写

# 空白
字符串.rstrip # 删除字符串空白

# 计数
字符串.count(value)  # 某个字符在字符串出现的次数
len(字符串)  # 求字符串长度

# 切片
字符串[起始位置:结束位置:步长]  # 字符串切片
字符串[-1::-1]  # 将字符串逆序

# 数学操作
+ # 拼接字符串
** # 重复字符串
```

**切片适用于字符串,列表和元组**

### 转义和编码

```python
# 转义字符同c语言一样
\n \t 
# unicode
\u****
```

### 遍历

```python
for char in 字符串 # 获得每一个字符
```

### 输出

```python
# print可以输出变量
# python2中print不带(),但有些print带括号,带括号的是函数与python3中的print函数有区别
printf "str"
# python3中的print需要带() 因为python3中的print是一个函数
print("str")
```

### 方法

1，去掉空格和特殊符号

strip() 去掉空格和换行符

strip('xx') 去掉某个字符串

lstrip() 去掉左边的空格和换行符

rstrip() 去掉右边的空格和换行符

2，字符串的搜索和替换

count('x') 查找某个字符在字符串里面出现的次数

capitalize() 首字母大写

center(n,'-')  把字符串放中间，两边用- 补齐

find('x')  找到这个字符返回下标，多个时返回第一个；不存在的字符返回-1

index('x') 找到这个字符返回下标，多个时返回第一个；不存在的字符报错

replace(oldstr, newstr) 字符串替换

format（） 字符串格式化

format_map(d) 字符串格式化，传进去的是一个字典

3，字符串的测试和替换函数

startswith(prefix[,start[,end]]) 
\#是否以prefix开头 
endswith(suffix[,start[,end]]) 
\#以suffix结尾 
isalnum() 
\#是否全是字母和数字，并至少有一个字符 
isalpha() #是否全是字母，并至少有一个字符 
isdigit() #是否全是数字，并至少有一个字符 
isspace() #是否全是空白字符，并至少有一个字符 
islower() #S中的字母是否全是小写 
isupper() #S中的字母是否便是大写 
istitle() #S是否是首字母大写的

4，字符串的分割

split() 默认是按照空格分割

split(',')  按照逗号分割

5，连接字符串

join(slit)   用逗号连接slit 变成一个字符串，slit 可以是字符，列表，字典（可迭代的对象）

​            int 类型不能被连接

## 列表

 *即c语言的数组,使用数组的下标来进行访问*

**列表中可以存储不同类型的数据**

### 常用方法

```python
# 增加元素
列表.append  # 将元素添加到数组末尾
列表.insert(position,value)  # 在指定位置插入元素
列表.extend(列表2)  # 将列表2追加到列表1

# 删除元素
del 数组名[下标]  # 删除指定下标的元素
列表.pop(position)  # 不给参数则删除数组最后一个元素--弹出栈,给定参数则删除指定位置的元素
列表.remove(value)  # 删除数组中第一个值为value的元素

# 元素排序
列表.sort  # 对数组从小到大或字符数组排序(按a-z),这样的操作会改变数组元素的位置,参数reverse=True;排序方式反转
列表.sorted  # 保留列表的原来位置,对列表临时排序
列表.reverse  # 反转列表

# 列表长度
len(列表)  # 求列表的长度
列表.count(值)  # 求此列表中该值出现的次数

# 其他方法
列表.index(值)  # 求值所在的索引,如果值不在列表中会报错
列表.clear  # 清空列表
list(range(intA, intB, 步长))  # 生成一个从intA到intB的递增数组但不含intB的数字集,即数字集为[intA , intB)不指定步长则步长默认为1,list函数将结果转换为列表
min  # 求列表的最小值
max  # 求列表的最大值
sum  # 求列表的和

# 检查某个值在列表中
值 in 列表  # True 或 False 
值 not in 列表  # True 或 False 

# 列表解析: 将一个有for循环创建的元素合并为列表
[表达式1 for 表达式2] # 表达式1和表达式2中的变量名一致,表达式1用于操作for循环每次的值
# 示列如下
arr = [value*2 for value in range(1,5)]

# 列表的运算
列表1 += 列表2  # 本质是在调用extend将列表2追加到列表1

# 列表切片
列表名[位置1:位置2] # 切片,如果位置2不写则默认到末尾,如果是列表[负数:]表示取列表最后几个元素,这里的切片不是引用,w
列表[:]  # 复制列表
```

**切片适用于字符串,列表和元组**

### 列表遍历

```python
for 变量 in 列表
while 列表:  # 循环的结束条件是列表为空
```

## 元组

**元组定义后不能增删改,可以存储不同类型的数据**

```python
变量 = (value1,value2,value3...)  # 元组

# 取值
变量[下标]  # 可以通过下标的方式对多元组进行取值,但是不能对其赋值,这样的操作不被允许 

变量 = ()  # 定义一个空元组
变量 = (value, )  # 定义一个数据的元组,注意必须有逗号,不然解释器会认为这是优先级的符号会忽略小括号 
# 多变量接收元组的值
变量1,变量2... = 元组  # 注意元组的长度要和变量的数量一致

# 常用方法
元组.count(value)  # 对元组中出现的某个value计数
元组.index(value)  # 求数据在元组中的索引
len(元组)  # 统计元组的长度

# 变量交换
a,b = (b,a)  # 元组交换数据
a,b = b, a  # 省略小括号的元组
```

### 元组遍历

```python
for 变量 in 元组
```
## 元组和列表相互转换

```python
list(元组)  # 将元组转换成列表
tuple(列表)  # 将列表转换为元组
```
## 字典

**字典的键只能是`字符串 数字 元组`类型但值可以是任意类型**

```python
变量 = {key1:value1,
      key2:value2, # 通常一行一个键值对 
      key3:value3...}  # 定义一个字典
变量 = {}  # 定义空字典
# 字典列表
[{},{},{}]

# 字典嵌套列表和字典
{key:[],key:{}}

# 取值
变量[key]  # 通过key取值 

# 添加键值对
变量[新键名] = 值

# 删除键值对
del 变量[键名]
字典.pop(key) # 删除字典中指定的键值对

# 改值
变量[键名] = 值

# 统计键值对数量
len(字典)

# 合并字典
字典1.update(字典2)  # 相同类型的键会被后者覆盖 

# 清空字典
字典.clear()  # 清空所有键值对 

```

### 遍历

```python
# 键值对变量
for key,value in 字典

# 键遍历
for key in 字典
for key in 字典.keys()  # 按键的顺序遍历

# 值遍历
for value in 字典.values()

# while
while 字典:  # 循环退出的条件是字典为空 
```

## 公共方法 运算符

#### 方法

**python中列表 元组 字典都能使用的方法**

```python
# python内置模块含有的方法无需导入
len  # 求长度
del(变量)  # 此处的del做函数
max  # 最大值,如果是字典只能比较key
min  # 最小值,如果是字典只能比较key
cmp  # 比较两个值,但是python3中取消了此值因为python3中比较使用大于符号,可以比较字符串,元组和列表  

# 切片,字典是不能切片的,字符串,列表元组可以切片
```

#### 运算符

```python
* 或 + # 重复,字符串,列表,元组
in 或 not in # 元素是否存在 字符串,列表,元组,字典
> 或 < 或 == 或 >= 或 <=  # 比较元素 字符串,列表,元组 
```

## 可变和不可变类型

- 不可变类型: 内存中的数据不允许被修改
  - 数字类型: int bool flaot complex long
  - 字符串
  - 元组
- 可变类型: 内存中的数据可以被修改
  - 列表
  - 字典

## 作用域

- 全局变量: 函数外部定义的变量,所有的函数都可以访问

  - python对全局变量的约束

    - 函数内部可以获得全局变量引用但是不能修改全局变量,python中尝试在函数内部修改的全局变量解释器会认为是在新定义一个和全局变量同名的局部变量,如果在此之前有对全局变量的引用且之后有重新定义变量会报错

      ```python
      a=2
      def print_a():
          print(a)  # 报错,a不能在被定义之前使用,暂时性死区
          a=3  # 解释器认为这是函数内部的局部变量而不是全部变量在被修改
          print(a)
      
      print_a()
      ```

  - python修改全局变量

    - 使用关键字global先声明一下变量

    ```python
    a = 1
    def fun()
    	global a
        a = 2
    print(a)  # 1
    fun()
    print(a)  # 2
    ```

  - 全局变量一般都放在import语句之后

  - 全局变量以`g_` 或`gl_`做前缀

- 局部变量: 函数内部的变量,运行结束后会自动回收

  - 在函数执行时创建
  - 执行结束后回收
  - 在此生命周期内函数内部使用

# 常量

**python中没有真正意义上的常量,只能人为的认为以大写字母开头的变量为常量**

**常量命名规范为: 所有字母大写加下划线组成**

# 输入输出

```python
# 输入
变量1=input("格式化字符串" % (变量2,变量3...))  # input获取的是字符串对于数字输入需要使用int()或float()转换一下 
# 输出
print("格式化字符串" % (变量1,变量2...)) # 小括号(变量)就是一个元组
str = "格式化字符串" % 元组
print(str) # 效果和上面一致
# 输出不换行
print("字符串", end="") # end可以替换字符串的结尾,默认是'\n'
```

# 顺序选择循环

## 顺序

**代码从上到下执行**

## 选择

### 比较运算符

```python
== # 判断相等
!= # 不等
> # 大于
< # 小于
>= # 大于等于
<= # 小于等于
```

### 逻辑运算符

```python
and or not # 与或非
```

### if语句

```python
if 表达式:
    执行语句1 # 此行要有一个Tab
    执行语句2 # 需要Tab
else:
    执行语句 # 此行要有一个Tab

#多重if
if 表达式:
   执行语句
elif 表达式:
	执行语句
else:
    执行语句
    
# 嵌套if
if 表达式:
    if 表达式:
 		执行语句

# 多条件
if ((表达式1)
        逻辑运算符(表达式2)   # 2个Tab
		逻辑运算符(表达式3)):  # 2个Tab
```

*tips: pycharm中可以选择多行按下tab键,选中行会缩进tab,按下shift+tab会减少tab缩进*

### 多重选择

**Python 中没有 switch/case 语法，如果使用 if/elif/else 会出现代码过长、不清晰等问题。而借助字典就可以实现 switch 的功能**

```python
def case1():                            # 第一种情况执行的函数
    print('This is the case1')


def case2():                            # 第二种情况执行的函数
    print('This is the case2')


def case3():                            # 第三种情况执行的函数
    print('This is the case3')


def default():                          # 默认情况下执行的函数
    print('No such case')


switch = {'case1': case1,                # 注意此处不要加括号
          'case2': case2,
          'case3': case3,
          }

choice = 'case1'                         # 获取选择
switch.get(choice, default)()            # 执行对应的函数，如果没有就执行默认的函数
```

## 循环

### while

```python
while 表达式: 
	执行语句 # tab缩进

# 循环嵌套
while 表达式:
    while 表达式:
```

### for

```python
# 只能遍历可迭代变量
for 变量 in 列表或元组或字典或字符串

# for else常用于查找,找到后break退出,未找到则执行else
for 变量 in 可迭代集合
	执行语句
else:  # 当for循环没有通过break退出循环时会执行
    执行语句 
```

### beak

```python
while 表达式:
    if 表达式:
        break  # 跳出循环
```

### continue

```python
while 表达式:
    if 表达式:
        continue  # 进入下一次循环
```

# 函数

```python
"""
函数定义上方需要两个空格
函数的描述不应该在函数的上方因为不方便阅读
"""


def 函数名(参数1=默认值, 参数2=默认值):
    """这里是函数描述信息
    :param 参数1: 描述
    :return: 返回值描述
    """
	# 函数体
	执行语句 # 有一个tab
    # 函数的嵌套调用
    函数名() # 此处的函数名一定是在此函数前已经申明的
	return 结果  # return关键字后续代码不会执行
    
# 函数调用
变量 = 函数名(传递参数名=值) # 注意函数的调用不能在函数声明或导入前
# 导入函数调用
变量 = python文件名.函数名() # 声明变量获取值
# 函数返回元组
变量1,变量2... = 函数()  # 用于依次获取返回的元组值并且赋值给新的变量,注意这种方式函数返回的元组长度要和变量的数量一致,否则报错

# 传递任意数量形参
def 函数名(形参1,形参2,* 形参3):  # 需要将余下的形参收集在* 形参3中

# 传递任意数量形参且接收任意数量的键值对
def 函数名(形参1,形参2,** 形参3):
	for key,value in 形参3.items()  # 获取形参3的
```

*tips: pycharm中使用ctrl+q查看函数说明*

**python中函数的参数传递和返回值都是引用传递**

## 形参和实参

```python
函数名(实参) # 调用函数传的是实参

def 函数名(形参): # 定义的是形参

# 函数中是不能修改不可变类型的,但是可以修改可变类型如列表或字典中的数据如果不想让函数修改可以使用
def 函数名(列表[:]):  # 通过创建一个列表的备份来避免被修改
```

**函数中,形参的地址和实参一致,但是在函数中对形参进行修改实际是修改了形参的引用形参指向了其他地址(该地址上的数据就是新赋值的数据)从而避免了实参的数据被修改**

## 缺省参数

```python
# 函数默认值
def 函数名(形参1,形参2=默认值,形参3=默认值):  # 函数的调用需要传递对应的参数,按照个数依次传递,对于有默认值的参数,想修改默认值但又不想传递其他参数可以这样调用函数名(形参2=其他值)
```

**缺省参数必需是在参数的末尾可以有多个缺省参数**

## 多值参数

**函数接受的参数是不确定的**

```python
# 一个*号可以接受元组两个*号可以接受字典
# * 将数字集合收集为元组arg,**将键值对收集为字典
def func (*args,**kwargs):

# 调用多值参数
func(数字集合,键值对)

#拆包
func(*args,**kwargs) # 将变量拆解: 元组变成数据集合,字典变成键值对
```

# class

## 封装

**OOP: 面对象编程** 概念: 类和对象和java一样的思想 对象是类的具体实例

```python
# dir(变量) 查看该类的所有方法

# 定义--类命名: 大驼峰命名
class 类:	# python中类是一个特殊的对象
    属性 = 值 # 类属性
	def 方法(self,参数...):  # 第一个参数必需是self就是java类中的this,是对象实例的引用

        # 分配空间
__new__(self,参数列表)  # 为对象分配内存空间并返回对象的引用 
        
# 构造函数
__init__(self,参数列表)  # 创建实例对象时都会调用这个方法,创建实例时的参数会被收集到参数列表

# 销毁
__del__(self,参数列表)  # 对象内存空间即将被回收时会执行此方法

# 修改print方法,返回值必须是一个字符串
__str__(self,参数列表)  # 在使用print输出这个对象实例时调用的方法其实就是java的toString,重写了原来的方法

# 私有属性和方法(特点和java一样private修饰一样)
__属性或方法  # 定义的方法名前有两个下划线表示是类私有的属性或方法

# 创建实例
变量 = 类()  # print 输出对象的类和地址,实例的创建过程和java一致,先调用__new__并将返回的引用传递给__init__

# 增加属性(不推荐)
实例.属性 = 值  # 为一个实例增加属性
```

*tips: 对象内置方法,在对象的方法中以`__`开头和`__`结尾的方法是内置的* 

**在创建一个对象时不应该让外界直接修改对象内部的属性,应该提供set和get方法(像java一样),python是没有真正的私有方法和属性的只是对`__`开头的属性和方法做了处理变成了`_类__属性或方法`的样子通过这样的方法防止外界访问对象的私有属性和方法所以python的私有属性和方法是伪私有属性和伪私有方法,但是java是有真正的私有属性和方法的,es6(JavaScript的标准)的私有属性和私有方法与python相似**

### 身份运算符

```python
# 判断两个变量是否为同一个对象的引用
A = 类（）
B = A
A is B  # True
A is not B # False
```

*tips: is和==的区别is用于判断对象引用是否为同一个而`==`判断值是否相等*

```python
a=[1,2,3]
b=[1,2,3]
a == b # True
a is b # False
```

**对python中None进行判断时不要使用==而使用is**

```python
A is None # 对象A不存在
```

### 类属性和方法

**类似于java的静态属性和静态方法**

```python
class 类:
    属性 = 值
    def 方法():
        类.属性 # 通过类.属性获取值所有的对象都有的一个值共享
        # 不要使用对象.属性来访问类属性,虽然python会向上查找,一旦使用对象.属性经过赋值后,python解释器会向对象添加属性,这个属性引用就不是类的属性了,而是这个对象的属性也不会修改到类属性的值
	@classmethod
    def 方法(cls) # 通过装饰器来添加类方法,第一个参数必须是cls,是对类的引用,调用方法时不需要传递cls这个参数
    	cls.属性 # 访问类的属性
     @staticmethod
    def 方法() #如果这个方法不访问实例属性和方法或调用类属性和方法,通过类名.方法来调用不需要实例化
```

**python的对象属性和方法查找类似js的原型和原型链,向上查找,查找对象本身然后找到父类**

## 继承

**基本的面对象开发都有的相似的概念,子类可以继承自父类,由此拥有父类的所有属性和方法**

```python
class Father:	# 基类,父类,所有类的基类是object
    def __init__(self):
        pass
    
class Son(Father):	# son继承父类,派生类
    def __init__(self)
    	super().__init__(参数)# 如果构造函数需要参数也要和java一样也需要去super--父类的构造函数

    # 父类的方法不能满足子类的需要需要重写父类的方法 override
    def 与父类同名的方法
```

**super在python中是一个特殊的类,spuer()就是super创建的一个对象,这里的super有和java中的相似,通过在子类中使用super()对象可以调用父类的方法**

**子类方法不能继承父类的私有属性和方法!!!**

**python没有抽象方法和抽象类**

## 多继承

**子类可以继承自多个父类这是java没有的,java中一个子类只能有一个父类**

```python
class A:
    def __init__(self):
        pass
class B:
    def __init__(self):
        pass
class C(A,B):	# 子类可以调用所有父类的公共方法
    def __init__(self):
        pass
```

**注意: 如果多个父类有相同的方法,那么避免使用多继承**

**MRO: python中多个父类有相同的方法时,python中类有一个属性`___mro__`可以查看方法的搜索顺序,主要用于多继承时方法,属性调用的判断顺序**

```python
class A:
	pass
class B:
	pass
class C(A,B):	# 子类可以调用所有父类的公共方法
    pass

print(C.__mro__)
# 结果: 按照元组中的顺序从左至右依次查找方法和属性
(<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>)
```



### abc模块实现抽象类和抽象方法

```python
#一切皆文件
import abc #利用abc模块实现抽象类

class All_file(metaclass=abc.ABCMeta):
    all_type='file'
    @abc.abstractmethod #定义抽象方法，无需实现功能
    def read(self):
        '子类必须定义读功能'
        pass

    @abc.abstractmethod #定义抽象方法，无需实现功能
    def write(self):
        '子类必须定义写功能'
        pass

# class Txt(All_file):
#     pass
#
# t1=Txt() #报错,子类没有定义抽象方法

class Txt(All_file): #子类继承抽象类，但是必须定义read和write方法
    def read(self):
        print('文本数据的读取方法')

    def write(self):
        print('文本数据的读取方法')

class Sata(All_file): #子类继承抽象类，但是必须定义read和write方法
    def read(self):
        print('硬盘数据的读取方法')

    def write(self):
        print('硬盘数据的读取方法')

class Process(All_file): #子类继承抽象类，但是必须定义read和write方法
    def read(self):
        print('进程数据的读取方法')

    def write(self):
        print('进程数据的读取方法')

wenbenwenjian=Txt()

yingpanwenjian=Sata()

jinchengwenjian=Process()

#这样大家都是被归一化了,也就是一切皆文件的思想
wenbenwenjian.read()
yingpanwenjian.write()
jinchengwenjian.read()

print(wenbenwenjian.all_type)
print(yingpanwenjian.all_type)
print(jinchengwenjian.all_type)
```

## 多态

**不同的子类对象调用相同的父类方法得到不同结果**

# 设计模式

## 单例设计模式

- 类创建对象--但该类只能有唯一的实例
- 每一次执行,类()返回的对象内存地址是相同的

## 单例

```python
class A:
    instance = None  # 保存实例的引用
    is_init = False # 是否已经初始化
    def __new__(cls,*args,**kwargs):  # 重写new方法,每一次返回相同地址
        if cls.instance is None:
    		return cls.instance = super().__new__(cls) # 一定要返回分配的内存空间
        return cls.instance
    def __init(self):
        # 初始化,某些情况下需要初始化函数只被执行一次
        if A.is_init :
            return;
        A.is_init = True
        # 初始化
```

# 异常

## 异常捕获

```python
try:
	# 执行语句
except:
    # 执行语句
 
# 按类型捕获
try:
    #执行语句
except 错误类型:
    # 对某种错误类型捕获
    pass
except (错误类型2,错误类型3):
    # 对某几种错误类型捕获
   	pass
except Exception as res:	# 捕获异常后需要用as将详细信息赋值到变量res中,这个错误是所有错误的父类,和java一样都可以捕获所有的错误
    print(res) # 捕获所有错误
else: 
    # 没有错误发生时需要执行
    pass
finally:
    # 无论什么情况下都会执行的代码
    pass
```

## 异常传递

**异常会在发生的地方冒泡传递,一直传递到主程序如果没有在主程序捕获异常那么程序将会终止**

```python
# 在主程序中捕获异常
try:
    主程序
except Exception as e:
    处理
```

## 主动抛出异常

```python
# 先使用Exception创建异常对象
err = Exception("错误信息")
# 出错后抛出这个异常
raise err# 抛出异常对象
```

## 自定义异常

**和java相似,python继承Exception类后重写方法**

```python
#1.用户自定义异常类型，只要该类继承了Exception类即可，至于类的主题内容用户自定义，可参考官方异常类
class myExceptin(Exception):
    def __init__(self):
        pass
    def __str__(self):
        return "错误描述信息"
```

# 包

​	*从物理上看，包就是一个文件夹，在该文件夹下包含了一个 __init__.py 文件，该文件夹可用于包含多个模块源文件；从逻辑上看，包的本质依然是模块。*

定义包更简单，主要有两步：

1. 创建一个文件夹，该文件夹的名字就是该包的包名。
2. 在该文件夹内添加一个 `__init__.py` 文件即可。
3. `__init__`文件必需指定对外提供的模块列表

**可以通过import将该包里的所有模块一次性导入**

```python
# 包/__init__.py

from . import python文件1
from . import python文件2...

# 外部python
import 包
包.模块.函数()
```

## 制作和发布包

#### 1) 创建 [setup.py](http://setup.py/)

包的同一级路径下新建`setup.py` 的文件

```python
from distutils.core import setup

# 多值的字典参数，setup是一个函数
setup(name="Hello",  # 包名
      version="1.0",  # 版本
      description="a simple example",  # 描述信息
      long_description="简单的模块发布例子",  # 完整描述信息
      author="hona",  # 作者
      author_email="1394948752@qq.com",  # 作者邮箱
      url="www.onefine.top",  # 主页
      py_modules=["hello.request",
                  "hello.response"])  # 记录包中包中包含的所有模块
```

有关字典参数的详细信息，可以参阅官方网站：https://docs.python.org/2/distutils/apiref.html

#### 2) 构建模块

###### 构建模块命令如下

```bash
python setup.py build
```

###### 如果出现下面情况

```bash
onefine@onefine-virtual-machine:~/PycharmProjects/Distutils$ python3 setup.py build
Traceback (most recent call last):
  File "setup.py", line 1, in <module>
    from distutils.core import setup
ModuleNotFoundError: No module named 'distutils.core'
```

> 因为ubuntu-18.10 默认没有安装 pip ，需要安装 python3-pip

#### 3) 生成发布压缩包

###### 生成发布压缩包命令如下

```bash
python setup.py sdist
```

## 安装模块

```bash
tar -zxvf 包名.tar.gz # 解压
python setup.py install # 安装
```

## 卸载模块

**直接删除这个包就行**或`pip uninstall 包`

# 文件

## 操作方法

```python
#  打开文件
open(文件路径,"rwa+")  # 返回文件对象,文件不存在则会抛出异常

# 读取文件
文件对象.read() # 文件对象自带的方法,文件指针会移动到文件的末尾,第二次调用就读取不到内容

# 写文件
文件对象.write() # 写

# 关闭文件
文件对象.close()

# 完整示列
file = open(test.txt)
file.read()
print(file)
file.close()
"""
python中对文件、文件夹（文件操作函数）的操作需要涉及到os模块和shutil模块。

得到当前工作目录，即当前Python脚本工作的目录路径: os.getcwd()

返回指定目录下的所有文件和目录名:os.listdir()

函数用来删除一个文件:os.remove()

删除多个目录：os.removedirs（r“c：\python”）

检验给出的路径是否是一个文件：os.path.isfile()

检验给出的路径是否是一个目录：os.path.isdir()

判断是否是绝对路径：os.path.isabs()

检验给出的路径是否真地存:os.path.exists()

返回一个路径的目录名和文件名:os.path.split()     eg os.path.split('/home/swaroop/byte/code/poem.txt') 结果：('/home/swaroop/byte/code', 'poem.txt') 

分离扩展名：os.path.splitext()

获取路径名：os.path.dirname()

获取文件名：os.path.basename()

运行shell命令: os.system()

读取和设置环境变量:os.getenv() 与os.putenv()

给出当前平台使用的行终止符:os.linesep    Windows使用'\r\n'，Linux使用'\n'而Mac使用'\r'

指示你正在使用的平台：os.name       对于Windows，它是'nt'，而对于Linux/Unix用户，它是'posix'

重命名：os.rename（old， new）

创建多级目录：os.makedirs（r“c：\python\test”）

创建单个目录：os.mkdir（“test”）

获取文件属性：os.stat（file）

修改文件权限与时间戳：os.chmod（file）

终止当前进程：os.exit（）

获取文件大小：os.path.getsize（filename）


文件操作：
os.mknod("test.txt")        创建空文件
fp = open("test.txt",w)     直接打开一个文件，如果文件不存在则创建文件

关于open 模式：

w     以写方式打开，
a     以追加模式打开 (从 EOF 开始, 必要时创建新文件)
r+     以读写模式打开
w+     以读写模式打开 (参见 w )
a+     以读写模式打开 (参见 a )
rb     以二进制读模式打开
wb     以二进制写模式打开 (参见 w )
ab     以二进制追加模式打开 (参见 a )
rb+    以二进制读写模式打开 (参见 r+ )
wb+    以二进制读写模式打开 (参见 w+ )
ab+    以二进制读写模式打开 (参见 a+ )

 

fp.read([size])                     #size为读取的长度，以byte为单位

fp.readline([size])                 #读一行，如果定义了size，有可能返回的只是一行的一部分

fp.readlines([size])                #把文件每一行作为一个list的一个成员，并返回这个list。其实它的内部是通过循环调用readline()来实现的。如果提供size参数，size是表示读取内容的总长，也就是说可能只读到文件的一部分。

fp.write(str)                      #把str写到文件中，write()并不会在str后加上一个换行符

fp.writelines(seq)            #把seq的内容全部写到文件中(多行一次性写入)。这个函数也只是忠实地写入，不会在每行后面加上任何东西。

fp.close()                        #关闭文件。python会在一个文件不用后自动关闭文件，不过这一功能没有保证，最好还是养成自己关闭的习惯。  如果一个文件在关闭后还对其进行操作会产生ValueError

fp.flush()                                      #把缓冲区的内容写入硬盘

fp.fileno()                                      #返回一个长整型的”文件标签“

fp.isatty()                                      #文件是否是一个终端设备文件（unix系统中的）

fp.tell()                                         #返回文件操作标记的当前位置，以文件的开头为原点

fp.next()                                       #返回下一行，并将文件操作标记位移到下一行。把一个file用于for … in file这样的语句时，就是调用next()函数来实现遍历的。

fp.seek(offset[,whence])              #将文件打操作标记移到offset的位置。这个offset一般是相对于文件的开头来计算的，一般为正数。但如果提供了whence参数就不一定了，whence可以为0表示从头开始计算，1表示以当前位置为原点计算。2表示以文件末尾为原点进行计算。需要注意，如果文件以a或a+的模式打开，每次进行写操作时，文件操作标记会自动返回到文件末尾。

fp.truncate([size])                       #把文件裁成规定的大小，默认的是裁到当前文件操作标记的位置。如果size比文件的大小还要大，依据系统的不同可能是不改变文件，也可能是用0把文件补到相应的大小，也可能是以一些随机的内容加上去。

 

目录操作：
os.mkdir("file")                   创建目录
复制文件：
shutil.copyfile("oldfile","newfile")       oldfile和newfile都只能是文件
shutil.copy("oldfile","newfile")            oldfile只能是文件夹，newfile可以是文件，也可以是目标目录
复制文件夹：
shutil.copytree("olddir","newdir")        olddir和newdir都只能是目录，且newdir必须不存在
重命名文件（目录）
os.rename("oldname","newname")       文件或目录都是使用这条命令
移动文件（目录）
shutil.move("oldpos","newpos")   
删除文件
os.remove("file")
删除目录
os.rmdir("dir")只能删除空目录
shutil.rmtree("dir")    空目录、有内容的目录都可以删
转换目录
os.chdir("path")   换路径
"""
```

## 示列

```python
# 读取文件
with open(文件,方法) as file:  # 别名
    contents = file.read()
    
# 按行读取
file = open()
while True
	line = file.readLine() # 每一次读取文件指针移动到行尾
    if not line # 读取到行尾
    	break

# 按行读取
with open() as file 
	for line in file
    	print(line) #读取行
        
```

# 关键字

## 所有关键字

```python
# 通过这个库查看所有的关键字
import keyword
print(keyword.kwlist)
# keyword.kwlist 33个关键字
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 
 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 
 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or',
 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']  
```
## import

**导入模块和文件**

**`import`语句必需放在可执行代码的首行**

```python
# 导入顺序
# 1. 官方标准
# 2. 第三方模块
# 3. 应用模块
# 放在可执行代码之前
import 包名/文件名 # 导入其他工具包或其他python文件,里面的所有语句都会被执行一次

# 导入特定函数/类
from 模块 import 函数名/类

# 导入所有函数/类
from 模块 import *

# 别名
from 模块 import 函数1 as 函数2  # 为函数1起别名为函数2

# 模块别名,模块别名应该是大驼峰命名
import 模块1 as 模块2  # 为模块1起别名为模块2

# 后导入的同名工具会覆盖先前导入的工具
# 每一个模块内置一个属性__file__表示该模块的路径
```

*tips: import的模块名也是一个标识符这意味着不能是以数字开头也不能是标识符,建议xx_xx*

**python提供了内置属性,每一个模块都有`__name__`,在本模块下`__name__`是字符串`__main__`,在被导入的文件里,这个变量是模块名可以用于测试代码**

```python
# 该文件是一个模块
def func():
    pass

def main():	# 测试该模块的主函数
    pass
if __name__ == "__main__"
	main() # 执行测试代码
    
# 该文件被导入时测试函数main不执行
```



**python会对导入的模块先进行编译为`.pyc`结尾的文件,pyc文件是python对模块编译后的二进制文件,因此二进制文件的执行速度会比先解释在执行的要快很多**

### pip

pip 是 Python 包管理工具，该工具提供了对Python 包的查找、下载、安装、卸载的功能。

### pip 最常用命令

**显示版本和路径**

```
pip --version
```

**获取帮助**

```
pip --help
```

**升级 pip**

```
pip install -U pip
```

> 如果这个升级命令出现问题 ，可以使用以下命令：
>
> ```
> sudo easy_install --upgrade pip
> ```

**安装包**

```
pip install SomePackage              # 最新版本
pip install SomePackage==1.0.4       # 指定版本
pip install 'SomePackage>=1.0.4'     # 最小版本
```

比如我要安装 Django。用以下的一条命令就可以，方便快捷。

```
pip install Django==1.7
```

**升级包**

```
pip install --upgrade SomePackage
```

升级指定的包，通过使用==, >=, <=, >, < 来指定一个版本号。

**卸载包**

```
pip uninstall SomePackage
```

**搜索包**

```
pip search SomePackage
```

**显示安装包信息**

```
pip show 
```

**查看指定包的详细信息**

```
pip show -f SomePackage
```

**列出已安装的包**

```
pip list
```

**查看可升级的包**

```
pip list -o
```

### pip 升级

**Linux 或 macOS**

```
pip install --upgrade pip    # python2.x
pip3 install --upgrade pip   # python3.x
```

**Windows 平台升级：**

```
python -m pip install -U pip   # python2.x
python -m pip3 install -U pip    # python3.x
```

### pip 清华大学开源软件镜像站

使用国内镜像速度会快很多：

临时使用：

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```

例如，安装 Django：

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple Django
```

如果要设为默认需要升级 pip 到最新的版本 (>=10.0.0) 后进行配置：

```
pip install pip -U
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

如果您到 pip 默认源的网络连接较差，临时使用本镜像站来升级 pip：

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U
```

## del

**从内存中删除变量**

```python
# 从内存中删除
del 变量  # 从内存中删除此变量,此后该变量不能再使用此变量
del 列表[下标]  # 删除列表的值但不推荐,建议使用列表的pop
del 字典[键名]  # 删除字典中的键值对
```

## pass

**pass用于保证程序的结构正确,在运行时不会有任何作用**

```python
# 占位符 -- 当写代码未写实际执行语句时可以使用pass占位,pass什么也不执行
if 1 == 2
	pass  # 暂时没有实际代码
elif 1 == 1
	pass  # 暂时没有实际代码
```

**python在执行上述代码时遇到pass会向后继续执行**

## global

**修改全局变量的值**

```python
# 函数内部修改全局变量
gl_num = 0;
def func(): 
    global gl_num
    gl_num=2  # 修改全局变量
```



