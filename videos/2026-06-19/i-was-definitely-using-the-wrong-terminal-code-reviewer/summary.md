# I Was Definitely Using The Wrong Terminal Code Reviewer

- 來源：https://www.youtube.com/watch?v=-4fJbIF8WAs
- 頻道：DevOps Toolbox
- 時長：13:33
- 上傳日期：2026-06-19
- 影片 ID：-4fJbIF8WAs

---

## 一句話總結
介紹 Mitchell Hashimoto 推崇的終端機程式碼審查工具 Hunk——一個具備語法高亮、GitHub 風格 diff 面板與 AI 行內註解的 TUI，專為本地端 code review 而生。

## 重點摘要
- 程式碼審查在 AI 大量產出程式碼（slop）的時代變得更吃重，工程師需要更好的本地審查工具來「把關」。
- Hunk 由前 Sentry 共同創辦人 Ben Vinegar 打造，建構在 Anomaly 的 Open TUI、PR diffs 渲染函式庫與 Shiki 語法高亮之上。
- 安裝簡單（`npm` 或 `brew install hunk`），兩個核心指令：`hunk diff`（未提交的本地變更）與 `hunk show`（預設審查最後一次 commit）。
- 操作支援 Vim 風格快捷鍵（Ctrl+D/U、方括號跳 hunk、GG/Shift+G、HJKL）與滑鼠，可切換堆疊或並排（side-by-side）檢視、主題與側邊欄（按 S 切換）。
- 從 GNU diff（51 年前發布）談到 git diff、diff-so-fancy、delta、diffnav、lumen 等演進，Hunk 的差異化在於互動式 TUI 加上行內 agent 與 AI 註解。
- 核心殺手級功能是「Notes」：類似 GitHub 行內留言的文字泡泡，可由人或 AI 留下；但這些註解不入 Git 版控，僅存於當前 session，結束即消失。
- Hunk 對 Git 與 Jujutsu（JJ）皆為一等公民支援，這正是 Mitchell Hashimoto 偏好它的主因。
- AI 工作流：透過 `hunk session` 在背景跑小型伺服器，搭配 skill 與通用 prompt 讓 agent（影片用 Pi）審查 diff 並留下註解；後續 session 還能讓 agent 讀取前一個 session 的註解並修正。
- 設定檔為 TOML（預設位於 `~/.config/hunk`），可設定版控系統、檢視模式、主題、行號、註解預設開關，並能用 stow 管理 dotfiles。
- 額外功能：`hunk stash show` 可直接審查 stash 中的變更（免 pop/restash）；也能設為 Git 的 pager，或設定 alias（如 `h show`）。

## 關鍵結論／takeaways
- 若你主要做「本地端」程式碼審查，Hunk 目前是作者看過最好的選擇，尤其同時用 Git 與 JJ 的人。
- 善用 AI 註解工作流：一個 agent session 留審查意見，另一個 session 讀取並修正，可搭配「babysitter」提升品質。
- 注意限制：Notes 不入版控、無法分享 session、不與 GitHub 留言同步，因此目前不適合「協作式」審查。
- 需要團隊協作、能讓他人看見留言的審查，仍應考慮 gh-dash + Octo + Vim 或 LazyGit 等整合 GitHub 的方案。
- 遵循 Unix 哲學「用對的工具做對的事」：Hunk 把本地 diff 審查這件事做到極致，但它不是萬用 GitOps 工具。
- 可將 Hunk 設為 Git pager 或建立 alias，無痛融入既有工作流；用 TOML 設定檔加 stow 讓偏好跨機器同步。
