---
title: css 绘制三角形
order: 4
toc: content
group:
  title: css
  order: 1
nav:
  title: 基础
  order: 1
---

# css 绘制三角形

CSS 绘制三角形有多种实现方式，每种方式都有其适用场景。以下是常用的实现方法：

`推荐方案1`

## 1. 使用 border 实现（简洁版）

通过设置边框和透明色来创建三角形。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Triangle - Simple</title>
    <style>
      div {
        margin: 10px;
      }
      .triangle {
        width: 0;
        height: 0;
        border: 10px solid transparent;
      }

      /* 向上三角形 */
      .triangle-up {
        border-bottom-color: #000;
      }

      /* 向下三角形 */
      .triangle-down {
        border-top-color: #000;
      }

      /* 向左三角形 */
      .triangle-left {
        border-right-color: #000;
      }

      /* 向右三角形 */
      .triangle-right {
        border-left-color: #000;
      }
    </style>
  </head>
  <body>
    <div class="triangle triangle-up"></div>
    <div class="triangle triangle-down"></div>
    <div class="triangle triangle-left"></div>
    <div class="triangle triangle-right"></div>
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

通过伪元素来创建三角形。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Triangle</title>
    <style>
      div {
        margin: 10px;
      }
      /* 基础三角形 */
      .triangle {
        position: relative;
        width: 20px;
        height: 20px;
      }

      .triangle::before {
        content: '';
        position: absolute;
        width: 0;
        height: 0;
        border: 10px solid transparent;
      }

      /* 向上三角形 */
      .triangle-up::before {
        border-bottom-color: #000;
        top: 0;
        left: 0;
      }

      /* 向下三角形 */
      .triangle-down::before {
        border-top-color: #000;
        top: 0;
        left: 0;
      }

      /* 向左三角形 */
      .triangle-left::before {
        border-right-color: #000;
        top: 0;
        left: 0;
      }

      /* 向右三角形 */
      .triangle-right::before {
        border-left-color: #000;
        top: 0;
        left: 0;
      }
    </style>
  </head>
  <body>
    <div class="triangle triangle-up"></div>
    <div class="triangle triangle-down"></div>
    <div class="triangle triangle-left"></div>
    <div class="triangle triangle-right"></div>
  </body>
</html>
```

### 特点

- 实现简单
- 兼容性好
- 性能好
- 可以轻松调整大小和颜色
- 可以添加动画效果
- 代码结构清晰
