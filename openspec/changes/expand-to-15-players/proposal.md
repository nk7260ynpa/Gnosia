## Why

目前遊戲僅有 8 個角色（5 原始 + 3 新增）和最多 8 人局，無法重現 Gnosia 原作的完整 15 人陣容。
需要補齊所有原作角色並將上限提升至 15 人，提供更大規模、更複雜的社交推理體驗。

## What Changes

- 新增 7 個 Gnosia 原作角色 agent：ジョナス（Jonas）、オトメ（Otome）、しげみち（Shigemichi）、クク（Kukrushka）、ラキ（Raki）、シャ=ミン（Sha-Ming）、ユルグ（Yurugu）
- **BREAKING**：人數上限從 8 提升至 15，角色配置表全面擴充
- 擴充 Gnosia 人數隨人數增長（9-15 人局 Gnosia 增加到 3-4 人）
- 高人數局新增第二名 Engineer（10 人以上）
- 高人數局調整討論輪數（10 人以上縮減為 1 輪避免過長）
- 更新 GM 的角色池和配置邏輯

## Non-Goals

- 新增原作以外的自創角色
- 新增原作以外的自創職業
- 使用者參與遊戲（維持觀戰模式）
- 角色 agent 的持久記憶

## Capabilities

### New Capabilities
- `expanded-character-agents`：7 個新角色 agent（ジョナス、オトメ、しげみち、クク、ラキ、シャ=ミン、ユルグ）的性格與說話風格定義

### Modified Capabilities
- `game-rules`：擴充角色配置表至 15 人局，調整 Gnosia 人數和 Engineer 數量
- `character-agents`：更新角色對照表，納入全部 15 個角色
- `game-master`：擴充 GM 角色池、配置邏輯、討論輪數控制

## Impact

- 新增檔案：`.claude/agents/jonas.md`、`otome.md`、`shigemichi.md`、`kukrushka.md`、`raki.md`、`sha-ming.md`、`yurugu.md`
- 修改檔案：`.claude/commands/gnosia.md`（角色池、配置表、討論輪數）
- 修改檔案：`README.md`（角色表、配置表）
