---
name: cmd-retro
description: >
  回顧與技能迭代。分析專案教訓並更新 skill。
---
## 執行步驟

1. 讀取當前專案的所有 `reviews/*.md` 稽核報告
2. 讀取所有 `sessions/*.md` 對話日誌
3. 分析模式：
   - 反覆出現的問題 → 更新相關 skill 的 `references/lessons.md`
   - 高嚴重度重複問題 → 更新 skill 的 `SKILL.md` 核心指示
   - 成功模式 → 記錄到 `references/patterns.md`
4. 檢查偏好：
   - 比對 `project.json.preference_overrides` 與系統 `preferences.yaml`
   - 通用偏好 → 建議更新 `preferences.yaml`（需用戶確認）
5. 效率建議：
   - 評估是否需要更新 agent description 的路由意圖
   - 評估是否需要新 agent 或 skill
6. 產出回顧報告並讓用戶確認所有變更
