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

1. 属性可读可写 则在obj上添加属性 屏蔽掉原型链上的属性 “属性屏蔽”
2. 只读 writable：flase 则无法修改也无法创建
3. 属性是setter 则调用此setter

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

