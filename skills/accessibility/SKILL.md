---
name: accessibility
description: WCAG 2.2 无障碍审计与实现，覆盖 Web/iOS/Android 跨平台语义化
source:
  type: derived
  repo: skills-repo/design-studio
  path: skills/accessibility/SKILL.md
  version: 1.0.0
  updated: 2026-07-26
  url: https://skills.sh/affaan-m/everything-claude-code/accessibility
metadata:
  category: 无障碍
  platform: 通用
  difficulty: 进阶
---

# 无障碍审计（WCAG 2.2）

> 确保数字产品对所有用户可感知、可操作、可理解、健壮（POUR），覆盖 Web、iOS 和 Android 平台。

## 能力

- **WCAG 2.2 审计**：对照最新标准检查颜色对比度、焦点可见性、目标尺寸（24px 最小）
- **语义化实现**：Web（ARIA + HTML5）、iOS（Accessibility Traits）、Android（Semantics）
- **焦点管理**：键盘导航顺序、可见焦点指示器（SC 2.4.11）
- **标签与提示**：`aria-label`、`accessibilityLabel`、`contentDescription` 跨平台对照
- **动态内容**：`aria-live` 区域，状态变更通知

## 使用方式

```
/accessibility 审计这个页面的 WCAG 2.2 合规性
/accessibility 为这个组件添加 ARIA 属性和键盘导航
/accessibility 检查这个 iOS 页面的辅助功能标注
```

## 工作流

1. 确定组件角色：优先使用原生语义元素
2. 检查可感知性：对比度 4.5:1（正文）/ 3:1（大文本/UI）、图片替代文本
3. 验证可操作性：24px 最小触控目标、键盘可达、焦点指示器可见
4. 确认可理解性：一致导航、描述性错误信息、避免重复输入
5. 测试健壮性：Name/Role/Value 模式、跨平台语义映射

## 适用场景

- WCAG 2.2 合规审计
- 组件无障碍标注（ARIA/SwiftUI/Compose）
- 屏幕阅读器适配验证
- 键盘导航和焦点管理优化

## 相关参考

- 对比度与焦点验收：`references/ui-review-checklist.md`（§3.2 可运行对比度脚本、§5 清单含对比度 ≥4.5:1 与焦点可见 SC 2.4.11）

## 限制

- 不替代专业无障碍审计工具（如 axe-core、Lighthouse）
- 不覆盖法律合规建议
- 不涉及手语或字幕等辅助内容制作