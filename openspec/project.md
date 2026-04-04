# Gnosia — 太空社交推理遊戲

## 概述

以 Claude Code 自訂指令與 agent 定義檔實作的 Gnosia（太空狼人殺）社交推理遊戲。
5 個 AI 角色全自動對戰，使用者以上帝視角觀戰。每個角色擁有獨立的 agent 定義檔，
包含固定的性格與說話風格，遊戲身份由 GM 每局隨機分配。

## 目標

- 實現 5 人局的完整社交推理遊戲流程（討論、投票、夜間行動）
- 每個角色展現獨特且一致的性格表現
- 透過資訊隔離確保 Gnosia 與船員的公平博弈
- 提供觀戰者清晰易讀的遊戲過程呈現

## 核心功能模組

### 遊戲主控（Game Master）
- 隨機分配角色身份
- 管理遊戲回合流程
- 控制資訊隔離
- 解析夜間行動結果
- 判斷勝負條件

### 角色 Agent 系統
- 5 個獨立角色 agent（セツ、ラキオ、ジナ、コメット、SQ）
- 固定性格定義與說話風格
- 動態接收遊戲身份（Gnosia/Engineer/Doctor/Crew）
- 支援討論發言、投票決策、夜間行動

### 遊戲規則引擎
- 5 人局角色配置（Gnosia x2、Engineer x1、Doctor x1、Crew x1）
- 日間討論（2 輪順序發言）
- 投票淘汰機制（平票跳過）
- 夜間行動系統（攻擊、掃描、保護）
- 勝負條件判定

### 觀戰呈現
- 彩色圓點標記區分角色
- 上帝視角顯示所有隱藏資訊
- 格式化的討論、投票、夜間行動呈現
- 結局統計與回顧

## 技術規格

- **平台**：Claude Code CLI
- **GM 模型**：opus（複雜遊戲邏輯管理）
- **角色 Agent 模型**：sonnet（平衡品質與速度）
- **指令系統**：`.claude/commands/gnosia.md`
- **Agent 系統**：`.claude/agents/*.md`
- **語言**：繁體中文（對話與文件）

## 開發規範

- 程式碼註解使用繁體中文
- Git commit 遵循 Conventional Commits（繁體中文）
- Markdown 遵循 Google Markdown Style Guide
- Agent 定義檔遵循 Claude Code agent 規格（name, description, model, color）

## 規格清單

| 規格 | 說明 | 狀態 |
|------|------|------|
| [game-rules](specs/game-rules/spec.md) | 遊戲規則與勝負條件（5-15 人局） | active |
| [character-agents](specs/character-agents/spec.md) | 角色 agent 定義規格（15 角色） | active |
| [game-master](specs/game-master/spec.md) | GM 流程控制與資訊隔離 | active |
| [output-format](specs/output-format/spec.md) | 觀戰者輸出格式規範 | active |
| [new-character-agents](specs/new-character-agents/spec.md) | 新增角色（シピ、ステラ、レムナン） | active |
| [advanced-roles](specs/advanced-roles/spec.md) | 進階職業（Guardian Angel、AC Follower、Bug） | active |
| [expanded-character-agents](specs/expanded-character-agents/spec.md) | 擴充角色（ジョナス等 7 人） | active |
