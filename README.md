# QuizHobb
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Amour & Humour - Pour Sarah ❤️</title>
    
    <!-- Google Fonts & Tailwind CSS -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Outfit:wght@400;600;700;800&family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Canvas Confetti Library pour l'effet féerique final -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <style>
        /* Polices personnalisées */
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #ffe5ec 0%, #ffc2d1 50%, #ffb3c6 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .font-handwriting {
            font-family: 'Dancing Script', cursive;
        }

        .font-outfit {
            font-family: 'Outfit', sans-serif;
        }

        /* Glassmorphism effet pour la carte principale */
        .glass-card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.6);
            box-shadow: 0 20px 50px rgba(235, 77, 120, 0.15);
        }

        /* Canvas d'arrière-plan pour la pluie de cœurs douce */
        #hearts-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 0;
        }

        /* Animations personnalisées */
        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(3deg); }
        }

        .animate-float {
            animation: float 4s ease-in-out infinite;
        }

        @keyframes popIn {
            0% { transform: scale(0.6); opacity: 0; }
            80% { transform: scale(1.05); opacity: 1; }
            100% { transform: scale(1); opacity: 1; }
        }

        .animate-pop-in {
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-8px); }
            40%, 80% { transform: translateX(8px); }
        }

        .animate-shake {
            animation: shake 0.4s ease-in-out;
        }

        @keyframes pulseGlow {
            0%, 100% { box-shadow: 0 0 15px rgba(244, 63, 94, 0.4); }
            50% { box-shadow: 0 0 30px rgba(244, 63, 94, 0.8); }
        }

        .pulse-glow {
            animation: pulseGlow 2s infinite;
        }

        /* Boutons personnalisés avec reflets */
        .btn-romantic {
            background: linear-gradient(135deg, #ff4d6d 0%, #c9184a 100%);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }

        .btn-romantic:hover {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 10px 25px rgba(201, 24, 74, 0.4);
        }

        .btn-romantic:active {
            transform: translateY(1px) scale(0.98);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.9);
            border: 2px solid #ff758f;
            color: #c9184a;
            transition: all 0.3s ease;
        }

        .btn-secondary:hover {
            background: #ffe5ec;
            transform: translateY(-2px);
        }

        /* Barre de progression avec dégradé */
        .progress-bar-fill {
            background: linear-gradient(90deg, #ff758f 0%, #ff4d6d 50%, #c9184a 100%);
            transition: width 0.5s ease-in-out;
        }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen p-4 relative">

    <!-- Canvas pour l'arrière-plan interactif de cœurs -->
    <canvas id="hearts-canvas"></canvas>

    <!-- Conteneur principal -->
    <main class="w-full max-w-lg glass-card rounded-3xl p-6 sm:p-8 relative z-10 my-8 transition-all duration-500">
        
        <!-- En-tête / Barre de progression (masquée sur l'écran final) -->
        <header id="quiz-header" class="mb-6">
            <div class="flex justify-between items-center mb-2">
                <span class="text-xs font-bold tracking-wider text-rose-500 uppercase">Quiz Spécial Ammar & Sarah</span>
                <span id="step-indicator" class="text-xs font-semibold px-3 py-1 rounded-full bg-rose-100 text-rose-600">Question 1 / 4</span>
            </div>
            <div class="w-full h-3 bg-rose-100 rounded-full overflow-hidden p-0.5 border border-rose-200">
                <div id="progress-bar" class="h-full rounded-full progress-bar-fill w-1/4"></div>
            </div>
        </header>

        <!-- ZONE DE JEU / QUESTIONS -->
        <div id="quiz-body" class="relative">

            <!-- QUESTION 1 -->
            <section id="step-1" class="space-y-6 transition-all duration-300">
                <div class="text-center space-y-2">
                    <span class="text-4xl inline-block animate-float">🥊 🆚 🦍</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-gray-800 font-outfit">Qui gagne en 1vs1 ?</h2>
                    <p class="text-sm text-gray-500">Réfléchis bien avant de répondre...</p>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 pt-2">
                    <button onclick="handleQ1Choice('gorille')" class="btn-secondary font-semibold py-4 px-6 rounded-2xl shadow-sm text-lg flex items-center justify-center gap-2">
                        Un gorille 🦍
                    </button>
                    <button onclick="handleQ1Choice('ammar')" class="btn-secondary font-semibold py-4 px-6 rounded-2xl shadow-sm text-lg flex items-center justify-center gap-2">
                        Ammar 🥊
                    </button>
                </div>

                <!-- Message d'erreur / Indice Q1 -->
                <div id="q1-feedback" class="hidden text-center p-4 bg-amber-50 border border-amber-200 text-amber-700 rounded-2xl text-sm font-medium animate-pop-in">
                    Raté ! Ni l'un ni l'autre... 😏 <br>
                    <span class="text-xs text-amber-600">Un indice : ça se mange et ça donne de la force ! 🍫</span>
                </div>

                <!-- Bouton Surprise Q1 -->
                <div id="q1-surprise-container" class="hidden text-center pt-2">
                    <button onclick="validateStep(1)" class="btn-romantic pulse-glow text-white font-bold py-4 px-8 rounded-2xl text-xl w-full flex items-center justify-center gap-3 animate-pop-in">
                        ✨ Un mars 🍫 ✨
                    </button>
                </div>
            </section>

            <!-- QUESTION 2 -->
            <section id="step-2" class="hidden space-y-6 transition-all duration-300">
                <div class="text-center space-y-2">
                    <span class="text-4xl inline-block animate-float">👑 ✨</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-gray-800 font-outfit">Quelle est la plus belle femme au monde ?</h2>
                    <p class="text-sm text-gray-500">Une question objective et indiscutable :</p>
                </div>

                <div class="pt-4">
                    <button onclick="validateStep(2)" class="btn-romantic pulse-glow text-white font-bold py-5 px-8 rounded-2xl text-2xl w-full flex items-center justify-center gap-3 shadow-lg hover:scale-105 transition-transform">
                        Sarah ✨👑
                    </button>
                </div>
            </section>

            <!-- QUESTION 3 -->
            <section id="step-3" class="hidden space-y-6 transition-all duration-300">
                <div class="text-center space-y-2">
                    <span class="text-4xl inline-block animate-float">🌸 🤡</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-gray-800 font-outfit">Quelle est la femme la plus douce ?</h2>
                    <p class="text-sm text-gray-500">Fais le bon choix...</p>
                </div>

                <div class="grid grid-cols-1 gap-4 pt-2">
                    <button id="q3-wrong-btn" onclick="handleQ3Wrong()" class="btn-secondary font-semibold py-4 px-6 rounded-2xl text-lg flex items-center justify-center gap-2">
                        Les ex d'Ammar 🤡
                    </button>
                    <button onclick="validateStep(3)" class="btn-romantic text-white font-bold py-4 px-6 rounded-2xl text-xl flex items-center justify-center gap-2 shadow-md">
                        Sarah 🌸
                    </button>
                </div>

                <!-- Feedback taquin Q3 -->
                <div id="q3-feedback" class="hidden text-center p-4 bg-rose-100 border border-rose-300 text-rose-700 rounded-2xl text-sm font-semibold animate-pop-in">
                    Euh... tu es sûre de toi là ? 😂<br>
                    <span class="text-xs font-normal">Reconsidère immédiatement ton choix mademoiselle !</span>
                </div>
            </section>

            <!-- QUESTION 4 -->
            <section id="step-4" class="hidden space-y-6 transition-all duration-300">
                <div class="text-center space-y-2">
                    <span class="text-4xl inline-block animate-float">💖 🤔</span>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-gray-800 font-outfit">Est-ce qu'Ammar il t'aime ?</h2>
                    <p class="text-sm text-gray-500">Essaie de dire non pour voir...</p>
                </div>

                <div class="relative min-h-[160px] flex items-center justify-center pt-2">
                    <!-- Bouton OUI (Immanquable) -->
                    <button onclick="finishQuiz()" class="btn-romantic pulse-glow text-white font-bold py-5 px-10 rounded-2xl text-2xl shadow-xl hover:scale-110 z-10 transition-transform">
                        Oui ❤️
                    </button>

                    <!-- Bouton NON (Qui s'enfuit) -->
                    <button id="btn-no" onmouseenter="evadeButton()" onclick="evadeButton()" class="btn-secondary font-semibold py-3 px-6 rounded-2xl text-base absolute z-20 transition-all duration-200">
                        Non ❌
                    </button>
                </div>
            </section>

            <!-- ÉCRAN DE VICTOIRE / FIN -->
            <section id="step-final" class="hidden space-y-6 text-center animate-pop-in">
                <div class="space-y-3">
                    <span class="text-6xl inline-block animate-bounce">💖 🎉 ✨</span>
                    <h2 class="text-3xl sm:text-4xl font-extrabold text-rose-600 font-outfit">Félicitations Sarah !</h2>
                    <p class="text-base text-gray-600 font-medium">Tu as réussi le test haut la main !</p>
                </div>

                <!-- Carte Déclaration de Ammar -->
                <div class="bg-white/80 p-6 rounded-2xl border-2 border-rose-200 shadow-inner space-y-4 text-left">
                    <div class="flex items-center gap-3 border-b border-rose-100 pb-3">
                        <div class="w-10 h-10 rounded-full bg-rose-500 flex items-center justify-center text-white text-xl font-bold">
                            A
                        </div>
                        <div>
                            <h3 class="font-bold text-gray-800">Message d'Ammar</h3>
                            <p class="text-xs text-rose-500 font-medium">Certifié 100% sincère et amoureux</p>
                        </div>
                    </div>
                    <p class="text-gray-700 italic leading-relaxed text-sm sm:text-base">
                        « Ma chère Sarah, tu es la personne la plus incroyable, la plus magnifique et la plus douce au monde. Ce petit jeu était juste une excuse pour te faire sourire et te rappeler à quel point je t'aime fort chaque jour ! »
                    </p>
                    <div class="text-right font-handwriting text-2xl text-rose-600 font-bold">
                        Pour toujours, Ammar ❤️
                    </div>
                </div>

                <button onclick="restartQuiz()" class="btn-secondary text-rose-600 font-semibold py-3 px-8 rounded-full text-sm inline-flex items-center gap-2 hover:bg-rose-50">
                    🔄 Recommencer le test
                </button>
            </section>

        </div>
    </main>

    <script>
        /* ==========================================
           LOGIQUE ET ÉTATS DU QUIZ
           ========================================== */
        let currentStep = 1;
        const totalSteps = 4;

        // Mise à jour de la barre de progression
        function updateProgress() {
            const progressBar = document.getElementById('progress-bar');
            const stepIndicator = document.getElementById('step-indicator');
            const percentage = (currentStep / totalSteps) * 100;

            if (progressBar) progressBar.style.width = `${percentage}%`;
            if (stepIndicator) stepIndicator.textContent = `Question ${currentStep} / ${totalSteps}`;
        }

        // Passer à la question suivante
        function validateStep(stepNumber) {
            // Animation explosion de cœurs locale
            triggerMiniConfetti();

            const currentElement = document.getElementById(`step-${stepNumber}`);
            currentElement.classList.add('opacity-0', 'scale-95');

            setTimeout(() => {
                currentElement.classList.add('hidden');
                currentElement.classList.remove('opacity-0', 'scale-95');

                currentStep++;
                const nextElement = document.getElementById(`step-${currentStep}`);
                if (nextElement) {
                    nextElement.classList.remove('hidden');
                    nextElement.classList.add('animate-pop-in');
                }

                updateProgress();

                // Si on arrive à la Q4, positionner le bouton Non proprement au départ
                if (currentStep === 4) {
                    resetNoButtonPosition();
                }
            }, 300);
        }

        /* Q1 : Gestion Gorille vs Ammar -> Apparition du Mars */
        function handleQ1Choice(choice) {
            const feedback = document.getElementById('q1-feedback');
            const surprise = document.getElementById('q1-surprise-container');

            if (feedback && surprise) {
                feedback.classList.remove('hidden');
                surprise.classList.remove('hidden');
                
                // Animation de secousse légère sur la carte
                const card = document.querySelector('main');
                card.classList.add('animate-shake');
                setTimeout(() => card.classList.remove('animate-shake'), 400);
            }
        }

        /* Q3 : Gestion des Ex d'Ammar */
        function handleQ3Wrong() {
            const feedback = document.getElementById('q3-feedback');
            const wrongBtn = document.getElementById('q3-wrong-btn');

            if (feedback && wrongBtn) {
                feedback.classList.remove('hidden');
                wrongBtn.classList.add('animate-shake');
                setTimeout(() => wrongBtn.classList.remove('animate-shake'), 400);
            }
        }

        /* Q4 : Bouton "NON" qui s'enfuit */
        function evadeButton() {
            const btnNo = document.getElementById('btn-no');
            if (!btnNo) return;

            // Calcul de coordonnées aléatoires à l'intérieur de la carte ou de la fenêtre
            const mainCard = document.querySelector('main');
            const rect = mainCard.getBoundingClientRect();

            // Générer de nouvelles positions relatives
            const maxX = rect.width - btnNo.offsetWidth - 30;
            const maxY = rect.height - btnNo.offsetHeight - 30;

            const newX = Math.random() * maxX - (rect.width / 2) + 50;
            const newY = Math.random() * maxY - (rect.height / 2) + 50;

            btnNo.style.transform = `translate(${newX}px, ${newY}px) scale(0.9)`;
        }

        function resetNoButtonPosition() {
            const btnNo = document.getElementById('btn-no');
            if (btnNo) {
                btnNo.style.top = '70%';
                btnNo.style.right = '10%';
                btnNo.style.transform = 'translate(0, 0)';
            }
        }

        /* ÉCRAN DE FIN / VICTOIRE */
        function finishQuiz() {
            document.getElementById('quiz-header').classList.add('hidden');
            document.getElementById('step-4').classList.add('hidden');

            const finalElement = document.getElementById('step-final');
            finalElement.classList.remove('hidden');

            // Pluie torrentielle de confetti/cœurs
            triggerGrandFireworks();
        }

        // Recommencer le quiz
        function restartQuiz() {
            currentStep = 1;
            
            // Masquer la fin et réafficher l'en-tête
            document.getElementById('step-final').classList.add('hidden');
            document.getElementById('quiz-header').classList.remove('hidden');

            // Cacher les feedbacks Q1 et Q3
            document.getElementById('q1-feedback').classList.add('hidden');
            document.getElementById('q1-surprise-container').classList.add('hidden');
            document.getElementById('q3-feedback').classList.add('hidden');

            // Réinitialiser les sections
            for (let i = 2; i <= 4; i++) {
                document.getElementById(`step-${i}`).classList.add('hidden');
            }
            document.getElementById('step-1').classList.remove('hidden');

            updateProgress();
        }

        /* ==========================================
           EFFETS CONFETTI & CŒURS (canvas-confetti)
           ========================================== */
        function triggerMiniConfetti() {
            if (typeof confetti === 'function') {
                confetti({
                    particleCount: 25,
                    spread: 60,
                    origin: { y: 0.7 },
                    colors: ['#ff4d6d', '#ff758f', '#ffb3c6']
                });
            }
        }

        function triggerGrandFireworks() {
            if (typeof confetti !== 'function') return;

            const duration = 5 * 1000;
            const animationEnd = Date.now() + duration;

            const interval = setInterval(function() {
                const timeLeft = animationEnd - Date.now();

                if (timeLeft <= 0) {
                    return clearInterval(interval);
                }

                const particleCount = 50 * (timeLeft / duration);

                // Tirer des deux côtés
                confetti({
                    particleCount,
                    startVelocity: 30,
                    spread: 360,
                    ticks: 60,
                    origin: { x: Math.random(), y: Math.random() - 0.2 },
                    colors: ['#ff4d6d', '#c9184a', '#ff8fa3', '#fff0f3', '#ff0054']
                });
            }, 250);
        }

        /* ==========================================
           CANVAS ANIMATION - PLUIE DE CŒURS DOUCE (BACKGROUND)
           ========================================== */
        const canvas = document.getElementById('hearts-canvas');
        const ctx = canvas.getContext('2d');

        let hearts = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Heart {
            constructor() {
                this.reset();
            }

            reset() {
                this.x = Math.random() * canvas.width;
                this.y = canvas.height + Math.random() * 100;
                this.size = Math.random() * 12 + 8;
                this.speedY = Math.random() * 1.5 + 0.5;
                this.speedX = Math.sin(Math.random() * Math.PI) * 0.5;
                this.opacity = Math.random() * 0.5 + 0.3;
                this.color = `hsla(${Math.random() * 20 + 340}, 100%, 75%, ${this.opacity})`;
            }

            update() {
                this.y -= this.speedY;
                this.x += Math.sin(this.y * 0.01) * 0.5;

                if (this.y < -20) {
                    this.reset();
                }
            }

            draw() {
                ctx.save();
                ctx.translate(this.x, this.y);
                ctx.beginPath();
                ctx.fillStyle = this.color;

                // Dessiner une forme de cœur simple
                const topCurveHeight = this.size * 0.3;
                ctx.moveTo(0, topCurveHeight);
                ctx.bezierCurveTo(0, 0, -this.size / 2, 0, -this.size / 2, topCurveHeight);
                ctx.bezierCurveTo(-this.size / 2, (this.size + topCurveHeight) / 2, 0, this.size, 0, this.size);
                ctx.bezierCurveTo(0, this.size, this.size / 2, (this.size + topCurveHeight) / 2, this.size / 2, topCurveHeight);
                ctx.bezierCurveTo(this.size / 2, 0, 0, 0, 0, topCurveHeight);

                ctx.closePath();
                ctx.fill();
                ctx.restore();
            }
        }

        // Créer les cœurs au démarrage
        for (let i = 0; i < 25; i++) {
            hearts.push(new Heart());
        }

        function animateHearts() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            hearts.forEach(heart => {
                heart.update();
                heart.draw();
            });
            requestAnimationFrame(animateHearts);
        }

        window.onload = function() {
            animateHearts();
            updateProgress();
        };
    </script>
</body>
</html>
