# Mihomo (Clash.Meta) Advanced Rules Profile

这是一份面向 Mihomo 的多机场分流模板，提供节点筛选、地区策略组、链式代理、服务分流和远程规则集。公开版本不包含真实订阅、手写节点凭据、私有 DNS 或 hosts 映射。

## 主要功能

### 多维度节点策略

常用地区分别提供以下模式：

- **自动选择（url-test）**：周期测速，优先使用延迟较低的可用节点。
- **故障转移（fallback）**：当前节点不可用时按顺序切换。
- **负载均衡（load-balance）**：使用 `consistent-hashing` 在优质节点池中分摊连接；它不会自动选择最低延迟节点。
- **手动选择（select）**：由用户固定地区或具体节点。

负载均衡组应只包含已经筛选过的稳定节点。需要调整节点池时，请修改配置中的 `Node Filters` 正则。

### 链式代理

`中转` 策略组可作为落地节点的前置代理。仓库中的 `LandNode` 是本地文件示例，其 `dialer-proxy` 已指向 `中转`；真实节点和凭据请只保存在未提交的本地文件中。

### 服务分流

配置包含常用服务策略组，例如 OpenAI、Gemini、Telegram、Twitter、Instagram、Netflix、YouTube、Spotify、Bilibili、Steam、Epic、GitHub、Apple、Microsoft、Google、Cloudflare、Emby、Pikpak 和 Binance。

### MRS 规则集

大部分域名和 IP 规则使用 MetaCubeX `meta-rules-dat` 提供的 MRS 文件，减少规则解析开销；隐私拦截规则仍使用兼容的 classical YAML 来源。`rule-providers` 会按配置的 `interval` 自动更新并缓存到 `path`。

### DNS 与 TUN

- 使用 `fake-ip` 增强模式。
- 国内/私有域名由国内 DoH 解析，其他域名使用 Cloudflare 和 Google DoH。
- 代理节点域名通过 `proxy-server-nameserver` 独立解析。
- TUN 开启自动路由、严格路由和 DNS 劫持。


## 使用方法

1. 下载 [`profile/mihomo.yaml`](https://github.com/loneshu7/mihomo_rules/blob/main/profile/mihomo.yaml)。
2. 在本地副本的 `proxy-providers` 中填写自己的订阅地址，不使用的示例 provider 可以删除。
3. 如需链式代理，在 `proxy_provider/LandNode.yaml` 中维护落地节点，并确认 `dialer-proxy` 指向 `中转`。
4. 根据机场节点命名调整 `Node Filters` 中的地区和排除关键词。
5. 导入 Mihomo 客户端并先执行配置校验，再启用 TUN。

## 配置结构

| 区域 | 用途 |
| --- | --- |
| `proxy-providers` | 订阅和本地节点来源 |
| `dns` / `tun` | DNS 解析与系统流量接管 |
| `Node Filters` | 按地区和关键词筛选节点 |
| `Proxy Group Templates` | 自动、回退、均衡等公共参数 |
| `proxy-groups` | 主入口、地区模式和应用策略组 |
| `rule-providers` | 远程 MRS/YAML 规则源 |
| `rules` | 自上而下执行的最终分流顺序 |

## 免责声明

本配置仅供技术交流与学习使用。请遵守所在地法律法规及所使用服务的条款。

感谢上游项目 [blackTangerine11/mihomo_rules_profile](https://github.com/blackTangerine11/mihomo_rules_profile)。本仓库配置按个人使用习惯进行了调整。
