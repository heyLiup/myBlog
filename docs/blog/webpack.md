# webpack

1. noParse

```js

RegExp | [RegExp]

RegExp | [RegExp] | function（从 webpack 3.0.0 开始）

防止 webpack 解析那些任何与给定正则表达式相匹配的文件。忽略的文件中不应该含有 import, require, define 的调用，或任何其他导入机制。忽略大型的 library 可以提高构建性能。

noParse: /jquery|lodash/

// 从 webpack 3.0.0 开始
noParse: function(content) {
  return /jquery|lodash/.test(content);
}

```

2. webpack打包

```js
//1. local 
npm scripts
./package.json
'scripts': {
    'bundle':'webpack'
}
npm run bundle

// 2.
npx webpack <入口文件>

// 3.global
webpack <入口文件>

```

3. webpack-cli
> 作用：在命令行里可以使用webpack相关的命令

4. babel-loader
babel-loader是webpack和babel之间通信的桥梁
@babel/core 是babel核心方法库
@babel/preset-env