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
| 🏗️ 设计系统 | `design-system` | 从网站提取设计基元生成 token，Tailwind v4 设计系统 | [衍生](https://skills.sh/arvindrk/extract-design-system/extract-design-system) |
| 👁️ 界面审查 | `ui-review` | UI 一致性和视觉回归审查，设计稿到代码对比 | [衍生](https://skills.sh/minimax-ai/skills/vision-analysis) |
| ♿ 可访问性 | `accessibility` | WCAG 2.2 无障碍审计，覆盖 Web/iOS/Android 跨平台 | [衍生](https://skills.sh/affaan-m/everything-claude-code/accessibility) |
| 🎬 动效 | `motion-design` | Framer Motion 动画与微交互：页面过渡、手势、滚动 | [衍生](https://skills.sh/patricio0312rev/skills/framer-motion-animator) |

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

## 安装 / Install

整库安装（含全部 4 个子技能）与单技能安装命令如下，按需在终端执行：

```
npx skills add skills-repo/design-studio
npx skills add skills-repo/design-studio@design-system
```

> 把 `@design-system` 换成任意子技能目录名即可单独安装：`design-system`、`ui-review`、`accessibility`、`motion-design`。

## 子技能索引

| 子技能 | 说明 |
|--------|------|
| design-system | 从网站提取设计基元，生成 token 与 Tailwind v4 设计系统 |
| ui-review | UI 一致性与视觉回归审查，设计稿到代码对比 |
| accessibility | WCAG 2.2 无障碍审计与跨平台语义化实现 |
| motion-design | Framer Motion 动画与微交互：页面过渡、手势、滚动 |