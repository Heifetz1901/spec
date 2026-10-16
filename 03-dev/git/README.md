# Git 提交规范 Skill

Agent Skill 资源包（遵循 [Agent Skills](https://agentskills.io/specification) 开放标准格式），提供提交工作流：按中文 Conventional Commits 模板生成 commit message → 五项自检 → 用户确认 → 执行提交；附 `.gitattributes` / `.gitignore` 参考模板。

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
mkdir -p ~/.claude/skills && cp -r .agents/skills/git-commit ~/.claude/skills/

# 或安装到单个项目根目录（仅该项目生效）
mkdir -p /path/to/your-project/.claude/skills && cp -r .agents/skills/git-commit /path/to/your-project/.claude/skills/
```

安装后，用户要求"提交代码 / 写 commit message"时自动触发，也可通过 `/git-commit {提交需求}` 显式调用。

> 建议配合 git `commit-msg` hook 使用：Skill 负责生成时合规与语义规则（一事一提交、body 说 why），hook 对任何工具/人做确定性兜底，两者互补。

### 参考文件

- [`.gitattributes`](.gitattributes)：换行符与二进制策略（入库一律 LF、`*.sh` 等强制 LF、Windows 脚本 CRLF、二进制不转换）
- [`.gitignore`](.gitignore)：忽略 AI 工具本地状态（`.omc/`、根 `/.claude/`）等

安装到目标仓库（按需增删条目）：

```bash
cp .gitattributes /path/to/your-repo/.gitattributes
cp .gitignore     /path/to/your-repo/.gitignore
```

- `.gitattributes` 只对此后的提交生效，存量仓库需执行一次 `git add --renormalize .` 归一换行符
- `.gitignore` 条目按目标仓库实际情况调整

## 目录结构

```
03-dev/git/
├── .agents/
│   └── skills/
│       └── git-commit/
│           └── SKILL.md              # 提交规范工作流 Skill（单一事实来源）
├── .gitattributes                    # 参考模板：换行符与二进制策略
├── .gitignore                        # 参考模板：忽略 AI 工具本地状态等
└── README.md                         # 本文件
```

## Skill 说明

### git-commit

| 步骤 | 内容 |
|------|------|
| 步骤0 | 盘点变更 — status/diff 理解变更，检查一事一提交，必要时提议拆分 |
| 步骤1 | 生成提交信息 — 按类型判据表选 type，中文描述，body 说 why |
| 步骤2 | 校验 — 五项自检，任一不通过回退修正 |
| 步骤3 | 用户确认 — 展示提交信息与校验结果，确认后放行 |
| 步骤4 | 提交 — heredoc 提交；hook 拒绝时读 stderr 修正重试（至多 2 次） |

**提交规范**：中文 Conventional Commits，八类型（feat/fix/refactor/docs/test/chore/perf/ci）+ 五规则，完整判据与示例见 [SKILL.md](.agents/skills/git-conventions/SKILL.md)。

**依赖的其他 Skill**：无。

## 与本仓库根目录文件的关系

本仓库根目录的 `.git-commit-template`、`.gitattributes`、`.gitignore` 是本模块规范在本仓库的落地实例。变更流程：先修改本模块源文档与参考文件，确认后同步根目录实例（遵循仓库"单一事实来源"约定）。
