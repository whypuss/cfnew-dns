# cfnew-cat 终端 v1.0

> ⚠️ **部署后请将兼容日期设置为 `2025-01-01`**
>
> ⚠️ **KV Namespace 已迁移，使用新的 Namespace ID（见 wrangler.toml）**

---

## 版本进度（v1.0）

### ✅ 已完成功能

**核心基础设施**
- Route 随机化（build.js，ROUTE_SEED_VERSION=1）
- Enum/constant name 随机化（vless→ak, ws→ku 等）
- Response key 随机化（ip→a, port→svc 等）
- Header key 随机化（X-Real-IP→cf-uf 等）
- `build/mappings.json` committed as artifact
- deterministic build（同一 seed 每次结果一致）

**静态资源**
- `static/` 目录（index.html, robots.txt, favicon.ico）
- 4 个 fake static assets（build 时注入，freeze at 4）
- Random response headers（x-build, x-edge, x-runtime）

**订阅功能**
- 多协议支持：VLESS、Trojan、xhttp、ECH
- KV 预编译 cache（15min TTL）
- 三层健康检查（TCP→TLS→WS）
- 节点信誉 + quarantine 系统
- 订阅输出过滤（20节点/80%/去重）
- 多客户端支持：CLASH、SURGE、SING-BOX、LOON、QUANTUMULT X、V2RAY、Shadowrocket、STASH、NEKORAY、V2RAYNG
- 隐藏订阅 URL
- **v1.05**: `?cc=` 国家过滤器（CF/CN/HK/JP/US 等）

**UI**
- 白色暖色调 UI
- 移除 Matrix/FX/HUD 动画
- `/api/config` — KV storage endpoint
- `/api/preferred-ips` — IP lookup endpoint

### ⚠️ 缺失 / 待实现

| 功能 | 优先级 | 状态 |
|------|--------|------|
| `/refresh` endpoint | P0 | ⚠️ 缺失 |
| `?refresh=1` query param | P0 | ⚠️ 缺失 |
| Config source tracing（`__trace`） | Stable-2 | ⚠️ 缺失 |
| Route registry centralization（`matchRoute`） | Stable-3 | ⚠️ 缺失 |
| Subscription MIME 多态 | P2-1 | ⏸️ 延期 |
| Query param polymorphism | P2-2 | ⏸️ 延期 |
| Rate limit（同 IP 30s） | P2-3 | ⏸️ 延期 |
| WebSocket connect backoff | P2-3 | ⏸️ 延期 |
| Fail fast（TCP 3s timeout） | P2-3 | ⏸️ 延期 |

---

## 部署说明

**Workers 部署：**
1. 登录 [Cloudflare 控制台](https://dash.cloudflare.com/)
2. 进入 **Workers 和 Pages** → 创建 Worker
3. 点击 **设置** → **运行时** → **兼容性日期** → 选择 `2025-01-01`
4. 粘贴 `worker.js` 的内容作为 Worker 代码

**Pages 部署：**
1. 进入 **Workers 和 Pages** → 创建 Pages 项目
2. 上传 `static` 目录
3. 设置兼容性日期 `2025-01-01`

**KV 配置：**
1. 在 Workers 页面左侧找到 **KV** → 创建命名空间（名称随意，如 `cfnew-cat`）
2. 复制新的 Namespace ID 到 `wrangler.toml`
3. 写入配置 key: `c`，value 为 JSON 配置

---

## 主要功能

- 自定义路径、订阅转换、延迟测试
- KV 图形化管理，配置实时生效
- 多客户端支持：CLASH、SURGE、SING-BOX、LOON、QUANTUMULT X、V2RAY、Shadowrocket、STASH、NEKORAY、V2RAYNG

## 节点地区（17个）

🇭🇰 香港 · 🇺🇸 美国 · 🇸🇬 新加坡 · 🇯🇵 日本 · 🇰🇷 韩国 · 🇩🇪 德国 · 🇸🇪 瑞典 · 🇳🇱 荷兰 · 🇫🇮 芬兰 · 🇬🇧 英国 · 🇦🇺 澳洲 · 🇧🇷 巴西 · 🇨🇦 加拿大 · 🇫🇷 法国 · 🇨🇭 瑞士 · 🇷🇺 俄罗斯 · 🇮🇳 印度 · 🇹🇼 台湾

**语言：** [中文](README.md) | [فارسی](فارسی.md)

[Telegram 交流群](https://t.me/+ft-zI76oovgwNmRh)