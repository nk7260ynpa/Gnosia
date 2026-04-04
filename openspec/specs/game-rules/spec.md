## Requirements

### Requirement: 角色配置

遊戲 SHALL 支援 5-15 人局。GM SHALL 根據人數從預設配置表中選擇角色配置。
角色池擴充至 15 個角色。

預設配置表：

| 人數 | Gnosia | Engineer | Doctor | Guardian Angel | AC Follower | Bug | Crew |
|------|--------|----------|--------|----------------|-------------|-----|------|
| 5 | 2 | 1 | 1 | 0 | 0 | 0 | 1 |
| 6 | 2 | 1 | 1 | 1 | 0 | 0 | 1 |
| 7 | 2 | 1 | 1 | 1 | 1 | 0 | 1 |
| 8 | 2 | 1 | 1 | 1 | 1 | 1 | 1 |
| 9 | 3 | 1 | 1 | 1 | 1 | 1 | 1 |
| 10 | 3 | 2 | 1 | 1 | 1 | 1 | 1 |
| 11 | 3 | 2 | 1 | 1 | 1 | 1 | 2 |
| 12 | 3 | 2 | 2 | 1 | 1 | 1 | 2 |
| 13 | 4 | 2 | 2 | 1 | 1 | 1 | 2 |
| 14 | 4 | 2 | 2 | 1 | 1 | 1 | 3 |
| 15 | 4 | 2 | 2 | 1 | 1 | 1 | 4 |

#### Scenario: 角色分配隨機性
- **WHEN** 遊戲初始化時
- **THEN** GM SHALL 從 15 個角色中隨機選取對應人數的角色，再隨機分配身份

#### Scenario: 多 Engineer 配置
- **WHEN** 人數 >= 10
- **THEN** 配置 SHALL 包含 2 名 Engineer，各自獨立掃描

#### Scenario: 多 Doctor 配置
- **WHEN** 人數 >= 12
- **THEN** 配置 SHALL 包含 2 名 Doctor，各自獨立保護

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

#### Scenario: Gnosia 攻擊
- **WHEN** 夜間階段且有 Gnosia 存活
- **THEN** Gnosia SHALL 選擇一名非 Gnosia 的存活玩家進行攻擊

#### Scenario: Engineer 掃描
- **WHEN** 夜間階段且 Engineer 存活
- **THEN** Engineer SHALL 選擇一名存活玩家進行掃描，得知其是否為 Gnosia

#### Scenario: Doctor 保護
- **WHEN** 夜間階段且 Doctor 存活
- **THEN** Doctor SHALL 選擇一名存活玩家進行保護。Doctor MUST NOT 連續兩夜保護同一人

#### Scenario: Doctor 成功保護
- **WHEN** Gnosia 攻擊目標等於 Doctor 保護目標
- **THEN** 攻擊被擋，無人死亡

#### Scenario: 攻擊成功
- **WHEN** Gnosia 攻擊目標不等於 Doctor 保護目標
- **THEN** 被攻擊者進入冷凍睡眠

### Requirement: AC Follower 勝利條件

#### Scenario: AC Follower 被投票淘汰
- **WHEN** AC Follower 被投票淘汰進入冷凍睡眠
- **THEN** GM SHALL 宣佈 AC Follower 個人勝利，遊戲繼續

#### Scenario: AC Follower 被夜間消滅
- **WHEN** AC Follower 被 Gnosia 夜間消滅
- **THEN** AC Follower MUST NOT 獲得勝利

### Requirement: Bug 勝利條件

#### Scenario: Bug 存活到結束
- **WHEN** 遊戲結束且 Bug 仍然存活
- **THEN** GM SHALL 額外宣佈 Bug 個人勝利

### Requirement: 第三陣營的人數計算

AC Follower 和 Bug SHALL 不計入船員或 Gnosia 的存活人數。

#### Scenario: 勝負判定時的人數計算
- **WHEN** 檢查 Gnosia 勝利條件（Gnosia >= 船員）
- **THEN** AC Follower 和 Bug 的存活人數 MUST NOT 計入任何一方

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
