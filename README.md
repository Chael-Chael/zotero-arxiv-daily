<p align="center">
  <a href="" rel="noopener">
 <img width=200px height=200px src="assets/logo.svg" alt="logo"></a>
</p>

<h3 align="center">Zotero-arXiv-Daily-Feishu</h3>

<div align="center">

  [![Status](https://img.shields.io/badge/status-active-success.svg)]()
  ![Stars](https://img.shields.io/github/stars/Chael-Chael/zotero-arxiv-daily?style=flat)
  [![License](https://img.shields.io/github/license/TideDra/zotero-arxiv-daily)](/LICENSE)

</div>

---

<p align="center"> 基于 <a href="https://github.com/TideDra/zotero-arxiv-daily">TideDra/zotero-arxiv-daily</a> 的飞书适配版，每日推送与你 Zotero 文献库相关的 arXiv 论文到飞书群。
    <br> 
</p>

> [!NOTE]
> 这是原项目的 Fork 版本，主要增加了**飞书机器人推送**支持，并优化了论文展示格式。

## 🆕 新增特性

相比原项目，本 Fork 版本新增：

- 📮 **飞书机器人推送** - 支持飞书自定义机器人，推送精美卡片消息
- 📊 **表格展示** - 论文以表格形式展示，包含序号、标题、arXiv ID、日期、链接
- 📅 **每日新论文 + 月度精选** - 分区推送前一天新论文和近一个月最相关论文
- 🌐 **双语摘要** - 同时展示英文原文和中文翻译摘要
- ⚙️ **灵活配置** - 可自定义每日/月度推送论文数量

---

## 🚀 快速开始

### 1. Fork 本仓库

### 2. 配置飞书自定义机器人

#### 步骤一：在群组中添加机器人

1. 进入目标飞书群组
2. 点击右上角 **设置** → **群机器人** → **添加机器人**
3. 选择 **自定义机器人**
4. 设置机器人名称和头像，点击 **添加**
5. **复制 webhook 地址**（格式：`https://open.feishu.cn/open-apis/bot/v2/hook/xxx`）

> [!WARNING]
> **请妥善保管 webhook 地址**，不要公开发布，避免被恶意调用。

#### 步骤二：（可选）配置签名校验

为提高安全性，建议开启签名校验：

1. 进入机器人配置页面
2. 在 **安全设置** 中选择 **签名校验**
3. **复制密钥**

### 3. 配置 GitHub Secrets

进入仓库 → **Settings** → **Secrets and variables** → **Actions**

#### 必需的 Secrets

| Key | 说明 | 示例 |
| :--- | :--- | :--- |
| `ZOTERO_ID` | Zotero 用户 ID（数字，非用户名）。[获取地址](https://www.zotero.org/settings/security) | `12345678` |
| `ZOTERO_KEY` | Zotero API 密钥。[获取地址](https://www.zotero.org/settings/security) | `AB5tZ877P2xxx` |
| `ARXIV_QUERY` | 目标 arXiv 类别，用 `+` 连接。[类别列表](https://arxiv.org/category_taxonomy) | `cs.AI+cs.CV+cs.LG` |
| `FEISHU_WEBHOOK_URL` | 飞书机器人 webhook 地址 | `https://open.feishu.cn/open-apis/bot/v2/hook/xxx` |

#### 可选的 Secrets

| Key | 说明 | 示例 |
| :--- | :--- | :--- |
| `FEISHU_SECRET` | 飞书机器人签名密钥（如开启签名校验）| `abc123secret` |
| `OPENAI_API_KEY` | LLM API 密钥。[SiliconFlow 免费申请](https://cloud.siliconflow.cn/i/b3XhBRAm) | `sk-xxx` |
| `OPENAI_API_BASE` | LLM API 地址 | `https://api.siliconflow.cn/v1` |
| `MODEL_NAME` | 模型名称 | `Qwen/Qwen2.5-7B-Instruct` |

### 4. 配置 Repository Variables

在 **Settings** → **Secrets and variables** → **Actions** → **Variables** 中添加：

| Key | 说明 | 默认值 |
| :--- | :--- | :--- |
| `DAILY_PAPER_NUM` | 每日新论文推送数量 | `5` |
| `MONTHLY_PAPER_NUM` | 月度精选论文数量 | `10` |
| `NOTIFY_METHOD` | 推送方式：`feishu` / `email` / `both` | `feishu` |
| `LANGUAGE` | 摘要翻译语言 | `Chinese` |
| `USE_LLM_API` | 使用云端 LLM（`1`）或本地（`0`）| `0` |
| `ZOTERO_IGNORE` | 忽略的 Zotero 文件夹（gitignore 风格）| |

### 5. 测试运行

1. 进入 **Actions** 标签页
2. 选择 **Test Workflow**
3. 点击 **Run workflow**

---

## 📖 工作原理

1. 从 Zotero 获取你的文献库
2. 从 arXiv RSS 获取前一天的新论文
3. 从 arXiv API 获取近一个月的论文
4. 使用 embedding 模型计算相关度（近期添加的论文权重更高）
5. 使用 LLM 生成中文翻译摘要
6. 通过飞书机器人推送卡片消息

---

## 📃 许可证

基于 AGPLv3 许可证分发。详见 `LICENSE`。

## ❤️ 致谢

- [TideDra/zotero-arxiv-daily](https://github.com/TideDra/zotero-arxiv-daily) - 原项目
- [pyzotero](https://github.com/urschrei/pyzotero)
- [arxiv](https://github.com/lukasschwab/arxiv.py)
- [sentence_transformers](https://github.com/UKPLab/sentence-transformers)
