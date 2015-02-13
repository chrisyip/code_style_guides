- [JavaScript Style Guide](#javascript-style-guide)
	- [EditorConfig](#editorconfig)
	- [File Encodings](#file-encodings)
	- [Naming Conventions](#naming-conventions)
		- [Files](#files)
			- [Node.js](#nodejs)
			- [Browsers](#browsers)
		- [Codes](#codes)
	- [Commas](#commas)
	- [Whitespaces and Semicolons](#whitespaces-and-semicolons)
	- [Braces, Brackets and Square Brackets](#braces-brackets-and-square-brackets)
	- [Indentations](#indentations)
	- [Chains](#chains)
	- [Quotes](#quotes)
	- [Variables](#variables)
	- [Types](#types)
	- [Numbers](#numbers)
	- [Objects](#objects)
		- [Accessors](#accessors)
			- [`Object.defineProperty()` and `Object.defineProperties()`](#objectdefineproperty-and-objectdefineproperties)
	- [Arrays](#arrays)
	- [Strings](#strings)
		- [`RegExp.exec` vs `String.match`](#regexpexec-vs-stringmatch)
	- [Functions](#functions)
		- [Arguments](#arguments)
		- [V8 Optimization](#v8-optimization)
	- [Scoping](#scoping)
	- [Eval](#eval)
	- [With](#with)
	- [Exceptions](#exceptions)
	- [Constructors and Prototypes](#constructors-and-prototypes)
	- [Namespaces](#namespaces)
	- [Conditional Expressions and Comparisons](#conditional-expressions-and-comparisons)
	- [Comments](#comments)
	- [Tag Your Codes](#tag-your-codes)
	- [DOM](#dom)
	- [jQuery](#jquery)
	- [ECMAScript Compatibility](#ecmascript-compatibility)
	- [Meta](#meta)

# JavaScript Style Guide

## EditorConfig

建议选择支持 [EditorConfig](http://editorconfig.org/) 的编辑器，并安装相应插件，在项目根目录建立一个 `.editconfig` 并插入以下内容：

```
[*.js]
charset = utf-8
end_of_line = lf
insert_final_newline = true
indent_style = space
indent_size = 2
trim_trailing_whitespace = true
```

## File Encodings

确保编辑器 / IDE 使用的编码为 UTF-8 without BOM。如不能确定使用的编辑器 / IDE 的编码，请使用 Atom、Sublime Text、WebStorm 等工具，并保持默认编码设置。

## Naming Conventions

### Files

- 使用 **半角小写英文字母（单词）和数字**
- 使用 **半角的 `-` 和 `.` 分割单词**
- 以依赖库作为前缀

```
utils.js
date-formater.js
```

#### Node.js

- 请勿包含版本号

#### Browsers

- 如非必要，请勿包含版本号
- 以依赖库作为前缀
- 除了已压缩文件外，请勿添加 `.min`。

示例：

    jquery.slideshow.js

### Codes

- 命名需选择有意义的名字，除了默认成俗的名字外，尽量不要使用简写形式
- 虽然 JavaScript 支持 Unicode 字符，但请使用 **`[a-zA-Z0-9_\$]`**
- 使用[驼峰命名法](http://zh.wikipedia.org/wiki/%E9%A7%9D%E5%B3%B0%E5%BC%8F%E5%A4%A7%E5%B0%8F%E5%AF%AB)（camel case），变量和函数使用小驼峰，如 `getElementById`，类、构造函数和枚举类型使用大驼峰，如 `DocumentFragment`
- 常量 **所有字母均大写并使用 `_` 分割单词** ，如 `Number.MAX_VALUE`
- 尊重惯例，避免使用常用库、框架名，如 `$ = {}`、`jQuery = {}`、`_ = {}`
- 使用 `_` 作为私有变量的前缀，如 `_index = arr.indexOf(value)`
- `Boolean` 变量、函数请加上 `is`、`has` 前缀
- 当保存 `this` 对象时，尽量使用可对应上下文的命名，或使用 `self` 等等

```js
// bad
valid = true;
k = 'word'
hasAttr = function (e, a) {
  var _a = e.getAttribute(a);
  return _a === null;
};

function user (opts) {
  this.name = opts.name;
  this.ID = opts.ID;
}

$form.on('submit', function(){
  var that = this;
});

// good
isValid = true;
keyword = 'word';
hasAttr = function (elem, attr) {
  var _attr = elem.getAttribute(attr);
  return _attr === null;
}

function User (options) {
  this.name = options.name;
  this.id = options.id;
}

$form.on('submit', function(){
  var rootForm = this;
  // or
  var self = this;
});
```

## Commas

逗号一律放在后面:

    var foo = 1,
        bar = false,
        arr = [
          1,
          2
        ],
        obj = {
          foo: 'foo',
          bar: 'bar'
        }
    ;

    function (argv1,
              argv2) {}

禁止添加多余的逗号（[IE bugs](http://tobyho.com/2014/01/07/js-trailing-comma-remover/)）：

    // bad
    var obj = {
          foo: 'foo',
          bar: 'bar',
        };

## Whitespaces and Semicolons

- 请用一个空格分割关键字、变量名、操作符、逗号、值
- 请不要省略分号
- 冒号仅在三元运算中需要空格分割

```js
// bad
typeof(foo)

// good
if (data && context) {
  // ..
} else {
  // ..
}

switch (context) {
  case true:
    break;
  case false:
    break;
  default:
    // ..
}

for (var i = 0; i < len; i++) {
  // ..
}

while (true) {
  // ..
}

var foo = 1 + 2;
var bar = (foo + 1) / 2;
bar = (bar ? 1 : 2) * 3;

var baz = {
  foo: 1,
  bar: 2
}
```

`function`：

- 请在 `function` 关键字、函数名、括号和大括号之间插入一个空格
- 如果函数没有名字和参数，可省略名字前后和括号前后的空格

```js
function foo (a, b) {

}

var bar = function(){

};

var foobar = function (a) {

};
```

`Array` & `Object`：

- `[]` 之间可插入空格
- `{}` 之间 **需** 插入空格

```js
var foo = [1, 2];
var bar = { baz: 'baz' };
```

## Braces, Brackets and Square Brackets

左大括号（花括号）置于行尾，右大括号放在代码块的下一行：

```js
if (foo) {
  // ..
} else {
  // ..
}

foo = {
  bar: 1
};

bar = function(){
  // ..
};
```

所有代码块需放在大括号（花括号）内（[ES 6 新语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/arrow_functions)除外）：

```js
// bad
if (false) return;

while (true)
  fn();

arr.map(function (elem) { return elem * 2; });

// good
if (false) {
  return;
}

while (true) {
  fn();
}

arr.map(function (elem) {
  return elem * 2;
});

[1, 2, 3].map(x => x * 2) // 2, 4, 6
```

括号、方括号通常放置在一行，如果遇到过长需要换行的时候，参考大括号（花括号）：

```js
// good
var foo, bar;

bar = (foo ? 'foo' : 'bar') + 'foobar';

fn(
  null,
  foo,
  bar
);

foo = [1, 2, 3];

bar = [
  1,
  2,
  3,
  4
];
```

## Indentations

- 以两个空格为单位
- 多行运算符以第一个运算对象为基准对齐，运算符置于行尾
- 函数参数以第一个参数或左括号为基准对齐
- `if`、`while` 以第一个条件为基准对齐
- `for` 以各个表达式各自对齐
- 多行三元运算符以第一个运算对象为基准对齐并进行一级锁进，运算符置于行尾

```js
// good
var str = 'hello' +
          ' ' +
          'world';

if (typeof str === 'string' &&
    str == 'hello wolrd') {
}

foo = function (arg1, arg2,
                arg3, arg4,
                arg5) {
};

var isEmpty = str.length == 0 ?
                true :
                false;

$('body').children()
  .first();

$('form')
  .on('submit', ajaxSubmit)
  .find('input')
    .on('input', validate)
    .end()
  .prop('novalidate', true);

// 以下代码仅供示例，实际编写代码时，应避免这种情况
for (var i = 0,
         j = 0,
         m = 0;
     i < 10 &&
     j < 10 &&
     m > 0;
     i++) {
  // ..
}
```

## Chains

链式写法请遵循以下规则：

- 若链过长，分多行放置，`.` 放在行首 (**除链式操作外，其他特殊字符不应出现在行首**)
- 按上下文进行缩进

示例：

```js
// good
$('img').responsive().lazyload();

$form
  .prop('novalidate', false)
  .find('[type=submit]')
    .prop('disabled', true)
    .end()
  .find('input')
    .each(function(){
      // ..
    });
```

## Quotes

使用单引号 `'`。

```js
elem.innerHTML = '<div class="sidebar"></div>';
```

## Variables

使用变量时，请遵循以下规范：

- 任何变量使用前均需 `var` 声明
- 如代码块有简单的中断逻辑（如参数数量不符合要求、error 处理），可将变量声明放置在该逻辑后
- 声明的同时有赋值的变量需独占一行，下一行变量需以第一个变量对齐，并以 `,` 结尾
- 仅有声明并没有赋值的变量放在其他变量后，可写在一行
- 避免直接在函数内调用、设置外部作用域的变量，建议使用参数传入、使用 `return`、`window.varName` 或 `export` 等形式（建议使用 [RequireJS](http://requirejs.org/docs/api.html#define)）输出到外部

```js
// bad
var globalVar;
window.onload = function(){
  globalVar = 'global var';
};

var a = 'Hello'
  , b, c;

// good
window.onload = function(){
  var arr = [],
      globalVar = 'global var',
      fn, fetchUser
  ;

  for ( var i = 0; i < 10; i++ ) {
    arr.push(i);
  }

  fn = function(){};

  window.globalVar = globalVar;
};

var fn = function (data) {
  if (!data) {
    return false;
  }

  var a = 'Hello'
    , b, c;

  return data;
};

fs.readFile(file, function (err, data) {
  if (err) {
    return handler(err);
  }

  var content = data.toString();
  // ..
})

window.globalVar = doSomething();

// better
// Promise
var promise = new Promise(function(resolve, reject){
  window.onload = function(){
    var data;
    // ..
    resolve(data);
  }
});

promise.then(function (data) {
});

// Event
window.onload = function () {
  $(window).trigger('windowDidLoad', data);
};

$(window).on('windowDidLoad', function (event, data) {
});

// Postal (Pub/Sub)
// foo.js
var sub = postal.subscribe({
  channel: "foo",
  topic: "bar",
  callback: function (data) {
    // data is response.json()
  }
});

// bar.js
fetch(uri).then(function (response) {
  postal.publish({
    channel: "foo",
    topic: "bar",
    data: response.json()
  });
})
```

## Types

- 优先使用原始类型 (primitive type)
- 需转换类型时请勿使用 `new`
- 优先使用字面量 (Literal)

```js
// bad
function (data) {
  var isValid = new Boolean(data);

  if (isValid) {} // always be true
}

var foo = new String('Hello');
var bar = new Array(1, 2);
var baz = new Object()
var qux ＝ new RegExp('\\w+');

// good
function (data) {
  var isValid = Boolean(data);

  if (isValid) {}
}

var foo = 'Hello';
var bar = [1, 2];
var foo = {};
var qux = /\w+/;
```

Note:

- 正则表达式优先使用字面量，需动态组装的才使用 `new RegExp`

在操作变量时，对变量进行类型转换：

```js
// bad
var foo = 123,
    bar = '321'
;

foo + bar; // '123321'

// good
foo + parseInt(bar, 10); // 444
```

## Numbers

请使用如下方式转换数字，可指定进制的，请勿省略进制：

- `Math.floor()` (`Math.floor(NUM) === parseInt(NUM, 10)`，但更快)
- `parseInt()`、`parseFloat`
- `Number()` (`Number(NUM) === parseFloat(NUM, 10)`，性能相当，但省去 radix 的隐患)

```js
// bad
parseInt(foo);
bar = +foo;
bar = new Number(foo);
bar = foo >> 0;

// good
parseInt(foo, 10);
bar = Number(bar);
```

由于以下原因，不推荐使用位运算：

- 因为 JavaScript 数字是 64-bit（[doc](http://es5.github.io/#x4.3.19)），位运算只会返回 32-bit（[doc](http://es5.github.io/#x11.7)）
- 虽然性能上，Firefox、IE 10 中会有明显提升（[jsPerf](http://jsperf.com/coercion-vs-casting/11)），但 `Math.floor()`、`parseInt()` 的性能已经足够
- `parseInt()` 可读性更好

## Objects

- 使用字面量
- 不要使用保留字 (可借助 `is`、`has` 等词)
- 使用可读性好的同义词
- 使用点 `.` 访问属性，当属性名为变量时使用 `[]`

```js
// bad
var foo = new Object();
foo['class'] = 'human';
foo['private'] = true;

if (foo['class']) {}

// good
var foo = {
  type: 'human',
  isPrivate: true
};

if (foo.type) {}

function getProp (prop) {
  return this[prop];
}

getProp.call(foo, 'isPrivate');
```

### Accessors

- 使用 `addVal`、`removeVal`、`getVal`、`setVal`、`hasVal`、`isVal` 等方式命名
- `hasVal` 和 `isVal` 等应代表只读并且返回 `Boolean` 值的操作。

```js
// bad
user.age();
user.age(20);
user.car(BMW);

if (user.kid()) {}

// good
user.getAge();
user.setAge(20);
user.addCar(BMW)

if (user.isKid()) {}

if (user.hasCar(carName)) {}
```

#### `Object.defineProperty()` and `Object.defineProperties()`

在兼容 EcmaScript 5 的平台中可考虑用属性：

```js
function User () {
  var age;
  Object.defineProperty(this, 'age', {
    enumerable: true,
    set: function (input) {
      if (!isNaN(input)) {
        age = Math.floor(input);
      }
    },
    get: function () {
      return age;
    }
  });
}

var john = new User();
john.age = 20;
console.log('John is', john.age, 'years old.');
```

## Arrays

- 使用字面量
- 添加、删除数组元素时，尽量使用 `push`、`pop`、`splice` 等函数
- 遍历数组时尽量使用 `forEach`、`map` 等函数（出于性能考虑，可使用 [lodash](http://lodash.com/)）
- `arr[index++] = VALUE` vs. `arr.push(VALUE)`，前者性能更好，但后者更易读并且不需要维护 `index`，若遇到性能瓶颈，再考虑使用前者

```js
// bad
var foo = new Array(1, 2);
foo[foo.length] = 3;

// not recommended
for (var i = 0, len = foo.length; i < len; i++) {
  foo[i];
}

// good
var foo = [1, 2];
foo.push(3);

// recommended
foo.forEach(function (item) {
});

_(foo).forEach(function (item) {
});
```

建议尽量使用 lodash 进行数组遍历，一般情况，性能比起原生的要快，具体见 [fast.js](https://github.com/codemix/fast.js) 的[对比数据](https://github.com/codemix/fast.js/blob/master/README.md#example-benchmark-output)：

```
Native .forEach() vs fast.forEach() (1000 items)
  ✓  Array::forEach() x 34,398 ops/sec ±0.99% (90 runs sampled)
  ✓  fast.forEach() x 93,377 ops/sec ±0.90% (87 runs sampled)
  ✓  fast.forEach() v0.0.2a x 93,894 ops/sec ±1.42% (85 runs sampled)
  ✓  fast.forEach() v0.0.1 x 98,412 ops/sec ±1.58% (91 runs sampled)
  ✓  fast.forEach() v0.0.0 x 66,422 ops/sec ±1.30% (87 runs sampled)
  ✓  underscore.forEach() x 33,300 ops/sec ±1.30% (82 runs sampled)
  ✓  lodash.forEach() x 95,146 ops/sec ±1.18% (88 runs sampled)

Native .map() vs fast.map() (1000 items)
  ✓  Array::map() x 32,971 ops/sec ±1.47% (87 runs sampled)
  ✓  fast.map() x 95,182 ops/sec ±1.51% (82 runs sampled)
  ✓  fast.map() v0.0.2a x 99,468 ops/sec ±1.32% (91 runs sampled)
  ✓  fast.map() v0.0.1 x 99,425 ops/sec ±1.66% (91 runs sampled)
  ✓  fast.map() v0.0.0 x 67,765 ops/sec ±1.60% (84 runs sampled)
  ✓  underscore.map() x 32,942 ops/sec ±1.45% (92 runs sampled)
  ✓  lodash.map() x 77,364 ops/sec ±1.42% (89 runs sampled)
```

fast.js、underscore.js 和 lodash 的关系：

- fast.js 和 lodash 类似，但提供的功能没有 lodash 丰富，因此建议优先考虑 lodash
- lodash 兼容 underscore.js 的接口，同时也更快，并且扩展了更多的功能，因此不建议使用 underscore.js

## Strings

- 使用字面量
- 连接字符串请使用 `+`
- 字符串过长可使用多个字符串字面量分行并使用 `+` 或数组 `join` 连接
- 超长静态字符串可考虑用 `function` 实现
- 优先使用 [EcmaScript 6 template strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings)

```js
// bad
var foo = new String('bar');

var longString = 'Quick fox jumps over the lazy dog. Quick fox jumps over the lazy dog. Quick fox jumps over the lazy dog.'

var longString = 'Quick fox jumps over the lazy dog. \
Quick fox jumps over the lazy dog. \
Quick fox jumps over the lazy dog.'

// good
var foo = 'bar';

var longString = 'Quick fox jumps over the lazy dog. ' +
                 'Quick fox jumps over the lazy dog. ' +
                 'Quick fox jumps over the lazy dog.';

var lists = []; // lots of '<li>'
ul.innerHTML = lists
                 .map(function (elem, index) {
                   elem += 'list #' + index;
                 })
                 .join('');

var foo = function(){/*
Quick fox jumps over the lazy dog. Quick fox jumps over the lazy dog.
Quick fox jumps over the lazy dog. Quick fox jumps over the lazy dog.
*/};
var bar = foo.toString().match(/\/\*([\s\S]+)\*\//)[1]

// ES6+ only
var fox = 'fox';
var dog = 'dog';
var foo = `Quick ${fox} jumps over the lazy ${dog}`
```

### `RegExp.exec` vs `String.match`

[Regular Expressions in JavaScript, part 2](http://james.padolsey.com/javascript/regular-expressions-in-javascript-part-2/)

```js
var s = 'test test test test',
    re = /t(e)(s)t/g;

console.log(s.match(re)); // ["test", "test", "test", "test"]

console.log(re.exec(s)); // ["test", "e", "s", index: 0, input: "test test test test"]
```

## Functions

- 使用函数表达式时可同时命名匿名函数，以便调试
- 声明同时执行的函数用 `(function(){})();`、`~function(){}();` 等方式书写
- 函数参数部分（括号部分）需以一空格和 `function`、`function_name` 和花括号分隔开；无参数的匿名函数可省略空格
- 参数若分多行，以第一个参数为基准对齐，一行一组，每组尽量保持数量一致

```js
// good
var foo = function () {};
var bar = function bar () {};

var baz = (function (x) { return x * x })(VALUE);

foo = function (argv1, argv2,
                argv3, argv4,
                argv5) {
};
```

### Arguments

在声明函数的时候，可以通过对象传递参数，一方面可以减少判断参数数量的问题，一方面利于日后扩展用。

```js
function request (data) {
  var url = '//domain.com/default_url';
  if (data.url) {
    url = encodeURIComponent(data.url);
  }
  if (data.json) {
  }
}

request({
  url: '//domain.com/users/1',
  json: {
    id: 1
  }
});

request({
  json: {
    id: 1
  }
});

$elem.trigger('updateProfile', {
  id: 1,
  name: 'John Doe'
});

$elem.on('updateProfile', function (event, profile) {
  request({
    url: '//domain.com/users/' + profile.id,
    json: profile
  });
});
```

### V8 Optimization

目前 V8 引擎无法对以下类型的 `function` 进行优化：

- Generator function
- 包含 `for..of` 的
- 包含 `try..catch` 的
- 包含 `try..finally` 的
- 包含 `let`、`const` 的
- 函数内包含 `__proto__`、`get`、`set` 声明的对象字面量

可能永不会优化的：

- 包含 `debugger` 的
- 包含 `with` 的
- 调用 `eval()` 的

`arguments`：

- 不要重新赋值给参数
- 不要把 `arguments` 传递出去
- 不要赋值给 `arguments`

```js
// bad
function foo (a, b) {
  if (somethingIsTrue()) {
    a = 1;
  }

  var args = [].slice.call(arguments);

  var bar = arguments;
  return bar; // or return arguments
}

// ok
function baz (a, b) {
  var _a = a;
  if (somethingIsTrue()) {
    _a = 1;
  }

  var args = [];
  for (var i = arguments.length; i--; ) {
    args[i] = arguments[i];
  }
  return args;
  // or
  otherFunc.apply(null, arguments);
}
```

更多请阅读 [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)。

## Scoping

- 代码块（一般以文件为单位）需包裹在一个 `function` 或 `define`（如 [RequireJS](http://requirejs.org/)）
- 变量在使用前必须先声明

```js
// foo.js
~function(){
}();

// bar.js
~function(){
}();

// define.js
define('module/name', function(){
});
```

## Eval

请勿使用 `eval()`。

## With

为了保持代码清晰，任何时候都不要使用 `with () {}`。

## Exceptions

`try..catch` 有严重性能问题（[jsPerf](http://jsperf.com/try-catch-error-perf/64)），因此：

- 不要过度依赖 `try..catch` 进行异常处理。注：ES6 promise 会将异常作为 `reject` 处理。
- 在程序中多进行类型判断、转换，避免不需要异常处理的时候抛出异常

```js
// not recommended
try {
  var foo = bar(); // bar() returns `null`
  foo.baz; // throwing TypeError
} catch (ex) {
  // ..
}

// recommended
var foo = bar();

if (foo) {
  foo.baz
} else {
  // ..
}
```

## Constructors and Prototypes

避免修改内置对象（如 `String`）的 `prototype`，只有用于扩展的 (如 polyfill) 才允许修改 `prototype`：

```js
/**
* A polyfill for EcmaScript 6 String.contains()
* @param  {Any}     str A string representing the value to search for;
*                       basicly, JS will use `toString` to convert passed argument to string
* @return {Boolean}     A boolean presenting search result
*/
if (!String.prototype.contains) {
  String.prototype.contains = function (str) {
    return this.indexOf(str) > -1;
  }
}
```

创建构造函数时，避免使用 `prototype` 的形式：

```js
// bad
function User () {}

User.prototype = {
  getName: function () {
    return this.name
  },
  setName: function (input) {
    this.name = input
  }
};

// good
function User () {}

User.prototype.getName = getter;
User.prototype.setName = setter;

// better
function User () {
  var name
  Object.defineProperty(this, 'name', {
    get: function () {
      return name;
    },
    set: function (input) {
      name = input;
    }
  });
}
```

## Namespaces

如出现依赖冲突，可使用命名空间分隔代码块，或者结合 [RequireJS](http://requirejs.org/docs/api.html) 等方式：

```js
TopNS.user.signIn = function(){};
TopNS.admin.signIn = function(){};

// Or

define('User', function(){
  return {
    signIn: function(){}
  };
});

define('Admin', function(){
  return {
    signIn: function(){}
  }
})

require(['User', 'Admin'], function (User, Admin) {
  if (adminLoginClicked) {
    Admin.signIn();
  } else {
    User.signIn();
  }
});
```

## Conditional Expressions and Comparisons

- 尽量使用 `===`、`!==`
- 尽量使用 `!` 来做 `true` / `fasle` 判断
- 多使用内置或第三方函数检查实例，如 `Array.isArray`、`_.isString`

```js
// bad
if (arr.length == 3) {}

if (isValid != true) {}

if (arr instanceof Array) {}

// good
if (arr.length === 3) {}

if (!isValid) {}

if (Array.isArray(arr)) {}
```

## Comments

对代码使用 [JSDoc](http://en.wikipedia.org/wiki/JSDoc) 风格对代码注释：

```js
/**
 * A polyfill for EcmaScript 6 String.contains()
 * @param  {Any}     str A string representing the value to search for;
 *                       basicly, JS VM will use `toString` to convert
 *                       passed argument to string
 * @return {Boolean}     A boolean presenting search result
 */
if (!String.prototype.contains) {
  String.prototype.contains = function (str) {
    return this.indexOf(str) > -1;
  }
}
```

文件头部：

```js
/**
 * 关于当前文件的描述和用途。
 * 是否有依赖项
 */
```

每个注释和代码段之间以一个空行进行分割：

```js
/**
 * 获知设备屏幕数据
 * 主要用于判断和解决 retina 屏的问题
 */
devicePixelRatio = window.devicePixelRatio || 'unknown',
screenPixelDepth = screen.pixelDepth || 'unknown',
screenColorDepth = screen.colorDepth || 'unknown',

// 判断 JS 引擎
querySelector = !!document.querySelector; // IE 7 或以下为 false
localStorage = !!window.localStorage; // IE 7 或以下为 false
arrayFilter = 'filter' in Array.prototype; // IE 8 或以下为 false
classList = 'classList' in document.getElementsByTagName('head')[0]; // IE 9 或以下为 false
// 若都支持，则说明 JS 为现代引擎

platform = navigator.platform;
```

## Tag Your Codes

使用 `#@tag` 在代码标记行为：

- `#@todo`：标记需尽快执行的事项
- `#@issue`：标记暂时可不执行的事项

```js
// #@issue auto calculate height according to its content
elem.height(200);

// #@todo should use promise instead callback
var request = function (callback) {
  $.ajax({
    success: function (data) {
      callback.success.call(this, data);
    }
  });
};
```

使用示例：

命令行 + [ag](https://github.com/ggreer/the_silver_searcher) = `ag -i -A 2 -B 2 '#@(todo|issue)'`：

```
JavaScript_Style_Guide.md
839-使用 `#@tag` 在代码标记行为：
840-
841:- `#@todo`：标记需尽快执行的事项
842:- `#@issue`：标记暂时可不执行的事项
843-
844-示例：
845-
846:    // #@issue auto calculate height according to its content
847-    elem.height(200);
848-
849:    // #@todo should use promise instead callback
850-    var request = function (callback) {
851-      $.ajax({
```

## DOM

活用 `cloneNode`、`innerHTML` 和 `DocumentFragment`（jsPerf: [1](http://jsperf.com/appendchild-documentfragment-innerhtml/4), [2](http://jsperf.com/clonenode-in-nodes-iteration/2)）：

```js
var nav = document.querySelect('nav'),
    clonedNode = nav.cloneNode(true),
    newItems = clonedNode.querySelectorAll('.item'),
    length = newItems.length,
    parent = nav.parentElement
;

while (length--) {
  newItems[length]; // do something...
}

parent.replaceChild(clonedNode, nav);
```

使用 `[].forEach.call` 等方式遍历元素数组：

```js
$('nav a').each(callback);

[].forEach.call(document.querySelectorAll('nav a'), callback);
```

事件命名建议使用可读性更高的句子：

```js
$profile
  .on('profileDidUpdate', callback)
  .on('profileDidUpdateFailed', callback);
```

利用 DOM 内置的行为，而不是强制抹去内置行为：

```js
// bad
<form>
  <input type="button" value="提交">
</form>

$('form').on('submit', function(){
  return false;
});

$('input').on('click', function(){
  $('form').submit();
});

// good
<form>
  <input type="submit" value="提交">
</form>

$('form').on('submit', function(){
  var $form = $(this);

  // ..

  return false;
});

// bad
<form novalidate>
  <input type="text" data-pattern="\S{3,20}" data-required>
</form>

// good
<form>
  <input type="text" pattern="\S{3,20}" required>
</form>

$('form').each(function(){
  this.setAttribute('novalidate', 'true');
});

$('input').on('input', function(){
  if (new RegExp(this.getAttribute('pattern')).test(this.value)) {}
});
```

对输入进行 `trim` 处理：

```js
// bad
var name = $('name').val();

// good
var name = $.trim($('name').val());
```

## jQuery

在变量名前添加 `$`：

```js
var $form = $(this),
    _$select = $form.find('select');
```

缓存元素或使用 `chains`：

```js
// bad
$('button').on('click', callback);
$('button').prop('disabled', false);

// good
$('button')
  .on('click', callback)
  .prop('disabled', false);

$form = $('form');

$.ajax().then(function(){
  $form;
});
```

使用高级 [CSS selector](http://api.jquery.com/category/selectors/)：

```js
// bad
$('div').first();

$('input').each(function(){
  if ($(this).css('display') !== 'none') {}
});

// good
$('div:first');

$('input:not(:hidden)').each(function(){});
```

合理选择 context 和 `find`：

```js
// bad
$('nav').find('a');
$('a', 'nav');
$('a', $nav);

// good
$('nav a');
$('nav > a');
$('a', document.getElementById('nav'));
$('a', $nav[0]);
$nav.find('a');
```

使用 `on`：

```js
$('button').live('click', callback); // deprecated by jQuery team
$('button').click(callback);

$(document).on('click', 'button', callback);
$('button').on('click', callback);
```

当需要判断元素是否存在才执行后续操作时，可使用 `each`：

```js
$('body').each(function(){
  $body = $(this);
});

// Equals to, but less code

var $body = $('body')
if ($body.length) {
  // ..
}
```

使用可读的变量名，避免使用 `$this`：

```js
// bad
$('body').each(function(){
  $this = $(this);
});

// good
$('body').each(function(){
  $body = $(this);
});
```

使用 `length` 而不是 `size()`（[jsPerf](http://jsperf.com/size-vs-length/5)）。

## ECMAScript Compatibility

- 兼容性列表：[ES5](http://kangax.github.io/es5-compat-table/), [ES6](http://kangax.github.io/es5-compat-table/es6/)
- [Polyfill.io](http://polyfill.io/) - 可针对各种浏览器添加垫片
- [ES5 Polyfill](https://github.com/es-shims/es5-shim)
- [ES6 Promise](https://github.com/jakearchibald/ES6-Promises), Node.js 端请使用 [bluebird](https://github.com/petkaantonov/bluebird)

## Meta

- 在每个文件的末尾添加一行空行
- 请删除行尾多余的空格
