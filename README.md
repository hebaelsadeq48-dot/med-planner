# med-plann<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MedHub Pro | الإصدار المتكامل</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body { background: radial-gradient(circle at top, #1e293b, #0f172a); color: white; font-family: 'Cairo', sans-serif; min-height: 100vh; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 24px; }
        .notebook-line { border-bottom: 1px solid rgba(255, 255, 255, 0.05); padding: 15px 0; }
        input[type="checkbox"] { appearance: none; width: 22px; height: 22px; border: 2px solid #fb923c; border-radius: 50%; cursor: pointer; position: relative; transition: 0.3s; }
        input[type="checkbox"]:checked { background: #fb923c; box-shadow: 0 0 15px #fb923c; }
        input[type="checkbox"]:checked::after { content: '✔'; position: absolute; color: white; font-size: 14px; top: -2px; left: 4px; }
        .mood-btn { cursor: pointer; transition: 0.3s; padding: 8px; border-radius: 15px; filter: grayscale(100%); opacity: 0.5; }
        .mood-btn.active { filter: grayscale(0%); opacity: 1; transform: scale(1.3); background: rgba(251, 146, 60, 0.2); box-shadow: 0 0 20px rgba(251, 146, 60, 0.4); }
        .hidden { display: none; }
    </style>
</head>
<body class="p-4 md:p-8">

    <div id="main-menu" class="max-w-6xl mx-auto mt-10 text-center animate-fade-in">
        <h1 class="text-4xl font-bold mb-16 text-white tracking-tight">بوابتك لإدارة يومك</h1>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 px-4">
            <div onclick="showPage('planner-page')" class="glass p-12 cursor-pointer hover:border-orange-500 transition border-2 border-transparent group">
                <i class="fas fa-book-open text-6xl text-orange-400 mb-6 group-hover:scale-110 transition"></i>
                <h2 class="text-2xl font-bold">نوتة الإنجاز</h2>
            </div>
            <div onclick="showPage('timer-page')" class="glass p-12 cursor-pointer hover:border-sky-400 transition border-2 border-transparent group">
                <i class="fas fa-stopwatch text-6xl text-sky-400 mb-6 group-hover:scale-110 transition"></i>
                <h2 class="text-2xl font-bold">مؤقت التركيز</h2>
            </div>
            <div onclick="showPage('medical-page')" class="glass p-12 cursor-pointer hover:border-red-500 transition border-2 border-transparent group">
                <i class="fas fa-heartbeat text-6xl text-red-500 mb-6 group-hover:scale-110 transition"></i>
                <h2 class="text-2xl font-bold font-sans uppercase">Health Stats</h2>
            </div>
        </div>
    </div>

    <div id="planner-page" class="hidden max-w-6xl mx-auto">
        <button onclick="showPage('main-menu')" class="text-orange-400 mb-8 font-bold flex items-center gap-2 hover:translate-x-2 transition">
            <i class="fas fa-arrow-right"></i> العودة للرئيسية
        </button>
        <div class="glass p-8 md:p-12">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-10 gap-6 border-b border-white/10 pb-8">
                <div>
                    <h2 id="today-date" class="text-2xl font-bold text-white mb-2">التاريخ: ...</h2>
                    <p class="text-orange-400 text-lg font-bold italic">"فَإِنَّ مَعَ الْعُسْرِ يُسْرًا"</p>
                </div>
                <div class="bg-white/5 p-4 rounded-2xl border border-white/10 flex items-center gap-4">
                    <span class="text-sm font-bold opacity-70">مود النهاردة:</span>
                    <div class="flex gap-3 text-3xl">
                        <span class="mood-btn" onclick="activateMood(this)">😊</span>
                        <span class="mood-btn" onclick="activateMood(this)">🙂</span>
                        <span class="mood-btn" onclick="activateMood(this)">☹️</span>
                        <span class="mood-btn" onclick="activateMood(this)">😫</span>
                    </div>
                </div>
            </div>
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                <div>
                    <h3 class="text-xl font-bold text-orange-400 mb-6 border-r-4 border-orange-500 pr-3">قائمة المهام</h3>
                    <div id="tasks-container">
                        <div class="notebook-line flex items-center"><input type="checkbox" class="ml-4"><input type="text" placeholder="اكتب مادة المذاكرة هنا..." class="bg-transparent border-none outline-none w-full text-xl text-white"></div>
                    </div>
                    <button onclick="addRow()" class="mt-6 text-orange-400 font-bold hover:text-white">+ إضافة سطر جديد</button>
                </div>
                <div class="bg-sky-900/20 p-8 rounded-3xl border border-sky-500/20 text-right">
                    <h4 class="text-sky-300 font-bold mb-4 italic text-lg">مكنتش تعرف.. أديك عرفت!</h4>
                    <p class="text-gray-300 leading-relaxed text-lg">"تقسيم المهام الكبيرة يجعلها أسهل في التنفيذ ويزيد من إنتاجيتك بشكل ملحوظ."</p>
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
            <button id="t-btn" onclick="startTimer()" class="bg-sky-600 px-20 py-5 rounded-2xl text-3xl font-bold shadow-2xl hover:bg-sky-500 transition">START</button>
            <button onclick="resetTimer()" class="bg-white/10 px-10 py-5 rounded-2xl text-xl font-bold hover:bg-white/20">RESET</button>
        </div>
    </div>

    <div id="medical-page" class="hidden max-w-4xl mx-auto" dir="ltr">
        <button onclick="showPage('main-menu')" class="text-red-400 mb-10 text-xl font-bold flex items-center gap-2">
            <i class="fas fa-chevron-left"></i> BACK TO HOME
        </button>
        <div class="glass p-12 text-center">
            <h2 class="text-4xl font-bold mb-10 text-red-500 font-sans tracking-widest">BMI CALCULATOR</h2>
            <div class="space-y-6 max-w-md mx-auto">
                <input type="number" id="weight" placeholder="Weight (kg)" class="w-full bg-white/5 p-6 rounded-2xl border border-white/10 text-2xl outline-none focus:border-red-500 transition">
                <input type="number" id="height" placeholder="Height (cm)" class="w-full bg-white/5 p-6 rounded-2xl border border-white/10 text-2xl outline-none focus:border-red-500 transition">
                <button onclick="calculateBMI()" class="w-full bg-red-600 py-6 rounded-2xl text-2xl font-bold hover:bg-red-700 transition">ANALYZE</button>
                <div id="bmi-result" class="text-8xl font-bold mt-10 text-red-400 animate-pulse">-</div>
            </div>
        </div>
    </div>

    <script>
        // 1. منطق التنقل بين الصفحات
        function showPage(id) {
            document.querySelectorAll('[id$="-page"], #main-menu').forEach(p => p.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
        }

        // 2. منطق الإيموجيز (أربعة خيارات)
        function activateMood(el) {
            document.querySelectorAll('.mood-btn').forEach(b => b.classList.remove('active'));
            el.classList.add('active');
        }

        // 3. منطق إضافة المهام
        function addRow() {
            const div = document.createElement('div');
            div.className = "notebook-line flex items-center";
            div.innerHTML = '<input type="checkbox" class="ml-4"><input type="text" class="bg-transparent border-none outline-none w-full text-xl text-white">';
            document.getElementById('tasks-container').appendChild(div);
        }

        // 4. عرض التاريخ التلقائي
        document.getElementById('today-date').innerText = "التاريخ: " + new Date().toLocaleDateString('ar-EG', {day:'numeric', month:'long'});

        // 5. منطق المؤقت (العد والعودة)
        let timeLeft = 1500, timerId = null;
        function startTimer() {
            const btn = document.getElementById('t-btn');
            if(timerId) { 
                clearInterval(timerId); 
                timerId = null; 
                btn.innerText = "START"; 
                btn.style.backgroundColor = "#0284c7";
            } else {
                btn.innerText = "PAUSE";
                btn.style.backgroundColor = "#ea580c";
                timerId = setInterval(() => {
                    timeLeft--; 
                    let m = Math.floor(timeLeft/60), s = timeLeft%60;
                    document.getElementById('display').innerText = `${m}:${s.toString().padStart(2,'0')}`;
                    if(timeLeft <= 0) { clearInterval(timerId); alert("انتهى وقت التركيز!"); }
                }, 1000);
            }
        }
        function resetTimer() { 
            clearInterval(timerId); 
            timerId = null; 
            timeLeft = 1500; 
            document.getElementById('display').innerText = "25:00"; 
            document.getElementById('t-btn').innerText = "START";
            document.getElementById('t-btn').style.backgroundColor = "#0284c7";
        }

        // 6. منطق حاسبة BMI
        function calculateBMI() {
            const w = document.getElementById('weight').value, h = document.getElementById('height').value/100;
            if(w && h) {
                const bmi = (w/(h*h)).toFixed(1);
                document.getElementById('bmi-result').innerText = bmi;
            }
        }
    </script>
</body>
</html>
er
