## 定义 & 基础

* 组件不仅能够支持当前的数据类型，也能够支持未来的数据数据类型。以此来达到通用

```js
function echo<T>(arg: T): T {
  return arg;
}
const num = echo('str'); // num的类型，根据传入的参数而变化。echo函数可复用
const num: number = echo('str');// false
```

* 使用两个类型变量

```js
// 泛型函数
function identity <T, U>(value: T, message: U) : [T, U] {
  return [value, message];
}
```

## 泛型接口

```js
interface Identities<V, M> {
    value: V,
    message: M
}
// 将 Identities 接口作为 identity 函数的返回类型：
function identity<T, U> (value: T, message: U): Identities<T, U> {
  console.log(value + ": " + typeof (value));
  console.log(message + ": " + typeof (message));
  let identities: Identities<T, U> = {
    value,
    message
  };
  return identities;
}

console.log(identity(68, "Semlinker"));

```

## 泛型类

```js
interface GenericInterface<U> {
  value: U
  getIdentity: () => U
}

class IdentityClass<T> implements GenericInterface<T> {
  value: T

  constructor(value: T) {
    this.value = value
  }

  getIdentity(): T {
    return this.value
  }

}

const myNumberClass = new IdentityClass<Number>(68);
console.log(myNumberClass.getIdentity()); // 68

const myStringClass = new IdentityClass<string>("Semlinker!");
console.log(myStringClass.getIdentity()); // Semlinker!
```

* 在实例化 `IdentityClass` 对象时，我们传入 `Number` 类型和构造函数参数值 `68`；

* 之后在 `IdentityClass` 类中，类型变量 `T` 的值变成 `Number` 类型；

* `IdentityClass` 类实现了 `GenericInterface<T>`，而此时 `T` 表示 `Number` 类型，因此等价于该类实现了 `GenericInterface<Number>` 接口；

* 而对于 `GenericInterface<U>` 接口来说，类型变量 `U` 也变成了 `Number`。这里我有意使用不同的变量名，以表明类型值沿链向上传播，且与变量名无关。

## 使用泛型

* 当你的函数、接口或类将处理多种数据类型时；
* 当函数、接口或类在多个地方使用该数据类型时。

很有可能你没有办法保证在项目早期就使用泛型的组件，但是随着项目的发展，组件的功能通常会被扩展。这种增加的可扩展性最终很可能会满足上述两个条件，在这种情况下，引入泛型将比复制组件来满足一系列数据类型更干净。

最近写组件的时候经常组件拆分或者写一些可复用组件，这个时候都不用我去寻找泛型的使用场景，他自己就出来了，因为父组件要向子组件传递参数。说白了，当出现参数传递的时候泛型大概率就要派上用场了，所以写子组件或者公用方法时，应该是泛型高频使用的场景，希望能帮到跟我当初一样疑惑的小伙伴。??
