ES 全称 ECMAScript，ECMAScript 是 ECMA 制定的标准化脚本语言

## ES6

### 类（class）

对熟悉 Java，object-c，c#等纯面向对象语言的开发者来说，都会对 class 有一种特殊的情怀。ES6 引入了 class（类），让 JavaScript 的面向对象编程变得更加简单和易于理解。

```javascript
class Animal {
    // 构造函数，实例化的时候将会被调用，如果不指定，那么会有一个不带参数的默认构造函数.
    constructor(name, color) {
        this.name = name;
        this.color = color;
    }
    // toString 是原型对象上的属性
    toString() {
        console.log('name:' + this.name + ',color:' + this.color);
    }
}

var animal = new Animal('dog', 'white'); //实例化Animal
animal.toString();

console.log(animal.hasOwnProperty('name')); //true
console.log(animal.hasOwnProperty('toString')); // false
console.log(animal.__proto__.hasOwnProperty('toString')); // true

class Cat extends Animal {
    constructor(action) {
        // 子类必须要在constructor中指定super 函数，否则在新建实例的时候会报错.
        // 如果没有置顶consructor,默认带super函数的constructor将会被添加、
        super('cat', 'white');
        this.action = action;
    }
    toString() {
        console.log(super.toString());
    }
}

var cat = new Cat('catch');
cat.toString();

// 实例cat 是 Cat 和 Animal 的实例，和Es5完全一致。
console.log(cat instanceof Cat); // true
console.log(cat instanceof Animal); // true
```

### 模块化 (Module)

ES5 不支持原生的模块化，在 ES6 中模块作为重要的组成部分被添加进来。模块的功能主要由 export 和 import 组成。每一个模块都有自己单独的作用域，模块之间的相互调用关系是通过 export 来规定模块对外暴露的接口，通过 import 来引用其它模块提供的接口。同时还为模块创造了命名空间，防止函数的命名冲突。

```javascrript
 //test.js
 export const  name = 'hello module';

//index.js
 import {name} from './test.js';// test.js

```

### 箭头函数 （Arrow）

ES5 不支持原生的模块化，在 ES6 中模块作为重要的组成部分被添加进来。模块的功能主要由 export 和 import 组成。每一个模块都有自己单独的作用域，模块之间的相互调用关系是通过 export 来规定模块对外暴露的接口，通过 import 来引用其它模块提供的接口。同时还为模块创造了命名空间，防止函数的命名冲突。

```javascrript
const addNum=(a,b)=>(a+b);

const say=()=>{
    return 'hello module'
}

```

### 函数参数默认值

```javascrript
const addNum=(a=10,b=10)=>(a+b);

```

### 模板字符串

```javascrript
const addNum=(name,age)=>{
   return  `Your name is ${name} you age is ${age}.`
};
```

### 解构赋值

```javascrript
const [name,age] = ["moudle", 12];
console.log(name,age)
```

### 延展操作符(Spread operator)

```javascrript
const itemInfo= {
    name: 'module',
    age:20
}
var newIteminfo={
    age:19,
    address:'shanghai',
    ...itemInfo
}

```

### Promise

Promise 是异步编程的一种解决方案，比传统的解决方案 callback 更加的优雅。它最早由社区提出和实现的，ES6 将其写进了语言标准，统一了用法，原生提供了 Promise 对象

```javascript
let promise1 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 1000);
});

promise1
    .then(function() {
        console.log('hello world');
    })
    .then(function() {
        console.log('erroe');
    });
```

### let 与 const

```javascript
const name = 'hello module';
let age = 12;
```

### Symbol

Symbol 是由 ES6 规范引入的一项新特性，它的功能类似于一种标识唯一性的 ID。通常情况下，我们可以通过调用 Symbol()函数来创建一个 Symbol 实例,

```javascript
let sy = Symbol('hello world');
```

### Proxy

proxy 用于修改某些操作的默认行为，可以理解为一种拦截外界对目标对象访问的一种机制，从而对外界的访问进行过滤和修改，即代理某些操作，也称“代理器”。

```javascript
let p = new Proxy(target, handler);
```

## ES7

### includes()

是查找一个值在不在数组里，若在，则返回 true，反之返回 false

```javascript
let arr = ['react', 'angular', 'vue'];
arr.includes('react'); //true
```

### \*\*

求幂运算符 \*\*

```javascript
console.log(10 ** 2);
```

## ES8

### async/await 异步

```javascript
const getSubject = async () => {
    let subjectInfo = await getInfo();
    console.log(subjectInfo);
};
```

### Object.values()

方法返回一个给定对象自身的所有可枚举属性值的数组，值的顺序与使用 for...in 循环的顺序相同 ( 区别在于 for-in 循环枚举原型链中的属性 )。

-   语法：Object.values(obj)
-   参数：
    -   obj: 被返回可枚举属性值的对象.
-   返回值：array 一个包含对象自身的所有可枚举属性值的数组。

!>Object.values()返回一个数组，其元素是在对象上找到的可枚举属性值。属性的顺序与通过手动循环对象的属性值所给出的顺序相同

```javascript
var obj = {
    foo: 'bar',
    baz: 42,
    arr: {a: 'aa', b: 'BB'},
    add: () => {
        console.log('add');
    }
};
console.log(Object.values(obj)); //["bar", 42, {a: "aa", b: "BB"}, () => {console.log('add');}]

var objArr = [1, 2, 3];
console.log(Object.values(objArr)); //[1, 2, 3]
```

### Object.entries()

返回一个给定对象自身可枚举属性的键值对数组，其排列与使用 for...in 循环遍历该对象时返回的顺序一致（区别在于 for-in 循环也枚举原型链中的属性）。

-   语法：Object.entries(obj)
-   参数：
    -   obj: object 可以返回其可枚举属性的键值对的对象
-   返回值：给定对象自身可枚举属性的键值对数组。

```javascript
const object1 = {
    a: 'somestring',
    b: 42
};
let obj = Object.entries(object1);
console.log(obj); //[["a", "somestring"],"b", 42]]
```

### Object.getOwnPropertyDescriptors()

Object.getOwnPropertyDescriptors() 函数用来获取一个对象的所有自身属性的描述符,如果没有任何自身属性，则返回空对象。

-   语法：Object.getOwnPropertyDescriptors(obj)
-   参数：
    -   obj: object 对象
-   返回值：返回 obj 对象的所有自身属性的描述符，如果没有任何自身属性，则返回空对象

```javascript
const obj = {
    name: 'hello module',
    get age() {
        return '20';
    }
};
Object.getOwnPropertyDescriptors(obj);
```

### padStart()，padEnd()

padStart()，padEnd() 字符串补全

```javascript
'x'.padStart(5, 'ab'); // 'ababx'
'x'.padStart(4, 'ab'); // 'abax'

'x'.padEnd(5, 'ab'); // 'xabab'
'x'.padEnd(4, 'ab'); // 'xaba'
```

## ES9

### 异步迭代

ES2018 引入异步迭代器（asynchronous iterators），这就像常规迭代器，除了 next()方法返回一个 Promise。因此 await 可以和 for...of 循环一起使用，以串行的方式运行异步操作

```javascript
async function process(array) {
    for await (let i of array) {
        doSomething(i);
    }
}
```

### Promise.finally()

一个 Promise 调用链要么成功到达最后一个.then()，要么失败触发.catch()。在某些情况下，你想要在无论 Promise 运行成功还是失败，运行相同的代码，

```javascript
new Promise(function(resolve, reject) {
    setTimeout(resolve, 1000);
})
    .then(() => {})
    .catch(err => {
        console.log(err);
    })
    .finally(() => {
        console.log('finally');
    });
```

### Rest/Spread 属性

对象解构提供了和数组一样的 Rest 参数（）和展开操作符

```javascript
const myObject = {
    a: 1,
    b: 2,
    c: 3
};
const {a, ...x} = myObject;
// a = 1
// x = { b: 2, c: 3 }
```

### Regexp 命名捕获组

```javascript
const reDate = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/,
    match = reDate.exec('2018-04-30'),
    year = match.groups.year, // 2018
    month = match.groups.month, // 04
    day = match.groups.day; // 30
```

### 正则表达式 dotAll 模式

标志：为这些表达式提供一致的行为。该特性旨在解决正则表达式中的点(.)不匹配行终止符的限制。s 标志改变了这一点。此标志将在选择的基础上运行，因此现有的正则表达式模式不会受到影响。

```javascript
/hello.world/.test('hello\nworld'); // false
/hello.world/s.test('hello\nworld'); // true
```

### 正则表达式反向断言

解决了环视（lookaround）的一个缺点，它是零宽度的断言，与字符串进行匹配，不消耗任何东西。使用隐藏的断言，开发人员可以确保模式之前有或没有另一个模式。例如：匹配美元的金额而不获取美元符号。

```javascript
const reLookbehind = /(?<=\D)\d+/,
    match = reLookbehind.exec('$123.89');
console.log(match[0]); // 123.89
```

### Unicode 属性转义

Regexp(正则表达式) Unicode 属性转义：使开发者能够更好地访问 Unicode 字符属性。属性转义将以\p{…}和\P{…}的形式添加。

## ES10

### Array.prototype.{flat,flatMap}

数组降维，递归地将数组展平到指定的深度，对数组的内含数组进行展开操作并返回一个新数组

!> depth: 需要展开内层数组的层数，默认为 1

```javascript
const array = [1, [2, [3]]];
array.flat(); // → [1, 2, [3]]
array.flat(Infinity); // → [1, 2, 3]
[2, 3, 4].flatMap(x => [x, x * 2]);
// → [2, 4, 3, 6, 4, 8]
const arr = ['Codedam', 'is Awsome', '!'];
const mapResult = arr.map(item => item.split(' '));
console.log(mapResult); // [ [ 'Codedam' ], [ 'is', 'Awsome' ], [ '!' ] ]
```

### Function.prototype.toString

Function.prototype.toString 方法,返回一个表示当前函数源代码的字符串

```javascript
const fun = name => {
    console.log(name);
};
fun.toString(); // "(name) => { console.log(name) }"
```

### Object.fromEntries()

把键值对列表转换为一个对象

-   语法：Object.fromEntries(iterable)
-   参数：
    -   iterable: 迭代对象，类似 Array 、 Map 或者其它实现了可迭代协议的对象
-   返回值：一个由该迭代对象条目提供对应属性的新对象。

?> 迭代对象:第一个元素是将用作属性键的值，第二个元素是与该属性键关联的值,其他的忽略

```javascript
const arr = [['0', 'a', 'c'], ['1', 'c', 'b', '4', 'F'], ['2']];
const obj = Object.fromEntries(arr);
console.log(obj); // { 0: "a", 1: "c", 2: undefined }
```

### trimStart 和 trimEnd

```javascript
// Trim
const name = '   Codedam ';
console.log(name.trim()); // "Codedam"
// Trim Start
const description = '   Unlocks Secret Codes ';
console.log(description.trimStart()); // "Unlocks Secret Codes "
// Trim End
const category = '  JavaScript ';
console.log(category.trimEnd()); // "  JavaScript"
```
