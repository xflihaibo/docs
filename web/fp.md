## 函数式编程

函数式编程（英语：functional programming），又称泛函编程，是一种编程范式，它将电脑运算视为数学上的函数计算，并且避免使用程序状态以及易变对象

说到函数式编程，大家可能第一印象都是学院派的那些晦涩难懂的代码，充满了一大堆抽象的不知所云的符号，似乎只有大学里的计算机教授才会使用这些东西。在曾经的某个时代可能确实如此，但是近年来随着技术的发展，函数式编程已经在实际生产中发挥巨大的作用了，越来越多的语言开始加入闭包，匿名函数等非常典型的函数式编程的特性，从某种程度上来讲，函数式编程正在逐步“同化”命令式编程

JavaScript 作为一种典型的多范式编程语言，这两年随着 React 的火热，函数式编程的概念也开始流行起来，RxJS、cycleJS、lodashJS、underscoreJS 等多种开源库都使用了函数式的特性。所以下面介绍一些函数式编程的知识和概念。

## 纯函数

相同的输入，永远得到相同的输出。而且没有任何可观察的副作用，也不依赖外部的环境变量

!> 可以有效的降低系统的复杂度，并且可以具有可缓存性

```javascript
var fp = [a, b, c, d, e, f];

// slice是纯函数，它没有副作用，对于固定的输入，输出总是固定的
fp.slice(0, 3); //[a,b,c]
fp.slice(0, 3); // [a,b,c]

// splice是不纯的，它有副作用，对于固定的输入，输出却不是固定的
fp.splice(0, 3); // [a,b,c]
fp.splice(0, 3); //[c,d,f]
```

## 函数的柯里化

函数柯里化（curry）的定义很简单：传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数

比如对于加法函数 var add = (x, y) =>　 x + y ，我们可以这样进行柯里化：

```jacascript
var add = function(x){ //比较容易读懂的ES5写法
    return function(y){
        return x + y
    }
}
var add = x => (y => x + y); //ES6写法，也是比较正统的函数式写法

var add2 = add(2);
add2(2); // 4
var add200 = add(200);
add200(80); // 280
```

?>事实上柯里化是一种“预加载”函数的方法，通过传递较少的参数，得到一个已经记住了这些参数的新函数，某种意义上讲，这是一种对参数的“缓存”，是一种非常高效的编写函数的方法;

## 函数组合 f(g(y(x))

学会了使用纯函数以及如何把它柯里化之后，我们会很容易写出这样的“包菜式”代码

```javascript
h(g(f(x)));
```

```javascript
//es5 两个函数的组合
var compose = function(f, g) {
    return function(x) {
        return f(g(x));
    };
};

//es6
var compose = (f, g) => x => f(g(x));
var add1 = x => x + 1;
var mul5 = x => x * 5;
compose(
    mul5,
    add1
)(2); //15
```

我们定义的 compose 就像双面胶一样，可以把任何两个纯函数结合到一起。

这种灵活的组合可以让我们像拼积木一样来组合函数式的代码

```javascript
var first = arr => arr[0];
var reverse = arr => arr.reverse();
var last = compose(
    first,
    reverse
);
last([1, 2, 3, 4, 5]); //5
```

### Point Free

不要命名转瞬即逝的中间变量

```javascript
var f = str => str.toUpperCase().split(' '); //这不Piont free
//这个函数中，我们使用了 str 作为我们的中间变量，但这个中间变量除了让代码变得长了一点以外是毫无意义的。下面改造一下这段代码：

var toUpperCase = word => word.toUpperCase();
var split = x => str => str.split(x);
var f = compose(
    split(' '),
    toUpperCase
);
f('abcd efgh'); //["ABCD", "EFGH"]
```
