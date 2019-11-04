---
layout: post
title: javaScript设计模式与开发实践
key: 20180914
tags: 前端 javascript
---    

### 1. 面向对象的JavaScript 
多态概念：  
不变的部分隔离起来，可变的部分封装起来。
类型检查和多态：可以考虑向上转型。  
继承和接口继承  

封装：  
使得对象内部的变化对其他对象而言是透明的，即不可见的。  
23种设计模式分为创建型模式、结构型模式和行为型模式。  

原型模式：   
基于原型链的委托机制就是原型继承的本质。原则：  
1.所有数据都是对象。  
2.要得到一个对象，不是实例化类，而是找到一个对象作为原型并克隆它。  
3.对象会记住它的原型。  
4.如果对象无法响应某个请求，它会把这个请求委托给自己的原型。  

```  
class Animal{
    constroctor(name){
        this.name=name;
    }
    getName(){
        return this.name;
    }
}
class Dog extends Animal{
    constructor(name){
        super(name);
    }
    speak(){
        return "woof";
    }
}
var dog = new Dog("scmap");
console.log(dog.getName()+ 'says'+dog.speak());  
```

### 2. this、call和apply  
*this*
指定一个对象，具体指向的对象是在运行时基于函数的执行环境动态绑定的，而非函数被声明时的环境。  
 1.作为对象的方法调用。  
 2.作为普通函数调用。  
 3.构造器调用。  
 4.Function.prototype.call或Function.prototype.apply调用。   
 
 在es5环境的strict模式下，this已经规定为不会指向全局对象，而是undefined。   
 使用new调用构造器时，如果构造器显示地返回了一个object对象，则此次结果最终会返回这个对象。
 call和apply方法可以很好地体现js的函数式语言特性。  
 apply 2个参数 第一个是函数内this对象指向，第二个为一个带下标的集合。apply方法可以把这个集合中的元素作为参考传递给被调用的函数。
 call传入的参数数量不固定，第一个参数也是代表函数体内的this指向，第二个是对应的参数。  
 
 **闭包**：可以访问函数作用域内的变量  
 用处：1.封装变量 2.延续局部变量的寿命。  
 闭包本身最好不好返回dom节点，与DOM和BOM中使用c++实现，易引起内存循环引用。  
 **高阶函数**  
 1.函数可以作为参数被传递。  
 2.函数可以作为返回值输出。
   
使用场景：  
1.函数作为参数传递。  
1.1回调函数    
1.2 array.prototype.sort.   
2.函数作为返回值输出
 
    


