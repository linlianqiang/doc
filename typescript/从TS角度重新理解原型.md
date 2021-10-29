## 变量空间 - 对象空间

```js
const myObj = {name: 'hello'}; // myObj 称为变量空间，存在栈中。{name: 'hello'}称为对象空间，存在堆中
const newObj = myObj;// 把引用地址复制给newObj
myObj = {name: 'world'}; // myObj指向堆中新建的 {name: 'world'};
newObj.name // hello
```

## 原型

* 定义：原型【 prototype ] 是定义函数由 JS 自动分配给函数的一个可以被所有构造函数实例对象变量共享的对象变量【也叫对象属性】

* 增加或修改原型对象的属性或方法后， 所有的实例或叫对象立即可以访问的到 【但创建实例后再覆盖原型除外】

  ```js
  ```

  

