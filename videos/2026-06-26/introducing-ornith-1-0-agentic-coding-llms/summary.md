# Introducing Ornith 1.0 - Agentic Coding LLMs

- 來源：https://www.youtube.com/watch?v=uD4-uy0GmHE
- 頻道：Sam Witteveen
- 時長：16:34
- 上傳日期：2026-06-26
- 影片 ID：uD4-uy0GmHE

---

## 一句話總結
Deep Reinforce 推出開源權重模型家族 Ornith 1.0，主打「自我搭建鷹架（self-scaffolding）」——讓模型自己學會為 agentic coding 任務即時撰寫專屬的 harness，而不再依賴人類手寫的腳手架。

## 重點摘要
- Ornith 1.0 是一組「自我搭建鷹架的 LLM」，核心理念是讓模型在解決問題的同時，也學會為該任務生成最合適的 harness／scaffold，等同於把「context engineering」交給模型自己做。
- 這不是全新的預訓練模型，而是基於 Qwen 3.5 與 Gemma 4 家族的微調／中段與後段訓練，共四個模型：9B（Qwen 3.5）、31B（Gemma 4）、35B MoE 與 397B MoE（皆 Qwen 3.5）。
- 與部分廠商不同，Ornith 把所有模型（含最大的 397B）全部開源釋出，方便不同算力條件的使用者嘗試。
- 訓練採兩階段 RL：先依任務與舊有 scaffold 提出精煉版 harness，再基於新 harness 產生 rollout（解題軌跡），並以多次 rollout 的結果作為獎勵訊號，用 GRPO 同時更新「生成鷹架」與「使用鷹架」兩種能力。
- 為防止 reward hacking（模型走捷徑騙取高分），設計了三層防線：① 沙箱環境與工具不可被模型修改（immutable）；② 確定性監控器，偵測是否竄改驗證腳本或使用未授權工具即懲罰；③ LLM-as-a-judge 可一票否決整個驗證結果。
- 基準測試上，最大模型可勝過 Qwen 3.7 Max、MiniMax 等，並與 Claude Opus 競爭；較小的 35B、甚至 9B 也能贏過體積常達其三倍的同級模型，9B 適合本地端有限算力的 coding 用途。
- 這個「模型自己寫程式當工具」的概念可追溯至 2022 年底／2023 初的 PAL 論文（讓模型寫 Python 算數學），Ornith 把它推進到「自動生成整套 scaffold」。
- 實測（35B MoE，於 Dell Pro Max + RTX 6000 Pro 上跑）：pelican SVG、RAG 問答表現不錯；要求「建立抓五日天氣預報的 harness」時，模型會生成清晰且切題的長 CoT 並產出程式碼，會要求 OpenWeather API key。
- 當被限制「沒有 API key」時，模型能理解隱含需求、改用免註冊的 Open-Meteo API 重寫腳本（含天氣代碼轉 emoji、GPS 座標處理）；抓 Twitter AI 新聞則改用 request 直接爬取（作者認為可能很快被封鎖，但邏輯合理）。
- 每次輸出結尾都會主動詢問是否要加上 Gradio／Streamlit UI；後續要求建 Gradio 介面時，模型理解已有 harness，僅快速補完 UI 而不重做整個流程。

## 關鍵結論／takeaways
- 若你想在本地端、無大型 GPU 的條件下跑 coding 模型，Ornith 的 9B 或 35B MoE 值得一試；想追求最高效能則可上 397B。
- Ornith 的真正價值不在跑分，而在「把 harness 當成可學習物件」這個範式——這是觀念上的轉變，可能也適用於 agentic coding 以外、只要獎勵訊號可驗證的領域。
- 想用 RL 訓練自我搭建鷹架的模型，務必正視 reward hacking：可借鏡其三層防線（不可變沙箱 + 確定性監控 + LLM 評審否決）。
- 範例皆為「一次性（one-shot）」生成，實務上可再串接：把執行結果回饋給模型、自動取出程式碼執行，形成迭代式 agent 迴圈。
- 作者結論務實：Ornith 目前還不會取代他日常的主力 coding 模型，但作為「讓模型自寫工具」的方向與本地端選項，是值得關注與動手實驗的專案。
