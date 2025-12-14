# dspt903107.github.io
奕成老師的教學網站
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>議論文寫作小幫手：如何在失敗中學習</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        /* Custom font settings for Traditional Chinese */
        body {
            font-family: 'Noto Sans TC', system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background-color: #fdfbf7; /* Warm neutral background */
            color: #4a4a4a;
        }
        
        /* Chart container specific styling as requested */
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }

        /* Custom tab active state */
        .tab-active {
            border-bottom: 3px solid #d97706; /* amber-600 */
            color: #d97706;
            font-weight: bold;
        }

        /* Card hover effects */
        .concept-card {
            transition: all 0.3s ease;
        }
        .concept-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        /* Input focus rings */
        input:focus, textarea:focus {
            outline: none;
            border-color: #d97706;
            ring: 2px;
            ring-color: #fcd34d;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Chosen Palette: Warm Neutrals (Background: #fdfbf7), Primary Text: #4a4a4a, Accents: Amber/Orange for focus, Sage Green for success. -->
    <!-- Application Structure Plan: 
         1. Hero Section: Introduces the topic and the "Teacher's Words" to set the tone.
         2. Tabbed Interface: 
            - "觀念學習" (Concepts): Visualizes the 3 Pillars of Argumentative Writing using interactive cards and a Chart.js doughnut chart to show structure balance.
            - "大綱構思" (Drafting): An interactive form wizard where students input their ideas. This directly translates the "Worksheet" table into a digital tool.
            - "自我檢核" (Checklist): A gamified checklist from the source material with a progress bar and a new "Export to Word" function upon completion.
         3. Dynamic Preview: A live-updating section that assembles the student's inputs into a cohesive essay structure, rewarding them for filling out the form.
         Rationale: This structure breaks the writing process into manageable chunks (Learn -> Do -> Review -> Export), making it less intimidating for 5th graders while keeping all content on one page.
    -->
    <!-- Visualization & Content Choices:
         1. Doughnut Chart: Represents the "Structure" of an essay. Goal: Inform/Organize. Interaction: Click slices to filter concept cards. Justification: Visualizes the proportion of intro/body/conclusion. Library: Chart.js.
         2. Interactive Cards: Represents Thesis, Evidence, Restatement. Goal: Inform. Interaction: Hover/Click to see details. Justification: Breaks down dense text into digestible chunks. Method: HTML/Tailwind.
         3. Input Wizard: Represents the Drafting Table. Goal: Organize/Change. Interaction: Real-time text update in the "Preview" box. Justification: Immediate feedback helps students see how their points connect. Method: Vanilla JS.
         4. Progress Bar: Represents Checklist completion. Goal: Inform/Motivate. Interaction: Updates on checkbox click. Justification: Gamifies the review process. Method: HTML/CSS/JS.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <!-- Navigation -->
    <nav class="bg-white shadow-sm sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4">
            <div class="flex justify-between items-center h-16">
                <div class="flex items-center">
                    <span class="text-2xl mr-2">📝</span>
                    <span class="font-bold text-xl text-gray-800">寫作小幫手</span>
                </div>
                <div class="flex space-x-4">
                    <button onclick="switchTab('concepts')" id="tab-concepts" class="px-3 py-2 text-sm font-medium text-gray-600 hover:text-amber-600 transition-colors tab-active">觀念學習</button>
                    <button onclick="switchTab('drafting')" id="tab-drafting" class="px-3 py-2 text-sm font-medium text-gray-600 hover:text-amber-600 transition-colors">大綱構思</button>
                    <button onclick="switchTab('checklist')" id="tab-checklist" class="px-3 py-2 text-sm font-medium text-gray-600 hover:text-amber-600 transition-colors">自我檢核</button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-6xl mx-auto px-4 py-8 w-full">

        <!-- Hero Section (Teacher's Words) -->
        <section class="mb-10 bg-amber-50 rounded-2xl p-8 border border-amber-100 shadow-sm">
            <h1 class="text-3xl font-bold text-amber-900 mb-4">題目：如何在失敗中學習</h1>
            <div class="flex flex-col md:flex-row gap-6 items-start">
                <div class="md:w-3/4">
                    <h2 class="text-xl font-semibold text-amber-800 mb-2">🌟 老師的話</h2>
                    <p class="text-gray-700 leading-relaxed text-lg">
                        失敗並不可怕，它就像我們在遊戲中遇到的「暫停」鍵 ⏸️，讓我們有機會喘口氣，看看自己哪裡可以做得更好。
                        一篇好的議論文，就是要讓讀者也相信這個道理！準備好開始你的寫作探險了嗎？
                    </p>
                </div>
                <div class="md:w-1/4 flex justify-center items-center bg-white p-4 rounded-xl shadow-sm">
                    <div class="text-center">
                        <div class="text-4xl mb-2">🌱</div>
                        <p class="text-sm text-gray-500 font-medium">失敗是成長的養分</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- View 1: Concepts (The 3 Pillars) -->
        <div id="view-concepts" class="animate-fade-in block">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                
                <!-- Left: Interactive Chart -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                    <h3 class="text-xl font-bold text-gray-800 mb-2">文章結構比例圖</h3>
                    <p class="text-sm text-gray-500 mb-6">這張圖顯示了一篇完整議論文的三個重要部分。試著點擊圖表上的區塊，看看它們代表什麼意思！</p>
                    
                    <div class="chart-container">
                        <canvas id="structureChart"></canvas>
                    </div>
                    
                    <div class="mt-4 text-center text-sm text-gray-400">
                        點擊上方圖表區塊可篩選右側卡片
                    </div>
                </div>

                <!-- Right: Concept Cards -->
                <div class="space-y-4">
                    <h3 class="text-xl font-bold text-gray-800 mb-2">議論文的三大核心要素</h3>
                    <p class="text-sm text-gray-500 mb-4">就像蓋房子需要柱子，這三個要素是支撐你文章的關鍵。</p>

                    <!-- Card 1: Thesis -->
                    <div id="card-thesis" class="concept-card bg-white p-6 rounded-xl border-l-4 border-amber-500 shadow-sm cursor-pointer hover:bg-amber-50 transition-colors" onclick="highlightConcept('thesis')">
                        <div class="flex justify-between items-start">
                            <div>
                                <h4 class="text-lg font-bold text-gray-800">1. 論點 (Thesis)</h4>
                                <span class="inline-block bg-amber-100 text-amber-800 text-xs px-2 py-1 rounded-full mt-1 mb-2">第一段</span>
                            </div>
                            <span class="text-2xl">🎯</span>
                        </div>
                        <p class="text-gray-600 mt-2">你的主要觀點或主張。告訴讀者你對主題的立場，這是文章的靈魂。</p>
                    </div>

                    <!-- Card 2: Evidence -->
                    <div id="card-evidence" class="concept-card bg-white p-6 rounded-xl border-l-4 border-sky-500 shadow-sm cursor-pointer hover:bg-sky-50 transition-colors" onclick="highlightConcept('evidence')">
                        <div class="flex justify-between items-start">
                            <div>
                                <h4 class="text-lg font-bold text-gray-800">2. 論據 (Evidence)</h4>
                                <span class="inline-block bg-sky-100 text-sky-800 text-xs px-2 py-1 rounded-full mt-1 mb-2">中間段落</span>
                            </div>
                            <span class="text-2xl">🌳</span>
                        </div>
                        <p class="text-gray-600 mt-2">用來證明論點的理由、事例、數據或故事。讓你的觀點站得住腳，有說服力。</p>
                    </div>

                    <!-- Card 3: Restatement -->
                    <div id="card-restatement" class="concept-card bg-white p-6 rounded-xl border-l-4 border-green-500 shadow-sm cursor-pointer hover:bg-green-50 transition-colors" onclick="highlightConcept('restatement')">
                        <div class="flex justify-between items-start">
                            <div>
                                <h4 class="text-lg font-bold text-gray-800">3. 重申論點 (Conclusion)</h4>
                                <span class="inline-block bg-green-100 text-green-800 text-xs px-2 py-1 rounded-full mt-1 mb-2">結尾段</span>
                            </div>
                            <span class="text-2xl">👑</span>
                        </div>
                        <p class="text-gray-600 mt-2">用不同的語氣再次強調論點。總結全文，加深印象，讓文章有力地結束。</p>
                    </div>
                    
                    <button onclick="switchTab('drafting')" class="w-full mt-4 bg-amber-600 text-white font-bold py-3 px-4 rounded-xl hover:bg-amber-700 transition-colors shadow-md flex justify-center items-center">
                        我懂了！開始構思大綱 <span class="ml-2">➡️</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- View 2: Drafting (The Interactive Form) -->
        <div id="view-drafting" class="hidden animate-fade-in">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                
                <!-- Left Column: Input Form -->
                <div class="lg:col-span-2 space-y-8">
                    
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                        <div class="border-b border-gray-100 pb-4 mb-4">
                            <h3 class="text-xl font-bold text-gray-800 flex items-center">
                                <span class="bg-amber-100 text-amber-800 rounded-full w-8 h-8 flex items-center justify-center mr-3 text-sm">1</span>
                                第一段：提出論點
                            </h3>
                            <p class="text-sm text-gray-500 mt-2">任務：清楚說明你對「失敗」的看法。</p>
                        </div>
                        <div class="space-y-4">
                            <label class="block text-sm font-medium text-gray-700">我的主張是：</label>
                            <div class="flex flex-col gap-2">
                                <button onclick="setInputValue('input-thesis', '失敗不是終點，而是成長的機會。')" class="text-left text-xs bg-gray-50 hover:bg-gray-100 p-2 rounded text-gray-500 border border-dashed border-gray-300 transition-colors">💡 範例：失敗不是終點，而是成長的機會。</button>
                                <button onclick="setInputValue('input-thesis', '只要我們願意檢討，失敗就是最好的老師。')" class="text-left text-xs bg-gray-50 hover:bg-gray-100 p-2 rounded text-gray-500 border border-dashed border-gray-300 transition-colors">💡 範例：只要我們願意檢討，失敗就是最好的老師。</button>
                            </div>
                            <textarea id="input-thesis" rows="3" class="w-full border-gray-300 border rounded-lg p-3 shadow-sm focus:border-amber-500 focus:ring-1 focus:ring-amber-500" placeholder="寫下你的論點..." oninput="updatePreview()"></textarea>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                        <div class="border-b border-gray-100 pb-4 mb-4">
                            <h3 class="text-xl font-bold text-gray-800 flex items-center">
                                <span class="bg-sky-100 text-sky-800 rounded-full w-8 h-8 flex items-center justify-center mr-3 text-sm">2</span>
                                中間段落：論據證明
                            </h3>
                            <p class="text-sm text-gray-500 mt-2">任務：準備兩個證據來支持你的論點。</p>
                        </div>
                        
                        <!-- Evidence 1 -->
                        <div class="mb-6 p-4 bg-gray-50 rounded-xl">
                            <h4 class="font-bold text-gray-700 mb-2">論據一：個人經驗</h4>
                            <p class="text-xs text-gray-500 mb-3">說一個自己親身經歷的失敗故事，並說明學到了什麼。</p>
                            <textarea id="input-evidence1" rows="3" class="w-full border-gray-300 border rounded-lg p-3 shadow-sm focus:border-sky-500 focus:ring-1 focus:ring-sky-500 mb-2" placeholder="例如：我曾因為考試粗心而考不好，但我學到了檢查的重要性..." oninput="updatePreview()"></textarea>
                        </div>

                        <!-- Evidence 2 -->
                        <div class="p-4 bg-gray-50 rounded-xl">
                            <h4 class="font-bold text-gray-700 mb-2">論據二：名人事蹟</h4>
                            <p class="text-xs text-gray-500 mb-3">舉一個名人的例子，證明他們也是從失敗中走向成功。</p>
                            
                            <!-- Famous Person Selector -->
                            <div class="flex gap-2 mb-3 overflow-x-auto pb-2">
                                <button onclick="fillFamousPerson('edison')" class="whitespace-nowrap px-3 py-1 bg-white border border-gray-200 rounded-full text-xs hover:border-sky-400 hover:text-sky-600 transition-colors">💡 愛迪生</button>
                                <button onclick="fillFamousPerson('jordan')" class="whitespace-nowrap px-3 py-1 bg-white border border-gray-200 rounded-full text-xs hover:border-sky-400 hover:text-sky-600 transition-colors">🏀 喬丹</button>
                                <button onclick="fillFamousPerson('rowling')" class="whitespace-nowrap px-3 py-1 bg-white border border-gray-200 rounded-full text-xs hover:border-sky-400 hover:text-sky-600 transition-colors">🧙‍♀️ JK 羅琳</button>
                            </div>

                            <textarea id="input-evidence2" rows="3" class="w-full border-gray-300 border rounded-lg p-3 shadow-sm focus:border-sky-500 focus:ring-1 focus:ring-sky-500" placeholder="寫下名人的例子..." oninput="updatePreview()"></textarea>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
                        <div class="border-b border-gray-100 pb-4 mb-4">
                            <h3 class="text-xl font-bold text-gray-800 flex items-center">
                                <span class="bg-green-100 text-green-800 rounded-full w-8 h-8 flex items-center justify-center mr-3 text-sm">3</span>
                                結尾段：總結重申
                            </h3>
                            <p class="text-sm text-gray-500 mt-2">任務：用一句有力的話總結全文，鼓勵大家面對失敗。</p>
                        </div>
                        <div class="space-y-4">
                            <label class="block text-sm font-medium text-gray-700">我的總結：</label>
                            <button onclick="setInputValue('input-conclusion', '所以，讓我們勇敢地擁抱失敗吧！')" class="text-left text-xs bg-gray-50 hover:bg-gray-100 p-2 rounded text-gray-500 border border-dashed border-gray-300 transition-colors w-full">💡 範例：所以，讓我們勇敢地擁抱失敗吧！</button>
                            <textarea id="input-conclusion" rows="3" class="w-full border-gray-300 border rounded-lg p-3 shadow-sm focus:border-green-500 focus:ring-1 focus:ring-green-500" placeholder="寫下你的結論..." oninput="updatePreview()"></textarea>
                        </div>
                    </div>

                </div>

                <!-- Right Column: Live Preview -->
                <div class="lg:col-span-1">
                    <div class="sticky top-24">
                        <div class="bg-amber-50 p-6 rounded-2xl border border-amber-200 shadow-md">
                            <div class="flex justify-between items-center mb-4">
                                <h3 class="text-lg font-bold text-amber-900">📄 文章大綱預覽</h3>
                                <span class="text-xs bg-white px-2 py-1 rounded text-amber-600 font-medium">即時更新</span>
                            </div>
                            
                            <div class="space-y-6 text-sm text-gray-700 font-serif leading-relaxed" id="preview-content">
                                <div class="preview-section">
                                    <h5 class="text-xs font-bold text-amber-600 mb-1">【第一段：論點】</h5>
                                    <p id="preview-thesis" class="italic text-gray-400">請在左側填寫論點...</p>
                                </div>
                                <div class="preview-section border-l-2 border-sky-200 pl-3">
                                    <h5 class="text-xs font-bold text-sky-600 mb-1">【論據一：經驗】</h5>
                                    <p id="preview-evidence1" class="italic text-gray-400">...</p>
                                </div>
                                <div class="preview-section border-l-2 border-sky-200 pl-3">
                                    <h5 class="text-xs font-bold text-sky-600 mb-1">【論據二：名人】</h5>
                                    <p id="preview-evidence2" class="italic text-gray-400">...</p>
                                </div>
                                <div class="preview-section">
                                    <h5 class="text-xs font-bold text-green-600 mb-1">【結尾：重申】</h5>
                                    <p id="preview-conclusion" class="italic text-gray-400">...</p>
                                </div>
                            </div>

                            <button onclick="switchTab('checklist')" class="w-full mt-8 bg-green-600 text-white font-bold py-2 px-4 rounded-lg hover:bg-green-700 transition-colors shadow flex justify-center items-center text-sm">
                                寫好了！去檢查 <span class="ml-2">➡️</span>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- View 3: Checklist (Review) -->
        <div id="view-checklist" class="hidden animate-fade-in">
            <div class="max-w-3xl mx-auto">
                <div class="bg-white p-8 rounded-2xl shadow-sm border border-gray-100">
                    <div class="text-center mb-8">
                        <h3 class="text-2xl font-bold text-gray-800">寫作檢核表</h3>
                        <p class="text-gray-500 mt-2">完成文章大綱後，來看看自己是不是都做到了！</p>
                    </div>

                    <!-- Progress Bar -->
                    <div class="mb-8">
                        <div class="flex justify-between text-sm font-medium text-gray-600 mb-2">
                            <span>完成進度</span>
                            <span id="progress-text">0%</span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-4">
                            <div id="progress-bar" class="bg-green-500 h-4 rounded-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                    </div>

                    <!-- Checklist Items -->
                    <div class="space-y-4">
                        <label class="flex items-center p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition-colors group">
                            <input type="checkbox" class="w-6 h-6 text-green-600 border-gray-300 rounded focus:ring-green-500 checkbox-item" onchange="updateProgress()">
                            <span class="ml-3 text-gray-700 group-hover:text-gray-900">1. 我的<strong>第一段</strong>是否清楚地提出了論點？</span>
                        </label>
                        <label class="flex items-center p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition-colors group">
                            <input type="checkbox" class="w-6 h-6 text-green-600 border-gray-300 rounded focus:ring-green-500 checkbox-item" onchange="updateProgress()">
                            <span class="ml-3 text-gray-700 group-hover:text-gray-900">2. 我的<strong>第二、三段</strong>是否有用具體的例子或故事來支持論點？</span>
                        </label>
                        <label class="flex items-center p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition-colors group">
                            <input type="checkbox" class="w-6 h-6 text-green-600 border-gray-300 rounded focus:ring-green-500 checkbox-item" onchange="updateProgress()">
                            <span class="ml-3 text-gray-700 group-hover:text-gray-900">3. 我的<strong>結尾段</strong>是否用不同的話再次強調了我的論點？</span>
                        </label>
                        <label class="flex items-center p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition-colors group">
                            <input type="checkbox" class="w-6 h-6 text-green-600 border-gray-300 rounded focus:ring-green-500 checkbox-item" onchange="updateProgress()">
                            <span class="ml-3 text-gray-700 group-hover:text-gray-900">4. 我的句子是否通順、語氣是否堅定，能說服別人？</span>
                        </label>
                        <label class="flex items-center p-4 border border-gray-200 rounded-xl cursor-pointer hover:bg-gray-50 transition-colors group">
                            <input type="checkbox" class="w-6 h-6 text-green-600 border-gray-300 rounded focus:ring-green-500 checkbox-item" onchange="updateProgress()">
                            <span class="ml-3 text-gray-700 group-hover:text-gray-900">5. 我檢查過所有的錯別字和標點符號了嗎？</span>
                        </label>
                    </div>

                    <!-- Final Success Message -->
                    <div id="success-message" class="hidden mt-8 text-center bg-green-50 p-6 rounded-xl border border-green-100 animate-bounce-slow">
                        <span class="text-4xl block mb-2">🎉</span>
                        <h4 class="text-xl font-bold text-green-800">太棒了！你已經準備好寫出一篇精彩的議論文了！</h4>
                        <p class="text-green-600 mt-2">現在就把你的大綱變成完整的文章吧！</p>
                    </div>
                    
                    <!-- New Export Button -->
                    <button id="export-button" onclick="exportToWord()" class="hidden w-full mt-4 bg-orange-600 text-white font-bold py-3 px-4 rounded-xl hover:bg-orange-700 transition-colors shadow-lg flex justify-center items-center text-lg">
                        📥 輸出完成的大綱 (Word 檔案)
                    </button>
                    
                     <div class="mt-8 text-center">
                        <button onclick="switchTab('drafting')" class="text-gray-400 hover:text-gray-600 underline text-sm">
                            ⬅️ 返回修改大綱
                        </button>
                    </div>

                </div>
            </div>
        </div>

    </main>

    <footer class="bg-gray-800 text-gray-300 py-6 text-center mt-auto">
        <p class="text-sm">五年級國語議論文寫作練習 | 加油！失敗是成功的媽媽！</p>
    </footer>

    <!-- JavaScript Logic -->
    <script>
        // State Management
        const state = {
            currentTab: 'concepts',
            inputs: {
                thesis: '',
                evidence1: '',
                evidence2: '',
                conclusion: ''
            }
        };

        // Initialize Chart
        document.addEventListener('DOMContentLoaded', function() {
            const ctx = document.getElementById('structureChart').getContext('2d');
            const chart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['論點 (開頭)', '論據 (中間)', '重申 (結尾)'],
                    datasets: [{
                        data: [20, 60, 20],
                        backgroundColor: [
                            '#f59e0b', // amber-500
                            '#0ea5e9', // sky-500
                            '#22c55e'  // green-500
                        ],
                        borderWidth: 0,
                        hoverOffset: 10
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                font: {
                                    family: "'Noto Sans TC', sans-serif",
                                    size: 14
                                },
                                padding: 20
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const labels = [
                                        '文章的靈魂，表明立場',
                                        '支持論點的理由與故事',
                                        '總結全文，加深印象'
                                    ];
                                    return labels[context.dataIndex];
                                }
                            }
                        }
                    },
                    onClick: (e, elements) => {
                        if (elements.length > 0) {
                            const index = elements[0].index;
                            const types = ['thesis', 'evidence', 'restatement'];
                            highlightConcept(types[index]);
                        }
                    }
                }
            });
        });

        // Tab Switching
        function switchTab(tabId) {
            // Update Tab UI
            document.querySelectorAll('nav button').forEach(btn => {
                btn.classList.remove('tab-active');
            });
            document.getElementById(`tab-${tabId}`).classList.add('tab-active');

            // Update View
            ['concepts', 'drafting', 'checklist'].forEach(id => {
                const el = document.getElementById(`view-${id}`);
                if (id === tabId) {
                    el.classList.remove('hidden');
                } else {
                    el.classList.add('hidden');
                }
            });

            // Scroll to top
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Concept Highlighting
        function highlightConcept(type) {
            // Reset all cards
            document.querySelectorAll('.concept-card').forEach(card => {
                card.classList.remove('ring-4', 'ring-opacity-50', 'ring-gray-300');
                card.style.transform = 'scale(1)';
            });

            // Highlight selected
            const selectedCard = document.getElementById(`card-${type}`);
            let ringColor = '';
            if(type === 'thesis') ringColor = 'ring-amber-300';
            if(type === 'evidence') ringColor = 'ring-sky-300';
            if(type === 'restatement') ringColor = 'ring-green-300';

            selectedCard.classList.add('ring-4', ringColor);
            selectedCard.style.transform = 'scale(1.02)';
            
            // Smooth scroll to cards on mobile
            if(window.innerWidth < 1024) {
                selectedCard.scrollIntoView({ behavior: 'smooth', block: 'center' });
            }
        }

        // Input Handling & Preview
        function updatePreview() {
            state.inputs.thesis = document.getElementById('input-thesis').value;
            state.inputs.evidence1 = document.getElementById('input-evidence1').value;
            state.inputs.evidence2 = document.getElementById('input-evidence2').value;
            state.inputs.conclusion = document.getElementById('input-conclusion').value;

            // Update Preview Text
            const setPreviewText = (id, text, placeholder) => {
                const el = document.getElementById(id);
                if (text.trim() === '') {
                    el.textContent = placeholder;
                    el.classList.add('text-gray-400', 'italic');
                    el.classList.remove('text-gray-800', 'not-italic');
                } else {
                    el.textContent = text;
                    el.classList.remove('text-gray-400', 'italic');
                    el.classList.add('text-gray-800', 'not-italic');
                }
            };

            setPreviewText('preview-thesis', state.inputs.thesis, '請在左側填寫論點...');
            setPreviewText('preview-evidence1', state.inputs.evidence1, '等待輸入經驗...');
            setPreviewText('preview-evidence2', state.inputs.evidence2, '等待輸入名人例子...');
            setPreviewText('preview-conclusion', state.inputs.conclusion, '等待輸入結論...');
        }

        // Helper: Set Input Value
        function setInputValue(id, value) {
            const input = document.getElementById(id);
            input.value = value;
            updatePreview();
            // Flash effect
            input.classList.add('bg-yellow-50');
            setTimeout(() => input.classList.remove('bg-yellow-50'), 300);
        }

        // Helper: Fill Famous Person Data
        function fillFamousPerson(person) {
            const data = {
                edison: '發明大王愛迪生失敗了上千次才發明燈泡，他說：「我沒有失敗，我只是發現了一千種行不通的方法。」',
                jordan: '籃球之神喬丹如果不曾投失過那麼多球，就不會如此成功。他曾說：「我可以接受失敗，但我不能接受沒嘗試。」',
                rowling: '哈利波特的作者JK羅琳，在成功之前曾被好幾家出版社拒絕，生活困苦，但她堅持寫作，最後終於成功。'
            };
            setInputValue('input-evidence2', data[person]);
        }

        // Checklist Progress
        function updateProgress() {
            const checkboxes = document.querySelectorAll('.checkbox-item');
            const total = checkboxes.length;
            let checked = 0;

            checkboxes.forEach(box => {
                if (box.checked) checked++;
            });

            const percent = Math.round((checked / total) * 100);
            
            // UI Update
            const bar = document.getElementById('progress-bar');
            bar.style.width = `${percent}%`;
            document.getElementById('progress-text').textContent = `${percent}%`;

            // Success Message & Export Button
            const successMsg = document.getElementById('success-message');
            const exportBtn = document.getElementById('export-button');
            if (percent === 100) {
                successMsg.classList.remove('hidden');
                exportBtn.classList.remove('hidden');
                bar.classList.add('bg-green-600');
                bar.classList.remove('bg-green-500');
            } else {
                successMsg.classList.add('hidden');
                exportBtn.classList.add('hidden');
                bar.classList.add('bg-green-500');
                bar.classList.remove('bg-green-600');
            }
        }
        
        // Export to Word Function
        function exportToWord() {
            const thesis = document.getElementById('preview-thesis').textContent.trim();
            const evidence1 = document.getElementById('preview-evidence1').textContent.trim();
            const evidence2 = document.getElementById('preview-evidence2').textContent.trim();
            const conclusion = document.getElementById('preview-conclusion').textContent.trim();

            if (!thesis || !evidence1 || !evidence2 || !conclusion || 
                thesis.includes('請在左側填寫') || evidence1.includes('等待輸入') || evidence2.includes('等待輸入') || conclusion.includes('等待輸入')) {
                // Use a simple prompt replacement for the alert constraint.
                alert('⚠️ 您的文章大綱尚未填寫完整，請先填寫好所有段落內容再匯出！'); 
                return;
            }

            // Word content structure as HTML
            const contentHtml = `
                <html xmlns:o='urn:schemas-microsoft-com:office:office' xmlns:w='urn:schemas-microsoft-com:office:word' xmlns='http://www.w3.org/TR/REC-html40'>
                <head><title>議論文大綱</title>
                <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
                <style>
                    body { font-family: "Noto Sans TC", "微軟正黑體", sans-serif; line-height: 1.8; max-width: 800px; margin: 40px auto; }
                    h1 { color: #f97316; border-bottom: 2px solid #f97316; padding-bottom: 10px; margin-bottom: 20px; font-size: 24px; }
                    .section { margin-bottom: 30px; padding: 15px; border-left: 5px solid #0ea5e9; background-color: #f0f9ff; }
                    .thesis { border-left-color: #f59e0b; background-color: #fffbeb; }
                    .conclusion { border-left-color: #22c55e; background-color: #f0fff4; }
                    p { margin: 5px 0 0 0; font-size: 16px; }
                    strong { font-size: 1.2em; display: block; margin-bottom: 5px; color: #4a4a4a; }
                </style>
                </head>
                <body>
                    <h1>【如何在失敗中學習】議論文大綱</h1>
                    
                    <div class="section thesis">
                        <strong>🎯 第一段：核心論點</strong>
                        <p>${thesis}</p>
                    </div>

                    <div class="section">
                        <strong>🌳 第二段：論據一 (個人經驗)</strong>
                        <p>${evidence1}</p>
                    </div>

                    <div class="section">
                        <strong>🌳 第三段：論據二 (名人事蹟)</strong>
                        <p>${evidence2}</p>
                    </div>

                    <div class="section conclusion">
                        <strong>👑 第四段：總結與重申</strong>
                        <p>${conclusion}</p>
                    </div>
                    
                    <p style="margin-top: 40px; color: #777; font-size: 0.9em;">---</p>
                    <p style="color: #777; font-size: 0.9em;">(此大綱由寫作小幫手產生，請以此為基礎開始撰寫完整文章。)</p>
                </body>
                </html>
            `;

            // Create a Blob with the content
            const blob = new Blob([contentHtml], {
                type: 'application/msword;charset=utf-8'
            });

            // Use URL.createObjectURL to create a temporary download link
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = '議論文大綱.doc'; // Use .doc extension

            // Append to body, click, and remove
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);

            // Revoke the object URL after a short delay
            setTimeout(() => URL.revokeObjectURL(link.href), 100);
        }
        
        // Simple alert replacement function for compliance
        function alert(message) {
            const existingAlert = document.getElementById('custom-alert');
            if (existingAlert) existingAlert.remove();
            
            const alertBox = document.createElement('div');
            alertBox.id = 'custom-alert';
            alertBox.className = 'fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4';
            alertBox.innerHTML = `
                <div class="bg-white p-6 rounded-xl shadow-2xl max-w-sm w-full border-t-4 border-orange-500">
                    <h5 class="text-xl font-bold text-orange-700 mb-3">注意！</h5>
                    <p class="text-gray-700 mb-4">${message}</p>
                    <button onclick="document.getElementById('custom-alert').remove()" class="w-full bg-orange-600 text-white font-bold py-2 rounded-lg hover:bg-orange-700 transition-colors">
                        確定
                    </button>
                </div>
            `;
            document.body.appendChild(alertBox);
        }

    </script>
</body>
</html>
