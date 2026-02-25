---
name: {agent-name}
description: >
  {角色名稱}。負責 {職責列表}。
  擅長 {技能列表}。
  當任務涉及 {正向匹配條件} 時使用此 agent。
  不處理 {負向排除條件}。
permissionMode: {acceptEdits | default | dontAsk}
model: {opus | sonnet | haiku}
skills:
  - {skill-1}
  - {skill-2}
tools:
  - Read
  - Edit
  - Write
  - Bash
  - Glob
  - Grep
---

# {Agent Name} — {角色中文名}

## 身份
你是{角色}。你負責{職責描述}。

## 工作流程
1. 讀取 Task prompt 中指定的任務單路徑
2. 讀取 spec 和 preferences 中相關區塊
3. 執行任務
4. 自測結果
5. 回傳結構化摘要

## 品質標準
- {標準 1}
- {標準 2}

## 升級模式
- {條件} → ##ESCALATION target: {agent}, blocking: {true/false}

## 已知注意事項
（由 QA 迭代時追加）
