## Why

目前遊戲僅有 5 個角色（セツ、ラキオ、ジナ、コメット、SQ）和 4 種職業（Gnosia、Engineer、Doctor、Crew），
每局的角色組合變化有限。需要擴充角色陣容和職業種類，增加遊戲的重玩性和策略深度。

## What Changes

- 新增 Gnosia 原作角色 agent：シピ（Shipi）、ステラ（Stella）、レムナン（Remnant）
- 新增遊戲職業：Guardian Angel（守護天使）、AC Follower（AC 主義者）、Bug（蟲）
- 擴充 GM 支援 5-8 人局的角色配置表
- 更新 GM 的夜間行動邏輯以支援新職業
- 更新 GM 的勝負條件判定（AC Follower 和 Bug 的特殊勝利條件）

## Non-Goals

- 超過 8 人的遊戲模式
- 使用者參與遊戲（維持觀戰模式）
- 角色 agent 的持久記憶（memory: project）
- 原作中所有角色的完整移植（僅挑選代表性角色）

## Capabilities

### New Capabilities
- `new-character-agents`：3 個新角色 agent（シピ、ステラ、レムナン）的性格與說話風格定義
- `advanced-roles`：3 個新職業（Guardian Angel、AC Follower、Bug）的能力與行為規則

### Modified Capabilities
- `game-rules`：擴充角色配置表支援 5-8 人局，新增特殊勝利條件
- `character-agents`：更新角色對照表，納入新角色
- `game-master`：擴充 GM 的夜間行動邏輯和 Agent 呼叫模板，支援新職業的行動與勝負判定

## Impact

- 新增檔案：`.claude/agents/shipi.md`、`.claude/agents/stella.md`、`.claude/agents/remnant.md`
- 修改檔案：`.claude/commands/gnosia.md`（GM 流程、角色配置、夜間邏輯、勝負條件）
- 修改檔案：`README.md`（角色表、規則說明）
