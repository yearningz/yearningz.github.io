---
layout: post
title: webpack&grunt&gulp&rollup等构建工具
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
## grunt
[grunt](http://www.gruntjs.net/getting-started)