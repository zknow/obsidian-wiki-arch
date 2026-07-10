---
job: garden
---

## Trigger

```
run garden              完整花園照顧（灌溉所有 seedling + sprout）
run garden --water      只灌溉 seedling
run garden --status     列出花園狀態（含一句建議）
run garden --harvest    採收 evergreen → wiki
run garden --h          顯示此說明
```

## Purpose

管理 `garden/` 目錄中的知識幼苗，透過 inbox 素材查閱與 web 研究來灌溉，使其成長為可採收的 evergreen 筆記。

## Directory

- **`garden/`**: 存放未成熟的知識概念筆記，使用 `templates/garden-template.md` 格式
- **`templates/garden-template.md`**: garden 筆記範本，內含成熟度檢查清單

## Maturity Levels

成熟度由 garden-template 中「檢查清單」的區塊完成度決定，**與連結數量完全脫鉤**。

| 分級 | 條件 |
|------|------|
| `seedling` | 僅完成「概述」，其餘區塊空白或有 TODO |
| `sprout` | 完成「概述」+「核心論點」+ 至少一個其他區塊 |
| `evergreen` | 概述 + 核心論點 + 詳細內容 + 應用案例 + 參考來源 完整無 TODO（關聯頁面不計入） |

## Steps

### Pass 0 — 狀態總覽 (`--status`)

列出 `garden/` 下所有頁面及其成熟度，附各區塊完成狀況。

輸出格式：
```
🌱 花園狀態 (YYYY-MM-DD)

seedling  (N)
  - [[頁面A]]   → 缺少：核心論點、詳細內容...
sprout    (N)
  - [[頁面B]]   → 缺少：應用案例...
evergreen (N)
  - [[頁面C]]   → 可 harvest

💡 建議：...
```

### Pass 1 — 灌溉 (`garden` / `garden --water`)

對每個目標頁面（`--water` 時只處理 seedling）：

1. **掃描 inbox** — 檢查 `inbox/` 有無未處理素材可補充當前概念
2. **Web 搜尋** — 若 inbox 無相關資料，依權重搜尋可信來源：
   官方文件 > GitHub > 學術論文 > 技術文章 > 技術部落格
3. **填入對應區塊** — 將找到的內容寫入 template 的對應區塊
4. **更新成熟度** — 重新計算檢查清單完成度
5. **可採收標記** — 若達到 evergreen，在報告中標示

### Pass 2 — 採收 (`--harvest`)

對每個 `evergreen` 頁面：

1. **確認完整性** — 所有區塊完整、有參考來源、無 TODO
2. **轉換類型** — frontmatter 的 `type: garden` 改為對應類型（根據內容判斷為 concept / work / event / person / place）
3. **清理 tags** — 移除 `tags` 中的 `seedling` / `sprout` / `evergreen`
4. **搬移檔案** — 直接移動到 `wiki/<type>/`（不經 archive）
5. **更新索引** — 更新 `wiki/index.md`（新增條目）
6. **更新日誌** — 更新 `wiki/changelog.md`（記錄採收）

### Pass 3 — 說明 (`--h`)

顯示此文件內容。

## Output

- **`garden --status`**: 直接輸出至終端
- **`garden` / `garden --water`**: 產出報告至 `outbox/reports/garden-YYYY-MM-DD.md`
- **`garden --harvest`**: 直接移動檔案，更新 `wiki/index.md` + `wiki/changelog.md`
