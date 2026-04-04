## Requirements

### Requirement: GM 指令定義

GM SHALL 定義為 `.claude/commands/gnosia.md`，使用 opus 模型。
使用者輸入 `/gnosia` SHALL 啟動一場完整遊戲。

#### Scenario: 遊戲啟動
- **WHEN** 使用者輸入 `/gnosia`
- **THEN** GM SHALL 執行完整遊戲流程：初始化 → 日間討論 → 投票 → 夜間行動 → 循環直到結束

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

### Requirement: 可變人數初始化

GM SHALL 支援 5-15 人局。預設為 5 人局，可透過指令參數指定人數。

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
