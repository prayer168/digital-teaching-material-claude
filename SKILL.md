---
name: digital-teaching-material-claude
description: >-
  Build, complete, revise, verify, and deploy accurate interactive digital teaching materials for any subject, grade, or lesson structure. Use when Claude Code must turn an HTML/Vite/CSS/JS scaffold or existing lesson into classroom-ready教材; research factual content; choose and refine instructional visuals, SVG/CSS/JS animations, diagrams, maps, charts, timelines, simulations, quizzes, or interactions; prevent inaccurate, decorative, clipped, or overlapping visuals; add accessible controls and social preview metadata; verify desktop/tablet/mobile behavior; document evidence; version the project; or deploy it to a folder-name or English-title GitHub repository and GitHub Pages.
---

# 數位互動教材開發 Claude Code 版

把已建立的教材骨架或既有網站完成為內容正確、視覺精準、互動有教學目的、可在課堂與多種裝置使用的數位教材。適用自然、數學、社會、語文、藝術、健康生活及跨領域主題。

## 必讀資源

- 每次實際製作或修改教材，都先讀取 [precision-visual-interaction-qa.md](references/precision-visual-interaction-qa.md)，並依其學科精準度、動畫、無障礙、瀏覽器驗證與部署閘門執行。
- 當專案是 kickoff 產生的七頁籤 Vite/HTML/CSS/JS 教材，或需要補齊既有骨架時，再讀取 [post-kickoff-polish.md](references/post-kickoff-polish.md)。
- 部署完成後若使用者要臉書文／FB文／社群貼文／宣傳文，讀取 [facebook-post.md](references/facebook-post.md) 產生中英雙語貼文與複製卡片。

## 核心規則

- 讓每張圖、每段動畫、每個互動都對應明確學習目標；無法說明教學用途的視覺不要加入。
- 對可客觀查證的名稱、外形、公式、數值、年代、地圖、字形、步驟、文化符號與時效資訊進行查核，不只依賴模型記憶。
- 重要概念至少交叉核對兩個可信來源；優先採政府、教育機關、博物館、大學、研究機構、官方文件及專業資料庫。
- 外部圖片只作研究與比對。除非授權明確且教材確實需要，否則不要重製、描摹或嵌入來源不明的圖片。
- 選擇能最清楚呈現關係的視覺形式：教學寫實圖、示意圖、剖面圖、流程圖、時間軸、地圖、圖表、動畫或互動模擬。不要把所有內容都畫成通用卡通。
- 優先改善教材原生 SVG/CSS/JS 視覺與互動。只有使用者明確要求或點陣圖具有必要教學用途時才使用 raster image。
- 不用裝飾圖片掩蓋未完成的 SVG、錯誤資料、空白活動或無效互動。
- 保留專案既有且合理的資訊架構。七頁籤是 kickoff 專案的預設，不要強迫其他有效教材改成七頁籤。
- 所有標籤、數值、引線和說明文字都避開主體、資料點、座標軸、地名、控制元件與動畫路徑。
- 支援滑鼠、觸控、鍵盤及 `prefers-reduced-motion`；動態回饋使用適當語意與 `aria-live`。
- 未完成內容查核、視覺目視檢查、正式建置與多尺寸瀏覽器驗證前，不得部署或宣告完成。

## 教材來源與 Repository 規則

- 優先在使用者指定的教材資料夾或目前 workspace 工作；不要因舊版規則擅自移動專案。
- 若教材位於 `D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>`，直接處理靜態來源；需要 npm/node_modules 時可複製到 C: 暫存位置安裝與建置，再只同步來源檔。
- 正式 repository 名稱使用教材資料夾名稱或簡潔、可辨識的英文教材名稱，採 kebab-case。
- 不使用工作編號、日期流水號或無法辨識主題的名稱作為新 repository 名稱。
- 除非使用者明確要求，不把新教材部署為無關舊 repo 的子資料夾。

## 執行流程

### 1. 盤點現況與建立學習契約

1. 讀取專案結構、內容資料、樣式、互動、測驗、文件、Git 狀態與遠端設定。
2. 記錄主題、年級、先備知識、核心目標、可觀察表現、迷思概念與限制。
3. 建立「目標 → 視覺／互動 → 學生任務 → 成功證據」清單。
4. 盤點每個主要畫面，標出缺漏、占位內容、失真視覺、文字重疊、無效控制與待查核資訊。

### 2. 查核內容與規劃視覺

1. 查核會影響答案、外形、比例、方向、順序、因果或安全的資訊。
2. 將事實、推論、示意與簡化分開標示。
3. 為每個概念選擇最適合的視覺形式；只有靜態圖無法說清變化時才使用動畫。
4. 在 `docs/references.md` 記錄來源、網址、查核日期、使用目的與授權方式。
5. 發現原教材名稱、數值或敘述錯誤時，先修正並記錄，不照錯誤內容製圖。

### 3. 完成內容與互動

1. 移除 `待補`、占位、範例題及沒有教學意義的內容。
2. 讓互動要求學生觀察、分類、排序、比較、預測、操作變因、蒐集證據、解釋或修正，而非無目的點擊。
3. 提供清楚任務、操作提示、即時但不洩漏答案的回饋、重設與概念整理。
4. 對測驗或生成題進行答案唯一性、邊界值與錯誤回饋檢查。
5. 保留並改善專案已存在的有效功能；不要用全新 landing page 取代教材。

### 4. 製作精準視覺與動畫

1. 維持真實或概念上必要的比例、數量、角度、位置、方向、時序與辨識特徵。
2. 讓細節足以支援觀察，但控制在學生年齡可理解的複雜度。
3. 將標籤放在安全區，以短引線指出正確部位；空間不足時重構版面，不只縮小文字。
4. 動畫一次聚焦一個變化，保留可比較的前後狀態，並提供同步文字、播放、暫停與重播。
5. SVG 使用唯一 ID、適當 `viewBox`、明確的 `fill="none"` 與雙層 transform 群組，避免意外填色、定位覆寫和裁切。
6. 為重要 SVG 加入 `role="img"` 及能描述主體、動作、關係與教學目的的替代文字。

### 5. 建置與實際驗證

1. 執行 placeholder 掃描、專案既有 verifier、正式 build、套件安全檢查與 `git diff --check`。
2. 在至少 1440×1000、768×1024、390×844 三種 viewport 實際逐頁操作。
3. 檢查頁面內容、錯誤覆蓋層、主控台、失敗請求、水平溢出、裁切、文字重疊、引線、動畫前中後狀態、控制元件、鍵盤與降低動畫模式。
4. 對每個主要活動保存截圖並目視檢查，不以 DOM 數量或建置成功取代視覺檢查。
5. 發現錯誤時保存證據、分類原因、修正後以相同尺寸和步驟重測。
6. 將環境、測試項目、數值結果、截圖範圍與未解限制寫入 `docs/test-report.md`。

### 6. 分享、版本與部署

1. 要部署的教材加入 1200×630 社群預覽圖，以及完整 Open Graph/Twitter Card metadata；使用正式公開絕對網址。
2. 小型修正提升 patch；大幅重繪或新增完整活動提升 minor；不相容改版提升 major。
3. 同步更新適用的 `package.json`、lockfile、project config、README、CHANGELOG、references 與 test report。
4. 只提交本次範圍內的檔案，推送到名稱正確的專用 repo。
5. 等待部署流程完成，再確認公開首頁、CSS、JavaScript、教材資料及分享圖片均可取得。
6. 在公開版重做關鍵互動與手機版檢查，回報 URL、repo、版本、commit、部署與驗證結果。

## 部署閘門

以下任一項未通過就停止部署：

- 核心內容或重要時效資訊尚未查核。
- 圖像、公式、數值、地圖、方向、順序或因果存在已知錯誤。
- 使用授權不明的外部資產。
- 文字遮住重要資訊，或主體在任一必要 viewport 被裁切、溢出。
- 動畫跑出畫面、改變不應變動的條件、控制無效或 SVG 出現意外填色。
- 主要流程無法使用鍵盤或觸控完成。
- 正式建置失敗、教材資料載入失敗，或有未處理主控台錯誤。
- 文件、版本、repo 名稱或公開網址尚未同步。
- 尚未實際驗證公開部署。

## Skill 自我更新

修改此 Skill 包時：

1. 保持 `SKILL.md` 精簡，詳細規則放在單層 `references/`，不要在多個檔案重複同一規範。
2. 確認 frontmatter `name` 與資料夾名稱一致，`description` 與觸發情境一致。
3. 驗證 frontmatter YAML 格式正確（UTF-8、name 為 kebab-case、description 非空）。
4. 執行至少一項 reference 路由與關鍵規則抽查。
5. GitHub CLI 已登入時，在同一回合把本機與 `prayer168/digital-teaching-material-claude` 同步（可用 `scripts/publish-skill.ps1`）。

## 避免事項

- 不盲目回報預設 localhost port；讀取開發伺服器的實際網址。
- 不在只有骨架、單張漂亮圖片或部分頁面完成時宣告教材完成。
- 不把 `node_modules`、`dist`、開發 log 或未使用生成圖加入教材來源。
- 不用 PowerShell 的 `npm` shim 遇到執行政策問題時反覆失敗；改用 `npm.cmd`。
