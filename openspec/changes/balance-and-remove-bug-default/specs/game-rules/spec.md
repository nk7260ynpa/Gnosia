## MODIFIED Requirements

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

## ADDED Requirements

### Requirement: AC Follower 計入船員人數

AC Follower SHALL 計入船員人數進行勝負判定。

#### Scenario: 勝負判定時的人數計算
- **WHEN** 檢查 Gnosia 勝利條件（Gnosia >= 船員）
- **THEN** AC Follower SHALL 計入船員人數

### Requirement: AC Follower 淘汰不公開身份

#### Scenario: AC Follower 被投票淘汰
- **WHEN** AC Follower 被投票淘汰
- **THEN** GM MUST NOT 公開 AC Follower 身份（保密到遊戲結束），AC Follower 仍達成個人勝利但不宣佈
