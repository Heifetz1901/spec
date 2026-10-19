# Readme - README 编写规范 Skill

README 编写规范模块:定义 README 的结构、安装章节写法与质量自检标准,并提供 `readme` Skill 为项目生成 README(盘点项目 → 补关键信息 → 按分章契约生成 → 自检 → 确认写入)。

## 状态

**可用**

## 安装

### Skill

`.agents/skills/` 是跨工具的 Agent Skills 约定目录,Codex 与 OpenCode 原生识别。将其复制到用户主目录下即可全局生效(所有项目均可使用):

```bash
# Windows
xcopy /E /I .agents %USERPROFILE%\.agents\

# macOS / Linux
cp -r .agents ~/.
```

Claude Code 读取 `.claude/skills/`、不识别 `.agents/`,需将 skill 复制一份(内容无需改动):

```bash
# 全局安装(所有项目可用)
mkdir -p ~/.claude/skills && cp -r .agents/skills/readme ~/.claude/skills/

# 或安装到单个项目根目录(仅该项目生效)
mkdir -p /path/to/your-project/.claude/skills && cp -r .agents/skills/readme /path/to/your-project/.claude/skills/
```

安装后,用户要求"写 README / 补全 README"时自动触发,也可通过 `/readme {项目路径或描述}` 显式调用。

## 目录结构

```
99-tools/readme/
├── .agents/
│   └── skills/
│       └── readme/
│           ├── SKILL.md              # 工作流编排(触发/边界/步骤 0→4),不含规范内容
│           └── assets/
│               ├── template.md       # 总纲:总体原则 + 全局格式 + 章节地图 + 全局自检
│               └── sections/         # 分章契约,每章固定三段:模板/规范(必须·建议·禁止)/示例
│                   ├── identity.md        # 首屏:项目名、简介、Badges、视觉展示
│                   ├── background.md      # 背景/特性
│                   ├── install.md         # 安装(含 Python 依赖惯例)
│                   ├── quick-start.md     # 快速开始(量化达标线)
│                   ├── usage-examples.md  # 使用示例
│                   ├── structure.md       # 目录结构
│                   ├── troubleshooting.md # 故障排查
│                   ├── roadmap.md         # Roadmap
│                   ├── api-reference.md   # API Reference
│                   ├── contributing.md    # 贡献指南
│                   └── license.md         # License
└── README.md                         # 本文件
```

> 2026-10 重构:原《README编写规范.md》(310 行)与独立骨架模板已整合为 skill 内 `assets/` 的"总纲 + 分章契约",规范与模板同文件、按章渐进加载,单一事实来源随技能走。

## 使用方式

编写或评审 README 时,读 skill 内规范执行:

| 场景 | 使用文件 |
|------|---------|
| 新建 README 搭骨架 | `assets/template.md` 章节地图 + 各章 `assets/sections/*.md` 的模板段 |
| 补安装 / 依赖说明 | `assets/sections/install.md`(含 Python 依赖惯例与完整示例) |
| 完成后达标检查 | 各分章"必须"项 + `assets/template.md` 全局自检 |

## Skill 说明

### readme

README 编写工作流,步骤 0→4 串行执行:

| 步骤 | 内容 |
|------|------|
| 步骤0 | 盘点项目 — 目录/依赖文件/LICENSE/现有 README,判定类型(库/应用/CLI/纯文档)与受众(开源/内部) |
| 步骤1 | 补关键信息 — 一句话定位、特性、最低版本依据、视觉素材、License,缺的问用户不编造 |
| 步骤2 | 生成 — 读总纲定适用章节集,逐章按分章契约的模板+规范生成 |
| 步骤3 | 自检 — 按各分章"必须"项逐章自检 + 总纲全局自检,任一不满足回退修正 |
| 步骤4 | 确认写入 — 用户确认后写入 README.md,已有文件先给保留/修改/删除对照 |

**依赖的其他 Skill**:无。

## 参考资料

- [GitHub Docs — About READMEs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
- [Standard ReadMe Spec](https://github.com/RichardLitt/standard-readme)([正式规范 spec.md](https://github.com/RichardLitt/standard-readme/blob/master/spec.md))
- [pyproject.toml vs requirements.txt(pydevtools handbook)](https://pydevtools.com/handbook/explanation/pyproject-vs-requirements)
- [Make a README](https://www.makeareadme.com/)
- [Awesome README](https://github.com/matiassingers/awesome-readme)
- [Top 100 高星仓库 README 结构分析](https://dev.to/belal_zahran/the-github-readme-template-that-gets-stars-used-by-top-repos-4hi7)
- [Best-README-Template](https://github.com/othneildrew/Best-README-Template)

## 后续规划

- 变更日志(CHANGELOG)规范(Keep a Changelog 风格,落地时独立为 `99-tools/changelog` 模块)
- docs/ 目录组织规范(多文档项目的结构约定,落地时独立模块)
