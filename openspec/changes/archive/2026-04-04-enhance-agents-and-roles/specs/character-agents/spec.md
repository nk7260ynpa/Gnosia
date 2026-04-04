## MODIFIED Requirements

### Requirement: 角色配置

系統 SHALL 定義 8 個角色 agent：

| 角色 | 檔案名 | 顏色 | 標記 |
|------|--------|------|------|
| セツ | setsu.md | red | 🔴 |
| ラキオ | raqio.md | blue | 🔵 |
| ジナ | gina.md | green | 🟢 |
| コメット | comet.md | yellow | 🟡 |
| SQ | sq.md | magenta | 🟣 |
| シピ | shipi.md | cyan | 🩵 |
| ステラ | stella.md | red | 🟠 |
| レムナン | remnant.md | green | ⚪ |

#### Scenario: 角色 agent 數量
- **WHEN** 列出所有可用角色 agent
- **THEN** SHALL 有 8 個 agent 定義檔，每個包含完整的 frontmatter 和系統提示

## ADDED Requirements

### Requirement: 新職業行為策略

每個角色 agent SHALL 支援所有可能被分配的職業身份，包括新增的 Guardian Angel、AC Follower、Bug。

#### Scenario: 角色被分配為 Guardian Angel
- **WHEN** GM 傳入 Guardian Angel 身份（含 Gnosia 名單）
- **THEN** 角色 SHALL 利用已知資訊暗示和引導討論，MUST NOT 直接宣稱知道 Gnosia 身份

#### Scenario: 角色被分配為 AC Follower
- **WHEN** GM 傳入 AC Follower 身份
- **THEN** 角色 SHALL 故意讓自己顯得可疑，引導他人投票淘汰自己

#### Scenario: 角色被分配為 Bug
- **WHEN** GM 傳入 Bug 身份
- **THEN** 角色 SHALL 盡量保持低調、附和多數意見、避免成為目標
