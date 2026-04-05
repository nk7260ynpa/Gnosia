## ADDED Requirements

### Requirement: Engineer 掃描模糊機制

每次 Engineer 掃描 SHALL 有 25% 機率回傳「無法判定」。GM SHALL 在夜間結果解析時擲骰決定。

#### Scenario: 掃描成功（75%）
- **WHEN** GM 解析 Engineer 掃描結果且擲骰結果為 2-4（75%）
- **THEN** Engineer SHALL 收到正常掃描結果（「是 Gnosia」或「不是 Gnosia」）

#### Scenario: 掃描模糊（25%）
- **WHEN** GM 解析 Engineer 掃描結果且擲骰結果為 1（25%）
- **THEN** Engineer SHALL 收到「無法判定」，MUST NOT 收到具體結果

#### Scenario: 模糊結果的呈現
- **WHEN** Engineer 收到「無法判定」結果
- **THEN** 下一輪討論 prompt 中 SHALL 顯示「掃描結果：【角色名】→ 無法判定」
