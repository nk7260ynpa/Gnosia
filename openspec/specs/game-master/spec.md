## Requirements

### Requirement: GM 指令定義

GM SHALL 定義為 `.claude/commands/gnosia.md`，使用 opus 模型。
使用者輸入 `/gnosia` SHALL 啟動一場完整遊戲。

#### Scenario: 遊戲啟動
- **WHEN** 使用者輸入 `/gnosia`
- **THEN** GM SHALL 執行完整遊戲流程：初始化 → 日間討論 → 投票 → 夜間行動 → 循環直到結束

### Requirement: Agent 呼叫方式

GM SHALL 透過 `subagent_type` 呼叫角色 agent（setsu/raqio/gina/comet/sq/shipi/stella/remnant）。
每次呼叫 SHALL 在 prompt 中傳入遊戲身份和當前狀態。

#### Scenario: 討論階段呼叫
- **WHEN** 進入討論階段
- **THEN** GM SHALL 按隨機順序逐一呼叫存活角色的 agent，每次 prompt 包含已發出的發言

#### Scenario: 投票階段呼叫
- **WHEN** 進入投票階段
- **THEN** GM SHALL 呼叫所有存活角色的 agent 進行投票（可並行）

#### Scenario: 夜間階段呼叫
- **WHEN** 進入夜間階段
- **THEN** GM SHALL 呼叫需要行動的角色 agent（Gnosia/Engineer/Doctor，可並行）。Guardian Angel、AC Follower、Bug MUST NOT 被呼叫進行夜間行動

### Requirement: 資訊隔離

GM MUST 嚴格控制傳入每個 agent 的資訊內容，確保遊戲公平性。

#### Scenario: Gnosia 的資訊限制
- **WHEN** 呼叫 Gnosia 角色的 agent
- **THEN** prompt MUST NOT 包含 Engineer 的掃描結果或 Doctor 的保護歷史

#### Scenario: Engineer 的私密資訊
- **WHEN** 呼叫 Engineer 角色的 agent
- **THEN** prompt SHALL 包含該 Engineer 自己的歷史掃描結果，MUST NOT 包含 Doctor 保護歷史或 Gnosia 同伴資訊

#### Scenario: Doctor 的私密資訊
- **WHEN** 呼叫 Doctor 角色的 agent
- **THEN** prompt SHALL 包含該 Doctor 自己的保護歷史（含連續保護限制提醒），MUST NOT 包含 Engineer 掃描結果或 Gnosia 同伴資訊

#### Scenario: 公開資訊
- **WHEN** 呼叫任何角色的 agent
- **THEN** prompt SHALL 包含：存活玩家列表、已淘汰者列表（不含身份）、所有公開發言記錄、投票結果歷史

### Requirement: 遊戲狀態管理

GM SHALL 在對話 context 中追蹤完整遊戲狀態。

#### Scenario: 狀態追蹤項目
- **WHEN** 遊戲進行中
- **THEN** GM SHALL 追蹤：回合數、每個角色的存活/死亡狀態、真實身份、Engineer 掃描結果、Doctor 保護歷史、所有公開發言、所有投票結果

### Requirement: 勝負檢查時機

#### Scenario: 投票後檢查
- **WHEN** 投票淘汰一名角色後
- **THEN** GM SHALL 立即檢查勝負條件

#### Scenario: 夜間行動後檢查
- **WHEN** 夜間行動結果解析完成後
- **THEN** GM SHALL 立即檢查勝負條件
