When creating PPTs with pptxgenjs in JavaScript, need to be careful with quote escaping - use single quotes for strings containing double quotes (e.g., 'text with "quotes"') or escape properly to avoid SyntaxError.
§
Hermes overriding base url warning: Even if base url is set in config.yaml under the model block, the kimi-coding provider internal logic might override it using environment defaults. For legacy Moonshot keys you MUST explicitly set KIMI_BASE_URL to api.moonshot.cn/v1 in the environment to force the correct endpoint. Kimi k2.5 also strictly requires temperature 1.0.
§
User's NAS is running fnOS v1.1.26 (飞牛).
§
Infrastructure setup:
- NAS running fnOS v1.1.26 (飞牛), Tailscale IP 100.85.28.37
- MacBook laptop (sleeps, not 24/7)
- Tailscale for cross-subnet networking
- Docker for NAS services
- Uses Syncthing for file sync between devices
- Messaging platforms: WeChat, Feishu, Discord, Telegram
- OpenRouter user, encountered Gemini 3.1 Pro regional restrictions (China IP)
§
用户工作风格偏好：不喜欢一次性给太多信息，要求一步步来，简洁明了。执行命令时需要包含sudo，避免手动添加。
§
用户NAS设备信息：
- 设备名：MEmini（飞牛NAS）
- 系统：fnOS v1.1.26
- Tailscale IP：100.85.28.37
- 数据路径：/vol1/1000/hermes-data
§
用户Hermes使用场景：
- 笔记本（MacBook）：本地运行，处理本地文件、终端操作、工具调用
- NAS：24/7运行，主要作为聊天服务器，对接微信/飞书
- 需求：两边记忆/SOUL.md数据同步
§
用户网络环境：
- 使用Tailscale打通跨子网访问
- 笔记本常休眠，NAS常开
- 两边通常不在同一子网
§
自定义API提供商调试（如Poe API）：当使用config.yaml中的providers配置自定义提供商时，Hermes内部存在硬编码问题。runtime_provider.py会将provider名称硬编码为"custom"，并在_openrouter_runtime中限制base_url使用。调试时发现：1) Hermes无法识别"poe"为内置provider，导致resolve_provider抛出AuthError；2) _resolve_named_custom_runtime总是返回"custom"作为provider名称；3) _try_resolve_from_custom_pool接收硬编码的"custom"标签；4) _resolve_openrouter_runtime仅在requested_norm=="custom"时使用config中的base_url。修复这三个位置的代码后，Poe API可正常工作：model_cfg字段必须存在，且provider字段必须匹配providers下的自定义provider名称。