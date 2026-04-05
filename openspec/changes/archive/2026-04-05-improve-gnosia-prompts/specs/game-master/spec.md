## MODIFIED Requirements

### Requirement: 資訊隔離

#### Scenario: Gnosia 的資訊限制
- **WHEN** 呼叫 Gnosia 角色的 agent 進行討論
- **THEN** prompt SHALL 包含同伴身份、存活人數局勢，MUST NOT 包含 Engineer 掃描結果、Doctor 驗屍結果、Guardian Angel 保護歷史。prompt MUST NOT 包含「絕不」「假裝」「掩護」等防守型指令。

## ADDED Requirements

### Requirement: Gnosia 討論 prompt 設計原則

Gnosia 的討論 prompt SHALL 採用「自然行為引導」而非「禁止清單」。prompt 的核心指令 SHALL 為引導 Gnosia 像普通船員一樣自然發言，僅附帶最低限度的同伴保護意識。

#### Scenario: Gnosia 討論 prompt 內容
- **WHEN** GM 建構 Gnosia 角色的討論 prompt
- **THEN** 身份描述 SHALL 為：「你是 Gnosia。你的同伴是【X】。像普通船員一樣自然地參與討論——推理、質疑、表達立場。你的性格不會因為身份而改變。唯一的額外意識：保護同伴不被投票淘汰，但用自然的方式。」

#### Scenario: Gnosia 策略提示
- **WHEN** GM 建構 Gnosia 角色的討論 prompt
- **THEN** 策略提示 SHALL 僅包含：局勢資訊（存活 Gnosia/船員人數）和投票分散提醒（避免和同伴投同一人）。MUST NOT 包含「不要急著辯護」「假裝中立」「假裝質疑同伴」等行為管控指令。

### Requirement: Gnosia 投票 prompt 設計原則

#### Scenario: Gnosia 投票 prompt 內容
- **WHEN** GM 建構 Gnosia 角色的投票 prompt
- **THEN** 投票指引 SHALL 為：「投你覺得對船員來說最合理的目標，但避免和同伴投同一人」。MUST NOT 使用「淘汰船員」等暴露 Gnosia 目標的措辭。
