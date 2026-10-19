# 安装(Install)

> 必选性:**必选**(纯文档仓库可省)| 适用性:全部 | README 的核心章节

## 模板

```markdown
## 安装

### 环境要求

| 依赖 | 版本 | 说明 |
|---|---|---|
| 操作系统 | {macOS / Windows / Linux} | {差异说明} |
| {语言运行时} | {≥ X.Y(推荐 X.Z)} | {哪个依赖卡的下限} |
| {外部服务/账号} | — | {申请地址} |

### 1. 安装 {运行时}(已安装可跳过)

### 2. 创建虚拟环境并安装依赖

### 3. 配置密钥(环境变量)

### 4. 初始化配置与目录

### 5. 验证安装
```

## 规范

**必须做**:

- **Prerequisites 表**放在步骤前,读者先自检再动手:依赖项 / **最低版本及原因**(如"Python ≥ 3.10(markitdown 硬性要求)",不允许只写"较新版本")/ 获取方式(下载地址、申请入口)
- 步骤**编号**(1、2、3…),每步只做一件事,目的写在该步标题里;已具备条件可跳过的标注"(已安装可跳过)"
- 每步结构 = 一句话说明 + 一个代码块 +(可选)预期输出
- 命令按"从零到可验证"排序:运行时 → 虚拟环境 → 依赖 → 配置/密钥 → 验证
- **密钥**:只写占位符(`sk-...`)与环境变量名;给出持久化方式(写入 shell profile);用 `.env` 承载时提醒加入 `.gitignore`;说明代码/配置中如何被引用(如 `${ENV_VAR}` 占位符自动替换)
- **验证**:章节结尾必须提供验证命令与**预期输出**(如"应输出 `deps ok`"),推荐两级——依赖冒烟(`python -c "import xxx; print('deps ok')"`,不调外部服务)/ 单元测试(应为 mock,不产生外部调用与费用)
- 平台差异(macOS / Windows)显式分块标注
- **(有非常规依赖时)**独立 Dependencies 小节:每项写清是什么、为什么需要、怎么装/怎么申请;依赖清单文件不在仓库根目录时**必须写明完整路径**(如 `.claude/skills/kb/requirements.txt`);dev / test 依赖与运行依赖分开说明

**建议做**:

- 最低版本与推荐版本同时给(如"≥ 3.10,推荐 3.12")
- 验证两级都给,冒烟在前(更快)

**禁止做**:

- "参考某某文档"式省略,步骤不可逐条复制执行
- 真实密钥、密码、内网地址出现在 README 或任何入库文件
- 命令带 `$` / `#` 提示符

## Python 项目依赖惯例

工具链选择:

| 场景 | 推荐方案 | 说明 |
|------|---------|------|
| 本地应用 / 脚本 / 工具项目(不发包) | `venv` + `requirements.txt` + pip | 最简单通用,零额外工具 |
| 要发布到 PyPI 的包 / 多人协作需锁版本 | `pyproject.toml` + lock 文件(uv / poetry) | 现代标准;`uv.lock` 取代手写 requirements |
| 简单项目但追求可复现部署 | requirements.txt + `pip freeze > requirements.lock` 固化 | 声明与锁定分离 |

- 版本策略:应用可用 `>=` 声明,验证通过后 `pip freeze` 固化为 lock;库用 `>=` 范围声明,兼容性优先
- Python 最低版本必须显式声明,**并注明是哪个依赖卡出的下限**
- 虚拟环境是标配:README 必含创建(`python -m venv .venv`)与激活命令,并标注 Windows 差异(`.venv\Scripts\activate`)
- 测试 / 开发依赖与运行依赖分离:`requirements-dev.txt` 或单列一行 `pip install pytest`
- 可选加速工具(如 uv)作为折叠小节或附注,不作为主线(主线保持零额外安装)
- 反模式:给不发包的简单项目强行上 pyproject + 打包配置。工具为项目服务,不为简历服务

## 示例(Python / macOS 主体)

````markdown
### 1. 安装 Python 3.12(已 ≥3.10 可跳过)

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

### 3. 配置 API Key(环境变量)

```bash
export MY_API_KEY="sk-..."        # 申请地址:https://...
# 持久化:追加到 ~/.zshrc
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
