# Array

JavaScript 的 Array 对象是用于构造数组的全局对象，数组是类似于列表的高阶对象

## concat()

用于连接两个或多个数组，该方法不会改变现有的数组，而仅仅会返回被连接的新数组

-   语法：Arr.concat(arr1,arr2,……,arrn)
-   参数： arr1 该参数可以是具体的值，也可以是数组,对象,字符串,bool 值等。可以是任意多个
-   返回值：返回一个新的数组。该数组是通过把所有 arr1 参数添加到 arrayObject 中生成的。如果要进行 concat() 操作的参数是数组，那么添加的是数组中的每一个元素，而不是数组

```javascript
let arr = [1, 2];
let arr2 = [123, 456, 678];
let obj = { name: '王二', age: 123 };
let initbool = false;
let newarr = arr.concat([3, 4, 5], 7, 8, [9, 10]);
let newarr2 = arr.concat(3, 4, 5, arr2, obj, initbool);
console.log(arr); //[1, 2]
console.log(newarr); //[1, 2, 3, 4, 5, 7, 8, 9, 10]
console.log(newarr2); //[1, 2, 3, 4, 5, 123, 456, 678, {name: "王二", age: 123}, false]
```

## copyWithin()

(ES6 新增) 将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。

-   语法： Arr.copyWithin(target, start = 0, end = this.length)
-   参数：传入的值 默认为 number,传入其他类型值 (bool,string,array,object,undefined)会进行类型转化成 number 类型(参数为 NaN 的话为默认值)

    -   target ：必需 从该位置开始替换数据。
    -   start ：可选 从该位置开始读取数据，默认为 0 。如果为负值，表示倒数。
    -   end ：可选 到该位置前停止读取数据，默认等于数组长度。如果为负值，表示倒数。

-   返回值：返回当前数组。也就是说，使用这个方法，会修改当前数组

```javascript
let arr = [1, 2, 3, 4, 5];
let arr1 = [1, 2, 3, 4, 5];
let arr2 = [1, 2, 3, 4, 5];
let arr3 = [1, 2, 3, 4, 5];
let arr4 = [1, 2, 3, 4, 5];
let arr5 = [1, 2, 3, 4, 5];
let arr6 = [1, 2, 3, 4, 5];
let arr7 = [1, 2, 3, 4, 5];
let arr8 = [1, 2, 3, 4, 5];
let arr9 = [1, 2, 3, 4, 5];
let arr10 = [1, 2, 3, 4, 5];
let newarr = arr.copyWithin(0, 3, 4);
arr1.copyWithin(0, 3);
arr2.copyWithin(2);
arr3.copyWithin(1, 2, 4);
arr4.copyWithin(false, 3);
arr5.copyWithin(true, 3);
arr6.copyWithin(2, NaN);
arr7.copyWithin(2);
arr8.copyWithin(2, -1);
arr9.copyWithin(2, -2);
arr10.copyWithin(2, -2, -1);
console.log(arr); //[4, 2, 3, 4, 5]
console.log(newarr); //[4, 2, 3, 4, 5]
console.log(arr1); //[4, 5, 3, 4, 5]
console.log(arr2); //[1, 2, 1, 2, 3]
console.log(arr3); //[1, 3, 4, 4, 5]
console.log(arr4); //[4, 5, 3, 4, 5]
console.log(arr5); //[1, 4, 5, 4, 5]
console.log(arr6); //[1, 2, 1, 2, 3]
console.log(arr7); //[1, 2, 1, 2, 3]
console.log(arr8); //[1, 2, 5, 4, 5]
console.log(arr9); //[1, 2, 4, 5, 5]
console.log(arr10); //[1, 2, 4, 4, 5]
```

## entries()

(ES6 新增) 是对键值对的遍历 方法返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键/值对,不会改变原数组

-   语法：Array.entries()
-   参数：
-   返回值：返回一个新的 Array Iterator 对象,该对象包含数组中每个索引的键/值对

```javascript
let arr = ['a', 'b', 'c'];
let iterator1 = arr.entries();
console.log(iterator1); //Iterator
console.log(iterator1.next()); //{value: Array(2), done: false}
console.log(iterator1.next().value); //[1, "b"]
console.log(iterator1.next().value); //[2, "c"]
console.log(iterator1.next().value); // undefined
console.log(arr); // ["a", "b", "c"]
```

## every()

用于检测数组所有元素是否都符合指定条件（通过函数提供）

-   语法：Arr.every(function(currentValue,index,arr), thisValue)
-   参数：
-   function(currentValue, index,arr) 必须。函数，数组中的每个元素都会执行这个函数
    -   currentValue:必须。当前元素的值
    -   index:可选。当前元素的索引值
    -   arr:可选。当前元素属于的数组对象
-   thisValue:可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。如果省略了 thisValue ，"this" 的值为 "undefined"
-   返回值：布尔值。如果所有元素都通过检测返回 true，否则返回 false

```javascript
const isBigEnough = (element, index, array) => {
    return element >= 10;
};
let passed1 = [12, 5, 8, 130, 44].every(isBigEnough);
let passed2 = [12, 54, 18, 130, 44].every(isBigEnough);
console.log(passed1); // false
console.log(passed2); // true
```

## fill()

(ES6 新增)用一个固定值填充一个数组中从起始索引到终止索引内的全部元素

-   语法：Arr.fill(value, start, end)
-   参数：
-   value:用来填充数组元素的值
-   start:可选 起始索引，默认值为 0
-   end:可选 终止索引，默认值为 this.length。
-   返回值：修改后的原数组。

```javascript
let arr1 = [1, 2, 3];
let arr2 = [1, 2, 3];
let arr3 = [1, 2, 3];
let arr4 = [1, 2, 3];
let arr5 = [1, 2, 3];
let arr6 = [1, 2, 3];
let arr7 = [1, 2, 3];
let arr8 = [1, 2, 3];
let arr9 = [1, 2, 3];
let newarr = arr1.fill(7);
arr2.fill(4);
arr3.fill(4, 1);
arr4.fill(4, 1, 2);
arr5.fill(4, 1, 1);
arr6.fill(4, 3, 3);
arr7.fill(4, -3, -2);
arr8.fill(4, NaN, NaN);
arr9.fill(4, 3, 5); // [1, 2, 3]
console.log(arr1); //[7, 7, 7]
console.log(newarr); //[7, 7, 7]
console.log(arr2); // [4, 4, 4]
console.log(arr3); // [1, 4, 4]
console.log(arr4); // [1, 4, 3]
console.log(arr5); // [1, 4, 3]
console.log(arr6); // [1, 2, 3]
console.log(arr7); // [1, 2, 3]
console.log(arr8); // [4, 2, 3]
console.log(arr9); // [1, 2, 3]
```

## filter()

创建一个新数组, 其包含通过所提供函数实现的测试的所有元素

-   语法：arr.filter(callback(element index array),thisArg])
-   参数：
-   callback 用来测试数组的每个元素的函数。调用时使用参数 (element, index, array)。返回 true 表示保留该元素（通过测试），false 则不保留。它接受三个参数
    -   element:当前在数组中处理的元素
    -   index:可选 正在处理元素在数组中的索引
    -   array:可选 调用了 filter 筛选器的数组
-   thisArg 可选。执行 callback 时的用于 this 的值。
-   返回值：一个新的通过测试的元素的集合的数组，如果没有通过测试则返回空数组

```javascript
let arr = [1, 2, 4, 5, 6, 9, 10, 15];
let newarr = arr.filter(function(x) {
    return x % 2 !== 0;
});
console.log(arr); // [1, 2, 4, 5, 6, 9, 10, 15]
console.log(newarr); //[1, 5, 9, 15]
//去重
let arr2 = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
let arr3 = arr2.filter(function(element, index, self) {
    return self.indexOf(element) === index;
});
console.log(arr3); // ["apple", "strawberry", "banana", "pear", "orange"]
```

## find()

(ES6 新增) 用来查找目标元素，找到就返回该元素，找不到返回 undefined

-   语法：arr.find(callback(element index array),thisArg])
-   参数：
-   callback 在数组每一项上执行的函数，接收 3 个参数
    -   element:当前遍历到的元素
    -   index:可选 当前遍历到的索引
    -   array:可选 数组本身
-   thisArg 可选。指定 callback 的 this 参数。
-   返回值：当某个元素通过 callback 的测试时，返回数组中的一个值，否则返回 undefined。

```javascript
let arr1 = [1, 2, 3, 4, 5, 6, 7, 8];
let arr2 = arr1.find((value, index, arr) => {
    return value > 4;
});
let arr3 = arr1.find((value, index, arr) => {
    return value > 14;
});
console.log(arr1); // [1, 2, 3, 4, 5, 6, 7, 8]
console.log(arr2); //5
console.log(arr3); //undefined
```

## findIndex()

(ES6 新增) 方法返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1

-   语法：arr.findIndex(callback(element index array),thisArg])
-   参数：
-   callback 在数组每一项上执行的函数，接收 3 个参数
    -   element:当前遍历到的元素
    -   index:可选 当前遍历到的索引
    -   array:可选 数组本身
-   thisArg 可选。指定 callback 的 this 参数。
-   返回值：返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

```javascript
let arr1 = [1, 2, 3, 4, 5, 6, 7, 8];
let arr2 = arr1.findIndex((value, index, arr) => {
    return value > 4;
});
let arr3 = arr1.findIndex((value, index, arr) => {
    return value > 14;
});
console.log(arr1); // [1, 2, 3, 4, 5, 6, 7, 8]
console.log(arr2); //4
console.log(arr3); //-1
```

## forEach()

对数组的每个元素执行一次提供的函数

-   语法：arr.forEach(callback(currentValue index array),thisArg])
-   参数：
-   callback 在数组每一项上执行的函数，接收 3 个参数
    -   currentValue:数组中正在处理的当前元素
    -   index:可选 数组中正在处理的当前元素的索引。
    -   array:可选 forEach()方法正在操作的数组。
-   thisArg 可选。指定 callback 的 this 参数。
-   返回值：undefined, 对原数组的操作有影响

```javascript
let arr = [{ a: 1 }, {}];
arr.forEach(function(item, idx) {
    item.b = idx;
});
console.log(arr); // [{a: 1, b: 0}, {b: 1}]
```

## from()

(ES6 新增) from() 方法用于通过拥有 length 属性的对象或可迭代的对象来返回一个数组。如果对象是数组返回 true，否则返回 false。

-   语法：Array.from(object, mapFunction, thisValue)
-   参数：
-   object:必需，要转换为数组的对象。
-   mapFunction:可选，数组中每个元素要调用的函数。
-   thisValue:可选，映射函数(mapFunction)中的 this 对象。
-   返回值：对象是数组返回 true，否则返回 false

```javascript
let setObj = new Set(['a', 'b', 'c']);
let arr = Array.from(setObj);
console.log(arr); //["a", "b", "c"]
console.log(Array.from([1, 2, 3], x => x + x)); //[2, 4, 6]
```

## includes()

(ES6 新增)方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回 false。

-   语法：arr.includes(searchElement, fromIndex)
-   参数：
-   searchElement :需要查找的元素值
-   fromIndex 从该索引处开始查找 searchElement。如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。
-   返回值：如果包含则返回 true，否则返回 false; (includes 方法使用全等（===）来判断一个元素是否符合您的搜索)

```javascript
[1, 2, 3].includes(2); // true
[1, 2, 3].includes(4); // false
[1, 2, NaN].includes(NaN); // true
let e1 = { name: 'zs', age: '12' };
let e2 = { name: 'ls', age: '13' };
let arr1 = [e1, e2];
let arr4 = arr1.includes(e1);
console.log(arr4); //true
```

## indexOf()

> 方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

-   语法：arr.indexOf(searchElement[, fromIndex = 0])
-   参数：
-   searchElement: 要查找的元素
-   fromIndex: 开始查找的位置。如果该索引值大于或等于数组长度，意味着不会在数组里查找，返回-1。如果参数中提供的索引值是一个负值，则将其作为数组末尾的一个抵消，即-1 表示从最后一个元素开始查找，-2 表示从倒数第二个元素开始查找 ，以此类推。 注意：如果参数中提供的索引值是一个负值，并不改变其查找顺序，查找顺序仍然是从前向后查询数组。如果抵消后的索引值仍小于 0，则整个数组都将会被查询。其默认值为 0,indexOf 方法使用全等（===）来判断一个元素是否符合您的搜索
-   返回值：首个被找到的元素在数组中的索引位置; 若没有找到则返回 -1

```javascript
let arr = [
    { name: 'zs', age: '12' },
    { name: 'ls', age: '13' }
];
let index = arr.indexOf({ name: 'zs', age: '12' });
console.log(index); //-1
let e1 = { name: 'zs', age: '12' };
let e2 = { name: 'ls', age: '13' };
let arr1 = [e1, e2];
let index1 = arr1.indexOf(e2);
console.log(index1); //1
```

## isArray()

> isArray() 方法用于判断一个对象是否为数组。如果对象是数组返回 true，否则返回 false。

-   语法：Array.isArray(obj)
-   参数：
-   obj:必需，要判断的对象。
-   返回值：布尔值，如果对象是数组返回 true，否则返回 false。

```javascript
console.log(Array.isArray([])); //true
console.log(Array.isArray([1])); //true
console.log(Array.isArray(new Array())); //true
console.log(Array.isArray()); //false
console.log(Array.isArray({})); //false
console.log(Array.isArray(null)); //false
console.log(Array.isArray(undefined)); //false
console.log(Array.isArray(17)); //false
console.log(Array.isArray('Array')); //false
console.log(Array.isArray(true)); //false
console.log(Array.isArray(false)); //false
```

## join()

方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。

-   语法：Arr.join(separator)
-   参数：
-   separator: 可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。
-   返回值：返回一个字符串。该字符串是通过把 Arr 的每个元素转换为字符串，然后把这些字符串连接起来，在两个元素之间插入 separator 字符串而生成的。

```javascript
let elements = ['1', '2', '3'];
console.log(elements.join());
console.log(elements.join('+'));
console.log(elements.join('-'));
```

## keys()

(ES6 新增) keys() 方法用于从数组创建一个包含数组键的可迭代对象。如果对象是数组返回 true，否则返回 false。

-   语法：arr.keys()
-   参数：
-   返回值：一个数组可迭代对象

```javascript
let arr = ['a', 'b', 'c'];
let iterator = arr.keys();
console.log(iterator.next()); // { value: 0, done: false }
console.log(iterator.next()); // { value: 1, done: false }
console.log(iterator.next()); // { value: 2, done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

## lastIndexOf()

lastIndexOf() 方法可返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。如果要检索的字符串值没有出现，则该方法返回 -1。

-   语法：array.lastIndexOf(item,start)
-   参数：
    item: 必需。规定需检索的字符串值
    start: 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 stringObject.length -1。如省略该参数，则将从字符串的最后一个字符处开始检索。
-   返回值：如果在 stringObject 中的 fromindex 位置之前存在 searchvalue，则返回的是出现的最后一个 searchvalue 的位置。

```javascript
let arr = ['ab', 'cd', 'ef', 'ab', 'cd'];
console.log(arr.lastIndexOf('cd')); //4
console.log(arr.lastIndexOf('cd', 2)); //1
console.log(arr.lastIndexOf('ab', -3)); //0
```

## map()

它创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果

-   语法：arr.map(function(currentValue,index,arr), thisValue)
-   参数：
    -   currentValue: 必须。当前元素的值
    -   index: 可选。当期元素的索引值
    -   arr: 可选。当期元素属于的数组对象
-   thisValue 可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。如果省略了 thisValue ，"this" 的值为 "undefined"
-   返回值：返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

```javascript
let arr1 = [1, 4, 9, 16];
const arr2 = arr1.map(x => x * 2);
console.log(arr1); //[1, 4, 9, 16]
console.log(arr2); //[2, 8, 18, 32]
```

## pop()

用于删除数组的最后一个元素并返回删除的元素。(此方法改变数组的长度！)

-   语法：arr.pop()
-   参数：
-   返回值：返回删除的元素。(改变了原数组长度)

```javascript
let plants = ['kale', 'tomato'];
console.log(plants.pop()); //tomato
console.log(plants); // ["broccoli", "cauliflower", "cabbage", "kale"]
console.log(plants.pop()); //kale
console.log(plants); //[]
console.log(plants.pop()); //undefined
```

## push()

向数组的末尾添加一个或多个元素，并返回新的长度。(此方法改变数组的长度！)

-   语法：arr.push(item1, item2, ..., itemX)
-   参数：
    -item1, item2, ..., itemX:必需。要添加到数组的元素。
-   返回值：数组新长度。

```javascript
let arr = ['pigs', 'goats', 'sheep'];
console.log(arr.push('cows')); //4
console.log(arr);
['pigs', 'goats', 'sheep', 'cows'];
console.log(arr.push(['hello', 'world'])); //5
console.log(arr); //["pigs", "goats", "sheep", "cows", ["hello", "world"]]
console.log(arr.push('hello', 'world')); //7
console.log(arr); //["pigs", "goats", "sheep", "cows", ["hello", "world"], "hello", "world"]
```

## reduce()

方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值,可以作为一个高阶函数，用于函数的 compose;可以作为一个高阶函数，用于函数的 compose;reduce 对于空数组是不会执行回调函数的

-   语法：arr.reduce(function(total, currentValue, currentIndex, arr), initialValue)
-   参数：
    -   total: 必需。初始值, 或者计算结束后的返回值。
    -   currentValue: 必需。当前元素
    -   currentIndex: 可选。当前元素的索引
    -   arr: 可选。当前元素所属的数组对象。
-   initialValue 可选。传递给函数的初始值
-   返回值：返回计算结果

```javascript
let items = [10, 80, 100];
let add = (sumSoFar, item) => {
    return sumSoFar + item;
};
let total = items.reduce(add, 0);
let total1 = items.reduce(add, 10);
console.log(items); //[10, 80, 100]
console.log(total); //190
console.log(total1); //200
```

## reduceRight()

reduceRight() 方法的功能和 reduce() 功能是一样的，不同的是 reduceRight() 从数组的末尾向前将数组中的数组项做累加。

-   语法：arr.reduceRight(function(total, currentValue, currentIndex, arr), initialValue)
-   参数：
    -   total: 必需。初始值, 或者计算结束后的返回值。
    -   currentValue: 必需。当前元素
    -   currentIndex: 可选。当前元素的索引
    -   arr: 可选。当前元素所属的数组对象。
-   initialValue 可选。传递给函数的初始值
-   返回值：返回计算结果

```javascript
let items = [10, 80, 100];
let add = (sumSoFar, item) => {
    return sumSoFar + item;
};
let total = items.reduceRight(add, 0);
let total1 = items.reduceRight(add, 10);
console.log(items); //[10, 80, 100]
console.log(total); //190
console.log(total1); //200
```

## reverse()

方法用于颠倒数组中元素的顺序

-   语法：arr.reverse()
-   参数：
-   返回值：颠倒顺序后的数组。(原数组也会改变)

```javascript
let arr1 = [0, 1, 5, 10, 15];
let arr2 = arr1.reverse();
console.log(arr1); //[15, 10, 5, 1, 0]
console.log(arr2); //[15, 10, 5, 1, 0]
```

## shift()

用于把数组的第一个元素从其中删除，并返回第一个元素的值。(此方法改变数组的长度！)

-   语法：arr.shift()
-   参数：

-   返回值：数组原来的第一个元素的值（移除的元素）

```javascript
var arr = [1, 2];
let arr1 = arr.shift();
console.log(arr); //[2]
console.log(arr1); //1
let arr2 = arr.shift();
console.log(arr2); //2
let arr3 = arr.shift();
console.log(arr3); //undefined
```

## slice()

可从已有的数组中返回选定的元素 并以新的字符串返回被提取的部分(改变原始数组)

-   语法：arr.slice(start, end)
-   参数：
    -   start: 可选。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推
    -   end: 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。
-   返回值：返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。

```javascript
let arr = [3, 5, 7, 9];
let arr1 = arr.splice(1, 2);
let arr2 = [3, 5, 7, 9];
let arr3 = arr2.splice(1);
console.log(arr); //[3, 9]
console.log(arr1); //[5, 7]
console.log(arr2); //[3]
console.log(arr3); //[5, 7, 9]
```

## some()

用于检测数组中的元素是否有满足指定的条件

-   语法：arr.some(function(currentValue,index,arr), thisValue)
-   参数：
    -   currentValue: 必须。当前元素的值
    -   index: 可选。当期元素的索引值
    -   arr: 可选。当期元素属于的数组对象
-   thisValue 可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。如果省略了 thisValue ，"this" 的值为 "undefined"
-   返回值：布尔值。如果数组中有一个元素满足条件返回 true，否则返回 false。

```javascript
let arr = [1, 2, 3, 4, 5];
let arr1 = arr.some((elem, index, arr) => {
    return elem >= 4;
});
console.log(arr); // [1, 2, 3, 4, 5]
console.log(arr1); //true
```

## sort()

法用于对数组的元素进行排序 排序顺序可以是字母或数字，并按升序或降序。默认排序顺序为按字母升序。(改变了原数组)

当数字是按字母顺序排列时"40"将排在"5"前面。使用数字排序，你必须通过一个函数作为参数来调用。函数指定数字是按照升序还是降序排列。这些说起来可能很难理解，你可以通过本页底部实例进一步了解它。这种方法会改变原始数组！

-   语法：arr.sort(sortfunction)
-   参数：
    -   sortfunction: 可选。规定排序顺序。必须是函数。
-   返回值：数组的引用。请注意，数组在原数组上进行排序，不生成副本

```javascript
let NumAscSort = (a, b) => {
    return a - b;
};
let NumDescSort = (a, b) => {
    return b - a;
};
var arr = [90, 88, 93, 106, 20, 10, 66];
let arr1 = arr.sort(NumDescSort);
console.log(arr); //[106, 93, 90, 88, 66, 20, 10]
console.log(arr1); //[106, 93, 90, 88, 66, 20, 10]
let arr2 = arr.sort(NumAscSort);
console.log(arr2); //[10, 20, 66, 88, 90, 93, 106]
```

## splice()

用于插入、删除或替换数组的元素

-   语法：array.splice(index,howmany,item1,.....,itemX)
-   参数：
    -   index: 必需。规定从何处添加/删除元素。该参数是开始插入和（或）删除的数组元素的下标，必须是数字。
    -   howmany: 必需。规定应该删除多少元素。必须是数字，但可以是 "0"。如果未规定此参数，则删除从 index 开始到原数组结尾的所有元素
    -   item1, ..., itemX: 可选。要添加到数组的新元素
-   返回值：如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。

```javascript
let arr = [1, 2, 3, 4, 5];
let arr2 = arr.splice(0, 1);
console.log(arr); // [2, 3, 4, 5]
console.log(arr2); // [1]
let arr3 = arr.splice(0, 1, 8, 9, 10);
console.log(arr); //[8, 9, 10, 3, 4, 5]
console.log(arr3); //[2]
```

## toLocaleString()

(es6 新增)返回一个字符串表示数组中的元素。数组中的元素将使用各自的 toLocaleString 方法转成字符串，这些字符串将使用一个特定语言环境的字符串（例如一个逗号 ","）隔开。

-   语法：arr.toLocaleString(function(currentValue,index,arr), thisValue)
-   参数：
    -   locales: 可选。带有 BCP 47 语言标记的字符串或字符串数组，关于 locales 参数的形式与解释，请看 Intl 页面
    -   options: 可选。一个可配置属性的对象
-   返回值：表示数组元素的字符串

```javascript
let arr = ['￥7', 500, 8123, 12];
let arr1 = arr.toLocaleString('ja-JP', { style: 'currency', currency: 'JPY' });
console.log(arr); //["￥7", 500, 8123, 12]
console.log(arr1); //￥7,￥500,￥8,123,￥12"
```

## toString()

可把数组转换为字符串，并返回结果

-   语法：arr.toString()
-   参数：

-   返回值：可把数组转换为字符串，并返回结果

```javascript
let arr = [1, 'heoolo', false, { name: 'zs', age: 12 }];
let arr1 = arr.toString();
console.log(arr); //[1, 'heoolo', false, {name:'zs',age:12}];
console.log(arr1); //1,heoolo,false,[object Object]
```

## unshift()

可向数组的开头添加一个或更多元素，并返回新的长度。(改变数组的长度)

-   语法：arr.unshift(item1,item2, ..., itemX)
-   参数：
    -   item1,item2, ..., itemX: 可选。向数组起始位置添加一个或者多个元素。
-   返回值：返回一个新数组的长度.

```javascript
let arr = ['张三', '李四', '王五'];
let count = arr.unshift('赵六', '小明');
console.log(count); //5
console.log(arr); // ["赵六", "小明", "张三", "李四", "王五"]
```

## valueOf()

返回 Array 对象的原始值。

-   语法：arr.valueOf()
-   参数：
-   返回值：valueOf() 返回数组值(不改变原始数组)

```javascript
let arr = ['2', '4', '5', '8'];
let arr1 = arr.valueOf();
console.log(arr); //["2", "4", "5", "8"]
console.log(arr1); //["2", "4", "5", "8"]
```
