---
title: 瀑布布局
order: 2
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 瀑布布局

瀑布布局是前端开发中常见的布局方式，特别适合展示卡片式内容，如小红书首页的瀑布流布局。以下是两种处理高度不一致内容的瀑布布局实现方案。

## 1. CSS Columns 实现

使用 CSS Columns 可以自动平衡内容，适合内容高度不一致的场景。

```jsx
/**
 * defaultShowCode: true
 */
import React from 'react';
import './demo1.less';

export default () => {
  const cards = [
    {
      image: 'https://picsum.photos/400/300?random=5',
      title: '卡片标题1',
      desc: '这是一段非常长的描述文本，详细介绍了卡片的内容和特点。这里可以包含更多的信息，比如产品的详细规格、使用说明、注意事项等。这样的长文本可以更好地展示不同布局方案的特点。同时，我们还可以添加更多的内容来测试布局的适应性。',
    },
    {
      image: 'https://picsum.photos/400/300?random=6',
      title: '卡片标题2',
      desc: '短描述。',
    },
    {
      image: 'https://picsum.photos/400/300?random=7',
      title: '卡片标题3',
      desc: '这是一段中等长度的描述文本，介绍了一些基本的内容和特点。这里可以包含一些简单的说明。',
    },
    {
      image: 'https://picsum.photos/400/300?random=8',
      title: '卡片标题4',
      desc: '这是一段非常长的描述文本，详细介绍了卡片的内容和特点。这里可以包含更多的信息，比如产品的详细规格、使用说明、注意事项等。这样的长文本可以更好地展示不同布局方案的特点。同时，我们还可以添加更多的内容来测试布局的适应性。最后再补充一些额外的信息。',
    },
  ];

  // 分成左右两列
  const left = cards.filter((_, i) => i % 2 === 0);
  const right = cards.filter((_, i) => i % 2 === 1);

  return (
    <div className="columns-layout-container">
      <div className="columns-column">
        {left.map((card, idx) => (
          <div key={idx} className="columns-card">
            <img src={card.image} alt={card.title} />
            <h3>{card.title}</h3>
            <p>{card.desc}</p>
          </div>
        ))}
      </div>
      <div className="columns-column">
        {right.map((card, idx) => (
          <div key={idx} className="columns-card">
            <img src={card.image} alt={card.title} />
            <h3>{card.title}</h3>
            <p>{card.desc}</p>
          </div>
        ))}
      </div>
    </div>
  );
};
```

### 特点

- 自动平衡内容
- 适合高度不一致的内容
- 实现简单
- 兼容性好

### 工作原理

1. 使用 `column-count` 定义列数
2. 使用 `column-gap` 控制列间距
3. 内容会自动分配到各列中

## 2. JavaScript 瀑布流实现

使用 JavaScript 实现瀑布流布局，可以更精确地控制每个卡片的位置。

```jsx
/**
 * defaultShowCode: true
 */
import React, { useEffect, useRef, useState } from 'react';
import './demo2.less';

export default () => {
  const containerRef = useRef(null);
  const [cards, setCards] = useState([
    {
      image: 'https://picsum.photos/400/300?random=9',
      title: '卡片标题1',
      desc: '短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。',
    },
    {
      image: 'https://picsum.photos/400/300?random=10',
      title: '卡片标题2',
      desc: '这是一段非常长的描述文本，详细介绍了卡片的内容和特点。这里可以包含更多的信息，比如产品的详细规格、使用说明、注意事项等。这样的长文本可以更好地展示不同布局方案的特点。',
    },
    {
      image: 'https://picsum.photos/400/300?random=11',
      title: '卡片标题3',
      desc: '这是一段中等长度的描述文本，介绍了一些基本的内容和特点。',
    },
    {
      image: 'https://picsum.photos/400/300?random=12',
      title: '卡片标题4',
      desc: '这是一段非常长的描述文本，详细介绍了卡片的内容和特点。这里可以包含更多的信息，比如产品的详细规格、使用说明、注意事项等。这样的长文本可以更好地展示不同布局方案的特点。同时，我们还可以添加更多的内容来测试布局的适应性。最后再补充一些额外的信息。',
    },
  ]);

  useEffect(() => {
    const container = containerRef.current;
    const columns = Array.from({ length: 2 }, () =>
      document.createElement('div'),
    );

    // 设置列样式
    columns.forEach((column, index) => {
      column.className = 'waterfall-column';
      container.appendChild(column);
    });

    // 分配卡片到最短的列
    cards.forEach((card) => {
      const cardElement = document.createElement('div');
      cardElement.className = 'waterfall-card';
      cardElement.innerHTML = `
        <img src="${card.image}" alt="${card.title}" />
        <h3>${card.title}</h3>
        <p>${card.desc}</p>
      `;

      // 找到最短的列
      const shortestColumn = columns.reduce((min, col) =>
        col.offsetHeight < min.offsetHeight ? col : min,
      );

      shortestColumn.appendChild(cardElement);
    });

    // 清理函数
    return () => {
      columns.forEach((column) => column.remove());
    };
  }, [cards]);

  return <div ref={containerRef} className="waterfall-layout-container" />;
};
```

### 特点

- 精确控制布局
- 支持动态加载
- 性能优化空间大
- 适合复杂场景

### 工作原理

1. 创建固定数量的列容器
2. 计算每列当前高度
3. 将新卡片添加到最短的列中
4. 监听窗口大小变化，重新计算布局

## 使用场景

1. CSS Columns: 内容高度不一致，需要自动平衡
2. JavaScript 瀑布流: 复杂的动态加载场景，需要精确控制

## 注意事项

1. 响应式设计
   - 小屏幕下切换为单列
   - 考虑不同设备的显示效果
2. 性能优化
   - 图片懒加载
   - 虚拟滚动
   - 防抖处理
3. 内容加载
   - 预加载策略
   - 加载状态处理
   - 错误处理

## 最佳实践

1. 选择合适的实现方案
   - 简单场景使用 CSS Columns
   - 复杂场景使用 JavaScript 瀑布流
2. 优化性能
   - 使用图片懒加载
   - 实现虚拟滚动
   - 添加加载动画
3. 提升用户体验
   - 添加过渡动画
   - 优化加载状态
   - 处理错误情况
4. 代码维护
   - 模块化设计
   - 添加注释
   - 考虑扩展性
