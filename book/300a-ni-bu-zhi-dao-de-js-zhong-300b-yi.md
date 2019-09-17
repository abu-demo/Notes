## 1

#### 类型 七种

string    boolean    number    null（假值）    undefined    object（function）    symbol

typeof    string    boolean    uumber    "object"    undefined    object（function）    symbol

typeof返回字符串

未声明是undeclared

声明未赋值是undefined

## 2

#### 数组

可以存放任何类型 不需要预设大小  delete可以删除单元值 但并不影响数组长度

类数组 转化为数组 slice\(\)  Array.from\(\)

字符串 获取字符 chatAt（）

字符串不可变是不会改变原始值 而是创建返回新数组  而数组成员则是在其原始值上操作

借用数组

Array.prototype.join.call\(a, "-"\);

Array.prototype.map.call\(a, function\(\){

return v.toUpperCase\(\) + ".";

\)}.join\(""\);

字符串反转 var c= a.split\(""\).reserve\(\).join\(""\);

#### 数字

prototype.tofixed\(\) 指定小数点后显示位数 四舍五入

prototype.toPrecision\(\) 有效数位显示位数

注意：“.”是有效数字运算符 所以 42.tofixed\(\)不成立 要42..tofixed\(\)才可得42

Number.EPSILON误差范围 机器精度

整数检测 Number.isInteger\(..\)方法

特殊

null 空 undefined 未定义 NaN 非自反 isNaN 检查

无穷数 -Infinity

特殊等式 Object.is\(..\)判断两值是否绝对相等 == ===效率更高

值和引用 简单值 6个基本类型

复合值 对象 函数 引用赋值

## 3

#### 原生函数

String\(\) Number\(\) Boolean\(\) Array\(\) Object\(\) Function\(\) RegExp\(\) Date\(\) Error\(\) Symbol\(\)  所有typeof返回值均为object

new创建的是基本封装对象

内部属性class 无法直接访问 可以通过 Object.prototype.toString.call\(\[1,2,3\]\); \|\| "\[object.Array\]"

封装对象包装 js自动为其封装

拆封 1）valueOf\(\) 函数 2）使用到的地方会隐形拆封

原生函数作为构造函数

* Array Object Function 不建议

* RegExp\(\) 动态创建正则可使用 （常用）

* Date\(\) 只能new 参数为事件 默认为当前unix时间戳 Date.now\(\)

* Error\(\)

* Symbol\(\) 符号 唯一性 不加new

原生原型 function是空函数 RegExp\(\)是空正则 Array是空数组可修改

## 4

#### 强制类型转换

显示 隐式（强制）

ToString JSON.stringify\(\);  字符串化

toJSON\(\)要JSON安全 不安全的JSON undefined function symbol 包含循环引用的对象（会自动忽略）

ToNumber true- 1 false- 0 undefined- NaN  null- 0  对以0开头的十六进制数按照十进制处理！

ToBoolean

假值 undefined null false +0 -0 NaN "" 强制转换结果为false

假值对象 自己创建的外来值

真值 假值列表以外的值

**显示类型转换**

字符串和数字之间的转换 通过String\(\) Number\(\)两个内建函数来实现 还可以通过toString\(\) +号 ～字位操作“非”

parseInt\(\) 第一个参数接收字符串 第二个参数接收进制数

剩下的 一些特例和一些奇怪的字符识别的特例 就不写了 记不住的

**隐式转换**

字符串和数字 “+” 如果有一方是字符串则进行拼接操作 如果是数字则进行相加操作

\|\| &&操作数选择器择一返回 “短路”操作

宽松相等 == （允许强制类型转换） 严格相等 === （不允许强制类型转换）

NaN != NaN 唯一的自反 +0 = -0 对象指向同一个值视为相等

数字==字符串 字符串ToNumber\(\)转换成数字

其他类型和布尔类型 总是布尔转换成数字 true - 1 false - 0

null == undefined 结果为true 视为同一个东西

对象和非对象 总是ToPrimitive\(\) 调用valueOf\(\) 再调用toString\(\)

避免出错 true flase \[\] "" 0 尽量不用==

