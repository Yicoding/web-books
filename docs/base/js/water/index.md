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

瀑布布局是前端开发中常见的布局方式，特别适合展示卡片式内容，如小红书首页的瀑布流布局。以下是使用 JavaScript 实现瀑布流布局的方案。

## JavaScript 瀑布流实现

使用 JavaScript 实现瀑布流布局，可以更精确地控制每个卡片的位置。

```jsx
/**
 * defaultShowCode: true
 */
import React, { useEffect, useRef, useState, useCallback } from 'react';
import './demo1.less';

export default () => {
  const columnRefs = [useRef(null), useRef(null)];
  const [cards] = useState([
    {
      image: 'https://picsum.photos/400/600?random=9',
      title: '卡片标题1',
      desc: '短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。短描述。',
    },
    {
      image: 'https://picsum.photos/400/600?random=10',
      title: '卡片标题2',
      desc: '这是一段非常长的描述文本，详细介绍了卡片的内容和特点。这里可以包含更多的信息，比如产品的详细规格、使用说明、注意事项等。这样的长文本可以更好地展示不同布局方案的特点。',
    },
    {
      image: 'https://picsum.photos/400/600?random=11',
      title: '卡片标题3',
      desc: '这是一段中等长度的描述文本，介绍了一些基本的内容和特点。',
    },
    {
      image: 'https://picsum.photos/400/600?random=12',
      title: '卡片标题4',
      desc: '这是一段非常长的描述文本，详细介绍了卡片的内容和特点。这里可以包含更多的信息，比如产品的详细规格、使用说明、注意事项等。这样的长文本可以更好地展示不同布局方案的特点。同时，我们还可以添加更多的内容来测试布局的适应性。最后再补充一些额外的信息。',
    },
    {
      image: 'https://picsum.photos/400/600?random=13',
      title: '卡片标题5',
      desc: '这是一段中等长度的描述文本，介绍了一些基本的内容和特点。这里可以包含一些简单的说明，让用户快速了解主要内容。同时也可以添加一些补充信息，使描述更加完整。',
    },
    {
      image: 'https://picsum.photos/400/600?random=14',
      title: '卡片标题6',
      desc: '这是一段较短的描述文本，简明扼要地介绍了主要内容。适合快速浏览和了解核心信息。',
    },
    {
      image: 'https://picsum.photos/400/600?random=15',
      title: '卡片标题7',
      desc: '这是一段较短的描述文本，简明扼要地介绍了主要内容。适合快速浏览和了解核心信息。',
    },
  ]);

  const [leftCards, setLeftCards] = useState([]);
  const [rightCards, setRightCards] = useState([]);
  const [isRebalanced, setIsRebalanced] = useState(false);

  // 处理图片加载完成
  const handleImageLoad = useCallback(() => {
    // 图片加载完成时不需要特殊处理，由Promise.allSettled统一管理
  }, []);

  // 重新计算并调整布局
  const rebalanceLayout = useCallback(() => {
    // 获取当前两列的实际高度
    const leftHeight = columnRefs[0].current?.offsetHeight || 0;
    const rightHeight = columnRefs[1].current?.offsetHeight || 0;

    console.log('重新平衡前 - 左列高度:', leftHeight, '右列高度:', rightHeight);

    // 将所有卡片重新分配
    const allCards = [...leftCards, ...rightCards].sort(
      (a, b) => a.originalIndex - b.originalIndex,
    );
    const newLeft = [];
    const newRight = [];
    let tempLeftHeight = 0;
    let tempRightHeight = 0;

    allCards.forEach((card) => {
      // 选择较短的列
      if (tempLeftHeight <= tempRightHeight) {
        newLeft.push(card);
        // 获取这个卡片的实际高度并累加
        const cardElement = document.querySelector(
          `[data-card-index="${card.originalIndex}"]`,
        );
        const cardHeight = cardElement?.offsetHeight || 400;
        tempLeftHeight += cardHeight;
      } else {
        newRight.push(card);
        const cardElement = document.querySelector(
          `[data-card-index="${card.originalIndex}"]`,
        );
        const cardHeight = cardElement?.offsetHeight || 400;
        tempRightHeight += cardHeight;
      }
    });

    setLeftCards(newLeft);
    setRightCards(newRight);
    setIsRebalanced(true);

    console.log(
      '重新平衡后 - 左列卡片数:',
      newLeft.length,
      '右列卡片数:',
      newRight.length,
    );
  }, [leftCards, rightCards]);

  // 等待所有图片加载完成的Promise
  const waitForAllImages = useCallback(async () => {
    const imagePromises = cards.map((card) => {
      return new Promise((resolve) => {
        const img = new Image();
        img.onload = () => resolve({ success: true, src: card.image });
        img.onerror = () => resolve({ success: false, src: card.image });
        img.src = card.image;
      });
    });

    await Promise.allSettled(imagePromises);
    console.log('所有图片加载完成，开始重新平衡布局');
    rebalanceLayout();
  }, [cards, rebalanceLayout]);

  // 初始交替分配
  useEffect(() => {
    if (!isRebalanced) {
      const left = cards
        .filter((_, index) => index % 2 === 0)
        .map((card, index) => ({ ...card, originalIndex: index * 2 }));
      const right = cards
        .filter((_, index) => index % 2 === 1)
        .map((card, index) => ({ ...card, originalIndex: index * 2 + 1 }));

      setLeftCards(left);
      setRightCards(right);

      // 开始等待所有图片加载
      waitForAllImages();
    }
  }, [cards, isRebalanced, waitForAllImages]);

  const Card = ({ card, onImageLoad }) => (
    <div className="waterfall-card" data-card-index={card.originalIndex}>
      <img
        src={card.image}
        alt={card.title}
        onLoad={onImageLoad}
        onError={onImageLoad}
        style={{ width: '100%', height: 'auto' }}
      />
      <h3>{card.title}</h3>
      <p>{card.desc}</p>
    </div>
  );

  return (
    <div className="waterfall-layout-container">
      <div ref={columnRefs[0]} className="waterfall-column">
        {leftCards.map((card, cardIndex) => (
          <Card
            key={`left-${cardIndex}`}
            card={card}
            onImageLoad={handleImageLoad}
          />
        ))}
      </div>
      <div ref={columnRefs[1]} className="waterfall-column">
        {rightCards.map((card, cardIndex) => (
          <Card
            key={`right-${cardIndex}`}
            card={card}
            onImageLoad={handleImageLoad}
          />
        ))}
      </div>
    </div>
  );
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

JavaScript 瀑布流: 复杂的动态加载场景，需要精确控制

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
