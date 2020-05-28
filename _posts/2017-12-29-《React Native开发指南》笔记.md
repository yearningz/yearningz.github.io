---
layout: post
title: 《React Native开发指南》笔记 
key: 20171229
tags: RN 笔记
---
## 1 概念    
1. React Native 是使用JavaScript和React用来开发真正原生，可渲染IOS和Android移动应用的JavaScript框架。  
React Native 生命周期与React相同，当属性或状态发生改变时，React Native 会重新渲染视图，而于浏览器上的React最大的不同是在于，React Native使用了宿主平台上的UI元素来代替HTML和CSS。 

2. 在React中，virtual DOM类似中间层，介于开发者描述的视图与实际在页面上渲染的视图之间。开发者过度操作DOM对性能影响严重，react维护了一个内存版本的DOM，通过计算得出必要的最小操作并重新渲染。

3. React Native完美兼容使用Objective-C、Java或是Swift编写的组件。react native 调用object-c的api去渲染iOS组件，调用java接口去渲染android组件。

## 2 React Native的工作原理   

“桥接”技术使得React可调用宿主平台开放的UI组件。  

| React     | React Native | 
| --------   | -----:  | 
|\<div> | \<View> |
|\<span>| \<Text> |
|\<li>\<ul> | \<ListView> |
|\<img> | \<Image> |

使用类xml标记来代替调用React.createElement方法传入HTML属性的做法。

flow: facebook出的类型检查库。  
brew update
brew upgrade.  


es6语法：
1. 解构
2. 导入模块.  
commonJS规范
每个文件是一个模块，有自己的作用域，在一个文件里面定义的变量、函数
类、都私有。用时再加载。
> 1. 所有代码运行在模块作用域，不会污染全局作用域。
> 2. 模块可多次加载，只在第一次运行一次。
> 3. 模块加载顺序，按照其在代码中出现顺序。  

${}字符串赋值。
## 3 构建

**state**   
  
* 1. 一切界面变化都是状态state变化。  
* 2. 必须通过setState()方法

**CSS**     
   
* 1.驼峰命名法   
* 2.StyleSheet.create({})

**受控组件与非受控组件**      

1. 受控组件需要为数据变化的每种方式都编写事件处理函数，并通过一个 React 组件传递所有的输入 state


**添加图片背景**
IOS:在xcode中添加
android在／android/app/src/main/res的目录中添加

图片内容，通过require进行引入  
require(image!flowers)语句会触发react native查询名为flowers的文件。  

```
  <Image
      source={require("./flowers.png")} 
      resizeMode="cover"
      style={styles.backdrop}
   />    
``` 

**从web获取数据**   
探索从react native中网络接口的用法。不能在移动端使用jquery发送ajax请求。
React native 实现了fetch请求。基于promise的语法非常简洁：   
 
``` 
fetch('http://www.somesite.com')
.then((response) => response.text())
.then((responseText) =>{
      console.log(responseText);
   });
```   

## 4 移动应用组件   
|HTML     | React Native | 
| --------   | -----:  | 
|\<div> | \<View> |
|\<span>,| \<Text> |
|\<li>\<ul> | \<ListView>,child items|
|\<img> | \<Image>|

### 1.文本组件
在react native中，仅有<Text>组件可以将纯文本作为子节点。
必须把文本用<Text>组件包装起来。  

```
<View>
<Text>this is ok!</Text>
</View>
```

样式中的fontWeight和fontStyle属性可以用。
例如：

```
<Text> 
  The quick <Text style = {{fontStyle :"italic"}}>brown</Text> fox jumped over the lazy <Text style={{fontWeight:"bold"}}>dog</Text>
```   
为文本样式创建可复用组件，Em\Strong
推荐在应用中创建并使用一个统一字体和尺寸的MyAppText组件，以此保持字体样式一致性。React Native提倡样式组件的复用而不是样式的复用。     

### 2.图片组件   

```
<Image source ={require('image!puppies')}
 style={{width:400,height:400}}/>;

```
当使用网络资源时，需要手动指定图片尺寸。在多数情况下，避免使用基于URI的方式。  
resizeMode属性：stretch\cover\contain。

### 3.TouchableHighlight   

dom通过事件通知js的过程即是回调，对应的函数就是回调函数

js通过监听函数得知事件的过程即是钩取，对应的函数就是钩子函数

钩子函数和回调函数都是事件处理函数。

<TouchableHighlight>组件同时为onPressIn\onPressOut\onLongPress提供了钩子，可以在React应用中使用这些事件。  

GestureResponder和PanResponder.      

### 4.结构化组件   
 
**\<ListView>**：
> 1. dataSource
> 2. renderRow  

Listview 的头部和尾部不是固定不动的，只能在该组件之外单独渲染。  

**使用Navigator** ：
允许应用在不同屏幕之间的切换（通常叫做“场景”）。  
维护了一个“栈”路由。可以推入、推出和替换场景。可以将其类比为浏览器的history接口。一个路由就是场景的名称和索引。

跨平台<Navigator>和<NavigatorIOS>

**其他组件**： 
<TabBarIOS>和<SegmentedControlIOS>
<DrawerLayoutAndroid>和<ToolbarAndroid>
可以通过a.android.js和a.ios.js

## 5 样式
react native 不支持伪类、动画或选择器。  
推荐采用 Stylesheet.Create

```
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF"
  },
  welcome: { fontSize: 20, textAlign: "center", margin: 10, color: "#FFFFFF" },
  touchable: { borderRadius: 100 },
  button: {
    backgroundColor: "#FF0000",
    borderRadius: 100,
    height: 200,
    width: 200,
    justifyContent: "center"
  }
});
```
使用条件样式. 

```
<View style = {[styles.button,this.state.touching&&style.highlight]}

```

react native 样式数组最右边有最高优先权，并且空值(false,null\defined)会被忽略。

样式作为属性传递：View.propTypes.style

**定位：**
flexbox和绝对定位：
rn中，flex可用属性： 
> 1.flex
> 2.flexDirection
> 3.flexWrap
> 4.alignSelf
> 5.alignItems

相关属性：
> 1.height
> 2.width
> 3.margin
> 4.border
> 5.padding

## 6 平台接口
### 1 使用定位接口
navigator.geolocation
react native暂时不支持到”地理围栏“
### 2 使用用户图片与摄像头
var {CameraRoll} = React ;

### 3 AsyncStorage持久化数据存储
AsyncStorage异步操作，储存键可以是任意字符串。

## 7 模块
react-native不支持的接口，通过npm安装由react native社区编写的模块。

## 8 调试与开发者工具 
command+control+z 处打开debug in chrome 

ios：
在xcode中，控制台看输出。

android:
在项目根目录运行logcat命令查看设备的日志。

应用内的审查元素可以

android avd 启动一个合适的模拟器。

**测试代码**
flow check
在.flowconfig文件下面的[ignore]下面：
.*/node_module/.*

jest框架：
基于jasmine的单元测试框架。它提供侵入性的依赖自动模拟功能。

npm install jest-cli --save-dev  

## 9 学以致用
## 10 部署至IOS应用商店
## 补充内容
[react native 中文官网](https://reactnative.cn/)    













