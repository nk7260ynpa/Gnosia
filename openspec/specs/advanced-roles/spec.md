## Requirements

### Requirement: Guardian Angel（守護天使）

Guardian Angel SHALL 屬於船員陣營。Guardian Angel MUST NOT 知道任何 Gnosia 的身份。
Guardian Angel SHALL 有夜間行動：保護一名玩家免受 Gnosia 攻擊。無連續保護同一人的限制。
Guardian Angel 可以公開自己的身份並推測 Gnosia，但只是推測，沒有確定情報。

#### Scenario: Guardian Angel 無情報
- **WHEN** 遊戲初始化 Guardian Angel
- **THEN** GM MUST NOT 在 prompt 中包含任何 Gnosia 身份資訊

#### Scenario: Guardian Angel 夜間保護
- **WHEN** 夜間階段且 Guardian Angel 存活
- **THEN** GM SHALL 呼叫 Guardian Angel agent 選擇一名保護目標（無連續限制）

#### Scenario: Guardian Angel 可公開身份
- **WHEN** Guardian Angel 在討論中發言
- **THEN** 可以選擇公開身份、推測 Gnosia，但沒有確定情報

### Requirement: Doctor（醫生）— 驗屍能力

Doctor SHALL 屬於船員陣營。Doctor 的夜間能力為**自動查看當日被投票淘汰者的陣營**。
Doctor MUST NOT 有保護能力。

#### Scenario: Doctor 驗屍
- **WHEN** 夜間階段且當日有人被投票淘汰
- **THEN** GM SHALL 自動將被淘汰者的陣營結果（是/不是 Gnosia）記錄，並在下一日的討論 prompt 中告知 Doctor

#### Scenario: 無人被淘汰時
- **WHEN** 夜間階段但當日投票平票（無人被淘汰）
- **THEN** Doctor 今夜無法使用能力

#### Scenario: Doctor 不需要 Launch agent
- **WHEN** 夜間行動階段
- **THEN** GM MUST NOT 呼叫 Doctor agent 進行夜間行動（驗屍為自動處理）

### Requirement: AC Follower（AC 主義者）

AC Follower SHALL 計入船員人數進行勝負判定。AC Follower 被投票淘汰時 GM MUST NOT 公開其身份。

#### Scenario: AC Follower 的勝利條件
- **WHEN** AC Follower 被投票淘汰
- **THEN** AC Follower 達成個人勝利，但 GM MUST NOT 在當場宣佈，SHALL 在遊戲結束時才揭曉

#### Scenario: AC Follower 對勝負判定的影響
- **WHEN** 計算存活人數的陣營比例
- **THEN** AC Follower SHALL 計入船員人數（投掉 AC Follower 等於削弱船員）

### Requirement: Bug（蟲）

Bug SHALL 屬於第三陣營（獨立）。Bug 的勝利條件為遊戲結束時自己仍然存活。

#### Scenario: Bug 的勝利條件
- **WHEN** 遊戲結束且 Bug 仍然存活
- **THEN** GM SHALL 額外宣佈 Bug 個人勝利（與主陣營勝利可疊加）

#### Scenario: Bug 被淘汰
- **WHEN** Bug 被投票淘汰或被 Gnosia 消滅
- **THEN** Bug MUST NOT 獲得勝利

#### Scenario: Bug 的行為策略
- **WHEN** GM 傳入 Bug 身份
- **THEN** 角色 SHALL 盡量保持低調、不被懷疑、避免成為任何人的目標

#### Scenario: Bug 無夜間行動
- **WHEN** 進入夜間階段
- **THEN** GM MUST NOT 向 Bug 發送夜間行動請求

#### Scenario: Bug 對勝負判定的影響
- **WHEN** 計算存活人數的陣營比例
- **THEN** Bug SHALL 不計入船員或 Gnosia 的人數
