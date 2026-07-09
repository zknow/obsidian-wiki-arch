---
job: idea
---

## Trigger

`run idea [主題提示]`

- 可選主題提示，如 `run idea 量子計算`、`run idea 教育科技`
- 無提示時隨機選取

## Purpose

從知識庫中挑選不同類型或領域的頁面，尋找跨域交會點，提煉出具體的 side-project 構想或研究假說。

## Input

- `wiki/` 下所有頁面（含 people / events / concepts / places / works）
- 如果有主題提示，優先篩選相關頁面

## Steps

1. 從 `wiki/` 中選取 2-3 個不同類型或領域的頁面
2. 閱讀各頁面內容，理解核心概念
3. 分析這些頁面之間潛在的連結點、衝突點或互補關係
4. 提出 1-3 個具體的構想，每個構想包含：
   - 概念名稱
   - 連結了哪些既有知識（引用頁面）
   - 可能的應用方向或實作方式

## Output

- **路徑**: `outbox/ideas/YYYY-MM-DD-<short-name>.md`
- **格式**:
  - 標題與日期
  - 每個構想的詳細描述
  - 參考資料清單（引用 wiki 頁面）
