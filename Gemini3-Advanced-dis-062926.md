Aura-7 醫材合規追蹤平台：全面技術規格與架構白皮書 (v4.0.0-Enterprise)
1. 項目背景與願景：為什麼我們需要 Aura-7？
在高風險醫療器材（Implantable Medical Devices）的管理領域中，安全性、追溯度與法規合規性是維繫醫療安全品質與病患生命健康的絕對防線。Class-III 醫療器材，例如植入式心律調節器（Implantable Pacemakers）、人工心臟瓣膜（Prosthetic Heart Valves）、人工關節、血管支架以及深部腦刺激器等，一旦在臨床使用後發生產品瑕疵、軟體設計缺失（Firmware Bug）或無菌包裝破損，其對患者與醫療機構帶來的風險與後續法律責任是極其巨大的。
中華民國衛生福利部食品藥物管理署 (TFDA) 針對特定高風險醫療器材之來源與流向制定了極為嚴格的法律規範。依據《醫療器材管理法》第十九條第一項規定，公告「應建立與保存來源及流向資料之醫療器材」品項，法規要求製造業、販賣業者及醫療機構必須精準記錄並保存每一件醫材從輸入、製造、流通至臨床使用的完整生命週期軌跡。其目的在於確保當國際（如美國 FDA）或國內發布重大醫材召回公告（Medical Device Recalls）時，監管單位與醫療機構能在數小時內精確鎖定受影響的批號與特定患者，迅速啟動防範與精準召回程序。
然而，在現行的業界實務與稽核流程中，合規管理面臨著三大核心痛點：
多源異質數據割裂 (Heterogeneous Data Silos)：美國 FDA 召回公告、台灣 TFDA 法規公文、全球唯一醫療器材識別碼 (UDI) 資料庫、醫療許可證資料庫、企業內部供應鏈分銷 (Distribution) 與採購 (Purchase) 數據等，散落在不同的 JSON、CSV、PDF、XML 甚至是紙本表單中，缺乏統一的模型進行整合與交叉校對。
人工對帳與轉譯成本高昂 (Manual Reconciliation Overhead)：將非標準格式的第三方召回公告轉譯為合規的結構化數據，並將其與企業內部成千上萬筆物流記錄進行比對，需要耗費法務與資訊人員大量的工時。手動編寫複雜的 SQL 查詢不僅緩慢，且極易產生人為疏漏。
缺乏空間感知與動態視覺化 (Lack of Spatial & Network Awareness)：傳統的二維報表無法直觀呈現召回器材在地理空間上的擴散路徑，亦無法揭示供應鏈拓撲網絡中的中介高危節點，這使得決策者難以在第一時間評估受災區域的嚴重性並制訂最佳的應急物流調撥方案。
Aura-7 平台 的誕生正是為了解決上述痛點。我們建構了一個基於先進人工智慧（Generative AI）與空間地理拓撲網絡的企業級合規監控、追蹤與召回管理工作區。Aura-7 不僅是一個數據展示面板，更是一個具備高度防錯機制、具備大語言模型（LLM）神經推理能力，且能自適應多種物理監控站點（DHA Stations）的數位孿生平台。
核心願景
端到端極致透明 (End-to-End Transparency)：確保每一件屬於「應建立與保存來源及流向資料之醫療器材」品項之高風險醫材，從海關進口、盤點入庫、分銷物流到院所終端，皆具備毫秒級的追蹤能力。
主動式智能干預 (Proactive AI Intervention)：利用 LLM 的跨域推理能力，將事後被動補救轉化為事前合規預測、自主對帳糾錯與自動化召回範圍劃定。
多維度空間感知 (Multidimensional Spatial Awareness)：將冰冷的供應鏈流水賬轉化為動態地理分佈圖與拓撲網路圖，讓決策者直觀理解召回危機的空間蔓延路徑，極大化縮短危機處理時間。
2. 核心技術架構：企業級全棧工具箱與設計模式
為了確保平台的高效能、強型別安全、極致的安全隔離與卓越的使用者體驗，Aura-7 Enterprise 採用了現代工業界最成熟且最具擴充性的技術棧。
code
Code
+-----------------------------------------------------------------------------------+
|                                  Aura-7 前端層                                     |
|  [React 18 / TS] -> [Tailwind CSS v4] -> [Motion] -> [Wow HTML / Canvas / SVG]   |
+-----------------------------------------------------------------------------------+
                                         |
                                         | RESTful API / JSON RPC
                                         v
+-----------------------------------------------------------------------------------+
|                                  Aura-7 後端層                                     |
|  [Node.js / Express] -> [tsx Engine] -> [SQLite / DuckDB In-Memory SQL Engine]   |
+-----------------------------------------------------------------------------------+
                                         |
                                         | Native API / SDK Call
                                         v
+-----------------------------------------------------------------------------------+
|                                AI 核心與大語言模型層                                |
|  [Google Gemini API] (gemini-3.1-flash-lite / gemini-1.5-pro / gemini-2.5-pro)     |
+-----------------------------------------------------------------------------------+
2.1 前端架構 (The Frontend Ecosystem)
React 18 & TypeScript (TS)：平台的核心基座。React 18 的 Concurrent Mode（並發模式）與 Transition API 確保了在處理上萬筆召回資料與複雜圖表切換時，介面依舊保持流暢、無卡頓。TypeScript 則透過嚴格的型別定義（Type Definitions），在編譯期阻斷因欄位缺失、未經校驗的 API 響應或型別污染導致的合規計算錯誤。
Vite & esbuild：極速構建與模組打包工具。利用原生 ESM 特性實現極速的熱更新，並確保生產環境的代碼分割（Code Splitting）與 Tree-shaking 達到最佳化，降低前端加載延遲。
Tailwind CSS (v4)：採用全新的 CSS 變數引擎與組合式設計系統，提供極致流暢的微觀原子化樣式控制。內建的自適應變數體系全面支援企業級暗黑模式 (Dark Mode) 與語意化色彩配置。
Motion (framer-motion)：負責系統內複雜數據面板切換、彈窗動態、空間節點脈衝 (Pulse) 效果的物理特性動畫控制，提升操作者的專注度與視覺層次。
Recharts & Dynamic SVG/Canvas Engine：用於繪製常態合規趨勢圖表，並結合低階 Canvas/SVG 混合渲染技術，實現大規模高負載下的空間圖表繪製。
2.2 後端與資料庫引擎 (The Backend & Storage Infrastructure)
Node.js & Express (TypeScript Native Via tsx)：異步事件驅動的後端運行環境。利用 tsx 執行引擎實現無需手動 Webpack 編譯的 TypeScript 原生高效執行，處理大檔案上傳與串流 (Streaming) 反應。
In-Memory SQL Serverless 引擎 (SQLite / DuckDB)：系統內置的高效能、無伺服器嵌入式關聯型資料庫。前端或後端邊緣節點可動態建立記憶體資料庫，用於承載 LLM 轉譯後的標準 SQL 指令執行，支援複雜的多表聯查 (JOIN) 與秒級大數據聚合。
2.3 人工智慧與大語言模型核心 (The AI Core Orchestration)
Google Gemini API Suite：
gemini-3.1-flash-lite (系統預設)：作為預設的高速、低延遲推理引擎，專門負責即時的非標準數據結構化轉換（Data Standardization）、自然語言轉 SQL 命令（NL-to-SQL）以及大批量的即時欄位比對。
gemini-1.5-pro / gemini-2.5-pro (用戶自選高級模型)：具備百萬級超長上下文視窗 (Long Context Window)，用於深度理解數萬字的 FDA/TFDA 法規原始文檔、執行極為複雜的多源跨表對帳 (Autonomous Reconciliation) 任務，以及產出高達數千字的綜合性合規分析報告。
3. Sophisticated Dark 設計語彙與視覺工程
Aura-7 的設計風格採用了 Sophisticated Dark（精緻暗黑） 的視覺主題。此設計旨在擺脫傳統管理軟體平庸、沉悶的刻板印象，為醫療器材合規專員及 TFDA 稽核官員營造一種冷計、精準且具備極致未來感的專業監控艙體驗。
3.1 顏色調配與物理配搭 (Palette & Sensory Feedback)
深色背景基底：採用深邃的炭黑（#050505）與冷灰（#0a0a0a、#0c0c0c）作為頁面底色與卡片底色，降低光線對眼部的刺激，並提供極佳的對比底層。
高亮指示色彩：
Amber Gold (琥珀金, #f59e0b)：作為系統的合規警示與核心品牌色。代表需要密切注意但尚未完全失控的合規節點，或「應建立與保存來源及流向資料之醫療器材」法規強制列管品項。
Emerald Green (翡翠綠, #10b981)：代表數據對帳成功（Matched）、系統狀態最佳、已通報且合規的正常路徑。
Crimson Red (緋紅, #ef4444)：代表 Class I 嚴重召回事件、到期滅菌警報（Critical Expiry）、或未通報的流向黑洞。
字體與排版：
Display Font：選用 Inter 與 Space Grotesk。字距微調，字重對比鮮明，展現現代、理性的科技美學。
Mono Space：選用 JetBrains Mono 或 Fira Code 用於展示 UDI 條碼、SQL 語法、時間戳、系統日誌 (Log) 以及 JSON Schema，強調數據的嚴謹性。
3.2 佈局結構與交互流動 (Layout Dynamics)
固定工作台佈局：寬度為 1024px，高度為 768px，採用完美比例。頂部為全功能 Navigation 標頭，中央為三欄式設計：
左側 Sidebar：AI Live Log 串流日誌。隨時打印 Gemini 的思考鏈路、SQL 執行日誌及系統事件。
中央 Main Area：Wow Dashboard 六大圖表與主動對帳工作區。
右側 Sidebar：AI 智慧特徵抽取與三大全新驚豔 AI 功能面板。
微觀動畫效果 (Micro-Interactions)：
脈衝呼吸燈 (Glow Pulse)：高風險醫材或 Class I 召回品項的外框會帶有緩慢呼吸的琥珀金/緋紅外發光效果（利用 box-shadow 與 motion 關鍵影格）。
粒子流動通道 (Flow Animation)：在拓撲網絡圖（Chart 2）中，高風險流向線條上會有發光粒子沿著導向箭頭快速移動，直觀呈現風險擴散的方向。
視窗淡入淡出：切換主題、語言或篩選條件時，所有卡片均伴隨 150ms 的 Motion 彈性縮放與淡入。
4. 三大演進功能模組技術規格
Aura-7 進化至 4.0.0-Enterprise 版本，其核心功能經過全面重構，主要分為三大相輔相成的技術模組：
3.1 異質醫材召回數據標準化、多模型 SQL 檢索與千字 Markdown 深度摘要模組
本模組提供一站式、高度自動化的醫材召回數據生命週期管理。使用者可任意上傳非標準格式的召回資料，由 AI 核心進行標準化清洗，並轉換為關聯型資料庫進行精準的自然語言檢索。
code
Code
+------------------+      +-------------------------+      +------------------------+
| 非標準 JSON 數據  | ---> |   Gemini Standardizer   | ---> | 統一標準化 JSON 資料結構 |
+------------------+      | (模型動態切換路由機制)   |      +------------------------+
                                                                        |
+------------------+      +-------------------------+                   | Import
| 自然語言查詢關鍵字| ---> |   NL-to-SQL Generator   |                   v
+------------------+      +-------------------------+      +------------------------+
                                         |                 | In-Memory SQL 資料庫   |
                                         +---------------> | (執行標準化安全 SQL)    |
                                           SQL Command     +------------------------+
                                                                        |
                                                                        v
+-----------------------------------------------------------------------------------+
|                              終端互動式展示與分析層                                 |
| 1. SQL 語法手動修改工作區                                                          |
| 2. 應建立與保存來源及流向資料之醫療器材 (TFDA 核心品項) -> 特效高亮 (高鮮明度脈衝外框)    |
| 3. Gemini 智能摘要生成器 -> 輸出 1000 - 2000 字合規分析報告 (Markdown 格式)         |
+-----------------------------------------------------------------------------------+
A. 異質數據導入、解析與生命週期控制
操作介面設計：提供多功能檔案拖曳上傳區 (Drag-and-Drop Zone) 與即時文字粘貼區 (Textarea Clipboard)。支援對單個或批量 JSON 檔案進行實時解析。
資料操作功能：介面完整整合「下載原始檔」、「上傳新配置」、「在線網格修改 (Inline Cell Editing)」功能。任何在介面上的變更皆具備雙向資料綁定 (Two-way Data Binding)，同步更新記憶體中的狀態機 (State Machine)。
AI 資料標準化引擎 (Data Standardization Engine)：
若使用者上傳之 JSON 資料不符合系統內置的標準 Schema（定義見下文），系統會自動觸發標準化流程。
模型路由機制：系統預設調用 gemini-3.1-flash-lite。使用者可透過 UI 下拉選單動態切換為 gemini-2.5-pro 或 gemini-1.5-pro。
提示詞工程 (Prompt Engineering)：AI 接收非標準 JSON 後，將執行精準的語義對齊與缺失欄位推論（例如：將 trade_name 映射至 device_name，將 recall_level 轉換為對應的 tfda_classification 邏輯）。
標準化醫材召回資料 Schema 定義 (JSON Schema Standard v4)
code
JSON
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "title": { "type": "string", "description": "召回事件標題或公告名稱" },
    "recall_date": { "type": "string", "format": "date", "description": "國際或國內宣告召回之日期 (YYYY-MM-DD)" },
    "device_name": { "type": "string", "description": "醫療器材英文/中文商業名稱或型號" },
    "tfda_classification": { 
      "type": "string", 
      "enum": ["應建立與保存來源及流向資料之醫療器材", "第一等級", "第二等級", "第三等級", "非屬上述列管類別"],
      "description": "台灣 TFDA 醫療器材分類分級狀態" 
    },
    "fda_regulation": { "type": "string", "description": "美國 FDA 聯邦法規編號 (例如 21 CFR 870.3610)" },
    "fda_product_code": { "type": "string", "maxLength": 3, "description": "美國 FDA 三字碼產品代碼 (e.g., DTA, LWS)" },
    "reason_for_recall": { "type": "string", "description": "導致召回的詳細技術、安全性或品質瑕疵原因" },
    "udi": { "type": "string", "description": "唯一醫療器材識別碼 (Device Identifier + Production Identifier)" },
    "lot_no_sn": { "type": "string", "description": "受影響的特定批號 (Lot Number) 或序號 (Serial Number)" }
  },
  "required": ["title", "recall_date", "device_name", "tfda_classification", "reason_for_recall", "udi"]
}
B. 自然語言轉 SQL 檢索與安全執行機制
自然語言語義理解：使用者可在搜尋列輸入如：「幫我找出 2025 年後，因為軟體異常被召回的所有第三等級與應保存來源流向的高風險心臟導管」。
SQL 生成與手動修改工作區：系統調用選定之 Gemini模型，將上述自然語言翻譯為標準符合 ANSI SQL 規範之查詢指令。系統不直接黑箱執行，而是彈出一個 「AI SQL 語法編譯與覆核工作區」，允許具備資安或資料庫背景的合規工程師在執行前直接手動修改 SQL 語法。
code
SQL
-- AI 自動生成的範例查詢指令
SELECT * FROM medical_device_recalls 
WHERE recall_date >= '2025-01-01' 
  AND (tfda_classification = '應建立與保存來源及流向資料之醫療器材' OR tfda_classification = '第三等級')
  AND (reason_for_recall LIKE '%software%' OR reason_for_recall LIKE '%韌體%' OR reason_for_recall LIKE '%bug%')
  AND device_name LIKE '%catheter%';
資安防禦技術：為防止惡意使用者透過自然語言進行「提示詞注入 (Prompt Injection)」進而生成破壞性 SQL（例如 DROP TABLE、DELETE FROM），系統的 SQL 執行引擎限制為唯讀權限 (Read-Only Context)，且在執行前透過正則表達式與 AST (抽象語法樹) 解析器強制攔截任何包含非 SELECT 的非授權指令。
C. TFDA 法規感知的核心品項高亮機制
法規觸發邏輯：當資料庫執行的搜尋結果返回並在前端 Grid 渲染時，系統的狀態追蹤引擎會檢驗每一條紀錄的 tfda_classification 欄位。
UI 特效高亮設計：若該記錄精準匹配字串 「應建立與保存來源及流向資料之醫療器材」，系統將透過 Tailwind CSS v4 與 Motion 觸發特殊樣式：該表格行 (Table Row) 背景更換為高飽和度的警示琥珀金變調色 (bg-amber-500/10，在暗黑模式下為 bg-amber-950/40)，邊框加上 border-amber-500，最左側附加一個具備持續發光脈衝動畫 (Pulse Loop Animation) 的紅色法規標籤，並帶有浮動工具提示 (Tooltip) 顯示：「此品項屬於《醫療器材管理法》法規強制列管來源流向之高風險醫材，必須於 24 小時內完成流向稽核。」
D. 1000 - 2000 字 Markdown 綜合性合規分析報告自動生成器
執行流程：當檢索結果產出後，系統自動將當前搜尋結果之全量數據子集、用戶的檢索意圖、當前的法規上下文打包，異步發送至用戶選定的 Gemini 模型（建議使用 gemini-1.5-pro 或 gemini-2.5-pro 以獲得最佳深度推理品質）。
報告結構與字數規格：AI 被嚴格限制輸出 1000 至 2000 字、具備完美工業級 Markdown 語法層次的「召回事件綜合性合規與風險評估報告」。報告必須包含以下固定結構：
## 1. 執行摘要 (Executive Summary)：當前檢索事件的宏觀統計、受災規模評估。
## 2. 核心技術風險源分析 (Technical Risk Root Cause Analysis)：深度拆解召回原因（如材料疲勞、軟體演算法崩潰、無菌包裝破損等）。
## 3. TFDA 法規遵循度與潛在法律責任 (Regulatory Compliance & Legal Liability)：針對高亮列管品項，評估未在法定期限內完成通報的罰則風險（引用醫療器材管理法相關條文）。
## 4. 供應鏈隔離與預防性糾正措施 (CAPA 建議)：提供具體可執行的隔離引導、下架與臨床通知步驟。
3.2 跨域多源數據融合、Wow HTML 六大圖表視覺化與動態導出模組
本模組升級為企業級多源大數據融合中心，可同時吞吐並關聯五種完全不同的醫療器材生命週期核心資料集。
A. 五大異質資料集融合與標準化 Schema 設計
系統支援上傳、粘貼 CSV 及 JSON 格式。上傳後，若格式不符，自動經由選定的 Gemini 模型執行 Schema 轉譯與補全。
TUDID 資料集 (Taiwan Unique Medical Device Identification Database)：核心主檔。包含 UDI-DI、許可證字號、全球品類代碼、製造商資訊。
醫療器材許可證資料集 (Medical Device License Dataset)：包含 許可證字號、中文品名、英文品名、有效日期、通關簽審狀態、類別。
醫療器材召回資料集 (Medical Device Recall Dataset)：即 3.1 所定義之標準化召回事件檔。
醫療器材分銷流向資料集 (Medical Device Distribution Dataset)：包含 出庫單號、UDI-PI（批號/序號）、發貨方代碼、接收方（醫療機構）名稱、出庫時間、物流追蹤碼。
醫療器材採購資料集 (Medical Device Purchase Dataset)：包含 採購訂單號、採購品項 UDI、單價、採購數量、驗收狀態、入庫庫位。
B. 搜尋關鍵字與大數據多表聯查 (Advanced Multi-Table SQL JOIN)
當使用者輸入複雜查詢（例如：「全面盤點目前在各分院中，受到本次 FDA 召回批號影響的庫存數量、當初採購的總金額，以及受影響的醫院名單」），AI 會自動產生如下的高級 SQL 命令並在工作區展示：
code
SQL
SELECT 
    dist.receiver_name AS 醫療機構名稱,
    lic.zh_device_name AS 中文品名,
    recall.udi AS 唯一識別碼,
    recall.lot_no_sn AS 受影響批號_序號,
    purch.purchase_qty AS 採購數量,
    (purch.unit_price * purch.purchase_qty) AS 採購總金額,
    recall.reason_for_recall AS 召回原因
FROM medical_device_recalls recall
INNER JOIN tudid_master tud ON recall.udi = tud.udi_di
INNER JOIN device_licenses lic ON tud.license_no = lic.license_no
INNER JOIN device_distribution dist ON recall.lot_no_sn = dist.lot_no_sn
INNER JOIN device_purchase purch ON dist.purchase_order_id = purch.order_id
WHERE recall.tfda_classification = '應建立與保存來源及流向資料之醫療器材';
C. 「Wow HTML」極致數據視覺化引擎：六大核心圖表規格
檢索結果產出後，系統將在獨立的高級畫布面板中動態渲染六個極具視覺衝擊力、具備高度互動性與動態粒子濾鏡的 Wow Charts：
圖表編號	圖表名稱	核心底層技術	視覺與互動特性 (Wow Features)	業務合規價值
Chart 1	GIS 地理空間流向分佈圖 (Geospatial Distribution Map)	WGS-84 Leaflet / Mapbox GL 混合 SVG 繪製	台灣地圖上動態標註各醫療機構。受災嚴重的院所節點會呈現暗紅色發光光環（發光半徑與受影響醫材數量成正比）。	直觀標示召回醫材在全台地理空間的擴散嚴重程度。
Chart 2	供應鏈物流拓撲網絡圖 (Supply Chain Network Graph)	d3-force (力導向拓撲網絡圖)	核心節點為製造商，分支到物流中心，再擴散至各家醫院。召回醫材流向之線條呈現高亮螢光黃色的**「粒子流動動畫 (Particle Flow Animation)」**，流動速度代表分銷頻次。	追蹤高風險醫材從源頭到終端的全鏈路拓撲結構，揪出中介高危節點。
Chart 3	召回類別與風險暴露桑基圖 (Sankey Diagram)	SVG / D3 Sankey Layout	左側為不同的召回原因，中間為醫材品類，右側為受災醫院。流動條寬度代表受影響的總金額 or 數量，懸停時流動條會產生漸變與數值提示。	視覺化呈現風險源頭如何流向不同的終端，展示風險傳導機制。
Chart 4	合規時序變遷與違規預警趨勢圖 (Temporal Timeline Horizon)	Recharts / Canvas 雙軸圖	X 軸為時間軸，Y 軸左側為召回事件密度，右側為未通報違規天數。具備漸變區域陰影（Gradient Area）與臨界值警告紅線。	監控全公司或全區域合規健康度隨時間的演變趨勢。
Chart 5	醫材生命週期損耗與庫存漏斗圖 (Funnel Risk Analytics)	SVG CSS Clip-Path	呈現從「許可證核發 -> 採購進庫 -> 轉運分銷 -> 醫院驗收 -> 臨床消耗」的各階段留存率，危險流失階段（如未經驗收即進入臨床）會以紅色鋸齒狀切口特效顯示。	精準抓出合規數據鏈路在線下的斷裂點與損耗點。
Chart 6	法規分級風險暴露矩陣雷達圖 (Regulatory Radar Chart)	Recharts Radar Engine	呈現六個維度的安全指標：法規覆蓋率、批號可追蹤度、召回響應速度、供應鏈集中度、過期風險係數、來源明晰度。覆蓋區域採半透明極光色填充。	供高階主管一秒評估當前企業法規合規架構的整體防禦力與薄弱環節。
動態過濾器 (Interactive Filter Shell)：所有圖表與底層 Grid 數據共享同一個響應式狀態中心。使用者可利用右側懸浮的 Filter Panel（包含 滑桿式日期篩選、法規分級複選框、採購金額區間滑塊）進行實時過濾，所有六大圖表與 SQL 結果集將在 16ms 內同步完成 Motion 淡入淡出重新渲染。
D. Wow HTML 多格式一鍵打包導出引擎
平台建構了強大的邊緣端文件編譯器，允許使用者將當前包含六大圖表、SQL 數據、Markdown 報告的整個工作區打包導出為以下格式：
JSON：完整匯出洗淨後的關聯化結構數據陣列，符合標準 REST 傳輸規範。
PDF：調用前端 window.print() 與預設的 CSS 分頁媒體查詢 (@media print)，自動將六大圖表與 Markdown 報告重新排列為適合 A4 紙張、帶有企業浮水印與頁碼的高級合規報告。
MD (Markdown)：純文字格式導出，完美保留完整的 Markdown 標題、表格與 AI 產出的風險評估。
HTML (Wow HTML 獨立運行檔)：此為本平台的殺手級功能。系統會將當前所有的數據、視覺化圖表的輕量級渲染引擎、Tailwind 樣式庫以及當前的全量資料集，封裝並編譯成單個獨立的 .html 檔案。使用者下載後，在完全離線、無網路的環境下雙擊該檔案，依然可以在任何瀏覽器中流暢操作上述六大圖表、執行動態過濾與數據檢視。
3.3 醫療器材召回數據生成模組與 3 大全新「驚豔」AI 功能設計
本模組旨在解決「數據源頭碎片化」的問題，賦予系統將非結構化的各國官方原始公告文檔，轉化為生產級結構化合規數據的能力。
A. 原始文檔結構化提取與生成工作流
文檔吞吐能力：使用者可直接上傳或粘貼美國 FDA 或台灣 TFDA 的原始召回公告，支援 TXT, MD, PDF, JSON 等格式。
AI 智能特徵提取：系統固定調用 gemini-3.1-flash-lite 執行高速解析（或用戶自選其他高級模型），精準從萬字冗長的法律與技術公告中，抽取出 3.1 節所定義的標準 JSON Schema 欄位。
自適應標準化管道 (Pipeline)：若提取出的資料存在缺失值，AI 將啟動上下文推理（例如：根據 FDA Product Code 自動反查對應的常規醫療器材品名，或根據公告內容推估其在台灣 TFDA 規範下是否屬於「應建立與保存來源及流向資料之醫療器材」）。使用者可在介面中下載、再次上傳或直接在 Grid 中進行修改與人工校核。
B. 3 大全新「驚豔」AI 未來感擴展功能設計
1. AI 驅動的預測性風險熱圖與擴散動態模擬器 (Predictive Risk & Contagion Simulator)
技術實現：本功能超越傳統的靜態數據展示。當用戶導入一筆全新的 FDA 召回事件時，後端 AI 代理（調用 gemini-1.5-pro 或更高階模型）會立刻主動讀取企業內部當前的「分銷流向資料集」與「採購資料集」。
WOW 點與視覺特效：AI 會在 Chart 1 (GIS 地理空間流向分佈圖) 上啟動擴散粒子動畫。它會根據過去六個月該款醫材在各醫院間的調撥頻率與消耗速率，模擬預測未來 14 到 45 天內，這批召回醫材可能隨患者轉院、跨院物流而擴散至其他未登記院所的「潛在風險熱區」。在地圖上，這些預測危險區域會呈現橙色發光光環與動態漣漪效果 (Ripple Effect)。這能讓合規主管在危機發生前，提前下達預防性封存指令。
2. 自主多源法規對帳、語義去重與糾錯代理人 (Autonomous Semantic Reconciliation Agent)
技術實現：在實務操作中，人工輸入的 UDI、批號或序號經常會因為肉眼誤讀（例如將條碼中的字母 O 誤打為數字 0，將 B 誤打為 8）或者不同資料庫間的命名不一致（例如「台大醫院」與「國立臺灣大學醫學院附設醫院」），導致 SQL 精準查詢失效。
WOW 點與互動設計：本功能是一個常駐的 AI Agent。當異質資料導入時，它會自動進行多源語義對帳。如果發現分銷單與採購單存在 1 碼的序號差異，且物流時間完全吻合，系統不會直接報錯，而是會在介面右下角彈出一個極具質感的 AI 助手視窗：
💡 Aura-7 自主對帳提示：「我發現分銷資料集中的序號 SN-94830O7 與採購資料集中的 SN-9483007 存在 98.6% 的語義重合度。根據過去本院掃描槍的誤差模式，此處極可能為 O/0 誤判。我已自動將其關聯。點擊 [確認修正] 將自動更新底層關聯資料庫並同步更新六大 Wow 圖表。」
3. 語音互動式合規協同代理人 (Voice-Activated Compliance Co-Pilot via Web Audio)
技術實現：本功能專為雙手正在執行盤點、無菌操作或手套不便觸碰螢幕的倉儲與手術室管理員設計。整合 HTML5 Web Audio API 與 Gemini 的語音流處理技術。
WOW 點與互動設計：使用者點擊介面上的微型麥克風圖示（或使用喚醒詞 "Aura"），直接說出法規查詢意圖：「Aura，幫我高亮所有北部地區屬於來源流向管制的嚴重召回醫材，並切換到供應鏈拓撲網絡圖。」系統的語音代理會即時完成語音轉文字 (STT)、意圖解析、動態過濾器參數修改、觸發 Chart 2 全螢幕最大化切換，並以清晰流暢的語音合成 (TTS) 回報：
🎙️ Aura-7 語音回報：「已為您找到 3 筆符合《醫療器材管理法》法規強制列管之核心召回品項。目前已切換至供應鏈拓撲網絡圖，高危流向粒子通道已為您用黃色螢光標註，請查看中央顯現的物流斷裂點。」
5. 系統潛在 Bugs 預防與極致防禦設計
為了保證 Aura-7 在企業級複雜高負載環境下的絕對穩定，我們針對以下關鍵技術環節，制定了極為嚴苛的防禦性設計與修復策略：
5.1 SQL 注入漏洞與 AST 沙箱隔離 (Read-Only SQL Enforcement)
潛在 Bug：惡意用戶可能通過 NL-to-SQL 的自然語言輸入列，蓄意誘導 Gemini 模型生成諸如 DROP TABLE、DELETE FROM、或包含 OR 1=1 的橫向越權攻擊 SQL 命令。
防禦策略：
前端 SQL 覆核工作區：AI 生成的 SQL 指令必須在前端 UI 的唯讀編輯器中展示，並提供一個「覆核確認」的二次攔截。
正則強制攔截機制 (Regex Interceptor)：系統中介層在將 SQL 傳入 SQLite 之前，會通過嚴格的 Regex 掃描。凡是包含 DROP、DELETE、UPDATE、INSERT、ALTER、CREATE、TRUNCATE、GRANT 等 DDL/DML 變更關鍵字的，一律拋出 500 Security Violation。
AST 抽象語法樹校驗：使用輕量級的 SQL AST 解析器，強制校驗查詢根節點必須且只能是 SelectStatement，從根本上杜絕多重分號指令拼裝的 SQL 注入攻擊。
5.2 數據流式加載與 OOM 崩潰防範 (Out-of-Memory Prevention)
潛在 Bug：當用戶拖入包含數十萬條出庫記錄的巨大分銷 JSON 檔案（大於 100MB）時，原生的 JSON.parse 會阻塞 JavaScript 單線程，引發頁面卡死，甚至導致 Node.js 服務器因 OOM（記憶體溢出）而重啟。
防禦策略：
邊緣端 Stream 解析：在後端引入 fs.createReadStream 結合 JSONStream 或 csv-parser，進行逐行流式掃描與數據塊寫入（Chunked Injection）。
前端分頁與虛擬列表 (Virtual Scrolling)：在渲染 Data Grid 時，不直接渲染上萬個 DOM 節點，而是使用虛擬滾動技術，僅在視口渲染 30 條數據，將 DOM 的內存佔用降至恆定常數。
5.3 異質對帳語義消歧義 (Entity Disambiguation Boundary)
潛在 Bug：同一家醫院在採購單中被登載為「北榮」，在分銷單中卻是「國立臺灣大學醫學院附設醫院」，這會引發對帳關係鏈斷裂。
防禦策略：
語義相似度比對門檻：系統建立一個標準對帳向量矩陣（Standard Dictionary），將所有非標準名稱輸入 Gemini，利用 Embeddings 映射到標準字典中的實體 ID（例如：北榮 ──> HOSP_004）。
置信度門檻 (Confidence Boundary)：當語義相似度高於 95% 時，系統執行自動靜默關聯，並在 Live Log 打印對帳日誌；介於 80% 到 95% 之間時，觸發「自主對帳 Agent 提示彈窗」，供官員一鍵人工確認；低於 80% 時判定為無關聯。
6. 20 個全面性後續問題與解決架構
為落實 Aura-7 系統的治理以及應對未來的技術升級，系統維護與 TFDA 稽核總部提出以下 20 個核心追蹤與發展追問，並給出高層次的技術設計思路：
【第一部分：前端渲染、效期與離線體驗 (Q1-Q5)】
Q1: 若全台灣的合作醫療機構（包含基層診所、藥局）高達上萬家，Chart 1 (GIS 地理地圖) 如何避免在 Leaflet / SVG 混合渲染模式下出現畫面調幀或卡頓？
技術解答：當節點規模突破 10,000+ 時，原生 SVG 將會使 DOM 樹過度龐大。Aura-7 設計了雙層降級渲染技術：
Canvas 叢集聚合 (Canvas Marker Clustering)：當地圖處於高縮放層級（Zoom Level < 10）時，地圖自動將相近的醫療機構節點聚合為一個 Cluster 標記，並使用 HTML5 Canvas 的 ctx.arc() 進行批次批量像素繪製，避免創建任何 DOM 節點。
WebGL 分層優化 (WebGL Overlay)：針對密集粒子流（如全台在途配送軌跡線），引入 PixiJS 或 Deck.gl WebGL 圖層，將圖形頂點數據直接提交給 GPU 進行並行渲染，在 10 萬個流動點下依然能保持 60 FPS 的流暢交互。
Q2: 3.2 節中提到的離線執行 Wow HTML 導出文件，如何在完全無網絡的隔離環境下實現部分 AI 標準化與對帳能力？
技術解答：在離線環境下，系統無法與雲端 Gemini API 通訊。
Web Assembly (Wasm) 本地引擎：導出的 Wow HTML 文件將內嵌一個輕量級的 JavaScript 規則對齊引擎，該引擎由 Rust 編譯而來，專門負責基本欄位格式校驗與標準化。
本地字典與 Aho-Corasick 算法：利用內嵌的微型醫療機構代碼對照表，在瀏覽器本地線程（Web Worker）中使用 AC 自動機算法進行極速的正則模糊匹配，替代部分的 AI 語義模糊對帳功能。
Q3: 針對 6.1 吋的手機或平板，Wow HTML 六大複雜圖表（特別是 D3 力導向拓撲圖和桑基圖）如何進行響應式設計 (Responsive Degradation)？
技術解答：對於極小屏幕，複雜的多維圖表會因為空間緊湊而失去可讀性。
斷點布局重構 (Breakpoint Grid Layout)：在 @media (max-width: 768px) 斷點下，系統會將三欄布局重構為單欄垂直佈局。
視覺組件降級策略 (Graceful Degradation)：D3 力導向網絡拓撲圖會降級為「卡片式核心節點卡片流」，桑基圖則降級為「分段式比例環形圖 (Donut Charts)」。
局部視窗平移與縮放 (Viewport Panning & Zooming)：保留 GIS 地圖，但強制開啟 touch-action: none 的雙指物理縮放（Pinch-to-zoom）與平移（Panning）功能，並加設「全螢幕最大化」按鈕。
Q4: 當導出長達 2000 字且包含六大 Wow 圖表的綜合合規報告為 PDF 時，如何解決圖表或表格在 A4 紙張邊界處被從中切斷的問題？
技術解答：普通的網頁打印容易在圖表中間產生醜陋的分頁切斷。
CSS Paged Media 規則：在 @media print 樣式表中，對六大圖表的外層卡片和 AI 報告的二級標題強制套用 page-break-inside: avoid; (在新版瀏覽器中為 break-inside: avoid;)。
動態高度檢測與 CSS Grid 強制分頁：導出引擎在打印前會調用 JavaScript 檢測各組件的實時高度，對於高度超出單張 A4 剩餘空間的組件，動態在其前方注入一個帶有 break-after: page; 的空白分頁標記，確保每一頁 PDF 均擁有優雅的頁邊距與視覺完整性。
Q5: 稽核現場往往位於屏蔽極強的地下庫房或信號不良的無菌室，Aura-7 如何實現離線運作快取 (PWA / Offline Sync) 機制？
技術解答：
Service Worker 快取代理：利用 Workbox 庫，將系統的所有靜態資源（CSS, JS, 潘通色樣式表）進行 Cache-First 本地預緩存。
IndexedDB 暫存隊列：當檢測到 navigator.onLine === false 時，官員對站點的修改、新增操作會被包裝成一個「Sync Action Transaction」寫入 IndexedDB 暫存隊列。
Background Sync 同步器：一旦信號恢復（online 事件觸發），背景同步器會自動將隊列中的事務按時間戳順序發送至後端進行合併對帳，並同步刷新 Live Log。
【第二部分：數據安全、SQL 注入與異常獵手 (Q6-Q10)】
Q6: 目前的唯讀 SQL 執行 Context 以及正則攔截防護，如何防範更為隱蔽的 Prompt Injection 提示詞注入攻擊？
技術解答：僅靠正則表達式容易被諸如 Hex 編碼、特殊 Unicode 字符、或嵌套 SQL 注釋等變形手法繞過。
內核級權限隔離：系統底層與 SQLite/DuckDB 的數據庫連接（Database Connection）在權限級別上被強制配置為 ReadOnly。即使注入指令成功突破防線，數據庫驅動也會在執行 INSERT/UPDATE/DELETE 時直接拋出操作拒絕異常。
抽象語法樹 AST 安全校驗：使用極速的 SQL AST 解析器在語法層面將生成的 SQL 解析為 Node 節點樹。校驗代碼遍歷所有 Node，若發現 DropStatement、UpdateStatement 或 UnionStatement 中包含敏感系統表（如 sqlite_master），立刻在內存中將其銷毀，並向 Live Log 發送高危資安警告。
Q7: 「神經網絡帳籍漏洞獵手 (Anomaly Hunter)」在計算綜合合規評分時，其權重矩陣與扣分機制如何設計以對齊 TFDA 法規？
技術解答：系統建立了一套基於法規嚴重性的動態扣分權重矩陣：
Ghost Stock (幽靈帳籍)：權重 -40分。此情況涉嫌走私或嚴重漏報，屬於 Class III 刑事邊界。
Unreported Discrepancy (出庫未登)：權重 -25分。屬於流向黑洞，有丟失風險。
Critical Lifecycle (滅菌到期小於 14 天)：權重 -15分。屬於醫療品質過期風險。
Reporting Lag (通報延遲大於 72 小時)：每多一天累計扣 -2分。
評分輸出：最終合規評分（S-Grade Compliance Score）採用 
。低於 60 分時，系統自動將頂部 Navigation 的 A7 標頭閃爍為紅色，提示官員必須在 24 小時內啟動限期改善調查。
Q8: 如何徹底防止上傳的 CSV/JSON 數據中包含惡意 Excel 公式，進而觸發 CSV Injection（Excel 巨集指令注入）攻擊？
技術解答：當稽核官員將 AURA-7 導出的 CSV 檔案在 Microsoft Excel 中打開時，若單元格內容以 =, +, -, @ 開頭，Excel 會將其作為公式執行，這常被黑客用來運行系統命令。
防禦策略：
首字元強制轉義：在 CSV 導出引擎（Export Engine）中，對所有寫入單元格的字串進行前置檢查。若首字元符合 ^[=\+\-\@\s] 正則表達式，強制在字串最前端包裹雙引號，並在最前方加一個單引號 '（例如：將 =CMD('calc') 轉義為 '"=CMD(\'calc\')"'），使 Excel 強制將其識別為純文字。
編碼格式限制：輸出文件統一採用 UTF-8 BOM（含字節順序標記），限制公式語意在非標準編碼下的隱形轉化。
Q9: 當頻繁執行大數據多表聯查與圖表重繪時，如何確保 Canvas 畫布、D3 事件監聽器與 Web Audio 上下文在 React 組件 Unmount 時被 100% 釋放，防止瀏覽器內存洩漏 (Memory Leak)？
技術解答：頻繁的銷毀與創建極易在內存中堆積垃圾，導致瀏覽器頁面崩潰。
D3 事件與節點清理：在 React 的 useEffect 清理函數（Cleanup function）中，明確執行 d3.select('#topology-graph').selectAll('*').remove()，並將拓撲力導向模擬器關閉：simulation.stop()，將所有節點引用置為 null。
Canvas 寬高歸零：對 Canvas 畫布，手動將其 width 與 height 設為 0，這會強迫瀏覽器底層的 GPU 顯存緩衝區立即釋放。
AudioContext 關閉：在 Web Audio API 卸載時，強制調用 audioContext.close() 並解除音頻節點（AudioNode）的 disconnect() 連接鏈。
Q10: 為了保障患者個人隱私，Aura-7 在將賬籍數據發送至外部 Google Gemini API 之前，施加了何種程度的去識別化與脫敏管道？
技術解答：根據醫療法規（HIPAA/GDPR/國內醫療法），患者隱私數據絕對禁止外流。
PII 數據過濾管道 (Sanitization Redaction Pipeline)：在將任何文本 payload 發送給 Gemini SDK 之前，後端 Express 會啟動正則模糊掃描器，自動識別並清除所有符合身分證字號（^[A-Z][1-2]\d{8}$）、手機號碼、病歷號（MRN）、以及中文姓名的敏感字詞。
令牌化替換 (Tokenization)：將患者個人資料自動替換為加密 Hash 代碼（例如：將「林○○」替換為 [REDACTED_PATIENT_SHA256_A3FF]）。Gemini 僅接收 UDI、批號、數量和地理代碼，確保 AI 在執行合規推理時絕不接觸任何實體患者隱私資訊。
【第三部分：高風險 UDI 條碼與法規更新 (Q11-Q15)】
Q11: 國際 GS1 標準下的 UDI 格式非常複雜，包含 DI 與 PI，Aura-7 條碼編譯器如何應對歐盟 (MDR) 與美國 FDA 未來新型超長變量 PI 條碼格式的擴展？
技術解答：
語義化解析樹 (AST-based UDI Parser)：條碼編譯器不使用硬編碼的正則，而是基於 GS1 全球標準規範，使用 ABNF 語法解析器。它會將 UDI 解析為一個語義化的 JSON 對象：
code
JSON
{
  "di": "00850014110147",
  "pi": {
    "expiration_date": "2029-06-10",
    "lot_number": "LOT135962",
    "serial_number": "SN94830O7"
  }
}
動態應用識別碼 (Application Identifiers, AI) 配置表：建立可配置的 AI 對照字典（如 (01) 代表 DI，(10) 代表批號，(17) 代表到期日）。當國際組織新增或擴充 AI 代碼（例如新增三維條碼定位代碼）時，僅需在數據庫中更新配置，條碼編譯器即可即時支持新型超長條碼的轉譯與生成。
Q12: TFDA 規定的「應建立與保存來源及流向資料之醫療器材」品項清單會隨時間滾動修正。當法規品項增加或減少時，平台如何實現「法規動態庫更新」，而無需重新編譯與發布系統代碼？
技術解答：
雲端動態法規映射表 (Dynamic Regulatory Mapping)：系統不在代碼中寫死品項清單，而是建立一張名為 regulatory_catalog 的底層數據表。
定時滾動拉取機制 (Cron Synchronization)：系統後端定時（如每週一凌晨）異步向 TFDA 開放數據 API 發起請求，拉取最新公告的列管器材分類代碼（Classification Codes）與字彙特徵。一旦拉取成功，寫入本地 DuckDB，前端高亮邏輯會依據這張動態表進行實時判定，達成「無感式、免維護」的動態法規庫更新。
Q13: 若平台需要部署到個別醫院的私有雲環境 (On-Premise Kubernetes)，Google Gemini API Key 的存放與定期輪轉 (Rotation) 該如何與醫院內部的安全體系整合？
技術解答：
Kubernetes External Secrets (KES) / Vault 整合：在 K8s 中部署時，嚴禁將 API Key 寫入環境變量 .env。我們將配置醫院內部的 HashiCorp Vault 作為安全保管箱。
Sidecar 動態注入：在 Aura-7 POD 中加裝一個 Vault Agent Sidecar。Sidecar 會定期向 Vault 獲取最新的 Gemini API Token，並將其動態寫入共享內存卷（Shared Memory Volume, /dev/shm/secrets）中。
熱加載讀取 (Hot Reloading)：Express 後端使用 chokidar 監聽該路徑的變化，一旦密鑰輪轉（Rotate）成功，系統在內存中瞬間無縫覆蓋 API Key，無需重啟任何 Container，確保系統 365 天不間斷運作。
Q14: 當預設的 gemini-3.1-flash-lite 遭遇服務端限流 (Rate Limit Exceeded) 或臨時服務中斷時，後端的 AI 路由引擎如何實現自動熔斷與多模型降級備份機制？
技術解答：
多路複用與自動重試 (Exponential Backoff)：使用 GoogleGenAI SDK 的內置重試機制，在遇到 429 (Rate Limit) 錯誤時，自動進行指數退避重試（3次，延遲分別為 1s, 2s, 4s）。
斷路器模式 (Circuit Breaker Pattern)：引入 Opossum 熔斷器。若 10 秒內 API 請求失敗率大於 50%，熔斷器自動切換為「開啟 (Open)」狀態。
多模型動態降級路由：當預設的 gemini-3.1-flash-lite 熔斷時，路由引擎自動將請求重定向至備用模型，降級路徑設計為：gemini-3.1-flash-lite ──> gemini-2.5-flash ──> gemini-1.5-flash。若全部雲端模型皆不可用，系統將降級為「本地內置對帳規則引擎」，保障系統最基本的對帳操作，並在 Live Log 標註 [FALLBACK: LOCAL ENGINE ACTIVE]。
Q15: 若本平台升級為多租戶 (Multi-Tenant) 雲端 SaaS 版本，如何確保 A 醫材商絕對無法透過經過設計的 SQL 語法跨界查詢到 B 醫材商的商業機密採購與分銷數據？
技術解答：
邏輯隔離與租戶過濾上下文 (Row-Level Security, RLS)：在多租戶架構下，系統強制在所有關鍵業務表（分銷、採購、TUDID、站點表）中加裝一個 tenant_id 欄位。
連接池注入過濾 (SQL Query Rewriter Middleware)：後端 Express 在調用 SQL 執行引擎前，會強制攔截所有 SQL 指令，解析 AST 語法樹，並在所有的 WHERE 條件中強制且無法移除地 appended 附加 AND tenant_id = ?（綁定當前 Session JWT 中解密出的租戶 ID）。這在底層邏輯上徹底隔絕了 SQL 被惡意改寫進行越權跨租戶查詢的可能性。
【第四部分：空間模擬、語意對帳與語音控制 (Q16-Q20)】
Q16: 在地理空間流向圖 (Chart 1) 中，若台灣因自然災害（如大型地震、強烈颱風等）發生大面積交通中斷，Aura-7 如何動態計算全島在途召回醫材的流動風險評級？
技術解答：
即時災害 API 接入 (Dynamic Hazard Integration)：後端定時向台灣交通部公路局、中央氣象署的動態路網 API 發起請求，拉取土石流、封路、以及極端天氣的空間坐標與範圍。
空間拓撲網格計算 (Dynamic Dijkstra Re-routing)：將 WGS-84 地圖上的配送路徑抽象為一個帶權的有向圖。一旦檢測到某段省道或高架道路受災，該路段的交通權重係數 
 立即趨於無窮大，系統隨即調用 Dijkstra 算法重新計算物流替代路徑，並將沿途受波及的 DHA 站點在途物資合規風險評級（Reporting Lag Risk）一秒內自動提升至 High，在地圖上引發動態漣漪擴散。
Q17: 在途配送高價值活性醫材常有全程冷鏈監測需求，Aura-7 如何與物聯網 (IoT) 通訊協議（如 NB-IoT / 藍牙 5.0）整合，將實時溫度異常寫入 Active Ledger？
技術解答：
輕量級 MQTT 代理人 (MQTT Client)：後端內嵌一個基於 MQTT 協議的長連接監聽服務，用以接收配送箱中內裝的 IoT 溫度傳感器發射的動態 JSON Payload。
熱數據流處理 (Hot Path Streaming)：數據經由後端解析後，若發現溫度波動超出冷鏈安全區間（如起搏器儲存溫度低於 2°C 或高於 8°C，持續超過 10 分鐘），系統將立即跳過定期對帳週期，直接向 active ledger 發射一筆 Temperature Breach 狀態標籤，並在前端 GIS 地圖中使該在途運輸線路閃爍緋紅色，並在 Live Log 打印突發告警。
Q18: 在 DHA 站點批次上傳中，若用戶上傳的數據存在經緯度緯度顛倒（例如把經度 121 填成緯度，使坐標落在太平洋或非本島區域）時，地圖如何實施自動化地理圍欄 (Geofencing) 糾錯與安全警告？
技術解答：
WGS-84 多邊形地理圍欄校驗 (WGS-84 Polygon Geofencing)：在前端和後端同時配置一個定義全台灣本島及離島領海範圍的多邊形坐標數組。
坐標合法性自動修正算法：當新站點被導入時，系統會調用 Ray-casting 射線法判斷其 GPS 坐標是否落在該多邊形內。若發現坐標落在海中或境外，且經度在 [22.0, 25.5]、緯度在 [120.0, 122.2] 區間內（即經緯度數值完美顛倒），算法會自動調換經緯度數值，將其重新修正回本島正確位置，並在 Live Log 打印：
"WARN: Station GPS coordinates swapped automatically to fit Taiwan geofence."
Q19: 語音互動式合規協同代理人 (Voice Co-Pilot) 如何在嘈雜的醫院倉庫、冷庫、或心導管手術室預備區，實現人聲的高精度識別與 Voice Activity Detection (VAD)？
技術解答：
Web Audio API 低通濾波器與增益補償 (Low-pass Filter & Gain Node)：在前端捕捉麥克風數據流時，利用 BiquadFilterNode 配置一個 lowpass 濾波器（過濾掉 4000Hz 以上的高頻機械雜音），並接駁 DynamicsCompressorNode（動態壓縮器，用以平衡突發環境噪聲），提升人聲段的信噪比。
瀏覽器端輕量 VAD 引擎 (onnxruntime-web)：前端引入輕量級 Silero VAD（基於 ONNX 格式在瀏覽器本地線程執行）。它能精準判斷用戶是否正在說話，僅在人聲開始與結束時切取音頻片段，發送給 Web Speech API 或雲端語音 API 進行文本轉譯，大幅降低無聲狀態下的無效請求。
Q20: AURA-7 在未來發展中，如何與區塊鏈 (Hyperledger Fabric 或 Ethereum Private Chain) 分布式不可篡改帳本整合，確保召回追蹤鏈路的證據不可篡改性與法律溯源力？
技術解答：
交易雜湊與鏈上存證 (Transaction Hashing & On-Chain Anchoring)：當發貨商、物流中心、醫院完成每一次的 UDI 點收與狀態變更（例如：狀態變為 Matched 或 Dispatched），系統將該筆變更記錄的關鍵屬性（批號、出庫單、簽收時間、操作官員 ID）進行 SHA-256 雜湊，生成一個獨一無二的 Compliance Hash。
智能合約異步寫入 (Smart Contract Invocation)：系統後端通過 JSON-RPC 異步調用 Hyperledger Fabric 上的智能合約（Chaincode），將 Compliance Hash、時間戳與原始對帳 ID 作為不可篡改的區塊交易（Block Transaction）寫入分布式帳本。在實地稽核時，官員能一鍵點擊「鏈上驗真 (Verify on Chain)」，核對本地 DuckDB 數據的 hash 是否與鏈上 hash 100% 吻合，徹底消除企業內部改單、作帳或事後偽造物流數據的可能性。
7. 系統實施與稽核標準工作流
當 TFDA 稽核團前往特定醫療器材物流中心或醫學中心現場進行實地考核時，請嚴格按照以下六步流程，操作 Aura-7 系統面板：
第一步：行前系統設置與外觀調配
系統調配：官員在瀏覽器中啟動 Aura-7 稽核工作台。
視覺切換：視現場採光，點擊「Theme Switch」切換至最舒適的亮度。若長時間作業，建議將色彩選擇器切換至 Ultimate Gray 17-5104（極致灰，字元對比清晰），防止眼睛疲勞。
語系確認：確認主介面語言切換至「繁體中文 (Traditional Chinese)」，確保在面臨現場醫療機構主管時，能提供清晰、權威的中文法規提示。
第二步：實地站點核證與 WGS-84 地圖查校
空間地理檢驗：稽核官員點擊「空間地理看板 (Geospatial Dashboard)」分頁。
據點核對：在地圖上檢查受檢物理據點（如 A00013 台大醫院或本地配送中心）是否有登載在 DHA 站點矩陣中。
新據點導入：若對應的新型倉儲點未在名冊中，可在「單點註冊器」中輸入新據點 ID，登載其名稱、GPS WGS-84 特徵與郵遞地址，點擊「立案此監控站」；或利用「CSV/JSON 批次覆蓋區」，拖曳新取得的全台醫療據點經緯度總表，完成閃擊式重置。
軌道驗證：在雷達投影圖中，確認連線軌道（顯示在途調撥的高空模擬航路/陸運線）無顯著偏移。
第三步：高風險账籍交叉檢索與狀態檢視
過濾篩選：在 Active 帳籍表上，設置篩選過濾：輸入特定的許可執照字號（如 衛部醫器輸字第025432號）或特定的型號。
重點對帳：清點受稽對象，重點比對所有標記為：
🔴 出庫未登 (Unreported Discrepancy)：追查為何經銷商已結案、發貨，其進口商 Medtronic 已申報放行，但臨床端並未入帳？追查現場簽收物流單號與紙本。
🟡 幽靈帳籍 (Ghost Stock Entry)：最危險漏洞。醫院有起搏器手術紀錄，但進口商 Medtronic 資料庫卻毫無此序號登記。現場官員必須立即抽查病歷，清點實體防偽標籤。
轉換戰場：針對以上異常行，點擊最右方的「Draft Audit Note」一鍵將該筆特定醫材技術參數提取、並注入至 AI 筆記 Keeper。
第四步：利用智慧 AI 稽核筆記草擬告誡公文
自動載入：系統會流暢地轉移至「AI 稽核筆記 (AI Note Keeper)」工作區，下方文字編輯區已自動載入該異常器材的所有序列號與流向明細。
公文指令下達：官員在最下方的 AI 指引輸入框中，輸入指令：「請針對此 Unreported 序號填寫，以食品藥物管理署名義起草一份違反醫療器材管理法第23條的限期改善警告公文，並明列現場扣押之序號與其滅菌效期，需具備威嚴之行政法用語。」
公文生成：點擊「調用神經引擎執行! (Call Neural Core)」，3 秒內於右側 Markdown 視圖中即可生成一份文字精湛的中華民國食品藥物署官方格式稽核告誡書。
用印發文：點擊「複製 Markdown 稽核公文 (Copy Output Markdown)」，可直接粘貼至 TFDA 內部發文行政系統（公文辦公套件）進行用印。
第五步：批量整合與追蹤條碼實質防偽校對
條碼生成與比對：切換至「數據庫整合 (Dataset Integration)」分頁。如果在現場發現受查驗貨架上有多個外包裝條碼，官員可利用 WOW 功能 三 (UDI Barcode Composer)，在輸入框中設定抽取出的 PI/DI 製造特徵，點擊生成條碼，用於物理外盒的直接肉眼及手持槍掃描比對。
爭端解決：若發貨商與院所互推責任，則立即在 WOW 功能 一 (Dispute Resolutor) 中輸入點收爭端事由，點擊分析，取得 AI 自動化法律追蹤與處置判定。
第六步：一鍵全局掃描與智能合規評分存擋
漏洞掃描：回到「數據庫整合」模組下半部的 WOW 功能 六 (Anomaly Hunter)，點擊「啟動全通路智能掃描 (Scan Supply Ledger Anomalies)」。
存擋存證：全台所有在途追蹤高風險起搏器的運行合規分數及最新的漏洞對應報告將一覽無遺。利用備份導出功能，點擊「安全備份下傳 (.json)」，導出全台據點 WGS-84 配置，隨同稽核終端日誌歸檔於 TFDA 安全伺服器，完成一次完美的實地主動合規追蹤。
8. 總結與未來藍圖
Aura-7 醫材合規追蹤平台 (v4.0.0-Enterprise) 深度融合了先進的 Google Gemini AI 語言神經網絡、WGS-84 地理空間軌道追蹤技術、SQLite/DuckDB 高效能 SQL 引擎，以及為稽核官員量身定製的 Sophisticated Dark 精緻暗黑視覺語意美學。
平台不僅從根本上打破了多源異質數據割裂的監管痛點，更通過六大驚豔 AI 代理引擎（合規爭端調解、預測性地理風險模擬、GS1 UDI 國際條碼編譯、TFDA 法規智慧諮詢、臨床資產效期優化、神經網絡帳籍漏洞獵手），將傳統被動、靜態、高成本的法規稽核轉化為主動式、智能化、毫秒級響應的空間數位孿生監控中心。
展望未來，Aura-7 將朝向 分布式區塊鏈主動存證、全程冷鏈 IoT 感知晶片、以及國家級合規大模型（TFDA Domain-Specific LLM） 深度演進。通過技術的持續沉澱與極致工藝，Aura-7 將繼續守護全台灣數萬名使用高風險醫療器材患者的生命安全。
合規無死角，追蹤零容忍 ── Aura-7 守護健康，智領未來！
技術規格文檔備忘 (Workspace Reference)
本白皮書與技術規格書已成功寫入項目工作區根目錄下的 /SPECIFICATION.md。您可以隨時在代碼編輯器中查看、導出或在後續開發中作為核心需求基準（Core System Requirements Baseline）。
