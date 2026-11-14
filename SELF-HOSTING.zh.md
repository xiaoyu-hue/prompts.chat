<p align="center">
  <a href="SELF-HOSTING.md">English</a> · <strong>简体中文</strong>
</p>

# 自托管指南

## 功能特性

- **精选提示词库** —— 内置 100+ 条经过社区检验的高质量提示词，适用于 ChatGPT、Claude、Gemini、Llama、Mistral 等 AI 模型
- **发现与浏览** —— 按分类、标签浏览提示词，或使用 AI 驱动的语义搜索
- **创建与分享提示词** —— 提交你自己的提示词，支持纯文本、结构化（JSON/YAML）以及带多媒体的格式
- **版本管理** —— 内置版本记录与变更请求机制（类似 Pull Request），可追踪提示词的每次改动
- **个性化订阅流** —— 订阅感兴趣的分类，获取为你定制的提示词信息流
- **私有提示词** —— 提示词可以设为仅自己可见，也可以分享给社区
- **投票与排行榜** —— 给提示词点赞，通过 PromptMasters 排行榜发现最受欢迎的提示词
- **多语言支持** —— 支持英语、西班牙语、日语、土耳其语和中文

## 优势

- **释放 AI 潜力：** 不必再为提示词工程头疼——直接使用来自 14.1 万 star 社区、久经实战检验的提示词
- **节省时间：** 一键复制提示词、在页面内直接填写变量，立刻在任何 AI 对话中使用
- **社区共建的质量：** 每条提示词都经由社区通过变更请求与投票不断打磨
- **可私有化部署：** 为你所在的团队或组织部署一套白标（可完全替换成自己品牌）提示词库，品牌、主题、登录方式均可自定义
- **CC0 授权：** 所有提示词均属公共领域——无论商用还是自用，都可以自由使用

## 快速了解

**基本要求：**

- **授权方式：** 免费开源（CC0 协议）
- **访问权限：** 浏览无需账号；登录 GitHub / Google 后可创建与收藏提示词
- **可用性：** 已在 [prompts.chat](https://prompts.chat) 正式上线

---

本指南介绍如何把 **prompts.chat** 部署到你自己的私有服务器上，以获得更好的隐私性与可定制性。

## 前置条件

- **Node.js** 24.x
- **PostgreSQL** 数据库
- **npm**

## 推荐数据库

prompts.chat 需要 PostgreSQL。如需托管式 PostgreSQL 数据库，我们推荐 [Neon](https://get.neon.com/VqfnMo4)：它提供 Serverless Postgres、连接池与数据库分支能力，很适合自托管的 prompts.chat 部署场景。

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

## 环境变量

参照 `.env.example` 创建一个 `.env` 文件：

```bash
# 数据库
DATABASE_URL="postgresql://user:password@localhost:5432/prompts"

# 登录认证（任选一种方式）
# GitHub OAuth
AUTH_GITHUB_ID="your-github-client-id"
AUTH_GITHUB_SECRET="your-github-client-secret"

# 或 Google OAuth
AUTH_GOOGLE_ID="your-google-client-id"
AUTH_GOOGLE_SECRET="your-google-client-secret"

# NextAuth
AUTH_SECRET="generate-a-random-secret"

# 可选：AI 语义搜索
OPENAI_API_KEY="your-openai-api-key"
```

## 安装部署

### 快速开始（推荐）

创建一个全新的 prompts.chat 实例，这是最快的方式：

```bash
npx prompts.chat new my-prompt-library
cd my-prompt-library
```

这条命令会：

1. 克隆一份干净的仓库副本（不含开发相关文件）
2. 安装依赖
3. 启动交互式配置向导

### 手动安装

1. **克隆仓库**
   ```bash
   git clone https://github.com/f/prompts.chat.git
   cd prompts.chat
   ```

2. **安装依赖**
   ```bash
   npm install
   ```

3. **运行交互式配置向导**
   ```bash
   npm run setup
   ```
   向导会引导你完成以下配置：

   - **品牌** —— 应用名称、Logo、描述
   - **主题** —— 主色、圆角、界面风格
   - **登录认证** —— GitHub、Google、Apple、Azure AD 或邮箱密码
   - **语言** —— 从 16 种受支持的语言中选择
   - **功能开关** —— 私有提示词、分类、标签、评论、AI 搜索、AI 生成、MCP 支持

4. **配置环境变量**
   ```bash
   cp .env.example .env
   # 编辑 .env，填入你的数据库与认证凭证
   ```

5. **执行数据库迁移**
   ```bash
   npm run db:migrate
   ```

6. **导入初始数据**（可选）
   ```bash
   npm run db:seed
   ```

7. **启动开发服务器**
   ```bash
   npm run dev
   ```

8. **构建生产版本**
   ```bash
   npm run build
   npm run start
   ```

## 配置说明

配置向导（`npm run setup`）会自动生成 `prompts.config.ts`。你也可以手动编辑它：

```typescript
// 设为 true 即可使用你自己的品牌，替换掉 prompts.chat 的品牌
const useCloneBranding = true;

export default defineConfig({
  // 品牌
  branding: {
    name: "Your Prompt Library",
    logo: "/your-logo.svg",
    logoDark: "/your-logo-dark.svg",
    description: "Your custom description",
  },

  // 主题
  theme: {
    radius: "sm",        // "none" | "sm" | "md" | "lg"
    variant: "default",  // "flat" | "default" | "brutal"
    colors: {
      primary: "#6366f1",
    },
  },

  // 登录认证
  auth: {
    provider: "github",  // "credentials" | "github" | "google" | "azure"
    allowRegistration: true,
  },

  // 功能开关
  features: {
    privatePrompts: true,
    changeRequests: true,
    categories: true,
    tags: true,
    aiSearch: false,  // 需要 OPENAI_API_KEY
    promptEnhancer: false,  // /developers 页面的提示词增强器 + /api/improve-prompt 接口（需要 OPENAI_API_KEY）
  },

  // 首页
  homepage: {
    useCloneBranding,  // 在首页使用你的品牌
    achievements: {
      enabled: !useCloneBranding,  // 隐藏 prompts.chat 的成就展示
    },
    sponsors: {
      enabled: !useCloneBranding,  // 隐藏 prompts.chat 的赞助商
    },
  },

  // 国际化
  i18n: {
    locales: ["en", "es", "ja", "tr", "zh"],
    defaultLocale: "en",
  },
});
```

### 白标模式（Clone Branding）

当 `useCloneBranding` 设为 `true` 时，首页会：

- 用你的**品牌名称**作为主标题
- 在标题下方显示你的**品牌描述**
- 用你的 **Logo** 替代视频作为背景水印
- 隐藏「部署你自己的私有服务器」按钮
- 隐藏成就展示区（福布斯、GitHub star 等）
- 隐藏赞助商链接与「成为赞助商」按钮

对于希望部署一套完全不带 prompts.chat 品牌痕迹的白标提示词库的组织来说，这是最理想的配置。

## 获取帮助

遇到问题或有疑问，请提交 [GitHub Issue](https://github.com/f/prompts.chat/issues)。

---

<sub>本文档由英文版 SELF-HOSTING.md 翻译而来，如中英文表述存在出入，请以<a href="SELF-HOSTING.md">英文原版</a>为准。</sub>
