---
name: cmd-status
description: >
  查看專案進度。展示當前專案的狀態和任務總覽。
---
## 執行步驟

1. 讀取 `.claude/state/active-project.json` 取得當前專案路徑
2. 如果無活躍專案 → 顯示「無進行中的專案。使用 /start 開始新需求。」
3. 讀取 `projects/{name}/project.json`
4. 讀取 `projects/{name}/README.md`
5. 向用戶展示：
   - 專案名稱與狀態
   - 進度百分比（completed / total tasks）
   - 任務總覽表（ID、標題、負責 agent、狀態、QA 結果）
   - 當前 blockers（如有）
   - 最後一次 session 摘要（從 sessions/ 讀取最新）
6. 如果有其他 active_projects → 列出並提示可用 /switch 切換
