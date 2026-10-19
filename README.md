# spec

研发全流程 Agent Skills 合集：开发工作流、技术设计模板、代码规范审查、测试用例设计、调研与 Git 提交规范，Claude Code / Codex / OpenCode 通用。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 目录

<details>
<summary>展开/收起</summary>

- [背景](#背景)
- [安装](#安装)
- [快速开始](#快速开始)
- [使用示例](#使用示例)
- [目录结构](#目录结构)
- [贡献指南](#贡献指南)
- [License](#license)

</details>

## 背景

团队规范（代码规约、设计模板、用例设计方法）写在文档里，靠人记忆和自觉执行，时间一长就变成"写了没人看，违反没人管"。本仓库把规范改写成 AI 编码工具可执行的 Skill——AI 编码助手读到规范后按规范干活，规范从"参考文档"变成"执行契约"。

核心特性：

- **全流程覆盖**：从调研、产品设计、技术设计到开发、测试，模块按研发阶段编号，需要哪个装哪个
- **零依赖、照抄可装**:Skill 以纯 Markdown 交付，一条 `cp` 命令完成安装，无运行时依赖
- **跨工具通用**:Codex / OpenCode 原生识别 `.agents/skills/`;Claude Code 复制到 `.claude/skills/` 即可
- **断点续跑**:`develop`、`research` 等工作流支持会话持久化，中断后下次继续
- **先自检再交人**：每个 Skill 内置自检清单（如 `git-commit` 五项自检），产出先过检、再交用户确认

## 安装

### 环境要求

| 依赖 | 要求 | 说明 |
|---|---|---|
| AI 编码工具 | Claude Code / Codex / OpenCode 任一 | Skill 以 Markdown 交付，无其他运行时依赖 |
| 操作系统 | macOS / Windows / Linux | 仅复制目录命令不同 |

### 1. 克隆仓库

```bash
git clone https://github.com/Heifetz1901/spec.git
cd spec
```

### 2. 安装 Skill

**Claude Code**(读取 `.claude/skills/`):

```bash
# 全局安装(所有项目可用)——以 git-commit 为例
mkdir -p ~/.claude/skills && cp -r 99-tools/git/.agents/skills/git-commit ~/.claude/skills/

# 或安装到单个项目根目录(仅该项目生效)
mkdir -p /path/to/your-project/.claude/skills && cp -r 99-tools/git/.agents/skills/git-commit /path/to/your-project/.claude/skills/
```

**Codex / OpenCode**(原生识别 `.agents/skills/`):

```bash
# 全局安装——以 research 为例
mkdir -p ~/.agents && cp -r 05-research/.agents/skills/research ~/.agents/skills/
```

各模块的 Skill 所在目录见下方[目录结构](#目录结构)，替换命令中的模块路径即可。

### 3. 验证

重启会话后，在任一有改动的 git 仓库中输入：

```text
/git-commit
```

预期：AI 编码助手按中文 Conventional Commits 模板生成 commit message，完成五项自检后请你确认，确认后才执行提交。

## 快速开始

以 `git-commit` 为例，3 步跑通：

```bash
# 1. 安装(仓库根目录执行)
mkdir -p ~/.claude/skills && cp -r 99-tools/git/.agents/skills/git-commit ~/.claude/skills/
```

2. 重启会话（新装 Skill 需重启后生效）
3. 在任意 git 仓库中输入 `/git-commit`，或说"帮我提交代码"

预期：AI 编码助手按中文 Conventional Commits 模板生成 commit message，完成五项自检后请你确认，确认后才执行提交。

## 使用示例

**Java 代码规范审查**(自然语言触发):

```text
审查一下这个 MR 的代码,重点看异常处理和单元测试
```

**调研工作流**(显式调用，断点续跑):

```text
/research ZGC 的低时延机制
```

产出标准格式 Markdown 调研文档；会话中断后再次调用可从断点继续。

**开发工作流**(需求变更全流程):

```text
需求:订单列表增加"仅看异常订单"筛选,请按工作流开发
```

`develop` Skill 按 步骤R/0→7 串行执行：恢复检查→需求分析→更新设计文档→补充测试场景→基线测试→TDD 开发→代码审核→修复问题→最终验证。

## 目录结构

```text
00-workflow/     开发工作流(需求变更/缺陷修复,串行工作流)
01-prod-design/  产品设计规范与 PRD 模板(规划中)
02-tech-design/  技术类设计文档模板与生成 Skill
03-dev/          代码规范审查(java / db/mysql)
04-test/         测试用例设计(等价类、边界值、判定表、场景法)
05-research/     调研工作流(断点续跑,沉淀个人知识库)
99-tools/        跨阶段通用工具(git / readme)
```

### 模块总览

| 模块 | 阶段 | Skill | 状态 | 说明 |
|------|------|-------|------|------|
| [00-workflow](00-workflow/README.md) | 贯穿全流程 | `develop` | 可用 | 开发工作流（需求变更/缺陷修复） |
| [01-prod-design](01-prod-design/README.md) | ① 产品设计 | — | 规划中 | 产品设计规范与 PRD 模板 |
| [02-tech-design](02-tech-design/README.md) | ② 研发设计 | `tech-design` | 可用 | 技术类设计文档模板与生成 |
| [03-dev/java](03-dev/java/README.md) | ③ 开发 | `java-coding-review` | 可用 | Java 规范审查（阿里手册七大维度） |
| [03-dev/db/mysql](03-dev/db/mysql/README.md) | ③ 开发 | `mysql-coding-review` | 可用 | MySQL 审查（建表/索引/SQL 语句） |
| [04-test](04-test/README.md) | ④ 测试 | `test-case-design` | 可用 | 测试用例设计 |
| [05-research](05-research/README.md) | 通用 | `research` | 可用 | 调研工作流（断点续跑） |
| [99-tools/git](99-tools/git/README.md) | 通用 | `git-commit` | 可用 | Git 提交工作流 + git 配置模板 |
| [99-tools/readme](99-tools/readme/README.md) | 通用 | `readme` | 可用 | README 编写规范与生成 |

状态说明：**规划中**(目录占位)→ **编写中**(草稿未定稿)→ **可用**(内容完整可使用)。

## 贡献指南

欢迎贡献：新 Skill 建议、规范内容改进、文档修正都可以。建议先开 [issue](https://github.com/Heifetz1901/spec/issues) 讨论确认方案后再提 PR；贡献规则见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

MIT

03-dev/java 中的《阿里巴巴Java开发手册》PDF 及 MD 转写源自 [alibaba/p3c](https://github.com/alibaba/p3c)(Apache-2.0)，版权归阿里巴巴所有。
