---
name: digital-teaching-material-claude
description: >-
  Polish, complete, verify, and deploy elementary interactive digital teaching materials after project kickoff. Use when Claude Code is asked to turn a generated Vite/HTML/CSS/JS lesson scaffold into a complete classroom-ready教材, fill all seven tabs, remove placeholder content, improve native SVG/CSS animations instead of adding unrelated static banners, add quizzes/resources/references/docs, verify builds, work from the Google Drive G:教材根目錄, commit, push, create a new same-name GitHub repo, or prepare GitHub Pages.
---

# 數位教材開發 Claude Code 版

Use this skill after a project has already been created by `teaching-material-kickoff` or has the same Vite + native HTML/CSS/JS structure.

The goal is to turn a working scaffold into a complete, classroom-usable interactive lesson without replacing the app with a landing page or unrelated images.

## Core Rules

- The local source-of-truth folder for every digital lesson is `G:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>`. The `<projectName>` folder name must be the lesson's English kebab-case name.
- Work directly in the G: lesson folder for static HTML/CSS/JS changes and documentation. If a Vite/npm workflow needs `node_modules`, copy to a temporary C: work folder for install/build only, then sync source changes back to G: excluding `node_modules`, `dist`, `.git`, and dev logs.
- When deploying remotely, create a new GitHub repo whose name exactly matches the local folder name. Do not deploy a new lesson as a subfolder inside an unrelated existing repo unless the user explicitly asks.
- Keep the seven-tab app structure: 學習任務、原理探索、互動實驗、動畫模擬、生活應用、闖關大挑戰、自學資源.
- Fill content, not just structure. Remove all `待補`, `範例`, `示範題`, and placeholder text.
- Prefer improving native SVG/CSS/JS interactions already in the lesson. If the user asks for more realistic SVG animation, refine the SVG paths, gradients, roots, veins, petals, seeds, timing, and CSS states; do not add static scene banners as a substitute.
- Use raster images only when the user explicitly asks for generated images or when an image is a purposeful interactive asset. Never hide incomplete SVG work behind a decorative image.
- Keep docs aligned with the implementation: `README.md`, `docs/design-spec.md`, `docs/lesson-plan.md`, `docs/references.md`, `docs/test-report.md`.
- When this skill package itself is modified, validate it and publish the change to its same-name GitHub repo with `scripts/publish-skill.ps1`. Do this in the same turn as the local edit whenever GitHub CLI is authenticated.

## Workflow

1. Read the project structure and current files:
   - `index.html`
   - `css/style.css`, `css/animation.css`, `css/responsive.css`
   - `js/app.js`, `js/interactions.js`, `js/quiz.js`
   - `data/content.json`, `data/quiz.json`, `data/resources.json`
   - `docs/*.md`
2. Load the detailed checklist only when doing actual polish work: `references/post-kickoff-polish.md`.
3. Complete the lesson content:
   - Every tab has meaningful grade-appropriate content.
   - `data/content.json` has 6-8 interactive生活應用 cases.
   - `data/quiz.json` has at least 10 questions with explanations.
   - `data/resources.json` media entries have `source`, `grade`, and `checkedDate`.
4. Improve interaction and visuals:
   - Make SVGs more realistic with structure and motion.
   - Keep text separated from animated visuals.
   - Preserve `prefers-reduced-motion`.
   - Verify all buttons, sliders, tabs, cards, quiz feedback, and resource links.
5. Validate:
   - Run `rg "待補|範例題|示範題|占位" <project> -g '!node_modules' -g '!dist'`.
   - Run the kickoff verifier if available:
     `python "%USERPROFILE%\.claude\skills\teaching-material-kickoff\scripts\verify.py" --project "<project>"`
   - Run `npm.cmd run build` only in a C: temporary copy when the project needs npm/node_modules.
6. Version and deploy:
   - Commit intentional changes in the G: lesson repo.
   - For remote deployment, use GitHub CLI to create/push a repo named exactly like the local folder, e.g. `gh repo create <githubUser>/<projectName> --public --source . --remote origin --push`.
   - Enable GitHub Pages from `main` branch root `/` and verify `https://<githubUser>.github.io/<projectName>/`.
7. Share (optional): after a successful deploy, offer to generate a bilingual (中文 + English) Facebook announcement post. See `## Bilingual Facebook Post` below.

## Bilingual Facebook Post (integrates the `social-post` skill)

When the user asks for a 臉書文／FB文／社群貼文／宣傳文／IG文／分享文, or right after a deploy when offering to share results, produce a bilingual Chinese + English Facebook post. This step **combines with the `social-post` skill** (by 駱君昊 Hao, MIT) for viral formulas and voice rules.

- Load `references/facebook-post.md` for the full integration flow, formula selection, copy-card template, and fallback.
- If `~/.claude/skills/social-post/` is installed, route the post through it: apply `style_profile.md` voice if present, pick a formula (default **F15 mini** for a freshly-shipped lesson; **F6b** for a big launch; **F29** for a re-ship), and follow its hard rules from `social-post/references/rules.md`. If it is not installed, use the fallback template and mention it can be installed for stronger copy.
- 🚨 **R25 — never put the repo / GitHub Pages URL in the FB or Threads body.** Put it in the 📌 first comment instead; use an R35 keyword CTA in the body ("留言『教材』我把連結傳你"). The real URL must be a true link (never `example.com`).
- Apply R34 (real voice, no AI-tone abstract words), R36 (demo > claim — cite the seven tabs, quiz count, live URL), R37 (value-prop-lead opening).
- Render an interactive copy card with `show_widget`: three blocks (中文正文 / English body / 📌 留言連結), each with its own copy button plus a top-right "複製全部", each flashing ✓ on success.
- Optionally save the same card as `share/facebook-post.html` inside the lesson project so it can ship to GitHub Pages.
- This skill only **generates copy**. If the user wants to actually auto-publish to Facebook, that is the `social-post` skill's Phase 2 — and its safety gate requires an explicit user "確認" before publishing; never bypass it.

## Skill Self-Publish

When updating this skill package, local and remote copies must stay in sync:

1. Edit the skill files locally.
2. Validate the skill if `skill-creator`'s `quick_validate.py` is available (the publish script skips validation gracefully when it is not).
3. Run:
   `powershell -ExecutionPolicy Bypass -File .\scripts\publish-skill.ps1 -Message "<short update summary>"`

The script commits changed files, pushes to a GitHub repo whose name matches this skill folder, and installs a local `post-commit` hook so future commits auto-push to the configured upstream.

## Avoid These Mistakes

- Do not report `http://127.0.0.1:5173/` blindly. Read Vite output and use the actual port.
- Do not say the material is complete when only the scaffold exists.
- Do not leave generated project assets in a temporary images folder; copy final project assets into `assets/`.
- Do not keep unused generated images referenced nowhere in the page.
- Do not use PowerShell `npm` when execution policy blocks `npm.ps1`; use `npm.cmd`.
