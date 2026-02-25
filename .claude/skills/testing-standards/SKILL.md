---
name: testing-standards
description: >
  測試標準。定義測試策略、命名慣例、覆蓋率要求等。
  QA Reviewer agent 應注入此 skill，開發類 agent 可選擇性注入。
---

# Testing Standards 規範

## 測試策略
- 單元測試：核心業務邏輯、工具函數
- 整合測試：API 端點、資料庫操作
- 元件測試：關鍵 UI 元件的渲染和互動
- E2E 測試：核心用戶流程（視專案規模決定是否需要）

## 測試框架
- 單元/整合測試：Vitest（優先）或 Jest
- 元件測試：React Testing Library
- E2E 測試：Playwright（如需要）

## 命名慣例
- 測試檔案：`{module}.test.ts` 或 `{module}.spec.ts`
- 測試描述：使用中文或英文皆可，保持一致
- describe：描述被測試的模塊/函數
- it/test：描述預期行為（「should ...」或「當...時，應該...」）

## 測試結構
```typescript
describe('模塊名稱', () => {
  describe('函數/方法名稱', () => {
    it('should 預期行為 when 條件', () => {
      // Arrange
      // Act
      // Assert
    })
  })
})
```

## 品質標準
- 每個 API 端點至少有 happy path + error path 測試
- 工具函數覆蓋率目標：80%+
- 測試應獨立、可重複執行
- 避免測試實作細節，測試行為和結果
- Mock 外部依賴（API 呼叫、資料庫）

## 稽核檢查清單
- [ ] 測試是否覆蓋完成定義中的所有驗收條件
- [ ] 測試是否包含邊界情況
- [ ] 測試是否可獨立執行（不依賴外部狀態）
- [ ] 測試命名是否清晰描述預期行為
- [ ] 是否有不必要的 snapshot 測試

## 已知注意事項
（由 QA 迭代時追加）

> 詳細模式參考：references/patterns.md
> 歷史教訓：references/lessons.md
