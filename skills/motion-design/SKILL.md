---
name: motion-design
description: Framer Motion 动画与微交互：页面过渡、手势、滚动动画、编排序列
source:
  type: derived
  repo: skills-repo/design-studio
  path: skills/motion-design/SKILL.md
  version: 1.0.0
  updated: 2026-07-26
  url: https://skills.sh/patricio0312rev/skills/framer-motion-animator
metadata:
  category: 动效
  platform: Web
  difficulty: 进阶
---

# Framer Motion 动画与微交互

> 使用 Framer Motion 声明式 API 构建流畅动画和微交互，覆盖页面过渡、手势、滚动驱动动画。

## 能力

- **入场/出场动画**：opacity、scale、position、rotation 的 animate 和 exit
- **手势交互**：whileHover、whileTap、whileDrag、whileFocus
- **页面过渡**：AnimatePresence 实现路由切换动画
- **滚动驱动**：useScroll + useTransform 实现视差和滚动触发
- **编排序列**：staggerChildren、delayChildren、when 控制动画时序
- **性能优化**：GPU 加速属性优先（transform、opacity）

## 使用方式

```
/motion-design 给这个 Modal 添加淡入淡出动画
/motion-design 设计一个列表项的 stagger 入场效果
/motion-design 这个按钮的 hover 动效不够流畅，帮我优化
```

## 工作流

1. 识别动画需求：入场/退场/hover/手势/滚动
2. 选择动画类型：简单动画 / variants / 手势 / layout
3. 定义 motion 属性：opacity、scale、y、rotate
4. 配置 transition：duration、ease、spring 物理参数
5. 编排序列：父容器 staggerChildren + delayChildren
6. 性能检查：优先使用 transform 和 opacity（GPU 加速）

## 适用场景

- 页面路由切换动画
- 列表项交错入场
- Modal/Drawer/Toast 进出动画
- 拖拽和手势交互
- 滚动视差效果

## 限制

- 仅支持 React 生态（需 `framer-motion` 包）
- 复杂物理动画建议使用 react-spring 或 GSAP
- 不涉及 Canvas/WebGL 动画
- 不涉及 iOS/Android 原生动效（SwiftUI matchedGeometry / Compose animateAsState）