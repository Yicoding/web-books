---
title: URL Params
order: 7
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# URL Params

在 JavaScript 中，有多种方法可以获取 URL 参数。本文将介绍最常用的几种方法。

## URLSearchParams

`URLSearchParams` 是现代浏览器提供的原生 API，用于处理 URL 的查询字符串。以下是封装后的方法：

```typescript
/**
 * 获取url参数
 * @param {string} field - 要获取的参数名
 * @returns {string | null} 参数值，如果不存在则返回 null
 */
export function getSearchParams(field: string) {
  const search = new URLSearchParams(window.location.search);
  return search.get(field);
}

// 使用示例
const value = getSearchParams('key');
console.log(value); // 例如：'value'
```

## 手动解析 URL 参数

如果需要手动解析 URL 参数，可以使用以下优化后的方法：

```javascript
/**
 * 手动解析URL参数
 * @param {string} key - 要获取的参数名
 * @returns {string | null} 参数值，如果不存在则返回 null
 */
function getParamValue(key) {
  try {
    // 获取查询字符串部分(去掉?符号)
    const queryString = location.search.slice(1);
    if (!queryString) return null;

    // 按&分割成数组
    const pairs = queryString.split('&');

    // 遍历数组，继续split
    for (let pair of pairs) {
      const [k, v] = pair.split('=');
      // 解码参数名和参数值
      const decodedKey = decodeURIComponent(k);
      const decodedValue = v ? decodeURIComponent(v) : '';

      if (decodedKey === key) {
        return decodedValue;
      }
    }

    return null;
  } catch (error) {
    console.error('解析URL参数出错:', error);
    return null;
  }
}

// 使用示例
const value = getParamValue('name');
console.log(value); // 例如：'John Doe'
```

## 更新 URL 参数

如果需要添加或更新 URL 参数，可以使用以下方法：

```typescript
/**
 * 添加或更新URL参数
 *
 * @param url 要添加或更新参数的URL
 * @param params 要添加或更新的参数对象，键为参数名，值为参数值
 * @returns 返回更新后的URL字符串
 * @throws 当提供的URL无效时，抛出异常
 */
export function addOrUpdateUrlParams(
  url: string,
  params: Record<string, any>,
): string {
  try {
    // 处理相对URL
    const baseUrl = url.startsWith('http') ? url : window.location.origin + url;
    const urlObj = new URL(baseUrl);

    // 遍历参数对象
    for (const [key, value] of Object.entries(params)) {
      if (value === null || value === undefined) {
        // 如果值为null或undefined，删除该参数
        urlObj.searchParams.delete(key);
      } else {
        // 将值转换为字符串并编码
        const stringValue = String(value);
        urlObj.searchParams.set(key, encodeURIComponent(stringValue));
      }
    }

    // 返回更新后的URL
    return urlObj.toString();
  } catch (error) {
    console.error('Invalid URL provided:', error);
    throw new Error('Invalid URL');
  }
}

// 使用示例
const originalUrl = 'https://example.com?name=John';
const updatedUrl = addOrUpdateUrlParams(originalUrl, {
  name: 'Jane',
  age: 25,
  active: true,
  empty: null,
  special: 'Hello & World!',
});
console.log(updatedUrl); // 'https://example.com?name=Jane&age=25&active=true&special=Hello%20%26%20World!'
```
