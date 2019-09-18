#### 箭头函数

* 没有this this不可更改 
* 没有\[\[Construct\]\]方法 所以不能new 自然也没有原型
* 没有arguments对象
* 不允许重复的具名参数

```js
var reflect = (value, sum)=> value + sum;
//等价于
var reflect = function(value, sum){
    return value + sum;
}
```



