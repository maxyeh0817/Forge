# Delivery 協議

## 觸發條件
所有 task 通過稽核

## 執行者
Orchestrator

## 流程

1. 彙整所有交付物
2. 產出交付摘要
3. 更新 project.json status → "delivered"
4. 最終更新 README.md（標記已交付）
5. 產出 session log（使用 session-template.md 格式）
6. git tag：v{spec-version}（如 v1.0）
7. 執行偏好回饋（見偏好回饋路徑）
