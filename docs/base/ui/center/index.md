---
title: 居中布局
order: 7
toc: content
group:
  title: ui
  order: 1
nav:
  title: 基础
  order: 1
---

# 居中布局

CSS 居中布局是前端开发中最常用的布局技巧之一。以下是六种最常用的居中实现方案。

## 1. text-align 居中

适用于行内元素（inline）和行内块元素（inline-block）的水平居中。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo1.less';

export default () => (
  <div className="text-align-center">
    <span>行内元素水平居中</span>
  </div>
);
```

### 特点

- 只支持水平居中
- 适用于行内元素
- 兼容性最好

## 2. line-height 居中

适用于单行文本的垂直居中。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo2.less';

export default () => (
  <div className="line-height-center">
    <span>单行文本垂直居中</span>
  </div>
);
```

### 特点

- 只适用于单行文本
- 需要知道容器高度
- 实现简单

## 3. vertical-align 居中

适用于行内元素在行内的垂直对齐。需要配合 line-height 使用，因为行内元素的垂直对齐是相对于行框（line box）进行的。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo3.less';

export default () => (
  <div>
    <div className="vertical-align-center">
      <span>有 line-height 的垂直对齐</span>
    </div>
    <div className="vertical-align-center-height-only">
      <span>只有 height 的垂直对齐</span>
    </div>
  </div>
);
```

### 特点

- 需要配合 line-height 使用
- 只适用于行内元素
- 常用于图标对齐

### 工作原理

1. 行内元素的垂直对齐是相对于行框（line box）进行的
2. 行框的高度由 line-height 决定，而不是 height
3. 只设置 height 时，行框高度仍然由内容决定，vertical-align 无法正确工作
4. 设置 line-height 后，行框有了固定高度，vertical-align 才能正确对齐

## 4. margin: auto 居中

适用于块级元素的水平居中。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo4.less';

export default () => (
  <div className="margin-center">
    <div className="box">
      <span>块级元素水平居中</span>
    </div>
  </div>
);
```

### 特点

- 只支持水平居中
- 需要设置元素宽度
- 兼容性好

## 5. position: absolute 居中

适用于固定尺寸元素的水平和垂直居中。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo5.less';

export default () => (
  <div className="position-center">
    <div className="box">
      <span>固定尺寸元素居中</span>
    </div>
  </div>
);
```

### 特点

- 支持水平和垂直居中
- 需要知道元素尺寸
- 会脱离文档流

## 6. flex 居中

最灵活的居中方案，支持各种尺寸元素的居中。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo6.less';

export default () => (
  <div className="flex-center">
    <div className="box">
      <span>flex 居中</span>
    </div>
  </div>
);
```

### 特点

- 支持水平和垂直居中
- 不需要知道元素尺寸
- 现代浏览器支持

## 使用场景

1. text-align: 文本、行内元素水平居中
2. line-height: 单行文本垂直居中
3. vertical-align: 行内元素垂直对齐
4. margin: auto: 块级元素水平居中
5. position: absolute: 固定尺寸元素居中
6. flex: 各种尺寸元素居中

## 注意事项

1. 选择合适的居中方案
2. 考虑浏览器兼容性
3. 注意元素尺寸要求
4. 考虑文档流影响
5. 注意性能影响

## 最佳实践

1. 优先使用 flex 布局
2. 考虑兼容性要求
3. 注意元素类型
4. 保持代码简洁
5. 考虑响应式设计
