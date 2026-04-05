## Why

兩個職業需要重設計：
1. **Guardian Angel**：原本的「知道 Gnosia 身份」機制太強，即使削弱為只知 1 個仍然過於有效
2. **Doctor**：原本的「夜間保護」與新 GA 重複，需要賦予全新的獨特能力

重設計後三個特殊船員角色各有明確分工：
- **Engineer**：掃描存活者（情報收集）
- **Guardian Angel**：保護存活者（防禦）
- **Doctor**：驗屍被投票淘汰者（事後情報）

## What Changes

### Guardian Angel 重設計
- **BREAKING**：不再知道任何 Gnosia 身份
- 新增夜間行動：保護一名玩家免受 Gnosia 攻擊
- 可以公開自己的身份，藉由對話推測 Gnosia
- 無連續保護同一人的限制（與舊 Doctor 不同）

### Doctor 重設計
- **BREAKING**：不再有夜間保護能力
- 新增夜間行動：查看前一日被投票淘汰者的陣營（是否為 Gnosia）
- 第一天夜間無法使用（因為第一天可能還沒有人被投票淘汰）
- 結果為「是 Gnosia」或「不是 Gnosia」

### Engineer 調整
- 恢復 100% 掃描準確率（移除 25% 模糊機制）——三個角色各有明確情報來源，不需要模糊

## Non-Goals

- 新增或移除職業
- 改變角色 agent 性格

## Capabilities

### Modified Capabilities
- `advanced-roles`：GA 和 Doctor 能力完全重設計
- `game-master`：GA 和 Doctor 的夜間行動、prompt、資訊隔離
- `game-rules`：夜間行動列表、保護判定更新

### Removed Capabilities
- `engineer-scan-fuzzy`：移除模糊掃描機制

## Impact

- 修改檔案：`.claude/commands/gnosia.md`
- 修改檔案：`.claude/agents/*.md`（更新 GA 和 Doctor 行為策略）
- 修改檔案：`README.md`
