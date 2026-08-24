# MySQL 数据库规范审查 Skill

Claude Code 自定义 Skill 资源包，可供 MySQL 数据库设计审查与 SQL 编写时使用。

## 声明

本资源包基于《阿里巴巴 Java 开发手册（黄山版 v1.7.1）》整理而成，仅供学习与参考使用。原手册版权归原作者所有。请勿将本内容用于商业用途或声称原创。

## 安装

将 `.claude` 目录复制到用户主目录下即可全局生效（所有项目均可使用）：

```bash
# Windows
xcopy /E /I .claude %USERPROFILE%\.claude\

# macOS / Linux
cp -r .claude ~/.
```

也可安装到单个项目根目录下，仅对该项目生效：

```bash
cp -r .claude /path/to/your-project/
```

## Skill 说明

### mysql-coding-review

MySQL 数据库规范审查标准，覆盖三大维度：

| 维度 | 内容 |
|------|------|
| 一、建表规约 | 表/字段命名、数据类型选择、必备字段、逻辑删除 |
| 二、索引规约 | 唯一索引、join限制、模糊查询、覆盖索引、深分页优化 |
| 三、SQL 语句 | count/sum/NULL处理、外键禁止、存储过程禁止、表别名 |

**激活条件：**
- 审查或设计 MySQL 数据库表结构时
- 编写或审查 DDL（CREATE TABLE、CREATE INDEX）时
- 编写或审查复杂 SQL 查询时
- 数据库性能优化或索引设计时

**规则级别：**
- 【强制】— 必须遵守，违反视为严重问题
- 【推荐】— 建议遵守，违反视为改进建议
