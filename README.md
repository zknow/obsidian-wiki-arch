# Obsidian LLM Wiki

一個由 AI 協助維護的 Obsidian 知識庫。將零散的原始素材丟進 `inbox/`，AI agent 會自動整理成結構化、互相連結的 wiki 筆記。

## 目錄架構

```
root/
├── inbox/          ← 原始素材暫存區（你放檔案的地方）
├── archive/        ← 處理完的素材歸檔
├── garden/         ← 未成熟的知識幼苗（由 garden job 灌溉、採收）
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
│   ├── skills/         ← skill 安裝清冊（見 skills/README.md）
│   └── jobs/           ← 自動化作業定義（report / idea / garden / inbox / init / lint / distill）
├── attachments/    ← 圖片、PDF 等嵌入檔案
└── outbox/         ← AI 自動產出
    ├── reports/
    ├── ideas/
    └── distill/
```

## 六種知識類型

每一則筆記屬於以下五種類型之一，範本統一只需填 `title` / `aliases` / `type` / `tags`：

| 類型 | 適用主題 | 範本 |
|---|---|---|
| Person | 人物、角色、組織創辦人 | `person-template.md` |
| Event | 歷史事件、活動、發布會、戰役 | `event-template.md` |
| Concept | 理論、技術名詞、思想、方法論 | `concept-template.md` |
| Place | 國家、城市、景點、建築 | `place-template.md` |
| Work | 書籍、電影、產品、論文、藝術品 | `work-template.md` |
| Garden | 未成熟的知識幼苗（灌溉中） | `garden-template.md` |

## 建議安裝的 Agent Skill

本專案使用以下 skills 來輔助特定任務。Skills 不納入版本控制，需自行安裝（詳見 `.agents/skills/README.md`）：

| Skill | 用途 | 安裝指令 |
|-------|------|---------|
| `obsidian-markdown` | Obsidian Flavored Markdown 語法規範 | `npx skills add kepano/obsidian-skills --yes --skill obsidian-markdown` |
| `beautiful-article` | 將素材渲染為單檔 HTML 網頁文章（distill job 使用） | `npx skills add ConardLi/garden-skills --yes --skill beautiful-article` |

## 核心工作流程

```
1. 放素材到 inbox/
2. 對 AI agent 說：「幫我把 inbox 中的資料全部匯入」
3. Agent 會：
   ├── 讀取並消化內容
   ├── 若內容充足 → 在 wiki/ 下建立或更新頁面
   ├── 若內容不足 → 在 garden/ 建立 seedling
   ├── 將原始檔移至 archive/
   ├── 更新 index.md 目錄
   └── 記錄到 changelog.md
4. 透過 run garden 灌溉 garden/ 幼苗
5. 成熟後透過 run garden --harvest 採收到 wiki/

## Jobs 自動化作業

本專案支援 7 種自動化作業，完整說明請見 [`.agents/jobs/README.md`](.agents/jobs/README.md)。

基本用法：

```
run report              ← 彙整報告（預設過去一週）
run report 過去一個月   ← 自訂時間範圍
run idea                ← Side-project 構想
run inbox               ← 匯入 inbox 素材到 wiki
run lint                ← 健康檢查（機械 + 語意 + 碰撞補強）
run garden              ← 數位花園照顧（灌溉 seedling + sprout）
run garden --water      ← 只灌溉 seedling
run garden --status     ← 列出花園狀態
run garden --harvest    ← 採收 evergreen 到 wiki
run distill             ← 知識蒸餾（深度分析 HTML 文章）
run init                ← 知識庫初始化／自我修復
```

## 常用操作範例

直接對 AI agent 說這些話即可：

```
# 匯入素材
run inbox

# 提問
「機器學習是什麼？請根據 wiki 中的內容回答」

# 跑報告
run report 過去兩週

# 產出 idea
run idea 教育科技

# 健康檢查
run lint

# 花園照顧（灌溉、狀態、採收）
run garden
run garden --water      ← 只灌溉 seedling
run garden --status
run garden --harvest

# 知識蒸餾
run distill               ← 自動推薦主題
run distill 機器學習       ← 指定主題

# 知識庫初始化
run init --fix

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
