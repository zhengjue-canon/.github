<div align="center">

<img src="https://raw.githubusercontent.com/zhengjue-canon/.github/8ddd1e3d4d8ff64abd1b64774e10ceb231ee20c2/assets/canon-scripture.svg" width="200" height="162" alt="《正覺藏》大藏經典籍與朱筆句讀經卷" />

# 《正覺藏》數位藏經工程 (Zhengjue Canon)

**正本清源 · 重新句讀審定 · 辨正偽經偽論 · 奠定正法久住千年基業**

[![Official Website](https://img.shields.io/badge/正覺同修會全球資訊網-enlighten.org.tw-D4AF37?style=for-the-badge)](https://www.enlighten.org.tw)
[![Electronic Newsletter](https://img.shields.io/badge/正智出版社·正覺電子報-books.enlighten.org.tw-8A5A10?style=for-the-badge)](https://books.enlighten.org.tw/zh-tw/e)
[![Architecture](https://img.shields.io/badge/底本架構-ZJ--Markdown_%2B_Standoff_JSON-2E1D0E?style=for-the-badge)](https://github.com/zhengjue-canon/zhengjue-corpus)

<img src="https://raw.githubusercontent.com/zhengjue-canon/.github/7384790573a86bd2383f6f6bbc006a64934f5c10/assets/banner.svg" width="100%" alt="Zhengjue Canon Banner" />

</div>

---

## 一、 緣起與核心使命

本組織（`zhengjue-canon`）致力於構建**《正覺藏》（《正覺大藏經》）**全流程數位化編審、重新句讀、多字型排版、電腦注解式劃詞辨正與跨平台（Web / 桌面審定端 / iOS & Android 移動端）高併發閱讀共創體系：

1. **正本清源、重編藏經目錄**：
   - 依佛滅後第一次七葉窟內五百阿羅漢結集與七葉窟外千人大眾部大乘結集之正統標準，重構**「正法藏部 · 正覺法寶部 · 部派論典辨正部 · 偽佛法部」**四維典籍體系；
   - 徹底剔除 2016 年版 CBETA《大藏經補編》所混入之宗喀巴《廣論》等喇嘛教外道著作及近代六識論邪說；
   - 對《大正藏》原密教部偽經（如《大日經》《金剛頂經》《大乘莊嚴寶王經》等）歸入**偽佛法部**，一對一掛載辨正專文並標註「剪貼簿式」法位錯置段落；
   - 為遭歐美日學術界誣指為「疑偽」之真實大乘經論（如《楞嚴經》《大乘起信論》《占察善惡業報經》等）審定平反。
2. **分散式初標與導師逐卷句讀審定**：
   - 糾正《大正藏》與既有電子佛典因不明八識論真義而導致之斷句錯謬（如《成唯識論述記》等），由破參同修透過網路協同初標現代標點逗標，最終由 **平實導師親自逐卷審定簽核**。
3. **正覺多字型語義排版還原**：
   - 完整收錄 平實導師與正覺同修會全部講經講義、《成唯識論釋》與專書，嚴格還原正覺書籍特有之 **8 種語義字型體系**（區分`經文`、`頌文`、`論文`、`問句`、`判教提示`、`白話語譯`、`導師釋文`、`編案`）。
4. **「類電腦檔案注解功能」之不改原文劃詞辨正**：
   - 針對部派佛教凡夫僧論典（如《大毘婆沙論》、安慧《大乘廣五蘊論》等），鎖定底本原文一字不改，採用**分離式偏移錨定（Standoff Annotation）**技術挑選論文段落，旁批注解其文意、錯誤落處與法義過失。
5. **內外部雙階段「提出質疑 / 補充糾正 / 相關問題」與多端離線/在線閱讀**：
   - 前期面向系統內同修協同勘誤，後期向社會公眾開放；支援針對任意經文區間、句讀或批注提交結構化句讀糾錯（`PunctuationPatch`）、法義質疑與修學提問；經審校與親教師撰寫辨正答覆後，將具代表性之**「大眾質疑 + 正覺辨正回覆」**公開掛載於經文旁。

---

## 二、 全局多倉庫職責解耦架構（7 大核心倉庫矩陣）

按照**「開源公益與內部業務解耦、前後端與多端演進週期解耦、公網閱讀與高權限後台安全物理隔離」**原則，本組織採用 **7 大核心倉庫 + 共享協議底座** 之架構設計：

```mermaid
flowchart TB
    subgraph Upstream ["外部上游數據源 (持續發版演進)"]
        CBETA["cbeta-org/xml-p5 (Git 持續發版)<br/>+ cbeta_gaiji 缺字庫 + 校勘元數據"]
    end

    subgraph OpenSourceLayer ["第一層：開源標準與跨端核心底座 (Public / MIT)"]
        Repo1["1. cbeta-markdown (公開開源)<br/>CBETA XML ⇄ 雙軌無損 Markdown 編譯器<br/>四級零丟失驗證器 + 上游發版三路變基引擎"]
        Repo2["2. canon-core (跨端共享核心 SDK)<br/>Unicode 字格尋址引擎 + 區間樹算法<br/>8 種語義字型規範 + Zod/OpenAPI 契約"]
    end

    subgraph DataLayer ["第二層：千年數位藏經資產主倉 (Public Read / 受控簽核)"]
        Repo3["3. zhengjue-corpus (藏經語料主倉)<br/>四部判教目錄 (catalog/) + 經卷 (.md & .standoff.json)<br/>cbeta-lock.json + 全藏零丟失哈希帳本"]
    end

    subgraph ServiceLayer ["第三層：後端核心服務與檢索引擎"]
        Repo4["4. zhengjue-server (後端 API 與調度中心)<br/>Fastify API + PostgreSQL (int4range) + Meilisearch<br/>審定工作流狀態機 + 質疑分流 + Git 雙向同步"]
    end

    subgraph ClientLayer ["第四層：三大終端應用倉 (前後端分離 + 多端覆蓋)"]
        Repo5["5. zhengjue-admin (編審工作台與管理端)<br/>同修字格初標台 + 導師大字號極簡審定台<br/>劃詞辨正批注器 + 大眾質疑審核後台 + 目錄權限管理"]
        Repo6["6. zhengjue-web (公開在線藏經閣 Web 端)<br/>SSG/ISR 高併發閱讀 + 8 種字型還原<br/>新舊句讀對比 + 電腦式旁批抽屜 + 劃詞質疑/提問"]
        Repo7["7. zhengjue-mobile (移動端與平板端 App)<br/>iOS / Android / iPadOS (Expo + SQLite FTS5)<br/>整部經論離線包秒搜 + 護眼閱讀 + 平板觸控審閱模式"]
    end

    CBETA ==>|持續發版同步 & 三路變基| Repo1
    Repo1 ==>|產出與驗證 100% 無損語料| Repo3
    Repo2 -.->|共享算法與類型契約| Repo1 & Repo4 & Repo5 & Repo6 & Repo7
    Repo3 <==>|Git 簽核持久化 / 靜態快照構建| Repo4
    Repo4 <==>|REST / OpenAPI / WebSocket| Repo5 & Repo6 & Repo7
```

### 組織核心倉庫導航與邊界劃分

| 序號 | 倉庫名稱 | 開源策略 | 核心職責與包含模組 | 核心技術棧 |
| :---: | :--- | :---: | :--- | :--- |
| **1** | 🔧 **`cbeta-markdown`** | **Public (MIT)** | **CBETA TEI-P5 XML ⇄ 雙軌無損 Markdown 雙向編譯與驗證引擎**：含 `xml2md` 正向編譯器、`md2xml` 逆向還原器、`verifier` 四級零丟失形式化驗證器、`rebase` 上游發版三路變基工具（零正覺業務耦合，面向全球佛學與數位人文社區開源）。 | `TypeScript` · `Node 22` · `fast-xml-parser` · `unified/remark` · `worker_threads` |
| **2** | 🧬 **`canon-core`** | **Public** | **跨四端共享核心協議與算法 SDK**（`@zhengjue/schema`、`@zhengjue/standoff`、`@zhengjue/api-client`）：封裝 CJK 擴展區生僻字安全之 `CodePointString` 字格尋址器與區間樹（Interval Tree）算法，確保後端、Web、管理端、移動端字偏移計算 100% 同構。 | `Pure TypeScript` · `Zod` · `openapi-typescript` |
| **3** | 📜 **[`zhengjue-corpus`](https://github.com/zhengjue-canon/zhengjue-corpus)** | **Public** (受控寫入) | **《正覺藏》千年數位資產語料主倉**：獨立存放四部判教目錄（`catalog/`）、雙軌制經卷（`.md` + `.standoff.json`）、上游版本鎖（`cbeta-lock.json`）及全藏零丟失驗證帳本（`integrity-manifest.json`）。 | `ZJ-Markdown` · `Standoff JSON` · `YAML Catalog` · `Git Signed Commits` |
| **4** | ⚙️ **`zhengjue-server`** | **Private** | **後端核心 API 服務與檢索引擎調度中心**：提供經卷與伴生圖層高併發查詢、同修初標 $\rightarrow$ 導師審定簽核狀態機、大眾質疑/糾錯工單預篩分流、上游變基任務調度及 Git 雙向自動同步。 | `Fastify 5` · `PostgreSQL 16 (GiST int4range)` · `Drizzle ORM` · `Meilisearch` · `opencc-js` |
| **5** | 🖥️ **`zhengjue-admin`** | **Private** (高權限) | **編審工作台與後台管理端（Studio + Admin 二合一）**：<br>• **審定工作台**：同修字格點選初標台、平實導師大字號極簡審定台、部派/偽經劃詞辨正批注器、CBETA 上游升級衝突三欄審閱台；<br>• **教務管理後台**：大眾質疑/補充糾正審校與親教師答覆台、四部目錄編排與 RBAC 權限審計。 | `React 19` · `Vite 6` · `TanStack Router & Query` · `Tailwind CSS v4` · `shadcn/ui` |
| **6** | 🌐 **`zhengjue-web`** | **Public** | **公開在線藏經閣閱讀與眾包考據 Web 端**：面向全球讀者的高併發點閱門戶（SSG/ISR + CDN 邊緣快取）、正覺 8 種語義字型排版、新舊句讀一鍵對照、電腦式旁批軌道、劃詞發起「質疑 / 補充糾正 / 提問」。 | `Next.js 15 (App Router)` · `React 19` · `Tailwind CSS v4` · `Typst PDF 導出` |
| **7** | 📱 **`zhengjue-mobile`** | **Private** (上架商店) | **跨平台移動端與平板端原生 App（iOS / Android / iPadOS）**：內置離線藏經閣引擎（支援整部/全藏離線下載與本地毫秒級繁簡全文檢索）、護眼宣紙精讀、書籤筆記雲同步，以及 **iPad 平板導師/親教師大字號觸控審閱模式**。 | `React Native (Expo 52+)` · `op-sqlite (SQLite FTS5)` · `@shopify/flash-list` |
| **0** | 🏛️ **[`.github`](https://github.com/zhengjue-canon/.github)** | **Public** | 組織主頁配置、全局架構設計藍圖與公共視覺資產庫。 | `GitHub Profile` · `Mermaid / SVG Architecture` |

---

## 三、 `cbeta-markdown` 開源底座：零信息丟失驗證與上游持續發版變基設計

現有開源 CBETA 轉 Markdown 工具普遍存在「靜默丟失 `<lg><l>` 偈頌、丟失雙行夾注、丟失宋元明麗校勘記與行號座標」之嚴重缺陷。`cbeta-markdown` 透過**雙軌無損分流**、**四級形式化驗證**與**三路字符偏移變基**徹底攻克上述難題。

### 1. 四級零丟失形式化驗證體系（4-Level Zero-Loss Verification Pipeline）

每一卷經文轉換前後，必須通過獨立於編譯器之外的四道數學守恆關卡，確保**正文乃至一切重要結構與校勘信息一字一符零丟失**：

```mermaid
flowchart TD
    XML["原始 CBETA XML-P5 經卷"] --> Compiler["cbeta2md 編譯器<br/>(L0: Fail-Closed 窮盡式狀態機)"]
    Compiler -->|遇到任何未註冊標籤/屬性| Fail0["❌ 立即報錯阻斷 (UnhandledXmlNodeError)"]
    Compiler --> Output["產出雙軌文件：<br/>fascicle.md + fascicle.standoff.json"]

    XML & Output --> L1["L1: 正文與夾注逐字序列 SHA-256 守恆校驗<br/>(Canonical Character Stream Invariant)"]
    L1 -->|哪怕 1 個字或碼位不一致| Fail1["❌ 二分哈希毫秒定位出錯字格與行號"]

    L1 -->|通過| L2["L2: 結構與校勘元數據計數及區間守恆帳本<br/>(Structural & Apparatus Conservation Ledger)"]
    L2 -->|科判/偈頌/行號/校勘記/舊標點數量或錨點不符| Fail2["❌ 輸出字段級差異帳本報錯"]

    L2 -->|通過| L3["L3: 雙向往返同構驗證 (終極數學證明)<br/>md2cbeta(md, standoff) → Reconstructed XML AST"]
    XML --> L3
    L3 -->|還原後的 XML AST 與原 XML AST 存在差異| Fail3["❌ AST Tree Diff 報錯"]

    L3 -->|100% 同構通過| Pass["✅ 簽發零丟失加密審計憑證<br/>寫入 integrity-manifest.json"]
```

- **L0 窮盡式 Fail-Closed 狀態機（未知節點零容忍）**：拒絕白名單抽取模式；凡 XML 中出現之任何標籤、屬性或文本節點均須顯式核銷，遇到任何未定義標籤立即報錯終止，絕不靜默丟棄。
- **L1 正文與夾注純字符流 SHA-256 守恆 + 二分哈希定位**：獨立提取器直接從原 XML 提取純漢字序列 $\mathcal{S}_{\text{main}}$ 與雙行夾注序列 $\mathcal{S}_{\text{inline}}$（**嚴禁執行會破壞古籍異體字的 NFKC 歸一化**，100% 保留 `說/説`、`真/眞` 原碼位），與 `.md` 提取結果比對字數與 `SHA-256`；一旦有 1 字差異，透過**二分前綴哈希搜尋**在 `< 1ms` 內精準定位至具體第 $k$ 字與 `<pb>/<lb>` 行號。
- **L2 結構、座標、校勘記與舊標點守恆帳本**：逐項核對 `<pb>/<lb>` 里程碑、`::keping` 科判樹、`:::gatha` 偈頌句數；並以 `.standoff.json` 中每條 `<app>` 的字格區間 `[start, end)` 反查 `.md` 純字流，斷言截取出的文字 **100% 等於原 XML `<lem>` 底本文字**；同時驗證將 `legacyPunctuation` 插回純字流後與原 XML 帶標點正文完全相等。
- **L3 雙向往返同構驗證（`XML ⇄ MD+Standoff`）**：內置逆向編譯器 `md2cbeta`，將 `.md + .standoff.json` 逆向還原為 TEI-P5 XML AST 並與原 XML AST 進行規範化同構比對，從信息論上給出 **100% 無損轉換** 之終極證明。

### 2. 上游 CBETA 持續發版同步：三路字符偏移變基引擎（3-Way Offset Rebase）

當上游 `cbeta-org/xml-p5` 持續發版（修正底本錯字、更新缺字表或增補校勘記）時，`cbeta2md rebase` 透過三路變基算法自動保護《正覺藏》已審定之新句讀與導師批注：

```mermaid
flowchart LR
    subgraph Upstream ["上游 CBETA 演進"]
        BaseV1["CBETA XML v1<br/>(舊基準底本)"]
        BaseV2["CBETA XML v2<br/>(上游新發版)"]
    end

    subgraph Engine ["cbeta-markdown 三路變基引擎 (cbeta2md rebase)"]
        Diff["1. 純字流 Myers 差分<br/>計算位移映射函數 φ(idx_v1) → idx_v2"]
        PunctRebase["2. 句讀與多字型圖層變基<br/>無衝突區間自動平移新逗標與字型"]
        StandoffRebase["3. Standoff 區間樹變基<br/>[start, end) → [φ(start), φ(end))"]
        ConflictFlag["4. 變動字格精準衝突標記<br/>僅當上游修改了批注覆蓋字時觸發人工確認"]
    end

    subgraph Downstream ["下游《正覺藏》語料倉"]
        ZJ_V1["正覺藏 v1<br/>(含導師新句讀 + 劃詞辨正)"]
        ZJ_V2["正覺藏 v2<br/>(同步上游修正 + 保留正覺句讀與批注)"]
    end

    BaseV1 & BaseV2 --> Diff
    ZJ_V1 --> PunctRebase & StandoffRebase
    Diff --> PunctRebase & StandoffRebase
    PunctRebase & StandoffRebase --> ConflictFlag --> ZJ_V2
```

---

## 四、 多端協同全流程與雙階段「質疑 / 補充糾正 / 提問」設計圖

### 1. 跨倉庫、多終端協同編審與發布時序圖

```mermaid
sequenceDiagram
    autonumber
    participant CBETA as cbeta-org/xml-p5 (上游)
    participant Conv as 1. cbeta-markdown (開源轉換/驗證)
    participant Corpus as 3. zhengjue-corpus (Git 語料主倉)
    participant Server as 4. zhengjue-server (後端 API/DB)
    participant Admin as 5. zhengjue-admin (導師審定/管理後台)
    participant Web as 6. zhengjue-web (公開藏經閣 Web)
    participant Mobile as 7. zhengjue-mobile (手機/iPad 端)

    CBETA->>Conv: 1. 拉取 XML 源數據或上游新版增量
    Conv->>Conv: 2. 轉換雙軌 .md + .standoff.json 並跑通【L0-L3 四級零丟失驗證】
    Conv->>Corpus: 3. 寫入基準語料與 integrity-manifest.json
    Corpus->>Server: 4. 同步入庫 PostgreSQL (int4range) 與 Meilisearch 索引
    Admin->>Server: 5. 破參同修初標句讀 → 平實導師大字號審定簽核 + 劃詞撰寫辨正批注
    Server->>Corpus: 6. 自動提交導師簽核 Git Commit 並打包離線 SQLite 增量包
    Server->>Web: 7. 觸發 ISR 刷新，全球讀者在線點閱 8 種字型經文與旁批
    Server->>Mobile: 8. 推送離線經卷增量包，手機/iPad 端離線秒搜與精讀
    Web->>Server: 9. 讀者/同修劃詞提交「質疑 / 補充糾正 / 提問」
    Mobile->>Server: 10. 移動端長按劃詞提交「質疑 / 提問」
    Server->>Admin: 11. 進入「質疑分流審校台」：合入句讀補丁 或 親教師撰寫辨正答覆並公開掛載
```

### 2. 「前期對內、後期公開」之質疑 / 補充糾正 / 提問狀態機

```mermaid
stateDiagram-v2
    [*] --> 讀者或同修劃詞提交: 選中經文區間 [start, end) 或某處斷句/批注
    讀者或同修劃詞提交 --> 待預篩分流(PENDING_TRIAGE): 預設僅【提交者本人 + zhengjue-admin 後台】可見
    
    state 待預篩分流(PENDING_TRIAGE) {
        [*] --> 規則與語義去重: 檢測是否已有相同法義辨正或重複勘誤
    }

    待預篩分流(PENDING_TRIAGE) --> 句讀或文字勘誤流: 類型 = 補充糾正 (帶 PunctuationPatch)
    待預篩分流(PENDING_TRIAGE) --> 法義辨正與問答流: 類型 = 提出質疑 / 相關問題
    待預篩分流(PENDING_TRIAGE) --> 歸檔摺疊(REJECTED): 無意義灌水或重複工單

    句讀或文字勘誤流 --> 導師或編審老師審閱: 在 zhengjue-admin 高亮預覽標點 Diff
    導師或編審老師審閱 --> 一鍵合入新版本(ACCEPTED_MERGED): 自動更新 .md 標點並記入勘誤致謝榜

    法義辨正與問答流 --> 親教師撰寫辨正答覆: 引用聖教量與正覺法寶辨析過失
    親教師撰寫辨正答覆 --> 審定並公開掛載(ANSWERED_PUBLISHED): 將【質疑原文 + 正覺辨正回覆】公開展示於經文旁
```

---

<div align="center">
  <sub><b>正覺同修會 · 《正覺藏》數位工程委員會</b> | 以八識正理審定句讀，令正法久住千年</sub>
</div>
