---
title: Vue3 Ref
published: 2024-09-08
image: ""
tags: [Vue3]
category: "前端"
draft: false
---

# Vue3 之 Ref 全家桶

Vue3 引入了新的 Ref API，这是一个非常重要的新特性。在 Vue3 中，`ref` 是一个函数，用于创建一个可响应的引用。`ref` 返回的对象具有一个名为 `value` 的属性，可以用来获取或设置其值。

在 Vue3 组件中，你可以使用 `ref` 创建一个响应式的数据源。例如：

```jsx
import { ref } from "vue";

export default {
  setup() {
    const count = ref(0);

    function increment() {
      count.value++;
    }

    return {
      count,
      increment,
    };
  },
};
```

在这个例子中，`count` 是一个响应式的值，每当 `increment` 函数被调用时，`count` 的值就会增加。

总的来说，Vue3 的 `ref` API 为我们提供了一个更灵活、直观的方式来管理和响应数据的变化。

> 以上为 AI 输出内容

## shallowRef

shallowRef 为浅层的响应

以下为代码示例

```jsx
<script setup>
import {shallowRef} from "vue";

const value = shallowRef({
  name: '触发'
})

const change = () => {
  // 以下不会触发
  value.value.name = '不触发'
  // 以下会触发
  value.value = {
    name: '触发了'
  }
}
</script>

<template>
  <div>
    {{ value }}
    <button @click="change">Click Me</button>
  </div>
</template>
```

shallowRef 的浅响应大概就是这样了

还有一点是`ref`和`shallowRef`是不能一起使用的，否则当 ref 变化时会影响到 shallowRef，导致视图更新

## triggerRef

顾名思义`trigger`触发 ，triggerRef 会触发 Ref，在上方不会触发的代码下加入下方代码就会完成触发事件，导致 shallowRef 更新

```jsx
triggerRef(value);
```

## customRef

自定义 Ref

```jsx
<script setup>
const myRef = (value) => {
  return customRef((track, trigger) => {
    return {
      get() {
        track() // 收集依赖
        return value
      },
      set(newVal) {
        value = newVal
        trigger() // 触发
      }
    }
  })
}

const obj = myRef('测试1')
const changeMyRef = () => {
  obj.value = '测试2'
}
</script>

<template>
  <div>
    {{ obj }}
    <button @click="changeMyRef">Click Me</button>
  </div>
</template>
```

再在上面修改一下加上防抖的功能

```jsx
const myRef = (value) => {
  let timer;
  return customRef((track, trigger) => {
    return {
      get() {
        track(); // 收集依赖
        return value;
      },
      set(newVal) {
        clearTimeout(timer);
        timer = setTimeout(() => {
          console.log("触发了");
          value = newVal;
          timer = null;
          trigger(); // 触发
        }, 1000);
      },
    };
  });
};
```
