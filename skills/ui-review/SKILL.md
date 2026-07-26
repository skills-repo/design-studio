---
name: ui-review
description: UI 一致性和视觉回归审查，从设计稿到代码的对比检查
source:
  type: derived
  repo: skills-repo/design-studio
  path: skills/ui-review/SKILL.md
  version: 1.0.0
  updated: 2026-07-26
  url: https://skills.sh/minimax-ai/skills/vision-analysis
metadata:
  category: 审查
  platform: Web
  difficulty: 入门
---

# UI 视觉审查

> 基于视觉分析检查 UI 一致性，发现布局错位、颜色偏差、交互不一致和视觉层次问题。

## 能力

- **布局审查**：检测元素对齐、间距不一致、响应式断点问题
- **颜色检查**：对比度验证、品牌色一致性、主题变量使用
- **交互一致性**：hover/active/disabled 状态完整性检查
- **视觉层次**：字体层级、间距节奏、信息密度评估
- **跨页面对比**：多页面 UI 模式一致性审查

## 使用方式

```
/ui-review 检查这个页面的 UI 一致性问题
/ui-review 对比设计稿和实现的差异
/ui-review 审查这个组件库的所有状态是否完整
```

## 工作流

1. 提供页面截图或 URL
2. AI 逐区域分析布局、颜色、字体、间距
3. 标注不一致的位置和偏离程度
4. 输出问题分级报告（严重/一般/建议）
5. 提供具体修复建议和代码

## 适用场景

- 上线前 UI 质量检查
- 设计稿与实现对比审查
- 组件库所有状态完整性验证
- 多浏览器/多设备 UI 一致性检查

## 限制

- 不替代专业视觉回归测试工具（如 Percy、Chromatic）
- 不涉及动画和交互时序的精确测量
- 品牌策略层面的设计评审不在范围内