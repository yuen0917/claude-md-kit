# CLAUDE.md 通用範本套件

可套用於任何專案的 CLAUDE.md 範本與配套 agent workflow。
目標:用最少的 context 換取最可靠的 agent 行為。

## 檔案索引

| 檔案 | 用途 |
|---|---|
| [CLAUDE.template.md](CLAUDE.template.md) | 通用範本:複製到專案根目錄改名 CLAUDE.md,填 placeholder、刪註解 |
| [STATE.template.md](STATE.template.md) | 跨 session 狀態檔範本:複製到專案的 `docs/STATE.md` |
| [WORKFLOW.md](WORKFLOW.md) | Agent 標準流程:定位 → 規劃 → 執行 → 驗證 → 交付,含狀態管理與維護迴圈 |
| [PLACEMENT_GUIDE.md](PLACEMENT_GUIDE.md) | 分層放置指引:什麼內容放全域、專案根、子目錄、rules、docs |
| [GLOBAL_CLAUDE.example.md](GLOBAL_CLAUDE.example.md) | 第 1 層範例:全域 `~/.claude/CLAUDE.md` |
| [RULES_EXAMPLE.md](RULES_EXAMPLE.md) | 第 4 層範例:`.claude/rules/` 路徑作用域規則 |
| [EXAMPLE_CLAUDE.md](EXAMPLE_CLAUDE.md) | 範例一:假想後端專案 BookTrail |
| [EXAMPLE_CLAUDE_SUNPLUS.md](EXAMPLE_CLAUDE_SUNPLUS.md) | 範例二:真實研究專案 Sunplus_Project,示範 152 行瘦身到 45 行的分層過程 |
| [CHECKLIST.md](CHECKLIST.md) | 套用後自我檢核清單(含持續維護項目) |

## 快速上手

1. 複製 `CLAUDE.template.md` 到專案根目錄,改名為 `CLAUDE.md`。
2. 對照兩份範例填寫 placeholder,刪除所有填寫註解。
3. 複製 `STATE.template.md` 到專案的 `docs/STATE.md`。
4. 用 `CHECKLIST.md` 逐項檢核,確保 60–80 行以內;之後每個里程碑重跑一次。

核心原則:每一行都要通過「刪掉這行,agent 會不會因此出錯?」的測試。
