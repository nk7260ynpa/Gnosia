## Why

需要建立一個以 Claude Code 自訂指令驅動的 Gnosia 太空社交推理遊戲，
讓 5 個 AI 角色能全自動進行社交推理對戰，使用者以上帝視角觀戰。

## What Changes

- 建立 GM 主控指令 `.claude/commands/gnosia.md`（opus 模型）
- 建立 5 個角色 agent 定義檔 `.claude/agents/*.md`（sonnet 模型）
- 實作完整遊戲流程：初始化 → 日間討論 → 投票 → 夜間行動 → 勝負判定
- 實作資訊隔離機制（GM 控制每個 agent 的 prompt 內容）
- 實作彩色圓點標記系統（🔴🔵🟢🟡🟣）
- 實作上帝視角輸出格式

## Non-Goals

- 使用者參與遊戲（本版本僅支援觀戰）
- 超過 5 人的遊戲模式
- 守護天使、AC 主義者、Bug 等進階角色
- 遊戲歷史記錄與統計的持久化儲存
- 多語言支援（僅繁體中文）

## Capabilities

### New Capabilities
- `game-master`：GM 主控流程，管理遊戲狀態與資訊隔離
- `character-agents`：5 個獨立角色 agent，各有固定性格與說話風格
- `game-rules`：完整 5 人局規則引擎（Gnosia x2, Engineer, Doctor, Crew）
- `output-format`：彩色標記、上帝視角、格式化呈現

## Impact

- 新增檔案：`.claude/commands/gnosia.md`
- 新增檔案：`.claude/agents/setsu.md`, `raqio.md`, `gina.md`, `comet.md`, `sq.md`
- 新增檔案：`README.md`, `.gitignore`
