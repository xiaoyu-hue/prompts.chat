<p align="center">
  <a href="DOCKER.md">English</a> · <strong>简体中文</strong>
</p>

# Docker 部署指南

用 Docker Compose 运行你自己的 prompts.chat 实例。

[`compose.yml`](/compose.yml) 既支持从 ghcr.io 拉取预构建的容器镜像，也支持在本地自行构建。

## 快速开始

### 本地构建

```bash
git clone https://github.com/f/prompts.chat.git
cd prompts.chat
docker compose up -d --build
```

然后在浏览器打开 http://localhost:4444

### 使用预构建镜像

只需把命令里的 `--build` 参数去掉：

```bash
git clone https://github.com/f/prompts.chat.git
cd prompts.chat
docker compose up -d
```

## 独立运行（使用你自己的数据库）

如果你已经有现成的 PostgreSQL 实例，可以只运行应用容器：

需要托管式 PostgreSQL 数据库？我们推荐 [Neon](https://get.neon.com/VqfnMo4)，它提供 Serverless Postgres、连接池与数据库分支能力。

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

```bash
docker build -f docker/Dockerfile -t prompts.chat .
docker run -d \
  --name prompts \
  -p 4444:3000 \
  -e DATABASE_URL="postgresql://user:pass@your-db-host:5432/prompts?schema=public" \
  -e AUTH_SECRET="$(openssl rand -base64 32)" \
  prompts.chat
```

或者，如果你直接想用预构建镜像：

```bash
docker run -d \
  --name prompts \
  -p 4444:3000 \
  -e DATABASE_URL="postgresql://user:pass@your-db-host:5432/prompts?schema=public" \
  -e AUTH_SECRET="$(openssl rand -base64 32)" \
  ghcr.io/f/prompts.chat:latest
```

## 自定义品牌

所有品牌相关配置都通过 `PCHAT_*` 环境变量在运行时生效——无需重新构建镜像。

```yaml
# compose.yml
services:
  app:
    environment:
      # ... 已有的变量 ...
      PCHAT_NAME: "Acme Prompts"
      PCHAT_DESCRIPTION: "Our team's AI prompt library"
      PCHAT_COLOR: "#ff6600"
      PCHAT_AUTH_PROVIDERS: "github,google"
      PCHAT_LOCALES: "en,es,fr"
```

然后重启使其生效：`docker compose up -d`

## 配置变量

所有变量统一加 `PCHAT_` 前缀，以避免命名冲突。

#### 品牌（`branding.*`，对应 prompts.config.ts）

| 环境变量 | 配置项路径 | 说明 | 默认值 |
|--------------|-------------|-------------|---------|
| `PCHAT_NAME` | `branding.name` | 界面上显示的应用名称 | `My Prompt Library` |
| `PCHAT_DESCRIPTION` | `branding.description` | 应用描述 | `Collect, organize...` |
| `PCHAT_LOGO` | `branding.logo` | Logo 路径（位于 public/ 目录） | `/logo.svg` |
| `PCHAT_LOGO_DARK` | `branding.logoDark` | 深色模式下的 Logo | 与 `PCHAT_LOGO` 相同 |
| `PCHAT_FAVICON` | `branding.favicon` | 网站图标路径 | `/logo.svg` |

#### 主题（`theme.*`，对应 prompts.config.ts）

| 环境变量 | 配置项路径 | 说明 | 默认值 |
|--------------|-------------|-------------|---------|
| `PCHAT_COLOR` | `theme.colors.primary` | 主色（十六进制） | `#6366f1` |
| `PCHAT_THEME_RADIUS` | `theme.radius` | 圆角：`none\|sm\|md\|lg` | `sm` |
| `PCHAT_THEME_VARIANT` | `theme.variant` | 界面风格：`default\|flat\|brutal` | `default` |
| `PCHAT_THEME_DENSITY` | `theme.density` | 间距：`compact\|default\|comfortable` | `default` |

#### 登录认证（`auth.*`，对应 prompts.config.ts）

| 环境变量 | 配置项路径 | 说明 | 默认值 |
|--------------|-------------|-------------|---------|
| `PCHAT_AUTH_PROVIDERS` | `auth.providers` | 登录方式：`github,google,credentials` | `credentials` |
| `PCHAT_ALLOW_REGISTRATION` | `auth.allowRegistration` | 是否允许公开注册 | `true` |

#### 国际化（`i18n.*`，对应 prompts.config.ts）

| 环境变量 | 配置项路径 | 说明 | 默认值 |
|--------------|-------------|-------------|---------|
| `PCHAT_LOCALES` | `i18n.locales` | 支持的语言（逗号分隔） | `en` |
| `PCHAT_DEFAULT_LOCALE` | `i18n.defaultLocale` | 默认语言 | `en` |

#### 功能开关（`features.*`，对应 prompts.config.ts）

| 环境变量 | 配置项路径 | 说明 | 默认值 |
|--------------|-------------|-------------|---------|
| `PCHAT_FEATURE_PRIVATE_PROMPTS` | `features.privatePrompts` | 启用私有提示词 | `true` |
| `PCHAT_FEATURE_CHANGE_REQUESTS` | `features.changeRequests` | 启用版本管理 | `true` |
| `PCHAT_FEATURE_CATEGORIES` | `features.categories` | 启用分类 | `true` |
| `PCHAT_FEATURE_TAGS` | `features.tags` | 启用标签 | `true` |
| `PCHAT_FEATURE_COMMENTS` | `features.comments` | 启用评论 | `true` |
| `PCHAT_FEATURE_AI_SEARCH` | `features.aiSearch` | 启用 AI 搜索 | `false` |
| `PCHAT_FEATURE_AI_GENERATION` | `features.aiGeneration` | 启用 AI 生成 | `false` |
| `PCHAT_FEATURE_MCP` | `features.mcp` | 启用 MCP 相关功能 | `false` |
| `PCHAT_FEATURE_PROMPT_ENHANCER` | `features.promptEnhancer` | 启用 `/developers` 页面的提示词增强器与 `/api/improve-prompt` 接口（需要 `OPENAI_API_KEY`） | `true` |

## 系统环境变量

| 变量 | 说明 | 默认值 |
|----------|-------------|---------|
| `AUTH_SECRET` | 登录令牌的加密密钥 | 自动生成（生产环境请显式设置） |
| `DATABASE_URL` | PostgreSQL 连接字符串 | 在 compose.yml 中设置 |
| `DIRECT_URL` | PostgreSQL 直连地址（绕过连接池） | 与 DATABASE_URL 相同 |
| `PORT` | 宿主机端口映射 | `4444` |

## 生产环境配置

生产环境务必显式设置 `AUTH_SECRET`：

```bash
# 生成一个密钥
export AUTH_SECRET=$(openssl rand -base64 32)

# 用这个密钥启动
docker compose up -d
```

或者把它写进 `compose.yml` 同级的 `.env` 文件：

```env
AUTH_SECRET=your-secret-key-here
```

### 接入 OAuth 登录

```yaml
# compose.yml
services:
  app:
    environment:
      # ... 已有的变量 ...
      PCHAT_AUTH_PROVIDERS: "github,google"
      AUTH_GITHUB_ID: "your-github-client-id"
      AUTH_GITHUB_SECRET: "your-github-client-secret"
      AUTH_GOOGLE_ID: "your-google-client-id"
      AUTH_GOOGLE_SECRET: "your-google-client-secret"
```

### 启用 AI 功能（OpenAI）

```yaml
# compose.yml
services:
  app:
    environment:
      # ... 已有的变量 ...
      PCHAT_FEATURE_AI_SEARCH: "true"
      OPENAI_API_KEY: "sk-..."
```

## 导入初始数据

向数据库导入示例提示词：

```bash
docker compose exec app npx prisma db seed
```

## 自定义 Logo

把你的 Logo 文件挂载进应用容器：

```yaml
# compose.yml
services:
  app:
    volumes:
      - ./my-logo.svg:/app/public/logo.svg
    environment:
      PCHAT_LOGO: "/logo.svg"
```

## 数据持久化

PostgreSQL 的数据保存在名为 `postgres_data` 的命名卷中，容器重启、重新构建、镜像升级都不会丢失。

### 备份

```bash
# 备份数据库
docker compose exec db pg_dump -U prompts prompts > backup.sql

# 恢复数据库
docker compose exec -T db psql -U prompts prompts < backup.sql
```

## 本地构建

```bash
docker compose build
docker compose up -d
```

## 健康检查

应用容器内置了健康检查接口：

```bash
curl http://localhost:4444/api/health
```

返回结果：
```json
{
  "status": "healthy",
  "timestamp": "2024-01-01T00:00:00.000Z",
  "database": "connected"
}
```

## 故障排查

### 查看日志

```bash
# 所有服务
docker compose logs

# 实时跟踪日志
docker compose logs -f

# 只看应用日志
docker compose logs app

# 只看数据库日志
docker compose logs db
```

### 访问数据库

```bash
# 连接 PostgreSQL
docker compose exec db psql -U prompts -d prompts

# 执行查询
docker compose exec db psql -U prompts -d prompts -c "SELECT COUNT(*) FROM \"Prompt\""
```

### 进入容器 Shell

```bash
docker compose exec app sh
docker compose exec db bash
```

### 常见问题

**应用容器反复重启：**
- 查看日志：`docker compose logs app`
- 数据库可能还没就绪——入口脚本会自动重试，最长等待 60 秒

**数据库连接报错：**
- 确认 `db` 服务状态健康：`docker compose ps`
- 查看数据库日志：`docker compose logs db`

**登录认证异常：**
- 生产环境请显式设置 `AUTH_SECRET`
- 使用 OAuth 时，确认回调地址与你的域名一致

## 更新升级

```bash
# 使用预构建镜像时
docker compose pull
docker compose up -d

# 本地构建时
git pull
docker compose build
docker compose up -d
```

更新过程中，数据始终保留在 `postgres_data` 卷中。

## 从旧版单镜像方案迁移

如果你之前用的是旧版「全合一」单镜像方案：

```bash
# 1. 从旧容器导出数据库
docker exec prompts pg_dump -U prompts prompts > backup.sql

# 2. 停止并删除旧容器
docker stop prompts && docker rm prompts

# 3. 启动新的 compose 服务
docker compose up -d

# 4. 导入数据
docker compose exec -T db psql -U prompts prompts < backup.sql
```

## 资源需求

**运行阶段**（首次构建之后）：
- 1 个 CPU 核心
- 1GB 内存
- 2GB 磁盘空间

**首次运行构建**（启动时编译 Next.js）：
- 1 个 CPU 核心
- 需要更多内存（限制过低会触发内存不足）
- 2GB 磁盘空间

> ⚠️ 如果首次启动时看到 `Killed`，紧接着是 `exited with code 137`，
> 说明容器在构建阶段内存不够用了。
> 把 Docker 的内存上限调大（例如 4GB 或更多）通常能解决。
> Docker Desktop 的位置：Settings → Resources → Memory。

**生产环境推荐配置：**
- 2 个 CPU 核心
- 2GB 内存（运行阶段）
- 10GB 磁盘空间

## 部署在反向代理之后

### Nginx

```nginx
server {
    listen 443 ssl http2;
    server_name prompts.example.com;

    ssl_certificate /etc/letsencrypt/live/prompts.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/prompts.example.com/privkey.pem;

    location / {
        proxy_pass http://localhost:4444;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### Caddy

```caddyfile
prompts.example.com {
    reverse_proxy localhost:4444
}
```

## 安全注意事项

1. **生产环境务必设置 `AUTH_SECRET`**
2. **启用 HTTPS**——在前面加一层反向代理（Nginx、Caddy、Traefik）
3. **修改默认数据库密码**——同步更新 `compose.yml` 里的 `POSTGRES_PASSWORD` 和连接字符串
4. **收敛暴露端口**——只开放真正需要的端口
5. **定期更新**——及时拉取最新镜像
6. **备份数据**——定期备份数据库

## 许可协议

MIT

---

<sub>本文档由英文版 DOCKER.md 翻译而来，如中英文表述存在出入，请以<a href="DOCKER.md">英文原版</a>为准。</sub>
