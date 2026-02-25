# Review 協議

## 觸發條件
某 agent 完成任務

## 執行者
QA Reviewer agent

## 流程

1. 派遣 QA agent（傳入稽核上下文：任務單路徑 + agent 摘要 + 專案根路徑）
2. Level 1 稽核（QA agent 執行）：
   - **Build 驗證**：執行 `npm run build`（或專案對應的 build 命令）
   - **Lint 驗證**：執行 `npm run lint`（如有配置）
   - **Type 驗證**：執行 `npx tsc --noEmit`（TypeScript 專案）
   - **功能完整性**：對照任務完成定義逐項檢查
   - **程式碼品質**：結構、命名、一致性
   - 全部通過 → review_status → "passed"
   - 任一未通過 → 產出稽核報告（含完整錯誤訊息）
     - review_status → "failed"
     - Orchestrator 回派原 agent 修正（不自己修）
     - 修正後重新 QA
     - 最多迭代 3 次，超過標記需人工介入
3. 全部通過 → Level 3 整合稽核
4. 發現模式性問題 → Level 2 技能迭代

## 重要原則
- Build / lint / test 驗證是 QA 的職責，**不是 Orchestrator 的職責**
- QA 發現問題後產出報告，修正工作回派給開發 agent
- Orchestrator 只負責調度，不負責修復
