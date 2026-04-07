# 1.TCREI 

**TCREI** 是一个 **AI 提示词（Prompt）编写框架**

| 字母    | 英文                             | 中文       |
| ----- | ------------------------------ | -------- |
| **T** | Task                           | 任务       |
| **C** | Context                        | 上下文/背景   |
| **R** | Resources / References / Rules | 资源/参考/规则 |
| **E** | Evaluate                       | 评估       |
| **I** | Iterate                        | 迭代       |
## 🎯 实际使用示例
### T - Task
请用智谱 GLM-4-7 模型调用示例，写一个 Python 脚本调用 OCR 接口识别图片文字
### C - Context
我是大一软件工程学生，正在学习 API 调用，需要代码有详细注释
### R - Resources/Rules
- 使用 zhipuai 官方 SDK
- 图片路径作为函数参数
- 添加异常处理
- 输出用中文注释
### E - Evaluate
请确保：
1. 代码可直接运行（假设已安装依赖）
2. 包含关键步骤的 print 日志
3. 说明如何配置 API Key
### I - Iterate
如果代码有兼容性问题，请提供替代方案或排查建议

# 2.ai的类别
## 1. 通用推理引擎
如ChatGPT, Claude, Gemini，擅长逻辑、写作、编码和总结
## 2. 研究引擎
如Perplexity, NotebookLM, Consensus，注重准确性并引用来源
## 3. 专业工具
如Midjourney, ElevenLabs, Cursor，专注于特定领域以提供高质量输出
## 4. 工作流自动化工具
如Zapier, Make, n8n，用于数据流转和系统集成

# 3.AI代理

AI代理不再仅仅是提供建议的聊天机器人，而是能够自主执行复杂多阶段任务的系统。无论是预构建代理（如Perplexity的Clods Projects, Gemini Deep Research）还是自定义代理，都能通过设定目标后自动完成从检测到发送的整个流程，将用户从繁琐的中间人角色中解放出来。

# 4.开源

理解开源AI的巨大潜力。与闭源AI（租用智能）不同，开源AI（拥有引擎）让用户能本地化处理数据，确保隐私、消除对第三方提供商的依赖，并摆脱使用限制和订阅费用。虽然ChatGPT对普通用户可能更易用，但越来越多AI初创公司正在转向开源。如Ollama这样的免费工具，让用户可以在本地运行Llama、DeepSeek等模型。