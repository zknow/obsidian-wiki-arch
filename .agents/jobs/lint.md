---
job: lint
---

## Trigger

`run lint`

單一指令，無需額外參數。支援 `--h` 顯示用法說明。

```
run lint        ← 執行全部檢查（機械 + 語意 + 碰撞補強）
run lint --h    ← 顯示此說明
```

## Purpose

對 wiki 進行完整健康檢查與連結補強。一次執行三個階段：機械檢查（失效連結、孤立頁面、錯置檔案等）、語意檢查（矛盾內容、交叉引用缺口等）、碰撞補強（找遺漏的關聯配對並自動補上連結）。產出報告至 `outbox/reports/`。

## Input

- `wiki/` 下所有筆記頁面（含 people / events / concepts / places / works 子資料夾）
- `wiki/index.md` — 目錄大綱
- `wiki/changelog.md` — 更新日誌

## Steps

### Pass 1 — 機械檢查

```
M1. 失效連結 — grep 所有 [[wikilinks]]，對照實際存在的檔案路徑
M2. 孤立頁面 — 計算每個頁面的反向連結數（來自其他頁面的 [[連結]]）
M3. 錯置檔案 — 讀取 frontmatter type，比對所在資料夾是否匹配
    type: person → wiki/people/
    type: event   → wiki/events/
    type: concept → wiki/concepts/
    type: place   → wiki/places/
    type: work    → wiki/works/
M4. 缺少 frontmatter — 檢查每個頁面是否有 title / type / tags 欄位
M5. 重複標題 — 列出所有檔名（不含路徑），找出同名者
M6. 空知識資料夾 — 檢查 people/events/concepts/places/works/
    有無任何 .md（排除 .gitkeep/.gitignore）
M7. 更新間隔過長 — 讀取 changelog.md 最後一筆日期，與今天相差天數
    （預設寬限期 14 天）
M8. 索引漂移 — 比對 index.md 中的 [[條目]] 與實際 wiki/ 下的 .md 檔案
```

### Pass 2 — 語意檢查

```
S1. 矛盾內容 — 掃描近期更新的頁面，比對相關頁面有無說法衝突
S2. 缺乏專頁的概念 — grep 純文字名詞在 3+ 頁面出現但無 [[wikilink]]
S3. 交叉引用缺口 — 頁面正文中提到的實體/人物未被 wikilink
S4. 過時主張 — 老舊頁面中是否有被新來源取代的舊主張
```

### Pass 3 — 碰撞補強

```
1. 掃描 wiki/ 中所有頁面的內容與 tags
2. 找出有潛在關聯但尚無 [[連結]] 的頁面對
   - 比對 tags、同名關鍵字、互補的內容主題
3. 逐一確認配對是否合理（禁止硬塞無關連結）
4. 對合理的配對：
   a. 在雙方的 Related Pages 區段補上 [[連結]]
   b. 如果可行，在內文適當位置補上嵌入連結
```

### Pass 4 — 報告產出

將 Pass 1 至 Pass 3 的結果依嚴重度分組彙整，輸出至 `outbox/reports/`。

## Output

- **路徑**: `outbox/reports/lint-YYYY-MM-DD.md`
- **格式**:
  - 標題與摘要統計（總頁數、問題數、補強連結數）
  - Error 區段（錯置檔案、重複標題等）
  - Warning 區段（孤立頁面、缺少 frontmatter、索引漂移等）
  - Info 區段（空資料夾、缺乏專頁的概念建議等）
  - 碰撞補強紀錄（新增了哪些連結到哪些頁面）
  - 建議行動一覽
