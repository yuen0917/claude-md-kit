# CLAUDE.md 通用範本套件

可套用於任何專案的 CLAUDE.md 範本與配套 agent workflow。
目標:用最少的 context 換取最可靠的 agent 行為。

## 檔案索引

### `templates/` — 可直接複製的範本
| 檔案 | 用途 |
|---|---|
| [CLAUDE.template.md](templates/CLAUDE.template.md) | 通用範本:複製到專案根目錄改名 CLAUDE.md,填 placeholder、刪註解 |
| [STATE.template.md](templates/STATE.template.md) | 跨 session 狀態檔範本:複製到專案的 `docs/STATE.md` |

### `guides/` — 配套指引
| 檔案 | 用途 |
|---|---|
| [WORKFLOW.md](guides/WORKFLOW.md) | Agent 標準流程:定位 → 規劃 → 執行 → 驗證 → 交付,含狀態管理與維護迴圈 |
| [PLACEMENT_GUIDE.md](guides/PLACEMENT_GUIDE.md) | 分層放置指引:什麼內容放全域、專案根、子目錄、rules、docs |
| [CHECKLIST.md](guides/CHECKLIST.md) | 套用後自我檢核清單(含持續維護項目) |

### `examples/` — 套用範例
| 檔案 | 用途 |
|---|---|
| [booktrail.md](examples/booktrail.md) | 範例一:假想後端專案 BookTrail 的專案根 CLAUDE.md |
| [sunplus.md](examples/sunplus.md) | 範例二:真實研究專案 Sunplus_Project,示範 152 行瘦身到 45 行的分層過程 |
| [global-claude.md](examples/global-claude.md) | 第 1 層範例:全域 `~/.claude/CLAUDE.md` |
| [rules.md](examples/rules.md) | 第 4 層範例:`.claude/rules/` 路徑作用域規則 |

### `docs/` — 其他文件
| 檔案 | 用途 |
|---|---|
| [fable5_claude_md_prompt.md](docs/fable5_claude_md_prompt.md) | 產生本套件的原始 prompt(存檔用) |

## 快速上手

1. 複製 `templates/CLAUDE.template.md` 到專案根目錄,改名為 `CLAUDE.md`。
2. 對照 `examples/` 的兩份範例填寫 placeholder,刪除所有填寫註解。
3. 複製 `templates/STATE.template.md` 到專案的 `docs/STATE.md`。
4. 用 `guides/CHECKLIST.md` 逐項檢核,確保 60–80 行以內;之後每個里程碑重跑一次。

核心原則:每一行都要通過「刪掉這行,agent 會不會因此出錯?」的測試。
