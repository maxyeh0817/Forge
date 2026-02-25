---
name: cmd-review
description: >
  觸發全面稽核。對所有已完成但未通過的任務進行 QA。
---
## 執行步驟

1. 讀取 `project.json` 的 tasks 陣列
2. 篩選所有 `status: "completed"` 且 `review_status` 非 `"passed"` 的任務
3. 如果無符合任務 → 顯示「所有任務已通過稽核。」
4. 對每個待稽核任務：
   - 派遣 QA Reviewer agent（帶入任務單路徑 + spec 路徑 + 程式碼路徑）
   - 收到稽核結果 → 更新 tasks/Txxx.md 和 project.json
   - 如未通過 → 創建修正 sub-task，進入 Forge Loop 修正流程
5. 全部通過後 → 執行 Level 3 整合稽核（如尚未執行）
6. 向用戶展示稽核總結報告
