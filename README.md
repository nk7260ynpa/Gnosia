# Gnosia — 太空社交推理遊戲

以 Claude Code 自訂指令與 Agent 系統實作的 Gnosia（太空狼人殺）社交推理遊戲。
5-8 個 AI 角色全自動對戰，使用者純觀戰。

## 使用方式

在此專案目錄下啟動 Claude Code，輸入：

```
/gnosia        # 預設 5 人局
/gnosia 6      # 6 人局（含守護天使）
/gnosia 7      # 7 人局（含 AC 主義者）
/gnosia 8      # 8 人局（完整陣容）
```

## 遊戲規則

### 人數配置表

| 人數 | Gnosia | Engineer | Doctor | Guardian Angel | AC Follower | Bug | Crew |
|------|--------|----------|--------|----------------|-------------|-----|------|
| 5 | 2 | 1 | 1 | 0 | 0 | 0 | 1 |
| 6 | 2 | 1 | 1 | 1 | 0 | 0 | 1 |
| 7 | 2 | 1 | 1 | 1 | 1 | 0 | 1 |
| 8 | 2 | 1 | 1 | 1 | 1 | 1 | 1 |

### 職業說明

| 職業 | 陣營 | 能力 |
|------|------|------|
| Gnosia | Gnosia | 夜間消滅一名船員；互知同伴身份 |
| Engineer（工程師） | 船員 | 夜間掃描一名玩家，得知是否為 Gnosia |
| Doctor（醫生） | 船員 | 夜間保護一名玩家（不可連續兩夜同人） |
| Guardian Angel（守護天使） | 船員 | 開局知道所有 Gnosia 身份，但無夜間行動 |
| AC Follower（AC 主義者） | 獨立 | 勝利條件：被投票淘汰 |
| Bug（蟲） | 獨立 | 勝利條件：存活到遊戲結束 |
| Crew（船員） | 船員 | 無特殊能力 |

### 勝負條件

- **船員勝**：所有 Gnosia 進入冷凍睡眠
- **Gnosia 勝**：存活 Gnosia 數 >= 存活船員數（AC Follower 和 Bug 不計入）
- **AC Follower 個人勝**：被投票淘汰時立即宣佈（遊戲繼續）
- **Bug 個人勝**：遊戲結束時仍存活（可與主陣營勝利疊加）

### 回合流程

```
日間討論（2 輪順序發言）
    ↓
投票（最高票進冷凍睡眠，平票跳過）
    ↓
夜間行動（Gnosia 攻擊 / Engineer 掃描 / Doctor 保護）
    ↓
重複直到某方獲勝
```

## 角色（Gnosia 原作）

| 角色 | 標記 | 性格 |
|------|------|------|
| セツ | 🔴 | 冷靜分析型 — 邏輯推理、簡潔有力 |
| ラキオ | 🔵 | 衝動攻擊型 — 火爆直率、直接質問 |
| ジナ | 🟢 | 策略博弈型 — 假設性提問、策略深度 |
| コメット | 🟡 | 感性直覺型 — 依靠感覺、關心他人 |
| SQ | 🟣 | 神秘計算型 — 疏離感、概率分析 |
| シピ | 🩵 | 老練世故型 — 圓滑觀察、幕後操盤 |
| ステラ | 🟠 | 正義熱血型 — 重視公平、為人辯護 |
| レムナン | ⚪ | 沉默寡言型 — 話少精準、一語中的 |

## 技術架構

```
/gnosia [人數] 啟動
    │
    Claude Code（Game Master, opus）
    │
    ├─ 從 8 個角色中隨機選取 N 個
    ├─ 依人數配置表分配職業
    ├─ 討論階段：順序 Launch 角色 agent（subagent_type）
    ├─ 投票階段：並行 Launch 角色 agent
    └─ 夜間階段：Launch Gnosia/Engineer/Doctor agent（資訊隔離）
```

- **獨立 Agent 架構**：每個角色有專屬的 agent 定義檔（`.claude/agents/*.md`）
- 角色性格固定在 agent 定義中，遊戲身份由 GM 動態傳入
- 資訊隔離靠 GM 控制傳入每個 agent 的 prompt 內容
- 遊戲狀態在 GM 的對話 context 中自然維持

## 專案架構

```
Gnosia/
├── .claude/
│   ├── agents/
│   │   ├── setsu.md        # 🔴 セツ — 冷靜分析型
│   │   ├── raqio.md        # 🔵 ラキオ — 衝動攻擊型
│   │   ├── gina.md         # 🟢 ジナ — 策略博弈型
│   │   ├── comet.md        # 🟡 コメット — 感性直覺型
│   │   ├── sq.md           # 🟣 SQ — 神秘計算型
│   │   ├── shipi.md        # 🩵 シピ — 老練世故型
│   │   ├── stella.md       # 🟠 ステラ — 正義熱血型
│   │   └── remnant.md      # ⚪ レムナン — 沉默寡言型
│   └── commands/
│       └── gnosia.md       # 遊戲主指令（GM）
├── openspec/                # 專案規格文件
├── plan/                    # 設計規格文件
├── .gitignore
└── README.md
```

## 需求

- [Claude Code](https://claude.ai/claude-code) CLI
