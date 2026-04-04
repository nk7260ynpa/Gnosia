## ADDED Requirements

### Requirement: 彩色圓點標記

每個角色 SHALL 在所有輸出中使用專屬彩色圓點標記。

| 角色 | 標記 |
|------|------|
| セツ | 🔴 |
| ラキオ | 🔵 |
| ジナ | 🟢 |
| コメット | 🟡 |
| SQ | 🟣 |

#### Scenario: 發言標記
- **WHEN** 顯示角色發言
- **THEN** 格式 SHALL 為 `🔴 **セツ**：「發言內容」`

#### Scenario: 投票表格標記
- **WHEN** 顯示投票結果表格
- **THEN** 投票者欄位 SHALL 包含彩色圓點

### Requirement: 開場畫面

#### Scenario: 遊戲開始
- **WHEN** 遊戲初始化完成
- **THEN** SHALL 顯示 GNOSIA 標題畫面與角色分配表格（上帝視角）

### Requirement: 日間討論呈現

#### Scenario: 日間標題
- **WHEN** 進入日間討論
- **THEN** SHALL 顯示「第 N 日 — 日間討論」標題、存活者列表、夜間事件結果

#### Scenario: 發言呈現
- **WHEN** 角色完成發言
- **THEN** SHALL 以「🔴 **角色名**：「內容」」格式顯示，按發言順序排列

### Requirement: 投票結果呈現

#### Scenario: 投票表格
- **WHEN** 所有角色完成投票
- **THEN** SHALL 顯示完整投票表格（投票者 | 投票對象）和結果宣告

### Requirement: 夜間行動呈現（上帝視角）

#### Scenario: 夜間行動展示
- **WHEN** 夜間行動完成
- **THEN** SHALL 以上帝視角顯示：Gnosia 攻擊目標、Engineer 掃描結果、Doctor 保護目標、最終結果

### Requirement: 結局呈現

#### Scenario: 遊戲結束
- **WHEN** 某方達成勝利條件
- **THEN** SHALL 顯示：勝利陣營宣告、身份揭曉表格（角色 | 身份 | 結局）、遊戲統計（回合數、投票淘汰數、夜間消滅數、Doctor 保護次數）

### Requirement: 語言規範

#### Scenario: 輸出語言
- **WHEN** GM 產生任何輸出
- **THEN** 所有文字 SHALL 使用繁體中文
