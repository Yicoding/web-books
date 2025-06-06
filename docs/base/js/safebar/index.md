---
title: 安全底栏
order: 1
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 安全底栏

安全底栏（Safe Bottom Bar）是一个用于检测移动端是否存在底部安全区域的工具，主要用于判断 iPhone X 及以上机型是否具有底部安全区域。

## 功能特点

- 自动检测设备是否具有底部安全区域
- 支持 iOS 和 Android 设备
- 简单易用的 API

## 使用方法

```js
// 方案一：基于CSS特性和屏幕尺寸检测
const hasSafeArea1 = checkSafeBottomArea();
console.log('方案一检测结果:', hasSafeArea1);

// 方案二：基于屏幕长宽比检测
const hasSafeArea2 = hasSafeArea();
console.log('方案二检测结果:', hasSafeArea2);
```

## 实现代码

### 方案一：基于 CSS 特性和屏幕尺寸检测

```js
function checkSafeBottomArea() {
  // 检测是否支持 env() 函数
  if (window.CSS && window.CSS.supports) {
    // 检测是否支持 safe-area-inset-bottom
    if (window.CSS.supports('height: env(safe-area-inset-bottom)')) {
      // 创建临时元素检测安全区域高度
      const temp = document.createElement('div');
      temp.style.cssText = 'height: env(safe-area-inset-bottom)';
      document.body.appendChild(temp);
      const height = parseInt(getComputedStyle(temp).height);
      document.body.removeChild(temp);

      // 如果高度大于0，说明存在安全区域
      return height > 0;
    }
  }

  // 检测是否是 iPhone X 及以上机型
  const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent);
  if (isIOS) {
    const screenHeight = window.screen.height;
    const screenWidth = window.screen.width;
    // iPhone X 及以上机型的屏幕尺寸
    const iPhoneXHeight = 812;
    const iPhoneXMaxHeight = 896;
    return screenHeight === iPhoneXHeight || screenHeight === iPhoneXMaxHeight;
  }

  return false;
}
```

### 方案二：基于屏幕长宽比检测

```js
function hasSafeArea() {
  // Android 设备通常不需要安全区域处理
  if (deviceType === 'android') return false;

  // 通过屏幕长宽比判断
  const aspectRatio = window?.screen?.height / window?.screen?.width;
  return aspectRatio > 2;
}
```

## 实现原理

### 方案一原理

1. 使用 `env(safe-area-inset-bottom)` 检测底部安全区域高度
2. 通过屏幕尺寸判断是否是 iPhone X 及以上机型
3. 根据检测结果返回布尔值

### 方案二原理

1. 首先排除 Android 设备（大部分 Android 设备不需要安全区域处理）
2. 计算屏幕的长宽比（高度/宽度）
3. 具有安全区域的设备通常屏幕长宽比大于 2（如 iPhone X 系列）
4. 通过长宽比阈值判断是否存在安全区域

## 注意事项

1. 需要在 HTML 头部添加 viewport meta 标签：

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0, viewport-fit=cover"
/>
```

2. 在 iOS 设备上，需要设置 `viewport-fit=cover` 才能正确获取安全区域高度

## 兼容性

- iOS 11.0+
- Android 8.0+
- 现代浏览器

## 最佳实践

1. 在页面加载时进行检测
2. 根据检测结果设置相应的样式
3. 考虑横屏模式下的适配
4. 测试不同机型的显示效果
