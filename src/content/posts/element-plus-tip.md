---
title: Element-Plus 笔记
published: 2024-05-18
description: ""
image: ""
tags: [Vue3, Element-Plus]
category: "前端"
draft: false
lang: ""
---

## Tree

Tree 组件

### 设置 Tree 组件全部展开

```jsx
const authTreeRef = ref();
// checkbox
const checkStrictly = ref(true);
// 展开
const expand = ref(false);
watch(
  () => expand.value,
  () => {
    console.log(`output->expand.value`, expand.value);
    let nodes = authTreeRef.value.store.nodesMap;
    for (const node in nodes) {
      nodes[node].expanded = expand.value;
      // nodes[node].checked = expand.value; 设置全选
    }
  }
);
```
