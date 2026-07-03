# `.claude/rules/` 路徑作用域規則範例

對應 guides/PLACEMENT_GUIDE.md 的第 4 層:每則 rule 是一個獨立 `.md` 檔,
frontmatter 的 `globs` 決定「agent 動到哪些檔案時」才載入該規則,
平時不佔 context。以下兩個範例,實際使用時各自存成一檔。

## 範例一:`.claude/rules/sql-migrations.md`

```markdown
---
globs: ["migrations/**/*.sql"]
---
- 所有 migration 必須可回滾,附對應的 down script。
- migration 內不混入資料修補;data fix 另開獨立 script。
```

## 範例二:`.claude/rules/tests.md`

```markdown
---
globs: ["tests/**/*.py"]
---
- 測試命名 `test_<行為>_<情境>`;一個測試只驗證一件事。
- 只 mock 外部 I/O(網路、DB、時鐘),不 mock 被測物本身。
```

## 判斷是否該立一則 rule

- 規則只對**特定檔案類型或路徑**有意義 → rules(不要塞進根目錄 CLAUDE.md)。
- 規則對**整個子系統**有意義(不只特定檔型) → 子目錄 CLAUDE.md。
- 規則是**格式問題且工具擋得住** → formatter / linter / hook,不寫成文字。
