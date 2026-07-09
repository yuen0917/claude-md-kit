---
name: claude-md-slim
description: 將過長的 CLAUDE.md 依五層放置原則瘦身分層:逐條分類去向(全域/專案根/子目錄/rules/docs/hook/刪除),產出對照表經同意後搬移。當 CLAUDE.md 超過 80 行、內容開始被 agent 忽略,或使用者要求精簡分層時使用。
---

# 瘦身分層 CLAUDE.md

1. **讀對象與依據**:目前專案的 CLAUDE.md,加上 `${CLAUDE_PLUGIN_ROOT}/guides/PLACEMENT_GUIDE.md`(五層原則)。
2. **逐條分類**:每行(或每段)標注去向之一:
   - 保留專案根 CLAUDE.md(專案專屬、幾乎每次工作用到)
   - 移全域 `~/.claude/CLAUDE.md`(跨專案成立的個人準則)
   - 移子目錄 CLAUDE.md(只對某子系統有意義)
   - 移 `.claude/rules/`(只對特定檔型/路徑有意義,附 glob)
   - 移 `docs/` 按需讀(大型文件,CLAUDE.md 留一行「何時讀哪份」)
   - 改用 hook / linter 強制(工具擋得住的格式規則)
   - 直接刪(通不過「刪掉這行,agent 會不會出錯?」)
3. **先審後搬**:產出「原內容 → 去向」對照表給使用者審核,格式參考 `${CLAUDE_PLUGIN_ROOT}/examples/sunplus.md` 開頭的去向對照(152→45 行示範);經同意後才實際搬移。
4. **搬移後驗證**:成品 ≤ 80 行,用 `${CLAUDE_PLUGIN_ROOT}/guides/CHECKLIST.md` 重核一次。
5. **邊界**:使用者的 `~/.claude/CLAUDE.md` 屬個人全域設定,只提議修改內容,未經明確同意不直接改動。
