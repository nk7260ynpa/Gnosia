## MODIFIED Requirements

### Requirement: 資訊隔離

GM MUST 嚴格控制傳入每個 agent 的資訊內容。

#### Scenario: Guardian Angel 的私密資訊
- **WHEN** 呼叫 Guardian Angel 角色的 agent
- **THEN** prompt SHALL 僅包含 1 個隨機選取的 Gnosia 身份（而非全部），MUST NOT 包含 Engineer 掃描結果或 Doctor 保護歷史

#### Scenario: Gnosia 的策略提示
- **WHEN** 呼叫 Gnosia 角色的 agent 進行討論
- **THEN** prompt SHALL 包含策略提示段落，提醒不要和同伴投票方向一致、適時附和船員指控、不要急著為同伴辯護

#### Scenario: Engineer 模糊掃描結果
- **WHEN** 呼叫 Engineer 角色的 agent 且上一夜掃描結果為「無法判定」
- **THEN** prompt SHALL 顯示「掃描結果：【角色名】→ 無法判定」

#### Scenario: AC Follower 淘汰不公開
- **WHEN** AC Follower 被投票淘汰
- **THEN** GM MUST NOT 在投票結果中宣佈「AC Follower 個人勝利」，SHALL 在遊戲結束時才揭曉

## ADDED Requirements

### Requirement: Gnosia 策略提示模板

GM SHALL 在 Gnosia 的討論 prompt 中加入策略提示。

#### Scenario: Gnosia 討論 prompt
- **WHEN** GM 呼叫 Gnosia agent 進行討論
- **THEN** prompt SHALL 包含以下策略提示：
  - 目前局勢（存活 Gnosia 數 vs 船員數）
  - 不要和同伴投票方向一致
  - 適時附和船員的指控方向
  - 若同伴被質疑，不要急著辯護
  - 可以假裝質疑同伴以建立可信度

### Requirement: Engineer 掃描解析

#### Scenario: GM 解析掃描結果
- **WHEN** 夜間結果解析 Engineer 掃描
- **THEN** GM SHALL 擲骰（1-4），若結果為 1 則掃描結果改為「無法判定」
