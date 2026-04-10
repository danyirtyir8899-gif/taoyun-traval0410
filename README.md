<!DOCTYPE html>
<html lang="zh-TW" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>青銀共遊：桃園無礙永續時光漫旅</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&display=swap');
        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: #FAFAF9;
            color: #292524;
            overflow-x: hidden;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 350px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .timeline-container {
            position: relative;
            padding-left: 2rem;
        }
        @media (min-width: 640px) {
            .timeline-container {
                padding-left: 3rem;
            }
        }
        .timeline-line {
            width: 4px;
            background-color: #E7E5E4;
            position: absolute;
            top: 1rem;
            bottom: 0;
            left: 0.75rem;
            z-index: 0;
        }
        @media (min-width: 640px) {
            .timeline-line {
                left: 1.25rem;
            }
        }
        .timeline-dot {
            width: 2.5rem;
            height: 2.5rem;
            background-color: #0F766E;
            color: white;
            border-radius: 50%;
            position: absolute;
            left: -0.5rem;
            top: 0.5rem;
            z-index: 10;
            border: 4px solid #FAFAF9;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }
        @media (min-width: 640px) {
            .timeline-dot {
                left: 0rem;
            }
        }
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#0F766E',      
                        primaryLight: '#CCFBF1', 
                        secondary: '#D97706',    
                        secondaryLight: '#FEF3C7',
                        surface: '#FFFFFF',
                        background: '#FAFAF9',   
                        textMain: '#292524',     
                        textMuted: '#57534E',    
                        alert: '#BE123C',        
                        alertLight: '#FFE4E6'    
                    }
                }
            }
        }
    </script>
</head>
<body class="antialiased pb-20">

    <!-- Chosen Palette: Warm Neutrals with Vibrant Teal (#0F766E) and Amber (#D97706) Accents -->
    <!-- Application Structure Plan: The SPA is structured as an interactive strategic dashboard for tour planning. It logically flows from Empathy & Concept (the 'Why') -> Analytics (justifying pace/budget with data) -> Interactive Itinerary (the 'What' and 'How', using accordion UI to manage dense accessibility/transport data without clutter) -> Logistics (Summary of risks/budget). This ensures caregivers or senior travelers understand the rationale before executing the plan, prioritizing usability and cognitive ease. -->
    <!-- Visualization & Content Choices: 
         1. Empathy Time Comparison -> Goal: Compare -> Horizontal Bar Chart (Chart.js) -> Contrasts standard map times with accessible buffer times to visually justify the relaxed pace. Justification: Clear quantitative comparison. No SVG.
         2. Accessibility Risk Radar -> Goal: Evaluate -> Radar Chart (Chart.js) -> Provides a quick visual summary of how the itinerary handles key mobility risks. Justification: Holistic view of multi-variable safety. No SVG.
         3. Budget Distribution -> Goal: Inform -> Donut Chart (Chart.js) -> Displays cost breakdown. Justification: Simple proportion visualization. No SVG.
         4. Dynamic Itinerary -> Goal: Organize -> Interactive HTML Timeline (Vanilla JS) -> Manages dense text chronologically. Justification: Best for sequential data without complex SVG flowcharts. No SVG/Mermaid. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <nav class="bg-primary text-white shadow-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <div class="text-xl sm:text-2xl bg-white text-primary rounded-full w-10 h-10 flex items-center justify-center font-bold">憶</div>
                <div>
                    <h1 class="text-lg sm:text-xl font-bold tracking-wide">桃園時光慢旅</h1>
                    <p class="text-xs text-teal-100 opacity-90">國小同學會 ‧ 無礙永續一日遊規劃</p>
                </div>
            </div>
            <div class="flex gap-2 sm:gap-4 overflow-x-auto w-full sm:w-auto pb-1 sm:pb-0 no-scrollbar">
                <a href="#concept" class="whitespace-nowrap px-3 py-1.5 rounded-md text-sm font-medium hover:bg-teal-600 transition-colors">設計理念</a>
                <a href="#analytics" class="whitespace-nowrap px-3 py-1.5 rounded-md text-sm font-medium hover:bg-teal-600 transition-colors">數據分析</a>
                <a href="#itinerary" class="whitespace-nowrap px-3 py-1.5 rounded-md text-sm font-medium bg-secondary text-white hover:bg-amber-600 transition-colors shadow-sm">互動行程</a>
            </div>
        </div>
    </nav>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-12">

        <section id="concept" class="scroll-mt-24">
            <div class="mb-6">
                <h2 class="text-2xl sm:text-3xl font-bold text-primary mb-2 border-l-4 border-secondary pl-4">遊客同理心與設計理念</h2>
                <p class="text-textMuted text-base sm:text-lg leading-relaxed">
                    本區段闡述行程設計的核心價值觀。針對<strong class="text-primary">「退休、具行動不便需求（需輪椅或推車）、舉辦國小同學會」</strong>的特殊旅客輪廓，我們將行程定調為「從容、懷舊、無礙」。徹底摒棄緊湊的打卡模式，透過刻意留白的緩衝時間與100%大眾運輸，打造無壓力的跨世代對話空間。
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div class="bg-surface rounded-xl shadow-sm p-6 border border-slate-200 hover:shadow-md transition-shadow">
                    <div class="text-4xl mb-4 text-center">⏱️</div>
                    <h3 class="text-xl font-bold text-textMain mb-2 text-center">無障礙極寬容時間</h3>
                    <p class="text-textMuted text-sm leading-relaxed text-justify">
                        打破一般導航預估限制。將所有步行與轉乘時間增加 50%~100% 的緩衝，徹底消弭尋找電梯、推車避開顛簸路面、以及長者如廁的心理焦慮。
                    </p>
                </div>
                <div class="bg-surface rounded-xl shadow-sm p-6 border border-slate-200 hover:shadow-md transition-shadow">
                    <div class="text-4xl mb-4 text-center">🌱</div>
                    <h3 class="text-xl font-bold text-textMain mb-2 text-center">低碳永續移動網路</h3>
                    <p class="text-textMuted text-sm leading-relaxed text-justify">
                        以高鐵桃園站為樞紐，全線串聯桃園機場捷運與市區低底盤公車。在實踐永續旅遊、減少碳足跡的同時，確保輪椅使用者享有平穩安全的移動品質。
                    </p>
                </div>
                <div class="bg-surface rounded-xl shadow-sm p-6 border border-slate-200 hover:shadow-md transition-shadow">
                    <div class="text-4xl mb-4 text-center">📻</div>
                    <h3 class="text-xl font-bold text-textMain mb-2 text-center">跨世代共鳴記憶</h3>
                    <p class="text-textMuted text-sm leading-relaxed text-justify">
                        從現代靜謐的橫山書法藝術館，過渡到乘載半世紀記憶的黑松飲料博物館與老城區麵館，精心安排能激發「老同學」共同回憶的五感體驗。
                    </p>
                </div>
            </div>
        </section>

        <section id="analytics" class="scroll-mt-24 bg-surface rounded-xl shadow-sm p-6 lg:p-8 border border-slate-200">
            <div class="mb-8">
                <h2 class="text-2xl sm:text-3xl font-bold text-primary mb-2 border-l-4 border-secondary pl-4">時光與無礙風險分析</h2>
                <p class="text-textMuted text-base sm:text-lg leading-relaxed">
                    此區段透過數據視覺化，展現我們如何將「同理心」轉化為精確的行程參數。左圖對比了常規地圖導航預估與本行程的「包容性預估」時間；右圖則評估了整體行程在各大無障礙指標上的防護能力。
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 lg:gap-12">
                <div class="bg-background rounded-xl p-4 sm:p-6 border border-slate-200 flex flex-col">
                    <h3 class="text-lg font-bold text-textMain mb-1 text-center">同理心時間規劃對比 (分鐘)</h3>
                    <p class="text-sm text-textMuted text-center mb-4">一般地圖導航 vs 本行程包容性預估</p>
                    <div class="chart-container flex-grow">
                        <canvas id="timeComparisonChart"></canvas>
                    </div>
                    <div class="mt-4 text-sm text-textMuted bg-surface p-4 rounded-lg shadow-sm border border-slate-100">
                        <span class="font-bold text-primary">📊 分析洞察：</span> 在「高鐵至機捷轉乘」、「市區公車轉乘」等節點，我們刻意設計高倍率緩衝時間，確保長者能從容等待電梯與低底盤公車斜坡板作業，避免追趕班車的跌倒風險。
                    </div>
                </div>

                <div class="bg-background rounded-xl p-4 sm:p-6 border border-slate-200 flex flex-col">
                    <h3 class="text-lg font-bold text-textMain mb-1 text-center">行程風險防護雷達圖</h3>
                    <p class="text-sm text-textMuted text-center mb-4">五大無障礙與永續指標評估 (滿分5分)</p>
                    <div class="chart-container flex-grow">
                        <canvas id="riskRadarChart"></canvas>
                    </div>
                    <div class="mt-4 text-sm text-textMuted bg-surface p-4 rounded-lg shadow-sm border border-slate-100">
                        <span class="font-bold text-primary">🛡️ 防護總結：</span> 本行程在「地形平坦度」與「低碳交通無礙度」表現優異。針對中壢老城區可能的「人群擁擠度」與戶外的「天氣變化」，已於下方互動行程表中制定嚴格備案。
                    </div>
                </div>
            </div>
            
            <div class="mt-8 bg-background rounded-xl p-4 sm:p-6 border border-slate-200 grid grid-cols-1 md:grid-cols-2 gap-6 items-center">
                <div>
                    <h3 class="text-xl font-bold text-textMain mb-2">預算結構與成本分析</h3>
                    <p class="text-sm text-textMuted mb-4">預估單人費用 (包含長者優惠票價與彈性緊急預備金)。總花費極度親民，將預算保留於品質較高的餐飲或應急計程車資。</p>
                    <ul class="space-y-3 text-sm">
                        <li class="flex justify-between border-b border-slate-200 pb-2"><span class="text-textMuted font-medium">永續交通 (機捷+公車敬老票)</span> <span class="font-bold text-primary">約 $80</span></li>
                        <li class="flex justify-between border-b border-slate-200 pb-2"><span class="text-textMuted font-medium">懷舊餐飲 (老巷小館)</span> <span class="font-bold text-primary">約 $150</span></li>
                        <li class="flex justify-between border-b border-slate-200 pb-2"><span class="text-textMuted font-medium">門票費用 (長者優惠/免費)</span> <span class="font-bold text-primary">$0 - $50</span></li>
                        <li class="flex justify-between border-b border-slate-200 pb-2"><span class="text-textMuted font-medium">緊急備用金 (計程車資分攤)</span> <span class="font-bold text-alert">預備 $200</span></li>
                        <li class="flex justify-between text-lg text-secondary pt-2 font-bold"><span>單人總計預估</span> <span>約 $430 - $480</span></li>
                    </ul>
                </div>
                <div class="chart-container" style="max-height: 280px;">
                    <canvas id="budgetChart"></canvas>
                </div>
            </div>
        </section>

        <section id="itinerary" class="scroll-mt-24">
            <div class="mb-8">
                <h2 class="text-2xl sm:text-3xl font-bold text-primary mb-2 border-l-4 border-secondary pl-4">客製化互動時光軸</h2>
                <p class="text-textMuted text-base sm:text-lg leading-relaxed">
                    本區段為一日行程的操作核心。點擊各站點卡片，即可展開專為輪椅與推車族群調查的「動線指引」、「永續交通」以及極為重要的「風險備案」。請依據當日長者實際體力彈性應用。
                </p>
            </div>

            <div class="bg-surface rounded-xl shadow-sm p-4 sm:p-8 border border-slate-200">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-8 bg-slate-50 p-4 rounded-lg border border-slate-200 gap-4">
                    <div>
                        <span class="font-bold text-textMain text-lg flex items-center gap-2">🗺️ 最佳移動順序建議</span>
                        <span class="text-sm text-textMuted block mt-1">避免繞路折返。高鐵桃園站 ➔ 橫山書法藝術館 ➔ 中壢老城區 ➔ 黑松飲料博物館 ➔ 賦歸。</span>
                    </div>
                    <button id="expandAllBtn" class="w-full sm:w-auto px-4 py-2 bg-primaryLight text-primary text-sm font-bold rounded shadow hover:bg-teal-200 transition-colors">
                        展開所有細節
                    </button>
                </div>

                <div class="timeline-container" id="timeline-wrapper">
                    <div class="timeline-line"></div>
                </div>
            </div>
            
            <div class="mt-8 bg-alertLight border border-rose-200 rounded-xl p-6">
                 <h3 class="text-xl font-bold text-alert mb-3 flex items-center gap-2"><span>⚠️</span> 最終風險防護聲明</h3>
                 <p class="text-sm text-textMain leading-relaxed">
                     <strong>體力透支與突發不適對策：</strong> 行程中任一節點若長者表示疲勞，應立即取消後續景點。放棄等候公車，啟動預備金呼叫無障礙計程車直達高鐵站或最近醫療點（如中壢天晟醫院）。<br><br>
                     <strong>預約限制注意：</strong> 黑松飲料博物館嚴格規定需至少 5 個工作天前預約。出發前一週需再次致電確認輪椅通道是否暢通及廠區電梯維護狀況。
                 </p>
            </div>
        </section>

    </main>

    <footer class="bg-textMain text-surface py-8 border-t-4 border-primary mt-12">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <h4 class="font-bold mb-2">桃園青銀共遊專案小組</h4>
            <p class="text-sm text-stone-400 mb-2">本網頁資料擷取自：桃園公車動態系統、桃園捷運時刻表、景點官方網站與 Google Maps 旅客評論分析。</p>
            <p class="text-xs text-stone-500">© 2026 永續旅遊規劃展示用 SPA. Designed with Tailwind CSS & Chart.js.</p>
        </div>
    </footer>

    <script>
        const appState = {
            expandedItems: new Set()
        };

        const itineraryData = [
            {
                id: 'stop1',
                time: "10:00 - 10:30",
                title: "高鐵桃園站 集合出發",
                icon: "🚄",
                summary: "寬裕的集合時間，悠閒轉乘機場捷運，為旅程暖身。",
                transport: "步行約 5-10 分鐘。室內平坦無坡度。",
                details: "高鐵站內無障礙電梯指標清楚，請直接搭乘電梯至B1連通道前往機捷A18站。特別保留30分鐘，考量長者久未見面需要寒暄，且同行者尋找電梯與使用無障礙廁所較耗時。",
                risk: "無特殊風險。若遇假日人潮，請國小同學互相照應協助推車開道。",
                isRisk: false
            },
            {
                id: 'stop2',
                time: "10:30 - 12:00",
                title: "橫山書法藝術館",
                icon: "🏛️",
                summary: "當代清水模建築與平靜墨池，早晨避開擁擠人潮。",
                transport: "搭乘機捷從 A18(高鐵桃園站) 至 A17(領航站)，車程約3分鐘。出站沿大豐四街平坦人行道步行或推車約 10-15 分鐘。",
                details: "環境友善度極高。館內設有大型無障礙電梯，展區完全平坦。戶外橫山書法公園環湖步道為平整鋪面。停留1.5小時足以慢慢欣賞當代書法，並於湖畔合影。",
                risk: "若遇大雨，戶外推車移動不便。備案：直接進入館內，延長室內語音導覽時間，並於館內無障礙休息區透過落地窗欣賞雨景。",
                isRisk: true
            },
            {
                id: 'stop3',
                time: "12:00 - 13:00",
                title: "永續移動：前往老城區",
                icon: "🚌",
                summary: "體驗在地低碳運輸，感受城鄉風景變換。",
                transport: "從 A17 站搭機捷至 A21 環北站。出站後轉乘市區公車 (如170路) 至「中壢公車站」或「第一銀行」。",
                details: "此段路程距離較長，為實踐永續旅遊，捨棄計程車改搭大眾運輸。170路等多為低底盤公車。時間抓60分鐘，包容步行至站牌、等車以及上下車斜坡板作業的緩衝時間。",
                risk: "公車停靠可能未完全貼齊人行道。對策：請同學主動告知司機需放下輪椅斜坡板，並於上下車時協助留意後方機車動態。",
                isRisk: true
            },
            {
                id: 'stop4',
                time: "13:00 - 14:30",
                title: "午餐懷舊：老巷小館",
                icon: "🍜",
                summary: "品嚐傳承數十年的庶民飲食，滿足老同學的懷舊味蕾。",
                transport: "從公車站沿中壢老街廓步行約 5-8 分鐘前往。",
                details: "選擇此處為滿足「國小同學」聚會的懷舊需求。依據網路評論，老店空間較擠、周邊騎樓可能不平整。我們刻意安排於 13:00 非尖峰時段抵達。入座時請店家協助安排靠近門口或走道較寬的區域。",
                risk: "老城區騎樓高低落差大或無人行道。對策：放慢腳步，必要時由同學協助搬抬推車。終極備案：若現場極度不便，立即改搭計程車前往平鎮『食寓』用餐(致力食農教育與無障礙環境)。",
                isRisk: true
            },
            {
                id: 'stop5',
                time: "14:30 - 16:30",
                title: "黑松飲料博物館",
                icon: "🥤",
                summary: "廠區導覽，歷代汽水瓶與海報喚起跨世代共鳴。(需預約)",
                transport: "從中壢市區搭乘 1路公車 等路線至「中壢工業區」站，步行進入廠區大門。",
                details: "下午最適合安排室內行程避暑或避寒。博物館位於廠區內，冷氣開放、完全平坦無階梯、座椅充足，極度適合行動不便長者。欣賞歷代懷舊海報能引發熱烈討論。",
                risk: "工業區外圍大車多。對策：下車後務必緊靠廠區圍牆或人行道行走。進入廠區大門後即非常安全平穩。",
                isRisk: false
            },
            {
                id: 'stop6',
                time: "16:30 - 17:15",
                title: "賦歸：帶著回憶返程",
                icon: "🌅",
                summary: "避開下班尖峰，平安返回高鐵或台鐵車站。",
                transport: "公車返回中壢火車站，或搭乘計程車直達高鐵桃園站。",
                details: "強烈建議於 16:30 前結束行程離開工業區，以避開 17:00 後龐大的下班與放學車潮，減輕長者在擁擠車廂中的壓力。若預算允許且長者顯露疲態，建議直接搭乘計程車回高鐵。",
                risk: "傍晚尖峰塞車導致長者疲累。對策：嚴格控管結束時間，備用金隨時準備啟動計程車方案。",
                isRisk: false
            }
        ];

        function renderTimeline() {
            const container = document.getElementById('timeline-wrapper');
            let html = '<div class="timeline-line"></div>';

            itineraryData.forEach((item) => {
                const isExpanded = appState.expandedItems.has(item.id);
                const riskBadge = item.isRisk ? `<span class="bg-rose-100 text-alert text-xs px-2 py-0.5 rounded font-bold ml-2 whitespace-nowrap border border-rose-200">⚠️ 需留意</span>` : '';
                const contentDisplay = isExpanded ? 'block' : 'hidden';
                const chevronRotate = isExpanded ? 'rotate-180' : '';
                const borderActive = isExpanded ? 'border-primary ring-1 ring-primary/20' : 'border-slate-200';

                html += `
                    <div class="relative mb-6">
                        <div class="timeline-dot">${item.icon}</div>
                        <div class="bg-white rounded-xl shadow-sm border ${borderActive} p-4 sm:p-5 hover:shadow-md transition-all duration-200 ml-12 sm:ml-16">
                            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center cursor-pointer select-none" onclick="toggleTimelineItem('${item.id}')">
                                <div class="w-full pr-0 sm:pr-4">
                                    <div class="flex items-center flex-wrap gap-2 mb-1.5">
                                        <span class="text-xs sm:text-sm font-bold text-secondary bg-secondaryLight px-2 py-0.5 rounded">${item.time}</span>
                                        ${riskBadge}
                                    </div>
                                    <h3 class="text-lg sm:text-xl font-bold text-primary mt-1">
                                        ${item.title}
                                    </h3>
                                    <p class="text-textMain text-sm mt-1.5">${item.summary}</p>
                                </div>
                                <div class="mt-3 sm:mt-0 self-end sm:self-center flex-shrink-0 text-primary bg-primaryLight w-8 h-8 rounded-full flex items-center justify-center transition-transform duration-300 ${chevronRotate}">
                                    ▼
                                </div>
                            </div>
                            
                            <div id="detail-${item.id}" class="mt-4 pt-4 border-t border-slate-100 ${contentDisplay}">
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
                                        <h4 class="text-sm font-bold text-primary mb-2 flex items-center gap-1"><span>🚍</span> 永續交通與動線</h4>
                                        <p class="text-sm text-textMuted leading-relaxed">${item.transport}</p>
                                    </div>
                                    <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
                                        <h4 class="text-sm font-bold text-primary mb-2 flex items-center gap-1"><span>📋</span> 設計考量與細節</h4>
                                        <p class="text-sm text-textMuted leading-relaxed">${item.details}</p>
                                    </div>
                                </div>
                                <div class="mt-4 bg-alertLight border border-rose-200 p-4 rounded-lg">
                                    <h4 class="text-sm font-bold text-alert mb-2 flex items-center gap-1"><span>🛡️</span> 風險管理與備案</h4>
                                    <p class="text-sm text-alert opacity-90 leading-relaxed">${item.risk}</p>
                                </div>
                            </div>
                        </div>
                    </div>
                `;
            });

            container.innerHTML = html;
        }

        function toggleTimelineItem(id) {
            if (appState.expandedItems.has(id)) {
                appState.expandedItems.delete(id);
            } else {
                appState.expandedItems.add(id);
            }
            renderTimeline();
        }

        document.getElementById('expandAllBtn')?.addEventListener('click', () => {
            const btn = document.getElementById('expandAllBtn');
            if (appState.expandedItems.size === itineraryData.length) {
                appState.expandedItems.clear();
                btn.textContent = '展開所有細節';
            } else {
                itineraryData.forEach(item => appState.expandedItems.add(item.id));
                btn.textContent = '收起所有細節';
            }
            renderTimeline();
        });

        function wrapLabels(labels, maxChar = 16) {
            return labels.map(label => {
                if (label.length <= maxChar) return label;
                const words = label.split(''); 
                let lines = [];
                let currentLine = '';
                words.forEach(word => {
                    if ((currentLine + word).length > maxChar) {
                        lines.push(currentLine);
                        currentLine = word;
                    } else {
                        currentLine += word;
                    }
                });
                if (currentLine) lines.push(currentLine);
                return lines;
            });
        }

        const tooltipConfig = {
            callbacks: {
                title: function(tooltipItems) {
                    const item = tooltipItems[0];
                    let label = item.chart.data.labels[item.dataIndex];
                    if (Array.isArray(label)) {
                        return label.join(''); 
                    } else {
                        return label;
                    }
                }
            }
        };

        function initCharts() {
            Chart.defaults.font.family = "'Noto Sans TC', sans-serif";
            Chart.defaults.color = '#57534E';

            const ctxTime = document.getElementById('timeComparisonChart').getContext('2d');
            const timeLabels = wrapLabels(['高鐵轉機捷(等電梯)', '機捷至書法館(推車)', '書法館至老城區(轉乘)', '老城區至黑松廠區'], 16);
            new Chart(ctxTime, {
                type: 'bar',
                data: {
                    labels: timeLabels,
                    datasets: [
                        {
                            label: '一般地圖預估 (分鐘)',
                            data: [10, 10, 35, 20],
                            backgroundColor: '#E7E5E4', 
                            borderRadius: 4
                        },
                        {
                            label: '包容性緩衝預估 (分鐘)',
                            data: [30, 20, 60, 35],
                            backgroundColor: '#0F766E', 
                            borderRadius: 4
                        }
                    ]
                },
                options: {
                    indexAxis: 'y', 
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { position: 'bottom' },
                        tooltip: tooltipConfig
                    },
                    scales: {
                        x: { beginAtZero: true, grid: { color: '#F5F5F4' } },
                        y: { grid: { display: false } }
                    }
                }
            });

            const ctxRadar = document.getElementById('riskRadarChart').getContext('2d');
            const radarLabels = wrapLabels(['地形平坦度(輪椅友善)', '醫療與休息支援度', '人群擁擠避開率', '低碳交通無礙度', '天氣變化防護力'], 16);
            new Chart(ctxRadar, {
                type: 'radar',
                data: {
                    labels: radarLabels,
                    datasets: [{
                        label: '本行程指標防護力',
                        data: [4.5, 4.5, 3.5, 4.8, 3.8],
                        backgroundColor: 'rgba(217, 119, 6, 0.2)', 
                        borderColor: '#D97706',
                        pointBackgroundColor: '#D97706',
                        pointBorderColor: '#fff',
                        pointHoverBackgroundColor: '#fff',
                        pointHoverBorderColor: '#D97706',
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        r: {
                            angleLines: { color: '#E7E5E4' },
                            grid: { color: '#E7E5E4' },
                            pointLabels: { font: { size: 11 }, color: '#292524' },
                            ticks: { display: false, min: 0, max: 5 }
                        }
                    },
                    plugins: {
                        legend: { display: false },
                        tooltip: tooltipConfig
                    }
                }
            });

            const ctxBudget = document.getElementById('budgetChart').getContext('2d');
            const budgetLabels = wrapLabels(['永續大眾交通(敬老票)', '老巷小館餐飲', '預備金(計程車等)'], 16);
            new Chart(ctxBudget, {
                type: 'doughnut',
                data: {
                    labels: budgetLabels,
                    datasets: [{
                        data: [80, 150, 200],
                        backgroundColor: ['#0F766E', '#D97706', '#E7E5E4'],
                        borderWidth: 2,
                        borderColor: '#FAFAF9'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '70%',
                    plugins: {
                        legend: { position: 'bottom', labels: { padding: 20, usePointStyle: true } },
                        tooltip: tooltipConfig
                    }
                }
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            renderTimeline();
            initCharts();
        });
    </script>
</body>
</html>
