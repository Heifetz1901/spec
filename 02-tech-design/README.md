# Tech Design - 技术设计文档 Skill

Claude Code 自定义 Skill 资源包，基于技术类设计文档模板生成符合规范的技术设计文档，支持团队分工和 Agent 并行执行。

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

安装后，通过 `/tech-design {设计需求描述}` 调用。

## 目录结构

```
02-tech-design/
├── .claude/
│   └── skills/
│       └── tech-design/
│           └── SKILL.md              # 技术设计文档 Skill
├── 技术类设计文档模板.md              # 源文档
├── 技术类设计文档工作流.md            # 源文档
└── README.md                         # 本文件
```

## Skill 说明

### tech-design

基于《技术类设计文档模板》生成符合规范的公共库/组件技术设计文档：

- 按模板结构生成各章节内容
- 支持团队分工，可拆分给多个 Agent 并行执行
- 配合《技术类设计文档工作流》完成评审与定稿
