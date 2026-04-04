## 1-3. 基礎架構

- [x] 1.1 建立專案目錄結構（.claude/commands/, .claude/agents/）
- [x] 1.2 建立 .gitignore（排除 log, CLAUDE.md, plan/）
- [x] 1.3 建立 README.md（使用方式、遊戲規則、專案架構）

## 4. GM 主控指令

- [x] 4.1 建立 gnosia.md 基礎框架（frontmatter, 遊戲規則, 角色定義）
- [x] 4.2 實作遊戲流程指令（初始化 → 討論 → 投票 → 夜間 → 結局）
- [x] 4.3 實作 Agent Prompt 模板（討論/投票/夜間行動三種）
- [x] 4.4 實作輸出格式規範（開場/討論/投票/夜間/結局）
- [x] 4.5 實作資訊隔離邏輯說明

## 5-9. 角色 Agent 定義

- [x] 5.1 建立 setsu.md（🔴 セツ — 冷靜分析型, red）
- [x] 6.1 建立 raqio.md（🔵 ラキオ — 衝動攻擊型, blue）
- [x] 7.1 建立 gina.md（🟢 ジナ — 策略博弈型, green）
- [x] 8.1 建立 comet.md（🟡 コメット — 感性直覺型, yellow）
- [x] 9.1 建立 sq.md（🟣 SQ — 神秘計算型, magenta）

## 10. 架構迭代

- [x] 10.1 嘗試持久 Agent 架構（SendMessage）→ 環境不支援，回退
- [x] 10.2 改用 subagent_type 呼叫自訂 agent → 需重啟 CLI 載入
- [x] 10.3 修正 @提及語法 → 確認 subagent_type 正確運作
- [x] 10.4 實機驗證完整遊戲流程（3 場測試遊戲）
