<!--
這是套用 templates/CLAUDE.template.md 後的完整範例,對象是一個假想專案 BookTrail
(Python + FastAPI 的閱讀進度追蹤 API)。實際使用時整份即為專案根目錄的
CLAUDE.md,不含任何說明註解。全文約 37 行,低於 80 行上限。
-->

# BookTrail

面向個人讀者的閱讀進度追蹤 API 服務(FastAPI + PostgreSQL),目前處於 MVP 階段,尚未上線。

## 環境與技術棧
- 語言/框架:Python 3.12 + FastAPI + SQLAlchemy 2.x
- 套件管理:uv;新增依賴用 `uv add`,禁止直接 pip install
- 環境變數:讀自 `.env`(不入版控);缺少時先停下告知,不要硬編碼替代值。

## 驗證指令
- Test:`uv run pytest -q`
- Lint/Typecheck:`uv run ruff check . && uv run mypy src/`
- 本地執行:`docker compose up -d db && uv run uvicorn booktrail.main:app --reload`

IMPORTANT:任務只有在 Test 與 Lint/Typecheck 全數通過後才算完成;「程式碼寫完」不等於完成。

## 架構地圖
- `src/booktrail/api/` — FastAPI route,只做 I/O 驗證與轉發,不含商業邏輯
- `src/booktrail/services/` — 商業邏輯層
- `src/booktrail/repos/` — 資料庫存取(SQLAlchemy)
- `migrations/` — Alembic migration
- `tests/` — pytest,目錄結構鏡射 `src/`
- 需要動資料模型時,先讀 `docs/ARCHITECTURE.md` 的 ER 圖章節。

## 慣例與陷阱
- 所有 DB 存取一律經過 `repos/` 層;route 與 service 不直接下 query。
- integration 測試依賴本地 Postgres:先 `docker compose up -d db`,否則整批失敗。
- 日期時間一律存 UTC(timezone-aware);時區轉換只在 API 回應層做。

## 跨 session 狀態
- 開工前:讀 `docs/STATE.md`(目前目標、進度、未決事項、關鍵決策)。
- 收工前:更新 `docs/STATE.md`(本次變更、新決策與理由、下一步)。

## 邊界
- 絕不將秘密寫入任何會被讀取或提交的檔案;一律走 `.env`。
- 絕不自動執行 `alembic downgrade` 或刪除 migration 檔;先產出方案供人審核。
