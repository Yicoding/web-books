---
title: 时间格式化
order: 8
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 时间格式化

使用原生 Date 对象进行日期时间格式化。

```typescript
/**
 * 格式化日期时间
 * @param date 要格式化的日期
 * @param format 格式化模板，支持 YYYY、MM、DD、HH、mm、SS，默认为 'YYYY-MM-DD HH:mm:SS'
 * @returns 格式化后的日期字符串
 */
export function formatDateTime(
  date: Date | string | number,
  format: string = 'YYYY-MM-DD HH:mm:SS',
): string {
  const dateObj = new Date(date);
  if (isNaN(dateObj.getTime())) {
    throw new Error('Invalid date');
  }

  const year = dateObj.getFullYear();
  const month = String(dateObj.getMonth() + 1).padStart(2, '0');
  const day = String(dateObj.getDate()).padStart(2, '0');
  const hours = String(dateObj.getHours()).padStart(2, '0');
  const minutes = String(dateObj.getMinutes()).padStart(2, '0');
  const seconds = String(dateObj.getSeconds()).padStart(2, '0');

  return format
    .replace(/YYYY/g, String(year))
    .replace(/MM/g, month)
    .replace(/DD/g, day)
    .replace(/HH/g, hours)
    .replace(/mm/g, minutes)
    .replace(/SS/g, seconds);
}
```

## 使用示例

```typescript
const now = new Date();

// 默认格式（完整时间）
console.log(formatDateTime(now));
// 输出: '2024-03-21 14:30:45'

// 各种灵活组合
console.log(formatDateTime(now, 'YYYY')); // 输出: '2024'
console.log(formatDateTime(now, 'MM-DD')); // 输出: '03-21'
console.log(formatDateTime(now, 'YYYY-MM')); // 输出: '2024-03'
console.log(formatDateTime(now, 'HH:mm')); // 输出: '14:30'
console.log(formatDateTime(now, 'MM-DD HH:mm')); // 输出: '03-21 14:30'
console.log(formatDateTime(now, 'YYYY年MM月DD日')); // 输出: '2024年03月21日'
```
