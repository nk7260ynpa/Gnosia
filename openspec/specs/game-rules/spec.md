## ADDED Requirements

### Requirement: 角色配置

5 人局 SHALL 包含以下角色配置：Gnosia x2、Engineer x1、Doctor x1、Crew x1。
每局遊戲 SHALL 從 [Gnosia, Gnosia, Engineer, Doctor, Crew] 中隨機分配給 [セツ, ラキオ, ジナ, コメット, SQ]。

#### Scenario: 角色分配隨機性
- **WHEN** 遊戲初始化時
- **THEN** 5 個身份 SHALL 隨機分配給 5 個角色，每次遊戲的分配結果不同

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
