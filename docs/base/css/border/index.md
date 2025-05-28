---
title: 1像素边框
order: 2
toc: content
group:
  title: css
  order: 1
nav:
  title: 基础
  order: 1
---

# 1 像素边框

在移动端开发中，由于设备像素比（Device Pixel Ratio，DPR）的存在，1px 的边框在设备上实际显示时会显得过粗。这是因为在高清屏下，1px 的 CSS 像素实际上对应着多个物理像素。本文将介绍几种解决 1px 边框问题的方案。

## 方案一：使用 transform: scale(0.5)

通过 transform: scale(0.5) 将边框缩小一半，实现 0.5px 的效果。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>1px border solution</title>
    <style>
      div {
        margin: 10px 0;
      }

      /* 全边框 */
      .border-1px {
        position: relative;
      }

      .border-1px::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 200%;
        height: 200%;
        transform: scale(0.5);
        transform-origin: left top;
        box-sizing: border-box;
        border: 1px solid #000;
        border-radius: 4px;
      }

      /* 单边框 */
      .border-top-1px {
        position: relative;
      }

      .border-top-1px::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 200%;
        height: 1px;
        transform: scale(0.5);
        transform-origin: left top;
        background: #000;
      }

      .border-bottom-1px {
        position: relative;
      }

      .border-bottom-1px::after {
        content: '';
        position: absolute;
        left: 0;
        bottom: 0;
        width: 200%;
        height: 1px;
        transform: scale(0.5);
        transform-origin: left bottom;
        background: #000;
      }

      .border-left-1px {
        position: relative;
      }

      .border-left-1px::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 1px;
        height: 200%;
        transform: scale(0.5);
        transform-origin: left top;
        background: #000;
      }

      .border-right-1px {
        position: relative;
      }

      .border-right-1px::after {
        content: '';
        position: absolute;
        right: 0;
        top: 0;
        width: 1px;
        height: 200%;
        transform: scale(0.5);
        transform-origin: right top;
        background: #000;
      }
    </style>
  </head>
  <body>
    <div class="border-1px">全边框</div>
    <div class="border-top-1px">上边框</div>
    <div class="border-bottom-1px">下边框</div>
    <div class="border-left-1px">左边框</div>
    <div class="border-right-1px">右边框</div>
  </body>
</html>
```

## 方案二：使用 box-shadow

使用 box-shadow 模拟边框，可以精确控制边框的粗细。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>1px border solution</title>
    <style>
      div {
        margin: 10px 0;
      }

      /* 全边框 */
      .border-shadow {
        box-shadow: 0 0 0 0.5px #000;
      }

      /* 单边框 */
      .border-top {
        box-shadow: 0 -0.5px 0 0 #000;
      }

      .border-bottom {
        box-shadow: 0 0.5px 0 0 #000;
      }

      .border-left {
        box-shadow: -0.5px 0 0 0 #000;
      }

      .border-right {
        box-shadow: 0.5px 0 0 0 #000;
      }

      /* 多边框组合 */
      .border-top-bottom {
        box-shadow: 0 -0.5px 0 0 #000, 0 0.5px 0 0 #000;
      }

      .border-left-right {
        box-shadow: -0.5px 0 0 0 #000, 0.5px 0 0 0 #000;
      }
    </style>
  </head>
  <body>
    <div class="border-shadow">全边框</div>
    <div class="border-top">上边框</div>
    <div class="border-bottom">下边框</div>
    <div class="border-left">左边框</div>
    <div class="border-right">右边框</div>
    <div class="border-top-bottom">上下边框</div>
    <div class="border-left-right">左右边框</div>
  </body>
</html>
```

## 方案三：使用伪元素 + transform

使用伪元素配合 transform: scale(0.5) 实现 0.5px 边框。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>1px border solution</title>
    <style>
      div {
        margin: 10px 0;
      }

      /* 全边框 */
      .border-pseudo {
        position: relative;
      }

      .border-pseudo::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 200%;
        height: 200%;
        transform: scale(0.5);
        transform-origin: left top;
        box-sizing: border-box;
        border: 1px solid #000;
      }

      /* 单边框 */
      .border-pseudo-top {
        position: relative;
      }

      .border-pseudo-top::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 200%;
        height: 1px;
        transform: scale(0.5);
        transform-origin: left top;
        background: #000;
      }

      .border-pseudo-bottom {
        position: relative;
      }

      .border-pseudo-bottom::after {
        content: '';
        position: absolute;
        left: 0;
        bottom: 0;
        width: 200%;
        height: 1px;
        transform: scale(0.5);
        transform-origin: left bottom;
        background: #000;
      }

      .border-pseudo-left {
        position: relative;
      }

      .border-pseudo-left::after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 1px;
        height: 200%;
        transform: scale(0.5);
        transform-origin: left top;
        background: #000;
      }

      .border-pseudo-right {
        position: relative;
      }

      .border-pseudo-right::after {
        content: '';
        position: absolute;
        right: 0;
        top: 0;
        width: 1px;
        height: 200%;
        transform: scale(0.5);
        transform-origin: right top;
        background: #000;
      }
    </style>
  </head>
  <body>
    <div class="border-pseudo">全边框</div>
    <div class="border-pseudo-top">上边框</div>
    <div class="border-pseudo-bottom">下边框</div>
    <div class="border-pseudo-left">左边框</div>
    <div class="border-pseudo-right">右边框</div>
  </body>
</html>
```

## 方案四：使用 div + transform

使用 div 元素设置 1px 高度，然后通过 transform: scale(0.5) 实现 0.5px 边框。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>1px border solution</title>
    <style>
      div {
        margin: 10px 0;
      }

      /* 全边框 */
      .border-div {
        position: relative;
      }

      .border-div-top,
      .border-div-bottom,
      .border-div-left,
      .border-div-right {
        position: absolute;
        background: #000;
        transform: scale(0.5);
      }

      .border-div-top {
        left: 0;
        top: 0;
        width: 200%;
        height: 1px;
        transform-origin: left top;
      }

      .border-div-bottom {
        left: 0;
        bottom: 0;
        width: 200%;
        height: 1px;
        transform-origin: left bottom;
      }

      .border-div-left {
        left: 0;
        top: 0;
        width: 1px;
        height: 200%;
        transform-origin: left top;
      }

      .border-div-right {
        right: 0;
        top: 0;
        width: 1px;
        height: 200%;
        transform-origin: right top;
      }

      /* 单边框 */
      .border-div-single {
        position: relative;
      }

      .border-div-single-top {
        position: absolute;
        left: 0;
        top: 0;
        width: 200%;
        height: 1px;
        background: #000;
        transform: scale(0.5);
        transform-origin: left top;
      }

      .border-div-single-bottom {
        position: absolute;
        left: 0;
        bottom: 0;
        width: 200%;
        height: 1px;
        background: #000;
        transform: scale(0.5);
        transform-origin: left bottom;
      }

      .border-div-single-left {
        position: absolute;
        left: 0;
        top: 0;
        width: 1px;
        height: 200%;
        background: #000;
        transform: scale(0.5);
        transform-origin: left top;
      }

      .border-div-single-right {
        position: absolute;
        right: 0;
        top: 0;
        width: 1px;
        height: 200%;
        background: #000;
        transform: scale(0.5);
        transform-origin: right top;
      }
    </style>
  </head>
  <body>
    <!-- 全边框 -->
    <div class="border-div">
      全边框
      <div class="border-div-top"></div>
      <div class="border-div-bottom"></div>
      <div class="border-div-left"></div>
      <div class="border-div-right"></div>
    </div>

    <!-- 单边框 -->
    <div class="border-div-single">
      上边框
      <div class="border-div-single-top"></div>
    </div>

    <div class="border-div-single">
      下边框
      <div class="border-div-single-bottom"></div>
    </div>

    <div class="border-div-single">
      左边框
      <div class="border-div-single-left"></div>
    </div>

    <div class="border-div-single">
      右边框
      <div class="border-div-single-right"></div>
    </div>
  </body>
</html>
```

## 各方案对比

| 方案               | 优点                     | 缺点              | 适用场景 |
| ------------------ | ------------------------ | ----------------- | -------- |
| transform: scale   | 实现简单，兼容性好       | 可能影响其他元素  | 简单边框 |
| box-shadow         | 实现简单，可控制边框粗细 | 性能较差          | 简单边框 |
| 伪元素 + transform | 实现简单，兼容性好       | 需要额外元素      | 复杂场景 |
| div + transform    | 实现简单，结构清晰       | 需要额外 DOM 元素 | 复杂场景 |

## 最佳实践建议

1. 对于简单的边框需求，推荐使用 transform: scale 方案
2. 需要精确控制边框粗细时，可以使用 box-shadow 方案
3. 对于复杂场景，建议使用伪元素 + transform 方案
4. 需要更清晰的结构时，可以使用 div + transform 方案

## 注意事项

1. 使用 transform: scale 方案时，需要注意父元素的 overflow 属性
2. box-shadow 方案在大量使用时可能影响性能
3. 伪元素方案需要注意清除浮动
4. div + transform 方案需要注意额外的 DOM 结构
