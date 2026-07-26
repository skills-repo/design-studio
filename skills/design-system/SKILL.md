---
name: design-system
description: 从网站提取设计基元生成 token 文件，Tailwind v4 设计系统构建
source:
  type: derived
  repo: skills-repo/design-studio
  path: skills/design-system/SKILL.md
  version: 1.0.0
  updated: 2026-07-26
  url: https://skills.sh/arvindrk/extract-design-system/extract-design-system
metadata:
  category: 设计系统
  platform: Web
  difficulty: 入门
---

# 设计系统提取与构建

> 从公开网站反向提取设计基元，生成项目可用的 token 文件和 Tailwind v4 设计系统。

## 能力

- **设计提取**：从网站自动提取颜色、字体、间距、圆角、阴影等设计基元
- **Token 生成**：输出 `tokens.json`、`tokens.css` 供项目直接使用
- **Tailwind v4 设计系统**：CSS-first 配置、语义化 token、暗色模式、响应式变体
- **主题切换**：CSS 自定义属性驱动，支持明暗主题无缝切换

## 使用方式

```
/design-system 从 https://example.com 提取设计系统
/design-system 为我的项目创建一套 Tailwind v4 设计 token
/design-system 给这个设计系统添加暗色模式
```

## 工作流

1. 确认目标网站 URL 可公开访问
2. 运行 `npx extract-design-system <url>` 提取设计基元
3. 审查 `.extract-design-system/normalized.json` 中的颜色、字体、间距
4. 基于提取结果或用户需求，生成 Tailwind v4 `@theme` 配置
5. 输出 `tokens.json`、`tokens.css` 到项目目录

## 适用场景

- 从竞品网站提取设计参考
- 新项目快速搭建设计系统
- 已有项目从 Tailwind v3 迁移到 v4
- 统一团队的设计 token 规范

## 限制

- 提取结果适合初始化，不是像素级复刻
- 动态网站可能提取不完整
- 不覆盖完整组件库（仅 token 层面）
- 不要用提取结果覆盖已有设计系统