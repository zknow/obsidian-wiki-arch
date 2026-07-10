---
job: init
---

## Trigger

```
run init              ← 掃描並報告缺失
run init --fix        ← 自動補上遺漏的目錄與檔案
run init --h          ← 顯示此說明
```

## Purpose

初始化或修復知識庫的目錄結構與必備檔案。適用於全新 clone 專案後第一次設定，或檔案意外遺失時的自救機制。

## Input

- vault 根目錄結構
- `.agents/jobs/` 下的標準 job 定義（作為比對基準）
- `templates/` 下的標準範本（作為比對基準）

## Steps

### Check 1 — 目錄結構

確保以下目錄存在：

```
inbox/
archive/
attachments/
templates/
wiki/
wiki/people/
wiki/events/
wiki/concepts/
wiki/places/
wiki/works/
garden/
outbox/
outbox/reports/
outbox/ideas/
.agents/
.agents/jobs/
```

### Check 2 — 必備檔案

確保以下檔案存在：

```
wiki/index.md
wiki/changelog.md
README.md
AGENTS.md
.gitignore
templates/person-template.md
templates/event-template.md
templates/concept-template.md
templates/place-template.md
templates/work-template.md
.agents/jobs/README.md
.agents/jobs/report.md
.agents/jobs/idea.md
.agents/jobs/lint.md
.agents/jobs/garden.md
.agents/jobs/inbox.md
.agents/jobs/init.md
```

若 `--fix`，對所有缺失的目錄與檔案直接建立：
- 目錄 → `New-Item -ItemType Directory`
- 檔案 → 從內建標準內容重建（如空的 changelog.md、基本 index.md 結構、`.gitignore` 模式等）

## Output

- **報告**: 完成後於 terminal 輸出摘要（檢查 n 項、遺漏 n 項、已修復 n 項）
- `--fix` 模式下含已建立的目錄與檔案清單
