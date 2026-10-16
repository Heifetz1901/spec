# Docs - README 编写规范 Skill

文档类规范模块：定义 README 的结构与安装章节写法，并提供 `readme` Skill 按《README编写规范》为项目生成 README（盘点项目 → 补关键信息 → 按模板生成 → 自检 → 确认写入）。

## 状态

**可用**

## 安装

### Skill

`.agents/skills/` 是跨工具的 Agent Skills 约定目录，Codex 与 OpenCode 原生识别。将其复制到用户主目录下即可全局生效（所有项目均可使用）：

```bash
# Windows
xcopy /E /I .agents %USERPROFILE%\.agents\

# macOS / Linux
cp -r .agents ~/.
```

Claude Code 读取 `.claude/skills/`、不识别 `.agents/`，需将 skill 复制一份（内容无需改动）：

```bash
# 全局安装（所有项目可用）
mkdir -p ~/.claude/skills && cp -r .agents/skills/readme ~/.claude/skills/

# 或安装到单个项目根目录（仅该项目生效）
mkdir -p /path/to/your-project/.claude/skills && cp -r .agents/skills/readme /path/to/your-project/.claude/skills/
```

安装后，用户要求"写 README / 补全 README"时自动触发，也可通过 `/readme {项目路径或描述}` 显式调用。

## 目录结构

```
06-docs/
├── .agents/
│   └── skills/
│       └── readme/
│           ├── SKILL.md              # README 编写工作流 Skill（单一事实来源）
│           └── assets/
│               └── template.md       # README 骨架模板（含适用性标注）
├── README编写规范.md                  # 规范源文档
└── README.md                         # 本文件
```

## 使用方式

编写或评审 README 时对照《[README编写规范](README编写规范.md)》执行，重点章节：

| 场景 | 使用章节 |
|------|---------|
| 新建 README 搭骨架 | 第 3 节结构清单 + 第 7.1 节骨架模板（或直接用 readme Skill） |
| 补安装 / 依赖说明 | 第 4 节安装章节规范 + 第 7.2 节内嵌示例 |
| Python 项目依赖描述 | 第 5 节工具链与版本策略 |
| 完成后达标检查 | 第 6 节质量自检清单（15 项） |

## Skill 说明

### readme

README 编写工作流，步骤 0→4 串行执行：

| 步骤 | 内容 |
|------|------|
| 步骤0 | 盘点项目 — 目录/依赖文件/LICENSE/现有 README，判定类型（库/应用/CLI/纯文档）与受众（开源/内部） |
| 步骤1 | 补关键信息 — 一句话定位、特性、最低版本依据、视觉素材、License，缺的问用户不编造 |
| 步骤2 | 生成 — 按 assets/template.md 骨架 + 适用性裁剪章节，安装按"四要素"组织 |
| 步骤3 | 自检 — 15 项质量清单逐项检查，任一不满足回退修正 |
| 步骤4 | 确认写入 — 用户确认后写入 README.md，已有文件先给保留/修改/删除对照 |

**规范要点**：首屏 3 秒（<120 字符三处一致）、照抄可跑（验证命令+预期输出）、密钥不进仓库、一个 README 一个目的（超 300 行拆 docs/）、License 必须最后一节（SPDX 标识）。

**依赖的其他 Skill**：无。

## 后续规划

- 变更日志（CHANGELOG）规范（Keep a Changelog 风格）
- docs/ 目录组织规范（多文档项目的结构约定）
