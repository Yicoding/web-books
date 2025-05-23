---
title: rem 适配
order: 1
group:
  title: css
  order: 1
nav:
  title: 基础
  order: 1
---

# rem 适配

## 方案一：CSS 实现

- 可能会存在兼容性问题
- 比 js 生效更快

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      html {
        font-size: 12px;
      }

      @media screen and (max-width: 750px) {
        html {
          font-size: calc(100vw / 37.5);
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

## 方案二：JS 实现

- 兼容性更好
- 依赖 js 执行

```html
<!DOCTYPE html>
<html lang="zh">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
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
          resizeEvt =
            'orientationchange' in win ? 'orientationchange' : 'resize';
          var recalc = function () {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;
            docEl.style.fontSize =
              10 * ((clientWidth >= 750 ? 750 : clientWidth) / 375) + 'px';
          };
          if (!doc.addEventListener) return;
          win.addEventListener(resizeEvt, recalc, false);
          doc.addEventListener('DOMContentLoaded', recalc, false);
        } catch (error) {
          console.log('计算rem error: ', error);
        }
      })(document, window);
    </script>
  </body>
</html>
```
