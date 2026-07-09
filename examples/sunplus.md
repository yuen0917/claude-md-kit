<!--
第二份套用範例:基於真實 repo yuen0917/Sunplus_Project(語音降噪模型輕量化,研究型專案)。
原 repo 的 CLAUDE.md 有 152 行;本範例示範按 guides/PLACEMENT_GUIDE.md 分層瘦身後的結果(本文約 37 行)。

原內容的去向對照:
- 工作準則、省 token 規則         → 全域 ~/.claude/CLAUDE.md(見 examples/global-claude.md)
- 共享 server 安全限制(30+ 行)   → .claude/settings.json 的 permissions.deny + PreToolUse hook
                                    (工具強制勝過文字提醒;原 repo 其實已有 guard_bash.py)
- 程式碼風格與好壞範例            → black / ruff 已強制,整段刪除
- 階段計畫表、目前進度、待補規格   → docs/STATE.md(見 templates/STATE.template.md)
- DFNet2 技術細節、FPGA 未來方向   → docs/,需要時再讀
- 人員名單                        → docs/,agent 用不到
-->

# Sunplus_Project

清華大學 × 凌陽科技產學合作:將 DeepFilterNet2 (DFNet2) 降噪模型輕量化(量化/縮減/剪枝/蒸餾),最終落地 Cadence HiFi 5 DSP。目前在階段 0–2(基線量測 → PTQ INT8 → 架構縮減)。

## 環境與技術棧
- Python 3.11(uv 託管);一律用 `.venv`,重現環境:`uv pip install -r requirements.lock`
- torch==2.1.2 + torchaudio==2.1.2(版號須相同)。勿升級:deepfilternet 0.5.6 依賴 `torchaudio.backend`,2.2+ 已移除。numpy 勿升 2.x。
- DFNet2 原始碼另行 clone(不入庫):`git clone https://github.com/Rikorose/DeepFilterNet`

## 驗證指令
- Test:`.venv/Scripts/python.exe -m pytest -q`
- Lint:`.venv/Scripts/ruff.exe check src tests`
- Format:`.venv/Scripts/black.exe src tests`

IMPORTANT:任務只有在 Test 與 Lint 全數通過後才算完成;實測數字(RTF/PESQ)不能只跑一次就當定論。

## 架構地圖
- `src/sunplus_lite/` — 核心模組:metrics / baseline / profiling / quantize
- `scripts/` — 各階段 pipeline(stage0 基線 → stage1 PTQ → stage2 縮減重訓)
- `csrc/` — DSP 落地用 C kernel(STFT/ERB/deep filter),含 Makefile 與 golden 比對
- `tests/` — pytest;`results/` — 基線 CSV;`docs/` — 文件與計畫書 PDF
- 動輕量化策略前,先讀 `docs/CODE_GUIDE.md`;歷史教訓見 `docs/LESSONS.md`。

## 慣例與陷阱
- 任何輕量化實驗前,先用 `sunplus_lite.baseline.append_row` 填基線表(對照 FP32 原版)。
- 每階段必記七項指標:參數量 / MB / GMACS / RTF / 延遲 / PESQ / STOI。
- 量化敏感層 = GRU + 複數 deep filter;PESQ 掉幅過大時,這些層保留 INT16。
- pesq 套件需 MSVC build tools 才裝得起來;未裝前品質指標先用 pystoi。

## 跨 session 狀態
- 開工前:讀 `docs/STATE.md`(階段進度、關鍵決策、待補的凌陽 HiFi 5 規格)。
- 收工前:更新 `docs/STATE.md`;重複踩到的坑追記到 `docs/LESSONS.md`。

## 邊界
- 只有明確要求才 commit / push;commit message 用英文。新增依賴或變更 torch 版本先問。
- 絕不修改或刪除 `docs/` 內的計畫書 PDF,也不動 clone 進來的 `DeepFilterNet/`。
- 絕不提交密鑰。共享 server 上的操作限制由 `.claude/settings.json` 與 guard hook 強制,不靠本檔文字。
