# Workflow - 开发工作流 Skill

Claude Code 自定义 Skill 资源包，提供可重复执行的开发工作流，适用于已有项目的需求变更、缺陷修复等开发工作。

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

安装后，通过 `/develop {需求描述}` 调用工作流。

## 目录结构

```
00-workflow/
├── .claude/
│   └── skills/
│       └── develop/
│           └── SKILL.md              # 开发工作流 Skill
├── develop.md                         # 源文档
└── README.md                          # 本文件
```

## 迭代循环（理念视图）

```mermaid
%%{init: { "theme": "base", "flowchart": { "htmlLabels": false }, "themeVariables": { "primaryColor": "#fff8c5", "primaryTextColor": "#4d2d00", "primaryBorderColor": "#9a6700", "lineColor": "#9a6700", "edgeLabelBackground": "#fff8c5", "fontSize": "14px" } } }%%
flowchart LR
    REQ(["需求<br/>/develop 触发"]) --> DES["设计<br/>设计文档 + 测试场景"]
    DES --> DEV["开发<br/>TDD 红→绿→重构"]
    DEV --> REV["审核<br/>规范审核 + 修复"]
    REV --> SHIP(["交付<br/>验证 + 摘要归档"])
    SHIP -- "下一个需求" --> REQ

    classDef plain fill:#fff8c5,stroke:#9a6700,stroke-width:2px,color:#4d2d00
    class REQ,DES,DEV,REV,SHIP plain
    linkStyle 0,1,2,3,4 stroke:#9a6700,stroke-width:2px,color:#9a6700
```

> 每转一圈 = 交付一个需求。`dev-session.md` 记录进度，任意一步中断后由步骤R 从断点续跑。

## 工作流图（执行视图）

```mermaid
%%{init: { "theme": "base", "flowchart": { "htmlLabels": false }, "themeVariables": { "primaryColor": "#fff8c5", "primaryTextColor": "#4d2d00", "primaryBorderColor": "#9a6700", "lineColor": "#9a6700", "edgeLabelBackground": "#fff8c5", "fontSize": "14px" } } }%%
flowchart TD
    Start(["/develop 需求描述"]) --> R{"步骤R: 恢复检查<br/>dev-session.md 存在？"}
    R -- "否" --> S0["步骤0: 需求分析与准备<br/>评估变更规模 · 规划能力P1-P4<br/>初始化清单并创建 dev-session.md"]
    R -- "是" --> Resume["从断点恢复（用户确认）"]
    Resume --> S0
    S0 --> S1["步骤1: 更新设计文档"]
    S1 --> S2["步骤2: 补充测试场景<br/>test-case-design Skill"]
    S2 --> S3["步骤3: 基线测试<br/>记录已知失败"]
    S3 --> S4["步骤4: TDD 开发<br/>红 → 绿 → 重构"]
    S4 --> S5["步骤5: 代码审核<br/>按技术栈匹配审核 Skill"]
    S5 --> S6["步骤6: 修复审核问题<br/>CRITICAL → WARNING → INFO"]
    S6 --> S7["步骤7: 最终验证<br/>全量测试 + 交付物检查"]
    S7 --> Done(["输出开发完成摘要<br/>归档 dev-session.md"])

    S5 -. "审核发现设计缺陷" .-> S1
    S7 -. "测试失败" .-> S4

    linkStyle 0,1,2,3,4,5,6,7,8,9,10,11,12,13 stroke:#9a6700,stroke-width:2px,color:#9a6700
```

> 每个步骤完成时更新 `dev-session.md`，支持任意阶段中断后恢复（步骤R）。

## Skill 说明

### develop

开发工作流，8步串行执行：

| 步骤 | 内容 |
|------|------|
| 步骤0 | 需求分析与准备 — 解析需求、评估规模、初始化变更清单 |
| 步骤1 | 更新设计文档 — 将需求变更反映到设计文档 |
| 步骤2 | 补充测试场景 — 使用 test-case-design Skill 设计用例 |
| 步骤3 | 基线测试 — 确认现有测试状态 |
| 步骤4 | TDD开发 — 红→绿→重构 |
| 步骤5 | 代码审核 — 按项目技术栈匹配 Skill 审核 |
| 步骤6 | 修复审核问题 — CRITICAL/WARNING 逐条修复 |
| 步骤7 | 最终验证 — 测试通过 + 交付物检查 |

**依赖的其他 Skill：**
- `test-case-design` — 步骤2 测试用例设计
- `java-coding-review` / `mysql-coding-review` 等 — 步骤5 代码审核

**变更规模适配：**
- 大改（核心逻辑/新功能）：全步骤执行，覆盖率 >= 80%
- 中改（单模块功能）：全步骤执行，覆盖率 >= 70%
- 小改（bugfix/配置）：可跳过步骤2，覆盖变更部分即可
