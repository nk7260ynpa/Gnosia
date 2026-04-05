## MODIFIED Requirements

### Requirement: 資訊隔離

#### Scenario: Guardian Angel 的資訊
- **WHEN** 呼叫 Guardian Angel 角色的 agent
- **THEN** prompt MUST NOT 包含任何 Gnosia 身份資訊，僅包含公開資訊

#### Scenario: Doctor 的驗屍結果
- **WHEN** 呼叫 Doctor 角色的 agent 進行討論
- **THEN** prompt SHALL 包含驗屍歷史（每日被淘汰者的陣營結果），MUST NOT 包含 Engineer 掃描結果或 GA 保護歷史

#### Scenario: Engineer 掃描結果
- **WHEN** 呼叫 Engineer 角色的 agent
- **THEN** prompt SHALL 包含 100% 準確的掃描結果歷史

### Requirement: Agent 呼叫方式

#### Scenario: 夜間行動
- **WHEN** 進入夜間階段
- **THEN** GM SHALL 呼叫 Gnosia（攻擊）、Engineer（掃描）、Guardian Angel（保護）。Doctor 的驗屍為自動處理，MUST NOT 呼叫 Doctor agent。

## ADDED Requirements

### Requirement: Guardian Angel 夜間保護 prompt

#### Scenario: GA 保護 prompt
- **WHEN** GM 呼叫 Guardian Angel agent 進行夜間保護
- **THEN** prompt SHALL 包含：保護歷史、存活玩家列表、今日討論摘要。無連續保護限制。

### Requirement: Doctor 驗屍自動處理

#### Scenario: GM 自動解析驗屍
- **WHEN** 夜間結果解析且當日有人被投票淘汰
- **THEN** GM SHALL 記錄被淘汰者的真實陣營，下一日在 Doctor 的討論 prompt 中附上結果

### Requirement: Doctor 討論 prompt 更新

#### Scenario: Doctor 討論 prompt
- **WHEN** GM 呼叫 Doctor agent 進行討論
- **THEN** prompt 中身份描述改為：「你是醫生。你的能力是查看前一日被投票淘汰者的陣營。驗屍歷史：【列表】」
