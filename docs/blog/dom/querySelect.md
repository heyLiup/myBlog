
## querySelectorAll 和 getElement

- querySelectorAll
```js

1.接受一个参数，css选择符。
// CSS 选择器中的元素名，类和 ID 均不能以数字为开头

2.querySelector返回符合条件的第一个dom元素

```

- 所属标准不同  

1. querySelectorAll 属于 W3C 中的 Selectors API 规范 [1]
2. getElementsBy 系列则属于 W3C 的 DOM 规范 [2]

- 返回值不同

1. querySelectorAll 返回的是一个 Static Node List， 
2. getElementsBy 系列的返回的是一个 Live Node List (会自动更新)

```js
document.querySelectorAll('.sidebar-link')       // [NodeList]
document.getElementsByClassName('sidebar-link')  // HTMLCollection


// Demo 1  （正常）
var ul = document.querySelectorAll('ul')[0],
    lis = ul.querySelectorAll("li");
for(var i = 0; i < lis.length ; i++){
    ul.appendChild(document.createElement("li"));
}

// Demo 2  （无限循环）
var ul = document.getElementsByTagName('ul')[0], 
    lis = ul.getElementsByTagName("li"); 
for(var i = 0; i < lis.length ; i++){
    ul.appendChild(document.createElement("li")); 
}

因为 Demo 2 中的 lis 是一个动态的 Node List， 每一次调用 lis 都会重新对文档进行查询，导致无限循环的问题。 
而 Demo 1 中的 lis 是一个静态的 Node List，是一个 li 集合的快照，对文档的任何操作都不会对其产生影响。


```


[参考链接](https://www.zhihu.com/question/24702250)