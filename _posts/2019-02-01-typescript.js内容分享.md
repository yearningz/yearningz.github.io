---
layout: post
title: TypeScript的内容分享
key: 20190201
tags: 前端 javascript TypeScript
---      

### 定义    
[TypeScript](https://github.com/Microsoft/TypeScript) 是 JavaScript 的一个*超集*，它由 Microsoft 开发，可以编译成纯javaScript。TypeScript可以在任何浏览器、任何计算机和任何操作系统上运行，并且是*开源*的。      

**优点**  
1、提供了*类型系统*，增加了代码的可读性和可维护性。       
  
* 类型系统实际上是最好的文档，大部分的函数看看类型的定义就可以知道如何使用了  
* 可以在编译阶段就发现大部分错误，这总比在运行时候出错好。  
* 增强了编辑器和 IDE 的功能，包括代码补全、接口提示、跳转到定义、重构等。    

2、包容性强       
  
* .js 文件可以直接重命名为 .ts 
* 即使不显式的定义类型，也能够自动做出类型推论   
* 可以定义从简单到复杂的几乎一切类型   
* 即使 TypeScript 编译报错，也可以生成 JavaScript 文件   
* 兼容第三方库，即使第三方库不是用 TypeScript 写的，也可以编写单独的类型文件供 TypeScript 读取。    

3、TypeScript 拥有活跃的社区。    
![img](/statics/images/typescript.png)    
**缺点**  
* 有一定学习成本，需要理解接口（Interfaces）、泛型（Generics）、类（Classes）、枚举类型（Enums）、装饰器、反射等概念。   
* 短期可能会增加一些开发成本，毕竟要多写一些类型的定义，不过对于一个需要长期维护的项目，TypeScript 能够减少其维护成本。       


### 前景       
    
![img](/statics/images/rank.png)    

基于TS开发的项目越来越多    

* angular2
* ant-design
* VSCode
* babel7.0
* WebAssembly 
* vue 2.5    

**美团高性能跨平台动态化框架Picasso** 
![img](/statics/images/picasso.png)       

1.Picasso开发人员用TypeScript在VSCode中编写Picasso应用程序。    
2.提交代码后可以通过Picasso持续集成系统自动化的完成Lint检查和打包，在Picasso分发系统进行灰度发布.   
3.Picasso应用程序最终以JavaScript包的形式下发到客户端，由Picasso SDK解释执行，达成客户端业务逻辑动态化的目的。

**场景**   
1.静态类型检查    

```  
interface Profile {
  name: string;
  gender: 'man' | 'woman';
  age: number;
  height?: number;
}

function printProfile(profile: Profile) {
  console.log('name', profile.name);
  console.log('gender', profile. gender);
  console.log('age', profile.age);
  if (profile.height) {
    console.log('height', profile.height);
  }
}

printProfile({name: 'GuangWong', gender: 'man', age: 23});//通过   
printProfile({name: 'GuangWong', age: 23});//报错

```  
> tsc taste.ts
x.ts(19,14): error TS2345: Argument of type '{ name: string; age: number; }' is not assignable to parameter of type 'Profile'.
  Property 'gender' is missing in type '{ name: string; age: number; }'.   
  
接着传非number的height试下     

```  
printProfile({height: '190cm', name: 'GuangWong', gender: 'man', age: 23});      
```     
     
报错
> tsc taste.ts
x.ts(17,14): error TS2345: Argument of type '{ height: string; name: string; gender: "man"; age: number; }' is not assignable to parameter of type 'Profile'.
  Types of property 'height' are incompatible.
    Type 'string' is not assignable to type 'number'.
  
2.有一个很通用的函数，在工程里用的到处都是，有一天我们要在这个函数最前面增加一个参数。TypeScript 中你只需要改那个函数就好了，然后再执行静态类型分析，所有和这个函数参数不匹配的地方都会提示出来。  

3.控制流。    
  
```
function getDefaultValue (key, emphasis) {
  let ret;
  if (key === 'name') {
    ret = 'GuangWong';
  } else if(key=== 'gender') {
    ret = 'Man';
  } else if (key === 'age') {
    ret = 23;
  } else {
     throw new Error('Unkown key ' + info.type);
  }
  if (emphasis) {
    ret = ret.toUpperCase();
  }
  return ret;
}

getDefaultValue('name'); // GuangWong
getDefaultValue('gender', true) // MAN
getDefaultValue('age', true) // Error: toUpperCase is not a function
```                


> tsc taste.ts   
> x.ts(8,5): error TS2322: Type '23' is not assignable to type 'string'.
 
    
### 快速上手   
1.npm install -g typescript  
2.安装Visual Studio的TypeScript插件。(Visual Studio 2017和Visual Studio 2015 Update 3默认包含了TypeScript)

**构建**  
1.新建greeter.ts文件.  
  
```
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.innerHTML = greeter(user);
```  

2.tsc greeter.ts     
 
```
function greeter(person) {
    return "Hello, " + person;
}
var user = "Jane User";
document.body.innerHTML = greeter(user); 
```     

**示例**    
 
 ```    	
function greeter(person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}
 ```        
 我们可以推断 person 参数应该是具有 firstName 和 lastName 属性的 Object。但在运行时我们不能保证一定会是这样的。

项目越大，与类型相关的错误发生的几率就越高。   
为了避免出现这类错误，可以使用运行时类型检查和单元测试，如下所示：
 ```  
 function greeter(person) {
    if (!person || !person.firstName || !person.lastName) {
        throw new Error('invalid arguments');
    }

    return "Hello, " + person.firstName + " " + person.lastName;
}

// Jasmine spec:
describe("greeter", function() {
    it("returns greeting on valid input", function() {
        expect(
            greeter({firstName: 'James', lastName: 'Hetfield'})
        ).toEqual('Hello, James Hetfield');
    });

    it("throws on invalid input", function() {
        expect(() => greeter()).toThrowError('invalid arguments');
        expect(() => greeter(5)).toThrowError('invalid arguments');
        expect(() => greeter({firstName: 'Jason'})).toThrowError('invalid arguments');
    });
});   
 ```   
  
 增加类型注解后：      
    
```  
 interface Person {
    firstName: string;
    lastName: string;
}
 
function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}
 
// Jasmine spec:
describe("greeter", function() {
    it("returns greeting", function() {
        expect(
            greeter({firstName: 'James', lastName: 'Hetfield'})
        ).toEqual('Hello, James Hetfield');
    });
});   

```    
 
### 基础
**基本类型**       
[类型介绍](http://naotu.baidu.com/file/49445101e4b8de8c3a333b2c942b35a0?token=858c9c77ddc2e16b) 
   
**类型推论**  
TypeScript 会在没有明确的指定类型的时候推测出一个类型，这就是类型推论。   
如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成 any 类型而完全不被类型检查。    
原则包括：   
最佳通用类型和上下文类型    
 
**类**      
在TypeScript里，我们可以使用常用的面向对象模式。  
  
``` 
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}
let greeter = new Greeter("world");  
  
```   
继承     
 
```   
class Animal {
    name: string;
    constructor(theName: string) { this.name = theName; }
    move(distanceInMeters: number = 0) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}

class Snake extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 5) {
        console.log("Slithering...");
        super.move(distanceInMeters);
    }
}

class Horse extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 45) {
        console.log("Galloping...");
        super.move(distanceInMeters);
    }
}

let sam = new Snake("Sammy the Python");
let tom: Animal = new Horse("Tommy the Palomino");

sam.move();
tom.move(34);  
```   
**公共，私有与受保护的修饰符**   
在TypeScript里，成员都默认为 public。    
      
|    修饰符         | 含义|
| :----------: | :-----:|
|public|成员自由访问| 
| private | 只能在声明类内部访问 |
| protected |派生类可访问|
| readonly|只读属性必须在声明时或构造函数里被初始化|      

java       
  
|    修饰符         | 含义|
| :----------: | :-----:|
|public|成员自由访问| 
| private | 只能在声明类内部访问 |
| protected |同一包的类及其子类可访问|
| 默认 |同一包的类可访问|
|static |对该类所有对象来说，只有一个类成员存在|
| final|必须在创建它时赋值且不能更改|   
| transient|在类对象序列化时，此变量不需要持久保存|   
| volatile|确保多个线程共享变量的值发生变化时的可见性|   

**接口**  
TypeScript的核心原则之一是对值所具有的结构进行类型检查。      
1.接口只能被实现，不能实例化。   
2.当类实现接口时，必须将接口当中所有的方法全部实现。   
3.接口可以多实现，在一定程度上弥补了类不能多继承的缺陷，实现多个接口，接口之间使用逗号隔开。  
  
```  
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```    
在这里并不能像在其它语言里一样，说传给printLabel的对象实现了这个接口。我们只会去关注值的外形。 只要传入的对象满足上面提到的必要条件，那么它就是被允许的。   

可选属性（？）    

```  
interface SquareConfig {
  color?: string;
  width?: number;
}
```  
只读属性(readonly)    
    
```   
interface Point {
    readonly x: number;
    readonly y: number;
}     
```    
TypeScript具有ReadonlyArray<T>类型.     
 
*readonly vs const.  
最简单判断该用readonly还是const的方法是看要把它做为变量使用还是做为一个属性。 做为变量使用的话用 const，若做为属性则使readonly*    

类实现接口     

```
interface Alarm {
    alert();
}

class Door {
}

class SecurityDoor extends Door implements Alarm {
    alert() {
        console.log('SecurityDoor alert');
    }
}

class Car implements Alarm {
    alert() {
        console.log('Car alert');
    }
}  
``` 
接口继承接口    
     
``` 
interface Alarm {
    alert();
}

interface LightableAlarm extends Alarm {
    lightOn();
    lightOff();
}  
```     
接口定义函数类型  
  
``` 
interface SearchFunc {
    (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
    return source.search(subString) !== -1;
}  
```     
**函数**       
TypeScript函数可以创建有名字的函数和匿名函数      

```    
function add(x: number, y: number): number {
    return x + y;
}

let myAdd = function(x: number, y: number): number { return x + y; };    
```      
允许可选函数和默认值。   
允许重载      
   
**枚举**   
枚举（Enum）类型用于取值被限定在一定范围内的场景。    
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};

**联合类型**      
    
```  
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;  
```


**React和Webpack使用**     
初始化工程  
npm init   
安装依赖  
npm install -g webpack    
npm install --save react react-dom @types/react @types/react-dom  
npm install --save-dev typescript awesome-typescript-loader source-map-loader    
添加TypeScript配置文件  
1.创建一个[tsconfig.json文件](https://www.tslang.cn/docs/handbook/tsconfig-json.html)    
 
```   
{
  // 编译选项
  "compilerOptions": {
    // 输出目录
    "outDir": "./output",
    // 是否包含可以用于 debug 的 sourceMap
    "sourceMap": true,
    // 以严格模式解析
    "strict": true,
    // 采用的模块系统
    "module": "esnext",
    // 如何处理模块
    "moduleResolution": "node",
    // 编译输出目标 ES 版本
    "target": "es5",
    // 允许从没有设置默认导出的模块中默认导入
    "allowSyntheticDefaultImports": true,
    // 将每个文件作为单独的模块
    "isolatedModules": false,
    // 启用装饰器
    "experimentalDecorators": true,
    // 启用设计类型元数据（用于反射）
    "emitDecoratorMetadata": true,
    // 在表达式和声明上有隐含的any类型时报错
    "noImplicitAny": false,
    // 不是函数的所有返回路径都有返回值时报错。
    "noImplicitReturns": true,
    // 从 tslib 导入外部帮助库: 比如__extends，__rest等
    "importHelpers": true,
    // 编译过程中打印文件名
    "listFiles": true,
    // 移除注释
    "removeComments": true,
    "suppressImplicitAnyIndexErrors": true,
    // 允许编译javascript文件
    "allowJs": true,
    // 解析非相对模块名的基准目录
    "baseUrl": "./",
    // 指定特殊模块的路径
    "paths": {
      "jquery": [
        "node_modules/jquery/dist/jquery"
      ]
    },
    // typescript 语法检测支持的版本库，注意不是 polyfill！只是为了有对应版本的代码特性提示！
    "lib": [
      "es2015",
      "es2015.promise"
    ]
  }
}  
```       
  
2.创建webpack.config.js文件    
  
``` 
module.exports = {
    entry: "./src/index.tsx",
    output: {
        filename: "bundle.js",
        path: __dirname + "/dist"
    },

    // Enable sourcemaps for debugging webpack's output.
    devtool: "source-map",

    resolve: {
        // Add '.ts' and '.tsx' as resolvable extensions.
        extensions: [".ts", ".tsx", ".js", ".json"]
    },

    module: {
        rules: [
            // All files with a '.ts' or '.tsx' extension will be handled by 'awesome-typescript-loader'.
            { test: /\.tsx?$/, loader: "awesome-typescript-loader" },

            // All output '.js' files will have any sourcemaps re-processed by 'source-map-loader'.
            { enforce: "pre", test: /\.js$/, loader: "source-map-loader" }
        ]
    },

    // When importing a module whose path matches one of the following, just
    // assume a corresponding global variable exists and use that instead.
    // This is important because it allows us to avoid bundling all of our
    // dependencies, which allows browsers to cache those libraries between builds.
    externals: {
        "react": "React",
        "react-dom": "ReactDOM"
    }
};   
```      
**文档**   
> npm install -g typedoc   
typedoc hello.ts --module commonjs --out doc  

![img](/statics/images/readme.png)     

[JavaScript迁移](https://www.tslang.cn/docs/handbook/migrating-from-javascript.html)    
 
Typescript vs Flow  
1.生态圈，TypeScript 的生态圈明显在 Flow 之上，各大主流类库都提供了 TypeScript 的类型声明文件，配合 visual studio code 编码体验上比 Flow 强太多。   
2.Flow 是侵入 JavaScript 的，对 JavaScript 做了一层增强；而 TypeScript 则为 JavaScript 超集，在 JavaScript 之上进行的语言抽象，最终编译成 JavaScript。  

参考内容：  
[typescript.js官网](https://www.tslang.cn/docs/home.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
[TypeScript教程](https://ts.xcatliu.com/)  
[从 JavaScript 到 TypeScript 系列](https://tasaid.com/Blog/20171011231943.html?sgs=sf)
[Picasso开启大前端的未来](https://tech.meituan.com/2018/06/21/picasso-the-future.html)  
[2018 JavaScript 现状调查报告火热出炉](https://www.oschina.net/news/101954/the-state-of-javascript-2018)
