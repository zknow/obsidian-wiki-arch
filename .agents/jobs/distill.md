---
job: distill
---

## Trigger

```
run distill              ← 掃描 wiki 自動推薦主題
run distill [主題]        ← 指定主題
run distill --h          ← 顯示此說明
```

## Purpose

從 wiki 知識庫中提取相關頁面，進行深度交叉分析，蒸餾出結構化的學習總結，並透過 beautiful-article skill 產生可分享的單檔 HTML 文章。

## Output

- **路徑**: `outbox/distill/YYYY-MM-DD-<topic>.html`
- **格式**: 單檔 HTML 文章（beautiful-article 渲染）

## Steps

### Phase 1 — 主題選擇

**無指定主題時：**
1. 掃描 `wiki/` 下所有頁面
2. 分析連結圖譜，找出知識簇最密集的 3-5 個主題
3. 使用 Question tool 顯示選項，讓用戶選擇一個主題
4. 若用戶取消選擇則終止

**有指定主題時：**
1. 依主題搜尋 `wiki/`，找出所有相關頁面
2. 若未找到任何相關頁面，回報「未找到相關頁面，請嘗試其他主題」並終止

### Phase 2 — 深度分析

讀取所有相關頁面，提取：

- **核心概念** — 每個頁面的關鍵論點
- **關聯分析** — 頁面之間的連結脈絡與互補關係
- **矛盾與分歧** — 不同頁面之間觀點衝突或資訊不一致處
- **知識缺口** — 現有筆記尚未涵蓋的重要面向
- **延伸提問** — 從既有知識出發可繼續探索的方向

### Phase 3 — 產出

1. 將分析結果組織成結構化 markdown
2. 載入 beautiful-article skill，渲染為單檔 HTML
3. 若 beautiful-article 流程失敗，fallback 產出 markdown 至 `outbox/distill/`
4. 輸出至 `outbox/distill/YYYY-MM-DD-<topic>.html`

### Boundary Cases

| 情境 | 行為 |
|------|------|
| wiki 無任何頁面 | 回報「知識庫無內容可蒸餾」 |
| 指定主題找不到相關頁面 | 回報「未找到相關頁面，請嘗試其他主題」 |
| beautiful-article 流程失敗 | fallback 產出 markdown |
| 多主題時用戶取消選擇 | 終止不產出 |
