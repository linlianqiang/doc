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

## 接口

* 约束类

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

## 枚举类型 Enum

```js
enum Status {
    OFFLINE = 1, // d
    ONLINE,
    DELETED
}
// 默认值为下标
```



## private, public,protected

* 默认为public
* 当成员被标记为private时，它就不能在声明它的类的外部访问
* protected和private类似，但是，protected成员在派生类中可以访问。在实例中还是不能访问的

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

