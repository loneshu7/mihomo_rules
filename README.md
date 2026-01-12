# 🚀 Mihomo (Clash.Meta) Advanced Rules Profile

这是一个专为 **Mihomo (Clash.Meta)** 内核打造的高级配置文件。

本配置专注于**极致的分流体验**、**节点自动清洗**以及**灵活的策略组管理**。它集成了高质量的规则集，并针对流媒体、AI 工具（OpenAI/Gemini）以及特定应用场景进行了深度优化。

## ✨ 核心亮点 (Features)

### 1. 🎯 多维度策略组架构
不再是简单的“自动选择”。本配置为每个主流国家/地区（🇭🇰 HK, 🇯🇵 JP, 🇺🇸 US, 🇸🇬 SG 等）构建了三种维度的策略：
- **🔶 自动选择 (Auto):** 基于低延迟优先，自动切换最快节点。
- **🟢 故障转移 (Fallback):** 确保高可用性，节点挂掉自动切换。
- **🟨 手动选择 (Select):** 给予用户最大的控制权。

### 2. 🧹 智能节点清洗 (Regex Filtering)
利用强大的正则过滤逻辑，保持节点列表的“纯净”：
- **自动分组：** 自动识别节点名称中的国家标识，归类到对应地区。
- **排除干扰：** 自动在常规组中**剔除**包含“实验”、“测试”、“🔗”或“中转”字样的节点，防止不稳定节点影响日常体验。
- **独立实验区：** 设立 `🧪 实验低倍率` 独立分组，专门存放测试性质的节点，互不干扰。

### 3. 🔗 链式代理与中转逻辑 (Chain Proxy)
配置内置了高级的链式代理支持：
- **Dialer-Proxy 预设：** 定义了 `中转` 策略组，作为前置代理。
- **自建落地优化：** 包含针对自建 SS 节点的配置示例（`🔗 香港自建-SS-落地`），利用前置代理改善连接质量。

### 4. 📺 精细化服务分流
针对主流应用和服务配置了独立的策略组，图标精美，一目了然：
- **流媒体：** Netflix, YouTube, Disney+, Spotify, Bilibili, Emby, Pikpak
- **AI 工具：** OpenAI (ChatGPT), Gemini, Microsoft Copilot
- **社交/游戏：** Telegram, Twitter, Discord, Steam, Epic Games
- **其它：** Apple, Google, Microsoft, Cloudflare, Pornhub

### 5. 🔄 自动化规则集 (Rule Providers)
摒弃臃肿的单文件规则，采用 `rule-providers` 引用远程规则集（主要源自 `blackmatrix7`）：
- 每天自动更新规则，无需手动维护配置文件。
- 涵盖广告拦截 (AdBlock)、隐私保护、各大厂商分流规则。

### 6. 🛠 内核优化
- **DNS 优化：** 启用 `fake-ip` 模式，配合 H3/DoH (DNS over HTTPS)，解析速度快且防污染。
- **TUN 模式：** 预设 `strict-route` 和 `auto-route`，实现完美的系统级接管。
- **Geodata：** 使用 Meta 格式的 `geoip` 和 `geosite`，体积更小，查询更快。

---

## 📂 策略组预览

| 策略组名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| **🌐 代理** | 主控 | 总入口，控制所有流量走向 |
| **中转** | 筛选 | 用于链式代理的前置节点选择 |
| **🔶 自动选择** | Url-Test | 全球节点自动测速选择 |
| **🧪 低倍率** | 筛选 | 低倍率策略组需`Node Filters`处自定义关键词 |
| **OpenAI/Netflix...** | 应用 | 特定APP的专属策略 |

---

## ⚙️ 使用说明

1. **下载配置：** 下载本仓库的 YAML 文件。
2. **填写订阅：** 在 `proxy-providers` 部分，将 `url` 替换为你自己的机场订阅链接。
   - *提示：配置中保留了多个点阅示例用于多机场订阅使用，不需要的可以删除或者注释掉
3. **链式代理（可选）：** 如果你有自建落地节点，请在 `proxies` 头部填入你的节点信息，并确保 `dialer-proxy` 指向正确的策略组。
4. **加载运行：** 将文件导入 Mihomo/Clash.Meta 客户端即可使用。

---

## ⚠️ 免责声明
本配置文件仅供技术交流与学习使用。请遵守当地法律法规，切勿用于非法用途。

###### 感谢上游[mihomo_rules_profile](https://github.com/blackTangerine11/mihomo_rules_profile)本仓库配置仅倾向于博主本人个人使用习惯更改

