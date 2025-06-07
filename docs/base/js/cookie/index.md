---
title: 获取cookie
order: 4
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 获取 cookie

```js | pure
/**
 * 获取某个 cookie 中某个字段的值
 * @param name 字段名
 */
export function getCookie(name: string) {
  const value = `; ${document.cookie}`;
  const [, parts2] = value.split(`; ${name}=`);
  if (parts2) {
    return parts2.split(';').shift();
  }
  return undefined;
}
```
