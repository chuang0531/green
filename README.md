<!DOCTYPE html>
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

        .action-buttons {
            display: flex;
            flex-direction: column;
            gap: 15px;
            align-items: center;
        }

        .share-btn, .subscribe-btn {
            background: linear-gradient(135deg, #4ecdc4 0%, #44a08d 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 280px;
            max-width: 100%;
        }

        .share-btn:hover, .subscribe-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(78, 205, 196, 0.4);
        }

        .subscribe-btn {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        .subscribe-btn:hover {
            box-shadow: 0 10px 20px rgba(245, 87, 108, 0.4);
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
            width: 280px;
            max-width: 100%;
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

                <div class="action-buttons">
                    <button class="share-btn" onclick="shareResult()">📤 分享結果</button>
                    <button class="subscribe-btn" onclick="subscribeNewsletter()">📧 訂閱綠色電子期刊</button>
                    <button class="restart-btn" onclick="restartQuiz()">🔄 重新測驗</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        const questions = [
            {
                question: "平時喝飲料，你習慣選擇哪種方式？",
                options: [
                    { text: "自備環保杯", score: 3 },
                    { text: "自備環保杯但使用塑膠吸管", score: 2 },
                    { text: "使用塑膠杯自備環保吸管", score: 1 },
                    { text: "使用點家提供的塑膠杯及吸管", score: 0 }
                ]
            },
            {
                question: "日常生活中，你最常的交通工具？",
                options: [
                    { text: "騎腳踏車或走路", score: 3 },
                    { text: "搭乘大眾運輸", score: 2 },
                    { text: "開車", score: 1 },
                    { text: "騎機車", score: 0 }
                ]
            },
            {
                question: "用餐時你會選擇？",
                options: [
                    { text: "自備環保餐具", score: 3 },
                    { text: "使用可分解材質的餐具", score: 2 },
                    { text: "使用一次性塑膠餐具", score: 1 },
                    { text: "沒有注意", score: 0 }
                ]
            },
            {
                question: "你在購物時會選擇什麼樣的產品？",
                options: [
                    { text: "環保標章的產品", score: 3 },
                    { text: "環保材質包裝的產品", score: 2 },
                    { text: "CP值高的產品", score: 1 },
                    { text: "只選擇包裝美觀的產品", score: 0 }
                ]
            },
            {
                question: "你對低碳經濟的看法？",
                options: [
                    { text: "積極實踐中！", score: 3 },
                    { text: "開始學習", score: 2 },
                    { text: "有興趣還沒開始", score: 1 },
                    { text: "沒聽過/不太懂", score: 0 }
                ]
                
            }
        ];

        const personalityTypes = {
            warrior: {
                emoji: "🌿",
                title: "綠色鬥士型 (Green Warrior)",
                description: "你是環保界的行動派，每個生活細節都在實踐永續。你不只是說說而已，而是真正的綠色生活實踐者！✔ 你超棒的！可再進一步挑戰：減塑生活、參加淨灘或氣候倡議活動，影響更多人一起加入！",
                range: [13, 15]
            },
            everyday: {
                emoji: "🌱",
                title: "日常實踐者型 (Eco Everydayist)",
                description: "你穩定地做著力所能及的綠色選擇。雖然不是最極端的環保主義者，但你的日常行為已經為地球做出了實質貢獻！✔ 很好喔~可再進一步：記錄自己的低碳行為，設定一週一個新挑戰，例如：一週無外帶餐盒！",

                range: [10, 12]
            },
            explorer: {
                emoji: "🌤",
                title: "潛力型綠人 (Sustainability Explorer)",
                description: "你對永續有興趣，但生活中還有提升空間。你已經踏出了第一步，繼續保持這份好奇心和行動力！✔相信你可以的，試著從日常做起：開始自備環保杯、餐具，或試著搭大眾運輸一天看看，你會發現綠色其實不難！",
                range: [6, 9]
            },
            watcher: {
                emoji: "🪐",
                title: "冷感觀察者型 (Eco Watcher)",
                description: "你可能對環保話題還不太關心，但今天是一個很好的開始！每個人都可以從小地方開始為地球盡一份心力。✔ ㄧ現在開始也不晚！從一個小動作開始：少用一根吸管、多關一次電燈，或看看朋友都在怎麼做，讓綠色不再遙遠！",
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

        function shareResult() {
            const personalityType = getPersonalityType(totalScore);
            const shareText = `🌍 我剛完成了綠行星人格測驗！\n\n我的結果是：${personalityType.emoji} ${personalityType.title}\n綠色指數：${totalScore}/15\n\n${personalityType.description}\n\n你也來測測看你是哪種環保人格吧！`;
            
            // 檢查是否支援 Web Share API
            if (navigator.share) {
                navigator.share({
                    title: '綠行星人格測驗結果',
                    text: shareText,
                    url: window.location.href
                }).then(() => {
                    console.log('分享成功！');
                }).catch((error) => {
                    console.log('分享取消或失敗：', error);
                });
            } else {
                // 備用方案：複製到剪貼簿
                if (navigator.clipboard) {
                    navigator.clipboard.writeText(shareText).then(() => {
                        alert('✅ 結果已複製到剪貼簿！\n你可以貼到社群媒體分享給朋友。');
                    }).catch(() => {
                        // 如果剪貼簿 API 也不支援，顯示文字讓用戶手動複製
                        showShareModal(shareText);
                    });
                } else {
                    showShareModal(shareText);
                }
            }
        }

        function showShareModal(text) {
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0,0,0,0.8);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 1000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: white;
                padding: 30px;
                border-radius: 15px;
                max-width: 500px;
                width: 90%;
                max-height: 80%;
                overflow-y: auto;
            `;
            
            content.innerHTML = `
                <h3 style="margin-bottom: 15px; color: #333;">📤 分享你的測驗結果</h3>
                <textarea readonly style="width: 100%; height: 200px; padding: 10px; border: 2px solid #4ecdc4; border-radius: 10px; font-family: inherit; resize: none;">${text}</textarea>
                <div style="margin-top: 15px; text-align: center;">
                    <button onclick="this.parentElement.parentElement.parentElement.remove()" style="background: #4ecdc4; color: white; border: none; padding: 10px 20px; border-radius: 20px; cursor: pointer;">關閉</button>
                </div>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            // 點擊背景關閉
            modal.onclick = (e) => {
                if (e.target === modal) {
                    modal.remove();
                }
            };
        }

        function subscribeNewsletter() {
            const modal = document.createElement('div');
            modal.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0,0,0,0.8);
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 1000;
            `;
            
            const content = document.createElement('div');
            content.style.cssText = `
                background: white;
                padding: 40px;
                border-radius: 20px;
                max-width: 500px;
                width: 90%;
                text-align: center;
            `;
            
            content.innerHTML = `
                <div style="font-size: 3em; margin-bottom: 20px;">🌱</div>
                <h3 style="color: #4ecdc4; margin-bottom: 15px;">訂閱綠色電子期刊</h3>
                <p style="color: #666; margin-bottom: 25px; line-height: 1.6;">
                    獲取最新的環保資訊、永續生活小秘訣，以及專屬的綠色生活指南！
                </p>
                <form id="newsletter-form" style="margin-bottom: 20px;">
                    <input type="email" placeholder="請輸入您的電子信箱" required 
                           style="width: 100%; padding: 15px; border: 2px solid #e9ecef; border-radius: 25px; margin-bottom: 15px; font-size: 1em; box-sizing: border-box;">
                    <button type="submit" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; border: none; padding: 15px 30px; border-radius: 25px; font-size: 1.1em; cursor: pointer; width: 100%; transition: all 0.3s ease;">
                        🚀 立即訂閱
                    </button>
                </form>
                <button onclick="this.parentElement.parentElement.remove()" 
                        style="background: #6c757d; color: white; border: none; padding: 10px 20px; border-radius: 20px; cursor: pointer;">
                    稍後再說
                </button>
            `;
            
            modal.appendChild(content);
            document.body.appendChild(modal);
            
            // 處理表單提交
            document.getElementById('newsletter-form').onsubmit = (e) => {
                e.preventDefault();
                const email = e.target.querySelector('input[type="email"]').value;
                
                // 這裡可以串接真實的電子報訂閱 API
                setTimeout(() => {
                    content.innerHTML = `
                        <div style="font-size: 3em; margin-bottom: 20px;">✅</div>
                        <h3 style="color: #4ecdc4; margin-bottom: 15px;">訂閱成功！</h3>
                        <p style="color: #666; margin-bottom: 25px;">
                            感謝您的訂閱！我們已將確認信寄到 <strong>${email}</strong><br>
                            請查看您的信箱並點擊確認連結。
                        </p>
                        <button onclick="this.parentElement.parentElement.remove()" 
                                style="background: #4ecdc4; color: white; border: none; padding: 15px 30px; border-radius: 25px; cursor: pointer;">
                            太棒了！
                        </button>
                    `;
                }, 1000);
            };
            
            // 點擊背景關閉
            modal.onclick = (e) => {
                if (e.target === modal) {
                    modal.remove();
                }
            };
        }
    </script>
</body>
</html>
