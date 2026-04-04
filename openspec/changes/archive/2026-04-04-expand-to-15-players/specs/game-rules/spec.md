## MODIFIED Requirements

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

## ADDED Requirements

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
