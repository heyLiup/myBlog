## toString

- 鉴别类型

```js
toString.call([1,2])   //"[object Array]"
toString.call(123n)    //"[object BigInt]"
```

- 进制转换
```js
//默认模式
123..toString()       //"123"

//基模式
123..toString(2)       //"1111011"
(123).toString(8)      //"173"
(123).toString(16)     //"7b"

//将字符串转化为指定进制
//parseInt(string, radix)   
//将一个字符串 string 转换为 radix 进制的整数， radix 为介于2-36之间的数
parseInt('7b', 16)     //123
parseInt('173', 8)     //123

//parseFloat  
parseFloat('1.2.3')    // 1.2  第二个小数点的出现也会使解析停止
parseFloat('173', 8)   // 173  只接受单个参数

//如果参数字符串的第一个字符不能被解析成为数字,则 parseFloat 返回 NaN。
parseFloat('b12b')     //NaN   
```

