# UI 视觉审查 Playbook（ui-review-checklist）

> 适用技能：`skills/ui-review`（UI 一致性与视觉回归审查，设计稿到代码对比）。
> 本 playbook 提供审查的触发条件、分级标准、可运行的一致性检查代码，以及一份可直接勾选的审查清单。
> 相关技能：`skills/accessibility`（对比度/焦点属其范畴）、`skills/motion-design`（动效流畅度与 reduced-motion 在交互审查中验收）。

## 1. 何时使用本 playbook（选择矩阵）

| 触发场景 | 审查重点 | 输入形式 |
|----------|----------|----------|
| 上线前质量门禁 | 全维度一致性 | 生产环境 URL 或多张截图 |
| 设计稿 vs 实现对比 | 还原度偏差 | 设计稿 + 实现截图并排 |
| 组件库状态完整性 | hover/active/disabled/focus | 单组件多状态截图 |
| 多设备/多浏览器一致性 | 响应式断点、渲染差异 | 桌面/平板/手机截图 |
| 视觉回归回归检查 | 本次改动引入的偏离 | 改动前/后截图对比 |

**判定原则**：UI 审查是「主观 + 客观」混合任务。对比度、间距、字号这类可量化项用脚本/工具客观判定；视觉层次、信息密度这类主观项用分级描述，避免武断打分。

## 2. 决策树：选哪种审查

```
开始
├─ 是否有明确设计稿？
│   ├─ 是 → 「还原度审查」：逐区域对比设计稿与实现，标偏离%
│   └─ 否 → 「一致性审查」：以自身设计系统 token 为基准
├─ 是否只关心某组件？
│   └─ 是 → 「状态完整性审查」：聚焦 hover/active/disabled/focus/loading
├─ 是否跨设备？
│   └─ 是 → 加「响应式审查」：在 375 / 768 / 1280 三档断点各取一帧
└─ 是否本次有代码改动？
    └─ 是 → 「视觉回归」：改动前/后同视角对比，只报新增差异
```

## 3. 具体命令与代码

### 3.1 准备素材

```bash
# 用无头浏览器对目标 URL 多断点截图（示例：Playwright）
npx playwright install chromium
cat > shot.mjs <<'EOF'
import { chromium } from 'playwright';
const url = process.argv[2];
const browser = await chromium.launch();
for (const w of [375, 768, 1280]) {
  const page = await browser.newPage({ viewport: { width: w, height: 900 } });
  await page.goto(url, { waitUntil: 'networkidle' });
  await page.screenshot({ path: `shot-${w}.png`, fullPage: true });
}
await browser.close();
EOF
node shot.mjs https://your-site.com
```

### 3.2 客观项：可运行对比度检查（WCAG）

把设计稿/实现里抽出的前景色与背景色喂给下面脚本，自动判定是否达标（正文 4.5:1，大文本/UI 3:1）：

```python
# contrast_check.py —— 运行: python3 contrast_check.py "#18181b" "#f4f4f5"
import sys
from math import sqrt

def lin(c):
    c /= 255
    return c / 12.92 if c <= 0.03928 else ((c + 0.055) / 1.055) ** 2.4

def lum(hexv):
    h = hexv.lstrip("#")
    r, g, b = int(h[0:2], 16), int(h[2:4], 16), int(h[4:6], 16)
    return 0.2126 * lin(r) + 0.7152 * lin(g) + 0.0722 * lin(b)

def ratio(fg, bg):
    l1, l2 = lum(fg), lum(bg)
    hi, lo = max(l1, l2), min(l1, l2)
    return round((hi + 0.05) / (lo + 0.05), 2)

if __name__ == "__main__":
    fg, bg = sys.argv[1], sys.argv[2]
    r = ratio(fg, bg)
    body = "PASS" if r >= 4.5 else "FAIL"
    ui   = "PASS" if r >= 3.0 else "FAIL"
    print(f"contrast={r}  正文(4.5:1)={body}  大文本/UI(3:1)={ui}")
```

### 3.3 审查维度与严重级定义

| 维度 | 检查点 | 严重 | 一般 | 建议 |
|------|--------|------|------|------|
| 布局 | 对齐、间距节奏、溢出 | 元素错位/重叠 | 间距不统一 | 留白可优化 |
| 颜色 | 对比度、品牌色一致 | 对比度不达标 | 同色系偏差 | 可加层次 |
| 字体 | 字号层级、行高 | 不可读 | 层级模糊 | 节奏可更稳 |
| 交互 | 状态完整、焦点可见 | 缺关键状态 | hover/active 不一致 | focus 样式弱 |
| 响应式 | 断点表现 | 内容截断 | 错位 | 间距可收紧 |

### 3.4 报告模板

```markdown
## UI 审查报告 —— <页面/组件>
- 输入：<URL 或截图>
- 结论：通过 / 需修改（N 项严重）

### 严重
1. [布局]  hero 区 CTA 在 375px 溢出 12px —— 建议 p-{n} 收紧
### 一般
2. [颜色]  次要文字 #6b7280 on #f4f4f5 对比度 4.1，未达 4.5 —— 调深至 #4b5563
### 建议
3. [字体]  正文行高 1.4 偏紧，建议 1.6
```

## 4. 典型陷阱与规避

| 陷阱 | 后果 | 规避 |
|------|------|------|
| 凭印象说「不够好看」 | 无法落地修改 | 每项给具体 CSS 修复建议 |
| 只看桌面截图 | 移动端错位漏检 | 强制 375/768/1280 三档 |
| 对比度靠肉眼 | 主观误判 | 用 3.2 脚本客观判定 |
| 只报问题不分级 | 开发无从排期 | 严重/一般/建议三级 |
| 忽略交互状态 | 上线后 hover 失效 | 强制查 5 种状态 |
| 把品牌评审当审查 | 范围蔓延 | 仅查一致性，不评策略 |

## 5. 检查清单（上线前勾选）

- [ ] 布局：所有区块对齐到网格，无错位/溢出（375/768/1280）
- [ ] 间距：同层级间距一致，遵循 4px 节奏
- [ ] 颜色：正文对比度 ≥ 4.5:1，UI/大文本 ≥ 3:1（脚本验证）
- [ ] 颜色：品牌色在所有页面取值一致
- [ ] 字体：标题/正文层级清晰，行高 1.5–1.7
- [ ] 交互：hover / active / disabled / focus / loading 五态完整
- [ ] 焦点：键盘可达，焦点指示器可见（SC 2.4.11）
- [ ] 响应式：三档断点无内容截断、无横向滚动
- [ ] 还原度：与设计稿偏差已量化并记录
- [ ] 报告：问题已分级并附修复代码
