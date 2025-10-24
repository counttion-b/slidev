---
# try also 'default' to start simple
theme: ./theme
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: 匀变速直线运动实例
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
hideInToc: true
addons:
  - slidev-addon-graph
---

---
layout: cover
titleZh: 带电粒子在复合场中的运动
session: Autumn-7
date: 25.10.25
teacher: 田以恒
---

---
layout: two-cols
hideInToc: true
---

# Content

<Toc minDepth="1" maxDepth="2" />



---
transition: fade-out
---

# 自由落体
<Toc mode="onlyCurrentTree" minDepth="2"/>

---
transition: fade-out
level: 2
---

# 公式法
1
$\sqrt{3x-1}+(1+x)^2$

---
transition: fade-out
title: 推论法
level: 2
---

#自由落体
1

---
transition: fade-out
title: 竖直上抛
---

#竖直上抛
1

---
transition: fade-out
title: 多过程
---

#多过程
<SlidevGraph
  id="graph1"
  :items="[
    { name: 'foo', color: '#155' },
    { name: 'bar', color: '#551', from: ['foo'] },
  ]"
/>

---
title: 题解演示（可滚动容器）
level: 2
---

## 题目解答（触控可滚动）

使用方式一：组件
$\sqrt{3x-1}+(1+x)^2$
<Solution src="/files/9.27.md" maxHeight="25vh" />

<br>

$F=ma$
