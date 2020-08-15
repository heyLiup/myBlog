
## javaScript整数安全范围

**Number是双精度浮点数,它可以表示的最大安全范围是正负9007199254740991**
```js
//也就是2的53次方减一 
2 ** 53 -1
Math.pow(2, 53) - 1

//在浏览器控制台分别输入Number.MAX_SAFE_INTEGER和Number.MIN_SAFE_INTEGER可查看对应的最大/小值

//最大/小值 加/减 1可以正确运算，但是再次加/减 1， 结果却相同，表现为丢失精度
2 ** 53 -1 + 1       //9007199254740992
2 ** 53 -1 + 1 + 1   //9007199254740992

```

**BigInt**

BigInt是JavaScript中的一个新的原始类型，可以用任意精度表示整数。使用BigInt，即使超出JavaScript Number 的安全整数限制，也可以安全地存储和操作大整数。

chrome 67+开始支持BigInt，IE11及以下不支持

- 创建BigInt 
```js
number后直接加n  // 123n
BigInt(number)  // 123n   number需要为整数，不能带有小数

123n === BigInt(123)  //true

```

- 运算
```js
9007199254740991n + 3n    //9007199254740994n
Number(9007199254740994n)  //9007199254740994


```

- 因为BigInts是一个单独的类型，所以a BigInt永远不会等于a Number，例如 42n !== 42。


[参考链接1](https://www.cnblogs.com/wangmeijian/p/9217352.html)
[参考链接2](https://segmentfault.com/a/1190000019912017?utm_source=tag-newest)