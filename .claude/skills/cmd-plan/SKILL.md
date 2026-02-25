---
name: cmd-plan
description: >
  查看或修改計畫。展示 spec 並允許變更。
---
## 執行步驟

1. 讀取當前專案的 `spec/current.md`
2. 向用戶展示 spec 摘要（版本、狀態、功能列表、里程碑）
3. 詢問：「需要修改計畫嗎？」
4. 如果用戶提出修改：
   - 派遣 PM agent（帶入用戶修改意見 + 當前 spec 路徑）
   - PM 更新 spec/current.md + changelog.md
   - PM 回傳結果後，向用戶展示 diff 摘要
   - 確認後 commit：`docs: spec v{version} — {summary}`
5. 如果用戶無修改 → 結束
