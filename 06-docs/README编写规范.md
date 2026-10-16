# README 编写规范

## 1. 文档概述

### 1.1 目的

本规范定义 README 的整体结构、安装章节写法、依赖描述方式与质量自检标准，适用于所有新建或补全 README 的仓库，重点解决"读者照着 README 能否一次装好、跑通"的问题。

### 1.2 适用范围

- 新仓库创建 README
- 存量仓库补全 / 修订安装与依赖说明
- README 的评审与自检

### 1.3 参考依据

| 来源 | 说明 |
|------|------|
| [GitHub Docs — About READMEs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes) | GitHub 官方对 README 用途的定义 |
| [Standard ReadMe Spec](https://github.com/RichardLitt/standard-readme) | 被数万仓库采用的 README 结构规范 |
| Make a README / Awesome README | 社区最佳实践集 |
| Python 打包生态惯例（pip / venv / uv / pyproject） | 依赖描述与版本策略依据 |

---

## 2. 总体原则

1. **首屏 3 秒原则**：标题 + 一句话简介（1-2 句，**不超过 120 字符**）让读者明白项目是什么、解决什么问题。读者决定是否继续读，就在首屏。简介须与包管理器描述字段（package.json `description` / pyproject `description` 等）、GitHub 仓库 description **三处一致**，不一致视为 README 缺陷。
2. **照抄可跑**：安装步骤必须可逐条复制粘贴执行，不允许"参考某某文档"式的省略；装完有客观判据（验证命令 + 预期输出）。
3. **密钥不进仓库**：真实密钥、密码、内网地址永不出现；README 中只写占位符（如 `sk-...`）与环境变量名。
4. **单一事实来源**：README 与实际依赖文件（requirements.txt / pyproject.toml / package.json 等）必须一致；依赖变更时 README 同步修改，二者不一致以依赖文件为准并视为 README 缺陷。
5. **语言统一**：团队内部仓库与中文项目用中文；面向国际社区的开源项目用英文；不混用。需要多语言时按 BCP 47 命名（如 `README.zh-CN.md`），`README.md` 保留给英文版。
6. **一个 README 一个目的**：README 只做"让人会用"的入口，不承载全部文档。全文超过约 300 行或安装步骤超过 10 步时，将详细内容拆分到 docs/（或 INSTALL.md、API.md），README 保留索引与最小路径。

---

## 3. README 结构规范

### 3.1 章节清单

| 顺序 | 章节 | 必选性 | 适用性 | 内容要求 |
|------|------|--------|--------|---------|
| 1 | `# 项目名` + 一句话简介 | 必选 | 全部 | H1 全文唯一；简介见原则 1（<120 字符、三处一致） |
| 2 | Badges（CI / License / 版本） | 可选 | 开源 | 3-5 个为宜，只放有实际意义的，不堆砌 |
| 3 | 视觉展示（截图 / Demo GIF / 终端录制） | 可选 | 开源优先 | 放简介后、首屏内；CLI 工具可用终端录制（VHS / asciinema）；必须配文字说明 |
| 4 | `## 背景` 或 `## 特性` | 推荐 | 全部 | 为什么做、核心特性 3-6 条，写收益不写能力罗列；详细内容链接到 docs/ |
| 5 | `## 安装（Install）` | 必选 | 纯文档仓库可省 | 见第 4 节，是 README 的核心 |
| 6 | `## 快速开始 / 使用（Usage）` | 必选 | 纯文档仓库可省 | 最小可运行示例，达标线见 3.3 |
| 7 | `## 使用示例（Examples）` | 可选 | 全部 | 2-3 个由浅入深的完整用例 |
| 8 | `## 目录结构` | 推荐 | 全部 | 仓库布局树 + 关键目录一句话说明 |
| 9 | `## 故障排查（FAQ）` | 推荐 | 全部 | 已知坑及解法，按"现象 → 原因 → 解法"组织 |
| 10 | `## Roadmap` | 可选 | 开源 | checkbox 列表，链接到 issues / milestone |
| 11 | `## API Reference` | 可选 | 库项目 | 描述导出接口；可仅链接 API.md 或文档站 |
| 12 | `## 贡献指南（Contributing）` | 可选 | 开源 | 链接 CONTRIBUTING.md、issues；即使暂不接受贡献也可声明立场 |
| 13 | `## License` | 开源必选 | 全部 | **必须是最后一节**；SPDX 标识（如 `MIT`）；未授权写 `UNLICENSED`；与 LICENSE 文件一致 |
| — | 目录（TOC） | ≥100 行必选 | 全部 | 链接全部 H2 章节；长文可用 `<details>` 折叠 |

### 3.2 格式要求

| 要求 | 说明 |
|------|------|
| 代码块必须标注语言 | \`\`\`bash、\`\`\`python、\`\`\`yaml 等，便于高亮与复制 |
| 命令不带 `$` / `#` 提示符 | 便于直接复制执行；命令与输出分开两个块 |
| 表格优先 | 枚举型信息（版本要求、参数、对比）一律用表格 |
| 标题层级规范 | H1 唯一；章节用 H2；小节用 H3；不跳级 |
| 图片有目的 | 装饰性图片不用；截图 / Demo GIF 仅用于展示运行效果，必须配文字说明 |
| 平台命令分开写 | macOS / Windows / Linux 命令不同就分块标注，不让读者猜 |

### 3.3 快速开始量化标准

快速开始（Quick Start / Usage）章节的达标线：

- **≤5 步**：从获取代码到跑通第一个用例不超过 5 个步骤；超出时将过程脚本化（setup.sh / Makefile / npm scripts）
- **2 分钟**：在新机器上实测，2 分钟内可跑通（不含大文件下载）
- **第一个用例要最小**：选最典型、零配置、无副作用的路径；复杂场景放"使用示例"章节
- 安装解决"装好"，快速开始解决"跑通第一个用例"，两者验证命令可以复用（见 4.4）

---

## 4. 安装章节规范（核心）

### 4.1 Prerequisites 前置条件（必选）

以表格放在安装步骤之前，读者先自检再动手：

| 列 | 要求 |
|----|------|
| 依赖项 | 语言运行时、系统工具、外部服务账号 |
| 版本要求 | **必须给出最低版本及原因**（如"Python ≥ 3.10（markitdown 硬性要求）"），不允许只写"较新版本" |
| 获取方式 | 下载地址 / 申请入口（如 API Key 的申请页面） |

### 4.2 步骤组织（必选）

- 步骤**编号**（1、2、3…），每步只做一件事，目的写在该步骤标题里
- 每步结构 = 一句话说明 + 一个代码块 +（可选）预期输出
- 已具备条件的读者可跳过：步骤标题标注"（已安装可跳过）"
- 命令按"从零到可验证"排序：运行时 → 虚拟环境 → 依赖 → 配置/密钥 → 验证

### 4.3 敏感信息处理（必选）

```bash
# 正确：环境变量 + 占位符
export MY_API_KEY="sk-..."

# 错误：真实密钥写进 README 或任何入库文件
```

- 给出持久化方式（写入 shell profile）
- 若项目用 `.env` / 本地配置文件承载密钥，提醒将其加入 `.gitignore`
- 说明密钥在代码 / 配置中如何被引用（如 `${ENV_VAR}` 占位符自动替换）

### 4.4 验证步骤（必选）

安装章节结尾必须提供验证命令与预期输出，推荐两级：

| 级别 | 方式 | 示例 |
|------|------|------|
| 依赖冒烟 | import / 版本检查，不调外部服务 | `python -c "import xxx; print('deps ok')"` |
| 单元测试 | 跑项目自带测试（应为 mock，不产生外部调用与费用） | `python -m pytest tests/ -q` |

预期输出必须写明（如"应输出 `deps ok`"），让安装成功与否有客观判据。

### 4.5 依赖小节（有非常规依赖时必选）

Standard ReadMe 要求：当存在包管理器之外的依赖（系统库、外部服务、私有源）时，必须有独立的 Dependencies 小节说明：

- 每项写清：是什么、为什么需要、怎么装 / 怎么申请
- 依赖清单文件不在仓库根目录时，**必须写明完整路径**（如 `.claude/skills/kb/requirements.txt`）
- dev / test 依赖与运行依赖分开说明

---

## 5. Python 项目依赖描述惯例

### 5.1 工具链选择

| 场景 | 推荐方案 | 说明 |
|------|---------|------|
| 本地应用 / 脚本 / 工具项目（不发包） | `venv` + `requirements.txt` + pip | 最简单通用，零额外工具 |
| 要发布到 PyPI 的包 / 多人协作需锁版本 | `pyproject.toml` + lock 文件（uv / poetry） | 现代标准；`uv.lock` 取代手写 requirements |
| 简单项目但追求可复现部署 | requirements.txt + `pip freeze > requirements.lock` 固化 | 声明与锁定分离 |

> 反模式：给不发包的简单项目强行上 pyproject + 打包配置。工具为项目服务，不为简历服务。

### 5.2 版本策略

| 项目类型 | 策略 |
|---------|------|
| 应用 | requirements.txt 可用 `>=` 声明；验证通过后 `pip freeze` 固化实际版本作为 lock |
| 库 | 用 `>=` 范围声明，兼容性优先 |
| Python 版本 | README 必须显式声明最低版本，**并注明是哪个依赖卡出的下限**；推荐版本与最低版本可同时给（如"≥ 3.10，推荐 3.12"） |

### 5.3 虚拟环境与 dev 依赖

- 虚拟环境是标配：README 必须包含创建（`python -m venv .venv`）与激活命令，并标注 Windows 差异（`.venv\Scripts\activate`）
- 测试 / 开发依赖与运行依赖分离：`requirements-dev.txt` 或在 README 单列一行 `pip install pytest`
- 可选加速工具（如 uv）作为折叠小节或附注，不作为主线（主线保持零额外安装）

---

## 6. 质量自检清单

README 完成后逐项自检，全部满足才视为达标：

- [ ] 标题下 3 行内说清项目是什么、解决什么问题
- [ ] 简介不超过 120 字符，与包描述字段、GitHub description 三处一致
- [ ] Prerequisites 表完整，语言运行时含最低版本及依据
- [ ] 安装步骤编号清晰，每步可复制执行，无"参考其他文档"式省略
- [ ] 平台差异（macOS / Windows）显式标注
- [ ] 密钥只出现占位符与环境变量名，并说明获取入口
- [ ] 结尾有验证命令 + 预期输出
- [ ] 依赖清单文件路径与仓库实际路径一致
- [ ] dev / test 依赖单独说明
- [ ] 代码块全部标注语言，命令不带提示符
- [ ] 与依赖文件、配置模板（config.example）内容一致
- [ ] 无过时信息（版本号、链接、目录名）
- [ ] 全文 ≥100 行时已包含 TOC
- [ ] 无失效链接（重点：外链、锚点、相对路径）
- [ ] License 为最后一节，使用 SPDX 标识

---

## 7. 模板

### 7.1 README 骨架模板

```markdown
<!-- 使用说明：{花括号} 为占位符；标注"可选"的章节按适用性（开源/内部/库项目）取舍，
     定稿时删除不用的章节与本注释 -->

# {项目名}

{一句话简介：是什么 + 解决什么问题，<120 字符，与包描述 / GitHub description 一致}

<!-- 可选（开源）：Badges，3-5 个（CI / License / 版本） -->

<!-- 可选：视觉展示——截图 / Demo GIF / 终端录制，放首屏，必须配文字说明 -->

<!-- ≥100 行时在此加 TOC（长文可用 <details> 折叠） -->

## 背景

{为什么做这个项目，1-2 段。核心特性 3-6 条，写收益。}

## 安装

### 环境要求

| 依赖 | 版本 | 说明 |
|---|---|---|
| 操作系统 | {macOS / Windows / Linux} | {差异说明} |
| {语言运行时} | {≥ X.Y（推荐 X.Z）} | {哪个依赖卡的下限} |
| {外部服务/账号} | — | {申请地址} |

### 1. 安装 {运行时}（已安装可跳过）

### 2. 创建虚拟环境并安装依赖

### 3. 配置密钥（环境变量）

### 4. 初始化配置与目录

### 5. 验证安装

## 快速开始

{1-2 个最小可运行示例，≤5 步、2 分钟跑通。}

## 使用示例（可选）

{2-3 个由浅入深的完整用例。}

## 目录结构

{仓库布局树 + 关键目录一句话说明。}

## 故障排查

| 现象 | 原因 | 解法 |
|---|---|---|

## Roadmap（可选，开源）

{checkbox 列表，链接 issues。}

## API Reference（可选，库项目）

{描述导出接口，或链接 API.md / 文档站。}

## 贡献指南（可选，开源）

{链接 CONTRIBUTING.md 与 issues。}

## License

{SPDX 标识，如 MIT；未授权写 UNLICENSED。必须是最后一节。}
```

### 7.2 安装章节内嵌示例（Python / macOS 主体）

````markdown
### 1. 安装 Python 3.12（已 ≥3.10 可跳过）

```bash
brew install python@3.12
python3.12 --version        # 应输出 Python 3.12.x
```

### 2. 创建虚拟环境并安装依赖

```bash
cd {项目目录}
python3.12 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r {依赖清单路径}
```

### 3. 配置 API Key（环境变量）

```bash
export MY_API_KEY="sk-..."        # 申请地址：https://...
# 持久化：追加到 ~/.zshrc
```

### 4. 初始化配置与目录

```bash
cp config.example.yaml config.yaml
mkdir -p {运行所需目录}
```

### 5. 验证安装

```bash
python -c "import {核心依赖}; print('deps ok')"   # 应输出 deps ok
python -m pytest tests/ -q                        # 全部通过
```
````

---

## 8. 参考资料

- [GitHub Docs — About READMEs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)
- [Standard ReadMe Spec](https://github.com/RichardLitt/standard-readme)（[正式规范 spec.md](https://github.com/RichardLitt/standard-readme/blob/master/spec.md)）
- [pyproject.toml vs requirements.txt（pydevtools handbook）](https://pydevtools.com/handbook/explanation/pyproject-vs-requirements)
- [Make a README](https://www.makeareadme.com/)
- [Awesome README](https://github.com/matiassingers/awesome-readme)
- [Top 100 高星仓库 README 结构分析](https://dev.to/belal_zahran/the-github-readme-template-that-gets-stars-used-by-top-repos-4hi7)
- [Best-README-Template](https://github.com/othneildrew/Best-README-Template)
