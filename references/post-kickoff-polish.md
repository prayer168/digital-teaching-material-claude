# Post-Kickoff Polish Checklist

Use this reference when completing or revising a scaffolded elementary interactive digital lesson.

## Local Folder and Deploy Pattern

- The local source-of-truth folder for every digital lesson is:
  `D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>`
- `<projectName>` is the lesson's English kebab-case name and must also be the GitHub repo name.
- Static HTML/CSS/JS lessons can be edited, validated, committed, and deployed directly from the D: folder.
- If a project needs npm/node_modules, create a temporary C: copy only for install/build:

```powershell
robocopy "D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>" "C:\dev\<projectName>" /E /XD node_modules dist .git /XF vite-dev.out.log vite-dev.err.log
cd "C:\dev\<projectName>"
npm.cmd install
npm.cmd run build
robocopy "C:\dev\<projectName>" "D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>" /E /XD node_modules dist .git /XF vite-dev.out.log vite-dev.err.log
```

## Complete Content Standards

- Mission tab:
  - Has a concrete student role or task.
  - Lists 2-4 observable learning goals.
- Explore tab:
  - Explains core concepts with grade-appropriate language.
  - Uses a visual model beside text.
- Interact tab:
  - Has a real input (slider/button/toggle) and an observable result.
  - Readout text changes with the input.
- Animation tab:
  - Plays in stages; not all elements move at once.
  - Caption changes with the stage.
- Apply tab:
  - Has 6-8生活應用 cases.
  - Every card has a visible SVG/CSS change when clicked.
- Quiz tab:
  - At least 10 questions.
  - Each question has four choices, an answer index, and explanation.
  - Feedback appears immediately and locks each answered question.
- Resources tab:
  - Has real links, not `example.com`.
  - Each media item has `source`, `grade`, `checkedDate`.

## SVG Realism Pattern

When the user asks for more realistic visuals in an existing SVG app, improve the SVG itself.

Good SVG refinements:

- Add `<defs>` gradients for soil, stems, petals, water, sunlight.
- Add root branching and root hairs.
- Add leaf veins and asymmetrical leaf shapes.
- Add soil grains and cutaway layers.
- Add stem highlights and shadows.
- Add flower centers, petal outlines, fruit cross-sections, visible seeds.
- Use `filter: drop-shadow(...)` sparingly for depth.
- Use staged CSS transitions and subtle motion:
  - leaf sway
  - water flowing upward
  - flower opening
  - fruit appearing
  - seed movement

Avoid:

- Adding static 16:9 scene images when the request is to improve SVG animation.
- Covering SVG weakness with decorative banners.
- Making text overlap animation.
- Overly cartoonish faces or fantasy plant parts.

## Verification Commands

Run from any folder:

```powershell
rg "待補|範例題|示範題|占位" "D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>" -g "!node_modules" -g "!dist"
python "$env:USERPROFILE\.claude\skills\teaching-material-kickoff\scripts\verify.py" --project "D:\我的雲端硬碟\google drive\000000000backup\0000000000數位教材\<projectName>"
```

If a build is needed, run it from a C: temporary copy:

```powershell
npm.cmd run build
```

Read the real error and fix it. Common issue: CSS minifiers may reject invalid SVG/CSS fallback syntax such as `url(#id, fallback)`.

## Browser Verification

- Read Vite logs for the actual port. If `5173` is taken, Vite may choose `5174`, `5175`, etc.
- In the browser, verify:
  - all seven tabs switch
  - SVG details render
  - sliders/buttons update state
  - quiz shows 10 cards
  - apply cards respond to clicks
  - resource links are visible with sources

## Git / Push Pattern

- Commit in the D: lesson folder.
- Remote deployment always creates or uses a dedicated repo whose name exactly matches the local folder name:
  `<githubUser>/<projectName>`.
- If no remote exists, use GitHub CLI when authenticated:

```powershell
gh repo create <user>/<projectName> --public --source . --remote origin --push
gh api --method POST repos/<user>/<projectName>/pages -f "source[branch]=main" -f "source[path]=/"
```

- If remote exists, verify that it points to the same-name repo before pushinD:

```powershell
git push
```

Do not deploy a new lesson into an unrelated existing repo as a subfolder unless the user explicitly asks.
