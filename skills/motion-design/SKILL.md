---
name: motion-design
description: CSS/JS 动画与微交互设计，生成流畅的过渡效果和交互动效代码
source:
  type: original
  repo: skills-repo/design-studio
  path: skills/motion-design/SKILL.md
  version: 1.0.0
  updated: 2026-07-26
metadata:
  category: 动效
  platform: Web
  difficulty: 进阶
---

# 动效设计

> 为 Web 界面设计流畅的过渡动画和微交互，输出可直接使用的 CSS/JS 代码。

## 能力

- **过渡动画**：hover、focus、展开/收起等状态过渡
- **入场动画**：页面加载、滚动进入、列表项依次出现
- **微交互**：按钮反馈、表单验证、加载状态动效
- **性能优化**：使用 `transform`/`opacity` 确保 60fps
- **偏好尊重**：检测 `prefers-reduced-motion`，提供降级方案

## 使用方式

在 Claude Code 中使用 `/motion-design` 调用。

```
/motion-design 为这个按钮添加点击反馈动画
/motion-design 给这个页面设计滚动入场效果
```

## 工作流

1. 描述需要动效的交互场景
2. AI 设计动效方案（时长、缓动、触发条件）
3. 输出 CSS animation/transition 或 JS 代码
4. 确保包含 `prefers-reduced-motion` 降级
5. 给出性能注意事项

## 设计原则

- **200-300ms**：微交互最佳时长
- **ease-out**：入场用 ease-out，离场用 ease-in
- **一屏不超过 3 个动效焦点**：避免视觉噪音
- **动效要有目的**：引导注意、反馈操作、过渡状态

## 适用场景

- 产品页面缺乏交互反馈
- 页面切换生硬需要过渡
- 关键操作需要视觉确认（如添加到购物车）
- 数据可视化需要动画引导

## 限制

- 不输出复杂 3D/WebGL 动画
- 不替代 After Effects/Lottie 工作流
- 品牌动画（Logo 动效）需要专业动效设计师