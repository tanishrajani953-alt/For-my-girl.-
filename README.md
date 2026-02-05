<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Queen ❤️</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root { --primary: #ff4d6d; --soft-pink: #ffb3c1; --bg: #fff0f3; }
        body { margin: 0; background: var(--bg); font-family: 'Poppins', sans-serif; overflow-x: hidden; color: #555; }
        
        /* Romantic Floating Petals Animation */
        .petal { position: fixed; color: var(--primary); font-size: 20px; pointer-events: none; z-index: 999; animation: fall linear infinite; }
        @keyframes fall { to { transform: translateY(100vh) rotate(360deg); } }

        .container { min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 20px; }
        .glass-card { background: rgba(255, 255, 255, 0.95); padding: 40px; border-radius: 40px; box-shadow: 0 15px 35px rgba(255, 77, 109, 0.2); width: 100%; max-width: 450px; text-align: center; border: 2px solid var(--soft-pink); }
        
        h1 { font-family: 'Dancing Script', cursive; color: var(--primary); font-size: 3.2rem; margin-bottom: 10px; }
        .hidden { display: none; }
        
        .quiz-option {
            display: block; width: 100%; padding: 15px; margin: 12px 0;
            border: 2px solid var(--soft-pink); border-radius: 20px;
            background: white; cursor: pointer; transition: all 0.3s; font-size: 1rem;
        }
        .quiz-option:hover { background: var(--soft-pink); color: white; transform: scale(1.02); }
        
        #yesBtn { background: var(--primary); color: white; padding: 15px 40px; border-radius: 50px; border: none; font-size: 1.3rem; cursor: pointer; box-shadow: 0 5px 15px rgba(255, 77, 109, 0.4); }
        #noBtn { background: #f8f9fa; color: #999; padding: 10px 25px; border-radius: 50px; border: none; cursor: pointer; }

        .photo-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; padding: 20px; max-width: 800px; margin: 0 auto; }
        .photo-card { background: white; padding: 8px; border-radius: 15px; transform: rotate(-2deg); box-shadow: 0 10px 20px rgba(0,0,0,0.1); }
        .photo-card:nth-child(even) { transform: rotate(2deg); }
        .photo-card img { width: 100%; border-radius: 10px; }
    </style>
</head>
<body>

    <div class="container" id="proposalSection">
        <div class="glass-card">
            <h1>Hi Beautiful... ✨</h1>
            <p>I made something special for you. Ready?</p>
            <div style="margin-top: 30px; position: relative; height: 120px;">
                <button id="yesBtn" onclick="startQuiz()">YES, let's see! ❤️</button>
                <button id="noBtn" style="position: absolute; left: 50%; transform: translateX(-50%); top: 80px;" onmouseover="moveNo()">No</button>
            </div>
        </div>
    </div>

    <div class="container hidden" id="quizSection">
        <div class="glass-card">
            <h2 id="quizQuestion" style="color: var(--primary);">Question</h2>
            <div id="optionsContainer"></div>
        </div>
    </div>

    <div class="hidden" id="finalSection" style="padding-bottom: 50px;">
        <h1 style="margin-top: 50px;">You're my favorite person! ❤️</h1>
        <p>Every moment with you is a dream come true.</p>
        <div class="photo-grid">
            <div class="photo-card"><img src="images/photo1.jpg"></div>
            <div class="photo-card"><img src="images/photo2.jpg"></div>
            <div class="photo-card"><img src="images/photo3.jpg"></div>
            <div class="photo-card"><img src="images/photo4.jpg"></div>
        </div>
    </div>

    <audio id="bgMusic" loop><source src="music.mp3" type="audio/mpeg"></audio>

    <script>
        const questions = [
            { q: "Who is the prettiest girl in the world?", a: ["You", "Still You", "Definitely You", "All of the above"], correct: 3 },
            { q: "How much do I love you?", a: ["A little", "A lot", "To the moon and back", "More than pizza"], correct: 2 }
        ];

        let currentQuestion = 0;

        function createPetal() {
            const petal = document.createElement('div');
            petal.innerHTML = '🌸';
            petal.className = 'petal';
            petal.style.left = Math.random() * 100 + 'vw';
            petal.style.animationDuration = Math.random() * 3 + 2 + 's';
            document.body.appendChild(petal);
            setTimeout(() => petal.remove(), 5000);
        }
        setInterval(createPetal, 300);

        function moveNo() {
            const btn = document.getElementById('noBtn');
            btn.style.left = Math.random() * 80 + '%';
            btn.style.top = Math.random() * 80 + 'px';
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
                btn.onclick = () => {
                    currentQuestion++;
                    if(currentQuestion < questions.length) showQuestion();
                    else showFinal();
                };
            });
        }

        function showFinal() {
            document.getElementById('quizSection').classList.add('hidden');
            document.getElementById('finalSection').classList.remove('hidden');
            confetti({ particleCount: 200, spread: 100, origin: { y: 0.6 }, colors: ['#ff4d6d', '#ffb3c1', '#ffffff'] });
        }
    </script>
</body>
</html>
