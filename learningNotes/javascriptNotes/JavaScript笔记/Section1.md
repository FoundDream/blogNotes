# this 的指向

## this 的绑定规则

- 采用不同的方式调用函数，this 会指向不同的结果
  - 函数在调用时，JavaScript 会默认给 this 绑定一个值；
  - this 的绑定和定义的位置（编写的位置）没有关系；
  - this 的绑定和调用方式以及调用的位置有关系；
  - this 是在运行时被绑定的；

### 默认绑定

- 什么情况下使用默认绑定呢？独立函数调用。
  - 独立的函数调用我们可以理解成函数没有被绑定到某个对象上进行调用；
  - 函数定义在对象中，但是依旧可以独立调用
- 默认绑定时，this 绑定 window 对象（非严格模式下）

```js
// 案例一
var sayhi = function() {
  console.log("hi")
}

// 案例二
var obj = {
  name: "ziwen"
  foo: function() {
    console.log("hello,world")
  }
}
var bar = obj.foo
bar()

// 案例三：高阶函数
function test(fn) {
  fn()
}
test(obj.foo)
```

> 严格模式下，独立调用的函数中的 this 指向的是 undefined

> 高阶函数：接受一个或多个函数作为输入 or 输出一个函数

> 匿名函数：如果在传入一个函数时，我们没有指定这个函数的名词或者通过函数表达式指定函数对应的变量，那么这个函数称之为匿名函数

### 隐式绑定

- 隐式绑定是指通过某个对象进行调用的：
  - 也就是它的调用位置中，是通过某个对象发起的函数调用。
  - 此时 this 绑定为调用它的对象

```js
function foo() {
  console.log(this);
}

var obj = {
  bar: foo,
};

obj.bar(); // 此时this绑定为obj
```

### new 绑定

- JavaScript 中的函数可以当做一个类的构造函数来使用，也就是使用 new 关键字。
- 使用 new 关键字来调用函数是，会执行如下的操作：
  - 创建一个全新的对象；
  - 这个新对象会被执行 prototype 连接；
  - 这个新对象会绑定到函数调用的 this 上（this 的绑定在这个步骤完成）；
  - 如果函数没有返回其他对象，表达式会返回这个新对象；

```js
function foo() {
  console.log(this);
}

new foo();
```

### 显式绑定

- 隐式绑定有一个前提条件：
  - 必须在调用的对象内部有一个对函数的引用（比如一个属性）；
  - 如果没有这样的引用，在进行调用时，会报找不到该函数的错误；
  - 正是通过这个引用，间接的将 this 绑定到了这个对象上；
- 如果我们不希望在对象内部包含这个函数的引用，同时又希望在这个对象上进行强制调用，该怎么做呢？

```js
var obj = {
  name: "ziwen",
};

function foo() {
  console.log(this);
}

// 如果我们想绑定obj绑定到this，那就要这样做
// obj.bar = foo
// obj.bar()

// 但是这样做太麻烦了
// 所以我们可以用另一种方法
foo.call(obj);
```

#### call、apply、bind

- 通过 call 或者 apply 绑定 this 对象
  - JavaScript 所有的函数都可以使用 call 和 apply 方法
    - 第一个参数是相同的，要求传入一个对象；
  - 这个对象的作用是什么呢？就是给 this 准备的。
    - 在调用这个函数时，会将 this 绑定到这个传入的对象上。
  - 后面的参数，apply 为数组，call 为参数列表；
    - `func.apply(thisArg, [argsArray])` `func.call(thisArg, arg1, arg2, ...)`
- 通过 bind 绑定
- 如果我们希望一个函数总是显示的绑定到一个对象上，可以怎么做呢？
  - 使用 bind 方法，bind() 方法创建一个新的绑定函数（bound function，BF）；
  - 绑定函数是一个 exotic function object（怪异函数对象，ECMAScript 2015 中的术语）
  - 在 bind() 被调用时，这个新函数的 this 被指定为 bind() 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。

```js
function foo(name, age, address) {
  console.log(this);
  console.log(name, age, address); // "kobe" 18 usa
}

var obj = { name: "ziwen" };
var bar = foo.bind(obj, "kobe", 18);
bar("usa"); // 因为前面的参数我们已经绑定了，所以usa会到address里面
```

> 如果绑定一个字符串，或者数字，在非严格模式下，会转换成原始类型的包装类。严格模式下会直接是传入的值

## 内置函数的调用绑定

- 有些时候，我们会调用一些 JavaScript 的内置函数，或者一些第三方库中的内置函数。
  - 这些内置函数会要求我们传入另外一个函数；
  - 我们自己并不会显示的调用这些函数，而且 JavaScript 内部或者第三方库内部会帮助我们执行；
- 这些函数中的 this 又是如何绑定的呢？
  - 我们要根据一些经验

```js
// 1. 定时器 -> window
setTimeout(function () {
  console.log(this);
}, 1000);

// 2. 按钮的点击监听 -> DOM
var btnEl = document.querySelector("button");
btnEl.onclick = function () {
  console.log("btn的点击", this);
};

// 3. forEach -> 默认window，但是也可以自己绑定（可选参数）
var names = ["abc", "nba"];
names.forEach(function (item) {
  console.log(this);
}, thisArg);
```

## 规则优先级

- 默认规则的优先级最低
  - 毫无疑问，默认规则的优先级是最低的，因为存在其他规则时，就会通过其他规则的方式来绑定 this
- 显式绑定优先级高于隐式绑定
- new 绑定优先级高于隐式绑定
- new 绑定优先级高于 bind
  - new 绑定和 call、apply 是不允许同时使用的，所以不存在谁的优先级更高
  - new 绑定可以和 bind 一起使用，new 绑定优先级更高
- `new > 显式 > 隐式 > 默认`（粗暴的结论，因为 new 和 call，apply 不能同时使用）
- `bind > apply = call`

## this 规则之外

### 忽略显式绑定

- 情况一：如果在显示绑定中，我们传入一个 null 或者 undefined，那么这个显示绑定会被忽略，使用默认规则。
  - 但是在严格模式下，是可以成功绑定的

### 间接函数引用

- 情况二：创建一个函数的间接引用，这种情况使用默认绑定规则。
  - 赋值`(obj2.foo = obj1.foo)`的结果是 foo 函数；
  - foo 函数被直接调用，那么是默认绑定；

```js
var obj1 = {
  foo: function () {
    console.log(this);
  },
};

var obj2 = {};

(obj2.foo = obj1.foo)(); // 默认调用 window 严格模式下是undefined
```

> JavaScript 的赋值操作符返回被赋的值是为了方便链式赋值操作或者在条件语句中使用赋值操作。

### ES6 箭头函数

- 箭头函数不使用 this 的四种标准规则（也就是不绑定 this），而是根据外层作用域来决定 this。因为在箭头函数中，根本不存在 this，也就没有给 this 绑定的说法，所以就算我们用 apply 方法，也没有用

```js
var obj = {
  name: "obj",
  foo: function () {
    var bar = () => {
      console.log(this);
    };
    return bar;
  },
};

var fn = obj.foo();
fn.apply("bbb"); // obj
// 因为箭头函数没有this，所以无法绑定，所以往上一层作用域去查到，找到foo作用域，foo的this是obj，所以最终输出obj

var obj = {
  name: "obj",
  foo: () => {
    var bar = () => {
      console.log(this);
    };
    return bar;
  },
};

var fn = obj.foo();
fn.apply("bbb"); // window
/* 
因为箭头函数没有this，所以无法绑定，所以往上一层作用域去查到，找到foo，
但是foo也是箭头函数，foo也没有this，继续向上，找到window，所以最终输出window 
*/
```

- 写一个网络请求的实例
  - 这里我使用 setTimeout 来模拟网络请求，请求到数据后如何可以存放到 data 中呢？
  - 我们需要拿到 obj 对象，设置 data；
  - 但是直接拿到的 this 是 window，我们需要在外层定义：var \_this = this
  - 在 setTimeout 的回调函数中使用\_this 就代表了 obj 对象

```js
function request(url, callbackFn) {
  var results = ["nba", "cba"];
  callbackFn(results);
}

var obj = {
  names = [];
  network: function() {
    // 1. 早期方式
    // var _this = this
    // request('/name', function(res) {
    //   _this.names = [].concat(res)
    // }

    // 2. 箭头函数
    request("/name", res => {
      this.names = [].concat(res)
    })
  }
}

obj.newwork()

```

## 箭头函数 arrow function

- 箭头函数是 ES6 之后增加的一种编写函数的方法，并且它比函数表达式要更加简洁：
  - 箭头函数不会绑定 this、arguments 属性（用 ES6 语法 ...args 来代替）
  - 箭头函数不能作为构造函数来使用，因为没有原型 prototype（不能和 new 一起来使用，会抛出错误）

### 箭头函数的编写优化

- 优化一: 如果只有一个参数()可以省略
- 优化二: 如果函数执行体中只有一行代码, 那么可以省略大括号
  - 并且这行代码的返回值会作为整个函数的返回值
  - 一行代码中不能带 return 关键字，如果省略，需要带 return 一起省略
- 优化三: 如果函数执行体只有返回一个对象, 那么需要给这个对象加上()
  - 因为对象和函数的语法都有{}

```js
var names = ["abc", "cba"];
var nums = [2, 4, 1];
// 1. 优化一：其实可以不写item的括号，Prettier自动优化了
names.forEach((item) => {
  console.log(item);
});

// 2. 优化二
names.forEach((item) => console.log(item));
var newNums = nums.filter((item) => item % 2 === 0);

// 3. 优化三
var arr = () => {}; //这是一个执行体
var arr = () => ({ name: "ziwen" }); // 返回对象
```

## this 面试题

```js
// 第一题
var name = "window";
var person = {
  name: "person",
  sayName: function () {
    console.log(this.name);
  },
};
function sayName() {
  var sss = person.sayName;
  sss(); // window 默认调用
  person.sayName(); // person 隐式调用
  person.sayName(); // person 同上
  (b = person.sayName)(); // window 间接调用
}
sayName();
```

```js
// 第二题
var name = "window";
var person1 = {
  name: "person1",
  foo1: function () {
    console.log(this.name);
  },
  foo2: () => console.log(this.name),
  foo3: function () {
    return function () {
      console.log(this.name);
    };
  },
  foo4: function () {
    return () => {
      console.log(this.name);
    };
  },
};

var person2 = { name: "person2" };

person1.foo1(); // person1
person1.foo1.call(person2); //person2

person1.foo2(); // window
person1.foo2.call(person2); // window

person1.foo3()(); // window
person1.foo3.call(person2)(); // window
person1.foo3().call(person2); // person2

person1.foo4()(); // window
person1.foo4.call(person2)(); // person2
person1.foo4().call(person2); // person1
```

面试题 34....
