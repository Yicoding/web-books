---
title: box-shadow
order: 6
toc: content
group:
  title: css
  order: 1
nav:
  title: 基础
  order: 1
---

# box-shadow

`box-shadow` 属性用于在元素的框架上添加一个或多个阴影效果。该属性可以设置多个阴影，每个阴影用逗号分隔。

## 语法

```css
box-shadow: [inset?] <offset-x> <offset-y> <blur-radius>? <spread-radius>?
  <color>?;
```

### 参数说明

- `inset`（可选）：将外部阴影改为内部阴影
- `offset-x`（必需）：水平偏移量，正值向右，负值向左
- `offset-y`（必需）：垂直偏移量，正值向下，负值向上
- `blur-radius`（可选）：模糊半径，值越大阴影越模糊
- `spread-radius`（可选）：阴影扩散半径，正值扩大阴影，负值缩小阴影
- `color`（可选）：阴影颜色，默认为当前文本颜色

## 示例

### 1. 单边阴影

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo1.less';

export default () => (
  <div className="single-shadow-demo">
    <div className="shadow-bottom">底部阴影</div>
    <div className="shadow-right">右侧阴影</div>
  </div>
);
```

### 2. 内阴影

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo2.less';

export default () => (
  <div className="inset-shadow-demo">
    <div className="shadow-inset">内阴影效果</div>
  </div>
);
```
