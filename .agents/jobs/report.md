---
job: report
---

## Trigger

`run report [時間範圍]`

### 時間參數規則

1. 優先解析 `--since`、`--from`、`--to` 等 flags（如 `run report --since 30d`）
2. 無 flags 時以自然語言解析（如 `run report 過去一個月`、`run report 2026-06-01~2026-07-01`）
3. 完全無參數時，預設時間範圍為過去 7 天

## Purpose

掃描 `wiki/changelog.md`，篩選指定時間區間內的新增與變更記錄，整理成結構化的彙整報告。

## Input

- `wiki/changelog.md` — 主要的變更記錄來源
- 使用者指定的時間範圍

## Steps

1. 讀取 `wiki/changelog.md`，取得所有記錄
2. 依時間範圍篩選出符合條件的記錄
3. 讀取每條記錄關聯的新增或修改頁面
4. 依 type（person / event / concept / place / work）分類整理
5. 統計摘要：新增頁面數、更新頁面數、涉及的領域
6. 產出結構化的報告

## Output

- **路徑**: `outbox/reports/YYYY-MM-DD-summary.md`
- **格式**:
  - 報告標題與時間範圍
  - 各類型的變更清單（含 [[連結]] 與一句話說明）
  - 統計摘要
