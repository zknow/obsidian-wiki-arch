---
job: inbox
---

## Trigger

```
run inbox                  ← 掃描全部自動匯入
run inbox <檔名>           ← 只處理指定檔案
run inbox --h              ← 顯示此說明
```

## Purpose

將 `inbox/` 中的原始素材自動匯入 wiki。讀取內容、分類、建立或更新頁面、歸檔至 `archive/`、更新 `index.md` 與 `changelog.md`。

## Input

- `inbox/` 中的檔案（排除 `.gitignore`）
- `wiki/` 下所有現有頁面（用於比對重複）
- `wiki/index.md` — 目錄大綱
- `wiki/changelog.md` — 更新日誌

## Steps

### 1. 掃描 inbox

讀取 `inbox/` 中所有檔案（排除 `.gitignore`）。

若指定了 `<檔名>`，則只處理該檔案。

### 2. 分類與比對

對每個檔案：

a. 讀取內容與 frontmatter（來源、作者、日期、tags）
b. 依 frontmatter `type` 或內容判斷應歸類的知識類型（person / event / concept / place / work）
c. 比對 `wiki/` 下現有頁面，判斷是否重複（比對 title、檔案名稱、aliases）

### 3. 新建或補充

- **無重複**：依照對應範本格式建立新頁面，保留原始 frontmatter 中的來源、作者、日期等 metadata
- **有重複**：不覆蓋，將原始素材內容以 `> [!补充]` callout 附加到現有頁面底部

### 4. 歸檔與更新

a. 將原始檔案從 `inbox/` 移至 `archive/`
b. 新增對應條目到 `wiki/index.md`
c. Append 記錄到 `wiki/changelog.md`

## Output

- **路徑**: 直接在 `wiki/` 下建立或更新頁面
- **報告**: 完成後於 terminal 輸出摘要（新建 n 頁、補充 n 頁、歸檔 n 檔）
