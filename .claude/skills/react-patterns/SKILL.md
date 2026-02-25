---
name: react-patterns
description: >
  React/Next.js 開發模式。定義元件結構、狀態管理、路由模式等。
  Frontend Dev agent 應注入此 skill。
---

# React Patterns 規範

## Next.js App Router 慣例
- 使用 App Router（`app/` 目錄）
- 預設使用 Server Components
- 需要互動時才加 `'use client'`
- 路由檔案：`page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`
- API Routes：`app/api/*/route.ts`

## 元件結構
- 一個檔案一個元件（除非是緊密耦合的小元件）
- Props 使用 TypeScript interface，命名為 `{ComponentName}Props`
- 預設使用 named export（非 default export）
- 元件檔案結構順序：
  1. imports
  2. types/interfaces
  3. 常數
  4. 元件函數
  5. export

## 狀態管理
- 簡單狀態：`useState`
- 複雜狀態：`useReducer`
- 跨元件共享：React Context（小規模）或 Zustand（中大規模）
- 伺服器狀態：搭配 Server Components + Server Actions

## 樣式
- 使用 Tailwind CSS utility classes
- 複雜樣式邏輯使用 `clsx` 或 `cn()` 組合
- 避免 inline style objects
- 響應式設計使用 Tailwind breakpoints（`sm:`, `md:`, `lg:`）

## 常見模式
- 表單：controlled components + server actions
- 列表渲染：確保有穩定的 `key`
- 條件渲染：使用 `&&` 或三元運算子，避免 `if` 在 JSX 中
- 錯誤邊界：使用 `error.tsx` 檔案

## 效能
- 圖片使用 `next/image`
- 連結使用 `next/link`
- 大型列表考慮虛擬化
- 避免不必要的 re-render（適當使用 `memo`, `useMemo`, `useCallback`）

## 已知注意事項
（由 QA 迭代時追加）

> 詳細模式參考：references/patterns.md
> 歷史教訓：references/lessons.md
