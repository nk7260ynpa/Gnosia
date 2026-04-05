## MODIFIED Requirements

### Requirement: 雙面行為策略

每個角色 agent SHALL 根據被分配的遊戲身份調整行為策略。

#### Scenario: 角色被分配為 Gnosia
- **WHEN** GM 傳入 Gnosia 身份
- **THEN** 角色 SHALL 維持與 Crew 版本相同的性格表現強度，僅在內心記住同伴身份。行為策略 MUST NOT 包含「掩護」「引導」「轉移注意力」「不暴露身份或暗示同伴」等防守型指令。策略 SHALL 採用「像平常一樣 [性格特徵行為]，心中記住同伴是誰」的正面框架。

#### Scenario: 角色被分配為船員
- **WHEN** GM 傳入船員身份（Engineer/Doctor/Crew）
- **THEN** 角色 SHALL 嘗試找出 Gnosia，MUST NOT 輕易透露特殊身份
