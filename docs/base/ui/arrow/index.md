---
title: css 绘制箭头
order: 3
toc: content
group:
  title: ui
  order: 1
nav:
  title: 基础
  order: 1
---

# css 绘制箭头

CSS 绘制箭头有多种实现方式，每种方式都有其适用场景。以下是常用的实现方法：

`推荐方案1`

## 1. 使用 border 实现（简洁版）

通过设置边框和旋转来创建简洁的空心箭头。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo1.less';

export default () => (
  <div className="parant">
    <div className="arrow arrow-up"></div>
    <div className="arrow arrow-down"></div>
    <div className="arrow arrow-left"></div>
    <div className="arrow arrow-right"></div>
  </div>
);
```

### 特点

- 实现最简单
- 代码最简洁
- 兼容性好
- 性能最好
- 可以轻松调整大小和颜色

## 2. 使用伪元素实现

通过伪元素来创建空心箭头。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo2.less';

export default () => (
  <div className="parant2">
    <div className="arrow2 arrow-up2"></div>
    <div className="arrow2 arrow-down2"></div>
    <div className="arrow2 arrow-left2"></div>
    <div className="arrow2 arrow-right2"></div>
  </div>
);
```

### 特点

- 实现简单
- 兼容性好
- 性能好
- 可以轻松调整箭头大小和粗细
- 可以添加动画效果
- 代码结构清晰
