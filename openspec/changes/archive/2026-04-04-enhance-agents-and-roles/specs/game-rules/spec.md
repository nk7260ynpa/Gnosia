## MODIFIED Requirements

### Requirement: 角色配置

遊戲 SHALL 支援 5-8 人局。GM SHALL 根據人數從預設配置表中選擇角色配置。
每局遊戲 SHALL 從可用角色池中隨機選取對應人數的角色，再隨機分配身份。

可用角色池：セツ、ラキオ、ジナ、コメット、SQ、シピ、ステラ、レムナン

預設配置表：

| 人數 | Gnosia | Engineer | Doctor | Guardian Angel | AC Follower | Bug | Crew |
|------|--------|----------|--------|----------------|-------------|-----|------|
| 5 | 2 | 1 | 1 | 0 | 0 | 0 | 1 |
| 6 | 2 | 1 | 1 | 1 | 0 | 0 | 1 |
| 7 | 2 | 1 | 1 | 1 | 1 | 0 | 1 |
| 8 | 2 | 1 | 1 | 1 | 1 | 1 | 1 |

#### Scenario: 角色分配隨機性
- **WHEN** 遊戲初始化時
- **THEN** GM SHALL 先從角色池隨機選取對應人數的角色，再將身份隨機分配，每次遊戲結果不同

#### Scenario: 5 人局配置
- **WHEN** 遊戲人數為 5
- **THEN** 配置 SHALL 為 Gnosia x2、Engineer x1、Doctor x1、Crew x1

#### Scenario: 6 人局配置
- **WHEN** 遊戲人數為 6
- **THEN** 配置 SHALL 為 Gnosia x2、Engineer x1、Doctor x1、Guardian Angel x1、Crew x1

#### Scenario: 7 人局配置
- **WHEN** 遊戲人數為 7
- **THEN** 配置 SHALL 為 Gnosia x2、Engineer x1、Doctor x1、Guardian Angel x1、AC Follower x1、Crew x1

#### Scenario: 8 人局配置
- **WHEN** 遊戲人數為 8
- **THEN** 配置 SHALL 為 Gnosia x2、Engineer x1、Doctor x1、Guardian Angel x1、AC Follower x1、Bug x1、Crew x1

## ADDED Requirements

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
