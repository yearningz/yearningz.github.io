---
layout: post
title: webpack&grunt&gulp&rollup等打包工具
key: 20170420
tags: webpack grunt gulp 
---

## Webpack  
   
定义      

*  webpack 是一个模块打包器。它的主要目标是将 JavaScript 文件打包在一起，打包后的文件用于在浏览器中使用，但它也能够胜任转换(transform)、打包(bundle)或包裹(package)任何资源(resource or asset)。     
   
webpack就以这个初始js文件为「入口」，根据代码中声明的模块引用来加载其他资源文件，根据webpack配置来对加载的模块进行编译、打包，最终「输出」开发人员期望的打包结果。  
### 基本配置      
入口[entry]  
出口[output]    
path与publicPath  
模块[module]  
*loader 用于对模块的源代码进行转换。loader 可以使你在 import 或 "加载" 模块时预处理文件。*
*chunk:将一个webpack打包出的一个js文件认为是一个chunk*  
# webpack
默认文件webpack.config.js
### 入口
**可以将应用程序的入口起点认为是根上下文(contextual root) 或 app 第一个启动文件。**
### Output
在 webpack 中配置 output 属性的最低要求是，将它的值设置为一个对象，包括以下两点：

* filename 用于输出文件的文件名。
* 目标输出目录 path 的绝对路径。

```
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
         
```                        
### Loader

loader 用于对模块的源代码进行转换。loader 可以使你在 import 或"加载"模块时预处理文件。因此，loader 类似于其他构建工具中“任务(task)”，并提供了处理前端构建步骤的强大方法。loader 可以将文件从不同的语言（如 TypeScript）转换为 JavaScript，或将内联图像转换为 data URL。loader 甚至允许你直接在 JavaScript 模块中 import CSS文件！

在更高层面，在 webpack 的配置中 loader 有两个目标。
识别出(identify)应该被对应的 loader 进行转换(transform)的那些文件。(test 属性)
转换这些文件，从而使其能够被添加到依赖图中（并且最终添加到 bundle 中）(use 属性)  
*exclude:  除去这个目录中内容*
### 插件
插件是 wepback 的支柱功能。webpack 自身也是构建于，你在 webpack 配置中用到的相同的插件系统之上！

插件目的在于解决 loader 无法实现的其他事。  

[起步开始](https://www.webpackjs.com/guides/getting-started/)
起步-管理资源-管理输出-开发-模块热替换-tree shaking-生产环境构建-代码分离-懒加载
## grunt
[grunt](http://www.gruntjs.net/getting-started)
## gulp