---
name: cmd-start
description: >
  啟動新需求。讀取系統狀態，進入 intake 流程。
---
## 執行步驟

1. 讀取 `.claude/state/active-project.json`
2. 如果有進行中的專案：
   - 向用戶展示當前專案名稱與狀態
   - 詢問：「要開始新專案，還是繼續目前的 {name}？」
   - 用戶選「繼續」→ 進入路由 B（恢復 Forge Loop）
3. 如果無活躍專案（或用戶選「新專案」）：
   - 將用戶描述作為需求輸入
   - 派遣 PM agent（帶入用戶原文 + preferences.yaml 路徑）
   - PM 回傳結果後，進入 Planning → Project Init → Forge Loop
