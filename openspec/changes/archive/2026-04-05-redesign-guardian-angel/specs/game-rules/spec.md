## MODIFIED Requirements

### Requirement: 夜間行動

#### Scenario: 有夜間行動的角色
- **WHEN** 進入夜間階段
- **THEN** GM SHALL 呼叫 Gnosia（攻擊）、Engineer（掃描）、Guardian Angel（保護）。Doctor 驗屍為自動處理。AC Follower、Bug、Crew 無夜間行動。

### Requirement: 保護判定

#### Scenario: 攻擊被 GA 擋住
- **WHEN** Gnosia 攻擊目標被 Guardian Angel 保護
- **THEN** 攻擊被擋，無人死亡

## REMOVED Requirements

### Requirement: Engineer 掃描模糊機制
**Reason**: Engineer 恢復 100% 準確率。三個特殊角色各有明確分工，不需要模糊削弱。
**Migration**: 移除擲骰邏輯，掃描結果固定為「是 Gnosia」或「不是 Gnosia」。
