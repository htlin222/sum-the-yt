# Build an OKF brain like mine!

- 來源：https://www.youtube.com/watch?v=esYAIA6lU-s
- 頻道：Marie Haynes 
- 時長：22:48
- 上傳日期：2026-06-26
- 影片 ID：esYAIA6lU-s

---

## 一句話總結
作者展示了她依照 Google 開放知識格式（OKF）親手打造的個人「大腦」知識庫，說明它如何用標準化的 Markdown 檔案讓 AI agent 自動讀取、組織並運用知識，使日常 SEO 工作效率大幅提升。

## 重點摘要
- OKF（Open Knowledge Format）是 Google 推出的標準，它的價值不在於發明 Markdown，而在於把「給 agent 讀的知識檔案」變成一套通用規格，任何人的 agent 都能直接讀懂彼此的 OKF。
- 檔案結構簡單：核心是 `index.md` 與每個檔案開頭的 YAML front matter（標示 type、title、description、tags、timestamps），下方正文則完全選填，可放給 agent 的指令。
- 作者的大腦用幾種 type 分類：concepts、entities、playbooks、references、systems；type 是高階分類，tags 則負責讓檔案互相連結形成知識圖譜（knowledge graph）。
- 不需要會寫程式：作者非工程師背景，全程用 AI agent（她主要用 Google 的 Antigravity）打造，做法就是把 Google 的規格文件丟給語言模型，請它照著做。
- Playbook 是最實用的部分：例如「Google 更新後分析網站影響的檢查流程」原本要花兩天，做成 playbook 後，換客戶時叫 agent 跑一次就能快速產出滿意報告；也有定義溝通語氣（用「我」而非「我們」、口吻casual）的 playbook。
- OKF 與 RAG 的差異：不需把全部知識塞進 context window（耗 token），agent 先看 index 做「漸進式揭露」，只針對需要的單一 Markdown 檔做 RAG，速度較快、較省。
- 大腦會半自動成長：作者給它一個連結說「ingest this」，agent 會讀取、提出計畫（新增 reference、更新相關 concepts），經作者按鈕核可後才執行，並非完全自主。
- 技術細節：透過 Google Gemini API 使用 Gemini 3 Flash preview 模型（比 3.5 Flash 便宜且效果好），並設為 Antigravity 內的規則;大腦存在本機、每日備份到 GitHub。
- 作者也把社群（community.mariehaynes.com）的搜尋/AI 動態餵進 OKF，計畫做出個人化電子報；並另外設了會定期偵測 Google 文件是否更新的監控（這部分屬自寫軟體，非 OKF）。
- 作者對 OKF 與 skills.md 的差異仍感困惑，坦言這是大家邊做邊學的新領域，並鼓勵觀眾留言交流。

## 關鍵結論／takeaways
- 想自建類似系統：把 Google 的 OKF 規格文件連結（影片說明欄）連同這支影片的逐字稿，一起丟給你的 coding agent（Claude、ChatGPT Codex 或 Antigravity），請它「照 Marie 的方式」建立。
- 不要把整個網站每頁都做成一個 OKF 檔案；真正的威力在於把資訊拆解成「concepts」並用 tags 互相連結。
- 善用 playbook 把重複性的工作流程（如報告產出、分析流程、語氣規範）固化下來，一次建立、長期省時。
- 加上人類審核關卡（human-in-the-loop）：讓 agent 提計畫、你核可後再寫入，避免它放入不正確的內容;寫入前快速 skim 一遍。
- 預期要試幾次才會成功（作者第一版就因沒真正存成 Markdown 檔而重來），把它當成一項要練的新技能，重點是讓自己更有生產力而非取代工作。
- 務必做備份（如每日同步到 GitHub），以防程式覆寫或電腦遺失。
