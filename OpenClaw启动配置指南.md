# OpenClaw 启动配置指南

> 从零开始配置 OpenClaw，包括端口管理、Skill 配置、应用接入、AI 模型更换和 API Key 配置

---

## 📋 目录

- [端口配置指南](#端口配置指南)
- [快速启动流程](#快速启动流程)
- [Skill 配置管理](#skill-配置管理)
- [应用接入配置](#应用接入配置)
- [AI 模型配置](#ai-模型配置)
- [API Key 配置](#api-key-配置)
- [常见问题排查](#常见问题排查)

---

## 🔌 端口配置指南

### 默认端口说明

OpenClaw 使用多个端口，了解它们的用途很重要：

| 端口         | 服务             | 说明                             |
| ------------ | ---------------- | -------------------------------- |
| **18789**    | Gateway 主端口   | WebSocket 网关服务默认端口       |
| **19001**    | Gateway 开发端口 | 开发模式下的网关端口             |
| **自动分配** | Browser Canvas   | 浏览器控制服务（基于主端口偏移） |

### 启动前端口检查

```powershell
# 检查端口是否被占用
netstat -ano | findstr :18789
netstat -ano | findstr :19001

# 查看占用端口的进程
netstat -ano | findstr :18789
# 记录 PID（最后一列的数字）
tasklist | findstr <PID>
```

### 端口冲突解决

**方案 1：杀死占用进程**

```powershell
# 强制杀死占用 18789 端口的进程
taskkill /PID <PID> /F

# 或者使用 openclaw 的强制启动选项
openclaw gateway --force
```

**方案 2：使用自定义端口**

```powershell
# 在自定义端口启动网关
openclaw gateway --port 18790

# 持久化端口配置
openclaw config set gateway.port 18790
```

**方案 3：使用开发模式**

```powershell
# 开发模式自动使用 19001 端口，避免冲突
openclaw --dev gateway
```

### 防火墙配置

```powershell
# 允许 OpenClaw 网关端口通过防火墙（Windows）
New-NetFirewallRule -DisplayName "OpenClaw Gateway" -Direction Inbound -LocalPort 18789 -Protocol TCP -Action Allow

# 如果使用开发模式
New-NetFirewallRule -DisplayName "OpenClaw Dev Gateway" -Direction Inbound -LocalPort 19001 -Protocol TCP -Action Allow
```

### 多实例端口规划

```powershell
# 实例 1：生产环境（默认）
openclaw gateway

# 实例 2：开发环境
openclaw --dev gateway

# 实例 3：测试环境（自定义端口）
openclaw gateway --port 18791

# 使用 Profile 管理多实例
openclaw --profile test gateway
```

---

## 🚀 快速启动流程

### 第一次启动（完整流程）

```powershell
# 1. 检查环境
openclaw --version

# 2. 初始化配置
openclaw setup

# 3. 运行配置向导
openclaw configure

# 4. 配置 AI 模型（见下文）
openclaw models --help

# 5. 启动网关
openclaw gateway
```

### 日常启动（简化流程）

```powershell
# 方式 1：直接启动（前台运行）
openclaw gateway

# 方式 2：后台运行（推荐）
openclaw gateway --daemon

# 方式 3：使用配置文件启动
openclaw --config ~/.openclaw/config.yaml gateway
```

### 开发环境启动

```powershell
# 启动开发模式（隔离配置）
openclaw --dev gateway

# 指定日志级别进行调试
openclaw --log-level debug gateway
```

### 启动验证

```powershell
# 检查网关健康状态
openclaw health

# 查看系统状态
openclaw status

# 查看实时日志
openclaw logs

# 打开控制面板
openclaw dashboard
```

---

## 🧩 Skill 配置管理

### 查看可用 Skills

```powershell
# 列出所有可用的 Skills
openclaw skills list

# 查看特定 Skill 的详细信息
openclaw skills inspect <skill-name>

# 搜索 Skills
openclaw skills search <keyword>
```

### 安装 Skill

```powershell
# 从官方仓库安装
openclaw skills install <skill-name>

# 从 Git 仓库安装
openclaw skills install --git https://github.com/user/skill-repo.git

# 从本地文件安装
openclaw skills install --path /path/to/skill
```

### 配置 Skill

```powershell
# 配置 Skill 参数
openclaw config set skills.<skill-name>.<param> <value>

# 示例：配置翻译 Skill
openclaw config set skills.translate.api_key "your-api-key"
openclaw config set skills.translate.default_language "zh-CN"

# 查看当前配置
openclaw config get skills.<skill-name>
```

### 管理 Skill

```powershell
# 启用 Skill
openclaw skills enable <skill-name>

# 禁用 Skill
openclaw skills disable <skill-name>

# 卸载 Skill
openclaw skills uninstall <skill-name>

# 更新 Skill
openclaw skills update <skill-name>
```

### 常用 Skill 配置示例

**1. 文件处理 Skill**

```powershell
openclaw skills install file-processor
openclaw config set skills.file-processor.watch_dir "C:/Documents"
openclaw config set skills.file-processor.auto_process true
```

**2. 网页抓取 Skill**

```powershell
openclaw skills install web-scraper
openclaw config set skills.web-scraper.timeout 30
openclaw config set skills.web-scraper.headless true
```

**3. 数据分析 Skill**

```powershell
openclaw skills install data-analyzer
openclaw config set skills.data-analyzer.default_format csv
openclaw config set skills.data-analyzer.auto_chart true
```

---

## 📱 应用接入配置

### WhatsApp 配置

```powershell
# 登录 WhatsApp Web
openclaw channels login whatsapp --verbose

# 配置 WhatsApp 通道
openclaw config set channels.whatsapp.auto_reconnect true
openclaw config set channels.whatsapp.qr_timeout 120

# 查找联系人
openclaw directory lookup whatsapp --phone +8613800138000

# 发送测试消息
openclaw message send --channel whatsapp --target +8613800138000 --message "测试连接"
```

### Telegram 配置

```powershell
# 配置 Telegram Bot Token
openclaw config set channels.telegram.bot_token "your-bot-token"

# 登录 Telegram
openclaw channels login telegram

# 配置 Telegram 选项
openclaw config set channels.telegram.webhook_url "https://your-domain.com/webhook"
openclaw config set channels.telegram.allowed_users "@username1,@username2"

# 发送测试消息
openclaw message send --channel telegram --target @username --message "测试连接"
```

### 微信/企业微信配置

```powershell
# 登录企业微信
openclaw channels login wechat-work --verbose

# 配置企业微信
openclaw config set channels.wechat-work.corp_id "your-corp-id"
openclaw config set channels.wechat-work.agent_id "your-agent-id"
openclaw config set channels.wechat-work.secret "your-secret"

# 查找群组
openclaw directory lookup wechat-work --type group --name "项目组"
```

### 钉钉配置

```powershell
# 配置钉钉机器人
openclaw config set channels.dingtalk.webhook "https://oapi.dingtalk.com/robot/send?access_token=your-token"
openclaw config set channels.dingtalk.secret "your-secret"

# 测试连接
openclaw message send --channel dingtalk --target "your-webhook-url" --message "测试连接"
```

### 飞书配置

```powershell
# 配置飞书应用
openclaw config set channels.feishu.app_id "your-app-id"
openclaw config set channels.feishu.app_secret "your-app-secret"

# 登录飞书
openclaw channels login feishu

# 配置事件订阅
openclaw config set channels.feishu.encrypt_key "your-encrypt-key"
openclaw config set channels.feishu.verification_token "your-verification-token"
```

### QQ 配置

```powershell
# 登录 QQ
openclaw channels login qq --verbose

# 配置 QQ 选项
openclaw config set channels.qq.auto_reply true
openclaw config set channels.qq.group_only false

# 测试连接
openclaw message send --channel qq --target "QQ号" --message "测试连接"
```

### 通用通道配置

```powershell
# 查看所有通道状态
openclaw status

# 配置通道健康检查
openclaw config set channels.health_check_interval 60

# 配置重连策略
openclaw config set channels.max_retries 5
openclaw config set channels.retry_delay 10
```

---

## 🤖 AI 模型配置

### 查看可用模型

```powershell
# 扫描本地模型
openclaw models scan --local

# 扫描云端模型
openclaw models scan --cloud

# 列出所有配置的模型
openclaw models list

# 查看模型详情
openclaw models inspect <model-name>
```

### 配置 OpenAI 模型

```powershell
# 设置 OpenAI API Key
openclaw config set models.openai.api_key "sk-your-api-key"

# 配置默认模型
openclaw config set models.openai.default_model "gpt-4"

# 配置备用模型（自动切换）
openclaw config set models.openai.fallback_models '["gpt-3.5-turbo","gpt-4"]'

# 配置模型参数
openclaw config set models.openai.temperature 0.7
openclaw config set models.openai.max_tokens 2048
openclaw config set models.openai.timeout 30
```

### 配置国产模型

**智谱 AI (GLM)**

```powershell
openclaw config set models.zhipu.api_key "your-zhipu-api-key"
openclaw config set models.zhipu.default_model "glm-4"
openclaw config set models.zhipu.endpoint "https://open.bigmodel.cn/api/paas/v4"
```

**文心一言 (ERNIE)**

```powershell
openclaw config set models.ernie.api_key "your-ernie-api-key"
openclaw config set models.ernie.secret_key "your-ernie-secret"
openclaw config set models.ernie.default_model "ernie-bot-4"
```

**通义千问 (Qwen)**

```powershell
openclaw config set models.qwen.api_key "your-qwen-api-key"
openclaw config set models.qwen.default_model "qwen-max"
openclaw config set models.qwen.endpoint "https://dashscope.aliyuncs.com/api/v1"
```

**Claude (Anthropic)**

```powershell
openclaw config set models.anthropic.api_key "your-claude-api-key"
openclaw config set models.anthropic.default_model "claude-3-opus-20240229"
openclaw config set models.anthropic.max_retries 3
```

### 配置本地模型

**Ollama**

```powershell
# 配置 Ollama 端点
openclaw config set models.ollama.endpoint "http://localhost:11434"

# 设置默认模型
openclaw config set models.ollama.default_model "llama2:7b"

# 配置多个本地模型
openclaw config set models.ollama.available_models '["llama2:7b","mistral:7b","codellama:7b"]'
```

**vLLM**

```powershell
openclaw config set models.vllm.endpoint "http://localhost:8000"
openclaw config set models.vllm.default_model "your-model-name"
openclaw config set models.vllm.api_key "optional-api-key"
```

### 模型自动切换配置

```powershell
# 启用自动切换
openclaw config set models.auto_switch.enabled true

# 配置切换策略（按成本）
openclaw config set models.auto_switch.strategy "cost"

# 配置模型优先级
openclaw config set models.auto_switch.priority '["ollama:llama2","openai:gpt-3.5-turbo","openai:gpt-4"]'

# 配置切换阈值
openclaw config set models.auto_switch.max_cost_per_request 0.01
openclaw config set models.auto_switch.fallback_on_error true
```

### 模型性能优化

```powershell
# 配置缓存
openclaw config set models.cache.enabled true
openclaw config set models.cache.ttl 3600
openclaw config set models.cache.max_size 1000

# 配置批处理
openclaw config set models.batch.enabled true
openclaw config set models.batch.max_size 5
openclaw config set models.batch.timeout 2

# 配置并发控制
openclaw config set models.concurrency.max_requests 10
openclaw config set models.concurrency.max_per_model 3
```

---

## 🔑 API Key 配置

### 统一 API Key 管理

```powershell
# 使用 secrets 命令管理密钥
openclaw secrets list

# 添加新的 API Key
openclaw secrets add openai --key "sk-your-api-key"

# 更新现有密钥
openclaw secrets update openai --key "new-api-key"

# 删除密钥
openclaw secrets remove openai

# 重载所有密钥
openclaw secrets reload
```

### 环境变量配置

```powershell
# Windows PowerShell 临时环境变量
$env:OPENCLAW_OPENAI_API_KEY="sk-your-api-key"

# Windows 永久环境变量
[Environment]::SetEnvironmentVariable("OPENCLAW_OPENAI_API_KEY", "sk-your-api-key", "User")

# 配置文件方式
openclaw config set secrets.env_file "~/.openclaw/.env"
```

### 配置文件方式

创建 `~/.openclaw/.env` 文件：

```env
# OpenAI
OPENAI_API_KEY=sk-your-openai-key

# 智谱 AI
ZHIPU_API_KEY=your-zhipu-key

# 文心一言
ERNIE_API_KEY=your-ernie-key
ERNIE_SECRET_KEY=your-ernie-secret

# 通义千问
QWEN_API_KEY=your-qwen-key

# Claude
ANTHROPIC_API_KEY=your-claude-key

# Telegram
TELEGRAM_BOT_TOKEN=your-telegram-token

# 企业微信
WECHAT_CORP_ID=your-corp-id
WECHAT_AGENT_ID=your-agent-id
WECHAT_SECRET=your-secret
```

### 密钥安全配置

```powershell
# 启用密钥加密
openclaw config set security.encrypt_secrets true

# 配置密钥轮换
openclaw config set security.key_rotation_days 30

# 启用密钥审计日志
openclaw config set security.audit_log.enabled true
openclaw config set security.audit_log.path "~/.openclaw/logs/audit.log"
```

### 多环境密钥配置

```powershell
# 生产环境
openclaw --profile prod config set models.openai.api_key "prod-api-key"

# 开发环境
openclaw --profile dev config set models.openai.api_key "dev-api-key"

# 测试环境
openclaw --profile test config set models.openai.api_key "test-api-key"
```

---

## 🔍 常见问题排查

### 端口相关问题

**问题：端口被占用**

```powershell
# 检查占用进程
netstat -ano | findstr :18789

# 解决方案 1：杀死进程
taskkill /PID <PID> /F

# 解决方案 2：使用其他端口
openclaw gateway --port 18790

# 解决方案 3：使用开发模式
openclaw --dev gateway
```

**问题：防火墙阻止连接**

```powershell
# 检查防火墙规则
Get-NetFirewallRule | Where-Object {$_.DisplayName -like "*OpenClaw*"}

# 添加防火墙规则
New-NetFirewallRule -DisplayName "OpenClaw Gateway" -Direction Inbound -LocalPort 18789 -Protocol TCP -Action Allow
```

### 通道连接问题

**问题：WhatsApp 连接失败**

```powershell
# 重新登录
openclaw channels login whatsapp --verbose

# 检查网络连接
openclaw doctor

# 查看详细日志
openclaw logs --level debug
```

**问题：Telegram Bot 无响应**

```powershell
# 验证 Bot Token
openclaw config get channels.telegram.bot_token

# 重新配置 Webhook
openclaw channels configure telegram --webhook

# 测试连接
openclaw message send --channel telegram --target @username --message "测试"
```

### AI 模型问题

**问题：模型调用失败**

```powershell
# 检查 API Key
openclaw secrets list

# 测试模型连接
openclaw models test openai

# 查看模型状态
openclaw models status

# 启用详细日志
openclaw --log-level debug models scan
```

**问题：模型切换不工作**

```powershell
# 检查自动切换配置
openclaw config get models.auto_switch

# 重载配置
openclaw secrets reload

# 查看切换日志
openclaw logs | grep "model.*switch"
```

### Skill 配置问题

**问题：Skill 无法加载**

```powershell
# 检查 Skill 状态
openclaw skills list

# 重新安装 Skill
openclaw skills reinstall <skill-name>

# 查看 Skill 日志
openclaw logs --filter skill
```

**问题：Skill 执行错误**

```powershell
# 启用调试模式
openclaw --log-level debug agent --to <target> --message "测试"

# 检查 Skill 配置
openclaw skills inspect <skill-name>

# 查看 Skill 钩子
openclaw hooks list
```

### 性能优化建议

```powershell
# 启用缓存
openclaw config set cache.enabled true

# 配置批处理
openclaw config set batch.enabled true

# 限制并发请求
openclaw config set concurrency.max_requests 10

# 优化日志级别
openclaw config set log.level "warn"
```

---

## 📊 监控与维护

### 健康检查

```powershell
# 全面健康检查
openclaw doctor

# 检查网关状态
openclaw health

# 检查通道状态
openclaw status

# 检查模型状态
openclaw models status
```

### 日志管理

```powershell
# 实时查看日志
openclaw logs

# 查看特定级别日志
openclaw logs --level error

# 查看特定时间段日志
openclaw logs --since "1 hour ago"

# 导出日志
openclaw logs --export /path/to/logfile.log
```

### 备份与恢复

```powershell
# 创建备份
openclaw backup create --name "backup-$(Get-Date -Format 'yyyy-MM-dd')"

# 验证备份
openclaw backup verify --name "backup-2024-03-20"

# 恢复备份
openclaw backup restore --name "backup-2024-03-20"

# 列出所有备份
openclaw backup list
```

---

## 🎯 最佳实践

1. **端口管理**
   - 使用固定端口避免冲突
   - 在防火墙中明确配置规则
   - 使用 Profile 管理多环境

2. **密钥安全**
   - 使用 secrets 命令管理密钥
   - 定期轮换 API Key
   - 不要将密钥提交到版本控制

3. **模型配置**
   - 配置备用模型实现自动切换
   - 根据任务复杂度选择合适模型
   - 启用缓存减少重复调用

4. **通道配置**
   - 为每个通道配置超时和重试
   - 定期检查连接状态
   - 配置健康监控

5. **Skill 管理**
   - 只启用必要的 Skills
   - 定期更新 Skills
   - 监控 Skill 执行性能

---

**更多资源**：

- 官方文档：https://docs.openclaw.ai
- 社区支持：https://community.openclaw.ai
- 问题反馈：https://github.com/openclaw/openclaw/issues
