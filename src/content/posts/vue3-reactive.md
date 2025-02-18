---
title: Vue3 Reactive
published: 2024-09-09
image: ""
tags: [Vue3]
category: "前端"
draft: false
---

## Reactive

下面是 reactive 的基本用法

```jsx
let form = reactive({
  name: "123",
});

form.name = "321";
```

reactive 不能直接赋值，会导致破坏响应式对象，因为 reactive 是 proxy 代理对象
数组可以使用 push + 解构来赋值

```jsx
let list = reactive<string[]>([])

list = ['123'] // X
list.push(...['123']) // √
```

或者可以像这样也可以赋值

```jsx
let list = reactive<{arr: string[]}>({arr: []})
list.arr = ['123']
```

当然还有这种

```jsx
let list = reactive<{arr: string[]}>({arr: []})
Object.assign(list,{arr: ['123']})
```

那么它跟 ref 的区别是什么呢

1. ref 支持所有类型，而 reactive 只支持引用类型如：Array，Object，Map，Set
2. ref 取值赋值需要.value，而 reactive 不需要

## readonly

只读的意思，这样对象就只读了

```jsx
import { readonly } from "vue";

const obj = reactive({ name: "123" });
const read = readonly(obj);

const change = () => {
  read.name = "321";
  console.log(obj, read);
};
```

## shallowReactive

浅层次的 Reactive，当然也和 ref 和 shallowRef 一样，只要页面上有 reactive 被更改，页面也会重新渲染，导致 shallowReactive 深层次的更改在页面上更新

```jsx
import { shallowReactive } from "vue";

const shallow = shallowReactive({
  name: {
    age: 12,
  },
});

const change = () => {
  shallow.name.age = 17; // 不会触发更新
  shallow.name = { age: 18 }; //会触发更新
};
```

## Reactive 源码解析

还没想好怎么写

<strike>reactive 中如果传入基本类型会被抛出，并返回错误信息</strike>

```jsx
    if(!isObject(target)) {
        ...
    }
```
