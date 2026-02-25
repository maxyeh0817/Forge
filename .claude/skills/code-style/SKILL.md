---
name: code-style
description: >
  程式碼風格規範。定義命名慣例、格式化規則、import 排序等。
  所有開發類 agent 應注入此 skill。
---

# Code Style 規範

## 命名慣例
- 變數/函數：camelCase
- 元件/類型：PascalCase
- 常數：UPPER_SNAKE_CASE
- 檔案名：kebab-case（元件檔除外，用 PascalCase）

## 格式化
- 縮排：2 spaces
- 引號：single quotes
- 分號：不使用
- 行寬上限：100 字元

## Import 排序
1. 外部套件
2. 內部模組（@/ 路徑）
3. 相對路徑

## 已知注意事項
（由 QA 迭代時追加）

> 詳細模式參考：references/patterns.md
> 歷史教訓：references/lessons.md
