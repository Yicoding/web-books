---
title: css 实现文字省略号
order: 5
toc: content
group:
  title: css
  order: 1
nav:
  title: 基础
  order: 1
---

# css 实现文字省略号

CSS 实现文字省略号有多种方式，根据行数需求可以选择不同的实现方法。以下是常用的实现方法：

`推荐方案1`

## 1. 单行省略号

通过设置 `text-overflow` 属性实现单行文本省略。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Ellipsis - Single Line</title>
    <style>
      .ellipsis {
        width: 200px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
    </style>
  </head>
  <body>
    <div class="ellipsis">
      这是一段很长的文本，超出部分会显示省略号。这是一段很长的文本，超出部分会显示省略号。
    </div>
  </body>
</html>
```

### 特点

- 实现最简单
- 兼容性最好
- 性能最好
- 适用于单行文本截断

## 2. 多行省略号

通过设置 `-webkit-line-clamp` 属性实现多行文本省略，可以自定义显示行数。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Ellipsis - Multiple Lines</title>
    <style>
      /* 两行省略 */
      .ellipsis-2 {
        width: 200px;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
        overflow: hidden;
      }

      /* 三行省略 */
      .ellipsis-3 {
        width: 200px;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 3;
        overflow: hidden;
      }

      /* 更多行数省略 */
      .ellipsis-n {
        width: 200px;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: n; /* n 为需要显示的行数 */
        overflow: hidden;
      }
    </style>
  </head>
  <body>
    <div class="ellipsis-2">
      这是一段很长的文本，超出两行部分会显示省略号。这是一段很长的文本，超出两行部分会显示省略号。这是一段很长的文本，超出两行部分会显示省略号。
    </div>
    <div class="ellipsis-3">
      这是一段很长的文本，超出三行部分会显示省略号。这是一段很长的文本，超出三行部分会显示省略号。这是一段很长的文本，超出三行部分会显示省略号。这是一段很长的文本，超出三行部分会显示省略号。
    </div>
  </body>
</html>
```

### 特点

- 实现简单
- 兼容性较好
- 可以自定义显示行数
- 需要 webkit 内核支持
- 适用于两行及以上的文本截断

## 3. 兼容性处理

对于不支持 `-webkit-line-clamp` 的浏览器，推荐使用 JavaScript 动态截断文本并添加省略号。相比伪元素 `::after` 绝对定位的方式，JS 截断可以让省略号紧贴文本结尾，视觉和体验更佳。

> **注意**：伪元素 `::after` 方案会导致省略号固定在右下角，和文本之间有较大空白，无法做到真正的多行省略号，仅适合简单视觉补充，不推荐用于严谨场景。

### JS 动态截断方案（折半查找，性能更优）

采用折半查找（二分法）高效定位截断点，适合长文本场景。

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <title>CSS Ellipsis - Fallback (JS, Binary Search)</title>
    <style>
      .ellipsis-fallback {
        width: 200px;
        line-height: 1.5;
        font-size: 20px;
        overflow: hidden;
        word-break: break-all;
      }
    </style>
  </head>
  <body>
    <div class="ellipsis-fallback" data-line="3">
      这是一段很长的文本，超出部分会显示省略号。这是一段很长的文本，超出部分会显示省略号。这是一段很长的文本，超出部分会显示省略号。
    </div>
    <script>
      function multilineEllipsis(selector, lines) {
        const el = document.querySelector(selector);
        const lineHeight = parseFloat(getComputedStyle(el).lineHeight);
        const maxHeight = lineHeight * lines;
        const fullText = el.innerText;
        let left = 0,
          right = fullText.length,
          result = '';
        // 先还原完整文本
        el.innerText = fullText;
        // 折半查找
        while (left <= right) {
          const mid = Math.floor((left + right) / 2);
          el.innerText = fullText.slice(0, mid) + '...';
          if (el.scrollHeight > maxHeight) {
            right = mid - 1;
          } else {
            result = fullText.slice(0, mid) + '...';
            left = mid + 1;
          }
        }
        el.innerText = result;
      }
      const el = document.querySelector('.ellipsis-fallback');
      const lines = parseInt(el.dataset.line) || 2;
      multilineEllipsis('.ellipsis-fallback', lines);
      window.addEventListener('resize', () =>
        multilineEllipsis('.ellipsis-fallback', lines),
      );
    </script>
  </body>
</html>
```

### 特点

- 兼容性最好
- 省略号紧贴文本结尾，视觉体验好
- 采用折半查找法，性能极高，适合长文本
- 需要 JavaScript 动态截断文本
- 适用于所有浏览器
- 支持动态调整行数（通过 data-line 属性）
- 响应式支持（监听窗口大小变化）

### 使用说明

1. 添加 `ellipsis-fallback` 类到需要省略的元素
2. 通过 `data-line` 属性设置需要显示的行数
3. 确保元素有固定宽度
4. JavaScript 会自动计算并设置正确的最大高度

### 注意事项

- 需要确保元素有明确的宽度
- 该方案会直接截断文本内容，不能保留 HTML 标签
- 如果内容动态变化，需要重新调用 multilineEllipsis 函数
- 建议在页面加载完成后执行初始化
