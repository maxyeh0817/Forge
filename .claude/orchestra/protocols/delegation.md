# Delegation 協議

## 觸發條件
專案已初始化

## 執行者
Orchestrator

## 流程

啟動 Forge Loop（見 CLAUDE.md）：

### 迴圈體
1. 掃描任務佇列（priority + 依賴排序）
2. 對當前最高優先可執行 task：
   a. 語義匹配 .claude/agents/ 中的 agent（靠 description）
   b. 若無匹配 → 執行 Agent Creation 協議
   c. 用 Task 工具派遣 agent（傳入任務單 + spec 路徑 + preferences 路徑）
   d. 收到摘要 → 檢查 ##ESCALATION → 處理升級請求
   e. 觸發 QA Review（QA 負責 build/lint/test 驗證，見 review 協議）
   f. QA 通過 → 更新 task md 狀態 + project.json + README.md → git commit → 回到步驟 1
   g. QA 未通過 → 回派原 agent（或語義匹配更合適的 agent）修正 → 重新 QA（最多 3 次）→ 通過則回到 1，否則標記 blocked

### Orchestrator 禁區（重要）
Orchestrator **絕不**執行以下動作，必須全部委派給 agent：
- 執行任何 shell 命令（npm run build、npx tsc、npm test 等）
- 修改原始碼（.ts, .tsx, .css, .json 等專案程式碼）
- 修復 build / lint / type 錯誤

**當 agent 交付後 build 失敗的正確流程：**
1. QA reviewer 發現 build 失敗 → 產出稽核報告（含錯誤訊息）
2. Orchestrator 收到報告 → 回派原 agent 修正（在 prompt 中附上錯誤訊息）
3. 原 agent 修正後 → 再次觸發 QA → 通過則繼續

### Task 狀態同步規則
每個 task 通過 QA 後，Orchestrator 必須更新**兩處**：
1. `tasks/TASK-XXX.md` 中的 `狀態` 欄位 → `completed`
2. `project.json` 中對應 task 的 `status` → `"completed"`

兩處必須同步，不可只更新其中一處。

### 退出條件
- 全部 completed + passed → delivery 協議
- 遇到 blocker / 安全閥 / 決策點 → 暫停，報告用戶
