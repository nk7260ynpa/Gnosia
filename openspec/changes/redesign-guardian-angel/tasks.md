## 1. 更新 GM 指令 — Guardian Angel 重設計

- [x] 1.1 修改 `gnosia.md` 職業說明：GA 無情報、有夜間保護、可公開身份
- [x] 1.2 修改 GA 的討論 prompt：移除 Gnosia 身份資訊，改為「無情報，可公開身份推測」
- [x] 1.3 新增 GA 的夜間行動 prompt（保護目標，無連續限制）
- [x] 1.4 修改夜間行動邏輯：GA 需要 Launch agent 進行保護
- [x] 1.5 更新保護判定：僅 GA 保護（移除舊 Doctor 保護邏輯）
- [x] 1.6 更新資訊隔離規則：GA prompt 不再包含 Gnosia 身份

## 2. 更新 GM 指令 — Doctor 重設計為驗屍

- [x] 2.1 修改 Doctor 職業說明：夜間查看前日被投票淘汰者的陣營
- [x] 2.2 修改 Doctor 的討論 prompt：改為包含驗屍歷史（非保護歷史）
- [x] 2.3 移除 Doctor 的夜間行動 prompt（驗屍為自動處理）
- [x] 2.4 新增夜間結果解析中的驗屍邏輯（自動記錄被淘汰者陣營）
- [x] 2.5 更新資訊隔離：Doctor prompt 包含驗屍結果而非保護歷史

## 3. 更新 GM 指令 — Engineer 恢復 100%

- [x] 3.1 移除模糊掃描擲骰邏輯
- [x] 3.2 更新 Engineer 討論 prompt（移除「無法判定」）

## 4. 更新角色 Agent

- [x] 4.1 更新所有角色 agent：GA 行為策略從「暗示已知 Gnosia」改為「公開推測、保護他人」
- [x] 4.2 更新所有角色 agent：Doctor 行為策略從「保護他人」改為「驗屍分析、選擇公開時機」

## 5. 更新文件

- [ ] 5.1 更新 `README.md`：GA 和 Doctor 新職業說明、Engineer 100%
