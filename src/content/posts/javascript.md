---
title: JavaScript 简记
published: 2024-06-10
image: ""
tags: [JavaScript]
category: "前端"
draft: false
---

# JavaScript 简记

Javascript 发展到现在有很多年了，而我作为一个开发者也使用了很久，但是有些特性还是不是很明白，故写下这篇笔记，以便于自己复习。

## 现代的标记 markup

`type` 特性: `<script type=...>`

## 外部脚本

```javascript
<script src="..."></script>
```

## 基本类型

`String` `Number` `Object` `Boolean` `null` `undefined` `bigint` `symbol`
symbol:唯一标识符
undefined: 含义是未被赋值
null: 含义就是空

### Bigint

在后面加上 n 表示为任意长度的**整数**

```javascript
let num = 12344521312543512323432n;
```

### typeof

```javascript
typeof undefined; // "undefined"
typeof 0; // "number"
typeof 10n; // "bigint"
typeof true; // "boolean"
typeof "foo"; // "string"
typeof Symbol("id"); // "symbol"
typeof Math; // "object" (1)
typeof null; // "object" (2)
typeof alert; // "function" (3)
```

最后三行可能需要额外的说明：

1.  `Math`  是一个提供数学运算的内建  `object`。我们会在  [数字类型](https://zh.javascript.info/number)  一节中学习它。此处仅作为一个  `object`  的示例。
2.  `typeof null`  的结果为  `"object"`。这是官方承认的  `typeof`  的错误，这个问题来自于 JavaScript 语言的早期阶段，并为了兼容性而保留了下来。`null`  绝对不是一个  `object`。`null`  有自己的类型，它是一个特殊值。`typeof`  的行为在这里是错误的。
3.  `typeof alert`  的结果是  `"function"`，因为  `alert`  在 JavaScript 语言中是一个函数。我们会在下一章学习函数，那时我们会了解到，在 JavaScript 语言中没有一个特别的 “function” 类型。函数隶属于  `object`  类型。但是  `typeof`  会对函数区分对待，并返回  `"function"`。这也是来自于 JavaScript 语言早期的问题。从技术上讲，这种行为是不正确的，但在实际编程中却非常方便。

## 交互

alert: 弹窗提示

```javascript
let a = prompt(title,[default]);
```

prompt: 两个参数 标题，输入框默认值，确认后输入框值赋值给 a

```javascript
let b = confirm("are you ready?");
alert(b);
```

confirm(question); 返回布尔值，确定 true，取消 false

以上窗口样式都不能改变，样式取决于浏览器

## 类型转换

```javascript
let a = 123;
String(a); // "123"

let b = "123";
Number(b);
Number(true); // 1
Number(false); // 0
Number("123z"); // NaN
Number(null); // 0
Number(undefined); // NaN

Boolean(1); // true
Boolean(0); // false
Boolean("hello"); // true
Boolean(""); // false
Boolean("0"); // true
Boolean(" "); //true
```

布尔型转换
|值 |变成 |
|--|--|
| `0`,`null`,`undefined`,`NaN`,`""` | `false` |
|其他值|`true`|

## 基本运算符

`2 ** 3` 2^3

## 相等

`==`：相等性检查 会进行类型转换 `!=` 同理
`===`：严格相等性检查 不会进行类型转换 `!==` 同理

## while-for

### while

`break` 跳出循环
`continue` 跳出当此循环

### for

标签

```javascript
fors: for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break fors;
  }
}
alert("Done!");
```

标签不允许跳到代码任意位置，break 只允许在代码块内。

## 对象 Object

简单来说就是键值对，但是值可以为任何值

```javascript
let user = new Object(); // 构造函数语法
let user = {}; // "字面量"语法
```

delete 移除对象属性

```javascript
let user = {
  name: "Jone",
};
delete user.name; // 移除属性
```

也可以用多字多词作为属性名

```javascript
let user = {
  "like more": true,
};

alert(user["like more"]);
delete user["like more"];
```

## 逻辑运算符

```javascript
// 或
alert(true || true); // true
alert(false || true); // true
alert(false || false); // false
// 与
alert(true && true); // true
alert(false && true); // false
alert(true && false); // false
alert(false && false); // false
// 非
alert(!true); // false
alert(!0); // true
// 会将某个值转成布尔
alert(!!"non-empty string"); // true
alert(!!null); // false
alert(Boolean("non-empty string")); // true
alert(Boolean(null)); // false

// 空值合并运算符 ??
// 如果第一个值为null/undefined则显示第二个值，否则则是第一个值
let user;
alert(user ?? "匿名"); // 匿名（user 未定义）
```

## 箭头函数

箭头函数没有 this 指向，箭头函数内部 this 值只能通过查找作用域链来确定，一旦使用箭头函数，当前就不存在作用域链。

使用箭头函数 内部没有 arguments 且箭头函数不能使用 new 来实例化对象 而 function 函数是一个对象，箭头函数不是对象

## 对象扩展

```javascript
const name = "xiao",
  age = 20;
const person = {
  name,
  age,
  sayName: function () {
    console.log(this.name);
  },
};
```

赋值不需要使用 : 直接写变量名就 OK

## Object

`Object.is()` 对比
`Object.assign()` 浅拷贝

## Symbol

原始数据类型，表示独一无二的值

## Set

无重复值的有序列表

```javascript
let set = new Set();
set.add(); // 添加元素
set.delete(); // 删除元素
set.clear(); // 清除
console.log(set.size); // 大小
console.log(set.has("4"));
```

## 扩展运算符

```javascript
console.log([...arr]);
```

## Array

```javascript
// from 将伪数组转成数组
Array.from(new Set(1, 2, 4));

// of 将任意数组类型转成数组
Array.of(1, 3, 4, 5, { id: 1 }, [1, 2, 3]);

// copyWithin() 复制后三个数值 替换从下标0开始的3个数值
[1, 2, 3, 4, 5].copyWithin(0, 3);

// find() 返回符合条件的数值 findIndex() 返回符合条件的数值的下标
[1, 2, 7, 9]
  .find((n) => n < 2) // 1
  [(1, 2, 7, 9)].findIndex((n) => n > 7); // 3

// entries() index,ele 键值对遍历器

// keys() values() 返回一个数组的遍历器
let arr = new Array(1, 3, 4, 5);
// key()
for (const key of arr.keys()) {
  console.log(key);
}
// value()
for (const value of arr.values()) {
  console.log(value);
}
// entries()
for (const [i, k] of arr.entries()) {
  console.log(i);
  console.log(k);
}
console.log(arr.entries().next().value); // [0,1]
// includes() 返回一个boolean，表示某个数组是否包含给定的值
console.log(arr.includes(1)); // true
```

## Iterator 迭代器

一种新的遍历机制，有两个核心

- 迭代器是一个接口，能快捷的访问数据，通过 Symbol.iterator 来创建迭代器 通过迭代器的 next()方法获取迭代后的结果
- 迭代器是用于遍历数据结构的指针(数据库的游标)

```javascript
const items = ["one", "two", "three"];
const ite = itmes[Symbol.iterator]();
console.log(ite.next()); // {value: 'one', done: false} done如果为false表示遍历继续 如果为true遍历结束
```

## Generator 生成器

通过 yield 关键字，将函数挂起，为了改变执行流提供了空间，同时也为异步编程提供了可能

- function 后面，函数名之前有个\*
- 只能在函数内部使用 yield 表达式，让函数挂起
  目前来看使用场景有异步编程，为不具备 Iterator 接口的对象提供了遍历操作

```javascript
function* func(a) {
  console.log("one");
  yield 2;
  console.log("two");
  yield 3;
  console.log("end");
}
let fn = func(); // 有个next()函数
console.log(fn.next());
console.log(fn.next());
console.log(fn.next());
```

`yield` 像断点 而 `next()`则是执行恢复运行

### 传值

```javascript
function* add() {
  console.log("start");
  let x = yield "2";
  console.log("one" + x);
  let y = yield "3";
  console.log("two" + y);
  return x + y;
}
const fn = add();
console.log(fn.next()); // 第一个不会传值
console.log(fn.next(10)); // x = 10
console.log(fn.next(20)); // y = 20,sum = 30
```

## Promise

Promise 有三个状态：

- pending(进行)
- resolved(成功)
- rejected(失败)

```javascript
let pro = new Promise(function (resolve, reject) {
  let response = {
    code: 400,
    msg: "success",
    error: "faild",
  };
  setTimeout(() => {
    if (response.code === 200) {
      resolve(response);
    } else {
      reject(response);
    }
  }, 1000);
});

pro.then(
  (res) => {
    console.log(res);
  },
  (err) => {
    console.log(err);
  }
);
```

## async 异步

async 使异步操作更加方便
async 会返回一个 Promise 对象 then catch
其实是 Generator 的语法糖

```javascript

```
