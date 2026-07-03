# CLAUDE.md 通用範本套件

可套用於任何專案的 CLAUDE.md 範本與配套 agent workflow。
目標:用最少的 context 換取最可靠的 agent 行為。

## 檔案索引

| 檔案 | 用途 |
|---|---|
| [CLAUDE.template.md](CLAUDE.template.md) | 通用範本:複製到專案根目錄改名 CLAUDE.md,填 placeholder、刪註解 |
| [WORKFLOW.md](WORKFLOW.md) | Agent 標準流程:定位 → 規劃 → 執行 → 驗證 → 交付,含跨 session 狀態管理 |
| [PLACEMENT_GUIDE.md](PLACEMENT_GUIDE.md) | 分層放置指引:什麼內容放全域、專案根、子目錄、rules、docs |
| [EXAMPLE_CLAUDE.md](EXAMPLE_CLAUDE.md) | 填好的完整範例(假想專案 BookTrail),供對照 |
| [CHECKLIST.md](CHECKLIST.md) | 套用後自我檢核清單 |

## 快速上手

1. 複製 `CLAUDE.template.md` 到專案根目錄,改名為 `CLAUDE.md`。
2. 對照 `EXAMPLE_CLAUDE.md` 填寫 placeholder,刪除所有填寫註解。
3. 建立 `docs/STATE.md`(結構見 WORKFLOW.md)。
4. 用 `CHECKLIST.md` 逐項檢核,確保 60–80 行以內。

核心原則:每一行都要通過「刪掉這行,agent 會不會因此出錯?」的測試。
