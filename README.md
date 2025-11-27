<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Everyday & Holiday Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #6a93cb 0%, #a4bfef 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .word-bank h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(74, 111, 165, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 111, 165, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #4a6fa5;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #4a6fa5;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #4a6fa5;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .option.selected {
            background: #4a6fa5;
            color: white;
            border-color: #4a6fa5;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #4a6fa5;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #4a6fa5;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #4a6fa5;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(74, 111, 165, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #4a6fa5, #6a93cb);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(74, 111, 165, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 20px;
        }

        .vocabulary-item {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #4a6fa5;
            margin-bottom: 10px;
            font-size: 1.4em;
            border-bottom: 2px solid #4a6fa5;
            padding-bottom: 8px;
        }

        .vocabulary-item p {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 15px;
            border-left: 3px solid #4a6fa5;
            margin-top: 10px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Everyday & Holiday Terms</h1>
            <p>Test your knowledge of these English terms and expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>wand</h3>
                    <p><strong>Definition:</strong> A thin stick or rod used by magicians, conjurers, or fairy tale characters.</p>
                    <p><strong>Usage:</strong> Often associated with magic, spells, and fairy tales.</p>
                    <p class="example"><strong>Example:</strong> "The magician waved his wand and a rabbit appeared from the hat."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>carpet</h3>
                    <p><strong>Definition:</strong> A floor covering made from thick woven fabric.</p>
                    <p><strong>Usage:</strong> Can also mean to cover a floor with carpet or metaphorically to cover something completely.</p>
                    <p class="example"><strong>Example:</strong> "The living room has a beautiful Persian carpet."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>Thanksgiving Day</h3>
                    <p><strong>Definition:</strong> A national holiday in the United States and Canada celebrating harvest and blessings.</p>
                    <p><strong>Usage:</strong> Traditionally involves family gatherings and a feast with turkey.</p>
                    <p class="example"><strong>Example:</strong> "We always visit my grandparents on Thanksgiving Day for a big family dinner."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>fur</h3>
                    <p><strong>Definition:</strong> The thick hair that covers the bodies of some animals.</p>
                    <p><strong>Usage:</strong> Can also refer to clothing or accessories made from animal fur.</p>
                    <p class="example"><strong>Example:</strong> "The cat's fur was soft and silky to the touch."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>tale</h3>
                    <p><strong>Definition:</strong> A story, especially one that is imaginative or fictional.</p>
                    <p><strong>Usage:</strong> Often used for fairy tales, folk tales, or any narrative story.</p>
                    <p class="example"><strong>Example:</strong> "Grandma told us an exciting tale about her childhood adventures."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>bowl</h3>
                    <p><strong>Definition:</strong> A round, deep dish or container used for food or liquid.</p>
                    <p><strong>Usage:</strong> Can also refer to the contents of a bowl or a sports stadium shaped like a bowl.</p>
                    <p class="example"><strong>Example:</strong> "She served the soup in a large ceramic bowl."</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">wand</span>
                    <span class="word-option">carpet</span>
                    <span class="word-option">Thanksgiving Day</span>
                    <span class="word-option">fur</span>
                    <span class="word-option">tale</span>
                    <span class="word-option">bowl</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #4a6fa5;">Match the words with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Words</h4>
                    <div class="match-item" data-word="wand" onclick="selectMatch(this)">wand</div>
                    <div class="match-item" data-word="carpet" onclick="selectMatch(this)">carpet</div>
                    <div class="match-item" data-word="Thanksgiving Day" onclick="selectMatch(this)">Thanksgiving Day</div>
                    <div class="match-item" data-word="fur" onclick="selectMatch(this)">fur</div>
                    <div class="match-item" data-word="tale" onclick="selectMatch(this)">tale</div>
                    <div class="match-item" data-word="bowl" onclick="selectMatch(this)">bowl</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What is a "wand"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, true)">A thin stick used by magicians or in fairy tales</div>
                    <div class="option" onclick="selectOption(this, false)">A musical instrument</div>
                    <div class="option" onclick="selectOption(this, false)">A type of clothing</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What is a "carpet"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of ceiling covering</div>
                    <div class="option" onclick="selectOption(this, true)">A floor covering made from thick woven fabric</div>
                    <div class="option" onclick="selectOption(this, false)">A window treatment</div>
                    <div class="option" onclick="selectOption(this, false)">A type of furniture</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What is "Thanksgiving Day"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A day for exchanging gifts</div>
                    <div class="option" onclick="selectOption(this, true)">A holiday celebrating harvest and blessings with family gatherings</div>
                    <div class="option" onclick="selectOption(this, false)">A religious fasting day</div>
                    <div class="option" onclick="selectOption(this, false)">A day for fireworks</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What is "fur"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of fabric made from plants</div>
                    <div class="option" onclick="selectOption(this, true)">The thick hair that covers the bodies of some animals</div>
                    <div class="option" onclick="selectOption(this, false)">A type of food</div>
                    <div class="option" onclick="selectOption(this, false)">A musical instrument</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: What is a "tale"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A scientific fact</div>
                    <div class="option" onclick="selectOption(this, true)">A story, especially one that is imaginative or fictional</div>
                    <div class="option" onclick="selectOption(this, false)">A mathematical equation</div>
                    <div class="option" onclick="selectOption(this, false)">A type of measurement</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What is a "bowl"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A type of chair</div>
                    <div class="option" onclick="selectOption(this, true)">A round, deep dish or container used for food or liquid</div>
                    <div class="option" onclick="selectOption(this, false)">A window frame</div>
                    <div class="option" onclick="selectOption(this, false)">A door handle</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "wand", text: "A thin stick used by magicians or in fairy tales" },
            { meaning: "carpet", text: "A floor covering made from thick woven fabric" },
            { meaning: "Thanksgiving Day", text: "A holiday celebrating harvest and blessings with family gatherings" },
            { meaning: "fur", text: "The thick hair that covers the bodies of some animals" },
            { meaning: "tale", text: "A story, especially one that is imaginative or fictional" },
            { meaning: "bowl", text: "A round, deep dish or container used for food or liquid" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "The magician waved his <input type='text' class='fill-blank' data-answer='wand' placeholder='answer'> and a rabbit appeared from the hat.", answer: "wand" },
            { text: "The living room has a beautiful Persian <input type='text' class='fill-blank' data-answer='carpet' placeholder='answer'>.", answer: "carpet" },
            { text: "We always visit my grandparents on <input type='text' class='fill-blank' data-answer='Thanksgiving Day' placeholder='answer'> for a big family dinner.", answer: "Thanksgiving Day" },
            { text: "The cat's <input type='text' class='fill-blank' data-answer='fur' placeholder='answer'> was soft and silky to the touch.", answer: "fur" },
            { text: "Grandma told us an exciting <input type='text' class='fill-blank' data-answer='tale' placeholder='answer'> about her childhood adventures.", answer: "tale" },
            { text: "She served the soup in a large ceramic <input type='text' class='fill-blank' data-answer='bowl' placeholder='answer'>.", answer: "bowl" },
            { text: "In the fairy tale, the fairy godmother used her magic <input type='text' class='fill-blank' data-answer='wand' placeholder='answer'> to grant wishes.", answer: "wand" },
            { text: "We need to clean the <input type='text' class='fill-blank' data-answer='carpet' placeholder='answer'> because it's full of stains.", answer: "carpet" },
            { text: "On <input type='text' class='fill-blank' data-answer='Thanksgiving Day' placeholder='answer'>, we traditionally eat turkey and pumpkin pie.", answer: "Thanksgiving Day" },
            { text: "The bear's thick <input type='text' class='fill-blank' data-answer='fur' placeholder='answer'> keeps it warm during winter.", answer: "fur" },
            { text: "The children loved listening to the fairy <input type='text' class='fill-blank' data-answer='tale' placeholder='answer'> before bedtime.", answer: "tale" },
            { text: "He ate a <input type='text' class='fill-blank' data-answer='bowl' placeholder='answer'> of cereal for breakfast every morning.", answer: "bowl" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>
