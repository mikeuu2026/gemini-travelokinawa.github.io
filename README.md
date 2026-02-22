<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>沖繩 6 天 5 夜精準自駕行程表</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <style>
        /* Custom scrollbar for cleaner look */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8; 
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            height: 300px;
            margin: 0 auto;
        }
        .timeline-line {
            position: absolute;
            left: 24px;
            top: 0;
            bottom: 0;
            width: 2px;
            background-color: #e2e8f0;
            z-index: 0;
        }
        .active-tab {
            border-bottom: 2px solid #0ea5e9;
            color: #0ea5e9;
            font-weight: 600;
        }
        .inactive-tab {
            color: #64748b;
        }
        .card-hover:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
    </style>
    <!-- Chosen Palette: Ocean Breeze (Teal/Blue/Sand/Coral) -->
    <!-- Application Structure Plan: 
         1. Hero Section: Trip Overview, Dates, Flight Status.
         2. Dashboard: "Trip Balance" Chart (Activity types), Car Rental Progress Bar.
         3. Main Content: Tabbed Daily Itinerary with filtering (Food, Sightseeing, Transport).
         4. Sidebar/Bottom: "Must-Know" Reservations & Tips card.
         Rationale: Users need to quickly check "What's next?" and see specific details like reservation numbers. Tabs allow focused daily views without scrolling fatigue.
    -->
    <!-- Visualization & Content Choices:
         - Trip Balance Chart (Doughnut): Shows the distribution of activities (Nature vs. Shopping vs. Food) to visualize the "Quality Life" aspect.
         - Rental Car Timeline (Progress Bar): Visualizes the specific window of car rental to emphasize the "Precision" budget saving.
         - Interactive Itinerary: Filterable list to quickly find "Where to eat" or "Where to go".
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
</head>
<body class="bg-slate-50 text-slate-800 font-sans antialiased selection:bg-teal-200 selection:text-teal-900">

    <!-- Navigation / Header -->
    <header class="bg-white shadow-sm sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-2">
                <span class="text-2xl">🌴</span>
                <h1 class="text-xl font-bold text-slate-800 tracking-tight">沖繩精準自駕之旅</h1>
            </div>
            <div class="text-sm font-medium text-slate-500 hidden sm:block">
                2026/03/28 - 04/02
            </div>
            <button id="toggle-info" class="p-2 rounded-full bg-slate-100 hover:bg-slate-200 text-slate-600 transition-colors sm:hidden">
                ℹ️
            </button>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- Intro Section -->
        <section class="mb-10 text-center max-w-3xl mx-auto">
            <h2 class="text-3xl font-bold text-slate-900 mb-4">您的專屬旅程儀表板</h2>
            <p class="text-lg text-slate-600 leading-relaxed">
                歡迎使用您的互動行程表。本應用程式整合了航班、住宿、租車與預約資訊。
                行程設計核心為「高CP值」與「聰明消費」，將租車效益最大化，並集中火力於主題樂園與免稅購物。
            </p>
        </section>

        <!-- Key Stats & Visualizations Grid -->
        <section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-12">
            
            <!-- Flight Card -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100 card-hover transition-all duration-300">
                <h3 class="text-sm font-semibold text-slate-400 uppercase tracking-wider mb-4">✈️ 航班資訊</h3>
                <div class="space-y-4">
                    <div class="flex justify-between items-center">
                        <div class="text-left">
                            <div class="text-2xl font-bold text-slate-800">TPE</div>
                            <div class="text-xs text-slate-500">14:45</div>
                        </div>
                        <div class="flex-1 px-4 text-center">
                            <div class="text-xs text-slate-400">VZ568 (3/28)</div>
                            <div class="h-0.5 bg-slate-200 w-full my-1 relative">
                                <div class="absolute -top-1 right-0 text-slate-300">✈</div>
                            </div>
                            <div class="text-xs text-slate-400">1h 20m</div>
                        </div>
                        <div class="text-right">
                            <div class="text-2xl font-bold text-slate-800">OKA</div>
                            <div class="text-xs text-slate-500">17:05</div>
                        </div>
                    </div>
                    <div class="border-t border-slate-100 pt-3 flex justify-between items-center">
                        <div class="text-left">
                            <div class="text-2xl font-bold text-slate-800">OKA</div>
                            <div class="text-xs text-slate-500">13:15</div>
                        </div>
                        <div class="flex-1 px-4 text-center">
                            <div class="text-xs text-slate-400">MM927 (4/02)</div>
                            <div class="h-0.5 bg-slate-200 w-full my-1 relative">
                                <div class="absolute -top-1 left-0 text-slate-300 scale-x-[-1]">✈</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="text-2xl font-bold text-slate-800">TPE</div>
                            <div class="text-xs text-slate-500">13:50</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Car Rental Widget -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100 card-hover transition-all duration-300">
                <div class="flex justify-between items-start mb-2">
                    <h3 class="text-sm font-semibold text-slate-400 uppercase tracking-wider">🚗 精準租車</h3>
                    <span class="px-2 py-1 bg-green-100 text-green-700 text-xs font-bold rounded">省錢重點</span>
                </div>
                <p class="text-sm text-slate-600 mb-4">僅租 55 小時，省下頭尾兩日停車費與租金。</p>
                
                <div class="relative pt-6 pb-2">
                    <div class="flex justify-between text-xs font-bold text-slate-700 mb-1">
                        <span>3/29 10:00</span>
                        <span>3/31 17:00</span>
                    </div>
                    <div class="h-4 bg-slate-100 rounded-full overflow-hidden">
                        <div class="h-full bg-teal-500 w-full shadow-inner"></div>
                    </div>
                    <div class="flex justify-between text-xs text-slate-400 mt-1">
                        <span>取車 (歌町)</span>
                        <span>還車 (歌町)</span>
                    </div>
                </div>
                <div class="mt-4 p-3 bg-amber-50 rounded border border-amber-100">
                    <p class="text-xs text-amber-800">
                        ⚠️ <strong>Day 4 提醒：</strong> 請設鬧鐘於 16:15 離開 PARCO CITY，以免超過 17:00 還車時間產生罰金。
                    </p>
                </div>
            </div>

            <!-- Trip Balance Chart -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100 card-hover transition-all duration-300 flex flex-col items-center">
                <h3 class="text-sm font-semibold text-slate-400 uppercase tracking-wider w-full text-left mb-2">📊 行程比重分析</h3>
                <div class="chart-container">
                    <canvas id="tripChart"></canvas>
                </div>
                <p class="text-xs text-center text-slate-400 mt-2">平衡展現：美食、購物、自然與樂園</p>
            </div>
        </section>

        <!-- Main Interaction Area: Itinerary -->
        <section class="bg-white rounded-2xl shadow-lg border border-slate-100 overflow-hidden">
            
            <!-- Day Tabs -->
            <div class="flex overflow-x-auto border-b border-slate-200" id="dayTabs">
                <!-- JavaScript will populate this -->
            </div>

            <!-- Toolbar -->
            <div class="p-4 bg-slate-50 border-b border-slate-200 flex flex-wrap gap-3 items-center justify-between">
                <div class="text-sm font-medium text-slate-600" id="currentDateDisplay">
                    <!-- Date will go here -->
                </div>
                <div class="flex gap-2">
                    <button class="filter-btn px-3 py-1.5 rounded-full text-xs font-medium border border-slate-300 bg-white hover:bg-slate-50 transition-colors active-filter" data-filter="all">
                        全部
                    </button>
                    <button class="filter-btn px-3 py-1.5 rounded-full text-xs font-medium border border-slate-300 bg-white hover:bg-slate-50 transition-colors" data-filter="food">
                        🍽️ 美食
                    </button>
                    <button class="filter-btn px-3 py-1.5 rounded-full text-xs font-medium border border-slate-300 bg-white hover:bg-slate-50 transition-colors" data-filter="shop">
                        🛍️ 購物
                    </button>
                    <button class="filter-btn px-3 py-1.5 rounded-full text-xs font-medium border border-slate-300 bg-white hover:bg-slate-50 transition-colors" data-filter="spot">
                        🎡 景點
                    </button>
                </div>
            </div>

            <!-- Content Area -->
            <div class="p-6 min-h-[500px] relative">
                <div id="itineraryContent" class="space-y-8 relative pl-6">
                    <!-- Timeline Line -->
                    <div class="timeline-line"></div>
                    <!-- JavaScript will populate items here -->
                </div>
            </div>
        </section>

        <!-- Important Reservation Section -->
        <section class="mt-12">
            <h2 class="text-2xl font-bold text-slate-800 mb-6">📌 重點預約與住宿</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                
                <!-- Dinner Reservation -->
                <div class="bg-gradient-to-r from-slate-800 to-slate-900 rounded-xl p-6 text-white shadow-xl relative overflow-hidden group cursor-pointer hover:scale-[1.01] transition-transform">
                    <div class="absolute top-0 right-0 p-4 opacity-10 text-6xl">🥩</div>
                    <div class="relative z-10">
                        <div class="flex items-center gap-2 mb-2">
                            <span class="bg-red-500 text-white text-xs font-bold px-2 py-0.5 rounded">MUST EAT</span>
                            <span class="text-sm text-slate-300">Day 3 (3/30) 晚餐</span>
                        </div>
                        <h3 class="text-2xl font-bold mb-1">焼肉こうちゃん (Yakiniku Ko-chan)</h3>
                        <p class="text-slate-300 text-sm mb-4">七輪炭火燒肉 | 黑毛和牛 & 阿古豬</p>
                        
                        <div class="bg-white/10 rounded-lg p-4 backdrop-blur-sm border border-white/10">
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <div class="text-xs text-slate-400">預約號碼</div>
                                    <div class="font-mono text-lg font-bold text-yellow-400">DYDYZCU8ZQ</div>
                                </div>
                                <div>
                                    <div class="text-xs text-slate-400">預約大名</div>
                                    <div class="font-bold">YU WENCHUNG</div>
                                </div>
                                <div>
                                    <div class="text-xs text-slate-400">時間</div>
                                    <div class="font-bold">18:30</div>
                                </div>
                                <div>
                                    <div class="text-xs text-slate-400">內容</div>
                                    <div class="font-bold">雙人套餐</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Hotel Info -->
                <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-100">
                    <h3 class="font-bold text-slate-800 mb-4 flex items-center gap-2">
                        🏨 住宿安排
                    </h3>
                    <div class="space-y-4">
                        <div class="flex items-start gap-3 pb-3 border-b border-slate-100">
                            <div class="bg-blue-100 text-blue-600 w-10 h-10 rounded-full flex items-center justify-center font-bold text-sm shrink-0">1,4,5</div>
                            <div>
                                <div class="font-bold text-slate-800">那霸歌町阿爾蒙特飯店</div>
                                <div class="text-sm text-slate-500">Almont Hotel Naha Omoromachi</div>
                                <div class="text-xs text-slate-400 mt-1">Day 1, 4, 5 (共3晚) | 離DFS與車站近</div>
                            </div>
                        </div>
                        <div class="flex items-start gap-3">
                            <div class="bg-teal-100 text-teal-600 w-10 h-10 rounded-full flex items-center justify-center font-bold text-sm shrink-0">2,3</div>
                            <div>
                                <div class="font-bold text-slate-800">沖繩名護超級飯店</div>
                                <div class="text-sm text-slate-500">Super Hotel Okinawa Nago</div>
                                <div class="text-xs text-slate-400 mt-1">Day 2, 3 (共2晚) | 北部動線核心</div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </section>

    </main>

    <footer class="bg-slate-800 text-slate-400 py-8 mt-12">
        <div class="max-w-7xl mx-auto px-4 text-center">
            <p class="text-sm">2026 沖繩財富自由之旅 | 精準消費，質感生活</p>
        </div>
    </footer>

    <script>
        // --- Data Structure ---
        const itineraryData = [
            {
                day: 1,
                date: "3/28 (六)",
                title: "抵達那霸，輕鬆安頓",
                location: "那霸",
                stay: "那霸歌町阿爾蒙特飯店",
                activities: [
                    { time: "14:45", title: "起飛", type: "transport", desc: "VZ568 桃園 TPE -> 那霸 OKA", icon: "✈️" },
                    { time: "17:05", title: "抵達沖繩", type: "transport", desc: "入境、領行李、搭單軌電車至歌町站", icon: "🛬" },
                    { time: "19:00", title: "飯店 Check-in", type: "stay", desc: "那霸歌町阿爾蒙特飯店", icon: "🏨" },
                    { time: "19:30", title: "晚餐與採買", type: "food", desc: "San-A 那霸 Main Place 超市採買飲料零食 (高CP值)", icon: "🍱" }
                ]
            },
            {
                day: 2,
                date: "3/29 (日)",
                title: "取車出發！美式風情與生態",
                location: "中部 -> 名護",
                stay: "沖繩名護超級飯店",
                activities: [
                    { time: "10:00", title: "🌟 取車出發", type: "transport", desc: "歌町營業所取車 (租車開始)", icon: "🚗", highlight: true },
                    { time: "11:00", title: "美國村", type: "spot", desc: "感受美式加州氛圍，拍照打卡", icon: "🎡" },
                    { time: "12:30", title: "午餐", type: "food", desc: "塔可飯 (Taco Rice) 或美式漢堡", icon: "🍔" },
                    { time: "14:30", title: "Neo Park 名護自然動植物公園", type: "spot", desc: "近距離與禽鳥動物互動", icon: "🦚" },
                    { time: "17:00", title: "飯店 Check-in", type: "stay", desc: "沖繩名護超級飯店 (連住兩晚)", icon: "🏨" },
                    { time: "18:00", title: "晚餐", type: "food", desc: "名護市區居酒屋或暖暮拉麵", icon: "🍜" }
                ]
            },
            {
                day: 3,
                date: "3/30 (一)",
                title: "樂園大串連 & 頂級和牛",
                location: "名護周邊",
                stay: "沖繩名護超級飯店",
                activities: [
                    { time: "09:30", title: "名護鳳梨園", type: "spot", desc: "搭乘鳳梨遊園車，試吃鳳梨點心", icon: "🍍" },
                    { time: "11:30", title: "OKINAWA 水果樂園", type: "spot", desc: "熱帶水果體驗與解謎遊戲", icon: "🥭" },
                    { time: "13:00", title: "午餐", type: "food", desc: "大家 (Ufuya) 或沖繩麵", icon: "🍜" },
                    { time: "15:00", title: "DINO 恐龍 PARK", type: "spot", desc: "亞熱帶之森尋找恐龍，買紅芋塔", icon: "🦖" },
                    { time: "18:30", title: "🌟 晚餐：焼肉こうちゃん", type: "food", desc: "預約號：DYDYZCU8ZQ (YU WENCHUNG)，黑毛和牛雙人套餐", icon: "🥩", highlight: true }
                ]
            },
            {
                day: 4,
                date: "3/31 (二)",
                title: "鐘乳石洞、植物樂園與爆買",
                location: "名護 -> 浦添 -> 那霸",
                stay: "那霸歌町阿爾蒙特飯店",
                activities: [
                    { time: "09:00", title: "退房南下", type: "transport", desc: "往東海岸前進", icon: "🚗" },
                    { time: "10:00", title: "金武觀音寺 & 日秀洞", type: "spot", desc: "神秘鐘乳石洞穴參訪", icon: "⛩️" },
                    { time: "11:30", title: "東南植物樂園", type: "spot", desc: "亞歷山大椰子林與水豚互動", icon: "🌴" },
                    { time: "14:00", title: "PARCO CITY", type: "shop", desc: "理財達人購物時間！集中火力買免稅品", icon: "🛍️", highlight: true },
                    { time: "16:15", title: "離開商場", type: "transport", desc: "⚠️ 務必出發還車，避免超時", icon: "⏰" },
                    { time: "17:00", title: "還車", type: "transport", desc: "抵達歌町營業所還車", icon: "🏁" },
                    { time: "18:30", title: "晚餐", type: "food", desc: "國際通商圈散步覓食", icon: "🍲" }
                ]
            },
            {
                day: 5,
                date: "4/01 (三)",
                title: "那霸深度遊與質感生活",
                location: "那霸市區",
                stay: "那霸歌町阿爾蒙特飯店",
                activities: [
                    { time: "10:00", title: "首里城公園", type: "spot", desc: "單軌電車至首里站，感受琉球歷史", icon: "🏯" },
                    { time: "12:30", title: "牧志公設市場", type: "food", desc: "高CP值海鮮，一樓買料二樓煮", icon: "🐟" },
                    { time: "14:30", title: "壺屋通", type: "shop", desc: "陶瓷街散步，挑選質感選物", icon: "🏺" },
                    { time: "16:00", title: "DFS 免稅店", type: "shop", desc: "憑明日機票購買精品，喝咖啡覆盤投資", icon: "💳" },
                    { time: "18:30", title: "最後晚餐", type: "food", desc: "新都心質感居酒屋", icon: "🍻" }
                ]
            },
            {
                day: 6,
                date: "4/02 (四)",
                title: "滿載而歸",
                location: "那霸 -> 桃園",
                stay: "溫暖的家",
                activities: [
                    { time: "10:15", title: "前往機場", type: "transport", desc: "搭單軌至那霸機場", icon: "🚆" },
                    { time: "10:45", title: "國內線航廈", type: "shop", desc: "最後衝刺！伴手禮款式最多", icon: "🎁" },
                    { time: "13:15", title: "回程起飛", type: "transport", desc: "MM927 那霸 OKA -> 桃園 TPE", icon: "🛫" },
                    { time: "13:50", title: "抵達台灣", type: "transport", desc: "繼續朝財富自由邁進！", icon: "🏠" }
                ]
            }
        ];

        // --- State Management ---
        let state = {
            currentDay: 0,
            filter: 'all'
        };

        // --- DOM Elements ---
        const dayTabsContainer = document.getElementById('dayTabs');
        const itineraryContent = document.getElementById('itineraryContent');
        const currentDateDisplay = document.getElementById('currentDateDisplay');
        const filterButtons = document.querySelectorAll('.filter-btn');

        // --- Logic ---

        function renderTabs() {
            dayTabsContainer.innerHTML = '';
            itineraryData.forEach((day, index) => {
                const btn = document.createElement('button');
                const isActive = index === state.currentDay;
                btn.className = `flex-none px-6 py-4 text-sm font-medium transition-colors border-b-2 whitespace-nowrap ${isActive ? 'border-teal-500 text-teal-600 bg-teal-50/50' : 'border-transparent text-slate-500 hover:text-slate-700 hover:bg-slate-50'}`;
                btn.innerHTML = `
                    <div class="font-bold">Day ${day.day}</div>
                    <div class="text-xs opacity-80">${day.date.split(' ')[0]}</div>
                `;
                btn.onclick = () => {
                    state.currentDay = index;
                    renderTabs();
                    renderItinerary();
                };
                dayTabsContainer.appendChild(btn);
            });
        }

        function renderItinerary() {
            const dayData = itineraryData[state.currentDay];
            currentDateDisplay.textContent = `${dayData.date} - ${dayData.title}`;
            
            // Filter logic
            const filteredActivities = dayData.activities.filter(act => {
                if (state.filter === 'all') return true;
                return act.type === state.filter;
            });

            itineraryContent.innerHTML = '<div class="timeline-line"></div>'; // Reset keep line

            if (filteredActivities.length === 0) {
                itineraryContent.innerHTML += `
                    <div class="pl-12 py-10 text-slate-400 italic">
                        此分類下無活動。
                    </div>
                `;
                return;
            }

            filteredActivities.forEach(act => {
                const item = document.createElement('div');
                item.className = 'relative flex gap-6 items-start group animate-fade-in';
                
                // Color coding based on type
                let iconColorClass = "bg-slate-100 text-slate-500";
                if (act.type === 'food') iconColorClass = "bg-orange-100 text-orange-600";
                if (act.type === 'shop') iconColorClass = "bg-pink-100 text-pink-600";
                if (act.type === 'spot') iconColorClass = "bg-teal-100 text-teal-600";
                if (act.type === 'transport') iconColorClass = "bg-blue-100 text-blue-600";
                if (act.type === 'stay') iconColorClass = "bg-indigo-100 text-indigo-600";

                // Highlight style
                const highlightClass = act.highlight ? "border-amber-200 bg-amber-50/50" : "border-slate-100 bg-white";

                item.innerHTML = `
                    <div class="z-10 flex-none w-12 h-12 rounded-full ${iconColorClass} flex items-center justify-center text-xl shadow-sm border-2 border-white">
                        ${act.icon}
                    </div>
                    <div class="flex-1 p-4 rounded-xl border ${highlightClass} shadow-sm card-hover transition-all">
                        <div class="flex justify-between items-start mb-1">
                            <h4 class="font-bold text-slate-800">${act.title}</h4>
                            <span class="text-xs font-mono font-medium text-slate-500 bg-slate-100 px-2 py-1 rounded">${act.time}</span>
                        </div>
                        <p class="text-sm text-slate-600 leading-relaxed">${act.desc}</p>
                    </div>
                `;
                itineraryContent.appendChild(item);
            });
        }

        // --- Event Listeners for Filter ---
        filterButtons.forEach(btn => {
            btn.addEventListener('click', (e) => {
                // Update UI
                filterButtons.forEach(b => {
                    b.classList.remove('active-filter', 'bg-slate-800', 'text-white', 'border-transparent');
                    b.classList.add('bg-white', 'text-slate-700', 'border-slate-300');
                });
                
                // Set active style (using simple Tailwind classes toggle)
                // Actually let's just use specific style logic
                filterButtons.forEach(b => {
                     b.classList.remove('bg-teal-600', 'text-white', 'border-transparent');
                });
                e.target.classList.add('bg-teal-600', 'text-white', 'border-transparent');
                
                // Update state
                state.filter = e.target.dataset.filter;
                renderItinerary();
            });
        });

        // Initialize Filter Style
        document.querySelector('[data-filter="all"]').classList.add('bg-teal-600', 'text-white', 'border-transparent');


        // --- Chart.js Initialization ---
        function initChart() {
            const ctx = document.getElementById('tripChart').getContext('2d');
            
            // Calculate distribution
            let counts = { spot: 0, food: 0, shop: 0, transport: 0 };
            itineraryData.forEach(day => {
                day.activities.forEach(act => {
                    if (counts[act.type] !== undefined) counts[act.type]++;
                });
            });

            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['景點 & 樂園', '美食 & 饗宴', '購物 & 免稅', '交通 & 移動'],
                    datasets: [{
                        data: [counts.spot, counts.food, counts.shop, counts.transport],
                        backgroundColor: [
                            '#0d9488', // Teal (Spot)
                            '#f97316', // Orange (Food)
                            '#db2777', // Pink (Shop)
                            '#3b82f6'  // Blue (Transport)
                        ],
                        borderWidth: 0,
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                usePointStyle: true,
                                font: { size: 11 }
                            }
                        }
                    },
                    layout: {
                        padding: 10
                    }
                }
            });
        }

        // --- Initialization ---
        window.addEventListener('DOMContentLoaded', () => {
            renderTabs();
            renderItinerary();
            initChart();
        });

    </script>
</body>
</html>
