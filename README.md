# Gnosia — 太空社交推理遊戲

以 Claude Code 自訂指令實作的 Gnosia（太空狼人殺）社交推理遊戲。
5 個 AI 角色全自動對戰，使用者純觀戰。

## 使用方式

在此專案目錄下啟動 Claude Code，輸入：

```
/gnosia
```

即可開始一場遊戲。

## 遊戲規則

### 角色配置（5人局）

| 陣營 | 角色 | 人數 | 能力 |
|------|------|------|------|
| Gnosia | Gnosia | 2 | 夜間消滅一名船員；互知同伴身份 |
| 船員 | Engineer（工程師） | 1 | 夜間掃描一名玩家，得知是否為 Gnosia |
| 船員 | Doctor（醫生） | 1 | 夜間保護一名玩家（不可連續兩夜同人） |
| 船員 | Crew（船員） | 1 | 無特殊能力 |

### 勝負條件

- **船員勝**：所有 Gnosia 進入冷凍睡眠
- **Gnosia 勝**：存活 Gnosia 數 >= 存活船員數

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

| 角色 | 性格 |
|------|------|
| セツ | 冷靜分析型 — 邏輯推理、簡潔有力 |
| ラキオ | 衝動攻擊型 — 火爆直率、直接質問 |
| ジナ | 策略博弈型 — 假設性提問、策略深度 |
| コメット | 感性直覺型 — 依靠感覺、關心他人 |
| SQ | 神秘計算型 — 疏離感、概率分析 |

## 技術架構

```
/gnosia 啟動
    │
    Claude Code（Game Master, opus）
    │
    ├─ 討論階段：順序 Launch sonnet agent（後者能看到前者發言）
    ├─ 投票階段：並行 Launch sonnet agent（各自獨立投票）
    └─ 夜間階段：並行 Launch sonnet agent（資訊嚴格隔離）
```

- 每個角色的發言和決策由獨立的 sonnet subagent 生成
- 資訊隔離靠 GM 控制每個 agent 的 prompt 內容
- 遊戲狀態在 GM 的對話 context 中自然維持

## 專案架構

```
Gnosia/
├── .claude/
│   └── commands/
│       └── gnosia.md       # 遊戲主指令
├── plan/                    # 設計規格文件
├── .gitignore
└── README.md
```

## 需求

- [Claude Code](https://claude.ai/claude-code) CLI
