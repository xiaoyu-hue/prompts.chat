<p align="center">
  <a href="README.md">English</a> · <strong>简体中文</strong>
</p>

<h1 align="center">
  <a href="https://prompts.chat">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://prompts.chat/logo-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://prompts.chat/logo.svg">
      <img height="60" alt="prompts.chat" src="https://prompts.chat/logo.svg">
    </picture>
    <br>
    prompts.chat
  </a>
</h1>

<p align="center">
  <strong>全球最大的开源 AI 提示词库</strong><br>
  <sub>兼容 ChatGPT、Claude、Gemini、Llama、Mistral 等模型</sub>
</p>
<p align="center">
  <sub>原名 Awesome ChatGPT Prompts</sub>
</p>

<p align="center">
  <a href="https://prompts.chat"><img src="https://img.shields.io/badge/Website-prompts.chat-blue?style=flat-square" alt="官网"></a>
  <a href="https://github.com/sindresorhus/awesome"><img src="https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg" alt="Awesome"></a>
  <a href="https://huggingface.co/datasets/fka/prompts.chat"><img src="https://img.shields.io/badge/🤗-Hugging_Face-yellow?style=flat-square" alt="Hugging Face"></a>
  <a href="https://deepwiki.com/f/prompts.chat"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
</p>

<p align="center">
  <a href="https://prompts.chat/prompts">🌐 浏览提示词</a> •
  <a href="https://fka.gumroad.com/l/art-of-chatgpt-prompting">📖 阅读本书</a> •
  <a href="https://raw.githubusercontent.com/f/prompts.chat/main/PROMPTS.md">📄 在 GitHub 查看</a> •
  <a href="#-自托管">🚀 自托管</a>
</p>

<p align="center">
  <sub>
    🏆 获<a href="https://www.forbes.com/sites/tjmccue/2023/01/19/chatgpt-success-completely-depends-on-your-prompt/">《福布斯》</a>专题报道 ·
    🎓 被<a href="https://www.huit.harvard.edu/news/ai-prompts">哈佛大学</a>、<a href="https://etc.cuit.columbia.edu/news/columbia-prompt-library-effective-academic-ai-use">哥伦比亚大学</a>引用 ·
    📄 <a href="https://scholar.google.com/citations?user=AZ0Dg8YAAAAJ&hl=en">40+ 篇学术论文引用</a> ·
    ❤️ Hugging Face 上<a href="https://huggingface.co/datasets/fka/prompts.chat">获赞最多</a>的数据集<br>
    ⭐ GitHub 14.3 万+ star ·
    🏅 <a href="https://spotlights-feed.github.com/spotlights/prompts-chat/index/">GitHub 官方精选项目</a> ·
    🚀 最早的提示词库（2022 年 12 月）
  </sub>
</p>

<p align="center">
  <sub><strong>深受 AI 先驱喜爱：</strong></sub><br>
  <sub>
    <a href="https://x.com/gdb/status/1602072566671110144"><strong>Greg Brockman</strong></a>（OpenAI 联合创始人）·
    <a href="https://x.com/woj_zaremba/status/1601362952841760769"><strong>Wojciech Zaremba</strong></a>（OpenAI 联合创始人）·
    <a href="https://x.com/clementdelangue/status/1830976369389642059"><strong>Clement Delangue</strong></a>（Hugging Face CEO）·
    <a href="https://x.com/ashtom/status/1887250944427237816"><strong>Thomas Dohmke</strong></a>（GitHub 前 CEO）
  </sub>
</p>

---

## 这是什么？

一份经过精挑细选的 AI 对话模型**提示词**合集。它最初是为 ChatGPT 而创作，但这些提示词同样适用于任何现代 AI 助手。

| 浏览提示词 | 数据格式 |
|----------------|--------------|
| [prompts.chat](https://prompts.chat/prompts) | [prompts.csv](prompts.csv) |
| [PROMPTS.md](https://raw.githubusercontent.com/f/prompts.chat/main/PROMPTS.md) | [Hugging Face 数据集](https://huggingface.co/datasets/fka/prompts.chat) |

**想贡献提示词？** 在 [prompts.chat/prompts/new](https://prompts.chat/prompts/new) 提交即可——它们会自动同步到本仓库。

---

## 🤖 Bots 与 Bot 团队

prompts.chat 同时也托管**常驻在线的 AI 智能体（Bots）**，以及它们协作组成的团队。

- **[Bots](https://prompts.chat/bots)** —— 分享与发现各类 Bot（OpenClaw、Hermes Agent、Grok Bot 等）。每个 Bot 页面都提供按平台划分的安装说明、它所需的运行环境（**云端**、**用户本机**，或**两者皆可**）、推荐搭配组合、点赞、评论与变更请求。
- **[Bot Teams](https://prompts.chat/bots/teams)** —— 由多个 Bot 互相交接工作组成的团队，以交互式关系图展示。你可以给团队点赞，也能一键安装团队内的全部 Bot。精选团队会出现在首页，**Teams** 入口位于顶部导航栏。
- **用户主页** —— 每位用户的主页都设有 Bots 与 Teams 标签页，并显示对应数量。
- **内容管理** —— Bot 与团队可以被设为不公开，从而从公开列表中隐藏。

团队数据同样提供 JSON 接口：`GET /api/teams?sort=newest`（还支持 `oldest` 或 `upvotes` 排序，通过 `page` 与 `perPage` 分页）。

---

## 📖 交互式提示词之书

用我们**免费、可交互的指南**学习提示词工程——31+ 个章节，从基础概念一直讲到思维链推理、少样本学习、AI 智能体等进阶技巧。较新的章节还覆盖了**从提示词到团队**的演进路径（提示词 → 技能 → 智能体 → Bot → 团队）、常驻 Bot、智能体团队、计算机操作、谁能给 Bot 派活，以及 **用 AI 做软件开发**（氛围编程与智能体工程的对比、算力投入档位、自主编码智能体），并提供 17 种语言版本。

**[开始阅读 →](https://fka.gumroad.com/l/art-of-chatgpt-prompting)**（源文件：[src/content/book](https://github.com/f/prompts.chat/tree/main/src/content/book)）

---

## 🎮 儿童提示词

<p>
  <a href="https://prompts.chat/kids">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://prompts.chat/promi-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://prompts.chat/promi.svg">
      <img height="60" alt="Promi" src="https://prompts.chat/promi.svg" align="left">
    </picture>
  </a>
</p>

一场基于游戏的互动式冒险，通过有趣的解谜与故事，教 8–14 岁的孩子如何与 AI 沟通。

**[开始游玩 →](https://prompts.chat/kids)**

<br clear="left">

---

## 🚀 自托管

部署一套属于你自己的私有提示词库，支持自定义品牌、主题与登录认证。

**快速开始：**
```bash
npx prompts.chat new my-prompt-library
cd my-prompt-library
```

**手动安装：**
```bash
git clone https://github.com/f/prompts.chat.git
cd prompts.chat
npm install && npm run setup
```

安装向导会为你配置品牌信息、主题、登录方式（GitHub / Google / Azure AD）以及功能开关。

**推荐数据库：** prompts.chat 使用 PostgreSQL。如需托管数据库，我们推荐 [Neon](https://get.neon.com/VqfnMo4)。

<div>
  <p>赞助商</p>
  <a href="https://get.neon.com/VqfnMo4">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/neon-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/neon.svg">
      <img width="250px" alt="Neon Logo fallback" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/neon-dark.svg">
    </picture>
  </a>
</div>

📖 **[完整自托管指南](SELF-HOSTING.zh.md)**（[English](SELF-HOSTING.md)）• 🐳 **[Docker 指南](DOCKER.zh.md)**（[English](DOCKER.md)）

---

## 🔌 集成

### 命令行工具（CLI）
```bash
npx prompts.chat
```

### Claude Code 插件
```
/plugin marketplace add f/prompts.chat
/plugin install prompts.chat@prompts.chat
```
📖 [插件文档](CLAUDE-PLUGIN.md)（英文）

### MCP Server
在你的 AI 工具中把 prompts.chat 当作 MCP 服务器使用。

**远程模式（推荐）：**
```json
{
  "mcpServers": {
    "prompts.chat": {
      "url": "https://prompts.chat/api/mcp"
    }
  }
}
```

**本地模式：**
```json
{
  "mcpServers": {
    "prompts.chat": {
      "command": "npx",
      "args": ["-y", "prompts.chat", "mcp"]
    }
  }
}
```

提供的工具覆盖提示词与技能，以及 Bot（`search_bots`、`get_bot`、`save_bot`、`list_my_bots`、`get_my_bot`）和 Bot 团队（`list_teams`、`get_team`、`save_team`）。

📖 [MCP 文档](https://prompts.chat/docs/api)

---

## 💖 赞助商

<p align="center">
  <!-- Neon (py-1) -->
  <a href="https://get.neon.com/VqfnMo4">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/neon-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/neon.svg">
      <img height="30" alt="Neon" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/neon.svg">
    </picture>
  </a>&nbsp;&nbsp;
  <!-- Clemta -->
  <a href="https://clemta.com/?utm_source=prompts.chat">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/clemta-dark.webp">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/clemta.webp">
      <img height="35" alt="Clemta" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/clemta.webp">
    </picture>
  </a>&nbsp;&nbsp;
  <!-- Wiro (py-1) -->
  <a href="https://wiro.ai/?utm_source=prompts.chat">
    <img height="30" alt="Wiro" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/wiro.png">
  </a>&nbsp;&nbsp;
  <!-- Cognition -->
  <a href="https://wind.surf/prompts-chat">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/cognition-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/cognition.svg">
      <img height="35" alt="Cognition" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/cognition.svg">
    </picture>
  </a>&nbsp;&nbsp;
  <!-- CodeRabbit (py-1) -->
  <a href="https://coderabbit.link/fatih">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/coderabbit-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/coderabbit.svg">
      <img height="30" alt="CodeRabbit" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/coderabbit.svg">
    </picture>
  </a>&nbsp;&nbsp;
  <!-- Sentry (py-1) -->
  <a href="https://sentry.io/?utm_source=prompts.chat">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/sentry-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/sentry.svg">
      <img height="30" alt="Sentry" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/sentry.svg">
    </picture>
  </a>&nbsp;&nbsp;
  <!-- Each Labs (py-[6px]) -->
  <a href="https://www.eachlabs.ai/?utm_source=promptschat&utm_medium=referral">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/eachlabs-dark.png">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/eachlabs.png">
      <img height="28" alt="Each Labs" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/eachlabs.png">
    </picture>
  </a>&nbsp;&nbsp;
  <!-- CommandCode (py-1) -->
  <a href="https://commandcode.ai/?utm_source=prompts.chat">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/commandcode-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/commandcode.svg">
      <img height="30" alt="CommandCode" src="https://raw.githubusercontent.com/f/prompts.chat/main/public/sponsors/commandcode.svg">
    </picture>
  </a>
</p>

<p align="center">
  <sub>由 <a href="https://wind.surf/prompts-chat">Windsurf</a> 与 <a href="https://devin.ai">Devin</a> 构建</sub><br>
  <a href="https://github.com/sponsors/f/sponsorships?sponsor=f&tier_id=558224&preview=false"><strong>成为赞助商 →</strong></a>
</p>

---

## 👥 贡献者

<a href="https://github.com/f/prompts.chat/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=f/prompts.chat" />
</a>

---

## 📜 许可协议

本项目采用双协议授权：

- **源代码与站方原创内容**采用 [MIT 协议](LICENSE-MIT)，
  包括 [`src/content/book`](src/content/book) 目录下的交互式书籍内容。
- **提示词内容与数据**（prompts.csv、PROMPTS.md、用户提交的提示词）以 [CC0 1.0 通用协议](LICENSE-CC0) 贡献至公共领域。

---

<sub>本文档由英文版 README 翻译而来，如中英文表述存在出入，请以<a href="README.md">英文原版</a>为准。</sub>
