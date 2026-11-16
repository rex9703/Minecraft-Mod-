# MCMOD 模組精選百科與結構指南 — AI 協作與開發規範 (AGENTS.md)

## 1. 專案目的與定位
本專案為一個互動式 **Minecraft (Java 版 1.20.1 / 1.21.1) 模組精選百科網站**，參考 MC百科 (MCMOD) 的資料分類邏輯，整理常見的科技工業、冒險頭目、史詩地形生成與渲染優化模組。透過「資料與視圖分離（Data-View Separation）」的設計，讓玩家能快速檢索各模組的核心機制、世界生成座標、前置依賴與硬體相容性建議。

## 2. 視覺風格與 UI 規範
- **技術框架**：使用單頁式 HTML5 搭配 **Tailwind CSS (CDN)** 與 **Font Awesome 6 圖示庫**，無須額外編譯環境即可部署於 GitHub Pages。
- **色彩系統**：
  - 背景主色：深石板灰 (`bg-slate-900`、`bg-slate-800`)，營造沉浸式深色閱讀體驗。
  - 強調主色：祖母綠 (`emerald-500` / `emerald-600`)，用於選中狀態、主要按鈕與重點標示。
  - 分類標籤色系：
    - 科技與工業 (`tech`)：琥珀黃 (`bg-amber-500/20 text-amber-300 border-amber-500/30`)
    - 冒險與頭目 (`adventure`)：玫瑰紅 (`bg-rose-500/20 text-rose-300 border-rose-500/30`)
    - 世界與地形生成 (`worldgen`)：青色 (`bg-cyan-500/20 text-cyan-300 border-cyan-500/30`)
    - 渲染與效能優化 (`performance`)：翠綠色 (`bg-emerald-500/20 text-emerald-300 border-emerald-500/30`)
- **版面配置**：
  - 左側為固定式 Wiki 分類導覽列（支援桌面端快速篩選與數量統計）。
  - 右側上方為 Sticky 即時關鍵字搜尋列與行動端過濾按鈕，下方為響應式卡片網格（RWD Grid）與詳情彈出視窗（Modal）。

## 3. 檔案結構
- `index.html`：主應用程式（包含左側導覽、搜尋過濾邏輯、Modal 彈窗與 `modsData` 核心資料庫）
- `AGENTS.md`：AI 協作規則與資料擴充標準（本檔案）
- `README.md`：專案說明文件

## 4. 資料結構與 AI 擴充規則 (Data Schema)
本網站的所有模組卡片與詳情彈窗皆由 `index.html` 內部的 `modsData` JavaScript 陣列動態渲染。
**當 AI 被要求「新增一個模組介紹」時，請勿破壞既有 HTML DOM 結構，僅需遵循以下 JSON Schema 在 `modsData` 陣列中新增物件：**

```javascript
{
    id: Number,                  // 遞增之唯一編號 (例如: 7)
    name: String,                // 模組中文譯名 (例如: "機械動力：飛空艇")
    enName: String,              // 模組英文原名 (例如: "Create Aeronautics")
    category: String,            // 必須為 'tech' | 'adventure' | 'worldgen' | 'performance' 其中之一
    categoryName: String,        // 對應之中文分類名稱 ("科技與工業" | "冒險與頭目" | "世界與地形生成" | "渲染與效能優化")
    badgeColor: String,          // 對應分類之 Tailwind 顏色 class
    versions: String,            // 主流支援版本 (例如: "1.20.1 / 1.21.1")
    loaders: String,             // 支援載入器 (例如: "NeoForge / Forge / Fabric")
    summary: String,             // 50~80 字之模組核心定位簡介（顯示於卡片正面）
    mechanics: [                 // 陣列：包含 3 點核心機制或重點玩法（顯示於詳情 Modal）
        "機制重點 1...",
        "機制重點 2...",
        "機制重點 3..."
    ],
    worldGenInfo: String,        // 說明該模組之礦物分佈高度 (Y 座標)、結構生成群系，若為純客戶端模組則註明不影響世界生成
    addons: String,              // 必備前置模組 (Dependencies) 與推薦聯動之附屬模組
    compatibilityNotes: String   // 渲染優化衝突、伺服器 TPS 負載或硬體調校實務建議
}
