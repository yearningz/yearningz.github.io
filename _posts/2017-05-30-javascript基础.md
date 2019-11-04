---
layout: post
title: javascript、html、css基础
key: 20170530
tags: javascript
---
### javascript基础
[廖雪峰-官方教程](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000)  

#### 1. 基础内容  

ECMAScript是一种语言标准，JavaScript是对ECMAScript标准的一种实现。  
> 注释：//和／**／  
> 类型：7种，Number、字符串、布尔值、数组、对象、null和undefined
> 运算符：比较

1.使用iterable 内置的forEach方法。接收一个函数，每次迭代就自动回调该函数。
2.有JavaScript引擎在行末自动添加分号机制。

#### 2. 严格模式
1. 在同一个页面的不同的JavaScript文件中，如果都不用var申明，恰好都使用了变量i，将造成变量i互相影响，产生难以调试的错误结果。
1. 使用var申明的变量则不是全局变量，它的范围被限制在该变量被申明的函数体内，同名变量在不同的函数体内互不冲突。

#### 3. 对象操作
**1.字符串**
> 字符串是不可变的.对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果  
> 常用方法：toUpperCase、toLowerCase、indexOf、substring。

**2.数组**

remove(). 
detach()绑定事件还在。

empty()清空节点  
clone()复制元素同时复制元素的绑定事件

prop()获取匹配元素集中的第一个元素的属性值

$(document).ready()只要dom就绪  
window.onload 完全加载

NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
由于JavaScript这个设计缺陷，不要使用==比较，始终坚持使用===比较。

const 常量
let 变量，块作用域，不能重复声明覆盖
var 变量，函数作用域，能重复声明覆盖    

赋值之后不会再做修改了就用const，如果后边还会修改就用let，不建议使用var.     

运行代码，如果浏览器报错，请修复后再运行。如果浏览器不报错，说明你的浏览器太古老了，需要尽快升级。

不用var申明的变量会被视为全局变量，为了避免这一缺陷，所有的JavaScript代码都应该使用strict模式。我们在后面编写的JavaScript代码将全部采用strict模式。

由于JavaScript的对象是动态类型.     
> 如果我们要检测xiaoming是否拥有某一属性，可以用in操作符：
> 要判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法：

遍历Array可以采用下标循环，遍历Map和Set就无法使用下标。为了统一集合类型，ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。

具有iterable类型的集合可以通过新的for ... of循环来遍历。  
由于JavaScript引擎在行末自动添加分号的机制

JavaScript的函数可以嵌套

#### 高阶函数
map/reduce. 

filter

sort

### html 基础
\<br />折行 
\<hr />水平线

\<!--这是一段注释。注释不会在浏览器中显示。-->. 
 
\<body bgcolor="yellow"> html背景颜色  
\<b> 粗体字   
电子邮件 \<a href="mailto:xxx@yyy">   
在html中，插入背景图像：\<background img="background.gif">   
\<bdi> 脱离其父元素文本方向

sessionStorage: 对一次session进行数据存储
localStorage：没有时间限制的数据存储   
cookie : 生命期为只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。 存放数据大小为4K左右 。有个数限制（各浏览器不同），一般不能超过20个。与服务器端通信：每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题。但Cookie需要程序员自己封装，源生的Cookie接口不友好. 

[localStorage、sessionStorage、Cookie的区别及用法](https://segmentfault.com/a/1190000012057010)  

[localStorage、sessionStorage、Cookie的区别及用法2](https://www.jianshu.com/p/f7b81e101a8c)  

相同浏览器的不同页面间可以共享相同的 localStorage（页面属于相同域名和端口），但是不同页面或标签页间无法共享sessionStorage的信息。  

页面及标 签页仅指顶级窗口，如果一个标签页包含多个iframe标签且他们属于同源页面，那么他们之间是可以共享sessionStorage的。  

web worker 是运行在后台的 JavaScript，不会影响页面的性能

for(var key in o){
    if(o.hasOwnProperty(key){}//过滤对象继承的属性
}
hasOwnProperty(key)是对象的属性  

map和set

for of ...  只循环集合本身的元素。  

var a = ['a','b','c'];
a.forEach(function(e,index,array){
});

由于javascript允许传入任意个参数而不影响调用，故传入的参数比定义的参数多也没有问题。    
javascript默认有一个全局对象window

##名字空间
减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中

用 var that = this;就可以在方法内部定义其他函数，而不是把所有语句堆到一个方法中。

##闭包     
[闭包](http://www.jb51.net/article/83524.htm）
有权访问另一个函数作用域内变量的函数都是闭包
返回函数不要引用任何循环变量，或者后续会发生变化的变量。   
闭包，即携带状态的函数，并且其状态可以完全对外隐藏起来。  

cookie是由服务器发送的key-value标示符，由于http协议是无状态的，服务器要区分具体是哪个用户发出来的请求，就可以用cookie来区分。当用户成功登录之后，服务器发送一个cookie给浏览器，此后，浏览器访问该网站时，会在请求头附上这个cookie，服务器根据cookie即可区分出用户。cookie是浏览器窗口共享。
服务器在设置cookie时可以使用httpOnly，设定了httpOnly的Cookie将不能被javascript读取。

正常情况下，不应该使用history这个对象。  

innerHTML用时注意，若写入字符是通过网络拿到了，要注意对字符编码来避免xss攻击。   
html表单：  
口令框，对应的<input type="password">，用于输入口令；

单选框，对应的<input type="radio">，用于选择一项；

复选框，对应的<input type="checkbox">，用于选择多项；

下拉框，对应的<select>，用于选择一项；

隐藏文本，对应的<input type="hidden">，用户不可见，但表单提交时会把隐藏文本发送到服务器。  

### node.js   
1.node命令进入交互模式，可以一步一步看结果
2.node a.js 会直接运行，直接输出结果