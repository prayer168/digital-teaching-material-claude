# Digital Teaching Material Claude Code Skill

這是一個給 Claude Code 使用的數位教材製作技能包，主要用來把已建立好的互動式教材骨架，打磨成可以在課堂上使用、可以部署到 GitHub Pages 的完整教材。

## 這個 Skill 做什麼

`digital-teaching-material-claude` 適合用在國小互動數位教材的後製、補完、驗證與部署。它會引導 Claude Code 完成下列工作：

- 補齊七個教材分頁：學習任務、原理探索、互動實驗、動畫模擬、生活應用、闖關大挑戰、自學資源。
- 移除 scaffold 產生的待補文字、範例題與 placeholder。
- 製作或改善原生 HTML/CSS/JS/SVG 互動效果。
- 補齊生活應用卡、測驗題、資源連結、教師文件與測試紀錄。
- 驗證教材互動、版面、測驗、資源與 GitHub Pages 部署結果。
- 依照本地資料夾名稱建立同名 GitHub repo，並啟用 GitHub Pages。

## 本地端教材資料夾規則

所有新教材的正式本地端來源都放在：

```text
D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>
```

其中 `<projectName>` 是教材英文名稱，使用 kebab-case，例如：

```text
light-shadow-inquiry
```

這個名稱同時也是：

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
3. 執行 placeholder 掃描與必要的 build/browser 驗證。
4. 在本地教材資料夾 commit。
5. 建立同名 GitHub repo。
6. 啟用 GitHub Pages 並確認公開網址。

## 遠端部署規則

遠端部署時，一份教材對應一個新的 GitHub repo。repo 名稱必須和本地端教材資料夾名稱完全一致。

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

1. 驗證 skill 格式（若找不到 skill-creator 的驗證工具會自動略過）。
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
- 修改 skill 後要同步到 GitHub，避免本地與遠端版本不一致。
