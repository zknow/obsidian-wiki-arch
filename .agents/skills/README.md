# Skills

本目錄存放本專案使用到的 agent skills。Skills 不納入版本控制，clone 專案後需自行安裝。

## 推薦 Skills

| Skill | 來源 | 用途 |
|-------|------|------|
| `beautiful-article` | [ConardLi/garden-skills](https://github.com/ConardLi/garden-skills) | 將素材渲染為單檔 HTML 網頁文章 |
| `obsidian-markdown` | [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) | Obsidian Flavored Markdown 語法規範 |

## 安裝方式

不同 agent 有不同的 skill 安裝機制：

- **opencode**: `npx opencode skills add <repo> --yes --skill <name>`
- **Claude Code**: 依其 skill 管理機制安裝
- **其他 agent**: 將 skill 原始碼下載至 `./.agents/skills/<name>/` 目錄

也可使用 `find-skills` 內建功能搜尋適合的 skill。
