# 🎮 FreezeHost 自动续期助手 (Pro Max)

基于 Playwright + GitHub Actions 打造的 **全自动、免打扰、防封控** 的 FreezeHost 免费服务器续期脚本。

## ✨ 核心特性

- 🛡️ **全新 Token 注入登录**：彻底抛弃传统账号密码，完美绕过 Discord 多端登录拦截、图形人机验证 (hCaptcha) 和二次验证 (2FA)。
- 🔄 **多账号无缝支持**：支持填入多个 Discord Token，全自动为每个账号分配独立的隔离沙盒，互不串号。
- 🖥️ **全量服务器巡检**：不管一个账号下挂了多少台免费服务器，脚本会自动遍历检查并精准续期。
- 💰 **实时金币探测**：全网首创！每次续期同时智能抓取账号当前的“💰 实时金币余额 / AVAILABLE BALANCE”并在 Telegram 战报中显眼展示。
- ⚡ **环境缓存提速**：引入 Actions 依赖缓存机制与失败自动重试 (Retry) 配置，兼顾极速运行与超高稳定性。

## ⚙️ 配置步骤

### 1️⃣ Fork 此仓库到您的 GitHub

### 2️⃣ 添加 Secrets
进入仓库 → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**：

| 🔑 Secret 名称 | 📝 格式 | ✅ 必填 |
|---|---|---|
| `DISCORD_TOKEN` | `你的 Discord Token (多个账号请用英文逗号 , 隔开)` | ✅ |
| `TG_BOT` | `chat_id,bot_token` | ✅ |
| `GOST_PROXY` | `socks5://host:port` 或 `http://host:port` | 可选 |

> **💡 如何获取 Discord Token？**
> 1. 在电脑浏览器中登录 [Discord 网页版](https://discord.com/app)。
> 2. 按 `F12` 打开开发者工具，切换到 **Network (网络)** 面板。
> 3. **关键步骤**：在 Network 面板的过滤选项卡中，选中 **"Fetch/XHR"**。
> 4. 保持面板打开，回到 Discord 页面并**随便点击左侧的其他服务器或频道**。
> 5. 这时 Network 列表会出现一些名为 `science`、`messages` 或 `typing` 的请求，点击其中一个。
> 6. 在右侧弹出的 **Headers (标头)** 标签页里向下滑，找到 **Request Headers (请求标头)** 区域。
> 7. 在里面寻找名叫 `Authorization` 的字段，它后面的那一串复杂字符就是您的 Token！直接复制下来即可。

### 3️⃣ 启用 Actions
进入 **Actions** 标签页，点击绿色按钮 **I understand my workflows, go ahead and enable them**。

### 4️⃣ 手动触发测试
进入 **Actions** → 左侧点击 **🎮 FreezeHost 自动续期** → 右侧点击 **Run workflow**。

## 🕐 运行机制与频次

- **智能续期阈值**：FreezeHost 官方规则为少于 7 天可续期并重置至 14 天。脚本会在识别到剩余时间 `<=` 7 天时才执行续期动作，避免徒劳无功。
- **默认执行频率**：配置为 **每 3 天**（即每月 1, 4, 7... 号）的北京时间 16:00 自动运行一次，完美契合机制并防止频繁刷新触发官方风控。
- *(如需修改频率，请前往 `.github/workflows/freeze.yml` 的 `cron` 表达式中调整)*

## 📊 Telegram 效果展示

```text
📝 所有账号处理完毕:

【账号 1】 💰金币: 2,078
   [Server 1]: 无需 (剩余 12.5 天 (需 ≤7 天))
   [Server 2]: ✅ 续期成功

【账号 2】 💰金币: 345
   [Server 1]: ⚠️ 余额不足
```
