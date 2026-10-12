# Task: BMI calculator v3 — Taiwan bands, bilingual / 任務：BMI 計算機 v3（台灣標準＋中英雙語）

- From: Leader · Wailan
- To: Member · Taroko
- Date: 2026-10-12
- Mode: manual relay
- Replaces: nothing — **this is a new file. Do NOT touch `bmi-calculator.html` (that stays as the v1).**

## What to do / 要做什麼

Take the v1 calculator and make **v3**: Taiwan standard categories + English and Traditional Chinese (Taiwan) in one page.

以 v1 為基礎做 **v3**：改用台灣標準分類，同一頁支援英文與繁體中文（台灣用語）。

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

### 4. Keep from v1 / 從 v1 保留

Reset button, result hidden on error, `aria-live` on the result, mobile viewport, clean layout.

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
5. Toggle to 中文 and every visible string — including an error message — is Chinese; toggle back and it is English again. / 切換後所有字串（含錯誤訊示）跟著換語言。
6. `bmi-calculator.html` (v1) is **unchanged**. / v1 原封不動。
7. Handoff file states: what was built, what to watch, ready to use or not.

⚠️ Only create new files; never overwrite anything in `shared/` or the v1 deliverable. / 只新增、不覆蓋。
