# 玩点什么 V4 · DeepSeek 实时推荐 / Live AI picks

## 启动与配置

安装 Node.js 22 或以上版本。将 `.env.example` 复制为 `.env`，填写：

```
AI_API_KEY=你的DeepSeek密钥
AI_BASE_URL=https://api.deepseek.com
AI_MODEL=deepseek-flash
PORT=3000
HOST=127.0.0.1
```

双击 `start.bat`，或运行 `npm start`，浏览器访问 http://127.0.0.1:3000 。修改配置后重启服务。密钥只由后端读取，请勿分享填写后的 .env。没有密钥时页面可打开，但不能生成推荐。

Install Node.js 22+. Copy `.env.example` to `.env`, enter your DeepSeek API key, then run `start.bat` or `npm start`. Visit http://127.0.0.1:3000 . Restart after editing configuration. Never share your configured `.env`.

## 推荐方式

“帮我决定”“理解并推荐”和“换一个”每次都请求后端，由 deepseek-flash 根据筛选条件、补充描述和近期游戏名现场选择真实游戏。没有内置候选游戏库，也没有本地推荐回退。补充描述可留空，仅用筛选条件即可推荐；平台与人数以筛选为准。请求失败显示错误，旧推荐如有则保留，不冒充新结果。

模型返回中英文游戏名、玩法、理由和本次建议时长，切换语言无需重新付费调用。游戏库仅保存已推荐的游戏，可手动标记拥有；历史保存在当前浏览器。旧版历史仍显示，但旧版游戏库的拥有标记因改用真实游戏名称标识，需要重新勾选。

Every recommendation and reroll calls DeepSeek. There is no fixed candidate catalog and no local fallback. Both languages are returned in a single response. Your library contains previously generated recommendations; it is not used as the candidate pool.

## 商店入口

未标记拥有的游戏提供商店搜索入口。PC 使用 Steam 搜索，手机提供 Google Play 与 App Store 搜索，桌游提供商品搜索。模型不生成商品网址或 Steam ID，因此不提供自动客户端启动，避免启动到错误游戏。拥有状态由用户维护，不会自动读取 Steam。

模型并未联网检索商店或价格；游戏是否存在、对应平台/模式是否正确、当地是否可售，仍可能有模型误差，请在商店确认。后端校验字段、平台/人数一致性和时长范围，不能替代外部事实核验。

## 验证与部署

运行 `npm test`：模拟 DeepSeek 服务检查现场推荐、不在原库中的游戏、去重、双语、异常响应、输入校验及密钥保护。测试不调用真实付费服务；真实连通需有效密钥后验证。

默认仅在本机运行。公开部署前需加用户认证、按用户配额和 HTTPS。当前限流为每 IP 每分钟 15 次、最多 4 个并发，进程重启会清空。

官方接口文档：https://api-docs.deepseek.com/zh-cn/
