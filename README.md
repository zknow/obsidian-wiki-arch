# Obsidian LLM Wiki

一個由 AI 協助維護的 Obsidian 知識庫。將零散的原始素材丟進 `inbox/`，AI agent 會自動整理成結構化、互相連結的 wiki 筆記。

## 目錄架構

```
root/
├── inbox/          ← 原始素材暫存區（你放檔案的地方）
├── archive/        ← 處理完的素材歸檔
├── wiki/           ← 知識庫本體（AI 維護）
│   ├── index.md    ← 目錄大綱，列出所有頁面
│   ├── changelog.md ← 更新日誌
│   ├── people/
│   ├── events/
│   ├── concepts/
│   ├── places/
│   └── works/
├── templates/      ← 筆記範本
├── .agents/         ← Agent 設定與自動化
│   ├── skills/obsidian-markdown/  ← Obsidian Markdown 語法規範
│   └── jobs/        ← 自動化作業定義（report / idea / collide）
├── attachments/    ← 圖片、PDF 等嵌入檔案
└── outbox/         ← AI 自動產出
    ├── reports/
    ├── ideas/
    └── collisions/
```

## 五大知識類型

每一則筆記屬於以下五種類型之一，範本統一只需填 `title` / `aliases` / `type` / `tags`：

| 類型 | 適用主題 | 範本 |
|---|---|---|
| Person | 人物、角色、組織創辦人 | `person-template.md` |
| Event | 歷史事件、活動、發布會、戰役 | `event-template.md` |
| Concept | 理論、技術名詞、思想、方法論 | `concept-template.md` |
| Place | 國家、城市、景點、建築 | `place-template.md` |
| Work | 書籍、電影、產品、論文、藝術品 | `work-template.md` |

## 已安裝的 Agent Skill

本專案安裝了 `obsidian-markdown` skill（位於 `.agents/skills/obsidian-markdown/`），負責規範所有筆記的 Obsidian 專屬語法：

> 此 skill 源自 [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)（@kepano），採用其 `skills/obsidian-markdown` 目錄中的規範與參考文件。

- `[[wikilinks]]` — 筆記之間的雙向連結
- Front Matter 屬性 — 頁面中繼資料（`---` 區塊）
- `> [!callouts]` — 重點提示區塊
- `![[embeds]]` — 嵌入圖片、檔案或其他筆記
- 標籤、註解、螢光筆、Mermaid 圖表等

Agent 在建立或編輯任何 `wiki/` 下的 `.md` 檔案時，會自動套用此 skill 的規範。

## 核心工作流程

```
1. 放素材到 inbox/
2. 對 AI agent 說：「幫我把 inbox 中的資料全部匯入」
3. Agent 會：
   ├── 讀取並消化內容
   ├── 在 wiki/ 下建立或更新頁面
   ├── 將原始檔移至 archive/
   ├── 更新 index.md 目錄
   └── 記錄到 changelog.md
```

## Jobs 自動化作業

本專案支援多種自動化作業（彙整報告、idea 產出、隨機碰撞等），完整說明請見 [`.agents/jobs/README.md`](.agents/jobs/README.md)。

基本用法：

```
run report              ← 預設過去一週
run report 過去一個月   ← 自訂時間範圍
```

## 常用操作範例

直接對 AI agent 說這些話即可：

```
# 匯入素材
「幫我把 inbox 中的檔案全部匯入到 wiki」

# 提問
「機器學習是什麼？請根據 wiki 中的內容回答」

# 跑報告
「run report 過去兩週」

# 產出 idea
「run idea 教育科技」

# 隨機碰撞
「run collide」

# 維護檢查
「幫我檢查知識庫中有沒有失效的連結或孤立頁面」
```

## Tag 使用建議

```yaml
---
tags:
  - machine-learning    # 領域標記
  - neural-network      # 主題標記
  - draft               # 狀態標記（draft / finished / needs-review）
---
```

## 需求

- [Obsidian](https://obsidian.md/) — 用於瀏覽與編輯知識庫
- Any AI Agent（如 Codex CLI、Claude Code 等）— 負責執行整理與產出任務

## 快速開始

1. 用 Obsidian 開啟此資料夾（作為 vault）
2. 將想整理的資料放進 `inbox/`
3. 對 AI agent 說：「幫我把 inbox 中的資料全部匯入」
