# research-ast (抽象语法树)

## 引用

- [平庸前端码农之蜕变 — AST](https://juejin.cn/post/6844903725228621832)
- [AST for JavaScript developers](https://itnext.io/ast-for-javascript-developers-3e79aeb08343)
- [WRITE A BABEL PLUGIN](https://stephencook.dev/blog/writing-a-babel-plugin-with-grandma/)
- [腾讯好文, 面向开发学习](http://www.alloyteam.com/2017/04/analysis-of-babel-babel-overview/)
- [ast-api](http://www.alloyteam.com/wp-content/uploads/2017/04/1491466252_26_w899_h884.png)

## 词法分析和语法分析

### 词法分析(scanner)

按照预定的规则合并成一个个的标识 tokens

```js
// 源码
const a = 1;

// 转义为:
[
  {
    value: "const",
    type: "keyword",
  },
  {
    value: "a",
    type: "identifier",
  },
];
```

当词法分析源代码的时候，它会**一个一个字母**地读取代码，所以很形象地称之为扫描；
当它遇到空格，操作符，或者特殊符号的时候，它会认为一个已经完成了。

### 语法分析(解析器)

1.  将词法分析出来的数组转化成树形的表达形式
2.  语法验证, 有错抛出错误

```js
// 将词法分析获得数组转义为:
{
  "type": "VariableDeclarator",
  "start": 6,
  "end": 11,
  "id": {
    "type": "Identifier",
    "start": 6,
    "end": 7,
    "name": "a"
  },
  "init": {
    "type": "Literal",
    "start": 10,
    "end": 11,
    "value": 1,
    "raw": "1"
  }
}
```


## babel-plugin

1. 解析（parsing) - 创建了AST - babylon
2. 转译（transforming）- 遍历树，修改tokens - babel-traverse
3. 生成（generation）- 从AST中生成新的代码 - babel-generator

### 开发会用到的小..
* 工具库 babel-types，用于构建、验证、变换节点
* 参数path
  * node节点
  * parent节点
  * path.node.x 返回value值
  * path.get(x)返回子节点path
* 树形遍历（enter+exit）+ 访问者模式（visitor）



![ast-api-tree](http://www.alloyteam.com/wp-content/uploads/2017/04/1491466252_26_w899_h884.png)


### babelrc - Plugin与Preset执行顺序
* 先执行完所有Plugin，再执行Preset。
* 多个Plugin，按照声明次序顺序执行。
* 多个Preset，按照声明次序逆序执行。
  - preset: [‘es2015’, ‘react’], 其实是先使用react插件再用es2015


## 好用的代码重构工具库
* ts-morph
* [jscodeshift](https://github.com/whxaxes/blog/issues/10)


