# Project State

> 最後更新:2026-07-09

## 目前目標 / 里程碑

套件已 plugin 化(claude-md-kit),待 push 後在其他專案實際安裝試用,依回饋修訂 skills 與範本。

## 進行中

- plugin 尚未在其他機器/專案驗證安裝流程(`/plugin marketplace add yuen0917/claude-md-kit`)。

## 已完成(近期,舊的移到 archive)

- 2026-07-09 README 改寫為對外形式:badges、價值主張開場、Quick Start、skills 情境、設計理念、目錄樹。
- 2026-07-09 repo plugin 化:`.claude-plugin/`(plugin.json + marketplace.json)+ 三個 skills(claude-md-apply / check / slim),README 與 CLAUDE.md 連動更新。
- 2026-07-09 補套件自身的 `docs/STATE.md`(dogfooding 跨 session 狀態機制)。
- 2026-07-03 檔案整理為 templates/ guides/ examples/ docs/ 四資料夾。
- 2026-07-03 加入分層範例(global-claude、rules)、STATE 範本、維護迴圈與 repo 衛生守則。
- 2026-07-03 初版:CLAUDE.template.md、WORKFLOW、PLACEMENT_GUIDE、CHECKLIST、兩份套用範例。

## 關鍵決策記錄

| 日期 | 決策 | 理由 |
|---|---|---|
| 2026-07-09 | 本 repo 直接兼作 plugin(marketplace `source: "./"`),plugin.json 不設 `version` | 單一 repo 免同步兩份範本;省略 version 則每次 commit 即新版本,適合迭代期 |
| 2026-07-09 | 不在本 repo 建實際 `.claude/rules/` 目錄,rules 示範只放 `examples/rules.md` | 真建會被 Claude Code 當成本 repo 生效設定載入,與「範例勿命名 CLAUDE.md」同一類陷阱 |
| 2026-07-03 | 範例檔不命名為 `CLAUDE.md` 放子資料夾 | 會被 Claude Code 當成生效設定載入 |
| 2026-07-03 | 成品行數上限訂 60–80 行 | 過長會被 agent 忽略;每行須通過「刪掉會不會出錯」測試 |

## 已知問題 / 陷阱

- 核心文件連動:改範本區塊結構時,`examples/` 兩份範例與 `guides/CHECKLIST.md` 必須同步。
- `docs/fable5_claude_md_prompt.md` 唯讀,勿修改。

## 下一步

1. push 後在另一台機器/專案跑 `/plugin marketplace add yuen0917/claude-md-kit` + `/plugin install claude-md-kit@claude-md-templates`,驗證三個 skills 可用。
2. 在真實新專案用 `/claude-md-apply` 套用一次,回收「填寫時卡住的點」修訂範本註解與 skill 步驟。
