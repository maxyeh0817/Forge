# Agent Creation 協議

## 觸發條件
Delegation 時找不到匹配 agent

## 執行者
Orchestrator

## 流程

1. 分析任務需要的能力
2. 確認現有 agent 無法覆蓋（掃描 .claude/agents/*.md frontmatter）
3. 從 templates/agent-template.md 複製範本
4. 撰寫新 agent 定義，包含：
   - 明確的 description（含正向和負向匹配）
   - 適當的 permissionMode
   - 適當的 model
   - 需要的 skills
   - 工具白名單（使用標準工具名稱）
5. 通知用戶：「已創建新員工 [name]」
6. 返回 Delegation 繼續分派
