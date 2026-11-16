<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MCMOD 模組精選百科與結構指南</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700&display=swap');
        body { font-family: 'Noto Sans TC', sans-serif; }
        /* 自訂捲軸樣式 */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #0f172a; }
        ::-webkit-scrollbar-thumb { background: #334155; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #10b981; }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 flex h-screen overflow-hidden">

    <!-- 1. 左側固定導覽列 (Sidebar - 對應 AGENTS.md 的 Wiki 架構) -->
    <aside class="w-64 bg-slate-800 border-r border-slate-700 flex flex-col justify-between hidden lg:flex shrink-0">
        <div>
            <!-- 網站 Logo 與標題 -->
            <div class="p-5 border-b border-slate-700 flex items-center space-x-3">
                <div class="w-9 h-9 bg-emerald-600 rounded-lg flex items-center justify-center text-white shadow-lg">
                    <i class="fa-solid fa-cubes text-lg"></i>
                </div>
                <div>
                    <span class="font-bold text-base tracking-wide text-white block">MCMOD 精選百科</span>
                    <span class="text-[11px] text-emerald-400">NeoForge / Fabric 知識庫</span>
                </div>
            </div>

            <!-- 分類快速導覽 -->
            <div class="p-4">
                <p class="text-xs font-bold text-slate-400 uppercase tracking-wider px-3 mb-2">模組分類導覽</p>
                <nav class="space-y-1" id="sidebarNav">
                    <button data-filter="all" class="sidebar-btn w-full flex items-center justify-between px-3 py-2.5 rounded-lg bg-emerald-600 text-white text-sm font-medium transition cursor-pointer">
                        <span><i class="fa-solid fa-layer-group w-5 text-center mr-1.5"></i>全部模組總覽</span>
                        <span class="text-xs bg-emerald-700 px-2 py-0.5 rounded-full" id="count-all">6</span>
                    </button>
                    <button data-filter="tech" class="sidebar-btn w-full flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-300 hover:bg-slate-700/70 text-sm font-medium transition cursor-pointer">
                        <span><i class="fa-solid fa-gears w-5 text-center mr-1.5 text-amber-400"></i>科技與工業</span>
                        <span class="text-xs bg-slate-700 text-slate-300 px-2 py-0.5 rounded-full">2</span>
                    </button>
                    <button data-filter="adventure" class="sidebar-btn w-full flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-300 hover:bg-slate-700/70 text-sm font-medium transition cursor-pointer">
                        <span><i class="fa-solid fa-skull w-5 text-center mr-1.5 text-rose-400"></i>冒險與頭目</span>
                        <span class="text-xs bg-slate-700 text-slate-300 px-2 py-0.5 rounded-full">1</span>
                    </button>
                    <button data-filter="worldgen" class="sidebar-btn w-full flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-300 hover:bg-slate-700/70 text-sm font-medium transition cursor-pointer">
                        <span><i class="fa-solid fa-mountain-sun w-5 text-center mr-1.5 text-cyan-400"></i>世界與地形生成</span>
                        <span class="text-xs bg-slate-700 text-slate-300 px-2 py-0.5 rounded-full">1</span>
                    </button>
                    <button data-filter="performance" class="sidebar-btn w-full flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-300 hover:bg-slate-700/70 text-sm font-medium transition cursor-pointer">
                        <span><i class="fa-solid fa-bolt w-5 text-center mr-1.5 text-emerald-400"></i>渲染與效能優化</span>
                        <span class="text-xs bg-slate-700 text-slate-300 px-2 py-0.5 rounded-full">2</span>
                    </button>
                </nav>
            </div>

            <!-- AGENTS.md 規範提示區塊 -->
            <div class="mx-4 p-3.5 bg-slate-900/80 border border-slate-700/80 rounded-xl text-xs space-y-1.5">
                <div class="flex items-center text-emerald-400 font-bold gap-1.5">
                    <i class="fa-solid fa-robot"></i>
                    <span>AI 擴充架構 (AGENTS.md)</span>
                </div>
                <p class="text-slate-400 leading-relaxed">
                    本百科採用標準化資料結構，AI 可依據專案根目錄之 <code class="text-amber-300 bg-slate-800 px-1 rounded">AGENTS.md</code> 規則，自動生成新模組條目或獨立子頁面。
                </p>
            </div>
        </div>

        <!-- 底部資訊 -->
        <div class="p-4 border-t border-slate-700 text-xs text-slate-500 flex justify-between items-center">
            <span>MCMOD Wiki &copy; 2026</span>
            <a href="https://github.com/rex9703/Minecraft-Mod-" target="_blank" class="text-slate-400 hover:text-white transition">
                <i class="fa-brands fa-github text-base"></i>
            </a>
        </div>
    </aside>

    <!-- 2. 右側主要內容區 -->
    <div class="flex-1 flex flex-col h-screen overflow-y-auto">
        
        <!-- 頂部搜尋與導覽列 -->
        <header class="bg-slate-800/90 backdrop-blur border-b border-slate-700 sticky top-0 z-30 px-6 py-4">
            <div class="max-w-6xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4">
                <div class="flex items-center gap-3 w-full sm:w-auto">
                    <div class="lg:hidden bg-emerald-600 text-white p-2 rounded-lg">
                        <i class="fa-solid fa-cubes"></i>
                    </div>
                    <div>
                        <h1 class="text-lg font-bold text-white">Minecraft 核心模組與結構互動百科</h1>
                        <p class="text-xs text-slate-400">整合模組核心機制、自然生成座標、相容性與附屬模組指南</p>
                    </div>
                </div>

                <!-- 即時搜尋框 -->
                <div class="w-full sm:w-80 relative">
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3.5 text-slate-400">
                        <i class="fa-solid fa-search text-sm"></i>
                    </span>
                    <input type="text" id="searchInput" placeholder="搜尋模組名稱、機械動力、座標或標籤..." 
                        class="w-full pl-10 pr-4 py-2 bg-slate-900 border border-slate-700 rounded-xl text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:border-emerald-500 transition">
                </div>
            </div>
        </header>

        <!-- 主內容容器 -->
        <main class="max-w-6xl mx-auto px-6 py-8 w-full flex-1">
            
            <!-- 手機版/快速過濾標籤列 -->
            <div class="flex flex-wrap gap-2 mb-6" id="topFilterButtons">
                <button data-filter="all" class="top-filter-btn px-3.5 py-1.5 rounded-lg text-xs font-medium bg-emerald-600 text-white shadow transition cursor-pointer">全部模組</button>
                <button data-filter="tech" class="top-filter-btn px-3.5 py-1.5 rounded-lg text-xs font-medium bg-slate-800 text-slate-300 hover:bg-slate-700 border border-slate-700 transition cursor-pointer">⚙️ 科技工業</button>
                <button data-filter="adventure" class="top-filter-btn px-3.5 py-1.5 rounded-lg text-xs font-medium bg-slate-800 text-slate-300 hover:bg-slate-700 border border-slate-700 transition cursor-pointer">💀 冒險與頭目</button>
                <button data-filter="worldgen" class="top-filter-btn px-3.5 py-1.5 rounded-lg text-xs font-medium bg-slate-800 text-slate-300 hover:bg-slate-700 border border-slate-700 transition cursor-pointer">🏔️ 地形擴充</button>
                <button data-filter="performance" class="top-filter-btn px-3.5 py-1.5 rounded-lg text-xs font-medium bg-slate-800 text-slate-300 hover:bg-slate-700 border border-slate-700 transition cursor-pointer">🚀 效能與遠景</button>
            </div>

            <!-- 模組卡片網格 -->
            <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6" id="cardGrid">
                <!-- 由 JavaScript 根據 AGENTS.md 標準格式動態渲染 -->
            </div>

            <!-- 查無結果提示 -->
            <div id="noResult" class="hidden text-center py-20 bg-slate-800/40 rounded-2xl border border-slate-800">
                <i class="fa-solid fa-box-open text-4xl text-slate-500 mb-3"></i>
                <p class="text-slate-300 font-medium">找不到符合條件的模組或結構資料</p>
                <p class="text-xs text-slate-500 mt-1">請嘗試搜尋「Create」、「Cataclysm」、「Sodium」或切換分類標籤</p>
            </div>
        </main>

        <!-- 頁尾 -->
        <footer class="text-center py-6 text-xs text-slate-500 border-t border-slate-800/80 mt-12">
            Minecraft Mod Wiki & Interactive Guide &copy; 2026 | 遵循 <span class="text-emerald-400">AGENTS.md</span> 模組化規範建置
        </footer>
    </div>

    <!-- 3. 詳情互動 Modal 視窗 (展示完整百科資料) -->
    <div id="detailModal" class="fixed inset-0 bg-black/75 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl max-w-2xl w-full p-6 sm:p-8 relative shadow-2xl max-h-[90vh] overflow-y-auto">
            <button id="closeModal" class="absolute top-5 right-5 w-8 h-8 rounded-lg bg-slate-700/80 text-slate-300 hover:bg-rose-600 hover:text-white flex items-center justify-center transition cursor-pointer">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <div id="modalContent">
                <!-- 動態注入完整 MCMOD 百科資訊 -->
            </div>
        </div>
    </div>

    <!-- 4. JavaScript 核心資料與渲染邏輯 (AGENTS.md 標準資料結構) -->
    <script>
        /**
         * 【AGENTS.md 擴充規範】：
         * 若 AI 需新增模組介紹，請於 modsData 陣列中依下列標準欄位新增物件：
         * id, name, enName, category ('tech'|'adventure'|'worldgen'|'performance'), categoryName,
         * badgeColor, versions, loaders, summary, mechanics (陣列), worldGenInfo, addons, compatibilityNotes
         */
        const modsData = [
            {
                id: 1,
                name: "機械動力",
                enName: "Create",
                category: "tech",
                categoryName: "科技與工業",
                badgeColor: "bg-amber-500/20 text-amber-300 border-amber-500/30",
                versions: "1.20.1 / 1.21.1",
                loaders: "NeoForge / Forge / Fabric",
                summary: "以旋轉力學與齒輪傳動為核心的沉浸式工業模組，提供極具視覺美感的自動化產線、火車系統與動態結構。",
                mechanics: [
                    "應力系統 (Stress Units, SU)：透過水車、風車或蒸汽引擎產生旋轉動力，並利用齒輪比調整轉速。",
                    "流體與加工：結合機械手、壓印機、攪拌盆與烈焰人燃燒室，實現礦石洗滌倍增與自動化合成。",
                    "動態結構與列車：使用強力膠將方塊組合成可移動的鑽頭礦車、電梯或跨維度鐵道火車。"
                ],
                worldGenInfo: "地表與地下生成鋅礦 (Zinc Ore, Y: -60 ~ 70) 及斑銅礦、赭金砂等裝飾岩層，用於合成安山合金與黃銅機殼。",
                addons: "Create Big Cannons (巨型火炮)、Create Aeronautics (飛空艇物理)、Steam 'n' Rails (鐵道擴充)",
                compatibilityNotes: "搭配 Sodium / Embeddium 時，建議確認 Flywheel 渲染後端版本相容性，避免大型齒輪陣列造成 FPS 驟降。"
            },
            {
                id: 2,
                name: "機械動力：巨型火炮",
                enName: "Create Big Cannons",
                category: "tech",
                categoryName: "科技與工業",
                badgeColor: "bg-amber-500/20 text-amber-300 border-amber-500/30",
                versions: "1.20.1 / 1.21.1",
                loaders: "NeoForge / Forge / Fabric",
                summary: "機械動力的重武裝附屬模組，允許玩家透過鑄造、鑽孔工藝組裝多方塊大口徑火炮與防空機炮 (Autocannon)。",
                mechanics: [
                    "多方塊火炮組裝：支援青銅、鑄鐵、鍛鋼與獄髓材質炮管，口徑與炮管長度直接影響射程與精準度。",
                    "機炮與散熱系統：速射機炮 (Autocannon) 具備炮管前方散熱器結構，可由機械動力轉速驅動進行高射速防空或平射。",
                    "真實彈道與引信：提供榴彈、穿甲彈、霰彈與定時/近炸引信，具備真實方塊穿透與爆炸物理。"
                ],
                worldGenInfo: "無獨立群系，但極度依賴主世界與地獄的鐵、銅、石英與獄髓資源來建立大型鑄造廠。",
                addons: "前置必備：Create (機械動力)、Ritchie's Projectile Library (RPL 彈道庫)",
                compatibilityNotes: "高速發射大量實體砲彈時會增加伺服器端 (TPS) 運算負擔，多人伺服器建議限制單一區域機炮陣列數量。"
            },
            {
                id: 3,
                name: "災變",
                enName: "L_Ender's Cataclysm",
                category: "adventure",
                categoryName: "冒險與頭目",
                badgeColor: "bg-rose-500/20 text-rose-300 border-rose-500/30",
                versions: "1.20.1 / 1.21.1",
                loaders: "NeoForge / Forge",
                summary: "專注於史詩級地下城與高難度頭目戰的冒險模組，每個頭目皆擁有獨立主題地牢、多階段變身與專屬傳奇武裝。",
                mechanics: [
                    "燃魂熔爐祭壇 (Ignis Altar)：位於地獄岩漿海周邊 (Y: 10~40)，擊敗烈焰魔君 Ignis 可鍛造無耐久消耗的強大炎魔武裝。",
                    "深淵地牢 (Sunken City)：位於深海底部 (Y: -45~-10)，由利維坦 (The Leviathan) 鎮守，具備次元裂隙與觸手攻擊機制。",
                    "遠古工廠與末地遺跡：包含機械守衛 (Harbinger) 與末影守衛，提供高難度動作閃避體驗。"
                ],
                worldGenInfo: "在主世界深海、沙漠金字塔底層、雪原、地獄荒地與終界外島皆會生成大型結構地牢（不可被活塞推動之防破壞方塊）。",
                addons: "前置必備：Lionfish API / Citadel；推薦搭配：Sophisticated Backpacks (精妙背包)",
                compatibilityNotes: "大型結構生成時若搭配 Tectonic 等極端地形模組，部分地牢邊緣可能出現地形高差，建議搭配結構平滑模組。"
            },
            {
                id: 4,
                name: "地殼構造：史詩地形",
                enName: "Tectonic",
                category: "worldgen",
                categoryName: "世界與地形生成",
                badgeColor: "bg-cyan-500/20 text-cyan-300 border-cyan-500/30",
                versions: "1.20.1 / 1.21.1",
                loaders: "NeoForge / Forge / Fabric",
                summary: "徹底重塑原版地形生成演算法，帶來突破 Y: 320 的宏偉阿爾卑斯山脈、深邃峽谷裂谷、地下長河與波浪起伏的真實海洋。",
                mechanics: [
                    "巨型沉降山脈 (Alpine Peaks)：將山脈高度上限推升至 Y: 300 以上，呈現真實的雪線與裸岩斷層。",
                    "深層大峽谷與地下河：在惡地與乾燥高原形成 Y: -20 ~ 50 的壯麗裂谷，內部可直接划船穿越大規模地下河系。",
                    "原版方塊完全相容：不新增任何自訂方塊，100% 使用原版方塊完成史詩級地貌改造。"
                ],
                worldGenInfo: "全面覆蓋主世界地形高度圖 (Heightmap)，山麓與高原過渡更加平緩，非常適合建造大型機械動力工廠或鐵道橋樑。",
                addons: "完美相容：Terralith (領域)、Distant Horizons (遙遠的地平線) / Voxy",
                compatibilityNotes: "因為山脈高度極高，建議搭配遠景渲染模組才能完整體驗壯麗山景；村莊生成於陡坡時偶爾會有高低落差。"
            },
            {
                id: 5,
                name: "鈉 / 嵌鈉 (渲染優化)",
                enName: "Sodium / Embeddium",
                category: "performance",
                categoryName: "渲染與效能優化",
                badgeColor: "bg-emerald-500/20 text-emerald-300 border-emerald-500/30",
                versions: "1.20.1 / 1.21.1",
                loaders: "NeoForge / Fabric",
                summary: "取代原版老舊 OpenGL 渲染管線的現代化優化核心，能提升 200%～400% 以上的遊戲幀率 (FPS) 並大幅消除區塊載入卡頓。",
                mechanics: [
                    "多執行緒區塊網格編譯：徹底解決移動時載入新地形造成的瞬間掉幀 (Micro-stuttering)。",
                    "記憶體與頂點壓縮：減少約 30%~40% 的 VRAM 與系統記憶體佔用，讓大型整合包運行更穩定。",
                    "光影無縫整合：搭配 Iris Shaders 或 Oculus 即可在享受極高 FPS 的同時開啟高品質光影。"
                ],
                worldGenInfo: "純客戶端渲染模組（不安裝於伺服器端，不影響任何世界生成與存檔資料）。",
                addons: "搭配模組：Iris Shaders (光影)、Lithium (邏輯優化)、FerriteCore (記憶體壓縮)",
                compatibilityNotes: "筆電玩家請務必在 Windows 圖形設定中將 javaw.exe 強制指定為獨立顯卡（如 RTX 5070），避免誤用內顯導致優化失效。"
            },
            {
                id: 6,
                name: "遙遠的地平線 / Voxy",
                enName: "Distant Horizons / Voxy",
                category: "performance",
                categoryName: "渲染與效能優化",
                badgeColor: "bg-emerald-500/20 text-emerald-300 border-emerald-500/30",
                versions: "1.20.1 / 1.21.1",
                loaders: "NeoForge / Fabric",
                summary: "透過 LOD (細節層次) 與體素降採樣技術，在不消耗大量伺服器效能的前提下，實現 128～512 區塊以上的超遠視距渲染。",
                mechanics: [
                    "LOD 動態細節層次：遠處區塊以簡化幾何模型渲染，近處保持原版精細度，輕鬆看見數千格外的山脈與建築。",
                    "非同步背景生成：利用多核心 CPU (如 Ryzen 9 系列) 在背景預先繪製遠景地圖。",
                    "光影相容支援：新版已支援與 Iris Shaders 聯動，讓遠景也能呈現真實的大氣霧氣與日落光影。"
                ],
                worldGenInfo: "客戶端視覺擴充模組（若安裝於伺服器端，可主動向玩家同步未探索過的遠方 LOD 地形資料）。",
                addons: "最佳拍檔：Tectonic + Terralith（能將高山與峽谷的視覺震撼力發揮到極致）",
                compatibilityNotes: "初次進入世界生成 LOD 時 CPU 負載較高，建議將生成模式調為「Balanced」以兼顧風扇噪音與幀率穩定。"
            }
        ];

        const cardGrid = document.getElementById('cardGrid');
        const searchInput = document.getElementById('searchInput');
        const sidebarButtons = document.querySelectorAll('.sidebar-btn');
        const topFilterButtons = document.querySelectorAll('.top-filter-btn');
        const noResult = document.getElementById('noResult');
        const detailModal = document.getElementById('detailModal');
        const closeModal = document.getElementById('closeModal');
        const modalContent = document.getElementById('modalContent');

        let currentFilter = 'all';
        let currentSearch = '';

        // 渲染卡片函式
        function renderCards() {
            cardGrid.innerHTML = '';
            const q = currentSearch.toLowerCase();

            const filtered = modsData.filter(item => {
                const matchesCategory = currentFilter === 'all' || item.category === currentFilter;
                const matchesSearch = 
                    item.name.toLowerCase().includes(q) ||
                    item.enName.toLowerCase().includes(q) ||
                    item.summary.toLowerCase().includes(q) ||
                    item.worldGenInfo.toLowerCase().includes(q) ||
                    item.addons.toLowerCase().includes(q);
                return matchesCategory && matchesSearch;
            });

            if (filtered.length === 0) {
                noResult.classList.remove('hidden');
                return;
            } else {
                noResult.classList.add('hidden');
            }

            filtered.forEach(item => {
                const card = document.createElement('div');
                card.className = "bg-slate-800/90 border border-slate-700/80 rounded-2xl p-6 shadow-lg hover:border-emerald-500/60 hover:-translate-y-0.5 transition duration-200 flex flex-col justify-between group";
                card.innerHTML = `
                    <div>
                        <div class="flex justify-between items-center gap-2 mb-3">
                            <span class="text-xs px-2.5 py-1 rounded-full border ${item.badgeColor} font-medium">${item.categoryName}</span>
                            <span class="text-[11px] text-slate-400 bg-slate-900/90 px-2.5 py-1 rounded-md border border-slate-700 font-mono">${item.versions}</span>
                        </div>
                        <h3 class="text-lg font-bold text-white group-hover:text-emerald-400 transition">
                            ${item.name} <span class="text-sm font-normal text-slate-400">(${item.enName})</span>
                        </h3>
                        <p class="text-xs text-slate-300 mt-2.5 mb-4 leading-relaxed line-clamp-3">${item.summary}</p>
                        
                        <div class="space-y-2 text-xs text-slate-400 border-t border-slate-700/60 pt-3.5">
                            <p class="flex items-start gap-2">
                                <i class="fa-solid fa-microchip text-emerald-400 mt-0.5 w-3.5 text-center"></i>
                                <span><strong class="text-slate-200">載入器：</strong>${item.loaders}</span>
                            </p>
                            <p class="flex items-start gap-2">
                                <i class="fa-solid fa-puzzle-piece text-amber-400 mt-0.5 w-3.5 text-center"></i>
                                <span class="truncate"><strong class="text-slate-200">關聯/附屬：</strong>${item.addons}</span>
                            </p>
                        </div>
                    </div>
                    <button onclick="openModal(${item.id})" class="mt-5 w-full bg-slate-700/80 hover:bg-emerald-600 text-slate-200 hover:text-white py-2.5 rounded-xl text-xs font-medium transition flex items-center justify-center gap-2 cursor-pointer shadow-sm">
                        <span>查看完整 MCMOD 百科與機制</span>
                        <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                    </button>
                `;
                cardGrid.appendChild(card);
            });
        }

        // 開啟詳情 Modal
        window.openModal = function(id) {
            const item = modsData.find(d => d.id === id);
            if (!item) return;

            const mechanicsList = item.mechanics.map(m => `<li class="flex items-start gap-2"><i class="fa-solid fa-caret-right text-emerald-400 mt-1"></i><span>${m}</span></li>`).join('');

            modalContent.innerHTML = `
                <div class="flex flex-wrap items-center gap-2 mb-3">
                    <span class="text-xs px-3 py-1 rounded-full border ${item.badgeColor} font-medium">${item.categoryName}</span>
                    <span class="text-xs bg-slate-900 text-slate-300 px-2.5 py-1 rounded-md border border-slate-700 font-mono"><i class="fa-solid fa-code-branch mr-1 text-emerald-400"></i>${item.versions}</span>
                    <span class="text-xs bg-slate-900 text-slate-300 px-2.5 py-1 rounded-md border border-slate-700">${item.loaders}</span>
                </div>
                <h2 class="text-2xl font-bold text-white mb-1">${item.name} <span class="text-base font-normal text-slate-400">(${item.enName})</span></h2>
                <p class="text-sm text-slate-300 leading-relaxed mb-5">${item.summary}</p>

                <div class="space-y-4">
                    <!-- 核心機制 -->
                    <div class="bg-slate-900/70 p-4 rounded-xl border border-slate-700/70">
                        <h4 class="text-xs font-bold text-emerald-400 uppercase tracking-wider mb-2.5 flex items-center gap-1.5">
                            <i class="fa-solid fa-gears"></i> 核心機制與重點玩法
                        </h4>
                        <ul class="space-y-2 text-sm text-slate-200 leading-relaxed">
                            ${mechanicsList}
                        </ul>
                    </div>

                    <!-- 世界生成與座標資訊 -->
                    <div class="bg-slate-900/70 p-4 rounded-xl border border-slate-700/70">
                        <h4 class="text-xs font-bold text-cyan-400 uppercase tracking-wider mb-1.5 flex items-center gap-1.5">
                            <i class="fa-solid fa-compass"></i> 世界生成與探索位置指南
                        </h4>
                        <p class="text-sm text-slate-300 leading-relaxed">${item.worldGenInfo}</p>
                    </div>

                    <!-- 前置與推薦搭配 -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        <div class="bg-slate-900/50 p-3.5 rounded-xl border border-slate-700/50">
                            <h4 class="text-xs font-bold text-amber-400 mb-1"><i class="fa-solid fa-puzzle-piece mr-1"></i>前置與推薦附屬模組</h4>
                            <p class="text-xs text-slate-300 leading-relaxed">${item.addons}</p>
                        </div>
                        <div class="bg-slate-900/50 p-3.5 rounded-xl border border-slate-700/50">
                            <h4 class="text-xs font-bold text-rose-400 mb-1"><i class="fa-solid fa-triangle-exclamation mr-1"></i>相容性與調校建議</h4>
                            <p class="text-xs text-slate-300 leading-relaxed">${item.compatibilityNotes}</p>
                        </div>
                    </div>
                </div>
            `;
            detailModal.classList.remove('hidden');
        };

        // 同步切換分類按鈕樣式
        function setCategoryFilter(filterValue) {
            currentFilter = filterValue;
            
            // 更新左側導覽列
            sidebarButtons.forEach(btn => {
                if (btn.getAttribute('data-filter') === filterValue) {
                    btn.classList.remove('text-slate-300', 'hover:bg-slate-700/70');
                    btn.classList.add('bg-emerald-600', 'text-white');
                } else {
                    btn.classList.remove('bg-emerald-600', 'text-white');
                    btn.classList.add('text-slate-300', 'hover:bg-slate-700/70');
                }
            });

            // 更新頂部標籤列
            topFilterButtons.forEach(btn => {
                if (btn.getAttribute('data-filter') === filterValue) {
                    btn.classList.remove('bg-slate-800', 'text-slate-300');
                    btn.classList.add('bg-emerald-600', 'text-white');
                } else {
                    btn.classList.remove('bg-emerald-600', 'text-white');
                    btn.classList.add('bg-slate-800', 'text-slate-300');
                }
            });

            renderCards();
        }

        // 綁定事件
        sidebarButtons.forEach(btn => btn.addEventListener('click', () => setCategoryFilter(btn.getAttribute('data-filter'))));
        topFilterButtons.forEach(btn => btn.addEventListener('click', () => setCategoryFilter(btn.getAttribute('data-filter'))));
        searchInput.addEventListener('input', (e) => {
            currentSearch = e.target.value.trim();
            renderCards();
        });
        closeModal.addEventListener('click', () => detailModal.classList.add('hidden'));
        detailModal.addEventListener('click', (e) => {
            if (e.target === detailModal) detailModal.classList.add('hidden');
        });

        // 初始渲染
        renderCards();
    </script>
</body>
</html>
