# 设计系统基础 Playbook（design-system-foundations）

> 适用技能：`skills/design-system`（从网站提取设计基元生成 token，构建 Tailwind v4 设计系统）。
> 本 playbook 不重复子技能的操作步骤，而是提供「何时用、怎么选、怎么落地、避什么坑」的方法论与可运行代码。

## 1. 何时使用本 playbook（选择矩阵）

| 你的情况 | 推荐动作 | 产物 |
|----------|----------|------|
| 新项目，没有任何设计资产 | 从零定义 token 体系 | `tokens.json` + Tailwind v4 `@theme` |
| 想参考竞品/灵感站点的视觉风格 | 网站提取（仅作初始化参考） | `normalized.json` → 人工筛选后落 token |
| 已有 Tailwind v3 项目 | 迁移到 v4（CSS-first） | 移除 `tailwind.config.js`，改用 `@theme` |
| 已有设计 token（Figma/Style Dictionary） | 直接转译，不重新提取 | `tokens.css` |
| 需要明暗双主题 | 主题切换（CSS 变量驱动） | `:root` / `.dark` 两套变量 |

**判定原则**：提取永远只是「起点」，不是「答案」。任何从外部站点提取的 token，都必须经过人工取舍，禁止直接覆盖团队已有设计系统。

## 2. 决策树：提取 vs 从零构建 vs 迁移

```
开始
├─ 目标站点是否公开可访问、静态为主？
│   ├─ 是 → 用「网站提取」拿到原始基元
│   │        └─ 是否要保留团队现有品牌色/字体？
│   │            ├─ 是 → 仅借用间距/圆角节奏，颜色字体用手写 token
│   │            └─ 否 → 直接采用提取结果（注明来源）
│   └─ 否（需登录/SPA/强动态）→ 不要硬提取，改为「从零定义」手动列 token
├─ 是否已有 v3 项目？
│   └─ 是 → 走「v3→v4 迁移」：config 中的 theme 搬到 CSS `@theme`
└─ 是否要暗色模式？
    └─ 是 → 所有颜色 token 必须成对（浅/深），用 CSS 变量而非硬编码
```

## 3. 具体命令与代码

### 3.1 从网站提取设计基元

```bash
# 安装提取器（一次性）
npx extract-design-system --help

# 提取某公开站点
npx extract-design-system https://example.com

# 提取结果落在 .extract-design-system/normalized.json
# 审查其中的 colors / fonts / spacing / radius / shadows
ls .extract-design-system
```

提取后**不要**直接信任全部数值。按以下优先级筛选：
- 颜色：保留主色、中性灰阶；丢弃一次性装饰色。
- 字体：只取 1 套标题 + 1 套正文。
- 间距：映射为 4px 基准的阶梯（4/8/12/16/24/32…）。

### 3.2 产出 token 文件

`tokens.json`（机器可读、可交给 Style Dictionary 转译）：

```json
{
  "color": {
    "primary": { "value": "#4f46e5" },
    "neutral-900": { "value": "#18181b" },
    "neutral-100": { "value": "#f4f4f5" }
  },
  "space": {
    "1": { "value": "4px" }, "2": { "value": "8px" }, "3": { "value": "12px" },
    "4": { "value": "16px" }, "6": { "value": "24px" }, "8": { "value": "32px" }
  },
  "radius": { "md": { "value": "8px" }, "lg": { "value": "16px" } }
}
```

`tokens.css`（CSS 自定义属性，浏览器原生可用）：

```css
:root {
  --color-primary: #4f46e5;
  --color-neutral-900: #18181b;
  --color-neutral-100: #f4f4f5;
  --space-1: 4px;  --space-2: 8px;  --space-3: 12px;
  --space-4: 16px; --space-6: 24px; --space-8: 32px;
  --radius-md: 8px; --radius-lg: 16px;
}
```

### 3.3 Tailwind v4 `@theme` 配置

Tailwind v4 是 CSS-first，不再需要 `tailwind.config.js`。在入口 CSS 中：

```css
@import "tailwindcss";

@theme {
  --color-primary: #4f46e5;
  --color-neutral-900: #18181b;
  --color-neutral-100: #f4f4f5;
  --spacing-1: 4px;  --spacing-2: 8px;  --spacing-3: 12px;
  --spacing-4: 16px; --spacing-6: 24px; --spacing-8: 32px;
  --radius-md: 8px;  --radius-lg: 16px;
}

/* 现在可直接写 class：bg-primary text-neutral-900 p-4 rounded-lg */
```

> 注意：Tailwind v4 已内置 `--spacing-*` 默认步进（基于 0.25rem）。若你用 `--spacing-4` 会**覆盖**默认 spacing 比例，导致 `p-4` 含义变化。建议：颜色/圆角自定义，间距沿用默认 `p-4`（`1rem`）即可，避免语义冲突。

### 3.4 暗色模式与主题切换

```css
@theme {
  --color-bg: #ffffff;
  --color-fg: #18181b;
  --color-primary: #4f46e5;
}

.dark {
  --color-bg: #0b0b0f;
  --color-fg: #f4f4f5;
  --color-primary: #818cf8;
}
```

切换逻辑（纯 CSS 变量驱动，无需重渲染组件）：

```js
// 读取用户偏好并切换
const mq = window.matchMedia("(prefers-color-scheme: dark)");
const apply = (dark) => document.documentElement.classList.toggle("dark", dark);
apply(mq.matches);
mq.addEventListener("change", (e) => apply(e.matches));
```

### 3.5 在组件中使用

```html
<button class="bg-primary text-white rounded-lg px-4 py-2 hover:opacity-90">
  立即开始
</button>
```

## 4. 典型陷阱与规避

| 陷阱 | 后果 | 规避 |
|------|------|------|
| 直接把提取的全部颜色写进 token | 颜色泛滥、失去一致性 | 只留主色 + 中性灰阶 |
| 用 `--spacing-*` 覆盖默认阶梯 | `p-4` 等语义被改，团队困惑 | 间距走默认，`--space-*` 仅自定义命名 |
| 硬编码颜色而非用变量 | 暗色模式失效 | 所有颜色经 `--color-*` 变量 |
| 把提取结果覆盖已有设计系统 | 团队资产被污染 | 提取结果只作参考，手动合并 |
| 字体一次引 3+ 套 | 加载慢、视觉乱 | 标题 1 + 正文 1 |
| 圆角/阴影无节奏 | 界面廉价感 | 固定 2–3 档圆角，阴影统一管理 |

## 5. 检查清单

- [ ] 颜色 token ≤ 主色 1 + 中性灰阶 1 套 + 状态色（成功/警告/错误）各 1
- [ ] 所有颜色用 CSS 变量表达，暗色模式有成对定义
- [ ] 间距沿用 Tailwind 默认阶梯，未误覆盖 `--spacing-*`
- [ ] 圆角/阴影不超过 3 档，命名语义明确
- [ ] 字体仅 标题 + 正文 两套，已 `font-family` 变量化
- [ ] `tokens.json` 已生成且可被 Style Dictionary 转译
- [ ] `tokens.css` 的 `:root` 与 `.dark` 变量名一致
- [ ] 组件实际引用了 token class，无硬编码色值
- [ ] 提取来源已在 README/注释中标注（合规溯源）
