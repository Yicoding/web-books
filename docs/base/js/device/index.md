---
title: 判断设备类型
order: 5
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 判断设备类型

```js | pure
/**
 * 获取设备类型
 */
export function getDevice(): Device {
  let device: Device = 'android';
  const ua = window.navigator.userAgent;
  if (/android/i.test(ua)) {
    device = 'android';
  } else if (ua.match(/iPhone|iPad|iPod/i)) {
    device = 'ios';
  }
  return device;
}
```
