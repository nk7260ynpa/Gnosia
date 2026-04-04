## Why

經過 9 場實測，船員陣營勝率高達 89%（8/9），Gnosia 僅贏 1 場。主要失衡原因：
1. **Engineer 掃描太強**：100% 準確率 + 每夜都能掃描，通常 1-2 夜就找到 Gnosia
2. **Doctor 預判太準**：AI agent 經常正確猜到攻擊目標，成功保護率極高
3. **Guardian Angel 暗示太有效**：知道所有 Gnosia 身份，暗示幾乎每次都被船員採納
4. **AC Follower 完全無效**：9 場 0 勝，船員永遠有更明確的投票目標
5. **Bug 太安全**：存在時 100% 存活，對遊戲毫無影響

此外，使用者要求預設不加入 Bug。

## What Changes

- **BREAKING**：預設配置表移除 Bug，Bug 位置改為額外 Crew
- **Guardian Angel 削弱**：從「知道所有 Gnosia」改為「只知道 1 個隨機 Gnosia」
- **Engineer 限制**：掃描結果有 25% 機率為「無法判定」（非假結果，是模糊結果）
- **Gnosia 增強**：討論 prompt 加入「同伴策略提示」，讓 Gnosia 在討論中更有方向感
- **AC Follower 增強**：AC Follower 被淘汰時不再公開身份，增加混亂度。同時 AC Follower 計入船員人數（投掉 AC Follower 等於損失一票）
- **配置表微調**：5 人局 Gnosia 維持 2 人，但 7+ 人局 Guardian Angel 只知道 1 個 Gnosia

## Non-Goals

- 改變角色性格或 agent 定義
- 新增角色或職業
- 修改輸出格式

## Capabilities

### New Capabilities
- `engineer-scan-fuzzy`：Engineer 掃描模糊機制（25% 無法判定）

### Modified Capabilities
- `game-rules`：移除 Bug 預設、AC Follower 計入船員、配置表調整
- `game-master`：Guardian Angel 只知 1 個 Gnosia、Engineer 模糊掃描、Gnosia 策略提示、AC Follower 淘汰不公開身份
- `advanced-roles`：Guardian Angel 和 AC Follower 規則修改

## Impact

- 修改檔案：`.claude/commands/gnosia.md`（配置表、GA 規則、Engineer 規則、AC 規則、Gnosia prompt）
- 修改檔案：`README.md`（配置表、職業說明）
