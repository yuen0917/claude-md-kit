# CLAUDE.md 通用範本套件

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code Plugin](https://img.shields.io/badge/Claude_Code-Plugin-d97757.svg)](https://code.claude.com/docs/en/plugins)
![Docs: 繁體中文](https://img.shields.io/badge/Docs-%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-blue.svg)

**用最少的 context,換取最可靠的 agent 行為。**

CLAUDE.md 寫太長會被 agent 忽略、寫太短 agent 又反覆踩同樣的坑;每開一個新專案都要重新想一次該寫什麼;session 一關,專案脈絡就歸零。本套件把這些問題收斂成一組經過驗證的範本、指引與檢核清單,並打包成 Claude Code plugin——三個指令就能在任何專案落地。

## 功能特色

- **60–80 行的精簡範本**:六區塊結構(描述/環境/驗證/架構/慣例/狀態/邊界),每一行都通過「刪掉這行,agent 會不會出錯?」的測試
- **跨 session 狀態機制**:`docs/STATE.md` 讓新 session 接得上前一個 session 的目標、決策與下一步
- **五層放置體系**:全域 → 專案根 → 子目錄 → rules → docs,內容放在最貼近生效範圍的層級
- **三個開箱即用的 skills**:建立(apply)、檢核(check)、瘦身(slim),涵蓋 CLAUDE.md 的完整生命週期
- **真實案例示範**:含一份 152 行 CLAUDE.md 瘦身到 37 行的完整分層過程

## 快速上手

### 方式一:安裝 plugin(建議)

在任何專案的 Claude Code 中執行:

```
/plugin marketplace add yuen0917/claude-md-kit
/plugin install claude-md-kit@claude-md-templates
```

templates 與 guides 隨 plugin 一起安裝,skills 自動引用。本 repo 每次 push 即為新版本,之後用 `/plugin update claude-md-kit` 取得更新。

### 方式二:手動套用

1. 複製 [templates/CLAUDE.template.md](templates/CLAUDE.template.md) 到專案根目錄,改名為 `CLAUDE.md`。
2. 對照 [examples/](examples/) 的範例填寫 placeholder,刪除所有填寫註解。
3. 複製 [templates/STATE.template.md](templates/STATE.template.md) 到專案的 `docs/STATE.md`。
4. 用 [guides/CHECKLIST.md](guides/CHECKLIST.md) 逐項檢核,確保 60–80 行以內。

## Skills 使用情境

### `/claude-md-apply` — 建立

> 情境:新專案(或想重寫 CLAUDE.md 的舊專案),不知道該寫什麼、寫多少。

探勘專案結構與工具鏈 → 實測 test / lint 指令確認可執行 → 選項式訪談補上探勘不到的資訊(階段、慣例、紅線)→ 產出 60–80 行的 `CLAUDE.md` 與 `docs/STATE.md` → 用檢核清單自我核對後交付。

### `/claude-md-check` — 檢核

> 情境:CLAUDE.md 用了一陣子,想確認它還健康;或每個里程碑的例行健檢。

以 [CHECKLIST.md](guides/CHECKLIST.md) 逐項核對(長度、強標記數量、驗證指令是否實際可跑、有無與全域重複……),每項回報 ✅/❌ 與具體修法;經同意才動手修改。

### `/claude-md-slim` — 瘦身

> 情境:CLAUDE.md 越寫越長、超過 80 行,agent 開始忽略其中的規則。

逐條分類每行內容的去向(保留/移全域/移子目錄/移 rules/移 docs/改用 hook/刪除)→ 產出「原內容 → 去向」對照表供審核 → 同意後搬移,成品回到 80 行以內。分層邏輯見 [PLACEMENT_GUIDE.md](guides/PLACEMENT_GUIDE.md),實際案例見 [sunplus.md](examples/sunplus.md)。

## 設計理念

1. **每一行都要值回 context**。CLAUDE.md 的每一行都佔用所有 session 的 context;去留的唯一判準是「刪掉這行,agent 會不會因此出錯?」不會就刪。
2. **60–80 行是上限,不是目標**。超過這個長度,agent 對個別規則的遵循率明顯下降;塞爆的 CLAUDE.md 等於沒有 CLAUDE.md。
3. **內容放在最貼近生效範圍的層級**。跨專案準則放全域、子系統規則放子目錄、檔型規則放 rules、大文件放 docs 按需讀——每個 session 只載入當下需要的東西,同一條規則只存在於一層。
4. **可執行的完成定義**。驗證指令必須實際跑過、可直接複製執行;「程式碼寫完」不等於完成,test 與 lint 全過才算。
5. **CLAUDE.md 是活文件**。agent 重複犯錯就濃縮成一行加入;從未生效的行就刪除;逼近上限就分層下放。維護迴圈見 [WORKFLOW.md](guides/WORKFLOW.md)。

## 目錄結構

```
claude-md-kit/
├── .claude-plugin/          # plugin.json(manifest)與 marketplace.json(發佈目錄)
├── skills/                  # 三個 Claude Code skills
│   ├── claude-md-apply/     #   建立 CLAUDE.md 與 STATE.md
│   ├── claude-md-check/     #   檢核既有 CLAUDE.md
│   └── claude-md-slim/      #   瘦身分層過長的 CLAUDE.md
├── templates/               # 可直接複製的範本
├── guides/                  # workflow、放置指引、檢核清單
├── examples/                # 四份套用範例
└── docs/                    # 原始 prompt 存檔、本 repo 自身的 STATE.md
```

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
| [sunplus.md](examples/sunplus.md) | 範例二:真實研究專案 Sunplus_Project,示範 152 行瘦身到 37 行的分層過程 |
| [global-claude.md](examples/global-claude.md) | 第 1 層範例:全域 `~/.claude/CLAUDE.md` |
| [rules.md](examples/rules.md) | 第 4 層範例:`.claude/rules/` 路徑作用域規則 |

### `skills/` 與 `.claude-plugin/` — plugin 元件
| 檔案 | 用途 |
|---|---|
| [claude-md-apply](skills/claude-md-apply/SKILL.md) | `/claude-md-apply`:為目前專案訪談式建立 CLAUDE.md 與 docs/STATE.md |
| [claude-md-check](skills/claude-md-check/SKILL.md) | `/claude-md-check`:用 CHECKLIST 逐項檢核既有 CLAUDE.md |
| [claude-md-slim](skills/claude-md-slim/SKILL.md) | `/claude-md-slim`:依五層原則瘦身分層過長的 CLAUDE.md |
| `.claude-plugin/` | plugin.json(plugin manifest)與 marketplace.json(發佈目錄) |

### `docs/` — 其他文件
| 檔案 | 用途 |
|---|---|
| [fable5_claude_md_prompt.md](docs/fable5_claude_md_prompt.md) | 產生本套件的原始 prompt(存檔用) |
| [STATE.md](docs/STATE.md) | 本套件自身的跨 session 狀態檔(dogfooding) |

## License

[MIT](LICENSE)
