---
title: css 绘制箭头
order: 3
toc: content
group:
  title: css
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

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Arrow - Simple</title>
    <style>
      div {
        margin: 10px;
      }
      .arrow {
        display: inline-block;
        width: 10px;
        height: 10px;
        border: 2px solid #000;
      }

      /* 向上箭头 */
      .arrow-up {
        border-width: 2px 2px 0 0;
        transform: rotate(-45deg);
      }

      /* 向下箭头 */
      .arrow-down {
        border-width: 0 2px 2px 0;
        transform: rotate(45deg);
      }

      /* 向左箭头 */
      .arrow-left {
        border-width: 2px 0 0 2px;
        transform: rotate(-45deg);
      }

      /* 向右箭头 */
      .arrow-right {
        border-width: 0 0 2px 2px;
        transform: rotate(45deg);
      }
    </style>
  </head>
  <body>
    <div class="arrow arrow-up"></div>
    <div class="arrow arrow-down"></div>
    <div class="arrow arrow-left"></div>
    <div class="arrow arrow-right"></div>
  </body>
</html>
```

### 特点

- 实现最简单
- 代码最简洁
- 兼容性好
- 性能最好
- 可以轻松调整大小和颜色

## 2. 使用伪元素实现

通过伪元素来创建空心箭头。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Arrow</title>
    <style>
      div {
        margin: 10px;
      }
      /* 基础箭头 */
      .arrow {
        position: relative;
        width: 10px;
        height: 10px;
      }

      .arrow::before {
        content: '';
        position: absolute;
        width: 10px;
        height: 10px;
        border-top: 2px solid #000;
        border-right: 2px solid #000;
      }

      /* 向上箭头 */
      .arrow-up::before {
        transform: rotate(-45deg);
        top: 0;
        left: 0;
      }

      /* 向下箭头 */
      .arrow-down::before {
        transform: rotate(135deg);
        top: 0;
        left: 0;
      }

      /* 向左箭头 */
      .arrow-left::before {
        transform: rotate(-135deg);
        top: 0;
        left: 0;
      }

      /* 向右箭头 */
      .arrow-right::before {
        transform: rotate(45deg);
        top: 0;
        left: 0;
      }
    </style>
  </head>
  <body>
    <div class="arrow arrow-up"></div>
    <div class="arrow arrow-down"></div>
    <div class="arrow arrow-left"></div>
    <div class="arrow arrow-right"></div>
  </body>
</html>
```

### 特点

- 实现简单
- 兼容性好
- 性能好
- 可以轻松调整箭头大小和粗细
- 可以添加动画效果
- 代码结构清晰
