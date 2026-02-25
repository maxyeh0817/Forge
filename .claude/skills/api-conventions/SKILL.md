---
name: api-conventions
description: >
  API 設計慣例。定義 RESTful 規範、錯誤格式、分頁策略等。
  PM、Architect、Backend Dev、QA Reviewer 應注入此 skill。
---

# API Conventions 規範

## RESTful 慣例
- 資源命名：複數名詞（`/users`, `/todos`）
- HTTP 方法語義：
  - `GET` — 讀取（無副作用）
  - `POST` — 創建
  - `PUT` — 全量更新
  - `PATCH` — 部分更新
  - `DELETE` — 刪除
- URL 路徑：kebab-case（`/user-profiles`）
- 巢狀資源：最多兩層（`/users/:id/todos`）

## 狀態碼
- `200` — 成功
- `201` — 創建成功
- `204` — 刪除成功（無回應體）
- `400` — 請求格式錯誤
- `401` — 未認證
- `403` — 無權限
- `404` — 資源不存在
- `422` — 驗證失敗
- `500` — 伺服器內部錯誤

## 錯誤格式
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "人類可讀的錯誤描述",
    "details": [
      { "field": "email", "message": "格式不正確" }
    ]
  }
}
```

## 分頁策略
- 預設採用 cursor-based 分頁
- 請求參數：`?cursor={cursor}&limit={limit}`
- 回應格式：
```json
{
  "data": [],
  "pagination": {
    "next_cursor": "abc123",
    "has_more": true
  }
}
```
- 預設 limit: 20，最大 limit: 100

## 版本策略
- URL path versioning（`/api/v1/...`）
- 只在破壞性變更時升版

## 已知注意事項
（由 QA 迭代時追加）

> 詳細模式參考：references/patterns.md
> 歷史教訓：references/lessons.md
