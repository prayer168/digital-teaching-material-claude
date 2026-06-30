# 社群貼文：中英雙語臉書文 + 複製按鈕（整合 social-post skill）

完成一份教材、或完成這個 skill 包的部署後，可以用這個流程生成一篇**中英雙語臉書宣傳文**，並提供「右上角複製按鈕」的互動卡片，讓使用者一鍵複製文案。

> 本流程已**整合 `social-post` skill**（作者：駱君昊 Hao，MIT）。產文時要套用它的爆款公式、語氣鐵則與安全規則；`social-post` 沒安裝時，仍可用本檔末的後備模板產出。

## 何時使用

- 使用者說「臉書文」「FB 文」「社群貼文」「宣傳文」「貼文」「IG 文」「分享文」，或要求把成果發到社群。
- 教材部署完成（GitHub repo / GitHub Pages 上線）後，主動詢問是否要產生分享文。

## 與 social-post skill 結合的步驟

1. **偵測 `social-post` skill**：檢查 `~/.claude/skills/social-post/` 是否存在。
   - 存在 → 走「整合模式」（下面 2–6 步）。
   - 不存在 → 用本檔末「後備模板」直接生成，並提醒使用者可安裝 `social-post` 取得更強的爆款語氣。
2. **套用語氣**：若 `~/.claude/skills/social-post/style_profile.md` 存在，先讀它當 voice 錨點（公式 < 語氣）。沒有就用本檔的預設教師口語語氣。
3. **選公式**（教材情境對應，細節讀 `social-post/references/formulas.md` 對應段落即可，不必全文）：
   | 情境 | 用公式 | 理由 |
   |---|---|---|
   | 教材／skill／repo **剛 ship**，想快速擴散（預設） | **F15 mini**（3 段：成果 hook + 歸功工具 + 零摩擦索取 CTA）| 5 秒讀懂、儲存率高、最低成本 |
   | 大型教材 launch、想衝 mega-viral | **F6b 變體 A**（4 段 4 句：成果炸場 meta hook → 過程數字 → 使用體驗 → 社群召集 CTA）| ship announcement 首次見光 |
   | 教材**大改版／補完**再推一次 | **F29 再ship揭露型** | 避開「又更新了」疲勞 |
   | 學員／同事用這套做出成績 | **F28 第三方戰績** | works-for-others > I'm great |
4. **套用硬規則**（讀 `social-post/references/rules.md` 對應條目；以下為產教材文必檢）：
   - 🚨 **R25：FB／Threads 正文絕不放外部連結**。GitHub／Pages 連結一律放**第一則留言（精選留言）**，正文改用 R35 keyword CTA（例：「想要的留言『教材』，我把連結傳你」）或「連結放留言區自取」。
   - 🚨 **R34：真實 voice**。禁抽象空詞（護城河／本質／真正的 X）、禁 staged 開場、禁 over-narrate；日常標點（，、！）照用。
   - **R36：demo > claim**。秀具體成品／可驗證數字（七大分頁、N 題測驗、實際網址成果），不要空泛「我很厲害」。
   - **R37：value-prop-lead 開場**。先講「它幫你／幫學生做到什麼」，再講 meta 故事。
   - **R35：keyword CTA** 比正文連結強 100x；爆量留言時改精選留言公開 link（別手動私訊全部，避免封號）。
5. **產出雙語 + 留言**：
   - 中文正文：套用上面選定公式（預設 F15 mini）。
   - English 正文：同結構但語感各自自然，不逐字直譯。
   - 📌 **第一則留言**：放真實連結（repo / GitHub Pages 教材網址），中英各一行。
6. **呈現**：用 `show_widget` 渲染下方互動卡片（中文正文 / English 正文 / 📌 留言連結 三區，各自有複製鈕，右上角「複製全部」）。可另存成教材專案的 `share/facebook-post.html` 隨 Pages 部署。

> ⚠️ 若使用者接著要**真的自動發到 FB**：那屬於 `social-post` 的 Phase 2 範疇，改走 `social-post/references/generate_and_publish.md` + `facebook.md`，且**發佈前必須拿到使用者明確「確認」字眼**（social-post 安全閘，不可 bypass）。本 skill 只負責「生成可複製文案」，不自動發佈。

## 文案結構（教材情境，中英對照）

以 F15 mini 為預設骨架（3 段，零繞圈）：

| 段落 | 中文 | English |
|------|------|---------|
| 1. 成果 hook + ！！！ | 「＜教材主題＞互動教材上線啦！！！」 | "Just shipped an interactive ＜topic＞ lesson!!!" |
| 2. 歸功工具 + 價值 | 「用 Claude Code + 這個 skill，七大分頁＋N 題測驗一次補完」 | "Built with Claude Code + this skill — seven tabs and N quizzes, all done" |
| 3. 零摩擦索取 CTA（R35，**不放連結**） | 「想要網址的留言『教材』，我放留言區」 | "Want the link? Comment 'lesson' — it's in the first comment" |

撰寫原則：

- 口語、溫暖、貼近教師日常；避免行銷腔與 AI 腔（R34）。
- 用教材實際做到的事（七大分頁、互動實驗、N 題測驗、實際成果）當 demo（R36）。
- **正文不放連結**；連結進第一則留言（R25）。
- 中英文是兩篇可獨立發佈的完整貼文，不是逐字直譯。
- FB hashtag 0–2 個即可（FB 不靠 tag 擴散）；要放多標籤改放貼文尾或留言。

## 互動複製卡片 HTML 模板

把 `{{ZH_POST}}` / `{{EN_POST}}` / `{{LINK_COMMENT}}` 換成實際內容（保留換行）。用 `show_widget` 渲染，或存成 `share/facebook-post.html`（當獨立網頁時需自行補 html 外層與字型）。

```html
<div style="padding: 0.5rem 0;">
<div style="background: var(--color-background-primary); border: 0.5px solid var(--color-border-tertiary); border-radius: var(--border-radius-lg); padding: 1.25rem 1.25rem 1.5rem;">
  <div style="display: flex; align-items: center; justify-content: space-between; gap: 12px; margin-bottom: 1.25rem;">
    <span style="font-size: 16px; font-weight: 500;">臉書文案 · Facebook post</span>
    <button id="copy-all" style="display: inline-flex; align-items: center; gap: 6px; font-size: 14px; padding: 6px 14px; cursor: pointer;">
      <i class="ti ti-copy" style="font-size: 16px;" aria-hidden="true"></i><span class="lbl">複製全部</span>
    </button>
  </div>
  <div style="margin-bottom: 1.25rem;">
    <div style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px;">
      <span style="font-size: 13px; font-weight: 500; color: var(--color-text-info); background: var(--color-background-info); padding: 3px 10px; border-radius: var(--border-radius-md);">中文正文</span>
      <button class="copy-one" data-target="zh" style="display: inline-flex; align-items: center; gap: 6px; font-size: 13px; padding: 4px 10px; cursor: pointer;"><i class="ti ti-copy" style="font-size: 15px;" aria-hidden="true"></i><span class="lbl">複製</span></button>
    </div>
    <div id="zh" style="white-space: pre-wrap; font-size: 15px; line-height: 1.7; background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 1rem 1.1rem;">{{ZH_POST}}</div>
  </div>
  <div style="margin-bottom: 1.25rem;">
    <div style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px;">
      <span style="font-size: 13px; font-weight: 500; color: var(--color-text-info); background: var(--color-background-info); padding: 3px 10px; border-radius: var(--border-radius-md);">English body</span>
      <button class="copy-one" data-target="en" style="display: inline-flex; align-items: center; gap: 6px; font-size: 13px; padding: 4px 10px; cursor: pointer;"><i class="ti ti-copy" style="font-size: 15px;" aria-hidden="true"></i><span class="lbl">Copy</span></button>
    </div>
    <div id="en" style="white-space: pre-wrap; font-size: 15px; line-height: 1.7; background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 1rem 1.1rem;">{{EN_POST}}</div>
  </div>
  <div>
    <div style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px;">
      <span style="font-size: 13px; font-weight: 500; color: var(--color-text-warning); background: var(--color-background-warning); padding: 3px 10px; border-radius: var(--border-radius-md);">📌 第一則留言（放連結 · R25）</span>
      <button class="copy-one" data-target="lk" style="display: inline-flex; align-items: center; gap: 6px; font-size: 13px; padding: 4px 10px; cursor: pointer;"><i class="ti ti-copy" style="font-size: 15px;" aria-hidden="true"></i><span class="lbl">複製</span></button>
    </div>
    <div id="lk" style="white-space: pre-wrap; font-size: 15px; line-height: 1.7; background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 1rem 1.1rem;">{{LINK_COMMENT}}</div>
  </div>
</div>
</div>
<script>
(function () {
  function flash(btn, okText) {
    var lbl = btn.querySelector('.lbl'), icon = btn.querySelector('i');
    var pl = lbl ? lbl.textContent : '', pi = icon ? icon.className : '';
    if (lbl) lbl.textContent = okText;
    if (icon) icon.className = 'ti ti-check';
    setTimeout(function () { if (lbl) lbl.textContent = pl; if (icon) icon.className = pi; }, 1600);
  }
  function fallback(text, btn, ok) {
    var ta = document.createElement('textarea');
    ta.value = text; ta.style.position = 'fixed'; ta.style.opacity = '0';
    document.body.appendChild(ta); ta.select();
    try { document.execCommand('copy'); flash(btn, ok); } catch (e) {}
    document.body.removeChild(ta);
  }
  function copy(text, btn, ok) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(text).then(function () { flash(btn, ok); }).catch(function () { fallback(text, btn, ok); });
    } else { fallback(text, btn, ok); }
  }
  var zh = document.getElementById('zh').textContent;
  var en = document.getElementById('en').textContent;
  var lk = document.getElementById('lk').textContent;
  document.getElementById('copy-all').addEventListener('click', function () { copy(zh + '\n\n— — —\n\n' + en + '\n\n— — —\n📌 ' + lk, this, '已複製！'); });
  document.querySelectorAll('.copy-one').forEach(function (b) {
    b.addEventListener('click', function () {
      var t = this.getAttribute('data-target');
      copy(document.getElementById(t).textContent, this, t === 'en' ? 'Copied!' : '已複製！');
    });
  });
})();
</script>
```

## 後備模板（`social-post` 未安裝時）

仍輸出中英雙語 + 複製卡片，但語氣用通用教師口語。**即使後備模式，也建議遵守 R25**（連結放第一則留言），因為 FB 演算法對正文外部連結降權 30–50%。

固定價值收尾句型：

- 中文：`AI 不是拿來取代老師，而是把備課裡那些重複、瑣碎的工通通交給它，讓我們把時間留給真正重要的事：陪孩子學習。 ❤️`
- English：`AI isn't here to replace teachers. It takes the repetitive, tedious parts of prep off our plate, so we can spend our time on what truly matters: being there for our kids. ❤️`

## 來源致謝

爆款公式、語氣鐵則（R1–R42）、發佈流程來自 `social-post` skill：
- 作者：駱君昊 (Hao) · https://github.com/Hao0321/claude-skill-social-post · MIT License
