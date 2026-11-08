<div align="center">

<img src="https://raw.githubusercontent.com/zhengjue-canon/.github/8ddd1e3d4d8ff64abd1b64774e10ceb231ee20c2/assets/canon-scripture.svg" width="200" height="162" alt="《正覺藏》大藏經典籍與朱筆句讀經卷" />

# 《正覺藏》數位藏經工程 (Zhengjue Canon)

**正本清源 · 重新句讀審定 · 全量改動溯源 · 奠定正法久住千年基業**

[![Official Website](https://img.shields.io/badge/正覺同修會全球資訊網-enlighten.org.tw-D4AF37?style=for-the-badge)](https://www.enlighten.org.tw)
[![Electronic Newsletter](https://img.shields.io/badge/正智出版社·正覺電子報-books.enlighten.org.tw-8A5A10?style=for-the-badge)](https://books.enlighten.org.tw/zh-tw/e)
[![Architecture](https://img.shields.io/badge/架構版本-v3.0_Change_Ledger_%2B_AI_Spec-2E1D0E?style=for-the-badge)](https://github.com/zhengjue-canon/zhengjue-docs)

<img src="https://raw.githubusercontent.com/zhengjue-canon/.github/7384790573a86bd2383f6f6bbc006a64934f5c10/assets/banner.svg" width="100%" alt="Zhengjue Canon Banner" />

</div>

---

## 一、 緣起與六大核心工程支柱

本組織（`zhengjue-canon`）致力於構建 <b>《正覺藏》（《正覺大藏經》）</b> 全流程數位化編審、重新句讀、底本文字校勘訂正、全過程改動溯源、評審專文撰寫與跨平台（Web / 桌面審定端 / iOS & Android 移動端）閱讀共創體系：

1. **正本清源、重編四部藏經目錄**：
   - 依佛滅後第一次七葉窟內五百阿羅漢結集與七葉窟外千人大眾部大乘結集之正統標準，重構 <b>「正法藏部 · 正覺法寶部 · 部派論典辨正部 · 偽佛法部」</b> 四維典籍體系；徹底剔除 2016 年版 CBETA《大藏經補編》混入之宗喀巴《廣論》等喇嘛教外道著作及近代六識論邪說；為遭歐美日學界誣指為「疑偽」之真實大乘經論審定平反。
2. **從 CBETA 到最終公開版 100% 全過程改動帳本（Audited Change Ledger）**：
   - 每一卷經文從 CBETA 原始基準（`001.cbeta.json`）到最終公開定稿（`001.md`）的所有改動（標點斷句、底本錯字訂正、分段、字型標註）均逐處留存於 `001.changes.jsonl`；
   - **底本錯字直接訂正入正文**：正文直接呈現訂正後的正確文字，點擊校勘標記即可查看 CBETA 原字、更改人、審閱人與考證專文；
   - **內外部全透明一致**：公開閱讀端與內部管理端一致展示完整的修訂演進鏈、更改人、審閱人及修改意見文章。
3. **「評審時直接寫文章 + 查看我的評審 + 事後回溯補充長文」之內部 Markdown 專文閉環**：
   - 支持審閱人在評審當下直接於右側雙欄編輯器撰寫完整 Markdown 辨正/考證文章（`articles/ART-*.md`），或先記提綱打上 **「🔖 待補充長文」** 標記；
   - 內置 **「我的評審與文章中心（My Reviews & Articles Hub）」**，隨時回溯自己發起或審閱的改動上下文，補充或擴寫完整專文。
4. **存量 Word (`.docx`) 審定稿雙向無損差分橋接（`docx2changes`）**：
   - 支援將內部現有 `.docx` 斷句/審定文稿直接導入，自動與 CBETA 原始基準執行字符級與標點級 Diff，提取全部標點改動、文字訂正（含防誤刪字核對台）、8 種字型與 Word 批注氣泡。
5. **正覺 8 種雙層正交多字型與「類電腦檔案注解」劃詞辨正**：
   - 嚴格還原正覺書籍特有之 **8 種語義字型體系**（`經文`、`頌文`、`論文`、`問句`、`判教提示`、`白話語譯`、`導師釋文`、`編案`）；對《大毘婆沙論》等部派論典採用分離式偏移錨定（Standoff Annotation）旁批辨正其過失。
6. **面向全 AI 驅動開發（AI-Driven Development）的四層可執行需求體系**：
   - 以 `zhengjue-docs` 中的統一領域詞典（`GLOSSARY.yaml`）、原子需求與數學不變量卡（`REQ-01..06`）、`canon-core` 強類型契約及 4 部黃金樣本（Golden Fixtures）直接驅動全倉 AI 開發與自動化驗收。

---

## 二、 全局 8 大私有倉庫職責解耦架構（`1 中樞 + 7 核心`）

前期所有倉庫均設為 **Private（私有孵化）**，在本地開發目錄 `/home/shubuzuo/code/zhengjue/` 下透過頂層 `pnpm-workspace.yaml` 聚合聯調：

<div align="center">
  <img src="https://raw.githubusercontent.com/zhengjue-canon/.github/main/assets/arch-repos-topology.svg" width="100%" alt="《正覺藏》全局 8 大核心倉庫職責解耦與 AI 驅動架構拓撲圖" />
</div>

### 組織核心倉庫導航與邊界劃分

| 序號 | 倉庫名稱 | 當前狀態 | 核心職責與包含模組 | 核心技術棧 |
| :---: | :--- | :---: | :--- | :--- |
| **1** | 📚 **[`zhengjue-docs`](https://github.com/zhengjue-canon/zhengjue-docs)** | **Private** | **全局文檔、Wiki、歷史考證、AI 可執行需求規格與排期中樞**：存放歷年會員大會考證報告、`GLOSSARY.yaml`、`REQ-01..06` 需求規格卡、`ADR` 架構決策、藏經編審凡例 Wiki 及全局 `ROADMAP.md` / `TODO.md`。 | `Markdown` · `YAML Specs` · `Mermaid / SVG` · `AI Context Routing` |
| **2** | 🔧 **[`cbeta-markdown`](https://github.com/zhengjue-canon/cbeta-markdown)** | **Private** *(成熟後 MIT 開源)* | **CBETA XML ⇄ 原始基準快照與雙軌無損 Markdown 雙向編譯與驗證引擎**：含 `xml2baseline`、`md2xml`、`verifier` L0～L3 四級零丟失驗證器、`rebase` 上游發版三路變基工具及 `docx2changes` 存量 Word 差分導入器。 | `TypeScript` · `Node 22` · `fast-xml-parser` · `unified/remark` · `worker_threads` |
| **3** | 🧬 **[`canon-core`](https://github.com/zhengjue-canon/canon-core)** | **Private** | **跨四端共享核心協議與狀態重放內核**（`@zhengjue/schema`、`@zhengjue/standoff`、`@zhengjue/ledger`、`@zhengjue/api-client`）：封裝 CJK 擴展區安全之 `CodePointString` 尋址器、`ChangeLedger` 確定性重放引擎與 Zod 契約。 | `Pure TypeScript` · `Zod` · `openapi-typescript` |
| **4** | 📜 **[`zhengjue-corpus`](https://github.com/zhengjue-canon/zhengjue-corpus)** | **Private** | **《正覺藏》千年數位資產與全量變更帳本主倉**：存放四部判教目錄（`catalog/`）及五位一體經卷結構（`*.cbeta.json` 原始基準、`*.changes.jsonl` 全量改動帳本、`articles/*.md` 修改意見專文、`*.md` 定稿主文、`*.standoff.json` 伴生圖層）。 | `ZJ-Markdown` · `JSONL Change Ledger` · `Standoff JSON` · `Git Signed Commits` |
| **5** | ⚙️ **[`zhengjue-server`](https://github.com/zhengjue-canon/zhengjue-server)** | **Private** | **後端核心 API 服務與檢索引擎調度中心**：提供經卷與變更帳本查詢、評審與內部 Markdown 專文工作流、「我的評審」中心 API、大眾質疑預篩分流及 Git 雙向自動簽核同步。 | `Fastify 5` · `PostgreSQL 16 (GiST int4range)` · `Drizzle ORM` · `Meilisearch` · `opencc-js` |
| **6** | 🖥️ **[`zhengjue-admin`](https://github.com/zhengjue-canon/zhengjue-admin)** | **Private** | **編審工作台與後台管理端（Studio + Admin 二合一）**：<br>• **審定工作台**：同修初標台、平實導師大字號極簡審定台、評審時同屏直接撰寫 Markdown 專文台、**「我的評審與文章中心」**、存量 `.docx` 差分導入核對台；<br>• **管理後台**：大眾質疑審校與親教師答覆台、四部目錄與 RBAC 權限管理。 | `React 19` · `Vite 6` · `TanStack Router & Query` · `Tailwind CSS v4` · `shadcn/ui` |
| **7** | 🌐 **[`zhengjue-web`](https://github.com/zhengjue-canon/zhengjue-web)** | **Private** | **公開在線藏經閣閱讀與全透明溯源共創 Web 端**：面向全球讀者的點閱門戶（SSG/ISR）、正覺 8 種字型排版、訂正字入正文與全過程改動歷史透明對照、點擊展開閱讀完整修改意見專文、劃詞發起質疑/糾錯/提問。 | `Next.js 15 (App Router)` · `React 19` · `Tailwind CSS v4` · `Typst PDF 導出` |
| **8** | 📱 **[`zhengjue-mobile`](https://github.com/zhengjue-canon/zhengjue-mobile)** | **Private** | **跨平台移動端與平板端原生 App（iOS / Android / iPadOS）**：內置離線藏經閣引擎（SQLite FTS5 本地毫秒級繁簡全文檢索、離線查閱改動溯源與評審專文）、護眼宣紙精讀、以及 **iPad 平板導師/親教師大字號觸控審閱模式**。 | `React Native (Expo 52+)` · `op-sqlite (SQLite FTS5)` · `@shopify/flash-list` |
| **0** | 🏛️ **[`.github`](https://github.com/zhengjue-canon/.github)** | **Public** | 組織主頁配置、全局架構設計圖與公共視覺資產庫。 | `GitHub Profile` · `Pure Vector SVG Architecture` |

---

## 三、 `cbeta-markdown` 四級零丟失驗證、狀態重放守恆與上游三路變基設計

<div align="center">
  <img src="https://raw.githubusercontent.com/zhengjue-canon/.github/7583ef606db87739a8cf9484b9dd15e0630753bf/assets/arch-zero-loss-rebase.svg" width="100%" alt="cbeta-markdown 四級零丟失形式化驗證與上游持續發版三路變基架構圖" />
</div>

1. **源頭導入四級零丟失驗證（`CBETA XML ⇄ 001.cbeta.json`）**：透過 L0 窮盡式狀態機、L1 純字流 `SHA-256` 守恆（禁 NFKC 歸一化，100% 保留異體字原碼位）、L2 結構與 `<app><lem>` 校勘錨點守恆帳本、L3 雙向往返同構驗證，確保原始基準一字一符零丟失。
2. **編審演進確定性重放守恆（`Project(001.cbeta.json, 001.changes.jsonl) === 001.md`）**：最終公開版 `001.md` 中的每一處標點修改與底本錯字訂正（`TEXT_EMENDATION`），均須 100% 由 `001.changes.jsonl` 中帶有「更改人 + 審閱人 + 修改意見/專文」之記錄精確重放生成；任何未登記之字詞變動立即報錯阻斷。

---

## 四、 多端協同全流程與雙階段「質疑 / 補充糾正 / 提問」狀態機設計

<div align="center">
  <img src="https://raw.githubusercontent.com/zhengjue-canon/.github/58a1d9e69d7fa102b36472166c2c199967da8edb/assets/arch-workflow-state.svg" width="100%" alt="《正覺藏》多端協同編審發布全流程與內外部雙階段質疑處理狀態機" />
</div>

---

<div align="center">
  <sub><b>正覺同修會 · 《正覺藏》數位工程委員會</b> | 以八識正理審定句讀，令正法久住千年</sub>
</div>
