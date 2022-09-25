# react

## react 与 vue的区别

使用上的区别：

* react事件需要指定this。或者使用箭头函数。
* react更多是在写纯js，需要自己造轮子。而vue提供了很多指令，方法，可以更快的上手。
* 状态管理： mobx, redux 与 vuex。
* 双向事件绑定。onChange自己实现 与 v-model。

原理上的区别：

* react是合成事件SyntneticEvent。不像vue是原生的nativeEvent

## 用法

### setState

* 不可变值。不能直接修改state的值，必须用setState()。原因是什么？shouldComponentUpdate
  * 纯函数：不改变原来数据的函数。slice()、

```js
this.setState({
    list1: this.state.list1.push('100') // 错误
    list1: [...this.state.list1, '100'] // 正确 或者使用concat
    list2: {...this.state.list2, a: '100'} // true. 或者使用 Object.assign()
})
```

* 可能是异步更新

  * 在setState 的回调函数中是同步的
  * 在setTimeout中是同步的
  * 在自定义DOM事件中也是同步的

  ```js
  this.state = {
      count: 0
  }
  this.setState({
  	count: this.state.count + 1
  }, () => {
      // 同 vue 中 $nextTick
      console.log(this.state.count); // 同步
  })
  console.log(this.state.count); // 0 异步
  
  setTimeout(() => {
      this.setState({
          count: this.state.count + 1
      })
      console.log(this.state.count) // 同步
  }, 0)
  
  ```

* 可能会合并

  ```js
  this.setState({count: this.state.count + 1})
  this.setState({count: this.state.count + 1})
  this.setState({count: this.state.count + 1})
  
  // 传入函数会被执行，不会合并
  this.setState((prevState, props) => {
      return {
          count: prevState.count + 1
      }
  })
  ```

  



### 类型检查

需要安装prop-types

### Props.children

类似vue的slot

### lazy 与Suspense

### 生命周期

<img src="/../media/image-20220329103348624.png" style="zoom: 70%" />

```js
componentWillUnmount() {
    // 及时销毁自定义事件， 计时器等
    document.body.removeEventListener('click', this.eventName)
}
```



### react-router-dom

* react-router-dom是基于react-router进行的二次开发。提供了link，BrowserRouter等通过dom操作触发路由。
* switch，根据不同的path渲染不同Route下组件。从上到下执行，一旦匹配，就不再匹配其余其他规则。

### 组件如何通信
* 父子组件 props：属性的传递与函数的传递一致。不像vue的写法。
* 自定义事件
* redux 和 context

### context是啥
* 父组件，向其所有子孙组件传递信息

* 场景：一些公共信息的传递，如语言，主题。

  * 用props太繁琐，用redux小题大做。

  ```js
  const ThemeContext = React.createContext('light');
  class App extends Component {
      return <ThemeContext.Provide Value={this.state.theme}>
          <Button />
          <OtherComp />
      </ThemeContext>
  }
  
  class Button extends Component {
      // static contextType = ThemeContext
      render() {
          const theme = this.context;
          return <div>{theme}</div>
      }
  }
  Button.contextType = ThemeContext // 指定contextType读取当前themeContext> 。与static静态属性一致。
  
  // 如果底层是函数式组件直接使用 ThemeContext.Consumer
  
  function OtherComp() {
      return <ThemeContext.Consumer>
          { context => <p>{context.theme}</p> }
      </ThemeContext.Consumer>
  }
  ```

  



### class组件与 函数组件的区别
* 如果组件只接收一个props，用函数组件
* 函数组件，没有state，没有生命周期。简易版的class组件。
* 函数组件更复合设计理念，函数式编程，react hooks提供了方案。

```js
// 函数组件
function List(props) {
    const { list } = this.props;
    return <div>
    </div>
}
```



### 受控组件 与 非受控组件
* 受控组件就是：自己用state控制表单的值。自定义实现onChange事件，来更新state。

* 非受控组件：就是将数据交给DOM节点来处理， 手动操作DOM。

  * defaultValue、defaultChecked (受控使用的是value,checked)

  * 通过ref获取DOM节点，使用 React.createRef 来实现。 与vue一致

  * 场景：手动操作DOM, setState实现不了。或者 文件上传。或者富文本编辑器。

    ```js
    // 非受控组件
    class RefComponent extends Component {
        constructor() {
            this.nameInputRef = React.createRef()
        }
        render() {
            return <div>
                <input ref={this.nameInputRef} />
                // 页面的数据，并不会随着表单的输入而改变。
                <span onClick={this.alertName}>{this.state.name}</span> 
            </div>
        }
        // 箭头函数this指向当前作用域
        alertName = () => {
            const elem = this.nameInputRef.current;
            // 所以获取state只能从dom元素里取。
            const InputValue = elem.value;
        }
    }
    ```

### 异步组件
* 加载大组件。
* 路由懒加载。router： import，lazy（）、Suspend（）

```js

```

### 组件公共逻辑如何抽离--
* 高阶组件：HOC，只是一种模式，并不是新功能或API。类似工厂模式？

  ```js
  // 接收组件，返回新组件
  
  const HOCFactory = (Compnent) => {
      class HOC extends Component {
          // 此处定义传进来不同组件的公共逻辑，达到复用。
          render() {
              // 此处的组件是变量，不是子组件，所以能做到逻辑复用。
              // t
              return <Component {...this.props} />
          }
      }
      return HOC
  }
  
  // 使用：
  export default HOCFactory(App)
  ```

* Render Props 

  通过一个函数将class组件的state作为props传递给纯函数组件。

  实战代码。看文档

  ```js
  const App = () => {
      
  }
  class Facotry
  ```

  

* 场景：

### 性能优化：shouldComponentUpdate
* 在setState之前，数据已经一致。而shouldComponentUpdate比较的两个值，将一直一致。
* shouldComponentUpdate 返回false，不更新组件。返回true则更新。什么时候用？在需要的时候用。
* 默认返回true，默认重新渲染所有子组件，而有的情况，子组件是不需要更新的。

```js
class childComponent extends Component {
    // 默认返回true
    shouldComponentUpdate(nextProps, nextState) {
        if(nextProps.text !== this.props.text) {
        	return true   
        }
        return false // 不重复渲染 即 componentDidUpdate 不执行
    }
}
```

### 性能优化：PureComponent & memo
默认实现了浅比较的shouldComponentUpdate：PureComponent用于class组件，memo用于函数组件。

仅在你的 props 和 state 较为简单时，才使用 `React.PureComponent`，或者在深层数据结构发生变化时调用 [`forceUpdate()`](https://zh-hans.reactjs.org/docs/react-component.html#forceupdate) 来确保组件被正确地更新。你也可以考虑使用 [immutable 对象](https://facebook.github.io/immutable-js/)加速嵌套数据的比较。

```js
function MyComponent(props) {
  /* 使用 props 渲染 */
}
function areEqual(prevProps, nextProps) {
  /*
  如果把 nextProps 传入 render 方法的返回结果与
  将 prevProps 传入 render 方法的返回结果一致则返回 true，
  否则返回 false
  */
}
export default React.memo(MyComponent, areEqual);
```

### immutable.js

类似深拷贝，用来解决不可变值的问题

* https://juejin.cn/post/6844903587458334733

### Portals

使用Portal可以把当前组件渲染到指定位置。

场景：父组件z-index太小。通常解决一些css的问题。

```js
// 比如fixed元素要放在body上，有更好的浏览器兼容性。
import ReactDOM from 'react-dom';

render() {
    return ReactDOM.createPortal(
    	<div>{this.props.children}</div>,
        document.body
    )
}
```



### react事件 与 DOM事件的区别

* react事件，全部都挂载到document上。
* react的event对象不是原生对象，是合成对象SyntneticEvent。
* React16，事件全部绑定到document上。 而react17事件绑定到root组件上。原因是有利于多个React版本并存。例如微前端，因为微前端是公用一个document。

### redux （react-redux）
* redux 提供createStore，接收reducer参数。集合了所有store（vuex）
* react-redux 提供了Provide和connect。（mapStateToProps，mapDispatchToProps）
* 用connect连接的组件，props能接收到store，和dispatch
* dispatch 触发reducer 接收一个action，和旧的state：dispatch(action(newState))
*  redux的设计思想，容器组件（维护state） 和 UI组件（只渲染）。

异步实现：
使用中间件：redux-thunk
先执行ajax，再dispatch同步action

### redux的设计理念
为什么要引入这么多复杂的概念：action，reducer，dispatch，store？
因为大型应用state什么时候，如何改变，没法追述缘由。

* action：用来描述state的变化（type,text）,只是一个普通的对象。
* reducer的目的就是连接变化，和旧的state，返回新的state。必须是纯函数
* 唯一改变state的方式就是触发action。



## react hooks

* 大型组件很难拆分和重构，class不易拆分
* 相同业务逻辑，分散到各个方法中，逻辑混乱。与 compositionAPI一致

* 复用逻辑变的复杂，HOC， Render Prop

以上就是hook出现的原因，react提倡函数式编程，但是现有的函数式组件，只能实现简单的单一组件。

* 函数更灵活，更易拆分和测试。

### State Hook

函数执行完毕，立即销毁作用域，通过hook，将state保留在函数中。

```js
import React, { useState, useEffect } from 'react';

function TestComponent() {
    const [count, setCount] = useState(0); // 返回一个state，及修改state的函数
    
    // 模拟了class组件的componentDidMount 和 componentDidUpdate
    useEffect(() => {
        
    })
    // 模拟class组件的componentDidMount。不依赖任何state
    useEffect(() => {
        
    }, [])
    // 模拟class组件的 componentDidUpdate。 数组里需要添加依赖，指明谁更新了
    useEffect(() => {
        
    }, [count])
    
    // 模拟componentWillUnmount
    useEffect(() => {
        let timer = window.setInterval(() => {
            ...
        }, 1000)
        
        // 返回给·一个函数。 在组件销毁时，执行该函数
        return () => {
            window.clearInterval(timer);
        }
    }, [])
}
```

### Effect Hook

让函数组件模拟生命周期。使纯函数有了副作用。解释：

* 默认情况，执行纯函数，输入参数，返回结果，无副作用

* 所谓副作用，就是对函数之外造成影响，如设置全局定时任务
* 而组件需要副作用。所以函数组件，需要useEffect ‘勾到’纯函数中。（技术向业务妥协）

模拟componentWillUnmount的注意事项：

```js
```

### useRef

* 获取DOM节点

### useContext

* 同class组件context一致

### useReducer

* 相对useState的扩展，用在单组件。 与redux中的reducer完全不同

### useMemo & useCallback

* hooks常用的优化策略

* 用useMemo缓存数据，用useCallback缓存函数

* class组件使用shouldComponentUpdate和PureComponent优化

  ```js
  import React, {useMemo, memo, useState} from 'react'
  
  function Parent {
      const [count, setCount] = useState(0)
      const [name] = useState('yaji')
      
      // 用useMemo缓存数据，有依赖
  	const userInfo = useMemo(() => {
          return {name, age: 12}
      }, [name])
      
      // 用useCallback缓存函数 const onchange = () => {}：子组件还是会更新
      const onChange = useCallback(() => {
      	console.log
      })
      return (
              //   正常情况，父组件更新，子组件无条件更新。用useMemo包裹，会进行浅层比较，依赖变化才会更新
              <div onClick={() => { setCount(count + 1) }}>{count}</div>
    			<Child userInfo={userInfo} onChange={onChange}>
       )
      
  }
  
  const Child = memo(({userInfo, onChange}) => {
      return <div>{userInfo.name}
      	<input onChange={onChange} />
      </div>
  }) 
  
  ```

### 自定义Hook

* 封装通用的功能。

* 扩展性，解耦代码

* 步骤

  * 利用useState, useEffect设置响应式数据
  * 确定参数
  * 确定返回值。类似： const [count,  setCount] = useState(0)

  ```js
  // 不是封装axios，而是要理解封装的思路
  import {useState, useEffect} from 'react'
  import axios from 'axios'
  
  function useAxios(url) = {
      const [loading, setLoading] = useState(false)
  	const [data, setData] = useState()
      const [error, setError] = useState()
      useEffect(() => {
          setLoading(true)
          axios.get(url)
              .then(res => setData(res))
          	.catch(err => setError(err))
          	.finally(() => setLoading(false))
      })
  	return [loading,]
  }
  ```

  

## 组件设计

* 状态提升。高层的组件设计数据,处理数据。低层组件负责UI，交互，触发等。

  1，何为组件和状态设计
1，单考状态（state，data），单考组件没办法考察能力。
2，根据具体的业务场景，如何设计组件，设计数据，父子组件如何通信？
3，不应该像以前一样，拿到一个需求，就嘎嘎嘎干，做着做着就想着分组件，数据也乱加。
2，如何设计状态 和 组件
错误：以前都是思考组件，没想到数据，通过代码量来分组件。。

state设计：
1，用数据描述所有的内容
2，数据尽量结构化并且层级不能太多，便于遍历，查找 及性能优化。（对象，数组）。
    eg：字符串就不是结构化数据。
3，数据要可扩展，方便增加新功能。

组件设计：
1，要从功能上拆分层次。
2，组件原子化，尽量让组件只做一件事。功能很复杂。。组件很简单
3，容器组件（只管数据，操作数据） 和 UI组件（只管视图，只管交互，给我什么就展示什么）
    所以，通常容器组件是最外层，汇总。负责给其他子UI组件传数据。

## 原理

### JSX本质是什么
1，babel 默认会编译JSX。类似vue-template-complier编译vue-temppate，会生成render函数
2，编译后的JSX，是React.createElement()，会生成vnode ,其实就是VDom里面的 h 函数。
    参数：（标签,属性，子节点，子节点，..）
3，所以严格规定了 JSX里面，标签要小写，组件名要大写。不然createElement在解析的时候，没法识别是
组件或者标签。

### 合成事件
1，react所有事件都绑定到document。
2，event不是原生的，是合成的原生对象。不同Vue事件，和DOM事件。syntneticEvent
3，原生对象挂在：event.nativeEvent.
event.currentTarget //指向当前对象，是假象。
实际，event.nativeDocument.currentTarget //指向document

为什么：
1, 更好的兼容性和跨平台
2，全部挂到document上，减少内存消耗，避免频繁解绑
3，方便事件统一管理，dispatchEvent（事务机制）

### setState，batchUpdate
1，setState 一定要遵循不可变值。即在setState外面，不能改变state本身的值。
    在用一些函数的时候要注意，尽量用纯函数，不改变对象本身的值。如forEach，push,pop等会改变。
2，setState有同步的情况，也有异步的情况。
    a，直接使用的话，是异步的。当然可以在setState里传回调函数。
    b，在setTimeout 或 自定义DOM事件中，是同步的
3，因为在执行setUpdate的过程中，会判断是否处于 batch update阶段，
会存到dirtyComponent。否的话：遍历dirtyComponents，updateComponent,更新state，props。

4，setState也有可能会合并的情况，如果同时修改某个值。如果参数是函数，则不会合并。

batchUpdate：
batchUpdate 就是setState 走同步或者走异步的原因。
1，调用setState时，newState 是否处于batch UpState中。
（如何判断呢：isBatchingUpdates，是true或者false）
2，是true的话就是在batchUpdate中（异步）。newState就保存在dirtyComponent中
3，是false的话，就不是处于batchUpdate中（走同步代码）
### 组件渲染、更新过程
渲染：
1, 组件接收数据props 或 state。
2，render函数生成vnode。解析JSX就是createElement（）
3，patch（ele，Vnode）。渲染到界面上。patch只是一个统称，vDOM一个核心渲染api。

更新：
1，通过setState将组件存到dirtyComponent中。
2，然后遍历所有的dirtyComponent，通过render函数生成vnode。
3，patch（）
6，react-fiber  时间调度原理
背景：复杂组件diff算法复杂，同时又存在DOM操作，如（拖拽），会造成页面卡顿。
    因为DOM渲染和js公用一个线程。

diff算法分两步：计算js 和 渲染到DOM

### react-fiber 就是优化 计算的这部分。

做法就是：
在DOM渲染的时候暂停，在DOM空闲时恢复。
react时间调度原理：利用 requestAnimationFrame 实现requestIdleCallback（计算一帧剩余的时间。）

