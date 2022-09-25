
## vue2使用

### v-show 和 v-if 的区别
* v-show 通过css控制。v-if是组件的渲染和销毁。
* 频繁切换 使用 v-show。

### v-for 中为何使用key
* key 一定要用，且不能用index，用业务标志。
* diff算法中通过tag 和 key 来判断是否是sameNode。减少更新，影响渲染性能。


### 组件如何通信
* 父子组件：props
* this.$emit
* 自定义事件
* vuex
* 依赖注入：provide，inject
* 边界情况：this.$root ,  this.$parent
* slot插槽

### 描述组件渲染、更新过程
###### 初次渲染：
1. 将模版转为render函数
2. 触发响应式，监听data属性getter / setter
3. 执行render函数，生成虚拟DOM：vnode，通过patch（elem，vnode）渲染界面。

###### 更新过程：
1. vue会将data所有的属性转为 getter/setter
2. 每个vue实例都有一个watcher，监听getter/setter。
3. 当data变化，触发setter，会通知watch，执行render函数，生成vnode，再patch，对应组件更新。

###### 画图。
**render函数生成的是vnode。渲染和更新都要触发render，从图中就能看出来。
### data必须是个函数
data如果不是函数，实例化时候，会造成data共享。保持数据独立。
### ajax应该放在哪个生命周期
mounted。
因为ajax是异步，js是单线程。放到mounted之前，并不会提前执行，也是要放到callback queue排队，
等同步代码执行完才执行。
### 如何实现自定义v-model

### 多个组件有相同逻辑，如何抽离？
1. mixin。
2. mixin的缺点：不清楚来源。
3. 3.0改进：composition API


### 何时使用异步组件？
* 加载大组件。
* 路由组件。
  * 2.x：import('./components/AsyncComponent.vue')
  * 3.0: defineAsyncComponent( () => import('../../..') )


### 何时使用缓存组件 keep-alive
* 不需要重复渲染的时候
* 多个静态tab页

## vue2性能优化。
### 何时使用beforeDestroy
* 解绑自定义事件（addEventListen）
* 清除计时器


### vuex中的action 和mutation的区别
* action做异步操作，mutation不行。
* mutation通常做一个操作。commit触发
* action可以做多个mutation的集合。dispatch触发

### 监听data变化的核心API
* Object.defineProperty
  ```js
    Object.defineProperty(object1, 'property1', {
      value: 42,
      writable: false,
      set:function(){},
      get: ...
    });
    ```

* 无法深度监听，无法监听数组。方案：重新定义原型（不改变Array原生能力），重写push，pop方法。
* 缺点：深度监听需要一次性递归到底。
* 3.0：
   ```js
   new proxy({},{ // 原生支持数组
        set:function(){},
        get:function(){},
        deleteProperty:..
    })
    ```

### diff算法

diff算法的目的是获得最新的vnode，vnode{children ,text,tag ,}patch最终即可生成html。

diff：将时间复杂度 O3 - O1
只比较统一层级，不做跨级比较
tag不相同，直接删除重建，不做深度比较
tag和key相同，则认为是相同节点，不继续比较。

### $nextTick
*  因为vue是异步渲染。
* 确保在DOM更新之后，获取最新DOM。
### vue的常见性能优化
* v-show 、v-if
* computed 缓存
* v-for 中使用key
* 异步（动态）组件
* 缓存组件
* beforeDestroy中及时销毁
* data层级不能太深（影响深度监听，一次性递归）
* SSR
## 原理
### mvvm
* mvvm 区别于传统组件，不是操作dom，抛弃jq。
* 数据驱动视图，让我们更专注数据（业务）
* view（视图） - viewModel（监听事件，指令） - Model(数据模型，就是vue组件中的data)
### 虚拟DOM

```js
{
    tag:'div',
    props: {
        className: '..',
        id: 'id'
    },
    children: [
        {
            tag: 'ul'
        },
        {
            tag: 'p'
        }
    ]
}
```
因为DOM操作非常消耗性能，所以用js对象模拟DOM结构，来进行计算和对比，以最小的更新范围来更新DOM。
对比的过程就是diff算法。
核心API：
* h():传入tag标签（属性，标签，值） 生成vnode。
* patch（vnode，newVnode）：对比  ，渲染或更新到DOM节点上
* diff

### vue原理的总结
几个核心：
模板编译生成vnode -> 虚拟DOM -> diff算法
模板编译：
* vue template complier 返回with语句。 将模板编译为render函数
* 执行render函数，生成vnode
* vnode最终通过虚拟Dom，diff算法，，最终生成html。
* 所以vue-template最终是生成vnode 


### vuex与全局变量的区别
* vuex的变量是响应式的
* vuex的变量是可跟踪的，追踪它的变化
* vuex是由统一的方法修改数据，全局变量可随意修改。
* 全局变量会造成命名污染
### computed （计算属性）与 watch（侦听器）的区别
* computed 是基于它的响应式依赖，当依赖改变时，才会重新求值
* watch 监听的数据必须在data定义，当data发生变化时，触发。不能return值。
* watch有三个属性：deep，handler，immdiate。

## vue3用法

### 生命周期

* beforeDestroy 改为 beforeUnmount
* destroyed 改为 unmouted

### Composition API

小型项目可以继续使用option API。composition API是高阶技巧，为解决大型复杂项目而设计。

* 更好的代码组织
* 更好的逻辑复用
* 更好的类型推导

### ref reactive toRef toRefs

* 生成值类型的响应式数据 （值类型，引用类型）

* 修改值 .value

* ref用在reactive和模板中

  ```js
  // 二：ref用在模板中 elementRef.value
  <template>
      <div ref = "elementRef"></div>
  </template>
  setup() {
      cons ageRef = ref(20);
      const elementRef = ref(null);
      // 一：ref用在reactive中
      const state = reactive({
          age: ageRef 
          name: 'hello'
      })
      // 不使用ref，可使用toRef转换
      const nameRef = toRef(state, 'name')
      
      return {
          nameRef,
          elementRef，
          state // 或者直接返回ref
      }
  }
  ```





## vue3原理

### vue3 比 2的优势是什么

* 性能更好，体积更小
* 更好的ts支持
* 更好的代码组织，更好的逻辑抽离



