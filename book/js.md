#### 数组去重 的108种方法

1. **Array.filter\(\) + indexOf  效率低**

```js
function distinct(a, b) {
//合并两个数组
    let arr = a.concat(b);
    //遍历数组 indexof排除
    return arr.filter((item, index)=> {
        return arr.indexOf(item) === index
    })
}
```

2.双重**for**循环  占内存

3.**for..of** + **includes\(\)**

4.**Array.sort\(\) 排序 比较相邻元素是否相等 快**

5.**new Set\(\)  超级快**

```js
function distinct(a, b) {
    return Array.from(new Set([...a, ...b]))
}
```

6.**for..of + Object 对象属性不会重复 比set还快**

```js
function distinct(a, b) {
    let arr = a.concat(b)
    let result = []
    let obj = {}

    for (let i of arr) {
        if (!obj[i]) {
            result.push(i)
            obj[i] = 1
        }
    }

    return result
}
```



