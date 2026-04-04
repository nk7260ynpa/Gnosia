## Context

使用者希望在 Claude Code CLI 中建立一個多 Agent 社交推理遊戲，
不使用 Claude API，完全透過 Claude CLI 的 Agent 系統驅動。

## Goals

- 5 個 AI 角色全自動對戰，性格一致且可區分
- 資訊隔離確保遊戲公平
- 觀戰者能清楚跟蹤遊戲進程

## Non-Goals

- 持久 Agent（SendMessage 在當前環境不可用）
- 使用者參與遊戲

## Decisions

### 1. Agent 架構：獨立 agent 定義檔

**選擇**：每個角色一個 `.claude/agents/*.md` 定義檔，透過 `subagent_type` 呼叫
**理由**：角色性格固定在 agent 定義中，遊戲身份由 GM 動態傳入，實現關注點分離
**替代方案**：
- 持久 Agent + SendMessage：環境不支援
- 每次 Launch 新 agent 並在 prompt 中嵌入完整性格：prompt 冗長且性格不一致
- Python 腳本 + `claude -p`：需要額外腳本，不夠優雅

### 2. GM 模型選擇

**選擇**：GM 使用 opus，角色 agent 使用 sonnet
**理由**：GM 需要管理複雜遊戲邏輯和資訊隔離，opus 更可靠；角色發言用 sonnet 平衡品質與速度

### 3. 資訊隔離策略

**選擇**：GM 控制每次 agent prompt 的內容
**理由**：每次 agent 呼叫是獨立 context，天然隔離。GM 只需確保不把私密資訊放入錯誤角色的 prompt

### 4. 討論順序：順序生成

**選擇**：每輪討論按順序逐一呼叫 agent（後者能看到前者發言）
**理由**：社交推理的核心是「反應」和「對話」，順序生成讓角色能回應彼此，製造爭論和互動
**替代方案**：並行生成——會導致自說自話

### 5. 視覺區分：彩色圓點

**選擇**：🔴🔵🟢🟡🟣 + agent 定義的 color 屬性
**理由**：終端不支援背景色，emoji 圓點是最直觀的區分方式

## Risks / Trade-offs

- **Agent 調用量大**（每局約 30-50 次）→ 可透過減少討論輪數優化
- **角色語言問題**（ラキオ agent 曾回傳日文）→ 在 prompt 中強調繁體中文
- **性格一致性**（非持久 agent，每次獨立 context）→ agent 定義檔提供穩定的性格基底
