## 1. 新角色 Agent 定義

- [x] 1.1 建立 `.claude/agents/shipi.md`（🩵 シピ — 老練世故型, cyan）：frontmatter + 性格定義 + 雙面行為策略 + 新職業行為策略
- [x] 1.2 建立 `.claude/agents/stella.md`（🟠 ステラ — 正義熱血型, red）：frontmatter + 性格定義 + 雙面行為策略 + 新職業行為策略
- [x] 1.3 建立 `.claude/agents/remnant.md`（⚪ レムナン — 沉默寡言型, green）：frontmatter + 性格定義 + 雙面行為策略 + 新職業行為策略

## 2. 更新現有角色 Agent

- [x] 2.1 更新 `setsu.md`：新增 Guardian Angel / AC Follower / Bug 的行為策略段落
- [x] 2.2 更新 `raqio.md`：新增 Guardian Angel / AC Follower / Bug 的行為策略段落
- [x] 2.3 更新 `gina.md`：新增 Guardian Angel / AC Follower / Bug 的行為策略段落
- [x] 2.4 更新 `comet.md`：新增 Guardian Angel / AC Follower / Bug 的行為策略段落
- [x] 2.5 更新 `sq.md`：新增 Guardian Angel / AC Follower / Bug 的行為策略段落

## 3. 更新 GM 指令 — 角色配置

- [x] 3.1 更新 `gnosia.md` 角色對照表：新增シピ、ステラ、レムナン的 subagent_type 和標記
- [x] 3.2 新增人數配置表（5-8 人局）到 `gnosia.md`
- [x] 3.3 新增指令參數支援：`/gnosia [人數]`，預設 5 人

## 4. 更新 GM 指令 — 新職業邏輯

- [x] 4.1 更新 `gnosia.md` 遊戲規則段落：新增 Guardian Angel / AC Follower / Bug 的說明
- [x] 4.2 新增 Guardian Angel 的討論 prompt 模板（含 Gnosia 身份資訊）
- [x] 4.3 新增 AC Follower 的討論 prompt 模板（含「讓自己被投票」的策略指示）
- [x] 4.4 新增 Bug 的討論 prompt 模板（含「保持低調」的策略指示）
- [x] 4.5 更新投票 prompt 模板：新增 Guardian Angel / AC Follower / Bug 的投票策略

## 5. 更新 GM 指令 — 夜間行動與勝負

- [x] 5.1 更新夜間行動邏輯：Guardian Angel / AC Follower / Bug 無夜間行動
- [x] 5.2 更新勝負條件判定：AC Follower 和 Bug 不計入陣營人數
- [x] 5.3 新增 AC Follower 被投票淘汰時的勝利宣告
- [x] 5.4 新增 Bug 存活到結束時的勝利宣告
- [x] 5.5 更新結局輸出格式：支援多方勝利的顯示（主陣營 + 個人勝利）

## 6. 更新 GM 指令 — 資訊隔離

- [x] 6.1 新增 Guardian Angel 的資訊隔離規則到 `gnosia.md`
- [x] 6.2 確認 Gnosia prompt 不包含 Guardian Angel 知情的事實
- [x] 6.3 確認 AC Follower 和 Bug prompt 僅包含公開資訊

## 7. 更新文件

- [x] 7.1 更新 `README.md`：新增角色表（8 個角色）、新職業說明、人數配置表
