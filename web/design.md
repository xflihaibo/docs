## 面向对象

**面向对象编程语言** （比如 C++ 和 Java），都有“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript 语言的对象体系，不是基于“类”的，而是基于构造函数（constructor）和原型链（prototype）。

!>构造函数就是一个普通的函数，但是有自己的特征和用法

### 继承

子类继承父类，继承可以把公共方法抽离出来，提高复用，减少冗余

### 封装

-   把数据封装起来
-   减少耦合，不该外部访问的不要让外部访问
-   利于数据的接口权限管理
-   ES6 目前不支持，一般认为\_开头的都会私有的，不要使用

### 多态

-   同一个接口可以不同实现
-   保持子类的开放性和灵活性
-   面向接口编程

## 面向切面编程

AOP(面向切面编程)的主要作用是把一些跟核心业务逻辑模块无关的功能抽离出来，这些跟业务逻辑无关的功能通常包括日志统计、安全控制、异常处理等。把这些功能抽离出来之后， 再通过“动态织入”的方式掺入业务逻辑模块中

### 优点

1. 可以保持业务逻辑模块的纯净和高内聚性。
2. 可以很方便地复用日志统计等功能模块。

```javascript
Function.prototype.before = function(beforefn) {
    var _self = this; //保存原函数引用
    return function() {
        //返回包含了原函数和新函数的"代理函数"
        beforefn.apply(this, arguments); //执行新函数，修正this
        return _self.apply(this, arguments); //执行原函数
    };
};

Function.prototype.after = function(afterfn) {
    var _self = this;
    return function() {
        var ret = _self.apply(this, arguments);
        afterfn.apply(this, arguments);
        return ret;
    };
};

var func = function() {
    console.log('2');
};

func = func
    .before(function() {
        console.log('1');
    })
    .after(function() {
        console.log('3');
    });

func();
```

## 设计模式

设计模式，是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性、程序的重用性。

### 目的

为了代码可重用性、让代码更容易被他人理解、保证代码可靠性。 设计模式使代码编写真正工程化；设计模式是软件工程的基石脉络，如同大厦的结构一样

### 设计模式五大原则

1.  单一职责原则
1.  开放封闭原则
1.  里氏替换原则
1.  接口隔离原则
1.  依赖反转原则

### S 单一职责原则

-   Single responsibility principle
-   一个程序只做好一件事
-   如果功能特别复杂就进行拆分

### O 开放封闭原则

-   Open Closed Principle
-   对扩展开放，对修改关闭
-   增加需求时，扩展新代码，而非修改已有代码
-   这是软件设计的终极目标

### L 里氏替换原则

-   Liskov Substitution Principle
-   子类能覆盖父类
-   父类能出现的地方子类就能出现
-   JS 使用比较少

### I 接口隔离原则

-   Interface Segregation Principle
-   保持接口的单一独立，避免出现胖接口
-   JS 中没有接口，使用较少
-   类似于单一职责原则，更关注接口

### D 依赖倒置原则

-   Dependence Inversion Principle
-   面向接口编程，依赖于抽象而不依赖于具体实现
-   使用方只关注接口而不关注具体类的实现
-   JS 中使用较少（没有接口，弱类型）

## 常见的设计模式

### 工厂模式

-   核心的工厂类不再负责所有的产品的创建，而是将具体创建的工作交给子类去做

```javascript
class Plant {
    constructor(name) {
        this.name = name;
    }
    grow() {}
}
class Apple extends Plant {
    constructor(name, taste) {
        super(name);
        this.taste = taste;
    }
    grow() {}
}
class Orange extends Plant {
    constructor(name, taste) {
        super(name);
        this.taste = taste;
    }
    grow() {}
}

class Factory {
    create(type) {
        switch (type) {
            case 'apple':
                return new Apple('🍎', '甜甜的');
            case 'orange':
                return new Orange('🍊', '酸酸的');
            default:
                throw new Error('错误❌');
        }
    }
}
let factory = new Factory();
let apple = factory.create('apple');
let orange = factory.create('orange');
console.log(apple.taste);
console.log(orange.taste);
react:
class Vnode {
    constructor(tag, attrs, children) {
        this.tag = tag;
        this.attrs = attrs;
        this.children = children;
    }
}
React.createElement  = function(tag, attrs, children) {
    return new Vnode(tag, attr, children);
};
```

#### 工厂方法模式

-工厂方法模式 Factory Method，又称多态性工厂模式。 -在工厂方法模式中，核心的工厂类不再负责所有的产品的创建，而是将具体创建的工作交给子类去做。

```code
class Plant {
    constructor(name) {
        this.name = name;
    }
    grow() {
        console.log('growing~~~~~~');
    }
}
class Apple extends Plant {
    constructor(name) {
        super(name);
        this.taste = '甜';
    }
}
class Orange extends Plant {
    constructor(name) {
        super(name);
        this.taste = '酸';
    }
}
class AppleFactory {
    create() {
        return new Apple();
    }
}
class OrangeFactory {
    create() {
        return new Orange();
    }
}
const settings = {
    apple: AppleFactory,
    orange: OrangeFactory
};
let apple = new settings['apple']().create();
console.log(apple);
let orange = new settings['orange']().create();
console.log(orange);
```

#### 抽象工厂

```code
class Button {
    render() {}
}
class AppleButton {
    render() {
        console.log('苹果按钮');
    }
}
class WindowButton {
    render() {
        console.log('Windows按钮');
    }
}

class Icon {
    render() {}
}
class AppleIcon {
    render() {
        console.log('苹果图标');
    }
}
class WindowIcon {
    render() {
        console.log('Windows图标');
    }
}
class Factory {
    createButton() {}
    createIcon() {}
}
class AppleFactory {
    createButton() {
        return new AppleButton();
    }
    createIcon() {
        return new AppleButton();
    }
}
class WindowsFactory {
    createButton() {
        return new WindowButton();
    }
    createIcon() {
        return new WindowIcon();
    }
}
const settings = {
    apple: AppleFactory,
    windows: WindowsFactory
};
let appleFactory = new settings['apple']();
appleFactory.createButton().render();
appleFactory.createIcon().render();

let windowsFactory = new settings['windows']();
windowsFactory.createButton().render();
windowsFactory.createIcon().render();
```

### 单例模式

保证一个类只有一个实例，并提供一个访问他的全局访问点，

```javascript
let __instance = (function() {
    let instance;
    return newInstance => {
        if (newInstance) instance = newInstance;
        return instance;
    };
})();

class Universe {
    constructor() {
        if (__instance()) return __instance();

        this.foo = 'bar';
        __instance(this);
    }
}

var CreateDiv = function() {
    var instance;
    var CreateDiv = function(html) {
        if (instance) {
            return instance;
        }
        this.html = html;
        this.init();
        return (instance = this);
    };
    CreateDiv.prototype.init = function() {
        var div = document.Element('div');
        div.innerHtml = this.html;
        document.body.appendChild(div);
    };
    return CreateDiv;
};
var a = new CreateDiv('a');
var b = new CreateDiv('b');
```

```code
code1:
function Window(name) {
    this.name = name;
}
Window.prototype.getName = function() {
    return this.name;
};
Window.getInstance = (function() {
    let instance;
    return function(name) {
        if (!instance) {
            instance = new Window(name);
        }
        return instance;
    };
})();
let w1 = Window.getInstance();
let w2 = Window.getInstance();
console.log(w1 === w2);

code2:
let Window = (function() {
    let window;
    let Window = function(name) {
        if (window) {
            return window;
        } else {
            this.name = name;
            return (window = this);
        }
    };
    Window.prototype.getName = function() {
        console.log(this.name);
    };
    return Window;
})();

let window1 = new Window('666');
let window2 = new Window('666');
window1.getName();
console.log(window1 === window2);
```

### 代理模式

为一个对象提供一个代用品或占位符，以便控制对他的访问

```javascript
var mgImag = (function() {
    var imgNode = document.createElement('img');
    document.body.appendChild(imgNode);
    return {
        setSrc: function(src) {
            imgNode.src = src;
        }
    };
})();

var ProxyImage = (function() {
    var img = new Image();
    img.onload = function() {
        myImage.setSrc(this.src);
    };
    return {
        setSrc: function(src) {
            mgImag.setSrc('loading.gif');
            img.src = src;
        }
    };
})();
ProxyImage.setSrc('xxxxxx.png');

class Peal {
    dosomething() {
        console.log('do something');
    }
}

class Proxy extends Real {
    constructor() {
        super();
    }
    dosomething() {
        setTimeout(super.dosomething, 1000 * 3);
    }
}
new Proxy().dosomething();
```

### 命令模式

命令模式中的命令指的是一个执行某些特定的事情的指令，有时候需要向某些特定事情的指令。

```javascript
var makeCommand = function(receiver, state) {
    return function(argument) {
        return receiver[state]();
    };
};
var Ryu = {
    attack: function() {
        console.log('攻击！');
    },
    defense: function() {
        console.log('防御');
    },
    crouch: function() {
        console.log('蹲下');
    }
};

var command = makeCommand(Ryu, 'attack');
command();
```

### 发布订阅模式

发布订阅模式又叫观察者模式，他定义对象间的一种一对多的依赖关系，当一个对象的状态发生变化时，所有依赖它的对象都将得到通知

```javascript
function Observer() {
    this.fns = [];
}
Observer.prototype = {
    subscribe: function(fn) {
        this.fns.push(fn);
    },
    unsubscribe: function(fn) {
        this.fns = this.fns.filter(function(el) {
            if (el !== fn) {
                return el;
            }
        });
    },
    update: function(o, thisObj) {
        var scope = thisObj || window;
        this.fns.forEach(function(el) {
            el.call(scope, o);
        });
    }
};

//测试
var o = new Observer();
var f1 = function(data) {
    console.log('Robbin: ' + data + ', 赶紧干活了！');
};

var f2 = function(data) {
    console.log('Randall: ' + data + ', 找他加点工资去！');
};

o.subscribe(f1);
o.subscribe(f2);

o.update('Tom 回来了！');

//退订 f1
o.unsubscribe(f1);
//再来验证
o.update('Tom 回来了！');

class Event {
    constructor() {
        this.subscribers = new Map([['any', []]]);
    }
    on(fn, type = 'any') {
        let subs = this.subscribers;
        if (!subs.get(type)) return subs.set(type, [fn]);
        subs.set(type, subs.get(type).push(fn));
    }
    emit(content, type = 'any') {
        for (let fn of this.subscribers.get(type)) {
            fn(content);
        }
    }
}

let event = new Event();
event.on(contenr => console.log(`get publish content:${content}`), 'myEvent');
event.emit('java ', 'myEvent');
```

### 职责链模式

使多个对象都有机会处理请求，从而避免请求的发送者和接受者之间的耦合关系，将这些关系连成一条链，并沿着这条链的传递请求，知道一个对象处理为止。

```javascript
var fn1=function(data){
if(data==1){
console.log('fn1=>'+data)
}else{
return 'next';
}

var fn2=function(data){
console.log('fn2=>'+data)
return 'next';
}
var fn3=function(data){
console.log('fn3=>'+data)
console.log('done')
}

Function.prototype.after=function(fn){
var self=this;
return function(){
var ret=self.apply(this,arguments);
if(ret=='next'){
return fn.apply(this,arguments)
}
return ret;
}
}
var order=fn1.after(fn2).after(fn3)
order(1)
```
