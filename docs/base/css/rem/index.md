---
title: rem 适配
order: 1
toc: content
group:
  title: css
  order: 1
nav:
  title: 基础
  order: 1
---

# rem 适配

## 方案一：纯 CSS 实现

- 可能会存在兼容性问题
- 比 js 生效更快
- 适合静态页面，不支持动态调整

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      /* 默认字体大小 */
      html {
        font-size: 12px;
      }

      /* 移动端适配 */
      @media screen and (max-width: 750px) {
        html {
          font-size: calc(100vw / 37.5);
        }
      }

      /* 防止字体大小过小 */
      @media screen and (max-width: 320px) {
        html {
          font-size: 8.53px;
        }
      }

      /* 防止字体大小过大 */
      @media screen and (min-width: 750px) {
        html {
          font-size: 20px;
        }
      }

      .root {
        font-size: 1.6rem;
      }
    </style>
  </head>
  <body>
    <div class="root">root</div>
  </body>
</html>
```

## 方案二：纯 JS 实现

- 兼容性更好
- 依赖 js 执行
- 支持动态调整和横竖屏切换

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      /* 默认字体大小 */
      html {
        font-size: 12px;
      }

      .root {
        font-size: 2rem;
      }
    </style>
  </head>
  <body>
    <div class="root">root</div>

    <script type="text/javascript">
      !(function (doc, win) {
        try {
          var docEl = doc.documentElement;
          var resizeEvt =
            'orientationchange' in win ? 'orientationchange' : 'resize';

          // 设置 rem 函数
          function setRem() {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;

            // 设置最大最小值限制
            var maxWidth = 750;
            var minWidth = 320;
            var maxFontSize = 20;
            var minFontSize = 8.53;

            // 计算当前宽度对应的字体大小
            var fontSize = 10 * (clientWidth / 375);

            // 限制字体大小范围
            fontSize = Math.min(Math.max(fontSize, minFontSize), maxFontSize);

            // 设置字体大小
            docEl.style.fontSize = fontSize + 'px';
          }

          // 监听事件
          if (!doc.addEventListener) return;
          win.addEventListener(resizeEvt, setRem, false);
          doc.addEventListener('DOMContentLoaded', setRem, false);

          // 页面显示时重新计算
          win.addEventListener(
            'pageshow',
            function (e) {
              if (e.persisted) {
                setRem();
              }
            },
            false,
          );

          // 初始化
          setRem();
        } catch (error) {
          console.log('计算rem error: ', error);
        }
      })(document, window);
    </script>
  </body>
</html>
```

## 方案三：CSS + JS 终极方案

- 结合了 CSS 和 JS 的优点
- 首次加载使用 CSS 方案，保证快速响应
- JS 方案作为降级和动态调整的补充
- 支持动态调整和横竖屏切换

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      /* 默认字体大小 */
      html {
        font-size: 12px;
      }

      /* 首次加载时使用 CSS 方案 */
      @media screen and (max-width: 750px) {
        html {
          font-size: calc(100vw / 37.5);
        }
      }

      /* 防止字体大小过小 */
      @media screen and (max-width: 320px) {
        html {
          font-size: 8.53px;
        }
      }

      /* 防止字体大小过大 */
      @media screen and (min-width: 750px) {
        html {
          font-size: 20px;
        }
      }

      .root {
        font-size: 1.6rem;
      }
    </style>
  </head>
  <body>
    <div class="root">root</div>

    <script type="text/javascript">
      !(function (doc, win) {
        try {
          var docEl = doc.documentElement;
          var resizeEvt =
            'orientationchange' in win ? 'orientationchange' : 'resize';

          // 设置 rem 函数
          function setRem() {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;

            // 设置最大最小值限制
            var maxWidth = 750;
            var minWidth = 320;
            var maxFontSize = 20;
            var minFontSize = 8.53;

            // 计算当前宽度对应的字体大小
            var fontSize = 10 * (clientWidth / 375);

            // 限制字体大小范围
            fontSize = Math.min(Math.max(fontSize, minFontSize), maxFontSize);

            // 设置字体大小
            docEl.style.fontSize = fontSize + 'px';
          }

          // 监听事件
          if (!doc.addEventListener) return;
          win.addEventListener(resizeEvt, setRem, false);
          doc.addEventListener('DOMContentLoaded', setRem, false);

          // 页面显示时重新计算
          win.addEventListener(
            'pageshow',
            function (e) {
              if (e.persisted) {
                setRem();
              }
            },
            false,
          );

          // 初始化
          setRem();
        } catch (error) {
          console.log('计算rem error: ', error);
        }
      })(document, window);
    </script>
  </body>
</html>
```

### 方案三的优势

1. **快速响应**：首次加载时使用 CSS 方案，保证页面快速渲染
2. **动态适配**：JS 方案作为补充，支持动态调整和横竖屏切换
3. **安全限制**：设置了字体大小的最大最小值，防止极端情况下的显示问题
4. **兼容性好**：同时支持现代浏览器和旧版浏览器
5. **性能优化**：使用防抖处理，避免频繁计算
6. **降级处理**：当 JS 失效时，CSS 方案仍然可以保证基本适配
