# Agent brief — HIS 多院區規劃 Project Tracker

You are writing one or more **task pages** for a static-HTML project tracker. The team is a vendor
evaluating / preparing to execute the NCKU Hospital project「醫療資訊系統多院區規劃」(rewrite the
VB.Net HIS in C#, make it multi-campus, deploy to the new geriatric hospital 老人醫院).

**Source of truth:** `C:\Users\user1\Desktop\programming\knowbook\HIS\02-規格表(含需求說明書).md`
Read it fully before writing. Quote the section numbers you rely on.

**Language:** Traditional Chinese for content (繁體中文). Keep technical terms in English where the spec does
(C#, WCF, CDC, PACS, HL7 …). Be concrete and opinionated: this is our internal working document, not marketing.

**Audience:** our own engineers and PM. Every page must answer:
1. 我們預期這個系統／任務長什麼樣（架構、資料流、元件）— a *sketch*, drawn as an inline SVG or a `<pre class="diagram">` box diagram.
2. 需要什麼領域知識，為什麼難。
3. 依賴哪些其他任務（use the task IDs below），誰依賴它。
4. 需不需要介接硬體／外部設備；若需要，是什麼設備、協定、誰的 SDK。
5. **我們需要緊急向院方／原廠取得什麼**（資料、文件、人、環境、授權），向誰要，沒有會怎樣。
6. 主要阻礙與風險。
7. 待確認問題（open questions）。

Be honest about unknowns: the spec is thin. Where the spec does not say, say「規格未載明，需確認」and put it in the asks.

---

## Output files (write exactly these)

For each assigned task ID `XX`:

1. `tasks/XX.html` — the page, using the skeleton below verbatim (same section order, same ids/classes).
2. `data/XX.json` — metadata, schema below. Must be valid JSON, UTF-8, no comments.

Base directory: `C:\Users\user1\.claude\jobs\6910e68e\tmp\project tracker\`
Stylesheet is at `assets/style.css` (already exists — do not modify). Pages link to it as `../assets/style.css`.
Overview is `../index.html`. Other task pages are `./T02.html` etc.

---

## Task list (IDs are fixed — use them for `depends_on`)

**Phase 1 「多院區整合功能開發與上線」— 決標次日起 300 天，付款 50%**
- T01 VB.Net→C# 全面改寫（門診／急診／住院／醫療共用；線上約 3,647 支、批次約 262 支，另有未盤點的本機獨立程式）
- T02 院區差異參數化（APP/WEB Config、Context 類別、if-else 改字典／函式映射、PCS_Ip_Config／PUB_Config 擴充、新設定表）
- T03 舊架構優化與效能（檢核引擎易於新增規則、共用／底層元件）
- T04 程式碼資安強化（SQL 移至後端執行、WCF 同時支援 HTTP/HTTPS）
- T05 開發期間與總院增修保持同步（總院 VB.Net HIS 持續改版，需定期合併到新系統）
- T06 斗六分院與成大醫院 Phase-1 上線（整合測試後先於兩院上線）

**Phase 2 「老人醫院 HIS 功能開發 + 外部介接開發」— 540 天，付款 30%**
- T07 老人醫院差異需求訪談與基準範圍確認（規格 貳-一-(二)-8）
- T08 數據整合中台（CDC／MQ／Replication 即時供應、讀寫分離、保護核心 HIS DB、清檔機制、銜接成大住院健檢歷史資料、Dashboard/Analytics 擴充）
- T09 跨院掛號資料查詢與辦理掛號（老人醫院 ↔ 成大）
- T10 跨院床位查詢（ICU、普通病房、空床）
- T11 跨院手術排程查詢與預約
- T12 跨院檢查排程查詢與預約
- T13 跨院供膳訂餐統計彙總
- T14 轉檢與代檢流程機制
- H01 急診檢傷系統介接（開發）
- H02 診間叫號機系統介接（開發）
- H03 藥局藥包機系統介接（開發）
- H04 PACS 系統介接（開發）
- H05 刀房叫號機介接（開發）
- H06 智慧藥櫃介接（開發）
- H07 自動繳費機介接（開發）
- H08 慢箋領藥機介接（開發）
- H09 住院健檢系統儀器介接（於使用者電腦定期執行之批次程式）（開發）
- X01 內部跨系統介接測試（規格 #11–#36 共 26 個系統：住院醫師排班、ADR 通報、傳呼、疾病分類輔助、病歷分類輔助、病歷品質審查、人體器官保存庫、院內感染控制、LIS、MIS、WEB EMR、個管、表單、麻醉管理、電子病歷管理、電子白板、檢查報告、AI 模組、SDM、Epinet 針扎、跨院介接（部立台南醫院、郭綜合）、NIIS、風采透析、住院健檢身心自評表、住院健檢營養評估表、住院健檢營養訂餐）

**Phase 3 「老人醫院建置上線 + 以老醫版本回饋斗六／成醫」— 630 天，付款 20%**
- T15 老人醫院上線環境準備與資料轉置（DC 組伺服器與測試環境、基本資料轉置、跨系統／外部機構連線設定、權限角色、Client 端環境）
- T16 老人醫院上線，再以含老醫功能之版本回饋成大醫院、斗六分院上線

**Cross-cutting（全程）**
- M01 專案管理交付物（得標 20 天內工作計畫書；導入步驟／測試步驟／上線前檢核／緊急復原四份工作書；變更管理；專案會議；分階段驗收）
- M02 教育訓練與技術移轉（驗收前 16 小時；至少 8 場 × 2 小時；操作手冊、系統文件、版本管理）
- M03 資通安全合規（防護需求等級評估報告、安全檢測證明、弱掃／滲透複測、遠端連線規範、原產地／大陸禁令、個資、5 年紀錄保存）
- M04 保固維運（1 年；緊急 2h／一般 72h SLA；罰則 ‰2／‰1、上限 20%；季維護報告）
- Q01 投標資格（CMMI Level 3、CNS/ISO 27001、BS 10012:2017 或 ISO 27701、原產地限制）

---

## `data/XX.json` schema

```json
{
  "id": "T01",
  "title": "VB.Net→C# 全面改寫",
  "phase": 1,
  "category": "core",
  "hardware": "no",
  "domain_difficulty": 4,
  "tech_difficulty": 5,
  "effort_pm": 120,
  "depends_on": ["T02"],
  "summary": "一句話說明這個任務。",
  "urgent_asks": [
    {"what": "全部 VB.Net 原始碼（含批次與本機獨立程式）與版本庫歷史", "from": "資訊室 HIS 組", "why": "沒有原始碼無法估算與改寫", "priority": "P0"}
  ],
  "blockers": ["…"],
  "contacts": ["資訊室 HIS 組", "資訊室 DC 組"],
  "open_questions": ["…"]
}
```

Field rules:
- `phase`: 1, 2, 3, or 0 for cross-cutting.
- `category`: one of `core`, `shared` (跨院共享功能), `platform`, `hardware`, `interface-test`, `deploy`, `management`, `compliance`, `bid`, `requirements`.
- `hardware`: `yes` (talks to a physical device / kiosk / instrument), `partial` (software system but device-adjacent or vendor-black-box), `no`.
- `domain_difficulty`, `tech_difficulty`: integers 1–5 (5 = hardest). Domain = medical/NHI/hospital-process knowledge needed. Tech = engineering difficulty.
- `effort_pm`: rough person-months, integer. Be realistic; explain the number on the page.
- `depends_on`: task IDs that must be (substantially) done before this one can complete. Only real dependencies.
- `urgent_asks`: 3–8 items. `priority` P0 = cannot start without it, P1 = needed within first month, P2 = needed before the phase ends.
- `contacts`: roles at the hospital or vendors we must reach (e.g. 資訊室 HIS 組, 資訊室 DC 組, 採購組, 老人醫院籌備處, 叫號機原廠, 健保署 …).

---

## `tasks/XX.html` skeleton (copy verbatim, fill the `…`)

```html
<!doctype html>
<html lang="zh-Hant">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>T01 VB.Net→C# 全面改寫 — HIS 多院區規劃 Tracker</title>
<link rel="stylesheet" href="../assets/style.css">
</head>
<body>
<nav class="topnav">
  <a href="../index.html">← 總覽</a>
  <span class="crumb">Phase 1 · core</span>
</nav>
<main class="page">
<header class="task-header">
  <div class="task-id">T01</div>
  <h1>VB.Net→C# 全面改寫</h1>
  <p class="lede">一段話：這個任務是什麼、為什麼重要。</p>
  <div class="meta-grid">
    <div class="meta"><span class="k">階段</span><span class="v">Phase 1 · 300 天內</span></div>
    <div class="meta"><span class="k">硬體介接</span><span class="v hw-no">無</span></div>
    <div class="meta"><span class="k">領域難度</span><span class="v"><span class="dots d4"></span> 4/5</span></div>
    <div class="meta"><span class="k">技術難度</span><span class="v"><span class="dots d5"></span> 5/5</span></div>
    <div class="meta"><span class="k">預估工作量</span><span class="v">約 120 人月</span></div>
    <div class="meta"><span class="k">依賴</span><span class="v"><a href="./T02.html">T02</a></span></div>
    <div class="meta"><span class="k">被依賴</span><span class="v"><a href="./T06.html">T06</a></span></div>
    <div class="meta"><span class="k">規格依據</span><span class="v">貳-一-(一)-1</span></div>
  </div>
</header>

<section id="spec">
  <h2>規格原文依據</h2>
  <blockquote>…直接引用或忠實摘錄規格條文…</blockquote>
</section>

<section id="sketch">
  <h2>我們預期的系統樣貌</h2>
  <p>…</p>
  <pre class="diagram">
┌──────────┐     ┌──────────┐
│  …       │ ──▶ │  …       │
└──────────┘     └──────────┘
  </pre>
  <h3>元件與資料流</h3>
  <ul><li>…</li></ul>
  <h3>工作量怎麼估的</h3>
  <p>…</p>
</section>

<section id="domain">
  <h2>需要的領域知識與難點</h2>
  <ul><li>…</li></ul>
</section>

<section id="deps">
  <h2>依賴關係</h2>
  <h3>前置任務</h3>
  <ul><li><a href="./T02.html">T02</a> — 為什麼…</li></ul>
  <h3>依賴本任務的任務</h3>
  <ul><li>…</li></ul>
</section>

<section id="hardware">
  <h2>硬體／外部設備介接</h2>
  <p>…（若無，說明為什麼無）</p>
  <table>
    <thead><tr><th>設備／系統</th><th>協定／介面</th><th>誰提供 SDK 或規格</th><th>測試需要什麼</th></tr></thead>
    <tbody><tr><td>…</td><td>…</td><td>…</td><td>…</td></tr></tbody>
  </table>
</section>

<section id="asks">
  <h2>需要緊急向院方／原廠取得</h2>
  <table class="asks">
    <thead><tr><th>優先</th><th>要什麼</th><th>向誰要</th><th>為什麼／沒有會怎樣</th></tr></thead>
    <tbody>
      <tr><td><span class="pri p0">P0</span></td><td>…</td><td>…</td><td>…</td></tr>
    </tbody>
  </table>
</section>

<section id="blockers">
  <h2>主要阻礙與風險</h2>
  <ul><li><strong>…</strong> — …</li></ul>
</section>

<section id="questions">
  <h2>待確認問題</h2>
  <ol><li>…</li></ol>
</section>
</main>
<footer class="foot">HIS 多院區規劃 · 內部工作文件 · 依據 02-規格表(含需求說明書) V9</footer>
</body>
</html>
```

Class cheatsheet: `hw-yes` / `hw-partial` / `hw-no` for the hardware value; `dots d1`…`d5` for difficulty;
`pri p0` / `p1` / `p2` for priority. Only relative links. No external scripts, no external fonts.

Keep each page substantial (roughly 600–1200 words of content) but concrete. Do not pad.
When done, reply with a compact summary per task: one line, top 3 urgent asks, top blockers, and the depends_on list.
