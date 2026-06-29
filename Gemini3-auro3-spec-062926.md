Aura-7 醫材合規追蹤平台：全面技術規格與架構白皮書 (v4.0.0-Enterprise)
1. 項目背景與願景：數位孿生與監管智慧的交匯
在現代醫療體系中，高風險醫療器材（如 Class-III 植入式起搏器、心臟瓣膜、人工關節等）的安全性、可追蹤性與合規管理是醫療品質的重中之重。中華民國台灣食品藥物管理署 (TFDA) 針對特定高風險醫療器材之來源與流向制定了極為嚴格的法律規範（依據《醫療器材管理法》第十九條第一項規定）。
Aura-7 平台 的誕生，旨在將繁瑣的法規轉化為自動化、視覺化且具備高度防錯機制的數位孿生平台。我們不只是在建立一個資料庫，我們是在建構一個具備「空間感知」與「神經推理」能力的合規中樞，確保每一件醫材在全台灣的流向皆如透明水晶般清晰。
2. 核心技術架構：企業級全棧工具箱
為了確保平台的高效能、強型別安全與卓越的使用者體驗，Aura-7 Enterprise 採用了現代工業界最成熟且最具擴充性的技術棧。
2.1 前端生態系 (The Frontend Ecosystem)
React 18 & TypeScript (TS)：平台核心基座，利用 Concurrent Mode 確保大規模數據處理時的 UI 響應性。
Tailwind CSS v4：利用其全新的引擎實現極致流暢的微觀原子化樣式控制，並全面支援 Pantone 語義化色彩配置。
Motion (framer-motion)：負責系統內複雜數據面板切換、彈窗動態、空間節點脈衝 (Pulse) 效果。
D3.js & Leaflet/Mapbox GL：支撐 WGS-84 地理空間看板與拓撲網絡圖的底層繪製引擎。
Three.js (可選擴充)：用於實現 3D 醫材結構與虛擬倉庫的「Wow」視覺特效。
2.2 後端與 AI 核心 (The Backend & AI Core)
Node.js & Express (TypeScript Native)：異步事件驅動的後端運行環境，處理大檔案上傳與串流。
Google Gemini API Suite：
gemini-3.1-flash-lite (預設)：作為高速、低延遲推理引擎，負責即時數據結構化。
gemini-2.0-pro (選配)：用於長文本法規分析與複雜對帳。
In-Memory SQL 引擎 (SQLite/DuckDB)：用於承載 LLM 轉譯後的標準 SQL 指令執行。
3. 「Wow」視覺特效與互動設計規格
視覺設計是 Aura-7 的靈魂，我們追求「科技感」與「專業感」的完美平衡。
3.1 LLM 執行過程的神經元視覺化 (Wow Execution Effects)
當 Gemini 模型在後端進行推理（如 NL-to-SQL 或數據標準化）時，前端將展示一個動態的神經元網路圖：
思考軌跡 (Thought Traces)：在對話框上方出現半透明的「粒子流」，象徵數據流向 AI 大腦。
節點脈衝 (Node Pulsing)：當 AI 辨識出關鍵欄位（如 UDI, Lot No）時，神經網絡中對應的節點會發出高對比色（如琥珀金）的脈衝光芒。
打字機 2.0 效果：Markdown 報告生成時，不僅是文字出現，還伴隨著輕微的螢幕震動與「數位掃描」聲效（可關閉）。
3.2 極致互動指示器 (Wow Interactive Indicators)
法規脈衝 (Regulatory Pulse)：對於 TFDA 核心列管品項，列表行會具備持續的「邊框呼吸」效果，且左側附帶一個 3D 旋轉的警告徽章。
空間漣漪 (Spatial Ripples)：當用戶在地圖上懸停於某個醫院據點時，該據點會向外擴散圓形漣漪，漣漪的顏色代表該院所的「風險評等」。
磁吸式光標 (Magnetic Cursor)：光標移近圖表關鍵節點時，會產生微小的吸引力，並自動彈出具備玻璃擬態 (Glassmorphism) 效果的懸浮資訊窗。
3.3 實時日誌系統 (Live Audit Log)
系統右側設有專屬的 Console 面板，實時滾動展示系統底層運作：
API 心跳 (API Heartbeats)：每當調用 Gemini API 時，會顯示毫秒級的延遲與 Token 消耗量。
數據檢核軌跡：顯示「正在執行 GS1 校驗... [成功]」、「正在比對 TFDA 公告資料庫... [命中]」。
系統狀態：以 Monospace 字體顯示當前記憶體佔用與 GPU 渲染壓力。
4. 「Wow」數據視覺化看板：六大圖表規格
這是平台的核心決策面板，旨在讓稽核官員在一秒內掌握全台風險。
圖表編號	名稱	技術實現	「Wow」特性與互動
Chart 1	GIS 地理空間流向分佈圖	Leaflet + WGS-84	台灣地圖上動態標註醫療機構，受災院所呈現暗紅色發光光環，支援 3D 傾斜視角。
Chart 2	供應鏈物流拓撲網絡圖	d3-force	展示製造商到醫院的流向。線條呈現螢光黃色「粒子流動動畫」，流速代表分銷頻次。
Chart 3	風險暴露桑基圖 (Sankey)	D3.js	展示召回原因與受災醫材品類的關聯。懸停時流動條會產生極光般的色彩漸變。
Chart 4	合規時序變遷趨勢圖	Recharts	X 軸為時間，Y 軸為違規天數。具備漸變區域陰影與動態浮動的臨界值警示紅線。
Chart 5	醫材生命週期漏斗圖	SVG Clip-Path	呈現從許可證核發到臨床消耗的留存。斷裂階段會以紅色「鋸齒狀切口」特效顯示。
Chart 6	法規分級風險矩陣雷達圖	Recharts Radar	呈現六個維度安全指標。覆蓋區域採半透明「極光色」填充，支援多個資料集重疊對比。
5. 核心功能模組與 AI 特色工程
5.1 多語系與多主題切換 (The Theme Engine)
語系支援：預設繁體中文 (Traditional Chinese) 與 英文 (English)。支援 AI 即時翻譯使用者輸入的非標註筆記。
10 大潘通色彩主題：
Classic Blue (19-4052)：專業穩重。
Living Coral (16-1546)：高度警示。
Ultimate Gray (17-5104)：平衡中性。
Very Peri (17-3938)：創新科技。
...等 10 種配色，支援 Light/Dark 模式下的自動對比度校正。
5.2 大語言模型深度整合 (Gemini Integration)
預設模型：gemini-3.1-flash-lite（極速回應）。
自選模型機制：使用者可透過 UI 切換至 gemini-1.5-pro 進行深度法規解析。
Prompt 修改工作區：開放高級使用者（Power Users）修改 AI 提示詞，例如設定 AI 輸出的專業度、口吻或特定的 Markdown 格式。
NL-to-SQL 編譯器：將自然語言轉換為 SQL，並在執行前提供「代碼檢查工作區」供人為審核，確保安全性。
5.3 三大全新「驚豔」AI 未來感擴展功能 (New AI Features)
1. AI 驅動的預測性風險擴散動態模擬器 (Risk Contagion Simulator)
技術原理：利用 Gemini 解析歷史物流與氣候數據，結合當前召回公告。
功能描述：當地圖上出現一個召回據點時，AI 會自動計算未來 14 天內，受影響醫材可能隨著患者轉院或物流重配而擴散的「風險熱區」。
視覺特效：在地圖上以橙色動態漣漪模擬「傳染路徑」，為預防性召回提供提前量。
2. 自主語義對帳與糾錯代理人 (Autonomous Semantic Reconciliation Agent)
技術原理：模糊語義匹配與序列號特徵提取。
功能描述：解決人為輸入錯誤（如將 0 誤打為 O）。AI 會自動辨識分銷單與採購單中的「高度相似但不完全一致」的紀錄，並彈出 AI 助手視窗：「我發現 98% 的重合度，極可能為 O/0 誤判，是否自動修正並關聯？」
價值：將對帳成功率從 85% 提升至 99.9%。
3. 語音互動式合規協同代理人 (Voice-Activated Compliance Co-Pilot)
技術原理：整合 HTML5 Web Audio API 與 Gemini 的語音處理技術。
功能描述：專為倉儲盤點人員設計。使用者可直接說出：「Aura，幫我找出過期天數大於 30 天的 Class-III 產品，並標記在地圖上。」
互動設計：系統會以 TTS (Text-to-Speech) 清晰回報處理結果，並自動切換 UI 視角至對應的圖表。
6. 數據策略與預設資料集架構
平台內置五大異質資料集，並透過 AI 執行主動關聯。
6.1 醫療器材召回資料集 (Recall Dataset)
包含美國 FDA 與台灣 TFDA 的召回公告。
Schema：title, device_name, manufacturer, date, recall_class, udi, sn_lot_no, reason.
6.2 醫療器材許可證資料集 (License Dataset)
TFDA 官方授權資料庫。
核心欄位：許可證字號、中文品名、英文品名、有效日期、製造廠國別。
6.3 TUDID 全球唯一識別資料集
醫材的身分證。
核心欄位：UDI-DI, 型號, 基本 DI, 註銷狀態。
6.4 智慧對帳管道 (Reconciliation Pipeline)
利用 UDI-DI 作為 Primary Key，關聯許可證資料庫；利用 SN/Lot No 作為次要 Key，關聯物流配送紀錄。AI 負責補全缺失的 Metadata。
7. 安全性與穩健性設計 (Robustness & Security)
7.1 SQL 注入與提示詞防禦
唯讀上下文：所有由 AI 生成的 SQL 指令皆在唯讀（ReadOnly）的記憶體資料庫實例中執行。
AST 解析器：後端在執行前會將 SQL 字串轉為抽象語法樹，攔截任何包含 DROP, DELETE, UPDATE 的非授權操作。
7.2 幻覺控制機制
RAG (檢索增強生成)：AI 輸出的法規報告必須標註來源條文，若無法命中法規庫，AI 將明確回報「證據不足」。
人工覆核按鈕：所有 AI 產出的建議皆附帶一個「官員覆核」開關，只有在人為點擊確認後，該紀錄才會寫入正式審核日誌。
7.3 效期衰變物理模擬 (Kinetic Aging Decay)
算法：
。
應用：AI 會根據醫院據點的濕度/溫度環境（若有 IoT 數據）預測醫材包裝劣化速率，提前發出重分配警報。
8. 專案實施路線圖 (v4.0.0 Milestone)
Phase 1 (UI/UX Foundation)：實作 Tailwind 4 與 Motion 的動態底座，建立 10 大 Pantone 主題與多語系網關。
Phase 2 (AI Core Integration)：對接 Gemini 3.1 接口，開發數據標準化 Pipeline 與 NL-to-SQL 引擎。
Phase 3 (Wow Visuals)：開發 WGS-84 地圖與 D3 拓撲網絡圖，加入粒子流動與脈衝特效。
Phase 4 (Enterprise Analytics)：完成六大圖表聯動與 Anomaly Hunter 異常檢測引擎。
Phase 5 (Wow HTML Export)：實現單一 HTML 文件導出引擎，包含完整離線運作能力。
9. 總結
Aura-7 v4.0.0-Enterprise 不僅是一個合規追蹤工具，它是醫療器材監理領域的「視覺化大腦」。透過 Gemini 3.1-flash-lite 的高速推理，搭配 Tailwind 4 與 Motion 的極致視覺呈現，我們將為 TFDA 稽核員與醫療機構提供前所未有的「合規感知力」。這份技術規格確保了系統在面對大規模異質數據時，依然能保持流暢、安全且具備高度的情緒價值（Wow Factor）。
10. 20 個全面性後續追蹤問題 (Comprehensive Follow-up Questions)
為了進一步優化本平台的架構設計，請團隊評估以下 20 個核心技術與法規問題：
地圖渲染效能：若平台導入的醫療機構節點突破上千家，目前的 Leaflet/SVG 混合渲染是否需要切換至 WebGL (Mapbox/Deck.gl) 以避免掉幀？
離線 Web Worker 執行：在斷網環境下使用「Wow HTML」導出檔時，如何將 Gemini 的標準化邏輯部分遷移至 Wasm (Web Assembly) 離線引擎？
SQL 注入深度防禦：目前的正則攔截是否能防禦高度變形的 SQL 注入提示詞（如 Hex 編碼繞過）？是否需要引入更嚴格的 AST 沙箱？
語義快取機制：頻繁的 NL-to-SQL 轉換會消耗大量 Token，是否應引入基於向量相似度 (Vector Similarity) 的 Redis 語義快取？
異質資料消歧義：當採購單寫「台大」而發貨單寫「NTU Hospital」時，AI Agent 的信心門檻值應如何設定以避免錯誤合併？
動態法規更新：當 TFDA 滾動修正列管品項清單時，平台如何實現「法規熱更新」而不需要重新部署前端代碼？
行動端視覺適配：六大 Wow 圖表在手機螢幕上的視覺體積極小，應設計怎樣的 Breakpoints 降級策略？（例如改為條列式卡片）
大檔案串流解析：若用戶上傳 500MB 的 CSV，後端架構如何確保不會出現 Node.js 記憶體溢出 (OOM)？
AI 幻覺與免責：AI 生成的風險報告若出現誤判，UI 應如何優化「人工覆核」流程以落實醫療法規責任歸屬？
UDI 解析與 Regex 防線：GS1 標準包含 DI 與 PI，我們是否需要在 AI 標準化前，先施加一套硬編碼的 Regex 正規表達式作為第一道防線？
多模型並發熔斷機制：當 Google API 發生 Rate Limit 時，後端路由該如何自動切換至備用模型或在地化規則引擎？
Wow HTML 安全性：導出的單一 HTML 文件如何確保不會被注入惡意第三方腳本？需要哪些 Content Security Policy (CSP) 設置？
資料脫敏與 PII：在帳籍上送 AI 前，如何確保自動過濾掉任何可能誤夾帶的患者姓名或病歷號（PII 數據）？
PDF 跨頁佈局優化：當 Markdown 報告長達 2000 字時，如何精確控制 CSS page-break 確保圖表不會被從中截斷？
語音互動噪音消除：在嘈雜的倉儲環境中，前端 Web Audio 是否需要引入低通濾波器或語音活動檢測 (VAD) 演算法？
密鑰管理與 On-Premise：若醫院部署在私有雲環境，Gemini API Key 如何與醫院內部的 Secrets Manager (如 Vault) 安全整合？
多租戶資料隔離：若升級為 SaaS 版本，如何確保 A 廠商絕對無法透過 SQL 注入查詢到 B 廠商的採購數據？
CSV 注入攻擊防禦：在導出 CSV 時，如何過濾掉所有以 = 開頭的惡意巨集字元？
Canvas 記憶體洩漏防護：頻繁重繪六大圖表時，如何確保 D3 的 Event Listeners 在 React 元件卸載時被完全釋放？
區塊鏈存證準備：系統底座是否具備 Append-Only 的審計日誌結構，以便未來無縫對接區塊鏈不可篡改帳本？
