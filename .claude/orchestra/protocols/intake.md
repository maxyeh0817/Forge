# Intake 協議

## 觸發條件
用戶提出新需求

## 執行者
Orchestrator → PM agent

## 流程

1. Orchestrator 收到用戶輸入
2. 路由判斷為新需求 → 派遣 PM agent
3. PM 分析需求完整度
   - ≥80% → 直接進入 Planning
   - <80% → 產出澄清問題
     - 更新 status → "clarifying"
     - 等待用戶回覆 → 回到分析
