<div align="center">

<h1><img src="icon.png" width="80" align="center" />&nbsp;Forge</h1>

### AI 驅動的開發團隊協調器

**將單一 Claude Code CLI 轉化為完整的虛擬開發團隊。**

[![Built with Claude](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet?style=for-the-badge&logo=anthropic)](https://claude.ai)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Agents](https://img.shields.io/badge/Agents-6%20個角色-orange?style=for-the-badge)](#-團隊成員)
[![Skills](https://img.shields.io/badge/Skills-10+-blue?style=for-the-badge)](#-技能系統)

[English](README.md) | [繁體中文](README.zh-TW.md)

---

*從一句需求描述到完整交付 ——*
*Forge 自動處理規劃、分工、品質保證與交付。*

</div>

---

## 什麼是 Forge？

Forge 是一個建構在 [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) 之上的**協調框架**。它將單一 AI 助手轉化為一支有分工的開發團隊 —— 產品經理、架構師、前後端工程師、QA 審查員和 DevOps 工程師 —— 在一個 Orchestrator（廠長）的統籌下協同作業。

可以把它想像成一座住在你 `.claude/` 目錄裡的**虛擬軟體公司**：

```
你（CEO）
 └─ Forge Orchestrator（廠長）
     ├─ PM Agent           → 分析需求、撰寫規格書
     ├─ Architect Agent    → 設計系統架構、技術選型
     ├─ Frontend Dev Agent → 使用 React/Next.js/Tailwind 建構 UI
     ├─ Backend Dev Agent  → 實作 API、資料庫、伺服器邏輯
     ├─ QA Reviewer Agent  → 驗證每一項交付物
     └─ DevOps Agent       → 處理部署、CI/CD、Docker
```

### 為什麼選擇 Forge？

| 痛點 | Forge 的解決方案 |
|------|-----------------|
| AI 在對話之間失去上下文 | 持久化專案狀態 —— 從上次中斷處精確恢復 |
| AI 不理解需求就直接寫程式 | PM Agent 先釐清需求；Architect 先設計再開發 |
| AI 產出的程式碼沒有品質關卡 | 每個任務都必須通過 QA（build、lint、型別檢查、功能驗證） |
| 單一 AI 試圖包辦一切 | 專業化 Agent，各有領域知識與獨立上下文 |
| 知識無法累積 | 技能隨時間演進；過去專案的經驗會改善未來的表現 |

---

## 使用方式

### 前置需求

- 已安裝並設定好的 [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code)
- Node.js 18+（用於專案建構）
- Git

### 快速開始

**1. 複製專案**

```bash
git clone https://github.com/your-username/forge.git
cd forge
```

**2. 啟動 Claude Code**

```bash
claude
```

Forge 會透過 `.claude/CLAUDE.md` 自動載入 —— 無需額外設定。

**3. 開始第一個專案**

```
/start
```

然後用自然語言描述你的需求：

```
我想做一個用 Next.js 的個人部落格。
要有 Markdown 文章系統、深色模式支援、還有 RSS feed。
```

Forge 會自動：
1. 將需求轉交 PM Agent 進行需求分析
2. 產生結構化規格書與任務拆解
3. 派遣任務給對應的 Agent
4. 對每個交付物執行 QA 驗證
5. 通過驗證後自動提交 Git commit

**4. 隨時查看進度**

```
/status
```

**5. 跨對話接續**

只要在同一目錄下啟動 Claude Code，Forge 就會讀取已儲存的狀態，從中斷處繼續。

### 斜線指令

| 指令 | 說明 |
|------|------|
| `/start` | 啟動新需求 —— 進入需求收集流程 |
| `/status` | 查看目前專案進度與任務總覽 |
| `/plan` | 查看或修改專案規格書 |
| `/review` | 對所有待審任務觸發全面 QA 稽核 |
| `/retro` | 執行專案回顧 —— 分析經驗教訓並更新技能 |
| `/switch` | 切換到其他進行中的專案 |

---

## 系統架構

### 雙層設計

Forge 將**系統層**（Agent、技能、協議）與**專案層**（規格、任務、程式碼）分離。這讓每個專案都是自包含且可攜帶的。

```
┌─────────────────────────────────────────────────────────────┐
│                  .claude/（系統層）                           │
│                                                             │
│   agents/          6 位專業 AI 團隊成員                      │
│   skills/          10+ 可複用知識套件                        │
│   orchestra/       協議、範本、路由規則                       │
│   state/           跨對話記憶 & 偏好設定                     │
│   CLAUDE.md        單一入口（自動載入）                       │
└─────────────────────────────────────────────────────────────┘
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
┌──────────────────────┐  ┌──────────────────────┐
│  projects/blog/      │  │  projects/api/       │
│                      │  │                      │
│  README.md           │  │  README.md           │
│  project.json        │  │  project.json        │
│  spec/current.md     │  │  spec/current.md     │
│  tasks/TASK-001.md   │  │  tasks/TASK-001.md   │
│  reviews/            │  │  reviews/            │
│  sessions/           │  │  sessions/           │
│  src/                │  │  src/                │
└──────────────────────┘  └──────────────────────┘
```

### Forge 主循環

驅動每個專案的核心執行引擎：

```
                    ┌──────────────┐
                    │  掃描任務佇列 │ ◄─────────────────────┐
                    └──────┬───────┘                       │
                           │                               │
                    ┌──────▼───────┐                       │
                    │  選取最高    │                       │
                    │  優先任務    │                       │
                    └──────┬───────┘                       │
                           │                               │
                    ┌──────▼───────┐                       │
                    │  語義匹配    │                       │
                    │  合適 Agent  │                       │
                    └──────┬───────┘                       │
                           │                               │
                    ┌──────▼───────┐     ┌────────────┐   │
                    │  透過 Task   │────►│ 升級請求   │   │
                    │  工具派遣    │     │ 處理器     │   │
                    └──────┬───────┘     └────────────┘   │
                           │                               │
                    ┌──────▼───────┐                       │
                    │   QA 審查    │                       │
                    │  （build、   │                       │
                    │   lint、     │                       │
                    │   型別檢查、 │                       │
                    │   功能驗證） │                       │
                    └──────┬───────┘                       │
                           │                               │
                    ┌──────▼───────┐    ┌──────────────┐  │
                    │   通過？     │─否─► 重新派遣     │──┘
                    └──────┬───────┘    │（最多 3 次） │
                           │是         └──────────────┘
                    ┌──────▼───────┐
                    │  Commit +    │
                    │  更新狀態    │
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │  下一任務 /  │
                    │  交付        │
                    └──────────────┘
```

### 工作流路由

Forge 會自動分類你的輸入並路由到正確的工作流：

| 輸入類型 | 規模 | 路由 |
|---------|------|------|
| 任何任務 | 微型（≤3 檔案、目標明確） | **路由 E** — 直接執行，跳過 PM |
| 新功能 | 小型（單一功能模組） | **路由 A** — 簡化規劃 |
| 新功能 | 中/大型（跨模組） | **路由 A** — 完整規劃含架構設計 |
| Bug 修復 | 任何 | **路由 A** 或 **路由 E** |
| 繼續工作 | 任何 | **路由 B** — 從已存狀態恢復 |
| 需要釐清 | 任何 | **路由 C** — PM 處理問答 |
| QA 待修正 | 任何 | **路由 D** — 修正後重審 |

---

## 團隊成員

### Agent 角色

<table>
<tr>
<td align="center" width="150">

**🎯 PM**

產品經理

</td>
<td>

分析需求、與用戶溝通、撰寫結構化規格書（OpenSpec 格式）、將工作拆解為任務。當需求完整度 < 80% 時主動提出澄清問題。

</td>
</tr>
<tr>
<td align="center">

**🏗️ Architect**

系統架構師

</td>
<td>

進行技術選型、設計系統架構、撰寫 ADR（Architecture Decision Records）。在中大型專案啟動時參與，或在其他 Agent 升級請求時介入。

</td>
</tr>
<tr>
<td align="center">

**🎨 Frontend Dev**

前端工程師

</td>
<td>

建構 UI 元件、頁面佈局、響應式設計。專精 React、Next.js（App Router）和 Tailwind CSS。

</td>
</tr>
<tr>
<td align="center">

**⚙️ Backend Dev**

後端工程師

</td>
<td>

實作 API 端點、資料庫 schema、伺服器邏輯。使用 Node.js、Next.js API Routes 及資料庫操作。

</td>
</tr>
<tr>
<td align="center">

**✅ QA Reviewer**

品質審查員

</td>
<td>

驗證每一項交付物：執行 `npm run build`、`npm run lint`、`npx tsc --noEmit`，檢查功能完整性，審查程式碼品質。

</td>
</tr>
<tr>
<td align="center">

**🚀 DevOps**

DevOps 工程師

</td>
<td>

處理部署設定、CI/CD 管線、Docker 容器、環境管理和 Git 分支操作。

</td>
</tr>
</table>

### 升級協議（Escalation Protocol）

Agent 可以在不阻塞工作的情況下請求其他 Agent 的協助：

```
Agent 遇到超出自身專業的問題
        │
        ▼
回傳 ##ESCALATION 標記給 Orchestrator
        │
        ├─ blocking: true  → 暫停當前任務，立即派遣目標 Agent
        │
        └─ blocking: false → 記錄需求，當前任務繼續，稍後安排
```

---

## 技能系統

技能是注入到 Agent 上下文中的可複用知識套件。它們會隨著團隊累積經驗而持續演進。

### 領域技能

| 技能 | 說明 | 使用者 |
|------|------|--------|
| `code-style` | 命名慣例、格式化規則、import 排序 | 所有開發類 Agent |
| `api-conventions` | RESTful 模式、錯誤格式、分頁策略 | PM、Architect、Backend |
| `react-patterns` | Next.js App Router、元件模式、狀態管理 | Frontend Dev |
| `testing-standards` | 測試策略、覆蓋率目標、命名慣例 | QA Reviewer、開發類 Agent |

### 技能如何演進

```
第 1 次出現某個模式  →  在 QA 審查報告中記錄
第 2 次出現         →  加入技能的 references/lessons.md
第 3 次以上         →  提升為核心技能定義
```

---

## 專案生命週期

```
 ┌──────┐    ┌──────────┐    ┌──────────┐    ┌───────────┐    ┌───────────┐
 │ 收集 │───►│   規劃   │───►│   開發   │───►│   審查    │───►│   交付    │
 │      │    │          │    │          │    │           │    │           │
 │/start│    │ PM+Arch  │    │ Dev 團隊 │    │ QA 迴圈  │    │ Git tag   │
 │與 PM │    │ 撰寫     │    │ 建構     │    │ 直到     │    │ 回顧      │
 │對話  │    │ 規格+    │    │ 功能     │    │ 全部通過 │    │ 清理      │
 │      │    │ 任務     │    │          │    │           │    │           │
 └──────┘    └──────────┘    └──────────┘    └───────────┘    └───────────┘
```

每個專案完全自包含在 `projects/{name}/` 中：

| 檔案/目錄 | 用途 |
|-----------|------|
| `project.json` | 狀態機 —— 狀態、進度、技術棧、對話歷史 |
| `spec/current.md` | 活文件式需求規格書（OpenSpec 格式） |
| `tasks/TASK-*.md` | 獨立工作單元，含驗收標準 |
| `reviews/` | 每個任務的 QA 審查報告 |
| `sessions/` | 對話紀錄，確保跨對話連續性 |
| `src/` | 實際交付物（程式碼、資源、設定檔） |

---

## 安全機制與防護

Forge 內建多重安全機制：

| 機制 | 上限 | 觸發後行為 |
|------|------|-----------|
| 主循環總迭代次數 | 50 | 儲存進度 → 產出報告 → 暫停 |
| 單一任務 QA 重試 | 3 次 | 將任務標記為阻塞 |
| 連續失敗次數 | 3 次 | 緊急暫停 → 等待用戶指示 |

Orchestrator **絕不會**直接寫程式碼。它只負責分派、審查和協調 —— 確保每一行程式碼在提交前都經過正式的 QA 驗證。

---

## 設定

### 用戶偏好

編輯 `.claude/state/preferences.yaml` 來自訂：

```yaml
tech_stack:
  frontend: "Next.js 16 (App Router)"
  styling: "Tailwind CSS"
  language: "TypeScript (strict mode)"
  backend: "Node.js / Next.js API Routes"
  database: "SQLite (小型) | PostgreSQL (中/大型)"

code_style:
  indent: 2
  quotes: single
  semicolons: false
  max_line_width: 100

communication:
  language: "繁體中文"
  style: "直接、簡潔"
```

### 新增自訂 Agent

在 `.claude/agents/` 中建立新的 `.md` 檔案，遵循 `.claude/orchestra/templates/agent-template.md` 範本格式即可。Orchestrator 會根據 `description` 欄位自動發現並路由任務給它。

---

## 設計原則

| 原則 | 說明 |
|------|------|
| **Orchestrator 模式** | 單一協調者，多個專業化 Agent 並行 |
| **零上下文損失** | 完整狀態持久化 —— 可從任何中斷點恢復 |
| **品質關卡** | 每項交付物必須通過 QA；失敗則帶著診斷資訊回圈 |
| **自包含專案** | 可攜帶、可交接、人類與 AI 皆可讀 |
| **累積式學習** | 技能、偏好、模式隨時間持續改善 |
| **規模自適應** | 同一框架處理 5 分鐘小修到數月大型專案 |
| **語義路由** | 任務描述自動匹配最合適的 Agent |

---

## 授權條款

MIT
