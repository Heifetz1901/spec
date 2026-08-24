# Java 代码规范审查 Skill

Claude Code 自定义 Skill 资源包，可供 Java 代码审查与代码生成时使用。

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
cp -r .claude /path/to/your-java-project/
```

安装后，Claude Code 在处理 Java 代码时将自动激活 `java-coding-review` Skill，无需额外配置。

## 目录结构

```
java/
├── .claude/
│   └── skills/
│       └── java-coding-review/
│           └── SKILL.md              # Java 代码规范审查标准
├── README.md                         # 本文件
├── 阿里巴巴Java开发手册-黄山版.md      # 源文档
└── 阿里巴巴Java开发手册-黄山版v1.7.1.pdf  # 原始 PDF
```

## Skill 说明

### java-coding-review

Java 代码规范审查标准，覆盖七大维度：

| 维度 | 内容 |
|------|------|
| 一、编程规约 | 命名风格、常量定义、代码格式、OOP、日期时间、集合处理、并发处理、控制语句、注释规约、前后端规约 |
| 二、异常日志 | 错误码、异常处理、日志规约 |
| 三、单元测试 | AIR原则、覆盖率、BCDE原则 |
| 四、安全规约 | 权限控制、SQL注入、XSS、CSRF、文件上传等 |
| 五、MySQL | 建表规约、索引规约、SQL语句、ORM映射 |
| 六、工程结构 | 应用分层、二方库依赖、服务器配置 |
| 七、设计规约 | 设计原则、UML建模、降级容灾 |

**激活条件：**
- 审查或审计 Java 源代码时
- 生成需要符合企业级规范的 Java 代码时
- 用户明确要求进行 Java 代码审查或规范检查时
- 涉及 MySQL、ORM 框架或 Web API 的 Java 项目工作时

**规则级别：**
- 【强制】— 必须遵守，违反视为严重问题
- 【推荐】— 建议遵守，违反视为改进建议
