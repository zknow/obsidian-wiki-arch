---
job: garden
---

## Trigger

```
run garden           ← 完整花園照顧
run garden --water   ← 只處理 seedling 頁面
run garden --h       ← 顯示此說明
```

## Purpose

對 wiki 頁面進行成熟度分級並給出養護建議。讓筆記從 seed（種子）持續成長為 evergreen（常青），避免半途而廢的內容沈底。

## Input

- `wiki/` 下所有筆記頁面（含子資料夾）

## Steps

### Pass 1 — 成熟度評估

讀取每個 wiki 頁面的內容長度、連結數、區段完整性，給出分級並寫入 frontmatter `maturity` 欄位：

| 分級 | 判斷條件 |
|---|---|
| `seedling` | 內容少於 100 字、或僅有標題大綱、或僅一個段落 |
| `sprout` | 有基本內容、至少 2 個 `[[連結]]`、涵蓋範本大部分區段 |
| `evergreen` | 內容完整、有引用來源、無 TODO/FIXME 殘留 |

若該頁面尚無 `maturity` 欄位則自動補上，已有則更新。

### Pass 2 — 澆水建議

依當前分級給出下一步行動：

- **seedling** → 對照對應範本，建議補上缺少的區塊
- **sprout** → 建議可延伸的連結方向與可補充的內容
- **evergreen** → 若超過 90 天未更新，提醒覆查是否過時

`--water` 模式時僅處理 seedling 頁面。

## Output

- **路徑**: `outbox/reports/garden-YYYY-MM-DD.md`
- **格式**:
  - 摘要統計（各分級數量）
  - 每個頁面的當前分級與建議行動
  - 修改的檔案一覽
