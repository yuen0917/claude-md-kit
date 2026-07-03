# CLAUDE_Template

CLAUDE.md 通用範本套件:供任何專案複製套用的範本、workflow 與檢核清單。本 repo 的「產品」就是這些 Markdown 文件本身。

## 檔案職責
- `CLAUDE.template.md` / `STATE.template.md` — 可複製範本(含 `<!-- -->` 填寫註解)
- `EXAMPLE_CLAUDE.md`(BookTrail 假想專案)/ `EXAMPLE_CLAUDE_SUNPLUS.md`(真實專案瘦身示範)— 套用後範例
- `GLOBAL_CLAUDE.example.md` / `RULES_EXAMPLE.md` — 分層第 1、4 層的範例
- `WORKFLOW.md` / `PLACEMENT_GUIDE.md` / `CHECKLIST.md` — 配套文件
- `fable5_claude_md_prompt.md` — 產生本套件的原始 prompt,唯讀,勿修改

## 驗證
- 修改範本或範例後,確認刪除註解後的成品仍在 60–80 行以內。
- 用 `CHECKLIST.md` 逐項核對被修改的檔案。

## 慣例與陷阱
- 說明文字用繁體中文;技術詞與指令保留英文。
- 三份核心文件必須連動:改了範本的區塊結構,`EXAMPLE_CLAUDE.md` 與 `CHECKLIST.md` 要同步更新。
- 範本內容本身要通過自己的準則:「刪掉這行,agent 會不會出錯?」不會就刪。
- `README.md` 的檔案索引表要與實際檔案清單一致。

## 邊界
- 範本與範例中絕不出現真實秘密、真實網址或真實個資;示範值一律虛構。
