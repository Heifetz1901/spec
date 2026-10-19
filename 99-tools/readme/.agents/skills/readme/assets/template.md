# README 总纲:全局规范与章节地图

> 本文件与 `sections/` 分章契约共同构成 README 编写规范的**唯一源**。
> 用法:生成/评审 README 时,先在此读全局规范、按章节地图确定适用章节,再逐章打开 `sections/` 对应文件按其 模板/规范/示例 执行。

## 全局规范

### 六条总体原则

1. **首屏 3 秒原则**:标题 + 一句话简介(1-2 句,**不超过 120 字符**)让读者明白项目是什么、解决什么问题。简介须与包管理器描述字段(package.json `description` / pyproject `description` 等)、GitHub 仓库 description **三处一致**,不一致视为 README 缺陷。
2. **照抄可跑**:安装步骤必须可逐条复制粘贴执行,不允许"参考某某文档"式的省略;装完有客观判据(验证命令 + 预期输出)。
3. **密钥不进仓库**:真实密钥、密码、内网地址永不出现;README 中只写占位符(如 `sk-...`)与环境变量名。
4. **单一事实来源**:README 与实际依赖文件(requirements.txt / pyproject.toml / package.json 等)必须一致;依赖变更时 README 同步修改,二者不一致以依赖文件为准并视为 README 缺陷。
5. **语言统一**:团队内部仓库与中文项目用中文;面向国际社区的开源项目用英文;不混用。需要多语言时按 BCP 47 命名(如 `README.zh-CN.md`),`README.md` 保留给英文版。
6. **一个 README 一个目的**:README 只做"让人会用"的入口,不承载全部文档。全文超过约 300 行或安装步骤超过 10 步时,将详细内容拆分到 docs/(或 INSTALL.md、API.md),README 保留索引与最小路径。

### 格式要求(全文适用)

| 要求 | 说明 |
|------|------|
| 代码块必须标注语言 | ```bash、```python、```yaml 等,便于高亮与复制 |
| 命令不带 `$` / `#` 提示符 | 便于直接复制执行;命令与输出分开两个块 |
| 表格优先 | 枚举型信息(版本要求、参数、对比)一律用表格 |
| 标题层级规范 | H1 唯一;章节用 H2;小节用 H3;不跳级 |
| 图片有目的 | 装饰性图片不用;截图 / Demo GIF 仅用于展示运行效果,必须配文字说明 |
| 平台命令分开写 | macOS / Windows / Linux 命令不同就分块标注,不让读者猜 |
| TOC | 全文 ≥100 行必选;链接全部 H2 章节;长文可用 `<details>` 折叠 |

## 章节地图(顺序固定)

| 顺序 | 章节 | 必选性 | 适用性 | 分章契约 |
|------|------|--------|--------|---------|
| 1 | 项目名 + 简介,Badges、视觉展示 | 简介必选,Badges/视觉可选 | 全部;Badges、视觉开源优先 | [sections/identity.md](sections/identity.md) |
| 2 | 背景 / 特性 | 推荐 | 全部 | [sections/background.md](sections/background.md) |
| 3 | 安装(Install) | 必选 | 纯文档仓库可省 | [sections/install.md](sections/install.md) |
| 4 | 快速开始 / 使用(Usage) | 必选 | 纯文档仓库可省 | [sections/quick-start.md](sections/quick-start.md) |
| 5 | 使用示例(Examples) | 可选 | 全部 | [sections/usage-examples.md](sections/usage-examples.md) |
| 6 | 目录结构 | 推荐 | 全部 | [sections/structure.md](sections/structure.md) |
| 7 | 故障排查(FAQ) | 推荐 | 全部 | [sections/troubleshooting.md](sections/troubleshooting.md) |
| 8 | Roadmap | 可选 | 开源 | [sections/roadmap.md](sections/roadmap.md) |
| 9 | API Reference | 可选 | 库项目 | [sections/api-reference.md](sections/api-reference.md) |
| 10 | 贡献指南(Contributing) | 可选 | 开源 | [sections/contributing.md](sections/contributing.md) |
| 11 | License | 开源必选 | 全部,**必须是最后一节** | [sections/license.md](sections/license.md) |

取舍速查:内部项目省 Badges / Roadmap / 贡献指南;库项目加 API Reference;纯文档仓库省安装与快速开始。

## 全局自检(与各分章"必须"项互补,不重复;章内项见各分章)

- [ ] 代码块全部标注语言,命令不带提示符
- [ ] 与依赖文件、配置模板(config.example)内容一致
- [ ] 无过时信息(版本号、链接、目录名);无失效链接(外链、锚点、相对路径)
- [ ] 全文 ≥100 行时已包含 TOC
