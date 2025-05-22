# green

<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>綠行星人格測驗 | Green Galaxy Personality Quiz</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', '微軟正黑體', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            color: white;
            padding: 40px 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .content {
            padding: 40px 30px;
        }

        .welcome-screen, .quiz-screen, .result-screen {
            display: none;
        }

        .welcome-screen.active, .quiz-screen.active, .result-screen.active {
            display: block;
        }

        .welcome-text {
            text-align: center;
            font-size: 1.1em;
            line-height: 1.6;
            color: #666;
            margin-bottom: 30px;
        }

        .start-btn {
            display: block;
            width: 200px;
            margin: 0 auto;
            padding: 15px 30px;
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 1.2em;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .start-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(78, 205, 196, 0.4);
        }

        .question-container {
            margin-bottom: 30px;
        }

        .question {
            font-size: 1.3em;
            color: #333;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .question-number {
            color: #4ecdc4;
            font-size: 0.9em;
            margin-bottom: 10px;
        }

        .options {
            display: grid;
            gap: 15px;
        }

        .option {
            background: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 15px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .option:hover {
            border-color: #4ecdc4;
            background: #f0fdfc;
            transform: translateX(5px);
        }

        .option.selected {
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            color: white;
            border-color: #44a08d;
        }

        .option-letter {
            font-weight: bold;
            margin-right: 10px;
            font-size: 1.1em;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e9ecef;
            border-radius: 4px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress {
            height: 100%;
            background: linear-gradient(90deg, #4ecdc4 0%, #44a08d 100%);
            transition: width 0.5s ease;
            border-radius: 4px;
        }

        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s ease;
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-primary {
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            color: white;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .result-card {
            text-align: center;
            padding: 30px;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
            border-radius: 20px;
            margin-bottom: 30px;
        }

        .result-emoji {
            font-size: 4em;
            margin-bottom: 20px;
        }

        .result-title {
            font-size: 2em;
            color: #333;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .result-description {
            font-size: 1.2em;
            color: #666;
            line-height: 1.6;
        }

        .score-display {
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
        }

        .score-text {
            font-size: 1.3em;
            font-weight: bold;
        }

        .restart-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .restart-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.4);
        }

        @media (max-width: 768px) {
            .container {
                margin: 10px;
                border-radius: 15px;
            }
            
            .header {
                padding: 30px 20px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .content {
                padding: 30px 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🌍 綠行星人格測驗</h1>
            <p>Green Galaxy Personality Quiz</p>
        </div>
        
        <div class="content">
            <!-- 歡迎畫面 -->
            <div class="welcome-screen active">
                <div class="welcome-text">
                    <h2 style="color: #4ecdc4; margin-bottom: 20px;">歡迎來到綠行星！</h2>
                    <p>你是哪種環保人格呢？透過這個簡單的測驗，我們將分析你的綠色生活指數，並為你量身打造專屬的環保人格類型。</p>
                    <br>
                    <p>測驗只需要 1 分鐘，共 5 個問題。讓我們一起探索你內心的綠色潛能吧！</p>
                </div>
                <button class="start-btn" onclick="startQuiz()">🚀 開始測驗</button>
            </div>

            <!-- 測驗畫面 -->
            <div class="quiz-screen">
                <div class="question-number">問題 <span id="current-question">1</span> / 5</div>
                <div class="progress-bar">
                    <div class="progress" id="progress-bar"></div>
                </div>
                
                <div class="question-container">
                    <div class="question" id="question-text"></div>
                    <div class="options" id="options-container"></div>
                </div>

                <div class="nav-buttons">
                    <button class="btn btn-secondary" id="prev-btn" onclick="previousQuestion()" disabled>上一題</button>
                    <button class="btn btn-primary" id="next-btn" onclick="nextQuestion()" disabled>下一題</button>
                </div>
            </div>

            <!-- 結果畫面 -->
            <div class="result-screen">
                <div class="score-display">
                    <div class="score-text">你的綠色指數：<span id="total-score">0</span> / 15</div>
                </div>
                
                <div class="result-card">
                    <div class="result-emoji" id="result-emoji"></div>
                    <div class="result-title" id="result-title"></div>
                    <div class="result-description" id="result-description"></div>
                </div>

                <button class="restart-btn" onclick="restartQuiz()">🔄 重新測驗</button>
            </div>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "你今天喝飲料，會選擇哪種方式？",
                options: [
                    { text: "自備環保杯", score: 3 },
                    { text: "自備環保杯但使用塑膠吸管", score: 2 },
                    { text: "使用塑膠杯自備環保吸管", score: 1 },
                    { text: "使用店]家提供的塑膠杯及吸管", score: 0 }
                ]
            },
            {
                question: "假日你最常的交通工具？",
                options: [
                    { text: "走路或騎腳踏車", score: 3 },
                    { text: "搭乘大眾運輸", score: 2 },
                    { text: "開車", score: 1 },
                    { text: "騎車", score: 1 },
                   
                ]
            },
            {
                question: "用餐時你會？",
                options: [
                    { text: "自備餐具", score: 3 },
                    { text: "使用可分解餐具", score: 2 },
                    { text: "使用一次性塑膠餐具", score: 1 },
                    { text: "不在意", score: 0 }
                ]
            },
            {
                question: "你在購物時會選擇？",
                options: [
                    { text: "環保標章的產品", score: 3 },
                    { text: "環保材質包裝", score: 2 },
                    { text: "平價商品", score: 1 },
                    { text: "只看包裝", score: 0 }
                ]
            },
            {
                question: "你對低碳經濟的看法？",
                options: [
                    { text: "我積極實踐中！", score: 3 },
                    { text: "我開始學習", score: 2 },
                    { text: "有興趣還沒開始", score: 1 },
                    { text: "沒聽過/不太懂", score: 0 }
                ]
            }
        ];

        const personalityTypes = {
            warrior: {
                emoji: "🌿",
                title: "綠色鬥士型 (Green Warrior)",
                description: "你是環保界的行動派，每個生活細節都在實踐永續。你不只是說說而已，而是真正的綠色生活實踐者！",
                range: [13, 15]
            },
            everyday: {
                emoji: "🌱",
                title: "日常實踐者型 (Eco Everydayist)",
                description: "你穩定地做著力所能及的綠色選擇。雖然不是最極端的環保主義者，但你的日常行為已經為地球做出了實質貢獻！",
                range: [10, 12]
            },
            explorer: {
                emoji: "🌤",
                title: "潛力型綠人 (Sustainability Explorer)",
                description: "你對永續有興趣，但生活中還有提升空間。你已經踏出了第一步，繼續保持這份好奇心和行動力！",
                range: [6, 9]
            },
            watcher: {
                emoji: "🪐",
                title: "冷感觀察者型 (Eco Watcher)",
                description: "你可能對環保話題還不太關心，但今天是一個很好的開始！每個人都可以從小地方開始為地球盡一份心力。",
                range: [0, 5]
            }
        };

        let currentQuestion = 0;
        let answers = [];
        let totalScore = 0;

        function startQuiz() {
            document.querySelector('.welcome-screen').classList.remove('active');
            document.querySelector('.quiz-screen').classList.add('active');
            showQuestion();
        }

        function showQuestion() {
            const question = questions[currentQuestion];
            document.getElementById('current-question').textContent = currentQuestion + 1;
            document.getElementById('question-text').textContent = question.question;
            
            const optionsContainer = document.getElementById('options-container');
            optionsContainer.innerHTML = '';
            
            question.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.className = 'option';
                optionElement.innerHTML = `
                    <span class="option-letter">${String.fromCharCode(65 + index)}.</span>
                    ${option.text}
                `;
                optionElement.onclick = () => selectOption(index, optionElement);
                optionsContainer.appendChild(optionElement);
            });

            // 如果已經有答案，恢復選擇狀態
            if (answers[currentQuestion] !== undefined) {
                const optionElements = document.querySelectorAll('.option');
                optionElements[answers[currentQuestion]].classList.add('selected');
            }

            updateProgress();
            updateNavigationButtons();
        }

        function selectOption(optionIndex, element) {
            // 移除其他選項的選中狀態
            document.querySelectorAll('.option').forEach(opt => opt.classList.remove('selected'));
            element.classList.add('selected');
            
            answers[currentQuestion] = optionIndex;
            document.getElementById('next-btn').disabled = false;
        }

        function nextQuestion() {
            if (answers[currentQuestion] === undefined) {
                return; // 確保已選擇答案
            }
            
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                showQuestion();
            } else {
                showResult();
            }
        }

        function previousQuestion() {
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion();
            }
        }

        function updateProgress() {
            const progress = ((currentQuestion + 1) / questions.length) * 100;
            document.getElementById('progress-bar').style.width = progress + '%';
        }

        function updateNavigationButtons() {
            document.getElementById('prev-btn').disabled = currentQuestion === 0;
            document.getElementById('next-btn').disabled = answers[currentQuestion] === undefined;
            
            if (currentQuestion === questions.length - 1) {
                document.getElementById('next-btn').textContent = '查看結果';
            } else {
                document.getElementById('next-btn').textContent = '下一題';
            }
        }

        function calculateScore() {
            totalScore = 0;
            for (let i = 0; i < answers.length; i++) {
                if (answers[i] !== undefined) {
                    totalScore += questions[i].options[answers[i]].score;
                }
            }
            console.log('計算分數:', totalScore, '答案陣列:', answers); // 除錯用
        }

        function getPersonalityType(score) {
            for (let type in personalityTypes) {
                const range = personalityTypes[type].range;
                if (score >= range[0] && score <= range[1]) {
                    return personalityTypes[type];
                }
            }
        }

        function showResult() {
            calculateScore();
            const personalityType = getPersonalityType(totalScore);
            
            console.log('顯示結果 - 總分:', totalScore, '人格類型:', personalityType); // 除錯用
            
            document.querySelector('.quiz-screen').classList.remove('active');
            document.querySelector('.result-screen').classList.add('active');
            
            document.getElementById('total-score').textContent = totalScore;
            document.getElementById('result-emoji').textContent = personalityType.emoji;
            document.getElementById('result-title').textContent = personalityType.title;
            document.getElementById('result-description').textContent = personalityType.description;
        }

        function restartQuiz() {
            currentQuestion = 0;
            answers = [];
            totalScore = 0;
            
            document.querySelector('.result-screen').classList.remove('active');
            document.querySelector('.welcome-screen').classList.add('active');
        }
    </script>
</body>
</html>
