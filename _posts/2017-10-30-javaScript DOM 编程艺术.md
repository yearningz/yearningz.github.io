---
layout: post
title: 《javaScript DOM 编程艺术》-入门系列
key: 20171030
tags: javascript
---
#### 1. javascript简史 
#### 2. 语法
1. 变量名包含数字_$字母（第一个不能是数字）
1. 使用var申明的变量则不是全局变量，它的范围被限制在该变量被申明的函数体内，同名变量在不同的函数体内互不冲突。
2. 驼峰格式或下划线格式
== 空字符串与false判断相等 !=
=== 比较值和类型。!==
函数可当作一种数据类型来使用，可以把一个函数的调用结果赋给一个变量。  
变量：my_abc.   
函数：myAbc
全局变量：在脚本中的任意位置
局部变量：声明在函数内部。
 
#### 3. DOM
* 内建对象：array\math\date
* 宿主对象：form\image\element\body
* 用户定义对象：自行创建

1.getElementById   
2.getElementByTagName  
3.getElementByClassName   
4.getAttribute.   
5.setAttribute.   
6.createElement.   
7.createTextNode.  
8.appendChild.   
9.insertBefore.     

window对象 对应着浏览器窗口本身，BOM（browser object model)


#### 4.案例研究：javascript图片库
#### 5.最佳实践
> 1.尽量少访问DOM和尽量减少标记
> 2.合并和放置脚本
> 3.压缩脚本
> 
> tab键+链接=onclick(). 

#### 6.案例 
#### 7.动态创建标记
js:
setAttribute.   
nodeValue.     
document.write: -> innerHTML    

文本节点。 
元素节点 

ajax优势：对页面请求以异步形式发送到服务器.   
XMLHttpRequest
#### 8.充实文档的内容
渐进增强：从最核心的部分开始   
平稳退化：利用DOM去生成内容有着广泛的用途。    
<abbr> 标签，“缩略语”。  
<!DOCTYPE html> 使用html5的文档类型声明。
键盘快捷键：   
accesskey="1" 对应着“返回到本网站主页”。  
accesskey="2" 对应着“后退到前一页面”的连接。  
accesskey="4 对应着“打开本网站的搜索表单／页面”。  
accesskey="9" 对应着“本网站联系办法”。  
accesskey="0" 对应着“查看本网站的快捷键清单”的链接。  

#### 9.CSS-DOM    
> 结构层：html  
> 表示层 :css
> 行为层 : js
> 
element.style.color. 
  
```
p{}. 
.app{}
#app{}. 
input[type='text']{}
p:first-of-type{}
p:nth-child{}
p:nth-of-type{}

```   
addLoadEvent 添加函数绑定。
#### 10.用javascript实现动画效果   
setTimeout("function",interval)
clearTimeout(variable). 

overflow:  
1.visible 全部内容可见   
2.hidden 隐藏溢出内容   
3.scroll 有滚动条  
4.auto 内容溢出才有

##### 11.HTML5  
canvas:  画布  
video: 视频   
audio:  音频   
1.localStorage和sessionStorage. 
2.websocket. 
3.web worker. 


---
**1.字符串**
> 字符串是不可变的.对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果  
> 常用方法：toUpperCase、toLowerCase、indexOf、substring. 

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

const 常量. 
> let 变量，块作用域，不能重复声明覆盖
> var 变量，函数作用域，能重复声明覆盖.      

赋值之后不会再做修改了就用const，如果后边还会修改就用let，不建议使用var.   
运行代码，如果浏览器报错，请修复后再运行。如果浏览器不报错，说明你的浏览器太古老了，需要尽快升级。

不用var申明的变量会被视为全局变量，为了避免这一缺陷，所有的JavaScript代码都应该使用strict模式。我们在后面编写的JavaScript代码将全部采用strict模式。

由于JavaScript的对象是动态类型.     
> 如果我们要检测xiaoming是否拥有某一属性，可以用in操作符：
> 要判断一个属性是否是xiaoming自身拥有的，而不是继承得到的，可以用hasOwnProperty()方法：

遍历Array可以采用下标循环，遍历Map和Set就无法使用下标。为了统一集合类型，ES6标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。

具有iterable类型的集合可以通过新的for ... of循环来遍历。  
由于JavaScript引擎在行末自动添加分号的机制

JavaScript的函数可以嵌套.  

正则表达式：     
+ 至少出现1次    
* 前面字符最多可出现1次    
{n} 匹配确定n次.    
{n,}至少匹配n次.      
{n,m}至少匹配n次，至多m次.   

test() 检索指定值，返回true或false.  
exec() 检索字符中指定值，返回找到值.  g:全局，i：不区分大小，m:多行。    
compile() 返回regexp. 

---

#### 编程习惯
map/reduce. 

filter. 

sort
