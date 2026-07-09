# Jobs 框架

每個 job 是一個 `.md` 檔案，定義一個可由觸發指令啟動的自動化作業。

## 共用結構

| 區段 | 說明 |
|---|---|
| Trigger | 觸發關鍵字與參數格式 |
| Purpose | 這個 job 的目標 |
| Input | 需要讀取的檔案或資料來源 |
| Steps | 執行的具體步驟（依序執行） |
| Output | 產出物的格式與存放位置 |

## 觸發方式

所有 job 透過 AGENTS.md 中定義的關鍵字觸發。使用者輸入對應指令後，agent 讀取對應的 job 檔案並依步驟執行。

## 現有 Jobs

- [[.agents/jobs/report.md]] — 彙整報告
- [[.agents/jobs/idea.md]] — Idea / Side-project 產出
- [[.agents/jobs/lint.md]] — Wiki 健康檢查（機械 + 語意 + 碰撞補強）
- [[.agents/jobs/garden.md]] — 數位花園照顧（成熟度分級與養護建議）
- [[.agents/jobs/inbox.md]] — 素材匯入自動化
