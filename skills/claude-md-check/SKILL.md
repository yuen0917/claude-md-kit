---
name: claude-md-check
description: 用檢核清單逐項核對目前專案的 CLAUDE.md(含子目錄 CLAUDE.md 與 .claude/rules/),回報每項通過與否及具體修法。當使用者要檢查、審核、健檢既有 CLAUDE.md,或在里程碑後重新檢核時使用。
---

# 檢核 CLAUDE.md

1. **收集對象**:讀專案根 `CLAUDE.md`;若存在,也讀子目錄 CLAUDE.md、`.claude/rules/*.md`、`docs/STATE.md`。
2. **逐項核對**:以 `${CLAUDE_PLUGIN_ROOT}/guides/CHECKLIST.md` 為準,每項給 ✅ / ❌ / 不適用。
3. **實測驗證指令**:清單中「驗證指令實際跑過」一項,實際執行 CLAUDE.md 內的 test / lint 指令確認可用;會產生副作用的指令先告知再跑。
4. **回報**:❌ 項目附具體修法;涉及內容放置層級時,引用 `${CLAUDE_PLUGIN_ROOT}/guides/PLACEMENT_GUIDE.md` 的建議(全域 / 專案根 / 子目錄 / rules / docs)。
5. **修改需同意**:未經使用者同意不動手改;同意後修完重跑一次清單,回報前後對照。
