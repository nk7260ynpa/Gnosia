## Requirements

### Requirement: Guardian Angel（守護天使）

Guardian Angel SHALL 屬於船員陣營。開局時 GM SHALL 在 prompt 中告知 Guardian Angel 所有 Gnosia 的身份。
Guardian Angel 沒有夜間行動能力。

#### Scenario: Guardian Angel 的資訊優勢
- **WHEN** GM 呼叫 Guardian Angel 的 agent
- **THEN** prompt SHALL 包含所有 Gnosia 的身份資訊

#### Scenario: Guardian Angel 的行為限制
- **WHEN** Guardian Angel 在討論中發言
- **THEN** MUST NOT 直接宣稱「我是守護天使，我知道誰是 Gnosia」，SHALL 用暗示和邏輯引導的方式傳遞資訊

#### Scenario: Guardian Angel 無夜間行動
- **WHEN** 進入夜間階段
- **THEN** GM MUST NOT 向 Guardian Angel 發送夜間行動請求

#### Scenario: Guardian Angel 對 Gnosia 的資訊隔離
- **WHEN** GM 呼叫 Gnosia 的 agent
- **THEN** prompt MUST NOT 包含 Guardian Angel 知道其身份的事實

### Requirement: AC Follower（AC 主義者）

AC Follower SHALL 屬於第三陣營（獨立）。AC Follower 的勝利條件為自己被投票淘汰。
被 Gnosia 夜間消滅 MUST NOT 算作勝利。

#### Scenario: AC Follower 的勝利條件
- **WHEN** AC Follower 被投票淘汰進入冷凍睡眠
- **THEN** GM SHALL 宣佈 AC Follower 個人勝利，遊戲繼續進行

#### Scenario: AC Follower 被夜間消滅
- **WHEN** AC Follower 被 Gnosia 夜間消滅
- **THEN** AC Follower MUST NOT 獲得勝利

#### Scenario: AC Follower 的行為策略
- **WHEN** GM 傳入 AC Follower 身份
- **THEN** 角色 SHALL 故意讓自己顯得可疑，引導他人投票淘汰自己

#### Scenario: AC Follower 無夜間行動
- **WHEN** 進入夜間階段
- **THEN** GM MUST NOT 向 AC Follower 發送夜間行動請求

#### Scenario: AC Follower 對勝負判定的影響
- **WHEN** 計算存活人數的陣營比例
- **THEN** AC Follower SHALL 不計入船員或 Gnosia 的人數

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
