# For-my-girl.-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Ultimate Valentine Challenge ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root { --primary: #ff4d6d; --bg: #fff0f3; }
        body { margin: 0; background: var(--bg); font-family: 'Poppins', sans-serif; text-align: center; color: #444; }
        
        .container { min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 20px; }
        .glass-card { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(10px); padding: 40px; border-radius: 30px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); width: 100%; max-width: 500px; }
        
        h1 { font-family: 'Dancing Script', cursive; color: var(--primary); font-size: 3rem; }
        .hidden { display: none; }
        
        /* Quiz Styling */
        .quiz-option {
            display: block; width: 100%; padding: 12px; margin: 10px 0;
            border: 2px solid var(--primary); border-radius: 15px;
            background: white; cursor: pointer; transition: 0.3s; font-weight: 600;
        }
        .quiz-option:hover { background: var(--primary); color: white; }
        
        button { padding: 15px 35px; border-radius: 50px; border: none; cursor: pointer; font-weight: 600; }
        #yesBtn { background: var(--primary); color: white; font-size: 1.2rem; }

        .photo-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; padding: 20px; }
        .photo-card img { width: 100%; border-radius: 15px; border: 5px solid white; box-shadow: 0 5px 15px rgba(0,0,0,0.1); }
    </style>
</head>
<body>

    <div class="container" id="proposalSection">
        <div class="glass-card">
            <h1>Will you be my Valentine? 🌹</h1>
            <div style="position: relative; height: 100px; margin-top: 30px;">
                <button id="yesBtn" onclick="startQuiz()">YES! ❤️</button>
                <button id="noBtn" style="position: absolute; margin-left: 10px;" onmouseover="moveNo()">No</button>
            </div>
        </div>
    </div>

    <div class="container hidden" id="quizSection">
        <div class="glass-card">
            <h2 id="quizQuestion">Question 1</h2>
            <div id="optionsContainer"></div>
            <p id="quizFeedback" style="margin-top: 15px; font-weight: bold;"></p>
        </div>
    </div>

    <div class="hidden" id="finalSection">
        <h1>You passed! You're officially mine. 😍</h1>
        <div class="photo-grid">
            <div class="photo-card"><img src="images/photo1.jpg"></div>
            <div class="photo-card"><img src="images/photo2.jpg"></div>
            <div class="photo-card"><img src="images/photo3.jpg"></div>
            <div class="photo-card"><img src="images/photo4.jpg"></div>
        </div>
    </div>

    <audio id="bgMusic" loop><source src="music.mp3" type="audio/mpeg"></audio>

    <script>
        // --- QUIZ DATA (Change these to your own!) ---
        const questions = [
            { q: "Where was our first date?", a: ["Coffee Shop", "The Mall", "The Park", "Movie Theater"], correct: 1 },
            { q: "Who said 'I love you' first?", a: ["Me", "You", "Both at once", "Still waiting..."], correct: 0 },
            { q: "What's my favorite thing about you?", a: ["Your smile", "Your eyes", "Everything", "Your cooking"], correct: 2 }
        ];

        let currentQuestion = 0;

        function moveNo() {
            const btn = document.getElementById('noBtn');
            btn.style.left = Math.random() * 200 + 'px';
            btn.style.top = Math.random() * 200 + 'px';
        }

        function startQuiz() {
            document.getElementById('proposalSection').classList.add('hidden');
            document.getElementById('quizSection').classList.remove('hidden');
            document.getElementById('bgMusic').play();
            showQuestion();
        }

        function showQuestion() {
            const q = questions[currentQuestion];
            document.getElementById('quizQuestion').innerText = q.q;
            const container = document.getElementById('optionsContainer');
            container.innerHTML = '';
            
            q.a.forEach((option, index) => {
                const btn = document.createElement('button');
                btn.innerText = option;
                btn.className = 'quiz-option';
                btn.onclick = () => checkAnswer(index);
                container.appendChild(btn);
            });
        }

        function checkAnswer(index) {
            if(index === questions[currentQuestion].correct) {
                currentQuestion++;
                if(currentQuestion < questions.length) {
                    showQuestion();
                } else {
                    showFinal();
                }
            } else {
                document.getElementById('quizFeedback').innerText = "Wrong! Try again, babe. 😘";
                setTimeout(() => { document.getElementById('quizFeedback').innerText = ""; }, 1500);
            }
        }

        function showFinal() {
            document.getElementById('quizSection').classList.add('hidden');
            document.getElementById('finalSection').classList.remove('hidden');
            confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 } });
        }
    </script>
    <audio id="bgMusic" loop>
    <source src="music.mp3" type="audio/mpeg">
</audio>

</body>
</html>
