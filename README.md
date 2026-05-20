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

| 模块 | 说明 | 详细文档 |
|------|------|---------|
| [dev/java](dev/java/README.md) | Java 代码规范审查（基于阿里巴巴 Java 开发手册） | [README](dev/java/README.md) |
| [dev/db/mysql](dev/db/mysql/README.md) | MySQL 数据库规范审查 | [README](dev/db/mysql/README.md) |
| [test](test/README.md) | 测试用例设计（等价类、边界值、判定表、场景法） | [README](test/README.md) |
| [workflow](workflow/README.md) | 开发工作流（需求变更/缺陷修复，8步串行执行） | [README](workflow/README.md) |

## 使用方式

各模块包含独立的 `.claude/skills/` 目录，复制到用户主目录或项目根目录即可激活。详见各模块 README。

## License

仅供学习与参考使用。原始文档版权归原作者所有。
