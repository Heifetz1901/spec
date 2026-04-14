# Claude Code 代码规范审查 Skills

基于《阿里巴巴 Java 开发手册（黄山版 v1.7.1）》整理的 Claude Code 自定义 Skill 资源包，可供代码审查与代码生成时使用。

## 声明

本资源包基于《阿里巴巴 Java 开发手册（黄山版 v1.7.1）》整理而成，仅供学习与参考使用。原手册版权归原作者所有。请勿将本内容用于商业用途或声称原创。

## 目录结构

```
spec/
├── java/                                # Java 代码规范审查 Skill
│   ├── .claude/skills/java-coding-review/
│   │   └── SKILL.md                     # Java 代码规范审查标准
│   ├── 阿里巴巴Java开发手册-黄山版.md     # 源文档
│   ├── 阿里巴巴Java开发手册-黄山版v1.7.1.pdf
│   └── README.md
├── db/
│   └── mysql/                           # MySQL 数据库规范审查 Skill
│       ├── .claude/skills/mysql-coding-review/
│       │   └── SKILL.md                 # MySQL 数据库规范审查标准
│       └── README.md
└── README.md                            # 本文件
```

## 包含的 Skills

| Skill | 说明 | 维度 |
|-------|------|------|
| `java-coding-review` | Java 代码规范审查 | 编程规约、异常日志、单元测试、安全规约、MySQL、工程结构、设计规约 |
| `mysql-coding-review` | MySQL 数据库规范审查 | 建表规约、索引规约、SQL 语句 |

## 安装

将对应模块的 `.claude` 目录复制到用户主目录下即可全局生效：

```bash
# 全局安装（所有项目生效）
cp -r java/.claude ~/.claude/
cp -r db/mysql/.claude ~/.claude/

# Windows
xcopy /E /I java\.claude %USERPROFILE%\.claude\
```

也可安装到单个项目根目录下，仅对该项目生效：

```bash
cp -r java/.claude /path/to/your-project/
```

安装后，Claude Code 在处理对应语言的代码时将自动激活相应 Skill，无需额外配置。

## 使用

安装后无需手动操作。Claude Code 在以下场景会自动激活对应 Skill：

- 审查或审计 Java 源代码时
- 生成需要符合企业级规范的 Java 代码时
- 审查或设计 MySQL 数据库表结构时
- 编写或审查 DDL、SQL 查询时

## License

仅供学习与参考使用。原手册版权归原作者所有。
