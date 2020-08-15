## sort方法

- 默认情况下（不传入compareFunction）
```js

//sort会先比较第一位的 `Unicode code points` 排序的，如相同，则会依次比较下一位

var array = [3, 7, 2, 8, 2, 782, 7, 29, 1, 3, 0, 34]
array.sort()
// => [0, 1, 2, 2, 29, 3, 3, 34, 7, 7, 782, 8]

```

- 传入compareFunction
```
var arr = [1, 2, 3, 4, 5]

arr.sort((a, b) => {

   // 第一次执行
   // a = arr[1] = 2
   // b = arr[0] = 1
   return a - b;   //如a - b >= 0 则a 和 b 不交换，反之交换 （在chorme71版本测试下）
})

//返回排序后的数组。请注意，数组已原地排序，并且不进行复制

```

- 让某些特定数字排在第一位

```
var arr = [1, 2, 3, 4, 5]

arr.sort((a, b) => {
   return a === 3 ? -1 : 0;  
})

//[3, 1, 2, 4, 5]

```

