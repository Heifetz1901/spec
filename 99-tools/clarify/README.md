# clarify —— 需求澄清与领域建模

开工前把需求搞清楚：澄清（clarify）+ 守门（gatekeep）两个技能，可单独使用或经组合壳（clarify-with-docs）一键启动。

## 技能

| 技能 | 角色 | 职责 | 调用方式 |
|------|------|------|---------|
| clarify | 澄清者 | 结构化追问直到达成可执行共识 | 用户说「澄清/讨论/头脑风暴/问清楚再干」触发，或被其它技能前置调用 |
| gatekeep | 守门人 | 术语挑战与锐化、代码交叉验证、GLOSSARY/ADR 维护 | 讨论术语/编辑 GLOSSARY/记录 ADR 时触发，或被 clarify-with-docs 组合调用 |
| clarify-with-docs | 组合壳 | 一键启动澄清+守门 | 仅用户调用 |

## 安装

```bash
cp -r 99-tools/clarify/.agents/skills/* <目标项目>/.agents/skills/
```

## 配置（可选）

技能正文内置全部默认值。需要自定义路径时，在目标项目创建 `.agents/config.yaml`：

```yaml
gatekeep:
  glossary_layout: single         # single | multi
  glossary_file: GLOSSARY.md
  glossary_map_file: GLOSSARY-MAP.md
  adr_dir: docs/adr/
  adr_name_pattern: "NNNN-短语.md"
  adr_slug_lang: zh               # zh | en
```

## 使用

- 新需求开工前：`/clarify-with-docs "需求描述"` → 一场完整访谈，同时产出术语表和 ADR
- 只想快速澄清：`/clarify "想法"` → 纯对话，不写文件
- 已有术语表要维护：直接讨论术语，gatekeep 自动触发

## 来源

基于 [mattpocock/skills](https://github.com/mattpocock/skills) 的 grilling + domain-modeling，经逐条评审后中文化并做少量增强（G0 收材料、预设还原、图语义措辞）。完整评审记录见设计文档。
