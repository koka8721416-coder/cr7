Enter<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>اختبر نفسك – الأوستراكودا (تفاعلي)</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background: linear-gradient(135deg, #f0f2f5 0%, #e0e5ec 100%);
            font-family: 'Tajawal', 'Cairo', 'Segoe UI', Tahoma, sans-serif;
            padding: 30px 20px;
            color: #1e2a36;
        }
        .container { max-width: 1000px; margin: 0 auto; }
        .header { text-align: center; margin-bottom: 40px; }
        .header h1 { font-size: 2rem; background: linear-gradient(135deg, #1e4a2f, #2c3e50); -webkit-background-clip: text; background-clip: text; color: transparent; }
        .sub { color: #5a6e7c; font-size: 1rem; border-bottom: 2px solid #b8860b; display: inline-block; padding-bottom: 6px; }
        .fossil-icon { font-size: 2rem; letter-spacing: 8px; color: #b8860b; margin-bottom: 10px; }
        .question-card {
            background: white;
            border-radius: 24px;
            margin-bottom: 25px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        .q-header {
            background: #1e3a2f;
            color: white;
            padding: 12px 24px;
            font-weight: bold;
            font-size: 1.1rem;
            border-right: 5px solid #b8860b;
        }
        .q-body { padding: 20px 25px; }
        .question-text { font-size: 1.05rem; font-weight: 600; color: #1a3a2a; margin-bottom: 18px; line-height: 1.5; }
        .options { display: flex; flex-direction: column; gap: 10px; margin-bottom: 15px; }
        .option {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 50px;
            padding: 10px 18px;
            cursor: pointer;
            transition: 0.2s;
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 500;
        }
        .option:hover { background: #e9ecef; border-color: #b8860b; transform: translateX(-3px); }
        .opt-letter { background: #2c3e50; color: white; width: 30px; height: 30px; display: inline-flex; align-items: center; justify-content: center; border-radius: 50%; font-weight: bold; font-size: 0.9rem; }
        .feedback {
            margin-top: 15px;
            padding: 12px 18px;
            border-radius: 12px;
            display: none;
            font-weight: 500;
        }
        .feedback.correct { background: #d4edda; color: #155724; border-right: 4px solid #28a745; }
        .feedback.wrong { background: #f8d7da; color: #721c24; border-right: 4px solid #dc3545; }
        .footer { text-align: center; margin-top: 30px; padding: 20px; color: #6c757d; font-size: 0.8rem; }
        @media (max-width: 700px) { .q-body { padding: 15px; } .option { padding: 8px 12px; } }
    </style>
</head>
<body>
<div class="container">
    <div class="header">
        <div class="fossil-icon">🦐 🧬 🐚</div>
        <h1>اختبر نفسك: الأوستراكودا</h1>
        <div class="sub">اختر الإجابة (أ، ب، ج، د) – ستصحح لك المنصة فورًا</div>
        <div style="margin-top: 10px; font-size: 0.85rem;">📌 30 سؤال اختيار من متعدد | 30 صح/خطأ | 10 مقالي (الإجابات تحت كل سؤال بعد اختيارك)</div>
    </div>

    <div id="questions-container"></div>
    <div class="footer">🦴 اضغط على أي إجابة – سيظهر لك "صحيح" أو "خطأ" مع الإجابة النموذجية</div>
</div>

<script>
    const questions = [
        // MCQ 1-30
        { type: "mcq", text: "الأوستراكودا تتبع أي شعبة من التصنيف؟", options: ["الرخويات", "المفصليات (Arthropoda)", "الحلقيات", "شوكيات الجلد"], correct: 1, explanation: "الأوستراكودا تتبع شعبة المفصليات (Arthropoda)، طائفة القشريات." },
        { type: "mcq", text: "الاسم العلمي للطائفة التي تتبعها الأوستراكودا هو:", options: ["Ostracoda", "Trilobita", "Maxillopoda", "Malacostraca"], correct: 0, explanation: "الاسم العلمي هو Ostracoda." },
        { type: "mcq", text: "كم زوجاً من الزوائد (appendages) تمتلك الأوستراكودا تقريباً؟", options: ["3 أزواج", "5 أزواج", "7 أزواج", "10 أزواج"], correct: 2, explanation: "تمتلك الأوستراكودا 7 أزواج من الزوائد." },
        { type: "mcq", text: "المصراعان في الأوستراكودا يرتبطان من الناحية:", options: ["البطنية", "الجانبية", "الظهرية (مفصلة hinge)", "الأمامية"], correct: 2, explanation: "ترتبط من الناحية الظهرية بواسطة المفصلة (hinge)." },
        { type: "mcq", text: "ما هو المدى الزمني (stratigraphic range) للأوستراكودا؟", options: ["الديفوني – الحديث", "الكمبري العلوي – الحديث", "الطباشيري – الحديث", "الترياسي – الحديث"], correct: 1, explanation: "ظهرت أول مرة في الكمبري العلوي واستمرت حتى الآن." },
        { type: "mcq", text: "العضلات التي تتحكم في فتح وغلق المصراعين تسمى:", options: ["العضلات الباسطة", "العضلات القابضة (Adductor muscles)", "الأربطة المرنة فقط", "العضلات الحلقية"], correct: 1, explanation: "العضلات القابضة (Adductor muscles) تتحكم في غلق المصراعين." },
        { type: "mcq", text: "أي من الأنواع التالية تمثل أوستراكودا المياه العذبة؟", options: ["Cythereidae", "Cypris", "Quadracythere", "Krithe"], correct: 1, explanation: "جنس Cypris من أوستراكودا المياه العذبة." },
        { type: "mcq", text: "أوستراكودا المياه العذبة تتميز بأن الدرقة:", options: ["سميكة وعليها زخرفة", "رقيقة – ملساء – بسيطة", "كبيرة جداً (أكثر من 5 سم)", "ذات مفصل مركب Amphidont"], correct: 1, explanation: "المياه العذبة: درقة رقيقة ملساء بسيطة." },
        { type: "mcq", text: "أوستراكودا المياه المالحة (البحرية) تتسم بـ:", options: ["اختفاء الزخرفة تماماً", "قنوات حافية متشعبة وثقوب عادية منخلية", "درقة شفافة بدون أي ثقوب", "غياب البقع العينية"], correct: 1, explanation: "البحرية: قنوات حافية متشعبة وثقوب منخلية وزخرفة واضحة." },
        { type: "mcq", text: "الأوستراكودا التي تعيش في منطقة الرف القاري (0-200م) تتميز بـ:", options: ["درقة طويلة رقيقة", "درقة سميكة – زخرفة واضحة – مفصل مركب", "غياب المفصلة", "درقة كروية عملاقة"], correct: 1, explanation: "الرف القاري: درقة سميكة، زخرفة واضحة، مفصل مركب." },
        { type: "mcq", text: "أوستراكودا أعماق Bathyal (200-2000م) مثالها جنس:", options: ["Cypris", "Quadracythere", "Krithe", "Macrocypris"], correct: 2, explanation: "جنس Krithe من أعماق Bathyal." },
        { type: "mcq", text: "في المناطق السحيقة Abyssal (>2000م) الأوستراكودا تكون:", options: ["كثيرة العدد ومتنوعة", "قليلة العدد – درقة شفافة", "ذات زخرفة خشنة جداً", "من نوع المياه العذبة"], correct: 1, explanation: "الأعماق السحيقة: قليلة العدد والتنوع، درقة شفافة." },
        { type: "mcq", text: "حرارة الماء المرتفعة تؤثر على الأوستراكودا بـ:", options: ["توقف النمو", "زيادة سرعة النمو", "تحولها إلى بيئة عذبة", "انقراضها فوراً"], correct: 1, explanation: "ارتفاع الحرارة يزيد من سرعة نمو الأوستراكودا." },
        { type: "mcq", text: "وفقاً لماركوفين (1962)، الأوستراكودا التي تعيش فوق النباتات البحرية تكون درقتها:", options: ["سميكة جداً وعليها أضلاع", "رقيقة – أملسة – خالية من الزخرفة", "قصيرة وخشنة", "كروية ضخمة"], correct: 1, explanation: "فوق النباتات: درقة رقيقة أملسة خالية من الزخرفة." },
        { type: "mcq", text: "الأوستراكودا الحافرة (Burrowing) تتميز بـ:", options: ["درقة جيرية قوية", "درقة شفافة هشة", "عدم وجود مفصلة", "زوائد طويلة جداً"], correct: 0, explanation: "الحافرة: درقة جيرية قوية." },
        { type: "mcq", text: "أي مما يلي يُستخدم لقياس معدل الترسيب في البيئات القديمة بواسطة الأوستراكودا؟", options: ["حجم الدرقة", "انفصال أو تلازم المصراعين", "لون الصدفة", "درجة زخرفة السطح"], correct: 1, explanation: "تلازم المصراعين = ترسيب سريع، انفصالهما = ترسيب بطيء." },
        { type: "mcq", text: "المفصلة من النوع Adont تعني:", options: ["مفصلة مركبة معقدة", "مفصلة عديمة الأسنان (بسيطة)", "مفصلة ذات أربعة أجزاء", "مفصلة متعرجة"], correct: 1, explanation: "Adont = عديمة الأسنان، بسيطة." },
        { type: "mcq", text: "مفصلة Amphidont تتكون من تقسيم الجزء الأوسط إلى:", options: ["جزء وحيد فقط", "جزء أمام أوسط + جزء خلف أوسط", "5 أجزاء متساوية", "حز واحد فقط"], correct: 1, explanation: "Amphidont: الجزء الأوسط مقسم إلى أمام أوسط وخلف أوسط." },
        { type: "mcq", text: "البقع العينية (Eye spots) في الأوستراكودا تكون بارزة بشكل خاص في:", options: ["أنواع المياه العذبة", "الأنواع البحرية ذات الزخرفة الواضحة", "الأنواع العمياء السحيقة", "اليرقات فقط"], correct: 1, explanation: "البقع العينية بارزة في الأنواع البحرية." },
        { type: "mcq", text: "أول من استخدم مصطلح Ostracoda كان:", options: ["سكوت (Scott)", "سارس (Sars)", "لاتريل (Latreille, 1806)", "هنجسمون"], correct: 2, explanation: "لاتريل (Latreille) عام 1806 أول من استخدم المصطلح." },
        { type: "mcq", text: "التصنيف الحديث للأوستراكودا (حقب المتوسطة والحديثة) يعتمد أساساً على:", options: ["لون الدرقة فقط", "شكل وتوزيع آثار العضلات (Muscle scars) والمفصلة", "حجم العيون", "طريقة السباحة"], correct: 1, explanation: "يعتمد على آثار العضلات والمفصلة." },
        { type: "mcq", text: "رتبة Paleocopida تتبع:", options: ["الرخويات", "الأوستراكودا", "الفورامينيفرا", "الراديولاريا"], correct: 1, explanation: "Paleocopida من رتب الأوستراكودا." },
        { type: "mcq", text: "الأوستراكودا تأتي في المرتبة ..... من حيث المضاهاة (Correlation) بعد الفورامينيفرا الطافية:", options: ["الأولى", "الثانية", "الثالثة", "الرابعة"], correct: 1, explanation: "المرتبة الثانية بعد الفورامينيفرا الطافية." },
        { type: "mcq", text: "أي العوامل البيئية التالية تؤثر بقوة على توزيع الأوستراكودا طبقاً لبرازييه (1980)؟", options: ["التيارات فقط", "الملوحة (Salinity)", "المد والجزر", "نوعية المفترسين فقط"], correct: 1, explanation: "الملوحة من أهم العوامل المؤثرة." },
        { type: "mcq", text: "أي من هؤلاء قسّم الأوستراكودا إلى 4 تحت رتب بناءً على الأجزاء الرخوة؟", options: ["سارس (Sars, 1866)", "سكوت (Scott)", "لاتريل", "داروين"], correct: 0, explanation: "سارس (Sars, 1866) قسمها إلى 4 تحت رتب." },
        { type: "mcq", text: "أي الفترات الجيولوجية شهدت تطوراً كبيراً وذروة انتشار للأوستراكودا؟", options: ["الكامبري المبكر", "البليستوسين (Pleistocene)", "الترياسي المبكر", "الأردفيشي السفلي"], correct: 1, explanation: "ذروة الانتشار في البليستوسين." },
        { type: "mcq", text: "الأوستراكودا التي تعيش حرة السباحة (Free swimming) تتميز بـ:", options: ["درقة سميكة مفصلية مركبة", "خفة وزن – طول – مفصلة Adont", "زوائد ضامرة", "عيون متحجرة"], correct: 1, explanation: "السباحة الحرة: خفة وزن، طول، مفصلة Adont." },
        { type: "mcq", text: "الأوستراكودا التي تعيش متكافلة مع الأسماك تتغذى على:", options: ["الطحالب فقط", "الفتات العالق بخياشيم الأسماك", "الدم", "العوالق النباتية فقط"], correct: 1, explanation: "تتغذى على الفتات العالق بخياشيم الأسماك." },
        { type: "mcq", text: "القيعان الرملية تؤدي إلى أن تكون درقة الأوستراكودا:", options: ["طويلة وناعمة", "قصيرة – ذات زخرفة خشنة", "كروية بالكامل", "مفقودة الزخرفة تماماً"], correct: 1, explanation: "القيعان الرملية: درقة قصيرة، زخرفة خشنة." },
        { type: "mcq", text: "رتبة Myodocopida في الأوستراكودا تضم غالباً أنواع:", options: ["قاعية حافرة", "هامة (pelagic) ذات درقة رقيقة", "مياه عذبة فقط", "متحجرة منذ الكمبري"], correct: 1, explanation: "Myodocopida: أنواع هائمة ذات درقة رقيقة." },
        // True/False 31-60
        { type: "tf", text: "الأوستراكودا من القشريات (Crustacea).", correct: true, explanation: "تصنف الأوستراكودا ضمن طائفة القشريات." },
        { type: "tf", text: "درقة الأوستراكودا تتكون من قطعة واحدة صلبة (مثل الحلزون).", correct: false, explanation: "تتكون من مصراعين (يميني ويساري)." },
        { type: "tf", text: "المفصلة (Hinge) توجد في الناحية البطنية للدرقة.", correct: false, explanation: "توجد في الناحية الظهرية." },
        { type: "tf", text: "المدى الزمني للأوستراكودا يبدأ من الكمبري العلوي.", correct: true, explanation: "ظهرت في الكمبري العلوي." },
        { type: "tf", text: "الأوستراكودا البحرية تكون زخرفتها أقل من أوستراكودا المياه العذبة.", correct: false, explanation: "البحرية زخرفتها أكثر وضوحاً." },
        { type: "tf", text: "المياه مختلطة الملوحة (Brakish) تتميز أوستراكوداها بدرقة سميكة ومفصلة Amphidont.", correct: true, explanation: "هذا صحيح وفقاً للتصنيف البيئي." },
        { type: "tf", text: "أوستراكودا الأعماق السحيقة تتميز بكثرة أعدادها وتنوعها الكبير.", correct: false, explanation: "قليلة العدد والتنوع." },
        { type: "tf", text: "ارتفاع درجة حرارة الماء يزيد من سرعة نمو الأوستراكودا.", correct: true, explanation: "الحرارة المرتفعة تزيد سرعة النمو." },
        { type: "tf", text: "عضلات Adductor muscles مسئولة عن فتح المصراعين فقط.", correct: false, explanation: "مسئولة عن غلق المصراعين." },
        { type: "tf", text: "الأوستراكودا يمكن أن تعيش في المياه العذبة والمالحة والمختلطة.", correct: true, explanation: "لها قدرة على التكيف في بيئات مختلفة." },
        { type: "tf", text: "جنس Cypris من أوستراكودا المياه المالحة.", correct: false, explanation: "من المياه العذبة." },
        { type: "tf", text: "التكاثر العذري (Parthenogenesis) هو أحد طرق تكاثر الأوستراكودا.", correct: true, explanation: "تتكاثر بالتكاثر العذري أو التزاوجي." },
        { type: "tf", text: "في المناطق سريعة الترسيب، تنفصل مصراعا الأوستراكودا بعد الموت.", correct: false, explanation: "تندفن معاً دون انفصال." },
        { type: "tf", text: "مفصلة Adont هي أكثر أنواع المفصلات تعقيداً.", correct: false, explanation: "هي بسيطة عديمة الأسنان." },
        { type: "tf", text: "أوستراكودا المياه العذبة تتميز بدرقة سميكة وزخرفة معقدة.", correct: false, explanation: "درقة رقيقة ملساء." },
        { type: "tf", text: "بعض أنواع الأوستراكودا تعيش متكافلة مع خياشيم الأسماك.", correct: true, explanation: "تعيش متكافلة وتتغذى على الفتات." },
        { type: "tf", text: "القيعان الرملية تؤدي إلى زخرفة ناعمة على درقة الأوستراكودا.", correct: false, explanation: "زخرفة خشنة." },
        { type: "tf", text: "البقع العينية (Eye spots) تكون أكثر وضوحاً في الأنواع البحرية.", correct: true, explanation: "بارزة في الأنواع البحرية." },
        { type: "tf", text: "الأوستراكودا تعيش فقط في البيئات البحرية.", correct: false, explanation: "تعيش في البحر والمياه العذبة والمختلطة." },
        { type: "tf", text: "العالم لاتريل (Latreille) هو أول من استخدم مصطلح Ostracoda.", correct: true, explanation: "عام 1806." },
        { type: "tf", text: "رتبة Myodocopida تضم أنواعاً قاعية فقط.", correct: false, explanation: "تضم أنواعاً هائمة pelagic." },
        { type: "tf", text: "الأوستراكودا تأتي في المرتبة الثانية في المضاهاة بعد الفورامينيفرا الطافية.", correct: true, explanation: "صحيح." },
        { type: "tf", text: "التصنيف الحديث للأوستراكودا يعتمد فقط على الشكل الخارجي للدرقة.", correct: false, explanation: "يعتمد على آثار العضلات والمفصلة." },
        { type: "tf", text: "الأوستراكودا الحافرة (Burrowing) درقتها قوية وجيرية.", correct: true, explanation: "صحيح." },
        { type: "tf", text: "الأعماق السحيقة (Abyssal) تتميز بتنوع كبير للأوستراكودا.", correct: false, explanation: "تنوع قليل." },
        { type: "tf", text: "درجة الحرارة المرتفعة تزيد من سرعة نمو الأوستراكودا.", correct: true, explanation: "صحيح." },
        { type: "tf", text: "مفصل Amphidont يحتوي على جزء أوسط مقسم إلى جزأين.", correct: true, explanation: "أمام أوسط وخلف أوسط." },
        { type: "tf", text: "الأوستراكودا ليس لها أهمية في تحديد المناخ القديم.", correct: false, explanation: "لها أهمية كبيرة." },
        { type: "tf", text: "أوستراكودا المياه العذبة تكون زخرفتها أكثر تعقيداً من البحرية.", correct: false, explanation: "البحرية أكثر تعقيداً." },
        { type: "tf", text: "الأوستراكودا تظهر في السجل الأحفوري من العصر الكمبري العلوي.", correct: true, explanation: "صحيح." },
        // Essay 61-70 (with show answer button concept but we keep answer hidden until clicked)
    ];

    function buildUI() {
        const container = document.getElementById('questions-container');
        container.innerHTML = '';

        for (let i = 0; i < questions.length; i++) {
            const q = questions[i];
            const card = document.createElement('div');
            card.className = 'question-card';
            card.setAttribute('data-qid', i);

            const header = document.createElement('div');
            header.className = 'q-header';
            header.innerHTML = `${q.type === 'mcq' ? '📌 سؤال ' + (i+1) : (q.type === 'tf' ? '✅❌ سؤال ' + (i+1) : '📝 سؤال ' + (i+1))}`;
            card.appendChild(header);

            const body = document.createElement('div');
            body.className = 'q-body';

            const textDiv = document.createElement('div');
            textDiv.className = 'question-text';
            textDiv.innerText = q.text;
            body.appendChild(textDiv);

            if (q.type === 'mcq') {
                const optionsDiv = document.createElement('div');
                optionsDiv.className = 'options';
                const letters = ['أ', 'ب', 'ج', 'د'];
                for (let optIdx = 0; optIdx < q.options.length; optIdx++) {
                    const optDiv = document.createElement('div');
                    optDiv.className = 'option';
                    const letterSpan = document.createElement('span');
                    letterSpan.className = 'opt-letter';
                    letterSpan.innerText = letters[optIdx];
                    const textSpan = document.createElement('span');
                    textSpan.innerText = q.options[optIdx];
                    optDiv.appendChild(letterSpan);
                    optDiv.appendChild(textSpan);
                    optDiv.onclick = (function(qid, selected, correctIdx, expl) {
                        return function() {
                            const parentCard = document.querySelector(`.question-card[data-qid='${qid}']`);
                            let oldFeedback = parentCard.querySelector('.feedback');
                            if (oldFeedback) oldFeedback.remove();
                            const feedback = document.createElement('div');
                            feedback.className = 'feedback';
                            const correctLetter = String.fromCharCode(65 + correctIdx);
                            const correctText = q.options[correctIdx];
                            if (selected === correctIdx) {
                                feedback.classList.add('correct');
                                feedback.innerHTML = `✅ <strong>صحيح!</strong> ${expl}`;
                            } else {
                                feedback.classList.add('wrong');
                                feedback.innerHTML = `❌ <strong>خطأ.</strong> الإجابة الصحيحة: ${correctText}.<br> 📖 ${expl}`;
                            }
                            parentCard.querySelector('.q-body').appendChild(feedback);
                            feedback.style.display = 'block';
                        };
                    })(i, optIdx, q.correct, q.explanation);
                    optionsDiv.appendChild(optDiv);
                }
                body.appendChild(optionsDiv);
            } 
            else if (q.type === 'tf') {
                const optionsDiv = document.createElement('div');
                optionsDiv.className = 'options';
                const optTrue = document.createElement('div');
                optTrue.className = 'option';
                optTrue.innerHTML = '<span class="opt-letter">أ</span> <span>صح (✓)</span>';
                const optFalse = document.createElement('div');
                optFalse.className = 'option';
                optFalse.innerHTML = '<span class="opt-letter">ب</span> <span>خطأ (✗)</span>';
                optTrue.onclick = (function(qid, selectedVal, correctVal, expl) {
                    return function() {
                        const parentCard = document.querySelector(`.question-card[data-qid='${qid}']`);
                        let oldFeedback = parentCard.querySelector('.feedback');
                        if (oldFeedback) oldFeedback.remove();
                        const feedback = document.createElement('div');
                        feedback.className = 'feedback';
                        if (selectedVal === correctVal) {
                            feedback.classList.add('correct');
                            feedback.innerHTML = `✅ <strong>صحيح!</strong> ${expl}`;
                        } else {
                            feedback.classList.add('wrong');
                            feedback.innerHTML = `❌ <strong>خطأ.</strong> الإجابة الصحيحة هي: ${correctVal ? 'صح (✓)' : 'خطأ (✗)'}.<br> 📖 ${expl}`;
                        }
                        parentCard.querySelector('.q-body').appendChild(feedback);
                        feedback.style.display = 'block';
                    };
                })(i, true, q.correct, q.explanation);
                optFalse.onclick = (function(qid, selectedVal, correctVal, expl) {
                    return function() {
                        const parentCard = document.querySelector(`.question-card[data-qid='${qid}']`);
                        let oldFeedback = parentCard.querySelector('.feedback');
                        if (oldFeedback) oldFeedback.remove();
                        const feedback = document.createElement('div');
                        feedback.className = 'feedback';
                        if (selectedVal === correctVal) {
                            feedback.classList.add('correct');
                            feedback.innerHTML = `✅ <strong>صحيح!</strong> ${expl}`;
                        } else {
                            feedback.classList.add('wrong');
                            feedback.innerHTML = `❌ <strong>خطأ.</strong> الإجابة الصحيحة هي: ${correctVal ? 'صح (✓)' : 'خطأ (✗)'}.<br> 📖 ${expl}`;
                        }
                        parentCard.querySelector('.q-body').appendChild(feedback);
                        feedback.style.display = 'block';
                    };
                })(i, false, q.correct, q.explanation);
                optionsDiv.appendChild(optTrue);
                optionsDiv.appendChild(optFalse);
                body.appendChild(optionsDiv);
            }

            card.appendChild(body);
            container.appendChild(card);
        }

        // Add essay questions separately
        const essayQuestions = [
            { text: "1. اشرح بالتفصيل الأهمية الجيولوجية للأوستراكودا.", answer: "للأوستراكودا أهمية جيولوجية كبرى: (1) تعتبر أحفوريات مرشدة مهمة خاصة في حقب الحياة القديمة حيث الفورامينيفرا قليلة، وفي حقبي المتوسطة والحديثة. (2) تأتي في المرتبة الثانية بعد الفورامينيفرا الطافية في عمليات المضاهاة (Correlation). (3) تستخدم في تحديد المناخ القديم والملوحة القديمة من خلال شكل وسمك الدرقة. (4) تساعد في قياس معدل الترسيب: انفصال المصراعين يدل على ترسيب بطيء، وتلازمهما يدل على ترسيب سريع." },
            { text: "2. قارن بين أوستراكودا المياه العذبة وأوستراكودا المياه المالحة من حيث شكل الدرقة والزخرفة والمفصلة.", answer: "المياه العذبة: درقة رقيقة، ملساء، بسيطة، مفصلة بسيطة (مثل جنس Cypris). المياه المالحة: درقة سميكة، زخرفة واضحة ومعقدة، قنوات حافية متشعبة، بقع عينية بارزة، مفصلة Amphidont أو Merodont متطورة." },
            { text: "3. اشرح كيف يؤثر العمق على توزيع وخصائص الأوستراكودا.", answer: "الرف القاري (0-200م): درقة سميكة، زخرفة خشنة، مفصلة مركبة (مثل Quadracythere). أعماق Bathyal (200-2000م): درقة طويلة، مفصلة أولية (مثل Krithe). مناطق Abyssal (>2000م): قلة عدد الأنواع، درقة شفافة رقيقة (مثل Macrocypris)." },
            { text: "4. اشرح أنواع المفصلات (Hinge) في الأوستراكودا بالتفصيل.", answer: "(1) Adont hinge: مفصلة عديمة الأسنان، بسيطة، تتكون من حز وحافة، توجد في رتبة Podocopida. (2) Merodont hinge: تتكون من ثلاثة أجزاء (أمامي، أوسط، خلفي)، الجزء الأوسط به بروزات. (3) Amphidont hinge: تطور من Merodont بتقسيم الجزء الأوسط إلى جزأين (أمام أوسط وخلف أوسط)، أكثر تعقيداً وتوجد في العائلات البحرية." },
            { text: "5. كيف يمكن استخدام الأوستراكودا في تحديد معدل الترسيب في البيئات القديمة؟", answer: "عندما يموت الكائن، إذا كان معدل الترسيب بطيئاً، تنفصل المصراعين عن بعضهما. أما إذا كان معدل الترسيب سريعاً، فإن الأفراد تدفن سريعاً قبل أن تنفصل المصراعين، فتبقى ملتصقتين في السجل الأحفوري. لذلك، وجود المصراعين متلازمين يشير إلى ترسيب سريع، ووجودهما منفصلين يشير إلى ترسيب بطيء." },
            { text: "6. اذكر الأسس التي يعتمد عليها التصنيف الحديث للأوستراكودا حسب سكوت (Scott, 1951) والتطورات اللاحقة.", answer: "أسس سكوت: الشكل العام للدرقة، الزخرفة، المفصلة، التراكب (overlap)، البقع العينية. التصنيف الحديث أضاف: شكل وتوزيع آثار العضلات (Muscle scars) وتركيب المفصلة بالتفصيل، وخصائص المنطقة الهامشية والثقوب العادية والحافية." },
            { text: "7. اشرح العلاقة بين طبيعة القاع (substrate) وشكل درقة الأوستراكودا حسب ماركوفين (1962).", answer: "فوق النباتات البحرية: درقة رقيقة، أملسة، خالية من الزخرفة، شكل طويل مضغوط. الأنواع الحافرة (Burrowing): درقة جيرية قوية. الأنواع الزاحفة (Crawling): السطح السفلي للدرقة مستوٍ. القيعان الرملية: درقة قصيرة، زخرفة خشنة. القيعان الطينية (المياه العذبة): زخرفة ملساء." },
            { text: "8. ناقش دور الأوستراكودا في تحديد الملوحة القديمة (Paleosalinity) والمناخ القديم (Paleoclimate).", answer: "الملوحة القديمة: المياه العذبة تعطي درقة رقيقة ملساء، والمياه المالحة تعطي زخرفة واضحة وقنوات حافية، والمياه المختلطة تعطي درقة سميكة ومفصلة Amphidont. المناخ القديم: تفضل الأوستراكودا المياه الدافئة (زيادة سرعة النمو)، واتجاه اللف في بعض الأنواع ارتبط بدرجة الحرارة، كما تستخدم في تحديد الفترات الجليدية." },
            { text: "9. اشرح التطور التاريخي للأوستراكودا خلال حقب الحياة المتوسطة والحديثة.", answer: "حقب المتوسطة: في الترياسي استمرت Podocopida، وفي الجوراسي والطباشيري ظهرت Platycopina وكان لها دور في التقسيم الطبقى الحياتي والبيئة القديمة. بنهاية الطباشيري حدث تراجع بسبب تغير السحنات. حقب الحديثة: تطور كبير وبلغت أقصى تنوع وانتشار لها خاصة خلال عصر البليستوسين (Pleistocene)." },
            { text: "10. اذكر رتب (Orders) الأوستراكودا المختلفة مع وصف مختصر لكل رتبة.", answer: "(1) Archaeopoda: رتبة بدائية منقرضة. (2) Leperditicopa: رتبة قديمة. (3) Paleocopida: رتبة منقرضة من حقب الحياة القديمة. (4) Myodocopida: تضم أنواعاً هائمة (pelagic) ذات درقة رقيقة. (5) Podocopida: أكبر الرتب وتضم معظم الأنواع الحديثة والقاعية." }
        ];

        for (let i = 0; i < essayQuestions.length; i++) {
            const eq = essayQuestions[i];
            const card = document.createElement('div');
            card.className = 'question-card';
            const header = document.createElement('div');
            header.className = 'q-header';
            header.innerHTML = `📝 سؤال مقالي ${i+1}`;
            card.appendChild(header);
            const body = document.createElement('div');
            body.className = 'q-body';
            const textDiv = document.createElement('div');
            textDiv.className = 'question-text';
            textDiv.innerText = eq.text;
            body.appendChild(textDiv);
            
            const showBtn = document.createElement('div');
            showBtn.style.cssText = 'background: #c4a35a; color: white; padding: 10px 18px; border-radius: 30px; cursor: pointer; display: inline-block; margin-top: 10px; font-weight: bold; text-align: center; width: fit-content;';
            showBtn.innerText = '📖 عرض الإجابة النموذجية';
            const answerDiv = document.createElement('div');
            answerDiv.className = 'feedback';
            answerDiv.style.display = 'none';
            answerDiv.style.background = '#f0f4f0';
            answerDiv.style.color = '#1a4a2a';
            answerDiv.innerHTML = `<strong>الإجابة النموذجية:</strong><br>${eq.answer}`;
            
            showBtn.onclick = () => {
                if (answerDiv.style.display === 'none') {
                    answerDiv.style.display = 'block';
                    showBtn.innerText = '📖 إخفاء الإجابة';
                } else {
                    answerDiv.style.display = 'none';
                    showBtn.innerText = '📖 عرض الإجابة النموذجية';
                }
            };
            
            body.appendChild(showBtn);
            body.appendChild(answerDiv);
            card.appendChild(body);
            container.appendChild(card);
        }
    }

    buildUI();
</script>
</body>
</html>
