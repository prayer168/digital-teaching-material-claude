# Digital Teaching Material Claude Code Skill

這是一個給 Claude Code 使用的數位教材製作技能包，主要用來把已建立好的互動式教材骨架，打磨成可以在課堂上使用、可以部署到 GitHub Pages 的完整教材。

## 這個 Skill 做什麼

`digital-teaching-material-claude` 適合所有學科、年級與教材架構的互動數位教材建立、後製、補完、驗證與部署。它會引導 Claude Code 完成下列工作：

- 若是 kickoff 七頁籤教材，補齊學習任務、原理探索、互動實驗、動畫模擬、生活應用、闖關大挑戰與自學資源；其他教材保留既有且合理的資訊架構。
- 移除 scaffold 產生的待補文字、範例題與 placeholder。
- 製作或改善原生 HTML/CSS/JS/SVG 互動效果。
- 補齊生活應用卡、測驗題、資源連結、教師文件與測試紀錄。
- 加入 1200x630 社群預覽圖與 Open Graph/Twitter Card meta 標籤，讓 Facebook、LINE、X 等平台分享時顯示漂亮縮圖卡片。
- 驗證教材互動、版面、測驗、資源與 GitHub Pages 部署結果。
- 依照教材資料夾名稱或簡潔英文教材名稱建立 GitHub repo，並啟用 GitHub Pages。
- 先建立學習目標與視覺證據矩陣，再以可信來源交叉查核重要內容。
- 依概念選擇教學寫實圖、示意圖、剖面圖、流程圖、時間軸、地圖、圖表、動畫或互動模擬。
- 檢查數學、科學、社會、語文、藝術及健康生活教材各自需要的精準度。
- 在桌機、平板、手機逐頁目視驗證裁切、重疊、動畫狀態、鍵盤、觸控與降低動畫模式。
- 部署完成後可產生中英雙語臉書宣傳文與一鍵複製卡片（見 `references/facebook-post.md`）。

## 本地端教材資料夾規則

優先在使用者指定的教材資料夾或目前 workspace 工作，不因舊版規則擅自移動專案。若使用者採用既有的 Google Drive 教材根目錄，路徑為：

```text
D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>
```

其中 `<projectName>` 是教材英文名稱，使用 kebab-case，例如：

```text
light-shadow-inquiry
```

此類專案通常讓 `<projectName>` 同時作為：

- 本地端資料夾名稱
- GitHub repo 名稱
- GitHub Pages 網址路徑

例如：

```text
D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\light-shadow-inquiry
https://github.com/prayer168/light-shadow-inquiry
https://prayer168.github.io/light-shadow-inquiry/
```

## 安裝方式

### 方法一：從 GitHub clone 到 Claude Code skills 目錄

在 PowerShell 執行：

```powershell
cd "$env:USERPROFILE\.claude\skills"
git clone https://github.com/prayer168/digital-teaching-material-claude.git
```

如果資料夾已存在，請改用更新：

```powershell
cd "$env:USERPROFILE\.claude\skills\digital-teaching-material-claude"
git pull
```

### 方法二：手動放置

把整個 `digital-teaching-material-claude` 資料夾放到：

```text
C:\Users\<你的使用者名稱>\.claude\skills\digital-teaching-material-claude
```

重新開啟 Claude Code 後，技能會被載入。

## 使用方式

在 Claude Code 對話中提到這個 skill，或提出符合它用途的任務，例如：

```text
使用 digital-teaching-material-claude，幫我把這份教材補完並部署。
```

或：

```text
把 D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\light-shadow-inquiry 補齊、驗證並部署到 GitHub Pages。
```

Claude Code 會依照 skill 流程執行：

1. 讀取教材檔案與資料結構。
2. 補齊內容、互動、動畫、測驗與文件。
3. 製作或複用 1200x630 社群預覽圖，放到 `public/img/og/<projectName>.png`。
4. 在 `index.html` 加入 `description`、`og:*`、`twitter:*` meta 標籤，`og:image` 使用 GitHub Pages 的絕對網址。
5. 執行 placeholder 掃描與必要的 build/browser 驗證，並確認 build 後 `dist/img/og/<projectName>.png` 存在。
6. 在本地教材資料夾 commit。
7. 建立同名 GitHub repo。
8. 啟用 GitHub Pages 並確認公開網址。

## 社群分享縮圖規則

每份要部署的教材都要具備 Facebook/Open Graph 分享卡片：

- 預覽圖尺寸固定為 `1200x630`，建議 PNG。
- 圖片放在 `public/img/og/<projectName>.png`，讓 Vite build 後輸出到 `dist/img/og/<projectName>.png`。
- `index.html` 的 `<head>` 需包含 `meta name="description"`、`og:title`、`og:description`、`og:url`、`og:image`、`og:image:secure_url`、`og:image:width`、`og:image:height`、`og:image:type`、`og:image:alt`、`twitter:card`、`twitter:title`、`twitter:description`、`twitter:image`。
- `og:url` 和圖片網址要使用部署後的絕對網址，例如：

```text
https://prayer168.github.io/<projectName>/
https://prayer168.github.io/<projectName>/img/og/<projectName>.png
```

- 部署後可用 Facebook Sharing Debugger 重新抓取快取：

```text
https://developers.facebook.com/tools/debug/
```

## 遠端部署規則

遠端部署時，一份教材使用一個專用 GitHub repo。repo 名稱採用教材資料夾名稱或簡潔、可辨識的英文教材名稱，不使用工作編號或日期流水號。

範例：

```text
本地資料夾：light-shadow-inquiry
GitHub repo：prayer168/light-shadow-inquiry
GitHub Pages：https://prayer168.github.io/light-shadow-inquiry/
```

除非使用者明確要求，否則不要把新教材放進舊 repo 的子資料夾。

## 更新這個 Skill 包

這個 skill 包本身也已經設定 GitHub 同步流程。

如果你修改了 skill 內容，請在 skill 資料夾內執行：

```powershell
cd "$env:USERPROFILE\.claude\skills\digital-teaching-material-claude"
powershell -ExecutionPolicy Bypass -File .\scripts\publish-skill.ps1 -Message "描述這次修改"
```

這個腳本會：

1. 驗證 skill 格式（若本機有 skill-creator 的 `quick_validate.py`；沒有則自動略過）。
2. commit 本地變更。
3. push 到 GitHub repo。
4. 安裝或更新本地 `post-commit` hook，讓後續 commit 自動嘗試 push。

目前遠端 repo：

```text
https://github.com/prayer168/digital-teaching-material-claude
```

## 注意事項

- Google Drive D: 目錄不要直接跑 `npm install`，避免 `node_modules` 損壞。
- 若教材需要 Vite/npm build，請暫時複製到 `C:\dev\<projectName>` 進行 install/build，再把原始碼同步回 D:。
- 每次部署前都要確認沒有 placeholder、範例題或待補內容。
- 每次部署前都要確認社群預覽圖尺寸、Open Graph meta 標籤和 GitHub Pages 絕對網址正確。
- 修改 skill 後要同步到 GitHub，避免本地與遠端版本不一致。
