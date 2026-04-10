# OpenClaw 命令指南

> OpenClaw 2026.3.13 - 一个功能强大的 AI Agent 管理平台

---

## 📋 目录

- [全局选项](#全局选项)
- [核心命令](#核心命令)
- [代理管理](#代理管理)
- [消息通信](#消息通信)
- [网关管理](#网关管理)
- [配置与设置](#配置与设置)
- [开发与调试](#开发与调试)
- [安全与备份](#安全与备份)
- [其他工具](#其他工具)

---

## 🛠️ 全局选项

这些选项可以与任何命令一起使用：

| 选项                 | 说明                                                    | 示例                               |
| -------------------- | ------------------------------------------------------- | ---------------------------------- |
| `--dev`              | 开发模式：隔离状态，使用端口 19001                      | `openclaw --dev gateway`           |
| `-h, --help`         | 显示命令帮助                                            | `openclaw agent --help`            |
| `--log-level <级别>` | 设置日志级别 (silent/fatal/error/warn/info/debug/trace) | `openclaw --log-level debug agent` |
| `--no-color`         | 禁用颜色输出                                            | `openclaw --no-color status`       |
| `--profile <名称>`   | 使用命名配置文件                                        | `openclaw --profile work gateway`  |
| `-V, --version`      | 显示版本号                                              | `openclaw --version`               |

---

## 🎯 核心命令

### 快速开始

```powershell
# 初始化配置和工作区
openclaw setup

# 交互式设置向导
openclaw configure

# 交互式入门向导
openclaw onboard
```

### 帮助与文档

```powershell
# 查看命令帮助
openclaw help
openclaw <命令> --help

# 搜索在线文档
openclaw docs
```

---

## 🤖 代理管理

### 运行代理

```powershell
# 通过网关运行代理
openclaw agent --to +15555550123 --message "Run summary" --deliver
```

- `--to`: 目标联系人/群组
- `--message`: 发送的消息
- `--deliver`: 发送回复

### 管理代理

```powershell
# 查看和管理代理工作区、认证、路由
openclaw agents --help

# 管理内部代理钩子
openclaw hooks --help

# 列出和查看可用技能
openclaw skills --help

# 搜索和重建记忆文件
openclaw memory --help
```

---

## 💬 消息通信

### 通道管理

```powershell
# 管理连接的聊天通道
openclaw channels --help

# 登录个人 WhatsApp Web 并显示 QR
openclaw channels login --verbose

# 查找联系人和群组 ID
openclaw directory --help

# 显示通道健康状态和最近会话
openclaw status
```

### 发送消息

```powershell
# 通过 WhatsApp 发送消息
openclaw message send --target +15555550123 --message "Hi" --json

# 通过 Telegram 发送消息
openclaw message send --channel telegram --target @mychat --message "Hi"

# 管理（发送、读取、删除）消息
openclaw message --help

# 列出存储的会话
openclaw sessions
```

---

## 🌐 网关管理

### 启动网关

```powershell
# 在默认端口运行 WebSocket 网关
openclaw gateway

# 在指定端口运行
openclaw gateway --port 18789

# 强制启动（杀死占用端口的进程）
openclaw gateway --force

# 开发模式（隔离状态）
openclaw --dev gateway
```

### 网关查询

```powershell
# 运行、检查和查询 WebSocket 网关
openclaw gateway --help

# 获取运行中的网关健康状态
openclaw health

# 通过 RPC 跟踪网关日志
openclaw logs

# 打开连接到网关的终端 UI
openclaw tui

# 网关服务（旧版别名）
openclaw daemon --help
```

---

## ⚙️ 配置与设置

### 配置管理

```powershell
# 交互式配置助手
openclaw config --help

# 查看配置文件
openclaw config file

# 获取配置值
openclaw config get <key>

# 设置配置值
openclaw config set <key> <value>

# 删除配置
openclaw config unset <key>
```

### 模型管理

```powershell
# 发现、扫描和配置模型
openclaw models --help
openclaw models --help
```

### 设备管理

```powershell
# 设备配对和令牌管理
openclaw devices --help

# 生成 iOS 配对 QR/设置代码
openclaw qr

# 安全 DM 配对（批准入站请求）
openclaw pairing --help
```

### 系统管理

```powershell
# 系统事件、心跳和在线状态
openclaw system --help
```

---

## 🔧 开发与调试

### 节点管理

```powershell
# 运行和管理无头节点主机服务
openclaw node --help

# 管理网关拥有的节点配对和命令
openclaw nodes --help
```

### 浏览器管理

```powershell
# 管理 OpenClaw 的专用浏览器（Chrome/Chromium）
openclaw browser --help
```

### 调试工具

```powershell
# 健康检查和快速修复
openclaw doctor

# Agent Control Protocol 工具
openclaw acp --help

# Legacy clawbot 命令别名
openclaw clawbot --help
```

---

## 🔒 安全与备份

### 安全管理

```powershell
# 安全工具和本地配置审计
openclaw security --help

# 管理（网关或节点主机）执行批准
openclaw approvals --help

# 密钥运行时重载控制
openclaw secrets --help
```

### 备份与恢复

```powershell
# 创建和验证 OpenClaw 状态的本地备份档案
openclaw backup --help
```

### 重置与卸载

```powershell
# 重置本地配置/状态（保留 CLI）
openclaw reset

# 卸载网关服务和本地数据（保留 CLI）
openclaw uninstall
```

---

## 🧩 其他工具

### 插件与扩展

```powershell
# 管理 OpenClaw 插件和扩展
openclaw plugins --help
```

### 定时任务

```powershell
# 通过网关调度器管理 cron 任务
openclaw cron --help
```

### Webhooks

```powershell
# Webhook 助手和集成
openclaw webhooks --help
```

### DNS 服务

```powershell
# 广域发现（Tailscale + CoreDNS）的 DNS 助手
openclaw dns --help
```

### Shell 补全

```powershell
# 生成 shell 补全脚本
openclaw completion
```

### 更新

```powershell
# 更新 OpenClaw 并检查更新通道状态
openclaw update --help
```

---

## 📊 控制面板

```powershell
# 使用当前令牌打开控制 UI
openclaw dashboard
```

---

## 💡 常用命令组合

### 日常使用流程
```powershell
# 1. 初始化设置
openclaw setup

# 2. 配置通道（如 WhatsApp）
openclaw channels login --verbose

# 3. 启动网关
openclaw gateway

# 4. 发送消息
openclaw message send --target +15555550123 --message "Hello!"
```

### 调试流程
```powershell
# 1. 检查健康状态
openclaw doctor

# 2. 查看日志
openclaw logs

# 3. 查看状态
openclaw status

# 4. 查看详细日志
openclaw --log-level debug agent --to +15555550123 --message "Test"
```

---

## 📚 更多资源

- 官方文档：https://docs.openclaw.ai/cli
- 命令帮助：`openclaw <命令> --help`
- 实时文档搜索：`openclaw docs`

---

**提示**：带有 `_` 后缀的命令有子命令，运行 `openclaw <命令> --help` 查看详细信息。
