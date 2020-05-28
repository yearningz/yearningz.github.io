---
layout: post
title: 《深入浅出React和Redux》笔记
key: 20180702
tags: React Redux 笔记
---    

### 1.react思维  
响应式布局：  
reactive programming   

工具类    
npm install --global create-react-app    
create-react-app first\_react\_app   
cd first\_react\_app
npm start

create-react-app 支持es6语法

JSX：javascript语法扩展。  
添加页面处理函数onclick事件。

所有点击事件都被事件处理函数捕获，根据具体组件分配给特定函数，使用事件委托的性能要比为每个onClick都挂载一个事件处理函数要高。

react 公式： UI=render(data);     
数据驱动渲染

事件a  >  
事件b  > rende > virtual DOM > DOM修改   
事件c  >      

### 2. 设计高质量的react组件  
prop是组件的对外接口，state是组件的内部状态。   
prop 可以是字符串，任何一种javascript支持的数据类型。
在jsx中，必须用{}把prop值包住，故有两层括号，外层花括号代表是jsx的语法，内层花括号代表这是一个对象常量。

react要求render只能返回一个元素。  
const {captions} = this.props;   
propTypes是通过增加类的propTypes属性来定义prop规格。只会报错误，不影响程序执行。在发布产品代码时，用一种自动的方式将propTypes去掉。
defaultProps
state必须是一个js对象。getInitialState。    
改变state必须使用this.setState函数  
组件不应该改变prop的值，state的存在目的是让组件来改变。  
  
组件生命周期  
**装载过程：**    
1.constructor:   
1.1初始化state.    
1.2绑定成员函数的this环境   

2.getIntialState只有在react.createClass的组件类才会发生作用。在一个组件整个周期，只会调用一次。 (es6语法定义不会用到）  
3.getDefaultProps只有在react.createClass的组件类才会发生作用。(es6语法定义不会用到）  
es6语法可用object.defaultProps. 

```
class Sample extends React.Component{
   constructor(props){
       super(props);
       this.state = {foo:'bar'};
   };
}
Sample.defaultProps = {
sampleProp:0
}   
```  

3.componentWillMount 在该组件render之前调用，包括一些组件启动的动作，包括像ajax数据的拉取操作、一些定时器的启动等
4.render： 返回一个jsx结构。纯函数，不要调用setState
5.componentDidMount. 在所有组件render之后调用。只在浏览器中执行。是最佳获取初始化组件内容请求的时机。
若如果需要带上jquery功能，就在componentDidMount函数中调用，因为dom树那时候已经渲染好了。


**更新过程**   
1.componentWillReceiveProps:   
组件从父组件接收到新的props之前调用。
根据新的props来计算出是不是要更新内部状态state。
要是父组件的render函数被调用，在render函数里面被渲染的子组件就会经历更新过程，而不管父组件传给子组件的props有没有改变，都会触发子组件的函数。
this.setState触发的更新过程不会调用该函数。  

2.shouldComponentUpdate(nextprops,nextState)
决定一个组件什么时候不需要渲染。
正常都返回true  
nextProps\nextState\this.props\this.state\
3.componentWillUpdate和componentDidUpdate   
4.componentWillMount和componentDidMount

**卸载过程**   
1.componentWillUnmount
组件从页面上销毁时做一些数据的清理。
该函数总和componentDidMount相关。   
 
全局状态是唯一可靠的数据源。
   
       
### 3. 从Flux到Redux  
     
 
 ```
 action -> dispatcher -> store -> view    
                   ^ - -  action < - |    
                  
 ```  
 
 dispater:处理动作分发，维持store之间关系。  
 store：负责存储数据和处理数据之间的关系。  
 action:驱动dispater的js对象。  
 view:视图部分，负责显示用户界面。   
 
**dispatcher** 一个对象。自始自终只需要暴露一个函数dispatch,用于派发action.  
**action** 纯对象，表示一个纯动作。
代表一个动作的纯数据。
 定义action需要两个文件，需要定义一个名为type的字段，一个定义action的构造函数。  
**store** 一个对象，用于存储应用状态。接收dispatcher派发的动作，根据动作来决定是否要重新更新应用状态。  
**view** 
1.创建时，要读取store上状态来初始化组件内部状态。
2.当store上状态发生变化时，组件要立刻同步更新内部状态保持一致。 
3.view如果要改变store状态，必须而且只能派发action。    


Redux-单向数据流
1.唯一数据源。（整个应用只有一个store）   
2.保持状态可读。   
修改store状态，通过派发一个action来实现。  
改变状态的方法不是去修改状态上的值，而是创建一个新的状态返回给redux，由redux完成新的状态组装。
3.数据改变只通过纯函数完成。   
即reducer,“规约”，第一个参数是上一个规约的结果，第二个参数是这一次规约的元素。函数体是返回两者之和。
  
  **reducer(state,action).**   
redux中的reducer只负责计算状态，不负责存储状态。  
action  
redux中 action是直接返回一个对象。
store  
createStore函数，第一个参数代表更新状态的reducer，第二个参数是状态初始值，第三个参数可选（store Enhancer). 
确定store状态，是设计好redux应用的关键。  
reducer
redux中把存储state的工作抽取出来交给redux框架本身，让reducer只关心如何更新state,而不管state怎么存。
  
**容器组件和傻瓜组件**  
一个react组件的功能：   
1.和redux Store打交道，读取store的状态。需要更新store对象，就派发action对象。（容器组件，通过props传递给傻瓜组件）  
2.根据props和state,渲染出用户界面。（傻瓜组件，纯函数，由props产生结果，不再有状态。）。

**组件context**  
provider是一个通用的context提供者，可以应用在任何一个应用中，我们把这个组件叫做provider.

react-redux  
作为容器组件：
1.把store状态转化为内层傻瓜组件的props.（mapStateToProps） 
2.把内层组件的用户行为转发给store组件。  （mapDispatch.ToProps).  

provider 必须包含三个参数
1.subscribe. 
2.dispatch. 
3.getState. 

### 4.模块化react和redux应用        
构造一个应用：  
1.代码文件的组织架构。 
2.确定模块的边界。   
3.store的状态树设计。    

状态树的设计要遵循如下原则：  
1.一个模块控制一个状态节点。   
2.避免冗余数据。  
3.树形结构扁平。   

* 1.在入口src/index.js文件中，用provider包住最顶层的TodoApp模块，这样让store可以被所有组件访问到。  
* 2.在顶层src／TodoApp.js中，把关键视图显示出来。
* 3.action构造函数。
* 4.reducer函数以action.type为条件的switch语句构成。  
reducer必须是一个纯函数，纯函数不能有任何副作用，包括不能修改参数对象。  
reducer函数会接收任意action，对于不感兴趣的action，执行default中的语句，将state原样返回，不需要更改state。     

mapStateToProps（state, ownProps）   
mapStateToProps是一个函数，用于建立组件跟 store 的 state 的映射关系   
作为一个函数，它可以传入两个参数，结果一定要返回一个 object 
传入mapStateToProps之后，会订阅store的状态改变，在每次 store 的 state 发生变化的时候，都会被调用   
ownProps代表组件本身的props，如果写了第二个参数ownProps，那么当prop发生变化的时候，mapStateToProps也会被调用。例如，当 props接收到来自父组件一个小小的改动，那么你所使用的 ownProps 参数，mapStateToProps 都会被重新计算）。   
mapStateToProps可以不传，如果不传，组件不会监听store的变化，也就是说Store的更新不会引起UI的更新.  

mapDispatchToProps   
mapDispatchToProps用于建立组件跟store.dispatch的映射关系,可以是一个object，也可以传入函数.  
如果mapDispatchToProps是一个函数，它可以传入dispatch,ownProps, 定义UI组件如何发出action，实际上就是要调用dispatch这个方法.

### 5.react组件的性能优化   
组件需要考虑装载阶段、更新阶段和卸载阶段。  
react的调和过程,即在o(n)时间复杂度完成virtual dom的比较。

同类型子组件出现多个实例时，可以写上key值.

### 6.react高级组件     
### 7.redux和服务器通信   
   redux的单向数据流是同步操作，驱动redux流程是action对象。每一个action对象被派发到store上之后，同步地被分配到所有的reducer函数，每个reducer都是纯函数，纯函数不产生任何副作用，自然是完成数据操作后立刻同步返回，reducer返回的结果又被同步地拿去更新store上的状态数据，更新状态数据的操作会立刻被同步给监听store状态改变的函数，从而引发作为视图的react组件更新操作。  
   redux-thunk是redux解决异步操作的解决方法之一。
   
### 8.扩展Redux   
暂无	