# Es6

## 版本更新记录

#### ES6

###### 迭代器

```code
let likeArray = {
  0: 1, 1: 2, 2: 3, length: 3, [Symbol.iterator]:function*() {
    let index = 0;
    while (index !== this.length) {
      yield this[index++];
    }
  }
}
// 迭代器就是一个有next方法的对象 每次调用next都会返回一个对象 对象里有done，value, for of 必须拥有迭代器的元素才能使用
// 默认我用...likeArray 会让迭代器执行
let arr = [...likeArray];
console.log(arr);
```

> -   let const. 字符串模版, 箭头函数, 结构赋值, promise, 默认参数。import(导入) 和 export(导出): generator（生成器）

#### ES7

> -   async/await 异步
> -   Array.prototype.includes()。 是查找一个值在不在数组里，若在，则返回 true，反之返回 false
> -   3 \*\* 2 求幂运算符

#### ES8

> -   async function foo() {}
> -   Object.entries() 如果一个对象是具有键值对的数据结构，则每一个键值对都将会编译成一个具有两个元素的数组，这些数组最终会放到一个数组中，返回一个二维数组
> -   Object.values()只返回自己的键值对中属性的值
> -   Object.getOwnPropertyDescriptors()
> -   padStart()。//'x'.padStart(4, 'ab') abax
> -   padEnd()。//'x'.padEnd(4, 'ab') xaba

#### ES9

> -   异步迭代器：使用 AsyncIterable 和 AsyncIterator 协议为异步迭代添加语法支持。该特性使创建异步生成器函数和方法的语法成为可能。
> -   为正则表达式添加 s (dotAll)标志：为这些表达式提供一致的行为。该特性旨在解决正则表达式中的点(.)不匹配行终止符的限制。s 标志改变了这一点。此标志将在选择的基础上运行，因此现有的正则表达式模式不会受到影响。
> -   Regexp(正则表达式) Unicode 属性转义：使开发者能够更好地访问 Unicode 字符属性。属性转义将以\p{…}和\P{…}的形式添加。
> -   Regexp 环视匹配断言：解决了环视（lookaround）的一个缺点，它是零宽度的断言，与字符串进行匹配，不消耗任何东西。使用隐藏的断言，开发人员可以确保模式之前有或没有另一个模式。例如：匹配美元的金额而不获取美元符号。
> -   Rest/spread 属性：提供一个较小的语法改进。
> -   prototype.finally()：用于在处理完资源后进行清理。
> -   Regexp 命名捕获组：用来标识捕获组，使它们更容易查找并使正则表达式更容易理解。以前，捕获组是通过数字访问的。
> -   模板文字的修订：为带标签的模板文字增加了语法的自由度。
> -   一个预期的功能，即 Function.prototype.toString 的更新被删除，因为仍然有人担心它正在解决中。 toString()方法会返回一个表示函数源代码的字符串

#### ES10

> 数组降维，递归地将数组展平到指定的深度，默认为 1

```code
const array = [1, [2, [3]]];
array.flat(); // → [1, 2, [3]]
array.flat(Infinity); // → [1, 2, 3]
[2, 3, 4].flatMap((x) => [x, x * 2]);
// → [2, 4, 3, 6, 4, 8]
const arr = ["Codedam", "is Awsome", "!"];
const mapResult = arr.map(item => item.split(" "));
console.log(mapResult); // [ [ 'Codedam' ], [ 'is', 'Awsome' ], [ '!' ] ]
```

> Object.fromEntries

> 我们之前已经在函数原型中使用了 toString 方法，但是在 ES2019 中它已被修改并包含函数内的注释，请注意它在 Arrow Functions 上不起作用。

```code
function /* comment */ foo /* another comment */() {}
// Before
console.log(foo.toString()); // function foo(){}
// Now ES2019
console.log(foo.toString()); // function /* comment */ foo /* another comment */ (){}
// Arrow Syntax
const bar /* comment */ = /* another comment */ () => {};
console.log(bar.toString()); // () => {}
```

> trimStart 和 trimEnd

```code
// Trim
const name = "   Codedam ";
console.log(name.trim()); // "Codedam"
// Trim Start
const description = "   Unlocks Secret Codes ";
console.log(description.trimStart()); // "Unlocks Secret Codes "
// Trim End
const category = "  JavaScript ";
console.log(category.trimEnd()); // "  JavaScript"
```
