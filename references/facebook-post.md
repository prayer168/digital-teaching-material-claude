# 社群貼文：中英雙語臉書文 + 複製按鈕

完成一份教材、或完成這個 skill 包的部署後，可以用這個模板生成一篇**中英雙語臉書宣傳文**，並提供一個「右上角複製按鈕」的互動卡片，讓使用者一鍵複製文案。

## 何時使用

- 使用者說「臉書文」「FB 文」「社群貼文」「宣傳文」「貼文」「IG 文」「分享文」，或要求把成果發到社群。
- 部署完成（GitHub repo / GitHub Pages 上線）後，主動詢問是否要產生分享文。

## 產出方式（兩種，可同時做）

1. **互動複製卡片**：用 `show_widget` 工具渲染下方的 HTML 卡片，右上角有「複製全部」，中英文各自也有獨立複製鈕，點擊後顯示 ✓ 已複製。
2. **存成可部署檔案**（選用）：把同一份 HTML 存成教材專案內的 `share/facebook-post.html`，可隨教材一起部署到 GitHub Pages，方便日後直接開網址複製。

## 文案結構（中英對照）

兩種語言都遵循同一結構，逐段對應：

| 段落 | 中文 | English |
|------|------|---------|
| 開場鉤子 | 一句話講成果 + 表情符號 | one-line win + emoji |
| 背景一句 | 做了什麼、用什麼工具 | what you built, with what tool |
| 功能條列 | 📌 開頭，3–5 點 | 📌 bullets, 3–5 items |
| 最有感的事 | 「最有感的是——」 | "The best part —" |
| 價值收尾 | AI 不取代老師，而是… | AI isn't here to replace teachers… |
| 連結 | 🔗 GitHub / Pages 連結 | 🔗 link |
| 標籤 | 5–8 個 #hashtag | 5–8 #hashtags |

撰寫原則：

- 口語、溫暖、貼近教師日常；避免行銷腔。
- 功能條列用教材實際做到的事，不要空泛。
- 連結用實際的 repo 或 GitHub Pages 網址（不要 `example.com`）。
- 中英文是兩篇可獨立發佈的完整貼文，不是逐字直譯，語感要各自自然。
- 標籤中英分開，符合各語系平台習慣。

## 互動複製卡片 HTML 模板

把 `{{ZH_POST}}` 與 `{{EN_POST}}` 換成實際文案（保留換行）。用 `show_widget` 渲染，或存成 `share/facebook-post.html`（若要當獨立網頁，需自行補上外層 html 結構與字型）。

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
      <span style="font-size: 13px; font-weight: 500; color: var(--color-text-info); background: var(--color-background-info); padding: 3px 10px; border-radius: var(--border-radius-md);">中文</span>
      <button class="copy-one" data-target="zh" style="display: inline-flex; align-items: center; gap: 6px; font-size: 13px; padding: 4px 10px; cursor: pointer;"><i class="ti ti-copy" style="font-size: 15px;" aria-hidden="true"></i><span class="lbl">複製</span></button>
    </div>
    <div id="zh" style="white-space: pre-wrap; font-size: 15px; line-height: 1.7; background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 1rem 1.1rem;">{{ZH_POST}}</div>
  </div>
  <div>
    <div style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 8px;">
      <span style="font-size: 13px; font-weight: 500; color: var(--color-text-info); background: var(--color-background-info); padding: 3px 10px; border-radius: var(--border-radius-md);">English</span>
      <button class="copy-one" data-target="en" style="display: inline-flex; align-items: center; gap: 6px; font-size: 13px; padding: 4px 10px; cursor: pointer;"><i class="ti ti-copy" style="font-size: 15px;" aria-hidden="true"></i><span class="lbl">Copy</span></button>
    </div>
    <div id="en" style="white-space: pre-wrap; font-size: 15px; line-height: 1.7; background: var(--color-background-secondary); border-radius: var(--border-radius-md); padding: 1rem 1.1rem;">{{EN_POST}}</div>
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
  document.getElementById('copy-all').addEventListener('click', function () { copy(zh + '\n\n— — —\n\n' + en, this, '已複製！'); });
  document.querySelectorAll('.copy-one').forEach(function (b) {
    b.addEventListener('click', function () {
      var t = this.getAttribute('data-target');
      copy(document.getElementById(t).textContent, this, t === 'zh' ? '已複製！' : 'Copied!');
    });
  });
})();
</script>
```

## 範例（可直接套用的語氣）

中文開場：`🎓✨ 來分享一個讓我教學備課大躍進的小成果！`
English opener: `🎓✨ Sharing a small win that's seriously leveled up my lesson prep!`

價值收尾固定句型：

- 中文：`AI 不是拿來取代老師，而是把備課裡那些重複、瑣碎的工通通交給它，讓我們把時間留給真正重要的事：陪孩子學習。 ❤️`
- English：`AI isn't here to replace teachers. It takes the repetitive, tedious parts of prep off our plate, so we can spend our time on what truly matters: being there for our kids. ❤️`
