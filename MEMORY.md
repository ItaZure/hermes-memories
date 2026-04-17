Kimi balance check script is at ~/hermes-files/kimi_balance.py. Requires MOONSHOT_API_KEY or KIMI_API_KEY environment variable to be set from https://platform.kimi.com/settings/api-keys. Remember to run it after every task completion.
§
When creating PPTs with pptxgenjs in JavaScript, need to be careful with quote escaping - use single quotes for strings containing double quotes (e.g., 'text with "quotes"') or escape properly to avoid SyntaxError.
§
File organization preference: All files created by Hermes should be placed in ~/hermes-files/ directory. This includes scripts, extracted data, PPTs, and any other output files. Check this folder first when looking for previously created files.
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