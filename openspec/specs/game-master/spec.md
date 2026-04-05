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

#### Scenario: 夜間行動
- **WHEN** 進入夜間階段
- **THEN** GM SHALL 呼叫 Gnosia（攻擊）、Engineer（掃描）、Guardian Angel（保護）。Doctor 的驗屍為自動處理，MUST NOT 呼叫 Doctor agent。

#### Scenario: 夜間多 Gnosia 攻擊
- **WHEN** 夜間階段且有多個 Gnosia 存活
- **THEN** GM SHALL 僅呼叫存活的第 1 個 Gnosia agent 做攻擊決策（代表制）

### Requirement: 資訊隔離

GM MUST 嚴格控制傳入每個 agent 的資訊內容，確保遊戲公平性。

#### Scenario: Gnosia 的資訊限制
- **WHEN** 呼叫 Gnosia 角色的 agent 進行討論
- **THEN** prompt SHALL 包含同伴身份、存活人數局勢，MUST NOT 包含 Engineer 掃描結果、Doctor 驗屍結果、Guardian Angel 保護歷史。prompt MUST NOT 包含「絕不」「假裝」「掩護」等防守型指令。

#### Scenario: Engineer 掃描結果
- **WHEN** 呼叫 Engineer 角色的 agent
- **THEN** prompt SHALL 包含 100% 準確的掃描結果歷史

#### Scenario: Doctor 的驗屍結果
- **WHEN** 呼叫 Doctor 角色的 agent 進行討論
- **THEN** prompt SHALL 包含驗屍歷史（每日被淘汰者的陣營結果），MUST NOT 包含 Engineer 掃描結果或 GA 保護歷史

#### Scenario: Guardian Angel 的資訊
- **WHEN** 呼叫 Guardian Angel 角色的 agent
- **THEN** prompt MUST NOT 包含任何 Gnosia 身份資訊，僅包含公開資訊

#### Scenario: AC Follower 的資訊
- **WHEN** 呼叫 AC Follower 角色的 agent
- **THEN** prompt SHALL 僅包含公開資訊，MUST NOT 包含任何私密資訊

#### Scenario: Bug 的資訊
- **WHEN** 呼叫 Bug 角色的 agent
- **THEN** prompt SHALL 僅包含公開資訊，MUST NOT 包含任何私密資訊

#### Scenario: AC Follower 淘汰不公開
- **WHEN** AC Follower 被投票淘汰
- **THEN** GM MUST NOT 在投票結果中宣佈「AC Follower 個人勝利」，SHALL 在遊戲結束時才揭曉

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
- **THEN** GM MUST NOT 在當場宣佈個人勝利，SHALL 在遊戲結束時才揭曉

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

### Requirement: Gnosia 討論 prompt 設計原則

Gnosia 的討論 prompt SHALL 採用「自然行為引導」而非「禁止清單」。prompt 的核心指令 SHALL 為引導 Gnosia 像普通船員一樣自然發言，僅附帶最低限度的同伴保護意識。

#### Scenario: Gnosia 討論 prompt 內容
- **WHEN** GM 建構 Gnosia 角色的討論 prompt
- **THEN** 身份描述 SHALL 為：「你是 Gnosia。你的同伴是【X】。像普通船員一樣自然地參與討論——推理、質疑、表達立場。你的性格不會因為身份而改變。唯一的額外意識：保護同伴不被投票淘汰，但用自然的方式。」

#### Scenario: Gnosia 策略提示
- **WHEN** GM 建構 Gnosia 角色的討論 prompt
- **THEN** 策略提示 SHALL 僅包含：局勢資訊（存活 Gnosia/船員人數）和投票分散提醒（避免和同伴投同一人）。MUST NOT 包含「不要急著辯護」「假裝中立」「假裝質疑同伴」等行為管控指令。

### Requirement: Gnosia 投票 prompt 設計原則

#### Scenario: Gnosia 投票 prompt 內容
- **WHEN** GM 建構 Gnosia 角色的投票 prompt
- **THEN** 投票指引 SHALL 為：「投你覺得對船員來說最合理的目標，但避免和同伴投同一人」。MUST NOT 使用「淘汰船員」等暴露 Gnosia 目標的措辭。

