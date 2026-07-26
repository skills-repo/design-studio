# AGENTS.md

## 仓库性质

这是一个 **AI Agent 技能库**，不是软件项目。所有内容为 Markdown 格式的技能定义文件。

## 目录约定

```
design-studio/
├── README.md              # 项目介绍和使用指南
├── AGENTS.md              # AI 助手使用指引（本文件）
└── skills/                # 技能目录
    ├── <skill-name>/      # 单个技能目录
    │   └── SKILL.md       # 技能定义文件
    └── ...
```

## 工作约定

- 所有技能内容使用中文编写
- 面向独立开发者和设计新手，不假设有专业设计师
- 输出可执行的代码（CSS 变量、HTML 结构、JS 动画），不是设计理论
- 优先 Tailwind/CSS 变量方案，不绑定特定 UI 库

## 技能添加流程

1. 在 `skills/` 下创建以技能名命名的目录
2. 编写 `SKILL.md`
3. 确保 `metadata` 字段完整
4. 更新 `README.md` 中的技能清单表

## 不做什么

- 不输出不可执行的设计理论文章
- 不绑定 Figma/Sketch 等商业设计工具
- 不做品牌策略/视觉识别设计