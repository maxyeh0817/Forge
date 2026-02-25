---
name: cmd-switch
description: >
  切換到其他專案。
---
## 執行步驟

1. 讀取 `.claude/state/active-project.json` 的 `active_projects` 列表
2. 如果只有一個專案 → 顯示「目前只有一個活躍專案。」
3. 向用戶展示所有活躍專案（名稱、狀態、進度、最後更新時間）
4. 用戶選擇目標專案後：
   - 儲存當前專案的 session log（如有未儲存的進度）
   - 更新 `active-project.json` 的 `current` 指標
   - 讀取目標專案的 `project.json`
   - 向用戶展示目標專案的 README.md 摘要
   - 進入路由 B（恢復 Forge Loop）
