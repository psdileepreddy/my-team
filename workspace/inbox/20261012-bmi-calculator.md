# Task: BMI calculator / 任務：BMI 計算機

- From: Leader · Wailan
- To: Member · Taroko
- Date: 2026-10-12
- Mode: manual relay

## What to do / 要做什麼

Build a simple **BMI calculator** the captain can open in a browser and use right away.

做一個小隊長直接用瀏覽器打開就能用的 **BMI 計算機**。

- Inputs: height in cm, weight in kg. / 入力：身高（公分）、體重（公斤）。
- Formula: `BMI = weight / (height/100)^2`. / 公式：`體重 / (身高/100)^2`。
- Show the BMI rounded to 1 decimal place. / 結果顯示到小數點一位。
- Show the category: Underweight `<18.5`, Normal `18.5–24.9`, Overweight `25–29.9`, Obese `≥30`. / 依數值顯示分類。
- Basic input checking: refuse negative/zero/empty values with a clear message. / 基本檢查：負數、0、空白要擋下來並給提示。

## Format / 格式

- One single self-contained HTML file (inline CSS + JS, no external libraries, no build step). / 單一 HTML 檔，CSS/JS 內嵌，不抓外部資源、不需編譯。
- File name: `bmi-calculator.html`. / 檔名 `bmi-calculator.html`。
- Save it as a **new file** in `workspace/outbox/`, plus one handoff line. / 另存新檔放 `workspace/outbox/`，並留一行交接。
- No personal data anywhere in the file or note. / 檔案與紙條都不放個資。

## Done looks like / 怎樣算做完

1. Opening `bmi-calculator.html` in a browser shows the form with no console errors. / 瀏覽器打開無錯誤。
2. `170 cm / 65 kg` → `22.5`, category Normal. / 測資正確。
3. Bad input (e.g. `-5`, `0`, blank) shows a friendly error, not a number. / 錯誤輸入有提示。
4. Handoff line in the outbox states: what was built, what to watch, ready to use or not. / outbox 有一行交接。

⚠️ Do not touch anything in `shared/`; do not overwrite any existing file. / `shared/` 不動、不覆蓋既有檔案。
