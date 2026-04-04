## MODIFIED Requirements

### Requirement: Agent 呼叫方式

GM SHALL 透過 `subagent_type` 呼叫角色 agent。完整的 subagent_type 列表：
setsu, raqio, gina, comet, sq, shipi, stella, remnant, jonas, otome, shigemichi, kukrushka, raki, sha-ming, yurugu

#### Scenario: 夜間多 Engineer 呼叫
- **WHEN** 夜間階段且有 2 個 Engineer 存活
- **THEN** GM SHALL 分別呼叫 2 個 Engineer agent 進行獨立掃描

#### Scenario: 夜間多 Doctor 呼叫
- **WHEN** 夜間階段且有 2 個 Doctor 存活
- **THEN** GM SHALL 分別呼叫 2 個 Doctor agent 進行獨立保護

#### Scenario: 夜間多 Gnosia 攻擊
- **WHEN** 夜間階段且有多個 Gnosia 存活
- **THEN** GM SHALL 僅呼叫存活的第 1 個 Gnosia agent 做攻擊決策（代表制）

## ADDED Requirements

### Requirement: 可變人數參數

GM SHALL 接受 5-15 的人數參數。

#### Scenario: 人數範圍驗證
- **WHEN** 使用者輸入 `/gnosia N`，N 超出 5-15 範圍
- **THEN** GM SHALL 提示「人數必須在 5-15 之間」並使用預設 5 人

### Requirement: 討論摘要機制

#### Scenario: 大型局討論記錄傳遞
- **WHEN** 人數 >= 10 且需要傳遞過往討論給 agent
- **THEN** GM SHALL 使用摘要（而非完整記錄）傳遞過往討論，避免 prompt 過長

### Requirement: 多重保護判定

#### Scenario: 2 Doctor 保護不同目標
- **WHEN** 2 個 Doctor 保護不同目標且 Gnosia 攻擊其中一個被保護的目標
- **THEN** 攻擊被擋，無人死亡

#### Scenario: 2 Doctor 保護相同目標
- **WHEN** 2 個 Doctor 保護相同目標
- **THEN** 效果等同 1 個 Doctor 保護（不疊加）
