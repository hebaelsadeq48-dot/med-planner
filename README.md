<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MedHub Pro | الإصدار الشامل</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body { background: radial-gradient(circle at top, #0f172a, #020617); color: white; font-family: 'Cairo', sans-serif; min-height: 100vh; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(15px); border: 1px solid rgba(251, 191, 36, 0.1); border-radius: 24px; }
        .mood-btn { cursor: pointer; transition: 0.3s; padding: 10px; border-radius: 15px; filter: grayscale(100%); opacity: 0.5; }
        .mood-btn.active { filter: grayscale(0%); opacity: 1; transform: scale(1.3); background: rgba(251, 191, 36, 0.2); box-shadow: 0 0 20px rgba(251, 191, 36, 0.4); }
        .notebook-line { border-bottom: 1px solid rgba(255, 215, 0, 0.05); padding: 12px 0; }
        input[type="checkbox"] { appearance: none; width: 22px; height: 22px; border: 2px solid #fbbf24; border-radius: 6px; cursor: pointer; position: relative; }
        input[type="checkbox"]:checked { background: #fbbf24; }
        input[type="checkbox"]:checked::after { content: '✔'; position: absolute; color: #000; font-size: 14px; top: -2px; left: 4px; font-weight: bold; }
        .hidden { display: none; }
    </style>
</head>
<body class="p-4 md:p-8">

    <div id="main-menu" class="max-w-6xl mx-auto mt-10 text-center">
        <h1 class="text-4xl font-bold mb-4 text-amber-400">MedHub Pro</h1>
        <p class="mb-12 opacity-80 text-lg italic text-amber-200">"خُطوة بخُطوة نحو الإنجاز"</p>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 px-4">
            <div onclick="showPage('planner-page')" class="glass border border-amber-500/30 p-10 cursor-pointer hover:bg-amber-900/10 transition group">
                <i class="fas fa-moon text-6xl text-amber-400 mb-6 group-hover:scale-110 transition"></i>
                <h2 class="text-2xl font-bold">نوتة الإنجاز</h2>
            </div>
            <div onclick="showPage('timer-page')" class="glass p-10 cursor-pointer hover:border-sky-400 transition group border border-white/5">
                <i class="fas fa-stopwatch text-6xl text-sky-400 mb-6 group-hover:scale-110 transition"></i>
                <h2 class="text-2xl font-bold">مؤقت التركيز</h2>
            </div>
            <div onclick="showPage('medical-page')" class="glass p-10 cursor-pointer hover:border-red-500 transition group border border-white/5">
                <i class="fas fa-heartbeat text-6xl text-red-500 mb-6 group-hover:scale-110 transition"></i>
                <h2 class="text-2xl font-bold uppercase font-sans">Health Stats</h2>
            </div>
        </div>
    </div>

    <div id="planner-page" class="hidden max-w-6xl mx-auto">
        <button onclick="showPage('main-menu')" class="text-amber-400 mb-8 font-bold flex items-center gap-2 hover:translate-x-2 transition">
            <i class="fas fa-arrow-right"></i> العودة للرئيسية
        </button>
        <div class="glass p-8 md:p-12 border border-amber-500/20">
            <div class="flex flex-col md:flex-row justify-between mb-10 gap-6 border-b border-amber-500/20 pb-8">
                <div>
                    <h2 id="today-date" class="text-2xl font-bold text-amber-400">التاريخ: ...</h2>
                    <p class="italic mt-2 text-amber-100/60">"فَاستَبِقُوا الخَيراتِ"</p>
                </div>
                <div class="bg-amber-900/20 p-4 rounded-2xl border border-amber-500/30 text-center min-w-[150px]">
                    <span class="block text-xs mb-1 opacity-70">سبحة الأذكار</span>
                    <div id="tasbih-count" class="text-3xl font-bold text-amber-400 mb-2">0</div>
                    <button onclick="countTasbih()" class="bg-amber-500 text-black px-6 py-1 rounded-full font-bold active:scale-90 transition">سبّح</button>
                </div>
                <div class="flex gap-3 text-3xl items-center bg-white/5 p-3 rounded-2xl">
                    <span class="mood-btn" onclick="setMood(this)">🌙</span>
                    <span class="mood-btn" onclick="setMood(this)">🕌</span>
                    <span class="mood-btn" onclick="setMood(this)">📿</span>
                    <span class="mood-btn" onclick="setMood(this)">🕯️</span>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                <div>
                    <h3 class="text-xl font-bold text-amber-400 mb-6 border-r-4 border-amber-500 pr-3">قائمة المهام اليومية</h3>
                    <div id="tasks-container">
                        <div class="notebook-line flex items-center"><input type="checkbox" class="ml-4"><input type="text" placeholder="ورد القرآن / مذاكرة فارما..." class="bg-transparent border-none outline-none w-full text-white text-lg"></div>
                    </div>
                    <button onclick="addRow()" class="mt-6 text-amber-400 font-bold hover:text-white">+ إضافة سطر جديد</button>
                </div>
                <div class="bg-white/5 p-8 rounded-3xl border border-white/5">
                    <h4 class="text-amber-300 font-bold mb-4 italic text-lg">مكنتش تعرف.. أديك عرفت!</h4>
                    <p class="text-gray-400 leading-relaxed">المذاكرة في رمضان تتطلب ذكاءً؛ استغلي ساعات "ما بعد الفجر" للمواد الصعبة، وساعات "ما قبل السحور" للمراجعة الخفيفة.</p>
                </div>
            </div>
        </div>
    </div>

    <div id="timer-page" class="hidden flex flex-col items-center justify-center min-h-[80vh]">
        <button onclick="showPage('main-menu')" class="text-sky-400 mb-12 text-2xl font-bold flex items-center gap-3 hover:scale-105 transition">
            <i class="fas fa-home"></i> العودة للرئيسية
        </button>
        <div id="display" class="text-[10rem] md:text-[14rem] font-bold text-white mb-10 leading-none tabular-nums">25:00</div>
        <div class="flex gap-8">
            <button id="t-btn" onclick="startT()" class="bg-sky-600 px-20 py-5 rounded-2xl text-3xl font-bold shadow-2xl hover:brightness-110 transition">START</button>
            <button onclick="resetT()" class="bg-white/10 px-10 py-5 rounded-2xl text-xl font-bold hover:bg-white/20">RESET</button>
        </div>
    </div>

    <div id="medical-page" class="hidden max-w-4xl mx-auto" dir="ltr">
        <button onclick="showPage('main-menu')" class="text-red-400 mb-10 text-xl font-bold flex items-center gap-2 hover:translate-x-[-10px] transition">
            <i class="fas fa-arrow-left"></i> BACK TO HOME
        </button>
        <div class="glass p-12 text-center border border-red-500/20">
            <h2 class="text-4xl font-bold mb-10 text-red-500 font-sans tracking-tighter">BMI CALCULATOR</h2>
            <div class="space-y-6 max-w-md mx-auto">
                <input type="number" id="w" placeholder="Weight (kg)" class="w-full bg-white/5 p-6 rounded-2xl border border-white/10 text-2xl outline-none focus:border-red-500 transition">
                <input type="number" id="h" placeholder="Height (cm)" class="w-full bg-white/5 p-6 rounded-2xl border border-white/10 text-2xl outline-none focus:border-red-500 transition">
                <button onclick="calcBMI()" class="w-full bg-red-600 py-6 rounded-2xl text-2xl font-bold hover:bg-red-700 transition shadow-lg">ANALYZE</button>
                <div id="res" class="text-8xl font-bold mt-10 text-red-400 animate-pulse">-</div>
            </div>
        </div>
    </div>

    <script>
        // التنقل بين الصفحات
        function showPage(id) {
            document.querySelectorAll('[id$="-page"], #main-menu').forEach(p => p.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
        }

        // منطق المود
        function setMood(el) {
            document.querySelectorAll('.mood-btn').forEach(b => b.classList.remove('active'));
            el.classList.add('active');
        }

        // إضافة أسطر للنوتة
        function addRow() {
            const div = document.createElement('div');
            div.className = "notebook-line flex items-center";
            div.innerHTML = '<input type="checkbox" class="ml-4"><input type="text" class="bg-transparent border-none outline-none w-full text-white text-lg">';
            document.getElementById('tasks-container').appendChild(div);
        }

        // التاريخ والسبحة
        document.getElementById('today-date').innerText = "التاريخ: " + new Date().toLocaleDateString('ar-EG', {day:'numeric', month:'long'});
        let c = 0;
        function countTasbih() { c++; document.getElementById('tasbih-count').innerText = c; }

        // منطق المؤقت (نفس المنطق القديم الشغال)
        let rem = 1500, inv = null;
        function startT() {
            const btn = document.getElementById('t-btn');
            if(inv) { 
                clearInterval(inv); inv = null; 
                btn.innerText = "START"; btn.classList.replace('bg-orange-600', 'bg-sky-600'); 
            } else {
                btn.innerText = "PAUSE"; btn.classList.replace('bg-sky-600', 'bg-orange-600');
                inv = setInterval(() => {
                    rem--; 
                    let m = Math.floor(rem/60), s = rem%60;
                    document.getElementById('display').innerText = `${m}:${s.toString().padStart(2,'0')}`;
                    if(rem <= 0) { clearInterval(inv); alert("انتهى وقت التركيز!"); resetT(); }
                }, 1000);
            }
        }
        function resetT() { clearInterval(inv); inv = null; rem = 1500; document.getElementById('display').innerText = "25:00"; document.getElementById('t-btn').innerText = "START"; document.getElementById('t-btn').classList.add('bg-sky-600'); }

        // حاسبة الـ BMI
        function calcBMI() {
            const weight = document.getElementById('w').value, height = document.getElementById('h').value/100;
            if(weight && height) {
                const bmi = (weight/(height*height)).toFixed(1);
                document.getElementById('res').innerText = bmi;
            }
        }
    </script>
</body>
</html>
