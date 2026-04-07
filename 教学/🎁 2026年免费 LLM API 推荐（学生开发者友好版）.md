
根据你的 AhaTutor 项目需求（需要生成 JSON、支持中文、稳定可靠），我按**推荐优先级**给你整理了一份清单👇

---

## 🥇 第一梯队：国内平台（网络稳 + 中文好 + 免费额度大）

### 1️⃣ 智谱 AI（GLM）⭐ 最推荐
- 🔗 官网：https://open.bigmodel.cn
- 💰 **免费额度**：
  - 新用户注册送 **500万 GLM-4 专属 Token** + **2000万 其他模型 Token**，有效期30天 [[52]]
  - `GLM-4-Flash` 模型：**完全免费，不限量**（QPS=30）[[37]]
  - 推荐计划：邀请好友每月最多可额外获得 **2亿 Token** [[47]]
- ✅ 优势：
  - 中文理解极强，适合遗传学内容生成
  - 支持 JSON Schema 输出，完美适配 A2UI
  - API 格式与 OpenAI 兼容，你的代码几乎不用改
- 🔧 调用方式：
  ```bash
  # .env 配置
  GLM_API_KEY=your_api_key
  DEFAULT_LLM_PROVIDER=glm
  ```

### 2️⃣ 硅基流动（SiliconFlow）⭐ 额度最大
- 🔗 官网：https://siliconflow.cn
- 💰 **免费额度**：**2000万 Token 永久额度** [[45]][[75]]
- 📦 支持模型：DeepSeek 全系、Qwen 全系、GLM 系列、Kimi 等
- ✅ 优势：
  - 聚合多家开源模型，一个 API Key 调用多个模型
  - 额度大，适合项目开发和测试
  - 实名认证后无每日调用次数限制 [[83]]
- ⚠️ 注意：需完成实名认证才能解锁全部免费额度

### 3️⃣ 讯飞星火（Spark Lite）⭐ 完全免费
- 🔗 官网：https://xinghuo.xfyun.cn
- 💰 **免费额度**：`spark-lite` 模型 **永久免费**，无 Token 限制 [[55]][[56]]
- ✅ 优势：
  - 真正永久免费，适合长期开发
  - 中文语音+文本多模态支持
- ⚠️ 限制：
  - Lite 版本能力较弱，复杂 JSON 生成可能不稳定
  - 建议仅用于开发调试，生产环境升级付费模型

### 4️⃣ 阿里云百炼
- 🔗 官网：https://bailian.aliyun.com
- 💰 **免费额度**：新用户 **每个模型 100万 Token**，有效期90天 [[65]][[73]]
- ✅ 优势：
  - 支持 Qwen、DeepSeek 等主流模型
  - 与阿里云生态集成好，适合后续部署
- ⚠️ 注意：免费额度用完后自动停止服务，需手动续费

---

## 🥈 第二梯队：国际平台（能力强 + 需科学上网）

### 5️⃣ Google AI Studio（Gemini）
- 🔗 官网：https://aistudio.google.com
- 💰 **免费额度**：
  - `gemini-1.5-flash`、`gemini-1.5-pro`：**免费调用**（有速率限制）[[24]]
  - 学生认证可额外获得 **$300 赠金**（90天有效期）[[90]]
- ✅ 优势：
  - JSON 输出稳定，适合 A2UI 格式生成
  - 多语言支持好，长上下文（128K）
- ⚠️ 限制：需科学上网，国内调用可能不稳定

### 6️⃣ Groq
- 🔗 官网：https://groq.com
- 💰 **免费额度**：**14,400 次请求/天**，30次/分钟 [[2]][[6]]
- ✅ 优势：
  - **极速响应**（毫秒级），适合实时对话场景
  - 支持 Llama 3、Mixtral 等开源模型
- ⚠️ 限制：模型选择较少，中文能力一般

### 7️⃣ OpenRouter（聚合平台）
- 🔗 官网：https://openrouter.ai
- 💰 **免费额度**：20请求/分钟，50请求/天（充值$10可提升至1000/天）[[1]]
- ✅ 优势：
  - 一个 API Key 调用 100+ 模型（GPT、Claude、Llama 等）
  - 统一接口格式，切换模型零代码修改
- ⚠️ 限制：免费额度较少，适合测试不适合生产

---

## 📊 快速对比表

| 平台 | 免费额度 | 中文能力 | JSON 稳定性 | 网络要求 | 推荐指数 |
|------|----------|----------|------------|----------|----------|
| **智谱 GLM** | 500万+2000万 Token | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 国内直连 | 🌟🌟🌟🌟🌟 |
| **硅基流动** | 2000万 Token 永久 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | 国内直连 | 🌟🌟🌟🌟 |
| **讯飞星火 Lite** | 永久免费 | ⭐⭐⭐⭐ | ⭐⭐⭐ | 国内直连 | 🌟🌟🌟 |
| **阿里云百炼** | 100万 Token/模型 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 国内直连 | 🌟🌟🌟🌟 |
| **Google Gemini** | 免费+学生$300 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 需科学上网 | 🌟🌟🌟🌟 |
| **Groq** | 14,400次/天 | ⭐⭐⭐ | ⭐⭐⭐⭐ | 需科学上网 | 🌟🌟🌟 |
| **OpenRouter** | 50次/天 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | 需科学上网 | 🌟🌟🌟 |

---

## 🎯 针对 AhaTutor 项目的配置建议

### 方案 A：纯国内组合（最稳）
```env
# .env 配置
DEFAULT_LLM_PROVIDER=glm
GLM_API_KEY=your_glm_key

# 备用（GLM 额度用完时切换）
# DEFAULT_LLM_PROVIDER=siliconflow
# SILICONFLOW_API_KEY=your_siliconflow_key
```

### 方案 B：国内 + 国际混合（能力最强）
```env
# 主用：智谱 GLM（中文+JSON 稳定）
DEFAULT_LLM_PROVIDER=glm
GLM_API_KEY=your_glm_key

# 备用：Google Gemini（复杂推理时切换）
GOOGLE_AI_API_KEY=your_gemini_key

# 你的 LLM 服务可配置自动降级逻辑：
# if (glm_quota_exhausted) → switch to gemini
```

### 方案 C：零成本开发（仅测试）
```env
# 主用：讯飞星火 Lite（永久免费）
DEFAULT_LLM_PROVIDER=spark
SPARK_API_KEY=your_spark_key
SPARK_MODEL=spark-lite

# 注意：Lite 模型生成复杂 A2UI JSON 可能不稳定
# 建议仅用于功能调试，上线前切换付费模型
```

---

## 🔧 快速接入指南（以智谱 GLM 为例）

1. **注册账号**：https://open.bigmodel.cn → 手机号注册
2. **创建 API Key**：控制台 → API 密钥 → 新建密钥
3. **配置项目**：
   ```bash
   # AhaTutor 根目录
   cp .env.example .env
   # 编辑 .env，填入：
   GLM_API_KEY=your_new_key
   DEFAULT_LLM_PROVIDER=glm
   ```
4. **测试调用**：
   ```bash
   cd src/backend
   pnpm start:dev
   # 访问 http://localhost:3001/api/docs 测试接口
   ```

---

## 💡 省钱小技巧

1. **开启缓存**：对相同问题启用 Redis 缓存，避免重复调用 LLM
2. **模板预置**：89 个遗传学知识点的 A2UI JSON 可预生成，AI 只填变量
3. **混合策略**：简单问题用免费模型（GLM-Flash），复杂推理用付费模型
4. **学生认证**：用 edu 邮箱申请 Google/GitHub 学生包，额外获赠金 [[88]][[91]]
5. **邀请好友**：智谱/硅基流动的推荐计划可叠加免费额度 [[47]][[80]]

---

> 🚀 **我的建议**：先用 **智谱 GLM**（500万+2000万 Token 够你开发好几个月），额度快用完时切换到 **硅基流动**（2000万永久额度），两者 API 格式兼容，切换成本几乎为零。

需要我帮你写一个 GLM API 的接入示例代码，或者配置 AhaTutor 的 LLM 路由逻辑吗？😊