# Project Init 協議

## 觸發條件
計畫已確認

## 執行者
Orchestrator

## 流程

1. 從 templates/project-template/ 複製腳手架到 projects/{name}/
2. 寫入 README.md（專案名片）
3. 寫入 project.json（狀態機）
4. 寫入 spec/current.md
5. 寫入 tasks/ 下各任務單
6. 寫入 docs/architecture.md（如有）
7. 在 projects/{name}/ 執行 git init + 建立 .gitignore
8. 初始 commit：「chore: project init — {project-name}」
9. 註冊到 .claude/state/active-project.json
10. 向用戶展示專案摘要
