# research-ast (抽象语法树)

## 引用

- [平庸前端码农之蜕变 — AST](https://juejin.cn/post/6844903725228621832)
- [AST for JavaScript developers](https://itnext.io/ast-for-javascript-developers-3e79aeb08343)
- [WRITE A BABEL PLUGIN](https://stephencook.dev/blog/writing-a-babel-plugin-with-grandma/)

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

1. 解析（parsing) - 创建了AST
2. 转译（transforming）- 遍历树，修改tokens 
3. 生成（generation）- 从AST中生成新的代码


## 好用的代码重构工具库
* ts-morph
* [jscodeshift](https://github.com/whxaxes/blog/issues/10)

