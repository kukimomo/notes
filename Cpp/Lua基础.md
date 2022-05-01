# Lua

Lua是一门小巧,轻快,跨平台以及开源的脚本语言,它的源代码完全由C语言编写,它的效率及其高,接近C语言.

## Lua基础

#### Lua基本语法

##### Lua的数据类型与值

###### 数据类型

在Lua中,有以下几种数据类型:

* number : 数字类型,它对应的值包括整数和浮点数

* nil : 表示空,像C中的NULL和Java中的null,它对应的值就是nil

* boolean : 布尔值,它对应的值包括true和false,在判断中只有false和nil会使得结果为false,其他结果都会导致判断结果为true.

* string : 字符串类型,它对应的值就是用单引号或者双引号以及双方括号括起来的东西.也就是'字符串内容',''字符串内容'',[[字符串内容]]都可以表示字符串

  * Lua中的转义字符是与C/C++中的转义字符一样的,都可以用\来表示,比如\n表示换行.

  * 字符串类型中如果全是数字的话,可以直接与number类型直接相加,纯数字的字符串会默认转换为number类型.

  * 字符串连接符 : .. ,比如10 .. "11"结果会是1011,或者10..11结果也是1011,用这个运算符会将对应类型转换成字符串

  * 字符串转换函数 : 

    * tonumber(需要转换的字符串),通过这个函数就可以将字符串转换成number类型的数据.
    * tostring(需要转换的数据) : 可以将其它类型的数据转换成字符串类型的数据.

  * 字符串库

    在Lua中,提供了对于string类型数据的相关库,它叫String Manipulation.里面包括了对字符串的各种操作.如同Java中String类中提供的各种方法一样.

* function : 函数类型

  函数是"一类值",所以一个变量是可以存储函数的,它就相当于一个普通的数据类型.

  * 函数的定义

    function 函数名(参数列表) 函数体 end

  函数定义好后,可以直接通过函数名去赋值给变量,那么那个变量就是一个函数类型的变量,并且函数是可以作为参数去传递到其他函数的参数列表里去的.

* userdata : 用户数据类型,也就是我们自定义类型的总称,这方面比较多,后面说

* thread : 线程类型,内容较多,后面说

* table : 表类型,内容也多,后面说

table,function以及userdata类型的值是对象,这三种类型的变量不会实际包含这些值,仅仅只是引用它们.赋值,参数传递,函数返回值都不会实际上对具体的那三种类型的东西复制一份,而是直接去引用它们.它们就相当于是Java中new出来的对象.是被其他变量或者操作去引用的,也相当于是C++中的new出来的对象,而且呢,Lua中的内存管理同Java一样,它是有GC的,所以我们需要把用完的对象引用置空,GC才会去回收内存,这点跟Java很相像.



##### Lua运算符与表达式

* 算术运算符

  在Lua中,数据之间的算术运算符包括二元运算符和一元运算符.它主要是number类型之间的计算,返回的也是number类型的东东.

  * 二元运算符 : + , - , * , / , ^ 
  * 一元运算符 : -

* 关系运算符

  * ==,~=,>,<,>=,<=这类一般的number类型间的比较
  * 对于==来讲,可以判断两个东西是否相同,相同的条件是数据类型以及数值都一致
  * 对于那三种对象类型的来讲,==需要是同一个引用才会返回true,也就是同时指向同一个对象的才算相等.

* 逻辑运算符

  * and,or,not.也就是与或非
  * 对于数值类型的数据,使用逻辑运算符会返回数值,而对于boolean类型来说,使用逻辑运算符会返回boolean类型的东东.

* 连接运算符

  * ..
  * 连接符可以对数字和字符串进行连接.

* 运算符优先级

  * ^ -> not,- ->*,/ -> +, - ->.. ->==,~=,>,>=,<,<= ->and -> or
  * 同样的,也可以用括号来改变优先级

##### Lua的表

###### 表的初始化

* 一般的初始化方式 : [] 或者{}这就是一个空表

  ```Lua
  a = [] --这样就是建立了一个空表并让a指向这个空表.
  b = [x = 100,y = 200,....] --这样就是静态化的建立了一个包含x,y两个键值对的表,并让b指向这个表
  a.x = 200 --或者a[x]也可以
  a.y = 2000 --也可以这样给表添加数据,这样就类似于一个只有成员变量的结构体.
  --对于表里的键值对,它的键类型可以是随便的,变量名也好,字符串也好都行.
  c = (["+"] = "abc"),(["axc"] = "===")
  print(c["+"]) --这样就可以输出abc
  --其实也可以不需要键值,如果不用键值的话,就相当于一个数组,键值就是数组下标,不过默认第一个是1.
  d = [1,2,3,4,5,6,7]
  print(d[1]) --输出1
  ```

  * 对于表,有一个例子:

    ```lua
    --比如我们有一个a.txt文件,它里面有几行字符串
    list = nil 
    filename = "a.txt所在的绝对路径"
    for line in io.inline(filename) do
        list = {next = list,value = line}
    end
    --io.inline()这个函数的作用是在循环中返回一个回调函数,这个回调函数会去获取到文件的每一行并返回,比如第一次返回文件里的第一行,第二次循环返回文件里的第二行...直到最后返回nil结束循环
    --在这个循环体中,每次都会构造一个表,它的结构是这样的:
    -- 刚开始是nil,然后构造一个next = nil,value = 第一行数据的表赋值给list,此时它的结构是这样的: next = nil ,value = 第一行数据. 经过第二次循环,它会再次构造一个表,这个表为:next = 上一个表 , value = 第二行数据.如果我们的文件只有两行数据,那么这个循环就会结束,就得到了结构如此的一个链表.这个链表有两个节点,一个是next = nil,value = 第一行数据, 第二个节点是next = [next = nil,value = 第一行数据],value = 第二行数据.
    --经过这个操作,list最终会是一个链表.
    
    ```

##### Lua赋值语句

* 在Lua里,变量不需要像强类型语言中那样进行声明,直接写出来直接赋值即可.

  比如可以直接这样 : a = 1

* 在Lua里,是可以对多个变量进行赋值的

  比如这样 : a , b = 1,3 可以同时对a,b进行赋值,相当于a = 1,b = 3

* Lua中在进行赋值的时候,像计算右边的值,再进行赋值.

  也就是如果右边是个表达式,那么就会先将右边的表达式算出来,再赋值给左边的变量,比如 : a,b = 1,2 a,b = b,a 这样就可以完成a,b的值交换.

* Lua中因为可以对多个变量进行赋值,所以呢有这种情况 : 变量个数与赋值个数不等,那么有以下两种策略

  * 当变量个数 > 值个数,那么会将没有值赋予的变量置为nil
  * 当变量个数 < 值个数,那么会将多余的值给忽略

##### Lua的变量

Lua中的变量与python和javascript中的类似,都是无需声明(虽然js中要写个var),写了就用,不需要具体数据类型来声明,想赋值啥就赋值啥.

###### Lua局部变量

在Lua中,如果不写什么修饰的话,那么那个变量就是全局的,跟py和js中一样,它也有个修饰符可以声明变量的作用域.

关键字local来修饰变量就可以限定变量的作用域了,就是限定这个变量在代码块中有效

使用局部变量的好处同其他语言一样,都是可以加速访问与避免命名冲突.

###### Lua代码块

在循环语句,函数体,chunk(变量声明的文件或者字符串)中都是属于代码块的

```lua
--比如for结构
for i = 1,100 do
    --在循环体中就是一个代码块
    local x = nil --这个x就只能在这个for里有效
end
--还有函数体
function fun(a,b)
	--函数体里面也是一个代码块
     local y = 1
end
--如果有几个lua文件,在某一个文件中定义了一个local变量,那么其他文件是不可以访问这个变量的.
```

###### Lua控制语句

* 条件控制语句(也就是if)

  * if 判断条件 then 条件满足要执行的操作 end
  * if 判断条件 then 条件满足要执行的操作 else 条件不满足要执行的操作 end
  * if 判断条件1 then 条件1满足要执行的操作 else if 判断条件2 then 条件2满足要执行的条件 ........... else 上面那些条件都不满足要执行的操作 end

* 循环控制语句(for和while)

  * for的
    * for 变量 = 初始值, 终止值, 步长 do 循环体 end
    * 步长不给的话默认就是1,初始值和终值要自己设置.
    * 泛型for
      * for 键,值 in 表 do 循环体 end
      * 这个键,值名字可以随便取
      * 这个就类似于Java和C++里的增强for循环,for each啥的
  * while的
    * while 判断条件 do 循环体 end
    * repeat 循环体 until 判断条件 (这个就像do while,这里有点不一样,是跟do while相反的,这里until后面的判断条件得是假才会继续执行下一次循环体,如果是真就不会继续循环了)

* break与return

  break主要是在循环里去终止循环的,return就是在函数里进行终止函数并且返回东西的,虽然也可以不返回什么东西

##### Lua函数

###### 函数定义

* function 函数名(参数列表) 函数体 end
* 函数名 = function(参数列表) 函数体 end

这两个方式跟js里的函数定义简直一毛一样有木有

* 变量名 = {} 变量名.函数名 = function(参数列表) 函数体 end
* 变量名 = {函数名 = function(参数列表) 函数体 end ....}

这种方式可以是因为function在Lua里面是一种数据类型,它可以作为函数参数,表的内容等等.

* 变量名 = {} function 变量名.函数名(参数列表) 函数体 end

* 对于函数的参数列表,我们可以使用可变参数

  * function 变量名.函数名(...) 函数体 end 这个方式等价于下面这个
  * function 变量名.函数名(arg = {...,n = 参数数量}) 函数体 end
  * 这个arg是使用了可变参数的函数的参数列表里面默认存在的表,而且这个arg表里面有一个键n,它的值就是参数的个数.除了通过这个n参数来获取参数的个数,也可也通过ipairs(表名)这个函数来获取arg表中的参数个数.

* 闭包(在函数里面定义的函数就称为闭包)的函数定义

  function 函数名(参数列表) 函数体 return function(参数列表) 函数体 end end

  ```lua
  function a()
      local i = 0
      return function()
          i = i + 1
          return i
      end
  end
  c1 = a()
  print(c1())--输出1
  print(c1())--输出2
  print(c1())--输出3
  --为什么会是1,2,3呢?
  --因为我们调用的是闭包,而不是外部的函数,这个i = 0是不会被多次调用的,因为它只在c1 = a()这一步进行了一次赋值为0的操作,后面都是在调用返回来的那个闭包,通过调用这个闭包,改变了i的值,但是没让它重新被外面的函数给赋值成0,所以i会递增.如果后面再调用一次这个外部函数,那这个i就会变回0了.
  ```

  **需要注意的是,Lua中函数的返回值是可以返回多个的**

###### 函数调用

* 一般的函数调用方式 : 函数名(参数列表)
  * 如果参数只有一个的话(一个值,一个表啊一个字符串这样的),可以不写这个括号,比如print()函数,我们平时都这样写 : print("aa"),其实也可以这样 : print "aa".这样是跟前面一样的
  
* 如果函数是表的一个值的话,可以这样调用

  ```lua
  tab = {}
  function tab.fun() ...... end
  tab.fun() --调用表里面的函数
  tab:fun() --等价于tab.fun(tab)
  ```

* 闭包的调用

  因为闭包返回的是一个函数,所以接收闭包的那个变量加一个()就是在调用闭包

* 函数调用时实参和形参个数不等

  跟赋值的时候一样,多余的参数会被忽略,不够的话用nil补

* 尾调用(也就是一个函数的最后一个动作是调用另一个函数,必须是在最后一步是调用函数)

###### 第一类值

Lua中的function类型的东西,也就是函数,是属于第一类值的,它可以被赋值给变量或者作为形参传入函数的形参.

```lua
tab = {1,2,3,5,6,81,1,3,4,2}
function compare(a,b) 
    return a-b > 0 
end
table.sort(tab,compare)--函数compare作为了参数传入了内置的函数sort中.这个函数是给表进行排序的

function a(tab)
    local sum = 0
    for k,v in ipairs(tab) do
        sum = sum + v
    end
    return sum
end

function b(tab)
    local sum = 1
    for k,v in ipairs(tab) do
        sum = sum * v
    end
    return sum
end

function getval(f,t)
    return f(t)
end

print(getval(sum,{1,2,3,4,5}))--将函数sum作为了函数getval的参数传入
```



##### Lua迭代器与泛型for

前面说for循环的时候,我们直到for对于表有一种特别的遍历方式叫泛型for,也就是:

for k,v in ipairs(表) do 循环体 end

这个泛型for到底是一个怎样的执行流程,它到底是怎么将表中的数据遍历出来的嘞?

泛型for在官网上是这样说的 : for 变量1,....变量n in 表达式列表 do 循环体 end

而它等价于:

```lua

for 变量1,....变量n in 表达式列表 do 循环体 end
--上面的与下面的等价
do
    local _f,_s,变量1 = 表达式列表 --把表达式列表的值赋值给前面三个变量
    local 变量2......变量n
    while true do
        变量1,....,变量n = _f(_s,变量1) --调用_f函数,说明表达式的第一个返回值是一个函数,然后把_f()函数计算的结果赋值给前面那些变量,这里的变量1会作为上一次的返回值也作为这次循环调用_f()的参数.
        if 变量1 == nil then break end --判断当前的变量1(经过了_f()调用的变量1是否为空,是空就退出循环
        循环体
    end
end
```

我们在这个表达式列表上一般都会用iparis(表名)这个函数,那这个iparis函数是干啥的呢?

在官方文档这么说ipairs : 它返回一个迭代函数,一个表,以及一个0,一共三个返回值.那么这个迭代函数是啥嘞?

```c
//在调用iparis的时候,实际调用的时候,是会执行它源代码中的luaB_iparis()这个函数,这个函数是在它的源码文件中的lbaselib.c中的.
//迭代函数就是这个C函数.也就是它自己
//除了在C函数里的这个迭代函数,我们其实也可以在Lua中写一个具有类似功能的函数
```

```lua
function ipairs1(tab)
    return iparis_iter,tab,0
end

function ipairs_iter(t,i)
    i = i + 1
    if t[i] ~= nil then
        return i,t[i]
    end
end

tab = {"12","31"}
for k,v in ipairs1(tab) do
    print(v)
end
--这样也可以实现ipairs一样的功能.
--那么这个ipairs_iter(t,i)函数就是我们的迭代函数.
--因为返回的是函数,所以我们其实是可以用闭包来写的.
```

##### Lua协程

进程: 计算机中正在运行的程序实例

线程: 进程内一个相对独立的,可调度的执行单元,是系统独立调度和CPU资源调度的最基本单元.

协程: 协作程序.协程之间通过协作(函数调用)来完成一个既定的任务

协程与多线程的区别 : 协程本质上是函数的调用,它其实还是一个单线程的,而多线程是可以根据CPU的核数实现真正的并行运行.

###### Lua中的协程相关函数

* coroutine.create(函数名) : 创建协程,它的返回值就是协程
* coroutine.wrap(函数名) : 创建协程,
* coroutine.status(协程) : 查看协程状态
* coroutine.resume(协程,var1....) : 执行协程,如果是第一次执行协程,那么将运行函数体,参数将会传入到协程对应的函数体中
* coroutine.yield(var1,....) : 暂停协程,返回到调用协程的地方继续执行,并返回这个yield函数的参数列表里的参数.

##### Lua的表与数据结构

在Lua中,我们好像就只见过表这种数据结构,那么如何用其他类型的数据结构呢?

Lua中的表是以哈希结构来存储数据的,也就是键值对的形式.

###### 数组表示

Lua的表虽然是键值对形式,但如果我们不给键的话,那么就会默认以1开始作为键值,这个时候就是一个数组了.

多维数组的话就是不给键,然后值是表就完事了.

###### 链表表示

键表示前一个表,值表示当前的值,这样的表就是链表了:

```lua
list = nil
list = {next = list,value = 1}
list = {next = list,value = 2}
--这样这个list就是一个有两个节点的链表了
--一般我们还要遍历链表,我们就可以写迭代函数,然后用泛型for来遍历了.
function ipairs_list(t)
	return ipairs_iter,t,nil
end

function ipairs_iter(t,node)
	if node = nil then 
        return t
     else
        return node.next
     end
end
--一般我们还想删除链表里的元素
function delnode(tab,val)
	--先找到要删的
    for node in ipairs_list(tab) do
        if node.next.value == val && node.next ~= nil then
            --当前节点的下一个节点是要删掉的
            local nextnode = node.next --保存要删除的节点
            node.next = nextnode.next --当前节点指向要删除节点的下一个节点
            nextnode.next = nil --把要删除的节点的next置为nil,删除完成
        end
     end    
end
```

##### Lua元表

每个表和userdata对象在Lua肿都拥有元表,元表实际上还是一个普通的表,这个表定义了表和userdata在特定情况下的一些行为.对于这些行为,我们需要定义元数据,元数据的类型是函数,比如我们需要让表完成相加操作的话,我们就得定义表的__add这个元数据,它的规范在官方文档中有解释:

```txt
__add: the addition () operation. If any operand for an addition is not a number, Lua will try to call a metamethod. It starts by checking the first operand (even if it is a number); if that operand does not define a metamethod for , then Lua will check the second operand. If Lua can find a metamethod, it calls the metamethod with the two operands as arguments, and the result of the call (adjusted to one value) is the result of the operation. Otherwise, if no metamethod is found, Lua raises an error. +__add
__sub: the subtraction () operation. Behavior similar to the addition operation. -
__mul: the multiplication () operation. Behavior similar to the addition operation. *
__div: the division () operation. Behavior similar to the addition operation. /
__mod: the modulo () operation. Behavior similar to the addition operation. %
__pow: the exponentiation () operation. Behavior similar to the addition operation. ^
__unm: the negation (unary ) operation. Behavior similar to the addition operation. -
__idiv: the floor division () operation. Behavior similar to the addition operation. //
__band: the bitwise AND () operation. Behavior similar to the addition operation, except that Lua will try a metamethod if any operand is neither an integer nor a float coercible to an integer (see §3.4.3). &
__bor: the bitwise OR () operation. Behavior similar to the bitwise AND operation. |
__bxor: the bitwise exclusive OR (binary ) operation. Behavior similar to the bitwise AND operation. ~
__bnot: the bitwise NOT (unary ) operation. Behavior similar to the bitwise AND operation. ~
__shl: the bitwise left shift () operation. Behavior similar to the bitwise AND operation. <<
__shr: the bitwise right shift () operation. Behavior similar to the bitwise AND operation. >>
__concat: the concatenation () operation. Behavior similar to the addition operation, except that Lua will try a metamethod if any operand is neither a string nor a number (which is always coercible to a string). ..
__len: the length () operation. If the object is not a string, Lua will try its metamethod. If there is a metamethod, Lua calls it with the object as argument, and the result of the call (always adjusted to one value) is the result of the operation. If there is no metamethod but the object is a table, then Lua uses the table length operation (see §3.4.7). Otherwise, Lua raises an error. #
__eq: the equal () operation. Behavior similar to the addition operation, except that Lua will try a metamethod only when the values being compared are either both tables or both full userdata and they are not primitively equal. The result of the call is always converted to a boolean. ==
__lt: the less than () operation. Behavior similar to the addition operation, except that Lua will try a metamethod only when the values being compared are neither both numbers nor both strings. Moreover, the result of the call is always converted to a boolean. <
__le: the less equal () operation. Behavior similar to the less than operation. <=
__index: The indexing access operation . This event happens when is not a table or when is not present in . The metavalue is looked up in the metatable of . table[key]tablekeytabletable
The metavalue for this event can be either a function, a table, or any value with an metavalue. If it is a function, it is called with and as arguments, and the result of the call (adjusted to one value) is the result of the operation. Otherwise, the final result is the result of indexing this metavalue with . This indexing is regular, not raw, and therefore can trigger another metavalue. __indextablekeykey__index

__newindex: The indexing assignment . Like the index event, this event happens when is not a table or when is not present in . The metavalue is looked up in the metatable of . table[key] = valuetablekeytabletable
Like with indexing, the metavalue for this event can be either a function, a table, or any value with an metavalue. If it is a function, it is called with , , and as arguments. Otherwise, Lua repeats the indexing assignment over this metavalue with the same key and value. This assignment is regular, not raw, and therefore can trigger another metavalue. __newindextablekeyvalue__newindex

Whenever a metavalue is invoked, Lua does not perform the primitive assignment. If needed, the metamethod itself can call rawset to do the assignment. __newindex

__call: The call operation . This event happens when Lua tries to call a non-function value (that is, is not a function). The metamethod is looked up in . If present, the metamethod is called with as its first argument, followed by the arguments of the original call (). All results of the call are the results of the operation. This is the only metamethod that allows multiple results. func(args)funcfuncfuncargs
```

比如这样:

```lua
a = {1,2,3}
b = {4,5,6}
mt = {}
mt.__add = function(a,b)
        local len = table.getn(a);--a表的长度
        local res = {}
        for i = 1,len do
            res[i] = a[i] + b[i];
            end
        return res;
        end
setmetatable(a,mt);--设置元表,a的元表设置为mt
setmetatable(b,mt);
c = a + b --在元表里有__add,所以可以进行+操作.类似于C++的运算符重载.
for k,v in ipairs(c) do
    print(k,v)
    end
```

对于其他的元数据以及行为可以参照官方文档.



##### Lua环境

Lua它本身其实也是一个表,这个表叫_G,我们是可以打印和添加以及操作这个表里的东西的.我们在进行变量赋值(全局变量)的时候其实就是在向这个表中加数据.这个表 : _G也称作环境表.我们可以在任意地方使用它.

这个_G是可以代替local这个关键字的,我们给这个表设置一个元表,元表中用一个__newindex元数据,写好它的处理机制,也就是当我们用一个全局变量的时候(一般不小心在函数里用了),其实就是在往这个环境表里去拿东西和存东西,如果这个全局变量是会引起报错的.用这种方式就可以防止我们忘记写local的问题.

除了上面那种方法,我们还可以通过Lua提供的函数 : setfenv(num,table) 来给函数设置一个环境,我们可以在函数里使用,如果我们在一个函数里写一个这个setfenv(1,{}),的话,就是给这个函数设置了一个环境表,并且是一个空表.此时这个函数只能使用这个环境表的东西,我们还可以给这个环境表设置一个元表,并且这个元表的__index为全局环境表,可以这样 : setmetatable(环境表,{\_\_index = _G}),然后在函数里使用设置环境表函数,就可以不怕没加上local而导致的全局变量错误了.

##### Lua包(package)

首先我们看看Lua提供的两个函数

* require(packagename) 

  这个函数的执行流程:

  * 在package.loaded表中查找我们指定的packagename

    这个loaded表里面存的是一堆表,它保存的就是string,debug,package,_G,io,os,table,math,coroutine这些表.

  * 如果还没找到就去package.preload去找,如果找到了就把它作为loader,调用loader(L)

    这个preload里面又是啥嘞,其实是一些文件的路径

  * 如果没找到就根据package.path来查找lua文件

    这个path(它是一个字符串)文件是一堆路径,如果能找到这个lua文件,就会执行它,如果这个文件最后有return,就能得到这个文件返回的东西,并且会修改package.loaded这个表里对应名称的东西.否则就会返回true,如果找不到就是返回false.

  * 还没找到就根据package.cpath来查找c库,并调用相应名字的接口

* module()

##### Lua面向对象

在Lua里,面向对象是通过table实现的

###### 对象和类的表示

```Lua
--可以这么表示一个对象:
p1 = {name = "a",age = 12}
--可以这么表示一个类:
ClassA = {name = "default",age = 10,}
function ClassA.funA()
    print("a");
end
function ClassA.funB()
    print("b");
end
--通过类生成对象:
--手写new函数,它表示如果传入一个nil的话就返回一个空表.
function ClassA.new(o)
    o = o or {};
    --可以通过元表来实现通过对象访问类的属性.
    setmetatable(o,ClassA);
    ClassA.__index = ClassA;
    return o;
end
--还可以这么写避免访问全局的表
function ClassA:new(o)
    o = o or {};
    setmetatable(o,ClassA);
    self.__index = self;--默认会把自己作为第一个参数传入,这个self就是第一个参数.
    return o;
end
--使用:
local p1 = ClassA.new();
p1.funA();
local p2 = ClassA.new({name="asda",age=12131});
p2.funB();
print(p2.name);
--调用的时候也可以用冒号的
local p3 = ClassA:new({name="asdasda",age=123});
```



###### 继承

```Lua
--以上面的ClassA为例,现在要让一个ClassB继承它
ClassB = {bfiled = "default"};
function ClassB:new(o)
    o = o or {};
    setmetatable(o,self);
    self.__index = self;
    setmetatable(self,ClassA);--设置这个表的元表是父类就行.
    ClassA.__index = ClassA;
   	return o;
end
```



###### 重载

```Lua
--在当前类实现跟父类中的同名方法的话就是重载了.
```



##### Lua弱表

弱表是为了实现这样的需求:我们想引用一个表,但是不想增加它的引用计数,也就是不想让增加一个强引用对象.

弱表是一个表,它拥有元表,而且元表定义了__mode字段.弱表中的引用是弱引用,弱引用不会导致对象的引用计数变化,也就是当一个对象只有弱引用指向它,那这个对象在gc的时候是会被回收掉的.

__mode字段可以取一下三个值:key,value,kv,key就是表的key,是弱表的.也就是表的键能够被自动gc,value表示表的值是弱表的,也就是表中的值可以被自动gc,kv就是二者的组合.任意情况下,只要key和value中任意一个被gc了,那这个键值对就从表中被移除了.

使用:

```Lua
table1 = {k = "asda"};
setmetatable(table1,{__mode = "k"});--设置这个表的键为弱引用,这样table1就是一个弱表了.
```

* 这里提一提Lua的垃圾回收机制 : 它的垃圾回收机制有自动回收和手动回收两种,自动就是它自己回收,由虚拟机决定哪些被回收.手动就是可以使用一个函数:collectgarbage来主动回收垃圾.

  ```Lua
  collectgarbage();--这样就可以直接回收当前环境中的辣鸡了.它只会回收引用计数为0的
  ```

  

##### Lua标准库

[Lua 5.4 Reference Manual](https://www.lua.org/manual/5.4/manual.html#6)

* 基本函数 : 具体看官方文档.![lua库](D:\C++学习笔记\pictures\lua库.PNG)

  

* 协程库

* string库

* table库

* 数学库

* IO库

* 操作系统

* 调试库

##### Lua的C程序API

Lua这种脚本语言就是给应用程序进行扩展的.它主要就是通过Lua提供的C语言API进行调用的.

在官方文档的4 – The Application Program Interface中有说明.

在调用API方法前,需要调用这个lua_open函数,它的原型:

```C
lua_State *lua_open(void);
```

在调用完API方法后,需要调用lua_close函数,它的原型:

```c
void lua_close(lua_State *L);
```

比如在C++中调用Lua:

```C++
//因为是在C++去调用C,得这样:而且还得将lua源代码加入一起编译.
extern "C"{
    #include <lua.h>
	#include <luaxlib.h>
	#include <lualib.h>
}
int main(){
    lua_State *luaState = lua_open();
    
    lua_close(luaState);
}
```

Lua和C的通信方式是通过堆栈进行的.在这个栈里面,Lua的数据有两种编号方式,一种是正数编号,一种是负数编号.正数就是栈底到栈顶为1~n,负数就是栈顶到栈底为-1~-n.

在官方文档的4.6 – Functions and Types中提供了所有的C函数.我们常用的就是栈操作(push元素,查询元素,获取指定位置的值等).lua_pushxxxx这样的函数就是在C中push元素到lua里,lua_type函数可以获取指定位置的元素,lua_isxxx可以判断某个元素是否是某个类型.lua_toxxx这种函数可以将某个位置的元素转换为某种类型.还留有一些设置栈顶啊,弹出元素啊,删除元素啊,插入元素啊,替换元素啊等等操作.具体看官方文档嗷.

* 应用程序中Lua代码的编译 : 通过两个函数 : luaL_loadfile和luaL_loadBuffer.它俩的原型:

  ```c
  luaL_loadfile(lua_State *L,const char* filename);//第二个参数可以是lua字节码文件或lua源代码文件.如果给的是源文件,那么它会先进行操作成lua字节码后返回函数.
  luaL_loadBuffer(lua_State *L,const char* buffer,int size);//输入字符串,然后会把它变成字节码.
  ```

* lua字节码的执行可以通过两个函数 : lua_call和 int lua_pcall,它俩的原型:

  ```c
  lua_cal(lua_State *L,int nargs,int nresults);//这个函数如果出错了,就会直接报错,程序寄
  lua_pcall(lua_State* L,int nargs,int nresults,int errfunc);//这个函数它可以指定出错后执行的函数,它自己也有返回值,如果它返回0,就说明它执行成功
  ```

* 还可以编译和执行放在一起.就用这个函数:luaL_dofile,或者luaL_dostring,它们的原型:

  ```c
  int luaL_dofile (lua_State *L, const char *filename);
  int luaL_dostring (lua_State *L, const char *str);
  ```

  

##### C程序中嵌入Lua

在C/C++程序中如何去访问Lua的全局变量嘞:首先要通过lua_getglobal函数将Lua的全局变量入栈.然后将元素转换成相应类型(lua_toxxxx这些函数),C/C++程序中就可以使用了.

```c
lua_getglobal(lua_State* L,const char* valname);//第二个参数就是lua文件/程序中变量的名字.
```

在对堆栈操作完成后,需要恢复堆栈状态.也就是把这个变量弹出.

那怎么访问table里的元素嘞 : 首先要将table变量入栈,跟上面那个函数一样,然后将要访问的元素的key入栈(lua_pushxxxx,key是什么类型的就push什么),调用lua_gettable将key对应的value出栈,将堆栈对应的元素转换成相应的类型就可以使用了.最后也需要将值和table弹出.

```c
lua_gettable(lua_State* L,int index);//第二个参数是table在堆栈中的位置
```

那怎么访问lua的函数嘞 : 将lua函数入栈(用lua_getglobal),然后将函数的参数入栈,然后调用lua_pcall函数将函数的返回结果入栈,将堆栈对应的元素转换成相应的类型,就可以用了.最后也需要把这些东东都弹出栈.

```lua
window = {width = 10,height = 20};
function get()
    return window.width,window.height;
end

function add(a,b)
    return a+b;
end
```



```cpp
int main(){
    lua_State* L = lua_open();
    luaopen_base(L);
    lua_settop(L,0);
    lua_dofile(L,"lua文件路径");
    lua_getglobal(L,"get");//函数入栈
    lua_pcall(L,0,2,0);//第二个参数是参数个数,第三个参数是返回值个数,第4给参数是错误处理
    int width = lua_tonumber(L,-1);//转换成对应类型
    int height = lua_tonumber(L,-2);
    lua_pop(L,-1);//返回值出栈
    lua_pop(L,-1);//两个返回值,出两次
    
    lua_getglobal(L,"add");
    lua_pushnumber(L,100);
    lua_pushnumber(L,200);
    lua_pcall(L,2,1,0);
    int sum = lua_tonumber(L,-2);
    lua_pop(L,-1);//只需要弹出返回值
    
}
```



##### Lua调用C程序函数

Lua调用C变量和函数也差不多是一个道理,就是在Lua中用相应的API函数将C变量入栈(用lua_pushxxx),在C/C++中需要将函数用lua_setglobal函数将要被Lua调用的函数进行注册.用完后也要出栈.

```cpp
//在C程序里面:
int main(){
    lua_State* L = lua_open();
    luaopen_base(L);
    lua_settop(L,0);
    lua_dofile(L,"lua文件路径");
    int a = 100;
    lua_pushnumber(L,a);//C++程序中的变量入栈
    lua_setglobal(L,"a");//注册变量a
    
    lua_dofile(L,"lua文件路径");
    
}
```

```lua
--这个lua文件就是上面lua文件路径指定的lua文件.
print(a);--此时可以输出100,而不是nil.因为C程序里面的变量a已经注册进来了.
```

```cpp
//老是创建变量很麻烦,我们可以直接创建一个表
int main(){
    lua_State* L = lua_open();
    luaopen_base(L);
    lua_settop(L,0);
    lua_dofile(L,"lua文件路径");
    
    lua_newtable(L);//在堆栈里建立一个表
    lua_pushstring(L,"width");//入栈键值对.-2
    lua_pushnumber(L,100);//-1
    lua_settable(L,-3);//设置表的属性,它是根据表所在的位置来设置的.要在键值对入栈后才能设置表
}
```

```cpp
//Lua里调用Cpp程序的函数
int width = 100000;
int show(lua_State* L){//lua_pushcfunction的第二个参数要求是一个函数指针,而且它要求有一个lua_State*类型的参数,而且必须有int返回值,这个返回值其实就是我们调用这个函数的返回结果,而且是指定了返回值的个数的.
    lua_pushnumber(L,width);//将想要返回给lua的结果入栈
    return 1;
}
int show1(lua_State* L){
    int a = lua_tonumber(L,1);//如果lua里调用传入了参数,可以直接拿出来用.
    lua_pushnumber(L,a + 121212);
    return 1;
}
int mian(){
    lua_State* L = lua_open();
    luaopen_base(L);
    lua_settop(L,0);
    lua_dofile(L,"lua文件路径");
    
    lua_pushcfunction(L,show);//将函数入栈
    lua_setglobal(L,"show");//注册函数
    
    lua_pushcfunction(L,show1);
    lua_setglobal(L,"show1");
}
```

```lua
--调用上面的C函数
print(show());
print(show1(1));
```

除了可以直接调用C程序里的函数,在C程序里还有一个lua_openlib函数,它的原型:

```c
lua_openlib(lua_State* L,const char* libname,luaL_reg* l,int nup);
//第二个参数就是库的名字,第三个参数其实就是一个数组,它里面都是要注册的函数名字和对应的函数,第四个参数
//用法:首先要有这个库的数组:
static const luaL_reg arrays[] = {
    {"fun1",show},//就是上面那个show函数
    {NULL,NULL}
}
int main(){
	lua_State* L = lua_open();
    luaopen_base(L);
    lua_settop(L,0);
    lua_dofile(L,"lua文件路径");
    
    lua_openlib(L,"arrays",arrays,0);
}
```

```lua
--使用上面注册的show()
print(fun1());--要用arrays里面函数对应的名字来调用.一般都和函数名一样,这里不一样是显得明显一点
```



# Lua源码解析

## Lua源码结构

以Lua5.2.1为例.Lua的源代码包括以下四个结构:

**1. 虚拟机运转的核心功能**

- **lapi.c** Lua API。实现大量的Lua C API（lua_ *函数）。
- **lctype.c** 标准库中ctype相关实现
- **ldebug.c** 调试接口。
- **ldo.c** Lua的堆栈和调用结构。处理函数调用（luaD_call / luaD_pcall），扩展堆栈，协程处理，...
- **lfunc.c** 函数原型及闭包管理
- **lgc.c** 垃圾回收
- **lmem.c** 内存管理接口【luaM_realloc / luaM_growaux_】
- **lobject.c** 对象操作的一些函数。包括数据类型<->字符串转换，原始相等性测试（luaO_rawequalObj）和日志基础2（luaO_log2）
- **lopcodes.c** 虚拟机的字节码定义
- **lstate.c** 全局状态机。包括用于打开和关闭Lua状态（lua_newstate / lua_close）和线程（luaE_newthread / luaE_freethread）的函数。
- **lstring.c** 字符串池
- **ltable.c** 表类型的相关操作。Lua表（哈希）
- **ltm.c** 标记方法。实现从对象访问元方法。
- **lvm.c** 虚拟机。执行字节码（luaV_execute）。还公开了lapi.c使用的一些功能（例如luaV_concat）。
- **lzio.c** 通用的缓冲输入流接口

**2. 源代码解析以及预编译字节码**

- **lcode.c** Lua的代码生成器。由lparser.c使用
- **ldump.c** 保存预编译的Lua块。实现luaU_dump，将功能对象转储为预编译的块字符串。
- **llex.c** 词法分析器。由lparser.c使用。
- **lparser.c** 解析器
- **lundump.c** 加载预编译的Lua块

**3. 内嵌库**

- **lauxlib.c** 库编写用到的辅助函数库
- **lbaselib.c** 基础库
- **lbitlib.c** 位操作库
- **lcorolib.c** 协程库
- **ldblib.c** Debug库
- **linit.c** 内嵌库的初始化
- **liolib.c** IO 库
- **lmathlib.c** 数学库
- **loadlib.c** 动态扩展库管理
- **loslib.c** OS 库
- **lstrlib.c** 字符串库
- **ltablib.c** 表处理库

**4. 可执行的解析器，字节码编译器**

- **lua.c** Lua独立解释器
- **luac.c** Lua编译器（将字节码保存到文件中；还列出字节码）

## Lua源码的编码约定

外部符号的前缀指示其来自的模块：

```text
luaA_-lapi.c
luaB_-lbaselib.c
luaC_-lgc.c 垃圾回收部分
luaD_-ldo.c 函数的运行流程：函数调用及返回
luaE_-lstate.c 虚拟机的当前状态
luaF_-lfunc.c function实现
luaG_-ldebug.c 
luaH_-ltable.c table实现
luaI_-lauxlib.c
luaK_-lcode.c
luaL_-lauxlib.c / h，linit.c（公共函数）
luaM_-lmem.c 内存管理
luaO_-lobject.c 不同的数据类型
luaP_-lopcodes.c 虚拟机的行为是由一组 opcode 控制的
luaS_-lstring.c string实现
luaT_-ltm.c 元表 
luaU_-lundump.c
luaV_-lvm.c 虚拟机对 opcode 的解析和运作
luaX_-llex.c
luaY_-lparser.c
luaZ_-lzio.c 带缓冲的流处理
lua_-lapi.c / h + luaconf.h，debug.c
luai_-luaconf.h
luaopen_-luaconf.h +库（lbaselib.c，ldblib.c，liolib.c，lmathlib.c，
                                  loadlib.c，loslib.c，lstrlib.c，ltablib.c）
```

## 阅读源代码的次序

- 首先、阅读外围的库是如何实现功能扩展的，
- 然后、阅读 Lua 的具体实现。
- 之后、可以开始了解 Lua VM 的实现。
- 接下来就是分别理解函数调用、返回，string，metatable，table实现
- debug模块是一个额外的设施、
- 最后是parse 等等编译相关的部分。
- 垃圾收集将是最难的部分，可能会花掉最多的时间去理解细节。[Lua GC 的源码剖析](https://link.zhihu.com/?target=https%3A//blog.codingnow.com/2011/04/lua_gc_multithreading.html)
