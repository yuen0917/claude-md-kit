# claude-md-kit

CLAUDE.md 通用範本套件:供任何專案複製套用的範本、workflow 與檢核清單。本 repo 的「產品」就是這些 Markdown 文件本身。

## 檔案職責
- `templates/` — 可複製範本(含 `<!-- -->` 填寫註解):CLAUDE.template.md、STATE.template.md
- `examples/` — 套用範例:booktrail.md(假想專案)、sunplus.md(真實專案瘦身示範)、global-claude.md、rules.md
- `guides/` — 配套文件:WORKFLOW.md、PLACEMENT_GUIDE.md、CHECKLIST.md
- `skills/` + `.claude-plugin/` — 本 repo 兼作 Claude Code plugin(claude-md-kit):apply / check / slim 三個 skills,以 `${CLAUDE_PLUGIN_ROOT}` 引用 templates 與 guides
- `docs/fable5_claude_md_prompt.md` — 產生本套件的原始 prompt,唯讀,勿修改
- `docs/STATE.md` — 本套件自身狀態:開工前讀、收工前更新
- 範例檔勿命名為 `CLAUDE.md` 放進子資料夾——會被 Claude Code 當成生效設定載入。

## 驗證
- 修改範本或範例後,確認刪除註解後的成品仍在 60–80 行以內。
- 用 `CHECKLIST.md` 逐項核對被修改的檔案。

## 慣例與陷阱
- 說明文字用繁體中文;技術詞與指令保留英文。
- 核心文件必須連動:改了範本的區塊結構,`examples/` 兩份範例與 `guides/CHECKLIST.md` 要同步更新。
- 改動 templates/ 或 guides/ 的檔名或路徑時,`skills/` 三個 SKILL.md 內的 `${CLAUDE_PLUGIN_ROOT}` 引用要同步。
- 範本內容本身要通過自己的準則:「刪掉這行,agent 會不會出錯?」不會就刪。
- `README.md` 的檔案索引表要與實際檔案清單一致。

## 邊界
- 範本與範例中絕不出現真實秘密、真實網址或真實個資;示範值一律虛構。
