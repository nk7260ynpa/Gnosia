## MODIFIED Requirements

### Requirement: Guardian Angel（守護天使）

Guardian Angel SHALL 屬於船員陣營。Guardian Angel MUST NOT 知道任何 Gnosia 的身份。
Guardian Angel SHALL 有夜間行動：保護一名玩家免受 Gnosia 攻擊。無連續保護同一人的限制。
Guardian Angel 可以公開自己的身份並推測 Gnosia，但只是推測，沒有確定情報。

#### Scenario: Guardian Angel 無情報
- **WHEN** 遊戲初始化 Guardian Angel
- **THEN** GM MUST NOT 在 prompt 中包含任何 Gnosia 身份資訊

#### Scenario: Guardian Angel 夜間保護
- **WHEN** 夜間階段且 Guardian Angel 存活
- **THEN** GM SHALL 呼叫 Guardian Angel agent 選擇一名保護目標（無連續限制）

#### Scenario: Guardian Angel 可公開身份
- **WHEN** Guardian Angel 在討論中發言
- **THEN** 可以選擇公開身份、推測 Gnosia，但沒有確定情報

### Requirement: Doctor（醫生）— 驗屍能力

Doctor SHALL 屬於船員陣營。Doctor 的夜間能力為**自動查看當日被投票淘汰者的陣營**。
Doctor MUST NOT 有保護能力。

#### Scenario: Doctor 驗屍
- **WHEN** 夜間階段且當日有人被投票淘汰
- **THEN** GM SHALL 自動將被淘汰者的陣營結果（是/不是 Gnosia）記錄，並在下一日的討論 prompt 中告知 Doctor

#### Scenario: 無人被淘汰時
- **WHEN** 夜間階段但當日投票平票（無人被淘汰）
- **THEN** Doctor 今夜無法使用能力

#### Scenario: Doctor 不需要 Launch agent
- **WHEN** 夜間行動階段
- **THEN** GM MUST NOT 呼叫 Doctor agent 進行夜間行動（驗屍為自動處理）
