---
title: 页面离开挽留
order: 2
toc: content
group:
  title: js
  order: 2
nav:
  title: 基础
  order: 1
---

# 页面离开挽留

页面离开挽留是一种防止用户意外关闭页面或离开当前页面的技术，常用于表单填写、文档编辑等重要操作场景。

```jsx
/**
 * defaultShowCode: true
 */
import React, { useState, useEffect } from 'react';
import './demo1.less';

export default () => {
  const [formData, setFormData] = useState('');
  const [hasUnsavedChanges, setHasUnsavedChanges] = useState(false);

  useEffect(() => {
    const handleBeforeUnload = (event) => {
      if (hasUnsavedChanges) {
        event.preventDefault();
        event.returnValue = '';
        return '';
      }
    };

    if (hasUnsavedChanges) {
      window.addEventListener('beforeunload', handleBeforeUnload);
    }

    return () => {
      window.removeEventListener('beforeunload', handleBeforeUnload);
    };
  }, [hasUnsavedChanges]);

  const handleInput = (value) => {
    setFormData(value);
    setHasUnsavedChanges(value.trim().length > 0);
  };

  const handleSave = () => {
    console.log('保存数据:', formData);
    setHasUnsavedChanges(false);
    alert('保存成功！');
  };

  const handleReset = () => {
    if (hasUnsavedChanges && !confirm('有未保存的更改，确定要重置吗？')) {
      return;
    }
    setFormData('');
    setHasUnsavedChanges(false);
  };

  return (
    <div className="retain-demo-container">
      <h3>页面离开挽留示例</h3>

      <textarea
        value={formData}
        onChange={(e) => handleInput(e.target.value)}
        placeholder="输入一些内容，然后尝试关闭页面或点击重置..."
        className="retain-demo-textarea"
      />

      <div className="retain-demo-button-group">
        <button onClick={handleSave} className="retain-demo-button save">
          保存
        </button>
        <button onClick={handleReset} className="retain-demo-button reset">
          重置
        </button>
      </div>

      <p className="retain-demo-status">
        状态: {hasUnsavedChanges ? '有未保存的更改 ⚠️' : '已保存 ✅'}
      </p>
    </div>
  );
};
```

## 注意事项

- 现代浏览器不允许自定义提示信息，只能显示默认确认对话框
- 移动端浏览器对 `beforeunload` 支持有限
- 只在真正有未保存数据时启用，避免过度提醒
