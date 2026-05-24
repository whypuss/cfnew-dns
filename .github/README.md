# cfnew-cat v1.03

> ⚠️ **部署后请将兼容日期设置为 `2026-01-20`**

---

## 🐱 v1.03 更新内容（2026-01-20）

### 修复
- **direct-domains 恢复**：VoWiFi/CMI 移动用户可通过 `epd=yes` 开启 direct-domains，节点直连 IP 绕过域名
- **DoH 多 Provider 回退**：`resolveDomainsToIPs` 支持 cloudflare-dns.com → dns.google → quad9.net 任一成功即返回

### v1.02 Quarantine 修复（保留）
- **backupHost 漏網**：6 處 `bestBackupIP.domain` 全部改為 `.address`，彻底切断域名依赖
- **Quarantine 繞過**：`source === 'direct-domains'` 的節點跳過 quarantine 檢查
- **Quarantine Key**：从 IP 級別改為 IP+Port 複合 key，避免同一 IP 不同端口被錯誤隔離

### v1.01 DNS 迴圈修復（保留）
- **backupIPs 硬編碼**：移除所有 `ProxyIP.*.CMLiussss.net` 域名，改用 Cloudflare Anycast IP
- **`forwardTCP` retryConnection**：fallback 階段直接使用 `.address`

---

## ✅ 已完成功能

**核心基礎設施**
- Route 隨機化（build.js，ROUTE_SEED_VERSION=1）
- Enum/constant name 隨機化（vless→ak, ws→ku 等）
- Response key 隨機化（ip→a, port→svc 等）
- Header key 隨機化（X-Real-IP→cf-uf 等）
- `build/mappings.json` committed as artifact
- deterministic build（同一 seed 每次結果一致）

**靜態資源**
- `static/` 目錄（index.html, robots.txt, favicon.ico）
- 4 個 fake static assets（build 時注入，freeze at 4）
- Random response headers（x-build, x-edge, x-runtime）

**訂閱功能**
- 多協議支持：VLESS、Trojan、xhttp、ECH
- KV 預編譯 cache（15min TTL）
- 三層健康檢查（TCP→TLS→WS）
- 節點信譽 + quarantine 系統
- 訂閱輸出過濾（20節點/80%/去重）
- 隱藏訂閱 URL

**UI**
- 白色暖色調 UI
- 移除 Matrix/FX/HUD 動畫
- `/api/config` — KV storage endpoint
- `/api/preferred-ips` — IP lookup endpoint

---

## 部署說明

**Workers 部署：**
1. 登錄 [Cloudflare 控制台](https://dash.cloudflare.com/)
2. 進入 **Workers 和 Pages** → 創建 Worker
3. 點擊 **設置** → **運行時** → **兼容性日期** → 選擇 `2026-01-20`
4. 粘貼 `worker.js` 的內容作為 Worker 代碼

**Pages 部署：**
1. 進入 **Workers 和 Pages** → 創建 Pages 項目
2. 上傳 `static` 目錄
3. 設置兼容性日期 `2026-01-20`

**KV 配置：**
1. 在 Workers 頁面左側找到 **KV** → 創建命名空間（名稱隨意，如 `cfnew-cat`）
2. 複製新的 Namespace ID 到 `wrangler.toml`
3. 寫入配置 key: `c`，value 為 JSON 配置

---

## 主要功能

- 自定義路徑、訂閱轉換、延遲測試
- KV 圖形化管理，配置實時生效
- 多客戶端支持：CLASH、SURGE、SING-BOX、LOON、QUANTUMULT X、V2RAY、Shadowrocket、STASH、NEKORAY、V2RAYNG

## 節點地區（17個）

🇭🇰 香港 · 🇺🇸 美國 · 🇸🇬 新加坡 · 🇯🇵 日本 · 🇰🇷 韓國 · 🇩🇪 德國 · 🇸🇪 瑞典 · 🇳🇱 荷蘭 · 🇫🇮 芬蘭 · 🇬🇧 英國 · 🇦🇺 澳洲 · 🇧🇷 巴西 · 🇨🇦 加拿大 · 🇫🇷 法國 · 🇨🇭 瑞士 · 🇷🇺 俄羅斯 · 🇮🇳 印度 · 🇹🇼 台灣

**語言：** [中文](../README.md) | [فارسی](../فارسی.md)

[Telegram 交流群](https://t.me/+ft-zI76oovgwNmRh)
