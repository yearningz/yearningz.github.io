---
layout: post
title: miniprogram执行环境
key: 20200815
tags: miniprogram
---  
### 微信小程序执行环境  
1.[小程序开发指南](https://developers.weixin.qq.com/ebook?action=get_post_info&token=935589521&volumn=1&lang=zh_CN&book=miniprogram&docid=0008aeea9a8978ab0086a685851c0a)   
 
 
 
| 名称 |说明 |  
| ----------  |  :-----:  |   
|神经网络|由简单处理单元组成的大规模并行处理器。受生物学启发的编程范式，让计算机从观测数据中进行学习。  |   
|人体神经识别|以视觉为例，视觉图像激发光感细胞，不同的视觉激发的光感细胞不同，依据大脑皮层中处理视觉的区域将不同信息匹配成同一信息。 |  
#### JS   
![数据绑定](/statics/images/2020-06/6.png)   
1. Promise的executor是一个**同步函数**，即非异步，立即执行的一个函数，因此他应该是和当前的任务一起执行的。  
2. Promise的链式调用then，每次都会在内部生成一个新的Promise，然后执行then，在执行的过程中不断向微任务(microtask)推入新的函数，因此直至微任务(microtask)的队列清空后才会执行下一波的macrotask。

**Event Loop：**    

* 第一步确认宏任务，微任务
* 宏任务：script，setTimeout，setImmediate，promise中的executor
* 微任务：promise.then，process.nextTick
* 第二步解析“拦路虎”，出现async/await不要慌，他们只在标记的函数中能够作威作福，出了这个函数还是跟着大部队的潮流。
*  第三步，根据Promise中then使用方式的不同做出不同的判断，是链式还是分别调用。
* 最后一步记住一些特别事件
* 比如，process.nextTick优先级高于Promise.then

**async/await：**  
[结论](https://developer.mozilla.org/zh-CN/docs/learn/JavaScript/%E5%BC%82%E6%AD%A5/Async_await)

### 理解
ECMAScript 6.0（以下简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。   
ECMAScript和JavaScript的关系是，前者是后者的规格，后者是前者的一种实现。
###

[30分钟掌握ES6/ES2015核心内容（上)](https://segmentfault.com/a/1190000004365693)   

[30分钟掌握ES6/ES2015核心内容（下)](https://segmentfault.com/a/1190000004368132)