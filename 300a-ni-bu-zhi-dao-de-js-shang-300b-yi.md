## 1

#### 作用链

LHS 和 RHS 查询都会在当前执行作用域中开始，如果有需要\(也就是说它们没有找到所 需的标识符\)，就会向上级作用域继续查找目标标识符，这样每次上升一级作用域\(一层 楼\)，最后抵达全局作用域\(顶层\)，无论找到或没找到都将停止。

#### 块级作用域

let 块级作用域 函数为作用域单元 内部变量隐藏

#### 变量提升

变量提升 var function（优先） let不进行提升

#### 闭包

闭包当函数可以记住并访问所在的词法作用域，即使函数是在当前词法作用域之外执行，这时 就产生了闭包。

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



