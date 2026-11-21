# Google's New Release Just Fixed AI Systems

- 來源：https://www.youtube.com/watch?v=k4sMSsMzX2g
- 頻道：AI LABS
- 時長：11:53
- 上傳日期：2026-06-26
- 影片 ID：k4sMSsMzX2g

---

## 一句話總結
Google 推出開放知識格式（Open Knowledge Format, OKF），用標準化的資料夾與 YAML metadata 結構，讓 AI 第二大腦更容易被代理人與人類共同理解、共享，並降低檢索成本。

## 重點摘要
- 現在很多人把 Claude code 當作業系統來經營「第二大腦」，但每個人各自設計結構、沒有標準，導致難以瀏覽也無法分享。
- 第二大腦常以 Claude.md 引導代理人，各資料夾也有專屬 Claude.md，但 Claude 仍常出錯：把檔案放錯位置、重複建立資料夾，因為它不知道知識庫裡已有類似內容。
- 根本問題在於 Claude 只靠關鍵字與檔名比對搜尋，面對大型、深層巢狀結構時需多次嘗試，既慢又耗 token。
- OKF 解決的核心是「標準化」，如同先前 MCP（外部資源溝通）、Skills（可重用指令）、design.md（設計意圖）所做的標準化一樣。
- 概念源自 Andrej Karpathy 的 LLM Wiki 模式：用 markdown 檔案累積知識，取代 RAG 向量法（後者每次提問都從零重建答案、無法累積知識）。
- OKF 把知識打包成 bundle，內含 markdown 檔，每個檔頭部加 YAML front matter 描述內容，讓代理人先讀描述再決定是否載入。
- 運作原理：資訊以「concept（概念）」物件表示，按主題分資料夾，每個資料夾都有最重要的 index.md 供代理人優先讀取以取得脈絡。
- 兩大設計原則：極簡主義（每個 concept 只代表單一事物，用 type 欄位標示）與知識庫和使用者分離（不綁定特定平台或對象）。
- OKF 隨附三樣工具：把 BigQuery 資料轉成 OKF 文件的 enrichment agent、HTML 互動圖視覺化工具，以及格式範例。
- 作者實測：因未用 BigQuery，自製「markdown to OKF」skill（script 為主、代理人只做判斷、附 evals 驗證），轉換後產生階層式 index.md，類似 Obsidian 的頁面連結與圖視圖。

## 關鍵結論／takeaways
- 測試後實際好處有二：更低的 token 用量與更快的檢索速度，並降低放錯檔案、重複建檔的錯誤率。
- 因 OKF 太新、Claude 預設不認得，需在 Claude.md 補上如何導覽該結構的說明，代理人才會改走 index.md 而非全庫關鍵字搜尋。
- 想轉換現有知識庫時，建議先開新分支實驗，避免動到主分支。
- 採 script-first 設計：用程式碼完成大部分工作、只讓代理人處理需判斷的部分，可減輕負擔並省 token。
- OKF 可能呼應 Google 將網路搜尋轉向「代理式搜尋」的方向——未來網站或許會在 LLMs.txt 之外，加上 OKF bundle 供代理人更有效率地查詢。
- 現階段模型本身的 pattern matching 已相當夠用，在 OKF 成為各代理開箱即用的標準之前，它比較像「優化選項」而非必需品。
