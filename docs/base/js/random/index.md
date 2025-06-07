---
title: 生成随机数
order: 6
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 生成随机数

在 JavaScript 中，有多种方法可以生成随机数。本文将介绍最常用的几种方法及其使用场景。

## Math.random()

`Math.random()` 是 JavaScript 中最常用的生成随机数的方法。它返回一个 [0, 1) 范围内的伪随机浮点数。

```javascript
// 生成 0 到 1 之间的随机数
const random = Math.random();
console.log(random); // 例如：0.123456789

// 生成指定范围内的随机整数
function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

// 生成 1 到 10 之间的随机整数
const randomInt = getRandomInt(1, 10);
console.log(randomInt); // 例如：7
```

## 生成 UUID

UUID（通用唯一标识符）是一个 128 位的标识符，通常用于唯一标识信息。在 JavaScript 中，推荐使用 uuid 库来生成 UUID：

```javascript
// 使用 uuid 库
import { v4 as uuidv4 } from 'uuid';

const uuid = uuidv4();
console.log(uuid); // 例如：'123e4567-e89b-12d3-a456-426614174000'
```

## 生成时间戳

在实际开发中，经常需要生成带有随机后缀的时间戳，可以这样实现：

```javascript
// 生成时间戳（毫秒）加上3位随机数
const timestamp = Date.now() + `00${getRandomInt(0, 100)}`.slice(-3);
console.log(timestamp); // 例如：1678234567123
```

## 注意事项

1. `Math.random()` 生成的是伪随机数，不适合用于安全相关的场景。
2. 对于需要生成唯一标识符的场景，推荐使用 uuid 库。
3. UUID 的格式为：8-4-4-4-12 个十六进制数字，例如：'123e4567-e89b-12d3-a456-426614174000'。
4. 时间戳加随机后缀的方式适合需要按时间排序且保证唯一性的场景。

## 浏览器兼容性

- `Math.random()`: 所有现代浏览器都支持
- uuid 库：支持所有现代浏览器和 Node.js 环境
- `Date.now()`: 所有现代浏览器都支持
