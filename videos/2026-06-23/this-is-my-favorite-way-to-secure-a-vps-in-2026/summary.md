# This is my favorite way to secure a VPS in 2026.

- 來源：https://www.youtube.com/watch?v=KqOceMFrMqA
- 頻道：Dreams of Code
- 時長：15:32
- 上傳日期：2026-06-23
- 影片 ID：KqOceMFrMqA

---

## 一句話總結
作者示範他在 2026 年偏好的 VPS 安全做法——用防火牆封鎖公網所有對內連線（焦土策略），再透過 Tailscale 私有網路存取後台服務、用 Cloudflare Tunnel 對外提供網站服務。

## 重點摘要
- 2026 年供應鏈攻擊與雲端服務（如 GitHub、Vercel）被攻破事件頻傳，因此主動強化資安姿態正當其時，尤其對使用 VPS 部署應用的人。
- 核心做法稱為「焦土策略」：用 Ubuntu 內建防火牆（UFW）封鎖公網 IP 上所有對內連線，預設拒絕所有 inbound，連 SSH 改 port 與否都已無關緊要。
- 此舉不僅擋下多種攻擊面，也能保護自己——例如不慎把資料庫等私有服務綁到公開連接埠時，仍不會曝露於公網。
- 私有服務存取靠 Tailscale：安裝後組成私有 mesh 網路（Tailnet），透過加密的 WireGuard 通道與僅限內網可達的 IP 連線；UFW 設定僅允許來自 Tailnet 裝置的連線。
- 實測驗證：用公網 IP 掃 port 22 或 SSH 皆 timeout，但連上 Tailnet 後可用 magic DNS 主機名正常 SSH；斷開 Tailnet 即失效。
- 對外網站服務改用 Cloudflare Tunnel：它對 Cloudflare 開「對外」連線（而非接受 inbound），由 Cloudflare 當反向代理，使用者打到 Cloudflare 而非 VPS。
- Cloudflare Tunnel 的好處：隱藏 VPS 真實 IP（OpSec）、提供 WAF（防 SQL injection、DDoS、機器人、零日漏洞如 2025 年底的 React Server Component RCE）、自動 HTTPS 憑證、速率限制，且採「明確 opt-in 才可存取」的安全模型。
- 設定流程：買網域 → 加入 Cloudflare 管理（改 name server）→ 建立 tunnel、安裝 cloudflared → 設定 DNS route 指向本機服務（如 localhost:3000），可選 path-based routing。
- 對於 Coolify／Dokploy 等自架平台的 GitHub webhook 重新部署問題：建議用 Tailscale 的 workload identity federation（搭配官方 Tailscale GitHub Action），讓 CI runner 連進 Tailnet 後以 API 觸發重新部署，無須對公網曝露服務。

## 關鍵結論／takeaways
- 把 VPS 公網 inbound 全部封鎖，是兼顧攻防與防呆的有效起點，但作者強調這不是萬靈丹，資安沒有銀彈。
- 私有服務（SSH、admin dashboard、自架平台前台）一律走 Tailscale，不對公網開放。
- 對外網站服務改用 Cloudflare Tunnel 的「對外連線」模式，順帶取得隱藏 IP、WAF、自動 HTTPS 與速率限制。
- 第三方服務（如 GitHub webhook 觸發部署）應透過 Tailnet + API 方式存取私有服務，而非為此打開公網連接埠。
- 在 AI 驅動的資安研究與攻擊日益興起的趨勢下，這種「預設拒絕、明確開放」的模型比「預設可存取」更值得採用。
