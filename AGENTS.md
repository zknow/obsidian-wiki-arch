# 關於這個知識庫

這是一個通用的知識庫，你的任務是將零散的原始素材整理成一套彼此連結、好查閱的筆記。

## 資料夾與檔案角色

- **inbox/** — 原始素材暫存區。你可以讀取這裡的檔案，但不要直接修改。
- **archive/** — 原始素材處理完後的歸檔位置，用於保存紀錄。
- **garden/** — 未成熟的知識概念幼苗存放處，由 garden job 灌溉與採收後移至 wiki。
- **wiki/** — 你建立、更新和維護筆記的地方。採用扁平結構，靠 `index.md` 和 `[[wiki 連結]]` 來組織。
  - **wiki/people/** — 人物筆記。
  - **wiki/events/** — 事件筆記。
  - **wiki/concepts/** — 概念、理論、技術名詞筆記。
  - **wiki/places/** — 地點、國家、城市、景點筆記。
  - **wiki/works/** — 書籍、文章、電影、產品、研究論文等作品筆記。
- **outbox/** — Jobs 自動化產出（報告、idea、碰撞分析、蒸餾等）。
  - **outbox/reports/** — 彙整報告產出。
  - **outbox/ideas/** — Idea / Side-project 構想產出。
  - **outbox/distill/** — 知識蒸餾深度分析產出。
- **attachments/** — 圖片、PDF 等嵌入檔案的統一存放位置。
- **templates/** — 可重複使用的筆記範本。
  - `person-template.md` — 人物頁面範本。
  - `event-template.md` — 事件頁面範本。
  - `concept-template.md` — 概念頁面範本。
  - `place-template.md` — 地點頁面範本。
  - `work-template.md` — 作品頁面範本。

- **wiki/index.md** — 知識庫的目錄大綱。知識庫中的所有頁面都應在此列出，附上一句話說明。
  - 格式：`[[頁面名稱]] — 一句話說明。`
  - 範例：`[[機器學習]] — 一種讓電腦從資料中學習的技術。`

- **wiki/changelog.md** — 記錄每一次更新。請在檔案最下方新增記錄。
  - 格式：`## [YYYY-MM-DD] 動作 | 說明`
  - 範例：`## [2026-07-09] 匯入 | 機器學習基礎觀念`
  - 每次匯入完成後，務必登記所有處理過的檔案名稱，避免重複匯入。

## Obsidian 操作須知

你正處於一個 **Obsidian vault** 之中。所有 wiki 筆記必須使用 Obsidian Flavored Markdown 撰寫，詳細語法請參考 `.agents/skills/obsidian-markdown/` 中的完整規範（含 `[[wikilinks]]`、Front Matter 屬性、`> [!callouts]`、`![[embeds]]`、標籤、註解等）。

### 基本規則

- **不要修改 `.obsidian/` 目錄** — 這個目錄存放 Obsidian 的設定與外掛，任何修改都可能導致設定錯亂。
- **檔案名稱即頁面標題** — 筆記的檔案名稱（不含 `.md`）會成為 Obsidian 中的頁面名稱。允許使用空格、中文、英文。
- **附件的嵌入** — 如果有圖片等嵌入檔案，請放在 `attachments/` 目錄，並使用 `![[檔名.png]]` 語法嵌入到筆記中。
- **所有操作都在 vault 目錄內進行** — 不要讀取或寫入 vault 目錄以外的任何檔案。
- **寫入後無需手動觸發同步** — Obsidian 會自動偵測檔案變化並更新圖譜檢視與反向連結面板。

## 檔案操作權限

以下表格定義你對各目錄與檔案的 CRUD 權限，所有操作須嚴格遵守。

| 路徑 | 讀取 | 寫入 | 刪除 | 說明 |
|------|------|------|------|------|
| `inbox/` | ✅ | ❌ | ❌ | 僅讀取素材 |
| `archive/` | ❌ | ✅ | ❌ | 僅移入歸檔 |
| `garden/` | ✅ | ✅ | ✅ | 灌溉、採收全流程 |
| `wiki/**/*.md` | ✅ | ✅ | ❌ | 建立與更新，不刪除 |
| `wiki/index.md` | ✅ | ✅ (append) | ❌ | 僅在頁面新增/移動時更新條目 |
| `wiki/changelog.md` | ✅ | ✅ (append) | ❌ | 僅在底部新增記錄 |
| `templates/` | ✅ | ❌ | ❌ | 唯讀 |
| `outbox/` | ✅ | ✅ | ✅ | Jobs 產出完全管理 |


| `attachments/` | ✅ | ✅ | ❌ | 可新增，不刪除 |
| `.obsidian/` | ❌ | ❌ | ❌ | 完全禁止 |
| `.agents/` | ✅ | ✅ | ✅ | 技能與 Job 全權管理 |
| `AGENTS.md` | ✅ | ❌ | ❌ | 用戶明確要求才改 |
| `README.md` | ✅ | ❌ | ❌ | 用戶明確要求才改 |
| `.gitignore` | ✅ | ❌ | ❌ | 用戶明確要求才改 |

> **匯入流程例外**：`run inbox` 執行時，允許將檔案從 `inbox/` 移動到 `archive/`（讀取 inbox → 寫入 archive → 清除 inbox 中的原始檔案）。此為唯一允許跨目錄刪除的流程。

## 已安裝的 Skill 使用指引

本專案已安裝以下 Obsidian 專用 skill，你應在對應情境中使用它：

### obsidian-markdown

- **位置**: `.agents/skills/obsidian-markdown/SKILL.md`
- **用途**: 所有 wiki 筆記的建立與編輯都必須遵循此 skill 的規範，包含 `[[wikilinks]]`、Front Matter 屬性、`> [!callouts]`、`![[embeds]]`、標籤、註解等語法。
- **參考文件**:
  - `references/PROPERTIES.md` — 所有屬性類型
  - `references/CALLOUTS.md` — 所有 callout 類型
  - `references/EMBEDS.md` — 所有嵌入類型

### Skill 不足時的處理

當任務需要但你身上未載入對應的 skill 時，先查閱 `.agents/skills/README.md` 確認是否有適用的 skill。若找到，列出安裝方式給用戶，詢問是否安裝後重試。若用戶拒絕或該 skill 不支援當前 agent，則繞過 skill 以常規方式執行任務。

## Tag 使用規範

Frontmatter 中的 `tags` 欄位用於多維度篩選與檢索。建議遵循以下原則：

- **領域標記**：標示所屬領域，如 `#machine-learning`、`#history`、`#biology`
- **主題標記**：標示具體主題，如 `#neural-network`、`#democracy`
- **狀態標記**（可選）：`#draft` / `#finished` / `#needs-review`

## 資料匯入與整理規則

1. 掃描 `inbox/` 資料夾，確認是否有新的檔案需要處理。
2. 讀取每一個新檔案，消化內容後，在 `wiki/people/`、`wiki/events/`、`wiki/concepts/`、`wiki/places/`、`wiki/works/` 中建立或更新對應的頁面，或在 `garden/` 中建立未成熟的知識幼苗。
3. 處理完成後，**將原始檔案從 `inbox/` 移動到 `archive/`** 保存。
4. 建立或更新頁面時，請遵循對應的範本格式（`person-template.md`、`event-template.md`、`concept-template.md`、`place-template.md` 或 `work-template.md`）。
5. 每個新頁面應在**正文內容**中自然地使用 `[[wiki 連結]]`，僅連結**确实相關**的頁面。有效關聯僅限以下類型（至少符合一項）：
    - **創作關係**：A 創作了 B、A 是 B 的作者
    - **依賴／擴充關係**：B 依賴 A 才能運作、B 是 A 的擴充或插件
    - **主題歸屬**：A 是 B 的核心概念或技術基礎
    - **因果／影響**：A 直接影響了 B 的發展方向

    以下情況**不構成有效關聯**，禁止建立連結：
    - A 在 B 的教學中被當作設定範例（除非教學本身是主題）
    - A 與 B 在同一篇文章中被並列提及但無直接互動
    - A 與 B 屬於同一類別但無直接關係

    添加任何 `[[wikilink]]` 前，問自己：「如果讀者從當前頁面跳到目標頁面，目標頁面的內容合理出現在當前脈絡中嗎？」答案是否定的話就移除。

    禁止在 Related Pages 區塊或在正文中硬塞無關連結。真的沒有相關頁面時，可以接受暫時沒有連結，也比錯誤連結好。任何頁面的品質與成熟度不應以 `[[wiki 連結]]` 數量衡量。連結是探索工具，不是評分指標。
6. 如果新素材與已有的人物、事件、概念、地點或作品相關，請更新現有頁面，不要重複建立。
7. 如果新素材中出現了重要的新人物、事件、概念、地點或作品，才建立新的頁面。若素材內容不足以構成完整的 wiki 頁面（例如僅為邊緣提及或簡短觀察），則應在 `garden/` 中建立 seedling 頁面，待後續灌溉。
8. 撰寫時請使用流暢的白話風格，避免文言文或艱澀詞彙。
9. 中文繁簡處理：原始素材可能為簡體中文，但 wiki 中的 `title` 與 `aliases`
   **一律使用繁體中文**。簡體轉繁體後再作為 alias 寫入，確保 `[[wikilink]]`
   解析一致。
10. 每次資料整理完成後，必須執行以下兩個任務：
    - 更新 `wiki/index.md` 以反映知識庫的最新內容。
    - 在 `wiki/changelog.md` 最下方新增一筆記錄，登記所有處理過的檔案名稱。

## 回答提問的要點

1. 當有人提出問題時，請先查閱 `wiki/index.md` 來定位相關頁面。
2. 閱讀那些頁面的內容，然後彙整出答案。
3. 回覆時請清楚標明你引用了哪些頁面的資訊，讓對方知道答案的依據來源。
4. 如果對話中有值得保留的見解，可以建議儲存到 wiki 中 — 但儲存前務必先詢問。

## 知識庫維護檢查清單

當有人要求你進行維護時，請執行以下檢查：

- 檢查是否有失效的 `[[wiki 連結]]`。
- 檢查是否有孤立頁面（沒有被任何其他頁面連結到的頁面）。
- 檢查是否有重複或高度相似的頁面，並提出合併建議。
- 檢查頁面之間是否有內容矛盾或不一致的地方。
- 完成後輸出一份簡短的報告。

## Jobs 觸發指令

本專案支援以下自動化作業（jobs），輸入對應指令即可觸發。詳細步驟定義在 `.agents/jobs/<name>.md` 中。

時間參數規則：優先讀取 `--since`、`--from`、`--to` 等 flags；無 flags 時以自然語言解析；完全無參數時使用預設值。

- `run report [時間範圍]` — 產生知識庫彙整報告（預設過去一週），產出至 `outbox/reports/`
- `run idea [主題提示]` — 從既有知識中提煉 side-project 構想，產出至 `outbox/ideas/`
- `run inbox` — 匯入 inbox 素材到 wiki/
- `run lint` — 健康檢查（失效連結、孤立頁面、矛盾內容等）
- `run init` — 知識庫初始化／自我修復
- `run garden` — 灌溉 garden/ 中的知識幼苗（灌溉所有 seedling + sprout）
- `run garden --water` — 只灌溉 seedling 頁面
- `run garden --status` — 列出花園狀態
- `run garden --harvest` — 採收 evergreen 到 wiki/
- `run distill` — 從 wiki 蒸餾深度分析 HTML 文章（自動推薦主題）
- `run distill [主題]` — 指定主題蒸餾
