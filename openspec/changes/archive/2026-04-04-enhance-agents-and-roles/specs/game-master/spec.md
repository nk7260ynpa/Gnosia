## MODIFIED Requirements

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
- **THEN** prompt MUST NOT 包含 Engineer 掃描結果、Doctor 保護歷史、或 Guardian Angel 知道其身份的事實

#### Scenario: Engineer 的私密資訊
- **WHEN** 呼叫 Engineer 角色的 agent
- **THEN** prompt SHALL 包含該 Engineer 自己的歷史掃描結果，MUST NOT 包含 Doctor 保護歷史或 Gnosia 同伴資訊

#### Scenario: Doctor 的私密資訊
- **WHEN** 呼叫 Doctor 角色的 agent
- **THEN** prompt SHALL 包含該 Doctor 自己的保護歷史（含連續保護限制提醒），MUST NOT 包含 Engineer 掃描結果或 Gnosia 同伴資訊

#### Scenario: Guardian Angel 的私密資訊
- **WHEN** 呼叫 Guardian Angel 角色的 agent
- **THEN** prompt SHALL 包含所有 Gnosia 的身份，MUST NOT 包含 Engineer 掃描結果或 Doctor 保護歷史

#### Scenario: AC Follower 的資訊
- **WHEN** 呼叫 AC Follower 角色的 agent
- **THEN** prompt SHALL 僅包含公開資訊，MUST NOT 包含任何私密資訊

#### Scenario: Bug 的資訊
- **WHEN** 呼叫 Bug 角色的 agent
- **THEN** prompt SHALL 僅包含公開資訊，MUST NOT 包含任何私密資訊

#### Scenario: 公開資訊
- **WHEN** 呼叫任何角色的 agent
- **THEN** prompt SHALL 包含：存活玩家列表、已淘汰者列表（不含身份）、所有公開發言記錄、投票結果歷史

## ADDED Requirements

### Requirement: 可變人數初始化

GM SHALL 支援 5-8 人局。預設為 5 人局，可透過指令參數指定人數。

#### Scenario: 預設人數
- **WHEN** 使用者輸入 `/gnosia` 不帶參數
- **THEN** GM SHALL 啟動 5 人局

#### Scenario: 指定人數
- **WHEN** 使用者輸入 `/gnosia 7`
- **THEN** GM SHALL 啟動 7 人局，從角色池隨機選取 7 個角色

### Requirement: AC Follower 勝利宣告

#### Scenario: AC Follower 被投票淘汰時
- **WHEN** AC Follower 被投票淘汰
- **THEN** GM SHALL 在冷凍睡眠宣告後額外顯示「AC Follower 個人勝利！」，遊戲繼續

### Requirement: Bug 勝利宣告

#### Scenario: 遊戲結束時 Bug 存活
- **WHEN** 遊戲結束且 Bug 仍然存活
- **THEN** GM SHALL 在結局中額外顯示「Bug 個人勝利！」
