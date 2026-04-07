# OpenClaw 技能列表详解

> OpenClaw 2026.3.13 - 完整的技能列表翻译和使用说明

---

## 📋 概述

OpenClaw 包含 **52 个内置技能**，当前有 **5 个已就绪**，其余技能需要额外配置才能使用。

**技能状态说明：**
- ✓ **ready** - 已就绪，可以直接使用
- ✗ **missing** - 缺失，需要安装依赖或配置后才能使用

---

## ✅ 已就绪技能（5个）

### 🧩 coding-agent - 代码代理
**状态：** ✓ ready  
**用途：** 委派编码任务给 Codex、Claude Code 或 Pi 代理

**使用场景：**
1. 构建新功能或应用
2. 审查 Pull Request（在临时目录中生成）
3. 重构大型代码库
4. 需要文件探索的迭代编码

**不适用于：**
- 简单的单行修复（直接编辑即可）
- 读取代码（使用读取工具）
- 线程绑定的 ACP 挂载请求（例如在 Discord 线程中生成/运行 Codex）
- 在 ~/clawd 工作区中的工作（从不在此生成代理）

**配置要求：**
- Claude Code: 使用 `--print --permission-mode bypassPermissions`（无 PTY）
- Codex/Pi/OpenCode: 需要 `pty:true`

---

### 📦 healthcheck - 健康检查
**状态：** ✓ ready  
**用途：** OpenClaw 部署的主机安全加固和风险容忍度配置

**使用场景：**
- 用户要求安全审计
- 防火墙/SSH/更新加固
- 风险姿态评估
- 暴露审查
- OpenClaw cron 定期检查调度
- 在运行 OpenClaw 的机器上检查版本状态（笔记本电脑、工作站、Pi、VPS）

---

### 📦 node-connect - 节点连接
**状态：** ✓ ready  
**用途：** 诊断 OpenClaw 节点连接和配对失败问题

**支持平台：**
- Android
- iOS
- macOS 伴侣应用

**使用场景：**
- QR/设置代码/手动连接失败
- 本地 Wi-Fi 工作但 VPS/tailnet 不工作
- 错误提到需要配对、未授权、引导令牌无效或过期
- 涉及 `gateway.bind`、`gateway.remote.url`、Tailscale 或 `plugins.entries.device-pair.config.publicUrl` 的错误

---

### 📦 skill-creator - 技能创建器
**状态：** ✓ ready  
**用途：** 创建、编辑、改进或审计 AgentSkills

**使用场景：**
- 从零开始创建新技能
- 改进、审查、审计、整理或清理现有技能或 SKILL.md 文件
- 编辑或重构技能目录（将文件移动到 references/ 或 scripts/，删除过时内容，根据 AgentSkills 规范进行验证）

**触发短语：**
- "创建一个技能"
- "编写一个技能"
- "整理这个技能"
- "改进这个技能"
- "审查这个技能"
- "清理这个技能"
- "审计这个技能"

---

### ☔ weather - 天气查询
**状态：** ✓ ready  
**用途：** 通过 wttr.in 或 Open-Meteo 获取当前天气和预报

**使用场景：**
- 用户询问任何位置的天气、温度或预报

**不适用于：**
- 历史天气数据
- 严重天气警报

---

## 🔐 安全与密码管理

### 🐻 1password - 1Password 管理
**状态：** ✗ missing  
**用途：** 设置和使用 1Password CLI (op)

**使用场景：**
- 安装 CLI 时
- 启用桌面应用集成
- 登录（单账户或多账户）
- 通过 op 读取/注入/运行密钥

---

## 📝 笔记与文档

### 📝 apple-notes - Apple Notes 管理
**状态：** ✗ missing（仅 macOS）  
**用途：** 通过 macOS 上的 `memo` CLI 管理 Apple Notes

**功能：**
- 创建、查看、编辑、删除笔记
- 搜索笔记
- 移动笔记
- 导出笔记

**使用场景：**
- 用户要求 OpenClaw 添加笔记
- 列出笔记
- 搜索笔记
- 管理笔记文件夹

---

### ⏰ apple-reminders - Apple 提醒事项
**状态：** ✗ missing（仅 macOS）  
**用途：** 通过 remindctl CLI 管理 Apple Reminders

**功能：**
- 列出、添加、编辑、完成、删除提醒
- 支持列表和日期筛选
- 支持 JSON 和纯文本输出

---

### 🐻 bear-notes - Bear 笔记
**状态：** ✗ missing  
**用途：** 通过 grizzly CLI 创建、搜索和管理 Bear 笔记

---

### 💎 obsidian - Obsidian 笔记
**状态：** ✗ missing  
**用途：** 使用 Obsidian vaults（纯 Markdown 笔记）并通过 obsidian-cli 自动化

---

### 📝 notion - Notion 管理
**状态：** ✗ missing  
**用途：** Notion API，用于创建和管理页面、数据库和块

---

## 📧 邮件与消息

### 📧 himalaya - 邮件管理
**状态：** ✗ missing  
**用途：** 通过 IMAP/SMTP 管理邮件的 CLI

**功能：**
- 列出、读取、编写、回复、转发、搜索邮件
- 从终端整理邮件
- 支持多账户
- 使用 MML（MIME 元语言）进行消息组合

---

### 📨 imsg - iMessage 管理
**状态：** ✗ missing（仅 macOS）  
**用途：** iMessage/SMS CLI，用于列出聊天记录和历史记录，并通过 Messages.app 发送消息

---

### 🫧 bluebubbles - iMessage 集成
**状态：** ✗ missing  
**用途：** 通过 BlueBubbles 发送或管理 iMessage（推荐的 iMessage 集成方式）

**调用方式：** 通过通用消息工具，设置 `channel="bluebubbles"`

---

### 📱 wacli - WhatsApp 管理
**状态：** ✗ missing  
**用途：** 通过 wacli CLI 向其他人发送 WhatsApp 消息或搜索/同步 WhatsApp 历史记录

**注意：** 不用于普通用户聊天

---

## 🎮 社交媒体与通讯

### 🎮 discord - Discord 控制
**状态：** ✗ missing  
**用途：** 通过消息工具进行 Discord 操作（channel=discord）

---

### 💬 slack - Slack 控制
**状态：** ✗ missing  
**用途：** 通过 slack 工具从 OpenClaw 控制 Slack

**功能：**
- 对消息做出反应
- 在 Slack 频道或私信中固定/取消固定项目

---

## 🎨 图像与视频处理

### 📸 camsnap - 相机抓拍
**状态：** ✗ missing  
**用途：** 从 RTSP/ONVIF 相机捕获帧或片段

---

### 🌊 songsee - 音频可视化
**状态：** ✗ missing  
**用途：** 使用 songsee CLI 从音频生成频谱图和特征面板可视化

---

### 🎨 openai-image-gen - OpenAI 图像生成
**状态：** ✗ missing  
**用途：** 通过 OpenAI Images API 批量生成图像

**功能：**
- 随机提示采样器
- `index.html` 图库生成

---

### 🍌 nano-banana-pro - 图像编辑
**状态：** ✗ missing  
**用途：** 通过 Gemini 3 Pro Image (Nano Banana Pro) 生成或编辑图像

---

### 🎬 video-frames - 视频帧提取
**状态：** ✗ missing  
**用途：** 使用 ffmpeg 从视频中提取帧或短片段

---

## 🎵 音乐与媒体

### 🫐 blucli - BluOS 控制
**状态：** ✗ missing  
**用途：** 用于发现、播放、分组和音量控制的 BluOS CLI (blu)

---

### 🔊 sag - 文字转语音
**状态：** ✗ missing  
**用途：** ElevenLabs 文字转语音，具有 macOS 风格的 say 用户体验

---

### 🔊 sherpa-onnx-tts - 本地 TTS
**状态：** ✗ missing  
**用途：** 通过 sherpa-onnx 进行本地文字转语音（离线，无云端）

---

### 🔊 sonoscli - Sonos 扬声器控制
**状态：** ✗ missing  
**用途：** 控制 Sonos 扬声器（发现/状态/播放/音量/分组）

---

### 🎵 spotify-player - Spotify 播放
**状态：** ✗ missing  
**用途：** 通过 spogo（首选）或 spotify_player 进行终端 Spotify 播放/搜索

---

## 💡 AI 与语音

### ✨ gemini - Gemini AI
**状态：** ✗ missing  
**用途：** Gemini CLI，用于一次性问答、摘要和生成

---

### 🧿 oracle - Oracle CLI
**状态：** ✗ missing  
**用途：** 使用 oracle CLI 的最佳实践

**功能：**
- 提示 + 文件打包
- 引擎
- 会话
- 文件附件模式

---

### 🎤 openai-whisper - 本地语音转文字
**状态：** ✗ missing  
**用途：** 使用 Whisper CLI 进行本地语音转文字（无需 API Key）

---

### 🌐 openai-whisper-api - OpenAI 语音转文字
**状态：** ✗ missing  
**用途：** 通过 OpenAI 音频转录 API (Whisper) 转录音频

---

## 📦 开发工具与集成

### 📦 clawhub - ClawHub 技能仓库
**状态：** ✗ missing  
**用途：** 使用 ClawHub CLI 从 clawhub.com 搜索、安装、更新和发布代理技能

**使用场景：**
- 动态获取新技能
- 将已安装的技能同步到最新版本或特定版本
- 发布新的/更新的技能文件夹

---

### 🐙 github - GitHub 操作
**状态：** ✗ missing  
**用途：** 通过 `gh` CLI 进行 GitHub 操作

**功能：**
- Issues、PRs、CI 运行
- 代码审查
- API 查询

**使用场景：**
- 检查 PR 状态或 CI
- 创建/评论 issues
- 列出/筛选 PRs 或 issues
- 查看运行日志

**不适用于：**
- 需要手动浏览器流程的复杂 Web UI 交互
- 跨许多仓库的批量操作
- gh auth 未配置的情况

---

### 📦 gh-issues - GitHub Issues 管理
**状态：** ✗ missing  
**用途：** 获取 GitHub issues，生成子代理实现修复并打开 PR，然后监控和解决 PR 审查评论

**用法示例：**
```
/gh-issues [owner/repo] [--label bug] [--limit 5] [--milestone v1.0] [--assignee @me] [--fork user/repo] [--watch] [--interval 5] [--reviews-only] [--cron] [--dry-run] [--model glm-5] [--notify-channel -1002381931352]
```

---

### 🧲 gifgrep - GIF 搜索
**状态：** ✗ missing  
**用途：** 通过 CLI/TUI 搜索 GIF 提供商，下载结果，并提取静态图像/工作表

---

### 📊 model-usage - 模型使用统计
**状态：** ✗ missing  
**用途：** 使用 CodexBar CLI 本地成本使用情况来总结 Codex 或 Claude 的每个模型使用情况

**功能：**
- 当前（最近）模型
- 完整的模型细分

**触发场景：**
- 要求来自 codexbar 的模型级别使用/成本数据
- 需要 codexbar 成本 JSON 的可编写脚本的每个模型摘要

---

### 📦 mcporter - MCP 服务器管理
**状态：** ✗ missing  
**用途：** 使用 mcporter CLI 列出、配置、认证和直接调用 MCP 服务器/工具

**功能：**
- HTTP 或 stdio
- 临时服务器
- 配置编辑
- CLI/类型生成

---

### 🧵 tmux - tmux 会话控制
**状态：** ✗ missing  
**用途：** 通过发送击键和抓取窗格输出远程控制 tmux 会话，用于交互式 CLI

---

## 🌐 网络与位置

### 📰 blogwatcher - 博客监控
**状态：** ✗ missing  
**用途：** 使用 blogwatcher CLI 监控博客和 RSS/Atom feed 的更新

---

### 📍 goplaces - Google Places 查询
**状态：** ✗ missing  
**用途：** 通过 goplaces CLI 查询 Google Places API (New)

**功能：**
- 文本搜索
- 地点详情
- 解析
- 评价

**用途：** 用于人性化的地点查找或脚本的 JSON 输出

---

### 🎮 gog - Google Workspace
**状态：** ✗ missing  
**用途：** Google Workspace CLI，用于 Gmail、Calendar、Drive、Contacts、Sheets 和 Docs

---

## 🏠 智能家居

### 💡 openhue - Philips Hue 控制
**状态：** ✗ missing  
**用途：** 通过 OpenHue CLI 控制 Philips Hue 灯光和场景

---

### 🛌 eightctl - Eight Sleep 控制
**状态：** ✗ missing  
**用途：** 控制 Eight Sleep 豆荚（状态、温度、闹钟、计划）

---

### 🛵 ordercli - 外卖订单
**状态：** ✗ missing（Foodora 专用）  
**用途：** 用于检查过去订单和活跃订单状态的 Foodora 专用 CLI（Deliveroo 开发中）

---

## 📋 任务管理

### ✅ things-mac - Things 3 管理
**状态：** ✗ missing（仅 macOS）  
**用途：** 通过 macOS 上的 `things` CLI 管理 Things 3

**功能：**
- 通过 URL scheme 添加/更新项目+待办事项
- 从本地 Things 数据库读取/搜索/列表

**使用场景：**
- 用户要求 OpenClaw 向 Things 添加任务
- 列出收件箱/今天/即将到来
- 搜索任务
- 检查项目/区域/标签

---

### 📋 trello - Trello 管理
**状态：** ✗ missing  
**用途：** 通过 Trello REST API 管理 Trello 看板、列表和卡片

---

## 📄 文档处理

### 📄 nano-pdf - PDF 编辑
**状态：** ✗ missing  
**用途：** 使用 nano-pdf CLI 通过自然语言指令编辑 PDF

---

### 🧾 summarize - 内容摘要
**状态：** ✗ missing  
**用途：** 从 URL、播客和本地文件摘要或提取文本/转录

**用途：** "转录这个 YouTube/视频" 的绝佳后备方案

---

### 📜 session-logs - 会话日志分析
**状态：** ✗ missing  
**用途：** 使用 jq 搜索和分析您自己的会话日志（较旧/父级对话）

---

## 🔍 其他工具

### 👀 peekaboo - macOS UI 自动化
**状态：** ✗ missing  
**用途：** 使用 Peekaboo CLI 捕获和自动化 macOS UI

---

### 🎯 voice-call - 语音通话
**状态：** ✗ missing  
**用途：** 通过 OpenClaw voice-call 插件启动语音通话

---

## 📚 如何启用缺失的技能

### 方法 1：使用 ClawHub 安装
```powershell
# 列出可用技能
openclaw skills list

# 从 ClawHub 安装
openclaw skills install <skill-name>

# 更新技能
openclaw skills update <skill-name>
```

### 方法 2：手动配置依赖
许多技能需要安装相应的 CLI 工具：

**示例：安装 GitHub CLI**
```powershell
# 安装 gh CLI
winget install --id GitHub.cli

# 配置认证
gh auth login

# 验证安装
gh --version
```

**示例：安装 Ollama（用于本地模型）**
```powershell
# 下载并安装 Ollama
# 从 https://ollama.ai 下载 Windows 版本

# 验证安装
ollama --version

# 拉取模型
ollama pull llama2
```

### 方法 3：检查技能状态
```powershell
# 查看技能详细信息
openclaw skills inspect <skill-name>

# 检查技能依赖
openclaw skills check <skill-name>
```

## 🎯 推荐技能配置顺序

### 初学者推荐
1. ☔ weather - 天气查询（已就绪）
2. 📦 healthcheck - 健康检查（已就绪）
3. 🧩 coding-agent - 代码代理（已就绪）

### 开发者推荐
1. 🧩 coding-agent - 代码代理
2. 🐙 github - GitHub 操作
3. 📦 clawhub - ClawHub 技能仓库

### 生产力提升
1. 📝 apple-notes - Apple Notes（macOS）
2. ⏰ apple-reminders - Apple 提醒事项（macOS）
3. 📧 himalaya - 邮件管理

### 智能家居
1. 💡 openhue - Philips Hue 控制
2. 🫐 blucli - BluOS 控制
3. 🔊 sag - 文字转语音

## 💡 使用技巧

1. **检查技能状态**：在使用技能前，先检查其状态是否为 "ready"
2. **阅读描述**：每个技能都有详细的使用场景说明，确保符合你的需求
3. **注意平台限制**：某些技能仅适用于 macOS（如 apple-notes、imsg）
4. **渐进式启用**：不要一次性启用所有技能，根据需求逐步启用
5. **定期更新**：使用 `openclaw skills update` 保持技能为最新版本

## 🔗 相关资源

- [OpenClaw 命令指南](./OpenClaw命令指南.md)
- [OpenClaw 启动配置指南](./OpenClaw启动配置指南.md)
- 官方文档：https://docs.openclaw.ai
- ClawHub 技能仓库：https://clawhub.com

---

**最后更新：** 2026-03-20  
**OpenClaw 版本：** 2026.3.13 (61d171a)
