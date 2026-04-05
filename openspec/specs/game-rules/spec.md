## Requirements

### Requirement: 角色配置

遊戲 SHALL 支援 5-15 人局。預設配置表中 Bug 位置改為 Crew。Bug 可透過指令參數手動啟用。

預設配置表（無 Bug）：

| 人數 | Gnosia | Engineer | Doctor | Guardian Angel | AC Follower | Crew |
|------|--------|----------|--------|----------------|-------------|------|
| 5 | 2 | 1 | 1 | 0 | 0 | 1 |
| 6 | 2 | 1 | 1 | 1 | 0 | 1 |
| 7 | 2 | 1 | 1 | 1 | 1 | 1 |
| 8 | 2 | 1 | 1 | 1 | 1 | 2 |
| 9 | 3 | 1 | 1 | 1 | 1 | 2 |
| 10 | 3 | 2 | 1 | 1 | 1 | 2 |
| 11 | 3 | 2 | 1 | 1 | 1 | 3 |
| 12 | 4 | 2 | 2 | 1 | 1 | 2 |
| 13 | 4 | 2 | 2 | 1 | 1 | 3 |
| 14 | 5 | 2 | 2 | 1 | 1 | 3 |
| 15 | 5 | 2 | 2 | 1 | 1 | 4 |

#### Scenario: 預設無 Bug
- **WHEN** 使用者未指定 bug 參數
- **THEN** 配置 SHALL 不包含 Bug，Bug 位置改為 Crew

#### Scenario: 手動啟用 Bug
- **WHEN** 使用者指定 bug 參數（如 `/gnosia 8 bug`）
- **THEN** 配置 SHALL 包含 1 個 Bug，從 Crew 中扣除 1 人

### Requirement: 勝負條件

#### Scenario: 船員陣營勝利
- **WHEN** 所有 Gnosia 進入冷凍睡眠
- **THEN** 遊戲結束，船員陣營勝利

#### Scenario: Gnosia 陣營勝利
- **WHEN** 存活的 Gnosia 人數 >= 存活的船員人數
- **THEN** 遊戲結束，Gnosia 陣營勝利

### Requirement: 日間討論

每個白天 SHALL 進行 2 輪討論。每輪中所有存活角色 SHALL 按隨機順序各發言一次。
第 2 輪的發言順序 SHALL 為第 1 輪的反轉。

#### Scenario: 第一天討論
- **WHEN** 第 1 天日間討論開始
- **THEN** GM SHALL 宣佈「沒有夜間事件」，直接進入討論

#### Scenario: 非第一天討論
- **WHEN** 第 N 天（N > 1）日間討論開始
- **THEN** GM SHALL 先公佈夜間結果（是否有人被消滅），再進入討論

### Requirement: 投票機制

討論結束後所有存活角色 SHALL 進行投票。每人投一票，不可投自己。

#### Scenario: 最高票淘汰
- **WHEN** 某角色獲得最多票且非平票
- **THEN** 該角色進入冷凍睡眠，其真實身份 MUST NOT 公佈（直到遊戲結束）

#### Scenario: 平票處理
- **WHEN** 投票結果出現平票
- **THEN** 無人被淘汰，直接進入夜間階段

### Requirement: 夜間行動

#### Scenario: 有夜間行動的角色
- **WHEN** 進入夜間階段
- **THEN** GM SHALL 呼叫 Gnosia（攻擊）、Engineer（掃描）、Guardian Angel（保護）。Doctor 驗屍為自動處理。AC Follower、Bug、Crew 無夜間行動。

### Requirement: 保護判定

#### Scenario: 攻擊被 GA 擋住
- **WHEN** Gnosia 攻擊目標被 Guardian Angel 保護
- **THEN** 攻擊被擋，無人死亡

### Requirement: AC Follower 勝利條件

#### Scenario: AC Follower 被投票淘汰
- **WHEN** AC Follower 被投票淘汰進入冷凍睡眠
- **THEN** AC Follower 達成個人勝利，但 GM MUST NOT 在當場宣佈，SHALL 在遊戲結束時才揭曉

#### Scenario: AC Follower 被夜間消滅
- **WHEN** AC Follower 被 Gnosia 夜間消滅
- **THEN** AC Follower MUST NOT 獲得勝利

### Requirement: Bug 勝利條件

#### Scenario: Bug 存活到結束
- **WHEN** 遊戲結束且 Bug 仍然存活
- **THEN** GM SHALL 額外宣佈 Bug 個人勝利

### Requirement: AC Follower 計入船員人數

AC Follower SHALL 計入船員人數進行勝負判定。

#### Scenario: 勝負判定時的人數計算
- **WHEN** 檢查 Gnosia 勝利條件（Gnosia >= 船員）
- **THEN** AC Follower SHALL 計入船員人數

### Requirement: AC Follower 淘汰不公開身份

#### Scenario: AC Follower 被投票淘汰
- **WHEN** AC Follower 被投票淘汰
- **THEN** GM MUST NOT 公開 AC Follower 身份（保密到遊戲結束），AC Follower 仍達成個人勝利但不宣佈

### Requirement: 討論輪數控制

#### Scenario: 小型局討論
- **WHEN** 人數為 5-7
- **THEN** 討論 SHALL 進行 2 輪

#### Scenario: 中大型局討論
- **WHEN** 人數為 8-15
- **THEN** 討論 SHALL 進行 1 輪

### Requirement: Gnosia 攻擊代表制

#### Scenario: 多 Gnosia 攻擊決策
- **WHEN** 夜間階段且有多個 Gnosia 存活
- **THEN** GM SHALL 僅呼叫 1 個 Gnosia agent（存活的第一個）做攻擊決策
