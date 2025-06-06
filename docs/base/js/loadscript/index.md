---
title: 动态加载脚本
order: 3
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 动态加载脚本

## 动态加载 JS

```ts | pure
/**
 * 异步加载脚本
 * @param url 脚本地址
 * @returns Promise
 */
export function loadScript(url: string) {
  return new Promise((resolve, reject) => {
    window.addEventListener('load', () => {
      const script = document.createElement('script');
      script.type = 'text/javascript';
      script.async = true;
      script.onload = () => resolve(true);
      script.onerror = () => reject();
      script.src = url;
      document.body.appendChild(script);
    });
  });
}
```

## 动态加载 CSS

```ts | pure
/**
 * 异步加载CSS
 * @param url CSS文件地址
 * @returns Promise
 */
export function loadCSS(url: string) {
  return new Promise((resolve, reject) => {
    const link = document.createElement('link');
    link.rel = 'stylesheet';
    link.type = 'text/css';
    link.href = url;
    link.onload = () => resolve(true);
    link.onerror = () => reject();
    document.head.appendChild(link);
  });
}
```

## 动态加载 iframe

```ts | pure
/**
 * 创建隐藏的iframe用于URL Scheme拦截
 * @param url 需要拦截的URL Scheme
 * @returns Promise
 */
export function createHiddenIframe(url: string) {
  return new Promise((resolve, reject) => {
    const iframe = document.createElement('iframe');
    iframe.style.display = 'none';
    iframe.style.width = '0';
    iframe.style.height = '0';
    iframe.style.position = 'absolute';
    iframe.style.left = '-9999px';
    iframe.style.top = '-9999px';

    // 设置超时处理
    const timeout = setTimeout(() => {
      document.body.removeChild(iframe);
      reject(new Error('URL Scheme 拦截超时'));
    }, 3000);

    iframe.onload = () => {
      clearTimeout(timeout);
      document.body.removeChild(iframe);
      resolve(true);
    };

    iframe.onerror = () => {
      clearTimeout(timeout);
      document.body.removeChild(iframe);
      reject(new Error('URL Scheme 拦截失败'));
    };

    iframe.src = url;
    document.body.appendChild(iframe);
  });
}
```

## 动态加载图片

```ts | pure
/**
 * 异步加载图片
 * @param url 图片地址
 * @param options 图片配置项
 * @returns Promise
 */
export function loadImage(
  url: string,
  options: {
    width?: string;
    height?: string;
    alt?: string;
    loading?: 'lazy' | 'eager';
    decoding?: 'async' | 'sync' | 'auto';
  } = {},
) {
  return new Promise((resolve, reject) => {
    const img = new Image();
    img.src = url;
    img.onload = () => resolve(true);
    img.onerror = () => reject();

    // 设置图片属性
    if (options.width) img.width = parseInt(options.width);
    if (options.height) img.height = parseInt(options.height);
    if (options.alt) img.alt = options.alt;
    if (options.loading) img.loading = options.loading;
    if (options.decoding) img.decoding = options.decoding;

    document.body.appendChild(img);
  });
}
```

## 使用示例

```ts
// 加载JS
loadScript('https://example.com/script.js')
  .then(() => console.log('JS加载成功'))
  .catch(() => console.error('JS加载失败'));

// 加载CSS
loadCSS('https://example.com/style.css')
  .then(() => console.log('CSS加载成功'))
  .catch(() => console.error('CSS加载失败'));

// 使用隐藏iframe拦截URL Scheme
createHiddenIframe('weixin://dl/business/?t=xxx')
  .then(() => console.log('URL Scheme 拦截成功'))
  .catch((error) => console.error('URL Scheme 拦截失败:', error));

// 加载图片
loadImage('https://example.com/image.jpg', {
  width: '300',
  height: '200',
  alt: '示例图片',
  loading: 'lazy',
})
  .then(() => console.log('图片加载成功'))
  .catch(() => console.error('图片加载失败'));
```

## 注意事项

1. 动态加载资源时，建议添加错误处理机制
2. 对于关键资源，可以考虑添加超时处理
3. 使用 `loading="lazy"` 可以实现资源的懒加载
4. 动态加载的资源可能会影响页面性能，请合理使用
5. 使用隐藏 iframe 拦截 URL Scheme 时，建议设置超时处理，避免 iframe 长期存在
6. URL Scheme 拦截主要用于唤起原生应用，如微信、支付宝等
