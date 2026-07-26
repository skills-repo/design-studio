# 设计工作室技能库

> AI Agent Skills for UI/UX Design —— 覆盖设计系统、界面审查、无障碍、动效设计

## 定位

为独立开发者和设计新手提供一套可安装的 AI Agent 设计技能，让 Claude Code 成为你的设计搭档。

## 核心理念

> 好的设计不是奢侈品，是产品的基本功。AI 帮你跨越设计门槛，一个人也能做出专业级界面。

- **系统化优先**——先建组件体系，再做页面，避免碎片化设计
- **无障碍内建**——可访问性不是事后检查，是设计的一部分
- **做减法**——帮你看哪些可以去掉，而不只是能加什么

## 技能清单

| 环节 | 技能 | 描述 | 来源 |
|------|------|------|------|
| 🏗️ 设计系统 | `design-system` | CSS 变量体系、组件 token、主题切换 | 原创 |
| 👁️ 界面审查 | `ui-review` | UI 一致性和可用性审查，发现布局/交互问题 | 原创 |
| ♿ 可访问性 | `accessibility` | WCAG 审查、颜色对比度、键盘导航、屏幕阅读器 | 原创 |
| 🎬 动效 | `motion-design` | CSS/JS 动画建议，过渡效果与微交互 | 原创 |

## 快速开始

```bash
npx skills add skills-repo/design-studio@design-system -g -y
npx skills add skills-repo/design-studio@ui-review -g -y
npx skills add skills-repo/design-studio@accessibility -g -y
npx skills add skills-repo/design-studio@motion-design -g -y
```

## 推荐工作流

```
设计系统 → 界面实现 → 审查迭代 → 无障碍检查 → 动效打磨
design-     ui-          ui-review    accessibility  motion-
system      review                                  design
```

## 许可

MIT