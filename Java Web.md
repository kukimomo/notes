# Java Web部分

## Maven

在web开发中，我们需要使用大量的jar包，而且需要手动添加，需要一个工具自动帮我们导入和配置这些jar包，这个工具就是Maven。

Maven是一个架构管理工具，它可以管理项目的架构，就是用来导入和配置jar包的，它有一个核心的思想:约定大于配置，它规定了我们该如何编写JAVA，必须按照这个规范写。

Maven的高级之处就在于它可以导入jar包所依赖的其它jar包

不过Maven也有可能会导致资源项目无法导出，我们可以在pom.xml文件中进行配置，写下如下的东东，避免该问题

 

```xml
 <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```



## HTML部分

HTML（Hyper Text Markup Language），超文本标记语言。HTML通过标签来标记要显示的网页中的各个部分，网页文件本身是一种文本文件，通过在文本文件中添加标记符，可以告诉浏览器如何显示其中的内容。

创建HEML工程

* 在IDEA中新建工程，选择Static Web项目，创建静态Web工程，工程建立后就可以新建HTML文件进行编辑了。

* HTML文件的书写规范

  * 可以使用<!--注释内容-->来注释

  * HTML文件中的<!DOCTYPE html>表示声明

  * <html lang = "en">表示标签，表明html的开始。lang = "en"表示英文

  * HTML标签一般分为两部分，即<head>标签和<body>标签

  * <head>标签表示头部信息，一般包含三内容，title标签，css样式，js代码

在<head>标签中，可以使用<meta charset>标签来设置使用的字符表，一般使用UTF-8字符表

在<head>标签中，可以使用<title>标签设置标题

```HTML
<html>                      表示html页面的开始
    <head>                  头信息
        <title>标题</title>  标题
    </head>              
    <body>                  页面主题内容的开始
        页面主题内容
    </body>
</html>                      整个html页面的结束
```

* HTML的标签

  * 标签格式：<标签名>封装的数据</标签名>

  * 标签明大小写不敏感

  * 标签拥有自己的属性，分为基本属性和事件属性

    * 基本属性可以控制基本的样式效果
    * 事件属性可以设置事件响应

  * 标签又分为单标签和双标签，单标签的格式：<标签名   />

    ​                                                    双标签的格式：<标签名>封装的数据</标签名>

  * 标签的语法

    * 标签不可以交叉嵌套，要有始有终。
    * 标签必须正确关闭，即要有结束标签。
    * 属性必须要有值，属性值必须加引号
    * 注释不可以嵌套

  * 常用的标签（HTML的文档库：https://www.w3school.com.cn/tags/index.asp）

    * <fout>，该标签可设置文本的字体，字体尺寸，字体颜色，其可选的属性有三种
      * color，该属性可以设置颜色，属性值可以是颜色名称或者rgb值
      * face，该属性可以设置字体，属性值为字体名称
      * size，该属性可以设置字体大小，属性值为1-7

  例：

  ```HTML
  <fout color = "red" face = "宋体" size = "7">字体</fout>
  可以将"字体"两字设置成大小为7，字体为宋体的红色字符
  ```

  * 特殊字符："<"字符的代码为  &lt

    ​                    ">"字符的代码为  &gt

    ​                    空格（在html中连续的空格会被裁掉只剩一个）的代码为   &nbsp

  * 标题标签：如<h1></h1>，1表示标题的优先级，1表示最高级，数字越大优先级越低，标题只有标题1到标题6，6以上的无法识别

    * 标签的属性
      * align，该属性可以设置对齐，其属性值可以是left,right,center，表示左右中对齐

  * 超链接标签：<a></a>

    * 超链接属性
      * href，该属性可以设置超链接对应的地址，值是要跳转的地址
      * target，该属性可以设置目标跳转，其值为 _self  或 _blank, 或者其它HTML界面的名称和iframe窗口的名称，_self表示从新窗口打开连接， _blank表示从当前窗口打开连接
    
  * 无序列表：<ul></ul>

    * 其中的内容用<li></li>标签指定
    * 可用type属性修改列表项前面的符号，值可设为none表示没有符号

  * img标签：可在HTML页面上显示图片，<img></img>

    * 可用src属性指定要显示图片的路径，路径又有 相对路径和绝对路径

      * 相对路径

        * .   表示当前文件所在目录
        * ..  表示当前文件所在的上一级目录

        * 文件名    也可也写作 ./文件名./     表示当前文件所在目录的文件

      * 绝对路径：http://ip:port/工程名/资源路径

    * 可用width属性设置图片宽度，属性值为具体数值

    * 可用hight属性设置图片高度，属性值为具体数值

    * 可用border属性设置图片边框，属性值为具体数值

    * 可用alt属性设置当指定路径找不到时，用来代替显示的内容，属性值为字符串

  * 表格标签：table

    * 可用longer,width,hight三个属性来指定表格长宽高
    * 可用cellspacing属性来设置单元格间距，其属性值为具体数值

    * 行用<tr></tr>标签指定，其中是单元格
    * 表头用<th></th>标签指定

    * 单元格用<td></td>标签指定，其中是单元格内容

  * 跨行跨列表格：

    * 可用colspan属性设置跨行，值为具体数值
    * 可用rowspan属性设置跨列，值为具体数值

  * 内嵌窗口标签：iframe

    * iframe标签可和a标签一起使用，可将想打开的HTML界面打开到iframe窗口中，其使用方法如下：
      * 在iframe标签中使用name属性定义名称
      * 在a标签的target属性中设置iframe的name的值

  * 表单标签：<form></form>,这是用来收集用户数据并发送到服务器的东东

    * 其中可用<input/>标签设置输入框，
      * 可使用其type属性设置输入框的类型，属性值为类型名称
    * 可用<select></select>标签设置下拉列表框
    * 可用<textarea></textarea>标签设置多行文本输入框
    * 一般表单是与表格一起用的

  * 表单提交

    * 在form标签中设置action属性可用设置提交表单的服务器地址
    * 在form标签中设置method设置表单提交的方式，其属性值为get或者post
      * get请求的特点：
        * 浏览器地址栏的内容是：action属性[+分隔符+请求参数]
        * 安全性低，会把信息显示在请求参数上
        * 有数据长度的限制
      * post请求的特点：
        * 浏览器地址栏的内容只有action的属性值
        * 比get安全
        * 理论上没有数据长度的限制
    * 表单无法正确提交给服务器的时候的三种情况
      * 表单项没有name属性，请求参数会缺少对应的表单项，故想要发送完整的表单，每个表单项都要设置name属性
      * 单选，复选和下拉列表标签中要写上value属性和option属性
      * 表单项要写在提交项的form标签中

  * 其它标签：<div></div>，<span></span>,<p></p>

    * div标签默认占一行,span标签的长度与内容相同，p标签的上方或下方会空出一行


## CSS部分

CSS是层叠样式表单，是用于增强控制网页样式并允许将样式信息与网页内容分离的一种标记性语言

* CSS的语法规则：               选择器{属性:属性值；}
  * 选择器：浏览器根据选择器决定受CSS样式影响的HTML标签
  * 属性：要改名的样式名，并且每个属性都有一个值，属性和值用冒号分隔，并由大括号包围，这样就组成了一个完整的样式声明
  * 多个声明：若要定义不止一个声明，则需要用分号将每个声明分开，最后一条声明可不加分号，不过还是推荐加上分号，一般一行只描述一个属性
  * CSS的注释：/* 注释内容 */
* CSS与HTML的结合方式
  * 在标签的style属性中设置“key:value value"，即“属性:键值对”来修改标签样式
    * 该方法在标签多的时候代码量会变得非常庞大
    * 可读性差
    * 代码多重复用
  * 在head标签中，使用style标签来定义需要的CSS样式，选择type属性的属性值为”text/css“就可用定义CSS样式了
    * 只能在同一页面内复用代码
    * 维护不方便，不能同时更改大量页面
  * 将CSS样式单独做为一个文件，给需要用的页面引用CSS文件
    * 在HTML文件中可使用<link/>标签来引用CSS文件，在其中用<href>标签来引用需要的CSS文件
  * 标签名选择器：标签名{属性:属性值}
    * 标签名选择器可决定哪些标签被动的使用这些样式
  * id选择器：#id 属性值{属性:属性值}
    * 该选择器可同通过id属性选择性的去使用样式
  * 类选择器：.class 属性值{属性:属性值}
    * 该选择器可通过calss属性有效的选择性的去使用样式
  * 组合选择器：选择器1，选择器2，......，选择器n{属性:属性值}
    * 该选择器可用让多个选择器共用一套CSS样式
  * 常用的样式属性
    * 字体颜色：color，值可以是rgb值，颜色值，颜色名称
    * 宽度，高度：width，highth，值为具体数值
    * 边框：”border，属性值为线宽值，类型，颜色
    * 背景：background
      * background-color可设置背景颜色，值为颜色
    * 字体大小：font-size，值为具体值
    * margin：对齐
      * margin-left，magrin-right：外边框，值设为auto
    * 文本位置：text-align，值为位置，如center
    * 超链接去下划线：text-decoration，值设为none可去下划线
    * 表格边框细线合并：border-collapse，值设为collapse可合并边框
    * 列表去除修饰：list-style，值设为none可去除列表修饰

## Java Script部分

java script语言是为了完成页面的数据验证，它运行在客户端，需要运行浏览器来解析执行，相较于JAVA，JS是弱类型（变量类型可变），而JAVA是强类型（变量类型不可变），Java Script常用olert()方法来弹窗输出

Java Script的特点：

* 交互性（能够完成信息的动态交互）

* 安全性（不允许直接访问本地存储）

* 跨平台（能够解析js的浏览器都可以允许js代码，与平台无关）

  

  

  Java Script和HTML的结合方式

* 在head标签中，或者body标签中，使用script标签来书写Java Script代码

* 使用script标签引入单独的Java Script文件，scr属性可用用来引入js文件



​       Java Script语言

* 变量

  * js的变量类型
    * 数值类型
    * 字符串类型
    * 对象类型
    * 布尔类型
    * 函数类型
  * js中特殊的值
    * undefined：未定义，即js变量未赋值时的默认值
    * null：空值
    * NAN：非数字，非数值，即Not A Number
  * js定义变量的格式：var 变量名 = 变量值；

* 运算符

  * 运算符基本等同于JAVA

  * 等于：== ，字面值的比较

  * 全等：===，字面值，数据类型的比较。

  * 逻辑运算基本等同于JAVA
    * 与运算：&&
    * 或运算：||
    * 非运算：！
    
  * 在js中，所有的变量都可以作为布尔类型的变量来用，其中：0，null，undefined，“”，都认为是false

  * 逻辑运算中的特殊情况：
    * 与运算：
      * 当表达式全为真的时候，返回最后一个表达式的值
      * 当表达式中有一个为假的时候，返回第一个为假的表达式的值
    * 或运算：
      * 当表达式全为假的时候，返回最后一个表达式的值
      * 只要表达式中有一个为真的表达式，就会返回第一个为真的表达式
    * 与运算和或运算有短路效应
      * 当与运算和或运算有结果后，后面的表达式就不再执行了
    
  * 数组
    * 定义格式
      * var 数组名[] = []；空数组
      * var 数组名[] = [.....];   定义数组同时赋值元素，里面可以是数值，字符串等
      * js中的数组，只要通过数组下标赋值，数组就会进行扩容
    
  * 函数

    * 定义函数
      * 使用function关键字来定义函数：function 函数名(参数){方法体}
        * 参数不使用任何类型符修饰，直接写参数名
      * var 函数名 = function(参数){方法体}
    * js中的方法重载会覆盖掉前面的定义，故js中不能做方法重载操作

    * 函数的arguments隐形参数(只在function函数内)
      * 在function函数中不用定义，却可以直接用来获取所有参数变量，该隐形参数类似于Java中的可变参数(public void fun(Object ... args)),可变参数是一个数组，操作类似于数组
    * 自定义对象
      * Object自定义对象：
        * var 对象名 = new Object();   对象实例(空对象)
        * 对象名.属性名 = 值；  定义属性
        * 对象名.函数名 = function();   定义函数
        * 调用自定义对象：自定义的对象名.属性(或函数名())
      * var 对象名 = {   属性名 1：值，属性名2：值，函数名：function(参数){方法体}  }
        * 多个属性和函数之间要用逗号隔开，最后一个函数或属性不用带逗号。

  * js中的事件

    事件是输入设备与页面进行交互的响应

    * 常见的事件：

      * onload：加载完成事件，即页面加载完成后，常用于做页面js代码初始化操作
      * onclick：单击事件，即按钮的单击响应操作
      * onblur：失去焦点事件，即输入框失去焦点后验证其输入内容是否合法
      * onchange：内容改变事件，即下拉列表和输入框内容发生改变之后的响应
      * onsubmit：表单提交事件，即表单提交前，验证表单项内容是否合法

    * 事件注册：

      事件的注册就是告诉浏览器当事件响应后要执行的操作

      * 静态注册：通过HTML标签多事件属性直接赋予事件响应的代码
      * 动态注册：先通过js代码获取标签的dom对象.事件名 = function(){}这种形式赋予事件响应的代码，其方法：
        * 获取标签对象
        * 使用标签对象.事件名 = function(){响应代码}添加响应代码

    * onload事件：

      * 静态注册：在body标签内使用onload属性，其值就是响应操作代码或者前面写好的js代码的方法
      * 动态注册：使用window.onload = function(){响应代码}来指定响应代码

    * onclick事件：

      一般使用于按钮

      * 静态注册：在需要使用onclick的标签中使用onclick属性，其值就为相应操作代码或者前面写好的js代码的方法
      * 动态注册：
        * 使用window.onload = function(){var 对象名 = document.getElementById(”标签id“)}通过标签id获取标签
        * 然后通过对象名.onclick = function(){响应代码}来指定单击响应代码

    * onblur事件：

      一般用于输入框，该方法测试时可用console对象的log()方法在浏览器的控制台进行输出，便于测试

      * 静态注册：在需要使用onblur的标签中使用onblur属性，其值为响应操作代码或者前面写好的js代码的方法
      * 动态注册：
        * 使用window.onload = function(){通过id获取标签，方法同onclick事件}
        * 通过对象名.onblur = function(){响应代码}来指定响应操作

    * onchange事件：

      一般用于下拉列表和输入框

      * 静态注册：同上面的事件
      * 动态注册：同上面的事件

    * onsubmit事件：

      用于表单提交前的检测操作，如果表单项有不合法项会阻止表单提交（return值为ture表单才能提交）

      * 静态注册：同上面的事件，不过要在引用的方法前加上return
      * 动态注册：同上面的事件

  * DOM模型：Document Object Model   即文档对象模型

    就是把文档中的标签，属性，文本转换为对象来管理

    * Document对象(HTML页面就是一个Document对象)

      ```HTML
      <html>
      	<head>
              <title>MYHTML.html</title>
          </head>
          <body>
              <a href = "http://www.baidu.com">我的连接</a>
              <h1>
                  我的标题
              </h1>
          </body>
      </html>
      ```

      该代码块对应的结构图(Document文档树内存结构)：

![html图](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\html图.PNG)

   *  Document对象的理解：
      * Document管理了所有的HTML文档内容
      
      * Document是一种树形结构的文档，有层级关系
      
      * Document让我们可用将所有的标签都对象化
      
      * 我们可用通过Document访问所有的标签对象
      
      * 对于DOM对象，它相当于：
      
        calss Dom{
      
        ​           private String id;        id属性
      
        ​		   private String tagName;   标签名
      
        ​		   private Dom parentNode;   父类
      
        ​		   private List<Dom> children;   子结点
      
        ​		   private String innerHTML;     其实标签和结束标签中间的内容
      
        }
      
* Document对象的常用方法：

   * document.getElementById(elementID)

     通过标签的id属性查找标签dom对象，参数elementId是标签的id属性值，返回对应id的标签

   * document.getElementsByName(elementName)

     通过标签的name属性查找标签dom对象，参数elementName是标签的name属性值，返回多个标签对象的集合(集合中的元素都属于dom对象)，该集合操作同数组

   * document.getElementsByTagName(tagName)

     通过标签名查找标签dom对象，tagName是标签名，返回带有指定标签名的对象集合(集合中的元素都属于dom对象)

   * 注意：以上三个查询方法，如果有id属性，优先使用查询id的方法，其次是name属性，最后才是标签名。且要在页面加载完成后才能进行查询操作

   * document.createElement(tagName)

     通过给定的标签名，创建一个标签对象，tagName是要创建的标签的标签名

   * 正则表达式(RegExp) ：/ 内容/          可用于验证字符串匹配及检索替换，我们可用RegExp对象的text()方法来检测字符串，其用法是 ：

     * var 对象名 = 正则表达式，使用的是我们定义的这个对象
     * var 对象名 = new RegExp(); 参数内容详见文档

*  节点常用属性和方法

   结点就是标签对象

   方法：

   * getElementsByTagNmame(),获取当前结点的指定标签名子结点

   * appendChild(oChildNode)，添加一个子结点，oChildNode是要添加的子结点名称

   属性：

   * childNodes

     获取当前结点中的所有子结点

   * firstChild

     获取当前结点中的第一个结点

   * lastChild

     获取当前结点中的最后一个结点

   * parentNode

     获取当前结点的父结点

   * nextSibling、

     获取当前结点的下一个结点

   * previousSibling

     获取当前结点的上一个结点

   * className

     获取或设置标签的class属性值

   * innerHTML

     表示获取或设置起始标签和结束标签之间的内容

   * innerText

     表示获取或设置其实标签和结束标签之间的文本
   
*  表单(form)验证

   * 表单提交

     * 这个表单可以直接用它的name来.里面的input标签的name直接得到里面的input对象

     * 在form标签中设置action属性可用设置提交表单的服务器地址
     * 在form标签中设置method设置表单提交的方式，其属性值为get或者post
       * get请求的特点：
         * 浏览器地址栏的内容是：action属性[+分隔符+请求参数]
         * 安全性低，会把信息显示在请求参数上
         * 有数据长度的限制
       * post请求的特点：
         * 浏览器地址栏的内容只有action的属性值
         * 比get安全
         * 理论上没有数据长度的限制
     * 表单无法正确提交给服务器的时候的三种情况
       * 表单项没有name属性，请求参数会缺少对应的表单项，故想要发送完整的表单，每个表单项都要设置name属性
       * 单选，复选和下拉列表标签中要写上value属性和option属性
       * 表单项要写在提交项的form标签中

   * 正则表达式(RegExp) ：/ 字符串内容(由正则表达式的内容构成)/          可用于验证字符串匹配及检索替换，我们可用RegExp对象的text()方法来检测字符串，其用法是 ：

     * var 对象名 = 正则表达式，使用的是我们定义的这个对象
     * var 对象名 = new RegExp(); 参数内容详见文档

   * 正则表达式的内容:

     * 元字符匹配

       * . :表示匹配跟在这个符号后面那个单个字符
       * \ :表示匹配一个字符,字符的规则由后面跟的那个东西限定.根据后面的一个字符串来进行适配,如果是\d,就是匹配一个数字,\D就匹配一个非数字字符.\w表示匹配一个单词字符(字母数字下划线).\s表示匹配一个空白字符

     * 方括号匹配

       * 表示是否匹配在方括号里面的字符,里面的字符是可以由逻辑表达式来写的,比如a|b

       * [abc]:表示匹配字符串是否含有a/b/c

       * [^abc]:表示匹配字符串是否不含有a/b/c

       * [a-z]:表示匹配字符串是否含有a/b/.../z.

     * 数量符匹配

       * 字符+:至少包含一个指定字符
       * 字符*:包含任意个指定字符
       * 字符?:包含0个或1个指定字符
       * ^字符:以指定字符开头
       * 字符$:以指定字符结尾

     * 以上匹配规则可以混合使用

## JQuery(框架)

JQuery是辅助js开发的js类库，它的核心思想是write less,do more,它实现了很多浏览器的兼容问题

* 在<script>标签里使用src属性引入jquery库

* JQuery核心函数

  * $  是JQuery的核心函数，能够完成JQery的大部分功能，$()就是调用$这个函数

    * 当传入参数为函数的时候

      即$(function(){})

      表示页面加载完成后要执行的操作，相当于window.onload = function(){}

    * 当传入参数为HTML字符串时

      即$("<div>"+"<span>  ？？？？？</span>" +“<span>??????</span>” +</div>").applendTo("body");

      会在指定标签中快速创建HTML标签对象，不用一个一个标签建立

    * 当传入参数为选择器字符串时

      $("#id属性值")

      表示根据id查询标签对象

      $("标签名")

      表示根据指定标签查询标签对象

      $(".class属性值")

      表示根据class属性查询标签对象

    * 传入参数为DOM对象时

      var bt = document.getElementById("id值")

      $("bt")

      表示将该DOM对象转换为JQuery对象

  * JQuery对象与DOM对象的区别

    * DOM对象
      * 通过getElementById()获取的标签对象是DOM对象
      * 通过getElementsByName()获取的标签对象是DOM对象
      * 通过getElementsByTabName()获取的标签对象是DOM对象
      * 通过createElement()创建的对象是DOM对象
    * JQuery对象
      * 通过JQuery提供的API创建的对象是JQuery对象
      * 通过JQuery包装的DOM对象是JQuery对象
      * 通过JQuery提供多API查询到的对象是JQuery对象

  * JQuery的本质

    JQuery对象是DOM对象的数组和JQuery提供的一系列功能函数

  * JQuery对象和DOM对象使用的区别

    JQuery对象是不能使用DOM对象的函数的，DOM对象也不能使用JQuery对象的函数，它们是两个对象

  * JQuery对象和DOM对象的互相转换

    * DOM对象转换成JQuery对象：使用$(DOM对象)可将DOM对象转换成JQuery对象
    * JQuery对象转换成DOM对象：使用JQuery对象[下标名]取相应的DOM对象

  * JQuery选择器

    * 基本选择器

      * #id  ：根据id获取相应标签
      * element  ：根据给定的标签名获取相应标签
      * .class  ：根据给定的类获取相应标签
      * *：获取全部标签
      * selector1，selector2，selector？ ：组合选择器

    * 层级选择器

      * ancestor descendant :表示在该标签中选取所有的子标签

         ancestor是需要寻找子标签的父标签，descendant是子标签

      * parent > child：表示在给定的标签中选取一级子标签

      * prev + next ：表示选取紧跟在给定标签(标签里)后的标签

      * prev ~ siblings：表示选取跟在给定标签(结束标签)后的所有标签

    * 过滤选择器

      * 基本过滤器
        * ancestor :first：表示获取给定标签中的第一个元素
        * ancestor :last()：表示获取给定标签中的最后一个元素
        * ancestor :not(selector)：表示去除所有与给定选择器匹配的元素
        * ancestor :even：表示匹配所有索引值为偶数的元素，从0开始计数
        * ancestor :odd：表示匹配所有索引值为奇数的元素
        * ancestor :eq(n)：表示匹配一个索引值为n的元素
        * ancestor :gt(n)：表示匹配所有索引值大于索引值为n的元素
        * ancestor :lt(n)：表示匹配所有索引值小于索引值为n的元素
        * ancestor :header：表示匹配标题元素，如<h1>
        * ancestor :animated：表示匹配正在执行动画效果的元素

    * 内容过滤器

      * ancestor :contains(text)：表示匹配包含给定文本的元素
      * ancestor :empty：表示匹配所有不包含子元素或文本的空元素
      * ancestor :parent：表示匹配所有非空元素
      * ancestor :has(selector)：表示匹配含有选择器所匹配的元素的元素

    * 属性过滤器

      * ancestor [attribute]：表示匹配给定属性的元素
      * ancestor [attribute=value]：表示匹配给定属性是某个值的元素
      * ancestor [attribute!=value]：匹配所有不包含指定的属性，或匹配属性不等于某个值的元素
      * ancestor [attribute^=value]：匹配给定的属性是以某些值开始的元素
      * ancestor [attribute$=value]：匹配给定的属性是以某些值结束的元素
      * ancestor [attribute*=value]：匹配给定的属性是包含某些值的元素
      * ancestor [selector1] [selector2] [selectorn]：组合属性选择器，匹配满足多个条件的元素。

    * 表单过滤选择器（type）

      *  :input：表示匹配所有的input，textarea，select和button元素
      * :text：匹配所有的单行文本框
      * :password：匹配所有的密码框
      * :radio：匹配所有的单选按钮
      *  :checkbox：选取所有的复选框
      *  :submit：选取所有的提交按钮
      *  :image：基本不用，可忽略
      *  :reset：匹配重置按钮
      *  :button：匹配所有按钮
      * :file：匹配所有的文件域
      *  :hidden：匹配所有的不可见元素
      * 表单对象属性：
        * :enabled：匹配所有可用元素
        * :disabled：匹配所有不可用元素
        * :checked：匹配所有选中的被选中元素(复选框，单选框等，不包括select中的option)
        * :selected：匹配选中的option元素

    * 元素的筛选

      * eq()                   获取给定索引值的元素
      * first()                获取第一个元素
      * last()                获取最后一个元素
      * filter(exp)        留下匹配的元素
      * is()                    判断是否匹配给定的选择器，只要有一个匹配就返回true
      * has(exp)          返回包含有匹配选择器的元素的元素
      * not(exp)          删除匹配选择器的元素
      * children(exp)  返回匹配给定选择器的子元素
      * find(exp)          返回匹配给定选择器的后代元素
      * next()               返回当前元素的下一个兄弟元素
      * nextAll()           返回当前元素后面所有的兄弟元素
      * nextUntil()       返回当前元素到指定匹配的元素为止的后面元素
      * parent()            返回父元素
      * prev(exp)         返回当前元素的上一个兄弟元素
      * precAll()           返回当前元素前面所有的兄弟元素
      * precUnit(exp) 返回当前元素到指定匹配的元素位置的前面元素
      * siblings(exp)   返回所有的兄弟元素
      * add()                 把add匹配的选择器的元素添加到当前的JQuery对象中

  * JQuery属性操作

    * html()

      该方法可用设置和获取标签中的内容，同DOM类的innerHTML

    * text()

      该方法可用设置和获取标签中的文本，同DOM类的innerText

    * val()

      该方法可以设置和获取表单项中的value属性值，同DOM类的value

      * val()同时设置多个表单项的选中状态：使用过滤器

    * attr()

      可以设置和获取属性值，设置一个参数就是获取参数，两个参数就是设置参数，如果找不到对应属性会返回undefinded。某些属性会返回undefinded，比如checked,readOnly,selected,disabled等，对这些属性不加使用attr()来操作。attr()较为常用，它还可以操作自定义属性

    * prop

      可以设置和获取属性值，如果找不到对应属性会返回false

  * DOM的增删改

    * 内部插入

      * appendTo()

        a.appendTo(b)表示将a插入到b元素末尾，成为最后一个子元素

      * prependTo()

        a.perpendTo(b)表示将a插入到b所有子元素前面，成为第一个子元素

    * 外部插入

      * insertAfter()

        a.insertAfter(b)表示将a插入到b元素的后面

      * inserBefore()

        a.inserBefore(b)表示将a元素插入到b元素的前面

    * 替换

      * replaceWith()

        a.replaceWith(b)表示用b替换a

      * replaceAll()

        a.replaceAll(b)表示用a替换掉所有的b

    * 删除

      * remove()

        a.remove()表示删除a标签

      * empty()

        a.empty()表示清空a标签内的内容

  * JQuery中的CSS样式操作

    * addClass()            向被选取元素添加一个或多个类
    * removeClass()     从选取元素删除一个或多个类
    * toggleClass()        对被选取元素进行添加或删除类的切换操作
    * offset()                   获取或设置第一个匹配元素相对于文档的位置

  * JQuery动画

    * 基本动画
      * show()            将隐藏的元素显示
      * hide()              将隐藏的元素显示
      * toggle()           将隐藏的元素显示，将隐藏的元素显示
      * 动画函数都可以添加参数，第一个参数是动画持续时长，单位为毫秒，第二个参数是动画的回调函数(动画完成后的操作)
    * 淡入淡出动画
      * fadeIn()            淡入
      * fadeOut()         淡出
      * fadeTo()           在指定时间内将透明度修改到指定值
      * fadeToggle()    淡入淡出切换

  * JQuery事件操作

    * $(function(){})于window.onload = function(){}的区别

      * 先执行JQuery

        原因：JQuery的页面加载玩成后是浏览器的内核解析完页面的标签创建好DOM对像后就会马上执行

      * 再执行原生

        原因：原生js页面加载完成后，还需等待标签显示需要加载的内容加载完成

      * 原生js页面加载完成后，只会执行最后一个

      * JQuery页面加载完成后，会将注册的function函数依次顺序执行
    
  * JQuery中常用的事件处理方法(这些方法都可以绑定，又可以触发)：

    * click()                        可绑定单击事件，还可以触发单击事件

    ​        参数传function是绑定，不传参数是触发事件

    * mouseover()            鼠标移入事件
    * mouseout()              鼠标移出事件
    * mousemove()          鼠标移动事件
    * bind()                         给一个元素绑定一个或多个事件，参数为想要绑定的事件名称，如click，和对应的操作(function(){}),如果要绑定多个事件，在事件名处用空格隔开多个事件名
    * one()                           使用方法同bind()方法，不过它只会触发一次
    * unbind()                      跟bind()方法相反，用来解除事件绑定,参数为想删除的事件
  * live()                             可以用来绑定事件，可以用于绑定选择器匹配的所有元素的事件，包括动态创建的事件
  
* 事件的冒泡：
  
  事件冒泡指的是父子元素同时监听一个事件，当触发子元素的事件时，同一个事件也传递到了父元素里去响应，可以在子元素的事件函数体内使用return false来阻止事件的冒泡传递
  
* Java Script事件对象

  事件对象是封装有触发的事件信息的一个Java Script对象。我们可以在元素绑定事件的时候，在事件函数(function(){})的参数列表中传一个参数，习惯将该参数名取为event，这个参数就算Java Script传递参事件处理函数的事件对象

## XML部分

* XML是可扩展的标记性语言

  * XML的作用

    * 用于保存数据，而且这些数据具有自我描述性
    * 作为项目或者模块的配置文件
    * 作为网络传输数据的格式(不过现在网络传输数据的格式主要是JSON)

  * XML语法及文件内容构成

    * 文档声明

      一般在XML的第一行，诸如<?xml version = "1.0" encoding = "utf-8" ?>,其中的version表示XML的版本，encoding表示XML文件的编码

    * 元素(标签)

      可以使用<></>符号来进行自定义标签(单标签也可以),<>中的内容是自定义标签的名称，在标签的中间可以定义标签的内容，还可以自定义属性，不过标签有一些命名规则

      * 名称可以包含字母，数字以及其它的字符，中文也可以
      * 名称不可以以数字或者标点符号开始
      * 名称不可以以字符xml(不论大小写)开始(其实这样命名也可也，不过习惯上不这样做)
      * 名称不可以包含空格

    * XML属性

      XML的标签属性和HTML的标签属性是非常类似的，属性都是提供元素的额外信息的，属性的定义规则：

      * 一个标签上可以书写多个属性，不同属性之间用空格隔开，每个属性的属性值必须用引号括起来，属性的命名规则于标签一致

    * XML注释

      同HTML，都是<!--注释内容-->

    * 文本区域(COATA区)

      <![CDATA[不想让XML解析的字符]]>这个标签可以将大块的特殊字符按文本显示，不使用XML解析

    * 语法规则

      * 所有XML元素都必须有关闭标签(必须闭合)
      * XML元素对名称的大小写敏感
      * XML必须正确的嵌套(正确的闭合)
      * XML文档必须有根元素(就是顶级元素，唯一一个没有父标签的元素)
      * XML中的特殊字符规则同HTML，如<>符号和空格

  * XML解析技术

    HTML文件还是XML文件都是标记性文档，都是使用W3C阻止指定的DOM技术

    ![DOM技术](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\DOM技术.PNG)

      即标签会被解释器解析成一个类。DOM解析技术是W3C阻止制定的，而所有的语言都对这个解析技术使用了自己语言的特性进行实现。早期JDK的两种XML解析技术(DOM和SAX)都已经过时，我们现在用的大部分是第三方解析技术(JDOM，DOM4J，PULL)

    * JDOM是在DOM基础上进行了封装
    * DOM4J是在JDOM基础上进行了封装
    * PULL主要是用在Android开发上，是与SAX类似的，属于事件机制解析XML文件
    * 这些第三方解析技术，我们需要使用第三方提供的类库才可以解析XML文件

  * DOM4J解析技术、

    DOM4J属于第三方解析技术，JDK中没有它的类库，我们需要从外部导入依赖包(jar包)，在它的docs文件下的index.html可以进入文档，lib文件下是它的类库，src文件是它的源码包以及测试代码和样例代码

    * 使用DOM4J解析将XML文件解析为JAVA类(class)的步骤：

      * 获取Document对象：

      ​        创建一个lib目录用于保存导入的jar包，将jar包Add as Library,在level(这个选项是将jar包指定使用对象，可以给整个工程使用，或者仅一个模块使用，或者一个组使用)选项选择Module Library

      ​      一般要使用dom4j的jar包，hamcrest-core的jar包，以及junit的jar包

      ​      创建SaxReader对象(输入流)，来读取XML配置文件(使用SaxReader对象的read方法，参数为需要读取的XML文件目录)，生成Document对象

      * 读取XML文件生成对应的类

        * 读取XML文件

          用SaxReader对象的read()方法读取

        * 通过Document对象获取根元素

          使用Document对象接收SaxReader对象生成的Doucment对象

          然后用Element对象接收根元素

        * 通过根元素获取标签对象

          使用Element对象的.element()或者.elements()查找子元素，当有多个子元素的时候用elements()，参数为标签id，一般使用List组来接收标签组

        * 处理每个标签转换成对应的类

          * 使用for循环遍历获取的标签，使用对应方法将标签对象转换为想要的类型，如asXML()可以将标签对象转换为标签字符串，getText()可以获取标签中的文本内容，elementText()可以获取指定标签名中的文本内容，attributeValue()可以获取指定属性的值

## Tomcat部分

* JavaWeb
  * JavaWeb概念
  
    所有通过Java语言编写可以通过浏览器访问的程序的总称，就是Java Web
  
    Java Web是基于请求和响应来开发的
  
  * 请求
  
    请求是指客户端给服务器发送数据，就是请求(Request)
  
  * 响应
  
    响应是指服务器给客户端回传数据，就算响应(Response)
  
  * 请求与响应的关系
  
    请求和响应是成对出现的，有请求就有响应
  
* Web资源的分类

  Web资源泛指浏览器能够访问的资源，Web资源按实现的技术和呈现的效果的不通用，又分为静态资源和动态资源

  * 静态资源：HTML文件，CSS样式，JS文件，txt文本，mp4视频，jpg图片等
  * 动态资源：JSP页面，Serviet程序

* 常用Web服务器

  * Tomcat：提供对JSP与Serviet的支持，当前应用最广泛的JavaWeb服务器，它是轻量级的Java Web容器，是免费的
  * Jboss：遵从JavaEE规范的，开源的，纯Java的EJB服务器，也是免费的
  * GlassFish：商业级服务器，应用较少
  * Resin：对Serviet和JSP提供了良好的支持，性能不错，自身是JAVA开发的，不过是收费的
  * WebLogic：目前应用最广泛的Web服务器，支持JavaEE规范，适合大型项目，不过是收费的

* Tomcat服务器和Serviet版本的对应关系

  Serviet程序从2.5版本是现在使用最多的版本，到3.0版本后，就算注释版本的Serviet使用

  ![Ts](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\Ts.PNG)

* ·Tomcat解压目录

  * bin：存放Tomcat服务器的可执行程序
  * lib：存放Tomcat服务器的jar包
  * conf：存放Tomact服务器的配置文件
  * logs：存放Tomcat服务器运行输出的日志
  * temp：存放Tomcat产生的临时数据
  * webapps：存放部署的Web工程
  * work：是Tomcat工作时的目录，存放服务器jsp翻译为Serviet钝化的目录

* Tomcat的启动与停止

  双击在bin目录下的startup.bat文件即可启动Tomcat服务器，shutdown.bat可停止Tomcat服务器。启动服务器后可以在浏览器输入localhost:8080看是否能跳转到Tomcat的官网页面，能够跳转就是启动成功了

* 修改Tomcat默认的端口号(默认为8080)

  在conf目录下的Serviet.xml文件中的<Connector>标签，修改port=“8080”的值，端口号范围一般在1-65535，端口尽量往大了选，1-1000一般是系统使用的端口，修改完后需要重启服务器。

  扩展：HTTP协议的端口号默认是80，当选择80端口时，会不显示端口号

* 部署Web工程到Tomcat中

  * 将Web工程的目录保存在webapps目录中

    访问工程方法：localhost:端口号/工程名/文件名

  * 使用配置文件部署：在conf目录下的\Catalina\localhost\下，创建一个XML配置文件，

    在里面写上<Context path = "/配置文件的名称" docBse = "Web工程的目录"/>,context表示一个工程上下文，path表示工程的访问路径，docbase表示工程目录的位置

* 手托html页面到浏览器启动工程与输入地址访问html页面的区别

  * 手托使用的协议为file://协议，这个协议是直接对本地文件进行读取
  * 输入地址使用的协议为http://协议，这个协议是通过对服务器发送请求再通过服务器的响应获取回传的信息
  
* ROOT的工程访问以及默认HTML页面的访问

  当我们只输入地址以及端口号时，没有指明工程名时，默认访问ROOT工程

  当我们输入了工程名，没有指定资源名时，默认访问index.html

* IDEA整合Tomcat服务器

  进入设置(Setting)界面中的Build选项中的Appliction Server，添加Tomcat服务器

* 创建动态Web工程

  在工程中创建新的模块，在IDEA20.2版本后没有了Jaca Enterprise选项，要创建Web项目的话就需要在新建模块上右键，选择添加模型支持，选择Web Application即可

  创建好Web工程后，我们习惯在WEB-INF目录下新建一个lib文件，这里面存放我们需要使用的jar包(还需要自己配置导入)。src目录下是我们自己编写的JAVA源代码，web目录下是用来存放web工程的资源文件(html页面，js文件，css样式等)，WEB-INF目录是一个受服务器保护的目录，浏览器无法直接访问该目录下的内容，该目录下的web.xml文件是整个web工程的配置部署描述文件，可以在这里配置许多web工程的组件(Serviet程序，Filter过滤器，Listener监听器，Session超时等等)。

* 为自己的工程添加jar包

  将jar包复制到lib目录下，将他们选中，右键选择Add as Library。也可以在File选项下的Project Strueture选项中的Libraries中添加，创建一个类库，选择jar包添加，添加后选择需要将类库添加给的模块，然后选择Artifacts，部署jar包。

* 在IDEA中部署Tomcat

  在运行选项的Exit Configurations中进行部署的配置

  在ON frame deactivation选择Update class and resources可以实现热部署更新

## Servlet技术部分

* Servlet
  * JAVAEE的规范之一(接口)
  * 是Java Web三大组件(Servlet，Filter，Listener)之一
  * 是运行在服务器商店一个java程序，可以接受客户端的请求并响应数据
  
* 手动实现Servlet程序

  * 直接使用实现类来实现Servlet接口
  * 实现service方法，处理请求并响应数据
    * service方法是专门用于处理请求和响应的,在它的service方法中写出要响应的代码
  * 到web.xml中去配置service程序的访问地址
    * 使用<servlet></servlet>标签来配置，在其中使用<servlet-name></servlet-name>标签来指定Servlet程序的名称(即Servlet的实现类名)，用<servlet-class></servlet-calss>来指定类名称(Servlet程序的全类名)，写好这个标签后，要添加一个<servlet-mapping></servlet-mapping>标签来告诉服务器当前配置的地址给哪个Servlet程序使用。其中的<url-pattern></url-pattern>标签用来配置访问地址，值一般写作/servlet程序名，一般Servlet的类名与访问地址要一样，/一定要写，它表示http://ip地址:端口/工程路径/
    * 一个Servlet可以指定一个映射路径或多个映射路径或者指定通用映射路径
      * 一个的话就是直接写一个/指定路径名称
      * 多个的话就是写多个Servletmapping标签,然后它们的servletname相同
      * 通用的话就是写个/请求名/*,这样任何请求都会经过这个Servlet,如果/ *的话,它的优先级会高过index,就不会过首页直接进入请求了.
    * 这些路径是有优先级的,指定了固定请求路径的路径优先级最高,其次就是通用的路径
    * 可以指定一些后缀或者前缀等
      * 自定义前缀,比如*.s,表示以s结尾的请求都能过Servlet,不过还是用一对一比较多
    * 扩展:错误
      * 我们也可以用一个错误页面来处理页面找不到等错误,就直接像一般Servlet那样写就行了

* url地址到Servle程序的访问

* Servlet的生命周期

  * 执行Servlet构造器方法
  * 执行init初始化方法
  * 上两步是在第一次访问的时候，创建Serviet程序的时候会调用
  * 执行service方法
  * 这一步每次访问都会调用
  * 执行destroy销毁方法
  * 这一步在web工程停止的时候才会调用

* GET和POST请求的分发处理

  * SercletletRequest接口的HttpServletRequest接口中有getMethod()方法可以获取请求类型,可以将参数中的servletRequest用类型强转成HttpServletRequest接口，再获取请求类型：

    HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest

    String Method = httpServletRequest.getMethod()

    通过这个请求类型，我们可以用if来区分不同请求类型要做的事

* 通过继承HttpServlet实现Servlet程序 

  我们在实际开发使不常实现Servlet接口来实现Servlet程序，通常使用继承HttpServlet类的方法去实现Servlet程序，步骤：

  * 创建一个继承HttpServlet类的类
  * 根据实际需要重写doGet或者doPost方法
    * doGet()方法会响应get请求
    * doPost()方法会响应post请求
    * 这个方式分发请求，较为方便
  * 在web.xml中配置Servlet程序的访问地址

* 在IDEA中直接创建Servlet程序

  可以在类的包名上直接NEW一个Servlet程序

* Servlet的继承体系

  这部分内容参照文档

* ServletConfig类(在init方法中的第一个参数)

  这个类是Servlet程序的配置信息类，它的三大作用：

  * 可以获取Servlet成需的servlet-name的值
  * 获取初始化参数init-param(这个东西是在web.xml文件中配置的)
  * 获取ServletContext对象

  Servlet程序和servletConfig类都是由服务器创建的，Servlet程序默认是第一次访问的时候创建，ServletConfig是每个Servlet程序创建时，就创建一个对应的ServletConfig对象

  * 在其它地方可以使用getServletConfig()方法来获取ServletConfig对象

* ServletContext类

  * ServletContext是一个接口，它表示Servlet上下文对象

  * 一个Web工程，只有一个ServletContext对象实例

  * ServletContext对象实例在web工程部署的时候创建一次，在web工程结束时才会销毁

  * ServletContext对象是一个域对象(这个对象是可以像Map存取数据的对象，域指的是存取数据的操作范围，这个范围是整个Web项目)

     这个东西与Map的区别：

    Map对象：存数据方法是put(),取数据方法是get(),删除数据方法是remove()

    域对象：存数据方法是setAttribute(),取数据方法是getAttribute(),删除数据方法是removeAttribute()

  * ServletContext类的四个作用

    * 获取web.xml中配置的上下文参数[getInitParameter()方法] (context.param)
    * 获取当前的工程路径(:/工程路径)[getContextPath()方法]
    * 获取工程部署后在服务器硬盘上的绝对路径[getRealPath()方法，参数写"/"的话就会映射到web目录，"/具体目录"会映射到具体目录]
    * 存取数据

  * HttpServletRequest类

    每次只要有请求进入Tomcat服务器，Tomcat服务器就会把请求的HTTP协议信息解析好封装到Request对象中，然后传递到service方法(doGet和doPost)中供我们使用，我们可以通过HttpServletRequest对象获取所有请求的信息，其中给定常用方法：

    * getRequestURI(),获取请求的资源路径

    * getRequestURL()，获取请求的统一资源定位符(绝对路径)

    * getRemoteHost()，获取客户端的ip地址

    * getHeader()，获取请求头

    * getParameter()，获取请求的参数

    * getParameterValues()，获取请求的参数(多个值的时候)

      获取请求参数时，如果请求方式为post，则获取的中文参数可能会变成乱码，要解决这个问题，就需要在doPost方法中使用HttpServletRequest类的setCharacterEncoding()方法来设置字符集，一般将参数设置为"UTF-8"

    * getMethod()，获取请求的方式(get或者post)

    * setAttribute(key,value)，设置域数据

    * getAttribute(key)，获取域数据

    * getRequestDispatcher()，获取请求转发对象

* HTTP协议

  协议是双方或多方共同约定遵守的规则，HTTP协议就是指客户端和服务器之间在通讯时所要遵守的规则，HTTP协议中的数据又称作报文

  * 请求的HTTP协议格式：请求行+请求头，请求行(请求方式，请求的资源路径，请求的协议和版本号)，请求头(由键值对组成)

    * get请求

      * 请求行

        GET   /请求的资源路径/   HTTP/版本号

      * 请求头

        一般包括这些内容

        * Accept:告诉服务器客户端可接受的数据类型
        * Accept-Language:告诉服务器客户端可接受的语言类型
        * User-Agent:浏览器信息
        * UA-CPU:CPU型号和位数
        * Accept-Encoding:告诉服务器客户端可接受的数据编码格式(压缩格式)
        * Host:表示请求的服务器ip和端口号
        * Connection:告诉服务器请求连接如何处理，常用值有Keep-Alive(回传完数据后继续保持一段事件的连接)，Closed(回传数据完成后就断开连接)

    * post请求

      * 请求行

        同上

      * 请求头

        同上

      * 请求体

        一般请求体和请求头之间有一个空行，用于隔开。请求体内容即发送给服务器的数据

    * 常用请求头说明

      见get请求的请求头

    * 区分get请求和post请求

      * get请求
        * form标签，method = get
        * a标签
        * link标签引入css
        * Script标签引入js
        * img标签引入图片
        * iframe引入html页面
        * 在浏览器地址栏中输入地址
      * post请求
        * form标签，method = post

  * 响应的HTTP协议格式

    * 相应行
      * 响应的协议和版本号
      * 响应的状态码
      * 响应状态描述
    * 响应头
      * 一堆键值对
      * Server:服务器信息
      * Accept-Ranges:
      * ETag:
      * Last-Modified:
      * Content-Type:响应体的数据类型
      * Content-Length:响应体长度
      * Date:请求响应的时间
    * 空行
    * 响应体
      * 回传给客户端的数据
    * 常见的响应码
      * 200：表示请求成功
      * 302：表示请求重定向
      * 404：表示服务器已接受到请求，但是需要的数据不存在(地址错误)
      * 500：表示服务器已接受到请求，但是服务器内部出错

  * MIME类型说明

    MME(Multipurpose Internet Mall Extensions),多功能Internet邮件扩充服务。它是HTTP协议中的数据类型，MIME类型的格式是大类型/小类型，并与某一种文件的扩展名对应

  * 在浏览器中查看HTTP协议

    在浏览器中按下F12键调出控制台，进入Network页面，在Headers和Response中会有请求和响应的各种信息

* 请求转发

  指服务器收到请求后，从一个资源跳转到另一个资源的操作，就是请求转发，图解：

  ![](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\请求转发.PNG)

  * 使用getRequestDispatcher()方法来将请求转发到目标位置(用RequestDispatcher对象来接收)，其中的参数为"/目标程序"，并使用forward()方法前进至目标程序

* base标签

  base 标签设置页面相对路径工作时参照的地址，href 属性就是参数的地址值，这个标签一般写在head标签下

* Web中的相对路径和绝对路径相对路径是： 

  * ./                      表示当前目录 
  * ../                     表示上一级目录 
  * 资源名            表示当前目录/资源名 
  * 绝对路径： http://ip:port/工程路径/资源路径
  * /的含义：
    * 若是浏览器解析：得到的地址是：http://ip:port/
    * 若是服务器解析：得到的地址是：http://ip:port/工程路径
    * 特殊情况：：response.sendRediect(“/”); 把斜杠发送给浏览器解析。得到 http://ip:port/

* HttpServletResponse 类

  HttpServletResponse 类和 HttpServletRequest 类一样。每次请求进来，Tomcat 服务器都会创建一个 Response 对象传 递给 Servlet 程序去使用。HttpServletRequest 表示请求过来的信息，HttpServletResponse 表示所有响应的信息， 我们如果需要设置返回给客户端的信息，都可以通过 HttpServletResponse 对象来进行设置

  * 两个输出流的说明
    * 字节流：getOutputStream()   常用于下载（传递二进制数据）
    * 字符流：getWriter()   常用于回传字符串（常用）
    * 两个流同时只能用一种
  * 响应时可能会出现中文乱码问题，我们可以直接使用HttpServletResponse 对象的setContentType()方法设置浏览器的响应字符集，该方法必须在获取流对象前设置才有效

* 请求重定向

  指客户端给服务器发请求，然后服务器告诉客户端说，我给你一些地址，你去新地址访问。叫请求重定向（因为之前的地址可能已经被废弃），图解：

  ![请求重定向](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\请求重定向.PNG)

  * 请求重定向的第一种方案： 
  
     设置响应状态码 302 ，表示重定向（已搬迁） :resp.setStatus(302);
  
    设置响应头,说明新的地址在哪里: resp.setHeader("Location", "新地址");
  
  * 请求重定向的第二种方案（推荐使用）：
  
     resp.sendRedirect("新地址")

## JAVAEE项目的三层架构

<img src="C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\EE三层架构.PNG" alt="EE三层架构" style="zoom:150%;" />

分层的目的是为了解耦，降低代码的耦合度，方便后期维护和升级

一般我们创建项目的时候，都会创建下列分层的包路径(在src目录下创建com.atguigu包)，其中atguigu这个名字可以更改成自己项目的名称

web 层               com.atguigu.web/servlet/controller 

service 层          com.atguigu.service           						  Service 接口包                                             							com.atguigu.service.impl  						  Service 接口实现类 

dao 持久层        com.atguigu.dao                  						  Dao 接口包  	

​							com.atguigu.dao.impl Dao      					接口实现类 

实体bean对象   com.atguigu.pojo/entity/domain/bean     JavaBean 类 

测试包                com.atguigu.test/junit 

工具类                com.atguigu.utils

创建好了工作环境，就可以开始进行编码了，一般开发的步骤：

* 创建数据库和表
* 编写数据库表对应的JavaBean对象
* 搭建工具类JdbcUtils(用来管理数据库并创建连接)
* 编写BaseDao
* 编写UserDao和测试。
* 编写UserService和测试

## JSP部分

JSP(java server pages),Java的服务器页面，jsp的主要作用是代替Servlet程序回传html的数据，因为Servlet程序回传html页面数据是非常繁琐的，开发和维护成本高，于是jsp就出现了，它可用简化数据回传

* 创建jsp页面：在web文件夹下直接new jsp文件

* jsp的访问：访问方式同html页面一样

* jsp的本质：jsp页面本质上是一个Servlet程序

  * 在我们访问jsp页面的时候，服务器会将jsp页面翻译成一个java文件，并且会将它编译成class文件，其中的源代码的HttpJspBase类，它直接的继承了HttpServlet类，即它翻译出来的是Servlet程序

* Jsp的语法

  * 头部page指令，书写格式：<% page page属性="属性值">page指令可用修改jsp页面中的重要属性或者行为，常见page指令属性：
    * lauguage 属性                  表示jsp翻译后的文件的语言
    * contentType 属性            表示jsp返回的数据类型
    * pageEncoding 属性          表示当前jsp页面的字符集
    * import 属性                       表示导包
    * autoFlush 属性                  给out输出流使用，设置out输出流缓冲区满了后是否自动刷新缓冲区，默认是ture
    * buffer 属性                        给out输出流使用，设置out缓冲区的大小，默认为8kb
    * errorPage 属性                 设置当jsp页面运行出错自动跳转去的错误页面路径，路径以/开头
    * isErrorPage 属性              设置当前jsp页面是否是错误信息页面，默认是false，如果是就可用获取错误信息        
    * session 属性                      设置访问当前jsp页面是否会创建HttpSession对象，默认是ture
    * extends 属性                     设置jsp翻译出的类默认继承哪个类

* Jsp脚本

  * 声明脚本
    * 格式：<%!  声明java代码 %>
    * 作用：可用给jsp翻译出的java类定义属性和方法，或是静态代码块，类方法，内部类
  * 表达式脚本
    * 格式：<%= 表达式 %>
    * 作用：在jsp页面上输出数据，可输出整型，浮点型，字符型，对象的数据
    * 特点：
      * 所有的表达式脚本都会被翻译到_jspService方法中
      * 表达式脚本都会被翻译成out.print()输出到页面上
      * _jspService方法中的对象可以直接用
      * 表达式结尾不加;
  * 代码脚本
    * 格式：<%   java语句  %>
    * 作用：可以在jsp页面中编写功能，如if语句，for循环语句，_jspService方法中的代码（使用其中的类）等
    * 代码脚本可以由多个代码脚本块组合
    * 代码脚本可以与表达式脚本一起使用

* 注释格式

  * jsp格式：<%--注释内容--%>m，可以注释所有jsp页面代码
  * html格式：<!--注释内容-->，会以out.write方法输出
  * java格式：写在表达式脚本或代码脚本中

* 九个内置对象

  内置对象指服务器将jsp页面翻译成Servlet程序后包含的对象

  * request    请求对象                       	域对象之一(HttpServletRequest类)，数据在一次请求内容有效

    对于form表单,它在里面的input'标签得有一个type为submit的才能进行数的提交,提交的数据是具有name属性的input标签,提交的路径是form表单的action属性所指定的路径,这个路径可以是jsp页面或者Servlet.

    * 常用的方法
      * getParameter(String name):获取request对象中name为指定值所对应的值,单值
      * getParameterValue(String name):用来获取复选框的的值,数组值
      * set/getAttribute(String s,Obj obj):存/取一个名为s的Obj类型的东西
      * getRrquestDispatcher(String url).forward(req,resp):将请求转发到位置为url的地方,会携带数据,就是forward方法带的那两个

  * response 响应对象  

    * sendRedirect(String url):将请求重定向到位置为url的地方,不会携带数据,可以通过在url上拼接数据

  * pageContext jsp上下文对象            域对象之一(PageContextImpl类)，数据在当前jsp页面有效

  * session 会话对象                               域对象之一(HttpSession类)，数据在一个会话(打开浏览器访问服务器到关闭浏览器位置)范围内有效

  * application ServletContext对象      域对象之一(ServletContext类)，数据在整个web工程范围内(从工程开始运行到工程终止)都有效,有跟Session,Cookie差不多的方法

  * config    ServletConfig对象

  * out     jsp输出流对象

  * page  指向当前jsp的对象

  * exception   异常对象

  * 四个域对象的区别为对数据的存取范围

* out输出和response.getWrite输出的区别

  out缓冲区会将数据缓存进response缓存区，在输出的时候会将response的输出放在前面输出

* 常用标签

  * 静态包含

    在一个页面中插入一个需要维护的页面，只需改动维护的页面，这个插入方式就是静态包含

    * 使用<%@ include file = "页面路径"%>标签指定要包含的jsp页面，属性值为文件目录，即要包含的页面路径

  * 动态包含

    * <jsp:include page = "页面路径"></jsp : include>标签动态插入页面
    * 动态包含与静态包含一样

  * 标签转发

    * <jsp:forward page="页面路径"></jsp : forward>标签可用两作请求转发，可以指定请求转发的路径。
  
* Listener监听器

  是接口，它可以监视某事件的变化，通过回调函数返回给用户并做一些相应的处理

  * ServletContextListener监听器

    这个监听器可以监听ServletContext对象的创建和摧毁，在ServletContext在创建和摧毁之后都会调用该监听器的方法反馈

    * 创建响应方法：public void contextInitialized(ServletContextEvent sce)
    * 摧毁响应方法：public void contextDestroyed(ServletContextEvent sce)

    * 监听器的使用步骤：
      * 使用实现类实现监听器接口
      * 实现两个回调方法
      * 在web.xml中配置监听器
        * 使用<listener><listener-class>监听器实现类的路径</listener-calss></listener>标签配置

## EL表达式部分

Expression Lauguage，表达式语言，是用来替代jsp页面中的表达式脚本在jsp页面中进行数据的输出，EL比jsp表达式更加简洁

* EL表达式格式：${表达式}
  
  * EL表达式结果输出null值时会输出空串
  
* EL表达式主要用于在jsp页面中输出request域的数据
  
  * 如果有多个相同的数据在不同的数据域中时，EL表达式会从数据域从小到大来寻找数据
  
* EL表达式输出Bean的普通属性，数组属性，List集合属性，map集合属性

  * 普通属型           ${类.普通变量}
  * 数组属性           ${类.数组名[下标]}
  * List集合属性     ${类.集合名[下标]}
  * map属性            ${类.map名.键名}
  * EL表达式是通过get方法来获取属性值的

* EL表达式运算

  * 关系运算(用法同JAVA)

    * "=="或eq
    * "!="或ne
    * "<"或it
    * ">"或gt
    * "<="或le
    * ">="或ge

  * 逻辑运算(用法同JAVA)

    * "&&"或and
    * "||"或or
    * "|"或not

  * 算术运算(用法同JAVA)

    * +
    * -
    * *
    * "/"或div
    * "%"或mod

  * empty运算

    可以判断一个数据是否为空，如果为空就输出true(值为null时，值为空串时，值为Object类型数组且长度为0时，值为list集合且元素个数为0，值为map集合且元素个数为0)

    * 用法：${empty 数据名}

  * 三元运算(用法同JAVA)

    * 表达式1 ? 表达式2：表达式3

  * .(点)运算与[]运算

    * 点运算是用来输出Bean对象中某个对象的值
    * []运算是用来输出集合中某个元素的值，还可以输出map集合中的key中含有特殊字符(运算符和.)的值，其中的key值要用单引号括起来

* EL表达式中的11个隐含对象

  这是EL表达式中自己定义的，可以直接使用

  * pageContext    (类型为PageContextImpl)     可用来获取jsp中的内置对象
  * pageScope       (类型为Map<String.Object>) 可获取**pageContext域**中的数据
  * requestScope   (类型同上)      可获取**Request域**中的数据
  * sessionScope    (类型同上)     可获取**Session域**中的数据
  * applicationScope   (类型同上)  可获取**ServcletContext域**中的数据
  * param     (类型为Map<String.String>)    可以获取请求参数的值
  * paramValues   (类型为Map<String.String[]>)   可以获取多个请求参数的值
  * header        (类型为Map<String.String>)    可以获取请求头的值
  * headerValues   (类型为Map<String.String[]>)   可以获取多个请求头的值
  * cookie          (类型为Map<String.Cookie>)     可以获取当前请求的Cookie信息
  * initParam        (类型为Map<String.String>)   可以以获取在web.xml中配置的<context-param>的上下文参数
    * 这些隐含对象的使用方法：
      * 可以用来输出对应域中的数据，格式：隐含对象.key值
      * pageContext用法：
        * pageContext.request.scheme可以获取请求的协议(同request.getScheme)
        * pageContext.request.serverName可以获取服务器ip(同request.getServerName)
        * pageContext.request.ServerPort可以获取请求的服务器端口号(同request.getServerPort)
        * pageContext.request.contextPath可以获取工程路径(同request.setContextPath)
        * pageContext.request.method可以获取请求方法(同request.getMethod)
        * pageContext.request.remoteHost可以获取客户端ip(同request.getRemoteHost)
        * pageContext.session.id可以获取会话的id(同session.getId)

## JSTL标签库部分

JSP Standard Tab Library,即JSTL标准标签库，它是为了替换代码脚本，从而使jsp页面变得更简洁而生的

* JSTL标签库的组成

  * 核心标签库：http//java.sun.com.jsp/jspl/core       前缀为c
  * 格式化：http//java.sun.com.jsp/jspl/fmt                 前缀为fmt
  * 函数：http//java.sun.com.jsp/jspl/functions           前缀为fn

* 在jsp中使用JSTL标签库：

  * 使用<%@ taglib prefix = "标签库前缀" uri="标签库连接" %>

* 标签库的使用步骤

  * 先导入JSTL表签库的jar包
  * 使用taglib指令引入标签库(看上面)
  * 接下来就可以使用了

* core核心库的使用

  * <c : set/>这个标签可以向域中保存数据(作用同：与对象.Attribute(key,value)).

    * set标签后可以设置属性
      * scope属性可以设置要数据要保存在哪个域中，值可以为page,request,session,application，分别对应四个域
      * var属性可以设置key值
      * value属性可以设置value值

  * <c : if ><c : if/>这个标签可以做if判断(做不了多路判断)

    * if标签后可以设置属性

      * test属性可以设置判断表达式，如果成立就执行标签中的内容

      ```jsp
      <%--
      ii.<c:if />
      if 标签用来做 if 判断。
      test 属性表示判断的条件（使用 EL 表达式输出）
      --%>
      <c:if test="${ 12 == 12 }">
      <h1>12 等于 12</h1>
      </c:if>
      <c:if test="${ 12 != 12 }">
      <h1>12 不等于 12</h1>
      </c:if>
      ```

      

  * <c : choose>与<c : when>与<c : otherwise>标签可以做多路判断

    ```jsp
    <%--
    iii.<c:choose> <c:when> <c:otherwise>标签
    作用：多路判断。跟 switch ... case .... default 非常接近
    choose 标签开始选择判断
    when 标签表示每一种判断情况
    test 属性表示当前这种判断情况的值
    otherwise 标签表示剩下的情况
    <c:choose> <c:when> <c:otherwise>标签使用时需要注意的点：
    1、标签里不能使用 html 注释，要使用 jsp 注释
    2、when 标签的父标签一定要是 choose 标签
    --%>
    <%
    request.setAttribute("height", 180);
    %>
    <c:choose>
    <%-- 这是 html 注释 --%>
    <c:when test="${ requestScope.height > 190 }">
    <h2>小巨人</h2>
    </c:when>
    <c:when test="${ requestScope.height > 180 }">
    <h2>很高</h2>
    </c:when>
    <c:when test="${ requestScope.height > 170 }">
    <h2>还可以</h2>
    </c:when>
    ```

​               

```jsp
<c:otherwise>
<c:choose>
<c:when test="${requestScope.height > 160}">
<h3>大于 160</h3>
</c:when>
<c:when test="${requestScope.height > 150}">
<h3>大于 150</h3>
</c:when>
<c:when test="${requestScope.height > 140}">
<h3>大于 140</h3>
</c:when>
<c:otherwise>
其他小于 140
</c:otherwise>
</c:choose>
</c:otherwise>
</c:choose>
```

* * <c : forEach/>标签可以做循环操作

    ```jsp
    <%--1.遍历 1 到 10，输出
    begin 属性设置开始的索引
    end 属性设置结束的索引
    var 属性表示循环的变量(也是当前正在遍历到的数据)
    for (int i = 1; i < 10; i++)
    --%>
    <table border="1">
    <c:forEach begin="1" end="10" var="i">
    <tr>
    <td>第${i}行</td>
    </tr>
    </c:forEach>
    </table>
    ```

    ```jsp
    <%-- 2.遍历 Object 数组
    for (Object item: arr)
    items 表示遍历的数据源（遍历的集合）
    var 表示当前遍历到的数据
    --%>
    <%
    request.setAttribute("arr", new String[]{"18610541354","18688886666","18699998888"});
    %>
    <c:forEach items="${ requestScope.arr }" var="item">
    ${ item } <br>
    </c:forEach>
    ```

    ```jsp
    <%
    Map<String,Object> map = new HashMap<String, Object>();
    map.put("key1", "value1");
    map.put("key2", "value2");
    map.put("key3", "value3");
    // for ( Map.Entry<String,Object> entry : map.entrySet()) {
    // }
    request.setAttribute("map", map);
    %>
    <c:forEach items="${ requestScope.map }" var="entry">
    <h1>${entry.key} = ${entry.value}</h1>
    </c:forEach>
    ```

    ```jsp
    public class Student {
    //4.编号，用户名，密码，年龄，电话信息
    private Integer id;
    private String username;
    private String password;
    private Integer age;
    private String phone;
    示例代码：
    <%--4.遍历 List 集合---list 中存放 Student 类，有属性：编号，用户名，密码，年龄，电话信息--%>
    <%
    List<Student> studentList = new ArrayList<Student>();
    for (int i = 1; i <= 10; i++) {
    studentList.add(new Student(i,"username"+i ,"pass"+i,18+i,"phone"+i));
    }
    request.setAttribute("stus", studentList);
    %>
    <table>
    <tr>
    <th>编号</th>
    <th>用户名</th>
    <th>密码</th>
    <th>年龄</th>
    <th>电话</th>
    <th>操作</th>
    </tr>
    <%--
    items 表示遍历的集合
    var 表示遍历到的数据
    begin 表示遍历的开始索引值
    end 表示结束的索引值
    step 属性表示遍历的步长值
    varStatus 属性表示当前遍历到的数据的状态
    for（int i = 1; i < 10; i+=2）
    --%>
    <c:forEach begin="2" end="7" step="2" varStatus="status" items="${requestScope.stus}" var="stu">
    <tr>
    <td>${stu.id}</td>
    <td>${stu.username}</td>
    <td>${stu.password}</td>
    <td>${stu.age}</td>
    <td>${stu.phone}</td>
    <td>${status.step}</td>
    </tr>
    </c:forEach>
    </table>
    ```

    

### 文件上传部分

文件上传和下载是很常见的功能，如软件中的上传头像或者邮箱中的附件上传和下载

* 文件上传的操作步骤：

  * 要有一个form标签，并且method=post

  * form标签的encType属性的值必须为multipatr/form-data值

  * 在form标签中使用input type=file添加上传的文件

  * 编写服务器代码(Servlet程序)接收，处理上传到数据

  * encType=multipart/form-data 表示提交的数据，以多段（每一个表单项一个数据段）的形式进行拼 接，然后以二进制流的形式发送给服务器

  * ```html
    <form action="http://192.168.31.74:8080/09_EL_JSTL/uploadServlet" method="post"
    enctype="multipart/form-data">
    用户名：<input type="text" name="username" /> <br>
    头像：<input type="file" name="photo" > <br>
    <input type="submit" value="上传">
    </form>
    ```

  * ```java
    /**
    * 用来处理上传的数据
    * @param req
    * @param resp
    * @throws ServletException
    * @throws IOException
    */
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
    IOException {
    //1 先判断上传的数据是否多段数据（只有是多段的数据，才是文件上传的）
    if (ServletFileUpload.isMultipartContent(req)) {
    // 创建 FileItemFactory 工厂实现类
    FileItemFactory fileItemFactory = new DiskFileItemFactory();
    // 创建用于解析上传数据的工具类 ServletFileUpload 类
    ServletFileUpload servletFileUpload = new ServletFileUpload(fileItemFactory);
    try {
    // 解析上传的数据，得到每一个表单项 FileItem
    List<FileItem> list = servletFileUpload.parseRequest(req);
    // 循环判断，每一个表单项，是普通类型，还是上传的文件
    for (FileItem fileItem : list) {
    if (fileItem.isFormField()) {
    // 普通表单项
    System.out.println("表单项的 name 属性值：" + fileItem.getFieldName());
    // 参数 UTF-8.解决乱码问题
    System.out.println("表单项的 value 属性值：" + fileItem.getString("UTF-8"));
    } else {
    // 上传的文件
    System.out.println("表单项的 name 属性值：" + fileItem.getFieldName());
    System.out.println("上传的文件名：" + fileItem.getName());
    fileItem.write(new File("e:\\" + fileItem.getName()));
    }
    }
    } catch (Exception e) {
    e.printStackTrace();
    }
    }
    }
    ```

  * 文件上传的请求内容![文件上传](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\文件上传.PNG)

* 上传和用到的jar包和类

  * commons-fileupload.jar包与commons-io.jar包
  * 在这两个包中有一些常用的类和方法：
    * ServletFileUpload类：
      * boolean isMultipartContent(HttpServletRequest request)方法可以判断当前上传的数据格式是否是多段的格式
      * public List parseRequest(HttpServletRequest request) 方法可以解析上传的数据
      * boolean FileItem.isFormField() 方法可以判断当前这个表单项，是否是普通的表单项。还是上传的文件类型。 true 表示普通类型的表单项 false 表示上传的文件类型
      * String FileItem.getFieldName() 方法可以获取表单项的 name 属性值
      * String FileItem.getString() 方法可以获取当前表单项的值。
      * String FileItem.getName()方法可以获取上传的文件名
      * void FileItem.write( file ) 方法可以将上传的文件写到参数 file 所指向抽硬盘位置

* 使用fileupload类库

  我们在上传数据的时候，要先判断上传的数据是否是多段数据，只有多段的数据才是文件上传的，使用例：

  ```HTML
  <form action="http://192.168.31.74:8080/09_EL_JSTL/uploadServlet" method="post"
  enctype="multipart/form-data">
  用户名：<input type="text" name="username" /> <br>
  头像：<input type="file" name="photo" > <br>
  <input type="submit" value="上传">
  </form>
  ```

  ```java
  /**
  * 用来处理上传的数据
  * @param req
  * @param resp
  * @throws ServletException
  * @throws IOException
  */
  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
  IOException {
  //1 先判断上传的数据是否多段数据（只有是多段的数据，才是文件上传的）
  if (ServletFileUpload.isMultipartContent(req)) {
  // 创建 FileItemFactory 工厂实现类
  FileItemFactory fileItemFactory = new DiskFileItemFactory();
  // 创建用于解析上传数据的工具类 ServletFileUpload 类
  ServletFileUpload servletFileUpload = new ServletFileUpload(fileItemFactory);
  try {
  // 解析上传的数据，得到每一个表单项 FileItem
  List<FileItem> list = servletFileUpload.parseRequest(req);
  // 循环判断，每一个表单项，是普通类型，还是上传的文件
  for (FileItem fileItem : list) {
  if (fileItem.isFormField()) {
  // 普通表单项
  System.out.println("表单项的 name 属性值：" + fileItem.getFieldName());
  // 参数 UTF-8.解决乱码问题
  System.out.println("表单项的 value 属性值：" + fileItem.getString("UTF-8"));
  } else {
  // 上传的文件
  System.out.println("表单项的 name 属性值：" + fileItem.getFieldName());
  System.out.println("上传的文件名：" + fileItem.getName());
  fileItem.write(new File("e:\\" + fileItem.getName()));
  }
  }
  } catch (Exception e) {
  e.printStackTrace();
  }
  }
  }
  ```

  

### 文件下载部分

文件下载的操作只与上传有些许不同，步骤：

* 获取要下载的文件名

* 读取要下载的文件内容(通过ServletContext对象的getResourceAsStream()方法读取)

* 把下载的文件内容回传给客户端

* 在回传前，通过响应头告诉客户端返回的数据类型

* 通过响应头告诉客户端收到的数据是用于下载的

* 文件下载的API说明：

  * response.getOutputStream()
  * servletContext.getResourceAsStream()
  * servletContext.getMimeType()
  *  response.setContentType()
  * response.setHeader("Content-Disposition", "attachment; fileName=1.jpg")这个响应头告诉浏览器。这是需要下载的。而 attachment 表示附件，也就是下载的一个文件。fileName=后面表示下载的文件名

* 如果客户端浏览器是 IE 浏览器 或者 是谷歌浏览器。我们需要使用 URLEncoder 类先对中文名进行 UTF-8 的编码 操作。 因为 IE 浏览器和谷歌浏览器收到含有编码后的字符串后会以 UTF-8 字符集进行解码显示。

*  // 把中文名进行 UTF-8 编码操作。 

  String str = "attachment; fileName=" + URLEncoder.encode("中文.jpg", "UTF-8"); 

  // 然后把编码后的字符串设置到响应头中 

  response.setHeader("Content-Disposition", str);

## 项目优化

* 将原本的HTML页面变为动态的jsp页面
  * 需要在HTML页面的头部添加page指令，然后将后缀名改为jsp
  
  * 抽取页面中相同的内容
  
    * 将多个页面中相同的内容写在一个jsp页面中，然后在需要这些内容的页面里使用<%include file = "引用的jsp页面路径">来静态包含jsp页面。
  
  * 使用动态base标签地址
  
    * 当我们引用jsp页面时，其中若是包含了base标签的地址，不用动态获取的话容易出错，我们可以使用<%String basePath>标签来设置动态的base路径，在其中使用request.getScheme()获取协议，请求的id，端口，路径等，要把地址写完整。做完以上操作我们可以在base标签的href属性中写上<%=basePath%>就设置好动态base地址了
  
  * 表单提交失败回传信息
  
    * 要回显的数据要放在Request域中，然后在相应地方引用即可
  
  * 在一个项目中，一个模块的功能一般只用一个Servlet程序实现，可通过在jsp页面中添加隐藏域，然后通过请求来实现不同功能
  
  * 当代码有大量if else时，可用反射来进行简化，比如这样：
  
    Method method = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);
  
    method.invoke(this, req, resp);
  
  * 当几个业务代码(Servlet程序)中有一些共同的操作，我们可用将这些内容放到一个类中，让我们的业务代码去继承这个类，就可以不用写这些重复代码了
  
  * BeanUtils工具类：这个东西可用一次性的将所有的请求参数注入JavaBean中，这个东西不是官方JDK中的类，是一个第三方的库，这个类中的一个populate()方法可以获取所有的请求参数并在JavaBean中注册
  
  * 表达式脚本可用EL表达式代替
  
* 项目的后端(以书城为例)：

  * 编写图书模块的数据库表
  * 编写图书模块的JavaBean
  * 编写图书模块的Dao
  * 编写图书模块的Service
  * 编写图书模块的Web层

## MVC架构

ModelViewController,模型视图控制器,它最早出现在web层，指导web层的代码的分离，单独工作，这个东西是一种思想，它主要是为了解耦，能让各层代码分开独立工作，便于维护升级

Model:业务处理，业务逻辑(service)，数据持久层DRUD(Dao)

View:页面视图，JSP页面这样的,展示数据，提供链接发起Servlet请求（a,form,img..）

Controller:即servlet程序，控制各种数据,接收用户的请求(请求参数，Session信息)，交给业务层处理对应的代码，控制视图的跳转



![JavaMVC](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\JavaMVC.PNG)















## Cookie部分

Cookie是服务器通知客户端保存键值对的一项技术，客户端有了Cookie后，每次请求都发送给服务器。且Cookie的大小不能超过4kb,它是一个浏览器的对象,

* Cookie是一个类，它的创建方法：![cookie](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\cookie.PNG)

  ```java
  protected void createCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
  IOException {
  //1 创建 Cookie 对象
  Cookie cookie = new Cookie("key4", "value4");
  //2 通知客户端保存 Cookie
  resp.addCookie(cookie);
  //1 创建 Cookie 对象
  Cookie cookie1 = new Cookie("key5", "value5");
  //2 通知客户端保存 Cookie
  resp.addCookie(cookie1);
  resp.getWriter().write("Cookie 创建成功");
  }
  ```

* 服务器获取Cookie的方法：req.getCookies()，可以获取Cookie信息的数组,Cookie对象的getName()和getValue()可以拿取里面的名字和值

* Cookie还可以由JavaScript来创建:document里面就由一个创建Cookie的方法.

## Session部分

Session会话:服务器会给每一个用户创建一个Session对象,一个Session独占一个浏览器,只要浏览器没有关闭,这个Session就会一直存在.用户登录之后,整个网站都可以用它访问(它可以保存用户信息等).

Session对象中常用的方法:

getId():返回一个String

getServletContext():返回一个ServletContext对象

getAttribute(String s):返回一个Obj对象

setAttribute(String s, Obj obj):void :设置名为s,类型为Obj的obj东西,并且这个东西不管是请求重定向还是转发,这个属性都不会丢失.

removeAttribute(String s):void

invalidate():void:注销掉当前Session,相当于关了浏览器

在web.xml中可以设置Session默认的失效时间:

<session-config>

<session-timeout>15<session-timeout/>表示15分钟后Session失效

<session-config/>

isNew():boolean

```java
//Session
//创建一个类,继承HttpServlet
public class SessionDemo extends HttpServlet{
    protected void doGet(HttpServletRequest req,HttpServletResponse resp){
        HttpSession session = req.getSession();//获取Session对象
        session.setAttribute("name","名字");//给session对象中存东西
        String id = session.getId();//获取session的ID
        boolean new = session.isNew();//判断session是不是新创建的
        
    }
}
```

Session在创建的时候:我们在浏览器抓包会发现它还产生了一个Cookie,而且这个Cookie的ID是一个固定的串加上Session的ID,

* Session与Cookie的区别
  * Cookie是把用户的数据写给用户的浏览器,可以持久化保存在客户端浏览器上,可以保存很多
  * Session是把用户数据放在用户的Session中,它是在服务器里面保存的,一般是保存重要资源的,以减少服务器资源的浪费
  * Session对象由服务器创建

* Session使用场景
  * 保存登录用户的信息
  * 购物车信息
  * 反正就是在整个网站中经常会使用的数据

当一个用户访问网站的时候,如果是第一次来访问的话,服务器就会给用户发一个Cookie,后面的访问就可以携带该Cookie,而Session是用户在来的时候就会进行登记,用户会拿到一个Session的ID,服务器里面的Session存的东西是通过Session的ID来区分用户的,ServletContext(ApplicationContext)的话跟这些差不多,不过是在中间的一层,如果我们要用到复杂的资源共用,比如两个用户需要访问相同的资源,或者服务器要统计访问人数,那么Session和Cookie就不能做到了,这个时候得用ServletContext来做,它后面有个别名叫ApplicationContext















## Filter部分

这个就是过滤器，跟Servlet很像，实现这个东西跟写Servlet程序基本一致，只不过继承的不是HttpServlet，是Filter，然后重写一些方法。要导入的包是javax.Servlet包里的Filter类，千万不能写错。init方法是初始化的时候进行的操作，这个方法会在web服务器启动的时候就执行，在web服务器关闭的时候才会销毁。

主要写doFilter方法，过滤器可以在获取或者回传数据的时候先对请求或数据做一些操作，完成操作后要使用chain.doFilter(request,response)方法，否则请求会中断。写完程序后要在配置文件中用<filter>和<filter-mapping>标签注册过滤器

### 监听器

实现一个监听器的接口:（监听器的接口非常的多，用对应的就行）重写的方法有监听器方法和销毁监听器方法。

也要在配置文件中用<listener>标签来注册监听器

## JSON部分

## AJAX部分

## _i18n国际化部分