---
job: collide
---

## Trigger

`run collide`

無需額外參數。

## Purpose

隨機找出知識庫中缺乏直接連結但內容上應有關聯的頁面對，補強跨域連結，讓知識網絡更完整。

## Input

- `wiki/` 下所有頁面

## Steps

1. 掃描 `wiki/` 中所有頁面（含 people / events / concepts / places / works）
2. 識別有潛在關聯但尚無 `[[連結]]` 的頁面對
   - 比對 tags、同名關鍵字、互補的內容主題
3. 對每一組潛在連結進行分析，判斷是否合理
4. 對確認合理的配對：
   a. 在雙方的 Related Pages 區段補上 `[[連結]]`
   b. 如果可行，在內文適當位置補上嵌入連結
5. 產出變更摘要

## Output

- **路徑**: `outbox/collisions/YYYY-MM-DD-link-report.md`
- **格式**:
  - 新增的連結清單（`來源頁面 → 目標頁面`）
  - 修改的檔案路徑一覽
- 同時**直接修改** `wiki/` 下的對應頁面
