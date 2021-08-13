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

## 数组

```js
let arrOfNumbers: number[] = [1, 2, 3, 4]
```

## 元组 tuple

* 数组合并相同类型的对象，而元组合并不同类型的对象。
* 元组内的元素，必须包含所有定义的类型，数组长度不固定，但类型不能多也不能少

```js
let user: [string, number] = ['viking', 20]
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

* 如果有多个属性都是string

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

// 假数组  不具备数组的方法

interface LikeArray {
    [index: number]: string;
}
const likeArray: LikeArray = ['1', '2']
```

