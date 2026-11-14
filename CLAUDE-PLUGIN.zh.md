<p align="center">
  <a href="CLAUDE-PLUGIN.md">English</a> · <strong>简体中文</strong>
</p>

# Claude Code 插件

借助官方插件，你可以在 [Claude Code](https://code.claude.com) 里直接使用 prompts.chat：搜索提示词、发现技能、优化你的提示词，全程不用离开 IDE。

## 安装

先把 prompts.chat 的插件市场添加到 Claude Code：

```
/plugin marketplace add f/prompts.chat
```

然后安装插件：

```
/plugin install prompts.chat@prompts.chat
```

## 功能

| 功能 | 说明 |
|---------|-------------|
| **MCP Server** | 连接 prompts.chat 的 API，实时获取提示词 |
| **命令** | 提供 `/prompts.chat:prompts` 与 `/prompts.chat:skills` 两个斜杠命令 |
| **Agent** | Prompt Manager 与 Skill Manager 两个智能体，处理复杂工作流 |
| **技能（Skills）** | 自动激活的技能，用于发现提示词与技能 |

## 命令

### 搜索提示词

```
/prompts.chat:prompts <query>
/prompts.chat:prompts <query> --type IMAGE
/prompts.chat:prompts <query> --category coding
/prompts.chat:prompts <query> --tag productivity
```

**示例：**
```
/prompts.chat:prompts code review
/prompts.chat:prompts writing assistant --category writing
/prompts.chat:prompts midjourney --type IMAGE
/prompts.chat:prompts react developer --tag coding
```

### 搜索技能

```
/prompts.chat:skills <query>
/prompts.chat:skills <query> --category coding
/prompts.chat:skills <query> --tag automation
```

**示例：**
```
/prompts.chat:skills testing automation
/prompts.chat:skills documentation --category coding
/prompts.chat:skills api integration
```

## MCP 工具

插件通过 prompts.chat MCP 服务器提供以下工具：

### 提示词工具

| 工具 | 说明 |
|------|-------------|
| `search_prompts` | 按关键词、分类、标签或类型搜索提示词 |
| `get_prompt` | 获取指定提示词；传入 `variables` 可填充其中的 `${name}` 占位符 |
| `save_prompt` | 保存新提示词（需要 API Key） |
| `improve_prompt` | 用 AI 优化提示词 |

### 技能工具

| 工具 | 说明 |
|------|-------------|
| `search_skills` | 搜索 Agent Skills |
| `get_skill` | 获取某个技能及其全部文件 |
| `save_skill` | 创建多文件技能（需要 API Key） |
| `add_file_to_skill` | 向已有技能添加文件 |
| `update_skill_file` | 更新技能中的某个文件 |
| `remove_file_from_skill` | 从技能中删除某个文件 |

### Bot 工具

| 工具 | 说明 |
|------|-------------|
| `search_bots` | 按关键词、平台、分类和标签搜索公开的 Bot 目录（开启 AI 搜索时按语义排序） |
| `get_bot` | 按 id 或 slug 获取某个公开 Bot，并附各平台的安装方式 |
| `save_bot` | 创建或更新你自己的 Bot（按 id、slug 或名称做幂等 upsert；需要 API Key） |
| `list_my_bots` | 列出你自己的 Bot，含私有 Bot（需要 API Key） |
| `get_my_bot` | 获取你自己某个 Bot 的完整定义（需要 API Key） |

工具返回的 `structuredContent` 与其 `outputSchema` 保持一致，并附带资源链接。支持分页的工具会返回 `nextCursor`，把它作为 `cursor` 参数传回即可翻页。

### 资源（Resources）

| URI | 内容 |
|-----|----------|
| `prompts-chat://prompts/{id}` | 以 Markdown 格式呈现的提示词 |
| `prompts-chat://skills/{id}` | 某个技能的全部文件 |
| `prompts-chat://skills/{id}/files/{path}` | 技能中的单个文件 |
| `prompts-chat://bots/{id}` | 某个 Bot 的定义与配置步骤（Markdown 格式） |

## Agent（智能体）

### Prompt Manager

`prompt-manager` 智能体可以帮你：

- 在 prompts.chat 中搜索提示词
- 获取提示词并填写变量
- 把新提示词保存到你的账号
- 用 AI 优化提示词

### Skill Manager

`skill-manager` 智能体可以帮你：

- 搜索 Agent Skills
- 获取技能并安装到你的工作区
- 创建包含多个文件的新技能
- 管理技能文件的内容

## 技能（自动激活）

### 提示词查找（Prompt Lookup）

在以下情况会自动激活：

- 你要提示词模板时
- 你想搜索提示词时
- 你需要优化提示词时
- 对话中提到了 prompts.chat

### 技能查找（Skill Lookup）

在以下情况会自动激活：

- 你要 Agent Skills 时
- 你想扩展 Claude 的能力时
- 你需要安装技能时
- 对话中提到了技能

## 登录认证

要保存提示词和技能，你需要从 [prompts.chat/settings](https://prompts.chat/settings) 获取 API Key。

### 方式一：环境变量

设置 `PROMPTS_API_KEY` 环境变量：

```bash
export PROMPTS_API_KEY=your_api_key_here
```

### 方式二：MCP 请求头

连接 MCP 服务器时加上请求头：

```
PROMPTS_API_KEY: your_api_key_here
```

## 插件目录结构

```
plugins/claude/prompts.chat/
├── .claude-plugin/
│   └── plugin.json          # 插件清单
├── .mcp.json                 # MCP 服务器配置
├── commands/
│   ├── prompts.md           # /prompts.chat:prompts 命令
│   └── skills.md            # /prompts.chat:skills 命令
├── agents/
│   ├── prompt-manager.md    # 提示词管理智能体
│   └── skill-manager.md     # 技能管理智能体
└── skills/
    ├── prompt-lookup/
    │   └── SKILL.md         # 提示词发现技能
    └── skill-lookup/
        └── SKILL.md         # 技能发现技能
```

## 相关链接

- **[prompts.chat](https://prompts.chat)** —— 浏览全部提示词与技能
- **[API 文档](https://prompts.chat/api/mcp)** —— MCP 服务器接入地址
- **[设置](https://prompts.chat/settings)** —— 获取你的 API Key

---

<sub>本文档由英文版 CLAUDE-PLUGIN.md 翻译而来，如中英文表述存在出入，请以<a href="CLAUDE-PLUGIN.md">英文原版</a>为准。</sub>
