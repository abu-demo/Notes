## 1

#### 作用链

LHS 和 RHS 查询都会在当前执行作用域中开始，如果有需要\(也就是说它们没有找到所 需的标识符\)，就会向上级作用域继续查找目标标识符，这样每次上升一级作用域\(一层 楼\)，最后抵达全局作用域\(顶层\)，无论找到或没找到都将停止。

#### 块级作用域

let 块级作用域 函数为作用域单元 内部变量隐藏

#### 变量提升

变量提升 var function（优先） let不进行提升

#### 闭包

闭包当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，这时 就产生了闭包。

```js
//函数工厂
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

```js
//api 数据隐藏和封装
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  //返回api方法
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var Counter1 = makeCounter(); //用变量存储api方法
var Counter2 = makeCounter();
console.log(Counter1.value()); /* logs 0 */
Counter1.increment(); //调用
Counter1.increment();
console.log(Counter1.value()); /* logs 2 */
Counter1.decrement();
console.log(Counter1.value()); /* logs 1 */
console.log(Counter2.value()); /* logs 0 */
```

#### 模块化开发

模块有两个主要特征:

1. 为创建内部作用域而调用了一个包装函数;
2. 包装函数的返回 值必须至少包括一个对内部函数的引用，这样就会创建涵盖整个包装函数内部作用域的闭包。

## 2

#### this

1）默认全局变量 函数独立调用的时候

2）隐式绑定 上下文对象 看对象属性引用链 容易出现this指向丢失的问题

3）显示绑定 call\(\) apply\(\) 如果参数是null 无影响 如果是原始值转换成它的对象形式 “装箱”

“硬绑定” ES5内置对象 function.prototype.bind\(\) 返回硬编码的新函数

4）new 绑定

在 JavaScript 中，构造函数只是一些 使用 new 操作符时被调用的函数。

* 创建\(或者说构造\)一个全新的对象。  
* 这个新对象会被执行\[\[原型\]\]连接。  
* 这个新对象会绑定到函数调用的this。  
* 如果函数没有返回其他对象，那么new表达式中的函数调用会自动返回这个新对象。

5）this绑定优先级

new -&gt; call、apply -&gt; 上下文调用 -&gt;默认指向

6）绑定例外

* 显示绑定 参数为null

* 绑定丢失

* 软绑定 为默认的this指向进行设置

7）箭头函数 根据外层\(函数或者全局\)作用域来决定 this指向 且无法更改

## 3

#### 对象

js基本类型 string boolean number null undefined object

内置对象 String Number Boolean Object Function Array Date Regexp Error

.name属性访问 要求name满足标识符命名规范

\["name"\] 键访问 可以接受人意UTF-8/Unicode字符串

属性名永远是字符串 非字符串会转化为字符串

ES6 新增 可计算属性名 \[\]包裹表达式

复制对象

* 浅拷贝ES6 Obect.assign\(\) 不会复制属性描述

* 深拷贝var newObj = JSON.parse\( JSON.stringify\( someObj \) \); 要求JSON安全

属性描述符

* writable（可写） - enumerable（可枚举） - configurable （可配置）

* Object.defineProperty\(\)添加或者修改属性

属性不可变性

* wirtable:false configurable:false

* Object.preventExtensions\(\) 不可扩展 - Object.seal\(\) 密封 - Object.freeze\(\) 冻结

查看对象属性

* hasOwnProperty\(\) 属性是否存在于对象中

* in 属性是否存在于对象和原型链中 要求可枚举属性

* Object.keys 返回对象中可枚举属性数组

* Object.getOwnPrepoertyNames\(\)返回对象中包含所有可枚举以及不可枚举的属性数组

遍历属性值

* for 循环

* ES5辅助迭代器 -forEach\(\) 忽略返回值 - every\(\) 返回false终止 - some\(\) 返回true终止

* ES6 for..of next\(\) 方法返回形式 {value: .. , done: ..}的值

## 4

#### 类

ES6 class 类是一种设计模式

构造函数 类实例有一个特殊的类方法构造 方法名与类名相同

继承 本质是复制

多态 在继承链的不同层次中一个方法名可以被多次定义，当调用方法时会自动选择合适的定义。

super  静态绑定

js中对象是关联关系 所以为了模拟复制行为 “混入” 显示（手动复制）和隐式（this重绑定）

```js
"use strict";

class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

class Square extends Polygon {
  constructor(sideLength) {
    super(sideLength, sideLength);
  }
  get area() {
    return this.height * this.width;
  }
  set sideLength(newLength) {
    this.height = newLength;
    this.width = newLength;
  }
}

var square = new Square(2); square = new Square(2);
```

## 5

#### 原型

[https://blog.csdn.net/u012468376/article/details/53121081](https://blog.csdn.net/u012468376/article/details/53121081)

> 声明一个函数，则这个函数默认会有一个属性叫 prototype 。而且浏览器会自动按照一定的规则 创建一个对象，这个对象就是这个函数的原型对象，prototype属性指向这个原型对象。这个原型对象 有一个属性叫constructor 执行了这个函数

**属性设置和屏蔽**

myObject.foo = "bar"

* 如果对象属性中包含 则修改已有属性
* 对象中不存在 则访问原型链中 不存在 则在obj对象上添加相应属性 存在还存在三种可能

* 属性可读可写 则在obj上添加属性 屏蔽掉原型链上的属性 “属性屏蔽”

* 只读 writable：flase 则无法修改也无法创建

* 属性是setter 则调用此setter

**原型查找**

`hasOwnProperty`是 JavaScript 中唯一一个处理属性并且不会遍历原型链的方法 另一个`Object.Keys()`

**原型继承**

[继承中的原型链理解 ](https://blog.csdn.net/u012468376/article/details/53127929)

Object.create\(..\) 创建一个新对象带有\__protype_\_属性  关联指定函数的原型对象 并用构造方法初始化属性

* = 直接赋值 并不会关联上去 而是直接引用 更改引用方会影响被引用方

* 使用new 确实会关联 但如果函数有一些副作用会影响其后代 后果很严重

缺点：创建新对象抛弃旧对象 不能修改已有的默认对象

ES6 添加辅助函数 Object.setPrototypeOf\(..\) 修改原型关联

Object.setPrototypeOf\( Bar.prototype, Foo.prototype \);

## 6

#### 行为委托

基于原型链 区别于类的另一种设计模式



