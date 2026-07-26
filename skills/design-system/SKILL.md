---
name: design-system
description: 构建 CSS 变量体系、组件 token、主题切换，输出可执行的设计系统代码
source:
  type: original
  repo: skills-repo/design-studio
  path: skills/design-system/SKILL.md
  version: 1.0.0
  updated: 2026-07-26
metadata:
  category: 设计系统
  platform: Web
  difficulty: 进阶
---

# 设计系统构建器

> 从零搭建可用的设计系统：颜色、间距、排版、圆角、阴影、组件 token、主题切换。

## 能力

- **Token 体系**：颜色/间距/排版/圆角/阴影的设计 token 定义
- **CSS 变量方案**：生成 `:root` 变量体系，支持 Tailwind 集成
- **主题切换**：明暗主题、品牌主题、用户自定义主题
- **组件级 token**：按钮、输入框、卡片等组件的专属 token
- **一致性检查**：扫描项目，标记偏离设计系统的样式

## 使用方式

在 Claude Code 中使用 `/design-system` 调用。

```
/design-system 为这个 SaaS 项目创建一套设计系统
/design-system 检查哪些组件样式不一致
```

## 工作流

1. 分析项目当前的样式分布（颜色、间距、字体大小）
2. 提取和规范化设计 token
3. 生成 CSS 变量文件（`:root` 明暗主题）
4. 为 5-8 个核心组件定义组件级 token
5. 输出 Tailwind 配置文件（如需要）

## 适用场景

- 新项目需要统一的设计基础
- 旧项目样式碎片化需要整理
- 多个项目间需要共享设计系统
- 为组件库准备 token 层

## 限制

- 不生成 Figma 设计文件
- 不涉及品牌策略和视觉定位
- 不输出完整组件库代码（仅 token 层）