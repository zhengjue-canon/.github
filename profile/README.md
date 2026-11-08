<div align="center">

<img src="https://raw.githubusercontent.com/zhengjue-canon/.github/8ddd1e3d4d8ff64abd1b64774e10ceb231ee20c2/assets/canon-scripture.svg" width="200" height="162" alt="《正覺藏》大藏經典籍與朱筆句讀經卷" />

# 《正覺藏》數位藏經工程 (Zhengjue Canon)

**正本清源 · 重新句讀審定 · 辨正偽經偽論 · 奠定正法久住千年基業**

[![Official Website](https://img.shields.io/badge/正覺同修會全球資訊網-enlighten.org.tw-D4AF37?style=for-the-badge)](https://www.enlighten.org.tw)
[![Electronic Newsletter](https://img.shields.io/badge/正智出版社·正覺電子報-books.enlighten.org.tw-8A5A10?style=for-the-badge)](https://books.enlighten.org.tw/zh-tw/e)
[![Architecture](https://img.shields.io/badge/底本架構-ZJ--Markdown_%2B_Standoff_JSON-2E1D0E?style=for-the-badge)](https://github.com/zhengjue-canon/zhengjue-platform)

<img src="https://raw.githubusercontent.com/zhengjue-canon/.github/7384790573a86bd2383f6f6bbc006a64934f5c10/assets/banner.svg" width="100%" alt="Zhengjue Canon Banner" />

</div>

---

## 一、 緣起與核心使命

本組織（`zhengjue-canon`）致力於構建**《正覺藏》（《正覺大藏經》）**全流程數位化編審、重新句讀、多字型排版、電腦注解式劃詞辨正與高併發在線閱讀平台：

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
5. **分階段協同「提出質疑 / 補充糾正 / 相關提問」與官網高併發閱讀**：
   - 支援內外部學人針對任意經文區間、句讀或批注提交結構化句讀糾錯（`PunctuationPatch`）、法義質疑與修學提問；經審校與親教師撰寫辨正答覆後，將具代表性之**「大眾質疑 + 正覺辨正回覆」**公開掛載於經文旁，並透過靜態化邊緣快取支援百人至萬人同時在線流暢點閱。

---

## 二、 組織核心倉庫導航

| 倉庫名稱 | 定位與職責 | 核心技術棧 |
| :--- | :--- | :--- |
| 📦 **[`zhengjue-platform`](https://github.com/zhengjue-canon/zhengjue-platform)** | **核心工程代碼倉（Monorepo）**：包含 Standoff 偏移引擎、CBETA 轉換與零漏字校驗器、佛典字格交互組件庫、導師極簡審定工作台（`studio-web`）、官網高併發閱讀與共創端（`reader-web`）及後端服務（`api-server`）。 | `TypeScript` · `pnpm + Turborepo` · `Next.js` · `Fastify` · `PostgreSQL (GiST int4range)` · `Meilisearch` |
| 📜 **[`zhengjue-corpus`](https://github.com/zhengjue-canon/zhengjue-corpus)** | **《正覺藏》數位語料資產倉**：存放經 `cbeta2zjmd` 轉換並通過 100% 逐字哈希校驗之雙軌制經卷主文件（`.md`）與伴生圖層文件（`.standoff.json`），以及四維藏經目錄樹與簽核歷史。 | `ZJ-Markdown` · `Standoff JSON` · `YAML Catalog` · `SHA-256 零篡改校驗` |
| 🏛️ **[`.github`](https://github.com/zhengjue-canon/.github)** | 組織主頁配置、視覺規範與公共文檔庫。 | `GitHub Profile` · `SVG Assets` |
