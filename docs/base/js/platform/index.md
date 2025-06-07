---
title: 判断平台环境
order: 5
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 判断平台环境

```js | pure
/**
 * 获取当前的运行平台
 */
export function getPlatform(): Platform {
  let platform: Platform = 'iting';

  const ua = window.navigator.userAgent;
  const impl = getCookie('impl') || '';
  if (/iting/i.test(ua) || /iting/i.test(impl)) {
    platform = 'iting';
  } else if (/wxwork/i.test(ua)) {
    // 企业微信
    platform = 'wecom';
  } else if (/micromessenger/i.test(ua)) {
    platform = 'wechat';
  } else if (/weibo/i.test(ua)) {
    platform = 'weibo';
  } else if (/qq\//i.test(ua)) {
    platform = 'qq';
  } else if (/ximalayababy/i.test(ua)) {
    platform = 'ximalayababy';
  } else if (/xiaoya/i.test(ua)) {
    platform = 'xiaoya';
  } else {
    platform = '_default';
  }

  return platform;
}
```
