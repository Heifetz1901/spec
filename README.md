# Spec - Claude Code Skills 合集

Claude Code 自定义 Skill 资源包，用于代码规范审查与测试用例设计。

## 变更约定

本仓库中的文档是**单一事实来源（Single Source of Truth）**，`~/.claude/skills/` 等安装目录是运行时副本。

**变更流程**：

1. 先修改本仓库中的源文档
2. 确认变更正确后，经用户确认再同步到安装目录

**原则**：
- 本仓库优先，安装目录从属
- 不得跳过源文档直接修改安装目录
- 同步到安装目录前需用户确认

## 模块

目录按研发流程顺序编号（0x-8x 号段），覆盖 调研 → 产品设计 → 研发设计 → 开发 → 测试 全流程；`99-` 号段收纳跨阶段通用工具（版本管理、文档等任何仓库都适用的工程基础）：

| 模块 | 阶段 | 状态 | 说明 |
|------|------|------|------|
| [00-workflow](00-workflow/README.md) | 贯穿全流程 | 可用 | 开发工作流（需求变更/缺陷修复，8步串行执行） |
| [01-prod-design](01-prod-design/README.md) | ① 产品设计 | 规划中 | 产品设计规范与 PRD 模板 |
| [02-tech-design](02-tech-design/README.md) | ② 研发设计 | 可用 | 技术类设计文档模板与生成 Skill |
| [03-dev/java](03-dev/java/README.md) | ③ 开发 | 可用 | Java 代码规范审查（基于阿里巴巴 Java 开发手册） |
| [03-dev/db/mysql](03-dev/db/mysql/README.md) | ③ 开发 | 可用 | MySQL 数据库规范审查 |
| [99-tools/git](99-tools/git/README.md) | 通用 | 可用 | Git 提交工作流（生成→校验→确认→提交）+ git 配置模板 |
| [04-test](04-test/README.md) | ④ 测试 | 可用 | 测试用例设计（等价类、边界值、判定表、场景法） |
| [05-research](05-research/README.md) | 通用 | 可用 | 调研工作流与文档模板（断点续跑，产出沉淀个人知识库） |
| [99-tools/readme](99-tools/readme/README.md) | 通用 | 可用 | README 编写规范与生成 Skill（盘点→补信息→生成→自检→写入） |

状态说明：**规划中**（目录占位，内容待编写）→ **编写中**（草稿未定稿）→ **可用**（内容完整可使用）。

## 使用方式

各模块包含独立的 skills 目录（`.claude/skills/`，或跨工具的 `.agents/skills/`），复制到用户主目录或项目根目录即可激活。详见各模块 README。

## License

仅供学习与参考使用。原始文档版权归原作者所有。
