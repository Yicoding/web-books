---
title: 1 像素边框
order: 2
toc: content
group:
  title: ui
  order: 1
nav:
  title: 基础
  order: 1
---

# 1 像素边框

在移动端开发中，由于设备像素比（Device Pixel Ratio，DPR）的存在，1px 的边框在设备上实际显示时会显得过粗。这是因为在高清屏下，1px 的 CSS 像素实际上对应着多个物理像素。本文将介绍几种解决 1px 边框问题的方案。

## 方案一：使用伪元素 + transform

使用伪元素配合 transform: scale(0.5) 将边框缩小一半，实现 0.5px 的效果。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo1.less';

export default () => (
  <div>
    <div className="border-1px">全边框</div>
    <div className="border-top-1px">上边框</div>
    <div className="border-bottom-1px">下边框</div>
    <div className="border-left-1px">左边框</div>
    <div className="border-right-1px">右边框</div>
  </div>
);
```

## 方案二：使用 box-shadow

使用 box-shadow 模拟边框，可以精确控制边框的粗细。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo2.less';

export default () => (
  <div>
    <div className="border-shadow">全边框</div>
    <div className="border-top">上边框</div>
    <div className="border-bottom">下边框</div>
    <div className="border-left">左边框</div>
    <div className="border-right">右边框</div>
    <div className="border-top-bottom">上下边框</div>
    <div className="border-left-right">左右边框</div>
  </div>
);
```

## 方案三：使用 div + transform

使用 div 元素设置 1px 高度，然后通过 transform: scaleY(0.5) 实现 0.5px 边框。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo3.less';

export default () => (
  <div>
    <div>item</div>
    <div className="border-div-single"></div>
    <div>item</div>
  </div>
);
```

## 各方案对比

| 方案               | 优点                     | 缺点              | 适用场景 |
| ------------------ | ------------------------ | ----------------- | -------- |
| 伪元素 + transform | 实现简单，兼容性好       | 需要额外元素      | 复杂场景 |
| box-shadow         | 实现简单，可控制边框粗细 | 性能较差          | 简单边框 |
| div + transform    | 实现简单，结构清晰       | 需要额外 DOM 元素 | 复杂场景 |

## 最佳实践建议

1. 对于复杂场景，建议使用伪元素 + transform 方案
2. 需要精确控制边框粗细时，可以使用 box-shadow 方案
3. 需要更清晰的结构时，可以使用 div + transform 方案

## 注意事项

1. 使用 transform: scale 方案时，需要注意父元素的 overflow 属性
2. box-shadow 方案在大量使用时可能影响性能
3. div + transform 方案需要注意额外的 DOM 结构
