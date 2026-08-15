---
name: design-studio
description: >-
  AI Agent 设计工作室技能库：覆盖设计系统提取与构建、UI 视觉一致性审查、WCAG 2.2
  无障碍审计、Framer Motion 动效实现四大能力，让独立开发者也能产出专业级界面。触发词："设计系统"、"提取设计"、"Tailwind
  v4"、"UI 审查"、"视觉回归"、"对比设计稿"、"无障碍"、"WCAG"、"对比度"、"ARIA"、"键盘导航"、"Framer
  Motion"、"页面过渡"、"手势动画"、"动效"、"微交互"。
agent_created: true
metadata:
  version: 1.0.0
  category: UI/UX 设计
  difficulty: 进阶
  platform: skills-repo
  created: 2026-07-26
  updated: 2026-08-15
  architecture: superpower
tags:
  - UI/UX
  - design-system
  - accessibility
  - motion-design
  - ui-review
---

# Design Studio 设计工作室

> 把 AI 编程助手变成一名覆盖「设计系统 → 界面实现 → 审查迭代 → 无障碍检查 → 动效打磨」全链路的设计搭档。本技能采用 superpower 架构：`SKILL.md` 只做路由，深层方法论放在 `references/`，细粒度能力放在 `skills/` 子技能，按需加载、互不干扰。

## 何时使用

- 想从竞品网站**提取设计基元**、搭建或迁移 **Tailwind v4 设计系统**
- 需要**审查 UI 一致性**、对比设计稿与实现、发现视觉回归
- 需要做 **WCAG 2.2 无障碍审计**、为组件加 ARIA / 键盘导航
- 需要用 **Framer Motion** 实现页面过渡、手势、滚动动效

## 能力索引（超级技能路由）

| 任务 | 读取 / 调用 | 关键词（grep 线索） |
|------|------------|---------------------|
| 设计系统基础方法论 | `references/design-system-foundations.md` | token, Tailwind v4, 主题切换, 暗色模式, 提取, 间距节奏 |
| UI 视觉审查方法论 | `references/ui-review-checklist.md` | 对比度, 审查清单, 视觉回归, 截图, Playwright, 严重级 |
| 设计系统提取与构建 | `skills/design-system/SKILL.md` | design-system, 设计系统, token, Tailwind v4, 主题切换 |
| UI 视觉一致性审查 | `skills/ui-review/SKILL.md` | ui-review, 视觉审查, 对比设计稿, 颜色偏差, 布局错位 |
| WCAG 2.2 无障碍审计与实现 | `skills/accessibility/SKILL.md` | accessibility, WCAG, 对比度, ARIA, 键盘导航 |
| Framer Motion 动效实现 | `skills/motion-design/SKILL.md` | motion-design, framer-motion, 页面过渡, 手势, 滚动动画 |

> 路由规则：先判断任务属于「系统搭建 / 视觉审查 / 无障碍 / 动效」哪一类，再直接调对应 `skills/` 子技能；需要先建立整体规范时读 `references/` 中的 playbook。

## 细粒度子技能（可单独安装）

| 子技能 | 路径 | 适用 |
|--------|------|------|
| design-system | `skills/design-system` | 网站提取 token、Tailwind v4 设计系统、暗色模式 |
| ui-review | `skills/ui-review` | 布局/颜色/字体一致性审查、设计稿对比、视觉回归 |
| accessibility | `skills/accessibility` | WCAG 2.2 审计、ARIA、跨平台语义、键盘焦点 |
| motion-design | `skills/motion-design` | Framer Motion 入场/手势/滚动/编排动画 |

## 适用场景

- 从零搭建新项目的设计体系，或 Tailwind v3 → v4 迁移
- 上线前的 UI 质量门禁与多设备一致性检查
- 面向所有用户的无障碍合规（目标 WCAG 2.2 AA）
- 用声明式动画提升 React 应用的交互质感

## 限制

- 设计提取适合初始化参考，不是像素级复刻，不覆盖完整组件库
- 视觉审查不替代 Percy / Chromatic 等专业视觉回归工具
- 无障碍审计不替代 axe-core / Lighthouse 与法律合规建议
- 动效仅限 React 生态（`framer-motion`），不涉及 Canvas/WebGL 与 iOS/Android 原生动效
