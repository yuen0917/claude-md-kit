---
name: claude-md-apply
description: 為目前專案建立精簡的 CLAUDE.md 與 docs/STATE.md:探勘專案、實測驗證指令、訪談補缺、填寫範本後刪註解並控制在 60–80 行。當使用者要初始化、建立或重寫專案的 CLAUDE.md 時使用。
---

# 套用 CLAUDE.md 範本

為目前專案產出 `CLAUDE.md` 與 `docs/STATE.md`,依序執行:

## 步驟

1. **讀範本與範例**
   - 範本:`${CLAUDE_PLUGIN_ROOT}/templates/CLAUDE.template.md`(六區塊結構,`<!-- -->` 註解是填寫說明)
   - 參考:`${CLAUDE_PLUGIN_ROOT}/examples/booktrail.md`(一般後端專案)、`${CLAUDE_PLUGIN_ROOT}/examples/sunplus.md`(研究型專案)
2. **探勘專案**:先讀再寫——目錄結構、套件管理器、test/lint/build 指令、README 與既有設定。從結構一看即知的資訊不寫進 CLAUDE.md。若已存在 CLAUDE.md,先讀並告知使用者將如何處理既有內容。
3. **實測驗證指令**:候選的 test / lint 指令實際各跑一次,確認可直接複製執行;跑不起來就標註原因並詢問使用者。
4. **訪談補缺**:只問探勘不出來的事(專案階段與目標、慣例與陷阱、紅線),用選項式提問。
5. **產出**
   - `CLAUDE.md`:填好所有 placeholder、刪除全部 `<!-- -->` 註解、成品 60–80 行以內
   - `docs/STATE.md`:依 `${CLAUDE_PLUGIN_ROOT}/templates/STATE.template.md`,填入目前目標與下一步,日期用絕對日期
6. **自我檢核**:用 `${CLAUDE_PLUGIN_ROOT}/guides/CHECKLIST.md` 逐項核對,不過的項目回頭修,最後回報檢核結果。

## 原則

- 每行去留判準:「刪掉這行,agent 會不會出錯?」不會 → 刪。
- 內容放置層級遵循 `${CLAUDE_PLUGIN_ROOT}/guides/PLACEMENT_GUIDE.md`;使用者全域 `~/.claude/CLAUDE.md` 已有的準則不重複寫入專案檔。
- 強標記(IMPORTANT / 絕不)全檔合計 ≤ 3 處。
- 絕不將任何秘密(API key、憑證)寫入產出的檔案。
