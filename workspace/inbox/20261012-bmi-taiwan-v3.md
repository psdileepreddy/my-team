# Task: BMI calculator v3 — Taiwan bands, bilingual / 任務：BMI 計算機 v3（台灣標準＋中英雙語）

- From: Leader · Wailan
- To: Member · Taroko
- Date: 2026-10-12
- Mode: manual relay
- Deliverable is a **new** file. Do NOT touch `bmi-calculator.html` (that stays as the v1).
- Note updated 2026-10-12: folded in the captain's "more detail / more actions / better UI + download" request before the build started.

## What to do / 要做什麼

Take the v1 calculator and make **v3**: Taiwan standard categories + English and Traditional Chinese (Taiwan) in one page — **plus more detail, more actions, and a cleaner UI**.

以 v1 為基礎做 **v3**：改用台灣標準分類，同一頁支援英文與繁體中文（台灣用語），**並增加更多細節、更多動作與更好的介面**。

### 1. Taiwan categories (國健署) / 台灣分類

| BMI | English | 中文 |
|---|---|---|
| `< 18.5` | Underweight | 過輕 |
| `18.5 – 24.0` | Normal | 正常 |
| `24.1 – 28.0` | Overweight | 過重 |
| `> 28.0` | Obese | 肥胖 |

- Classify from the **raw** BMI, then round only the displayed number to 1 dp. / 用**未四捨五入**的 BMI 判定分類，顯示時才取到小數點一位。
- Formula unchanged: `BMI = weight / (height/100)^2`. / 公式不變。

### 2. Language / 語言

- **English is the default on load**; a button switches to 中文 and back. / 開啟預設英文，按鈕切換中文。
- Every string localised: title, labels, buttons, result heading, category names, **and every error message**. / 所有字串都要翻：標題、標籤、按鈕、結果標題、分類名稱，**還有每一則錯誤訊息**。
- Traditional Chinese, Taiwan usage. / 繁體中文、台灣用語。

### 3. Fix the v1 gap: input sanity range / 補 v1 的洞：輸入範圍檢查

v1 let a unit mistake through (`1.7` for height → BMI 224913.5, "Obese"). Add range checks with a clear message:

- Height `50–250` cm, Weight `10–500` kg, otherwise show an error and hide the result.
- Keep the existing empty / negative / zero checks too.

### 4. More detail: healthy weight range / 更多細節：健康體重範圍

Show, for the height entered, the weight range that lands in **正常 (18.5–24.0)**:

- `low  = 18.5 × (height_m)²` and `high = 24.0 × (height_m)²`, displayed in kg to 1 dp.
- Example: `170 cm` → **53.5 – 69.4 kg**.
- Show it in the currently selected language, using the correct unit wording.

### 5. More actions: download + print / 更多動作：下載＋列印

Two new buttons under the result:

- **Download report** — saves a `.txt` report built with a `Blob` + `URL.createObjectURL` + `<a download>`. Must contain: date, height, weight, BMI, category, healthy weight range, **written in the currently selected language**. Works completely offline (no fetch, no server).
- **Print / Save as PDF** — `window.print()` plus a `@media print` stylesheet that hides the buttons/inputs and prints just the result cleanly, so the user can save a PDF from the browser dialog.
- Both buttons disabled (or hidden) until a valid result exists. **No external libraries** — this must stay a single self-contained file.

### 6. UI polish / 介面

- Stronger visual hierarchy: the BMI number is the hero, category and healthy range read as secondary.
- Visible keyboard focus styles, labelled controls, works from 320 px width up to desktop.
- Buttons need clear pressed/disabled states; layout must not jump when the result appears.

### 7. Keep from v1 / 從 v1 保留

Reset button, result hidden on error, `aria-live` on the result, mobile viewport, clean layout. The **中文 toggle must also re-render an already-shown result, its buttons, and any visible error message.**

## Format / 格式

- **New file:** `workspace/outbox/bmi-calculator-v3.html` — single self-contained HTML, inline CSS+JS, **no external libraries/CDN/fonts**, no build step.
- **Handoff:** one handoff line in a **separate** file `workspace/outbox/20261012-bmi-v3-handoff.md` — do not put it inside the shipped HTML.
- No personal data in any file. / 不放個資。

## Done looks like / 怎樣算做完

1. Opens in a browser, **0 console errors**, English shown first. / 開啟無錯誤、預設英文。
2. `170 cm / 65 kg` → `22.5` → **Normal / 正常**. / 測資正確。
3. Band boundaries classify correctly:
   - `165 / 65.3` → `24.0` → **Normal / 正常**
   - `170 / 70.8` → `24.5` → **Overweight / 過重**
   - `170 / 82.4` → `28.5` → **Obese / 肥胖**
   - `170 / 49.1` → `17.0` → **Underweight / 過輕**
4. `1.7` as height → **error**, not a number. / 單位打錯要有提示。
5. Toggle to 中文 and every visible string — including an error message **and the download/print button labels** — is Chinese; toggle back and it is English again. / 切換後所有字串（含錯誤訊息與按鈕）跟著換語言。
6. `170 cm` shows healthy weight range **53.5 – 69.4 kg**. / 健康體重範圍計算正確。
7. **Download report** produces a `.txt` file with date, height, weight, BMI, category and healthy range, in the selected language; no console errors and no network request. / 下載報告內容正確、離線可用。
8. **Print** opens the browser print dialog and the printed page shows only the result (no buttons/inputs). / 列印版面乾淨。
9. Full keyboard-only pass: Tab through the form, focus always visible, Enter submits. / 鍵盤操作順暢。
10. `bmi-calculator.html` (v1) is **unchanged**. / v1 原封不動。
11. Handoff file states: what was built, what to watch, ready to use or not.

⚠️ Only create new files; never overwrite anything in `shared/` or the v1 deliverable. / 只新增、不覆蓋。
