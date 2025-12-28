<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Викторина про Юру</title>
    <style>
        /* Основные стили остаются такими же */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #1a1a2e;
            color: #e6e6e6;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 800px;
            background-color: #16213e;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            overflow: hidden;
            border: 1px solid #2d4059;
        }
        
        .header {
            background-color: #0f3460;
            padding: 20px;
            text-align: center;
            border-bottom: 1px solid #2d4059;
        }
        
        h1 {
            color: #e94560;
            font-size: 2.2rem;
            margin-bottom: 5px;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .subtitle {
            color: #8ac6d1;
            font-size: 1rem;
            letter-spacing: 1px;
        }
        
        .content {
            padding: 30px;
            min-height: 400px;
        }
        
        .menu-screen, .question-screen, .result-screen {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
        }
        
        .hidden {
            display: none !important;
        }
        
        .menu-title {
            font-size: 1.8rem;
            margin-bottom: 30px;
            color: #e94560;
        }
        
        .menu-options {
            width: 100%;
            max-width: 300px;
        }
        
        .btn {
            display: block;
            width: 100%;
            padding: 15px;
            margin: 15px 0;
            background-color: #0f3460;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid #2d4059;
        }
        
        .btn:hover {
            background-color: #e94560;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .question-counter {
            color: #8ac6d1;
            font-size: 1.1rem;
            margin-bottom: 10px;
            text-align: left;
            width: 100%;
        }
        
        .question-text {
            font-size: 1.5rem;
            margin-bottom: 25px;
            color: #f1f1f1;
            width: 100%;
            text-align: left;
        }
        
        .answers {
            width: 100%;
        }
        
        .answer-option {
            display: block;
            width: 100%;
            padding: 15px;
            margin: 10px 0;
            text-align: left;
            background-color: #1a1a2e;
            border: 1px solid #2d4059;
            border-radius: 8px;
            color: #e6e6e6;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }
        
        .answer-option:hover {
            background-color: #2d4059;
            transform: translateX(5px);
        }
        
        .answer-option.selected {
            border-color: #e94560;
            background-color: rgba(233, 69, 96, 0.1);
        }
        
        .answer-option.correct {
            border-color: #4CAF50;
            background-color: rgba(76, 175, 80, 0.1);
        }
        
        .answer-option.incorrect {
            border-color: #f44336;
            background-color: rgba(244, 67, 54, 0.1);
        }
        
        .feedback {
            margin-top: 20px;
            padding: 10px 15px;
            border-radius: 8px;
            font-weight: bold;
            width: 100%;
        }
        
        .feedback.correct {
            background-color: rgba(76, 175, 80, 0.1);
            color: #4CAF50;
            border: 1px solid #4CAF50;
        }
        
        .feedback.incorrect {
            background-color: rgba(244, 67, 54, 0.1);
            color: #f44336;
            border: 1px solid #f44336;
        }
        
        .next-btn {
            margin-top: 20px;
            width: 200px;
        }
        
        .result-title {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: #e94560;
        }
        
        .score {
            font-size: 1.3rem;
            margin-bottom: 30px;
            color: #8ac6d1;
        }
        
        .hearts {
            font-size: 3rem;
            color: #e94560;
            margin-bottom: 30px;
            letter-spacing: 10px;
        }
        
        .final-message {
            margin-bottom: 30px;
            font-size: 1.2rem;
            line-height: 1.5;
        }
        
        .footer {
            background-color: #0f3460;
            padding: 15px;
            text-align: center;
            border-top: 1px solid #2d4059;
            color: #8ac6d1;
            font-size: 0.9rem;
        }
        
        .footer span {
            color: #e94560;
            font-weight: bold;
        }
        
        .loading {
            text-align: center;
            padding: 20px;
        }
        
        @media (max-width: 600px) {
            .content {
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .question-text {
                font-size: 1.3rem;
            }
            
            .answer-option {
                padding: 12px;
                font-size: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>▎Викторина про Юру</h1>
            <div class="subtitle">Проверьте свои знания о легендарном Юре</div>
        </div>
        
        <div class="content">
            <!-- Экран меню -->
            <div id="menuScreen" class="menu-screen hidden">
                <h2 class="menu-title">Меню:</h2>
                <div class="menu-options">
                    <button id="startGame" class="btn">1. Начать игру</button>
                    <button id="exitGame" class="btn">2. Выход</button>
                </div>
            </div>
            
            <!-- Экран вопросов -->
            <div id="questionScreen" class="question-screen hidden">
                <div class="question-counter" id="questionCounter">Вопрос 1 из 5</div>
                <div class="question-text" id="questionText">Кто Юра?</div>
                
                <div class="answers" id="answersContainer">
                    <!-- Варианты ответов будут добавлены динамически -->
                </div>
                
                <div class="feedback" id="feedback"></div>
                
                <button id="nextQuestion" class="btn next-btn hidden">Следующий вопрос</button>
            </div>
            
            <!-- Экран результатов -->
            <div id="resultScreen" class="result-screen hidden">
                <h2 class="result-title">▎Результаты:</h2>
                <div class="score" id="scoreText">Вы ответили правильно на 0 из 5 вопросов</div>
                
                <div id="heartsContainer" class="hearts"></div>
                
                <div class="final-message" id="finalMessage"></div>
                
                <button id="restartGame" class="btn">Сыграть еще раз</button>
            </div>
            
            <!-- Сообщение о загрузке -->
            <div id="loadingScreen" class="loading">
                <h2>Загрузка викторины...</h2>
                <p>Если викторина не загружается, попробуйте:</p>
                <ol style="text-align: left; margin: 20px auto; max-width: 400px;">
                    <li>Разрешить JavaScript в браузере</li>
                    <li>Использовать современный браузер (Chrome, Firefox, Edge)</li>
                    <li>Открыть файл через локальный сервер или двойной клик</li>
                </ol>
            </div>
        </div>
        
        <div class="footer">
            <p>scripts: <span>Taimarka</span> | Design: <span>Gagaofe</span></p>
        </div>
    </div>

    <script>
        // УПРОЩЕННАЯ ВЕРСИЯ ДЛЯ РАБОТЫ ИЗ ФАЙЛА
        
        // Данные викторины
        const quizData = [
            {
                question: "Кто Юра?",
                answers: [
                    { text: "Физик", correct: true, note: "Правильно" },
                    { text: "Доксер", correct: false, note: "Неправильно" }
                ]
            },
            {
                question: "Кого любит Юра?",
                answers: [
                    { text: "Софу", correct: false, note: "Неправильно" },
                    { text: "Он сигмо", correct: true, note: "Правильно" }
                ]
            },
            {
                question: "Кто он в киберспорте?",
                answers: [
                    { text: "Деко", correct: true, note: "Правильно" },
                    { text: "Донк", correct: false, note: "Неправильно" },
                    { text: "Саша Симл", correct: false, note: "Неправильно" }
                ]
            },
            {
                question: "Сколько ему лет?",
                answers: [
                    { text: "1488", correct: false, note: "Неправильно" },
                    { text: "1295", correct: true, note: "Правильно" },
                    { text: "14", correct: false, note: "Неправильно" }
                ]
            },
            {
                question: "Где живет Юра?",
                answers: [
                    { text: "В США", correct: false, note: "Неправильно" },
                    { text: "В России", correct: false, note: "Неправильно" },
                    { text: "В СССР", correct: true, note: "Правильно" }
                ]
            }
        ];

        // ОЧЕНЬ ПРОСТОЙ КОД БЕЗ СЛОЖНЫХ ФУНКЦИЙ
        let currentQuestion = 0;
        let score = 0;
        
        // Показываем меню сразу
        document.getElementById('loadingScreen').classList.add('hidden');
        document.getElementById('menuScreen').classList.remove('hidden');
        
        // Функция для начала игры
        function startGame() {
            currentQuestion = 0;
            score = 0;
            document.getElementById('menuScreen').classList.add('hidden');
            document.getElementById('questionScreen').classList.remove('hidden');
            showQuestion();
        }
        
        // Функция для выхода
        function exitGame() {
            alert("Спасибо за игру! До свидания!");
        }
        
        // Функция показа вопроса
        function showQuestion() {
            const question = quizData[currentQuestion];
            
            // Обновляем текст
            document.getElementById('questionCounter').textContent = `Вопрос ${currentQuestion + 1} из ${quizData.length}`;
            document.getElementById('questionText').textContent = `▎${question.question}`;
            
            // Очищаем контейнер ответов
            const answersContainer = document.getElementById('answersContainer');
            answersContainer.innerHTML = '';
            
            // Добавляем варианты ответов
            question.answers.forEach((answer, index) => {
                const button = document.createElement('button');
                button.className = 'answer-option';
                button.textContent = `• ${String.fromCharCode(97 + index)}) ${answer.text}`;
                
                button.onclick = function() {
                    // Отключаем все кнопки
                    const allButtons = answersContainer.querySelectorAll('button');
                    allButtons.forEach(btn => btn.disabled = true);
                    
                    if (answer.correct) {
                        button.classList.add('correct');
                        document.getElementById('feedback').textContent = "✓ " + answer.note;
                        document.getElementById('feedback').className = 'feedback correct';
                        score++;
                    } else {
                        button.classList.add('incorrect');
                        document.getElementById('feedback').textContent = "✗ " + answer.note;
                        document.getElementById('feedback').className = 'feedback incorrect';
                        
                        // Показываем правильный ответ
                        const correctButton = Array.from(allButtons).find(btn => 
                            question.answers[Array.from(allButtons).indexOf(btn)].correct
                        );
                        if (correctButton) correctButton.classList.add('correct');
                    }
                    
                    // Показываем кнопку "Следующий вопрос"
                    document.getElementById('nextQuestion').classList.remove('hidden');
                };
                
                answersContainer.appendChild(button);
            });
            
            // Скрываем кнопку "Следующий вопрос" и очищаем feedback
            document.getElementById('nextQuestion').classList.add('hidden');
            document.getElementById('feedback').textContent = '';
            document.getElementById('feedback').className = 'feedback';
        }
        
        // Функция для следующего вопроса
        function nextQuestion() {
            currentQuestion++;
            
            if (currentQuestion < quizData.length) {
                showQuestion();
            } else {
                showResults();
            }
        }
        
        // Функция для показа результатов
        function showResults() {
            document.getElementById('questionScreen').classList.add('hidden');
            document.getElementById('resultScreen').classList.remove('hidden');
            
            // Обновляем счет
            document.getElementById('scoreText').textContent = `Вы ответили правильно на ${score} из ${quizData.length} вопросов`;
            
            // Показываем сердечки
            const heartsContainer = document.getElementById('heartsContainer');
            heartsContainer.innerHTML = '';
            
            if (score === quizData.length) {
                heartsContainer.textContent = '❤️❤️';
                document.getElementById('finalMessage').textContent = "Поздравляем! Вы отлично знаете Юру и получаете два сердечка!";
            } else if (score >= 3) {
                heartsContainer.textContent = '❤️';
                document.getElementById('finalMessage').textContent = "Хороший результат! Вы много знаете о Юре!";
            } else {
                document.getElementById('finalMessage').textContent = "Попробуйте еще раз, чтобы лучше узнать Юру!";
            }
        }
        
        // Функция для перезапуска игры
        function restartGame() {
            currentQuestion = 0;
            score = 0;
            document.getElementById('resultScreen').classList.add('hidden');
            document.getElementById('questionScreen').classList.remove('hidden');
            showQuestion();
        }
        
        // Назначаем обработчики событий
        window.onload = function() {
            // Назначаем обработчики для кнопок
            document.getElementById('startGame').onclick = startGame;
            document.getElementById('exitGame').onclick = exitGame;
            document.getElementById('nextQuestion').onclick = nextQuestion;
            document.getElementById('restartGame').onclick = restartGame;
            
            // Убедимся, что меню видно
            document.getElementById('loadingScreen').classList.add('hidden');
            document.getElementById('menuScreen').classList.remove('hidden');
        };
        
        // Альтернативный способ инициализации
        setTimeout(function() {
            // Проверяем, назначены ли обработчики
            if (!document.getElementById('startGame').onclick) {
                document.getElementById('startGame').onclick = startGame;
            }
            if (!document.getElementById('exitGame').onclick) {
                document.getElementById('exitGame').onclick = exitGame;
            }
        }, 100);
    </script>
</body>
</html>

