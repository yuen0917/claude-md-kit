# 分層放置指引:什麼內容放哪裡

原則:每條內容放在「最貼近它生效範圍」的層級,讓每個 session 只載入當下需要的東西。
同一條規則只存在於一層,不重複。

## 第 1 層:全域(`~/.claude/CLAUDE.md`)

放「跨所有專案都成立」的個人行為準則,例如:

- 先讀再改、改完必驗、最小改動
- 遇 blocker 就停並浮現讓人決定;不確定就查證,不編造
- 破壞性或不可逆操作先確認
- 回覆語言等個人偏好

放進全域後,**各專案的 CLAUDE.md 不要再重複這些**——重複是最常見的 context 浪費。

## 第 2 層:專案根目錄(`<repo>/CLAUDE.md`)

只放專案專屬、且幾乎每次工作都會用到的內容(即範本的六個區塊:
描述、環境、驗證指令、架構地圖、慣例陷阱、狀態、邊界)。60–80 行以內。

- 入版控,團隊共享。
- 純個人的偏好差異放 `CLAUDE.local.md`(加入 `.gitignore`)。

## 第 3 層:子目錄 CLAUDE.md

大型 codebase 中,子系統專屬規則放該子目錄的 CLAUDE.md,
**只在 agent 於該目錄工作時才載入**,不佔其他任務的 context。

- `frontend/CLAUDE.md` — 元件結構、狀態管理慣例
- `infra/CLAUDE.md` — 部署流程、環境對應表

## 第 4 層:路徑作用域規則(`.claude/rules/*.md`)

只對特定檔案類型或路徑生效的規則,用 rules 檔搭配 glob frontmatter:

```markdown
---
globs: ["migrations/**/*.sql"]
---
所有 migration 必須可回滾,並附對應的 down script。
```

適合:SQL 規範、測試檔慣例、特定框架檔案的模式等「檔案類型綁定」的規則。

## 第 5 層:按需閱讀的文件(`docs/`)

架構細節、API 規格、ER 圖、決策記錄(ADR)等大型文件放 `docs/`,
在 CLAUDE.md 裡只寫一行「**何時**該讀**哪份**」,例如:

> 需要動資料模型時,先讀 `docs/ARCHITECTURE.md` 的 ER 圖章節。

不要用 `@` 把整份文件嵌入 CLAUDE.md——那會讓它在每個 session 都吃掉 context,
不管任務是否用得到。

## 快速判斷表

| 內容 | 放哪 |
|---|---|
| 「改完必跑測試」等跨專案準則 | 全域 `~/.claude/CLAUDE.md` |
| 專案的 build / test / lint 指令 | 專案根 CLAUDE.md |
| 只有前端子系統適用的慣例 | `frontend/CLAUDE.md` |
| 只有 `*.sql` 檔適用的規則 | `.claude/rules/` + glob |
| 完整架構文件、API 規格 | `docs/`,按需讀 |
| 個人偏好(不想入版控) | `CLAUDE.local.md` |
| API key、憑證 | 環境變數;**永遠不放以上任何一處** |
