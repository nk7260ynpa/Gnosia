## Why

Gnosia 角色在 Day 1 幾乎每場都被準確投出，因為 prompt 中過多的「禁止」指令（絕不暴露、不要辯護、假裝中立）導致 Gnosia agent 產生明顯異於正常船員的行為模式——過度謹慎、迴避、防守。AI agent 之間能敏銳捕捉這種「不自然的安全感」，使得偽裝完全失效。

## What Changes

### GM 討論 prompt（Gnosia 部分）
- **移除防守型指令**：刪除「絕不暴露身份或暗示同伴」等負面指令
- **改為正面行為引導**：指示 Gnosia「像普通船員一樣自然地推理和發言」
- **策略提示精簡化**：僅保留投票分散策略，移除過度的行為限制

### GM 投票 prompt（Gnosia 部分）
- 簡化投票策略，不再過度強調分散投票

### Agent 身份行為策略（Gnosia 部分）
- **移除所有 agent 的「不暴露身份或暗示同伴」尾綴**
- **重寫 Gnosia 策略**：從「利用 X 來掩護/引導」改為「像平常一樣 X，同時注意保護同伴」
- 讓 Gnosia 的行為指令與 Crew 版本高度相似，僅多出同伴意識

## Non-Goals

- 不改變 Gnosia 的夜間行動 prompt
- 不改變其他身份（Engineer/Doctor/GA/AC Follower/Bug/Crew）的 prompt
- 不改變角色性格定義
- 不改變遊戲規則或勝負條件

## Capabilities

### New Capabilities

（無新增）

### Modified Capabilities

- `game-master`：Gnosia 的討論和投票 prompt 模板改為正面行為引導
- `character-agents`：15 個角色 agent 的 Gnosia 行為策略重寫

## Impact

- 修改檔案：`.claude/commands/gnosia.md`（討論和投票 prompt）
- 修改檔案：`.claude/agents/*.md`（15 個角色的 Gnosia 策略行）
- 預期效果：Gnosia 在 Day 1 的存活率提升，遊戲更具懸疑性
