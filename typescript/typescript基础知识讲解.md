## 前言

TS无法在运行之前根据传递的值来推导方法最终返回的数据类型，只可以根据方法定义的类型展现。

TS是让我们在开发时，可以推断类型，产生语法提示。如，类型断言。不用类型断言难道就不能用该方法了么？，会不会是多此一举

## 基本类型

```js
let isDone: boolean = false;
let age: number = 10;
let test: string = 'xxx';
let u: undefined = undefined;
let n: null = null;

// 不能使用错误方法。如：
test.toString()
```

### any 、 unknow

* any  和unknow一样都可以定义任何数据类型。但unkonw类型不能随意赋值

* any可以直接获得属性，unkonw不行

  ```js
  let price: any = "abc"
  let total: number = price // true
  let stuName: unknow = "wangwu"
  let stuAge: number = stuName // false. unkonw类型不能赋值给string
  let obj: unkn = {name: 'hehe'};
  obj.name // false
  ```

  

## 数组 & 元组 tuple

* 数组合并相同类型的对象，而元组合并不同类型的对象。
* 元组内的元素，必须包含所有定义的类型，数组长度不固定，但类型不能多也不能少

```js
let arrOfNumbers: number[] = [1, 2, 3, 4] // 数组
let user: [string, number] = ['viking', 20] // 元组
```

## 函数

```js
// 没有返回值：void。
// 参数数量确定
function add(x: number, y: number， z?: number): number {
    return x + y
}
// es6写法

const add3: (x: number, y: number) => number = () => {
    
}
```

## 类

* 定义：类就是拥有相同属性和方法的一系列对象的集合，类是一个摸具，是从这该类包含的所有具体对象中抽象出来的一个概念。

  类定义了它所包含的全体对象的静态特征和动态特征。
  
  ```js
  class Person {}
  // 类的对象变量存在栈中，对象变量存储着对象的首地址，对象变量通过这个地址找到它的对象   
  const zhangsan = new Person();
  // 创建对象一共做了三件事
  // 第一件事: 在堆中为类的某个对象【实例】分配一个空间
  // 第二件事：调用对应的构造函数【构造器】并且把构造器中的各个参数值赋值给对象属性
  // 第三件事：把对象赋值给对象变量 【把实例赋值给实例变量】 - d
  ```
  
* 定义类中的属性，不同写法

  ```js
  class Person {
      // 写法一：
      // public 参数执行两步操作：
      // 一，定义变量：public orderId: number;
      // 二，构造函数默认赋值：this.orderId = orderId;
      // 写法二：初始化值
      // public orderId: number = 3;
      // 写法三：ts4 之前写undefined联合类型，会有其他错误。ts4之后：
      // public order!: number;  构造器未赋值的话，是undefined。写！不会检测，判断其类型。
  	constructor(public orderId: number) {
  
      }
  }
  ```

### private, public,protected

* 默认为public

* 当成员被标记为private时，它就不能在声明它的类的外部访问

* protected和private类似，但是，protected成员在派生类中可以访问。**在实例中还是不能访问的**

  ```js
  class Animal {
  　　protected name: string;
  　　constructor(theName: string) {
  　　　　this.name = theName;
  　　}
  	parentFun() {
          
      }
  }
  
  class Rhino extends Animal {
       constructor() {
            super('Rhino');
      }         
      getName() {
          super.parentFun()
          console.log(this.name) //此处的name就是Animal类中的name
      }
  }
  ```

  

### TS类与ES6类的区别

* 定义属性的方式不同，ts如上，es6沿袭了js赋值的方式，在构造函数直接用this来定义属性，并且赋值。
* es6类没有访问修饰符，ts有如上三个修饰符。
* ts有类型推导的能力，无隐藏语法的错误
* ts可以通过配置文件生成es5，或者es6的js版本

## 接口

是为一系列同类对象，同类别的类 提供属性定义和方法声明，但没有任何赋值和实现的数据类型。场景：

* 提供方法的对象类型的参数时使用
* 为多个同类别的类，提供统一的方法和属性声明：

```js
interface ClockInterface {
    currentTime: number;
    alert(): void;
}
// 类实现了接口： implements 
class CLock implements ClockInterface {
    currentTime: number = 123;
	alert() {
        // ...
    }
}
```

* 约束对象的类型

```js
interface Person {
    readonly id: number;
	name: string;
	age?: number;
}
let child: Person = {
    id: 10,
    name: 'xiaoMing'
}

// 只读属性不能赋值
child.id = 20 //false
```

* 约束函数类型

```js
const sum = (x: number, y: number) => {
    return x + y
}
interface ISum {
    (x: number, y: number): number;
    name: string
}

const sum2: ISum = sum; // true
sum2.name = 'xxx' // true
```

* 定义多个属性类型

```js
interface ObjStr{
    [propName: string]: string
}
let obj: ObjStr = {
    a: 'xx',
    b: 'xxx',
    c: 'xxx'
    ...
}
interface Component {
    props: { [propName: string] : any };
    id: string;
    
}
// 假数组  不具备数组的方法

interface LikeArray {
    [index: number]: string;
}
const likeArray: LikeArray = ['1', '2']
```

## 联合类型union Types

* type关键字。类型别名：（起个新类型）

```js
// 联合类型
type Name = string;
type objTest = {
    age: number
  	tech: string
}
type NameResolver = () => string;
type NameOrResolver = Name | NameResolver;
function getName(n: NameOrResolver): Name {  // getName(n: Name | NameResolver)
    if (typeof n === 'string') {
        return n;
    } else {
        return n();
    }
}
```

* 字符串字面量类型：(常用于严谨的类型判断)

```js
type EventNames = 'click' | 'scroll' | 'mousemove';
function handleEvent(ele: Element, event: EventNames) {
    // do something
}
// event  只能取值上面三种类型。
```

## 类型保护(联合类型)

* 无法判断变量具体是某个类型，在联合类型中使用

```js
interface Bird {
    fly: string;
    sing: () => {};
}
interface Dog {
    shout: string;
    run: () => {};
}
type Animal = Bird | Dog;
// 1. 用类型断言做类型保护
function trainAnimal(animal: Bird | Dog) {
    if(animal.fly) {
        (animal as Bird).sing();
    } else {
        (animal as Dog).bark();
    }
}
//  2. 或者用in语法做类型保护
function trainSecond(animal: Animal) {
	if('sing' in animal) {
     	animal.sing(); 
     } else {
         animal.run();
     }
}
// 3. 使用typeof做类型保护
function add(first: string | number, second: string | number) {
    if(typeof first === 'string') {
        ...
    }
}
// 4. 使用instanceof 语法做类型保护  instanceof只能用在类上面。
class NumberObj {
    count: number;
}
//const first = new NumberObj()   // true
function threeS(first: object | NumberObj, second: object | Number) {
    if(first instanceof NumerObj) {
        ...
    }
}
 // 5. ...
```

## type 与 interface的区别

* interface 只能定义对象类型或接口当名字的函数类型。

* type 可以定义任何类型，包括基础类型、联合类型 ，交叉类型，元组。

  ```js
  //  元组
  interface Car { brandNo: string}
  interface Plane { No: string; brandNo: string}
  type TypVechile = [Car, Plane]
  ```

* 接口可以extends，type没有继承功能
* 接口可以合并声明（名称相同），type会报错
* type 可以用 & 交叉类型。接口不能交叉

## 枚举类型 Enum

```js
enum Status {
    OFFLINE = 1, // d
    ONLINE,
    DELETED
}
// 默认值为下标
```

## 类与接口的关系

* 类包含静态类型 和实例类型，要分别对其进行约束。

```js
// 约束构造函数只能传两个参数
interface PersonStatic {
  new (h: number, m: number): any;
  time: number;
}
interface PersonInterface {
  currentTime: number;
  eat(): void;
}
// 前面约束静态类型   后面约束实例类型
export const Person: PersonStatic = class Person implements PersonInterface {
  currentTime: number;

  static time = 12;

  constructor(a: number, b: number) {
    this.currentTime = a;
  }

  eat() {
    console.log(this.currentTime);
  }
};

const son = new Person(11, 22);
console.log(son.eat());
```

