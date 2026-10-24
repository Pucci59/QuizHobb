# QuizHobb
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz d'Amour Ultimatum 💕</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Canvas Confetti CDN -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Fredoka:wght@400;600;700&family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        romantic: {
                            50: '#fff5f7',
                            100: '#ffe3ec',
                            200: '#fccadc',
                            300: '#f8a5c2',
                            400: '#f368e0',
                            500: '#ff4d4d',
                            600: '#e03657',
                            700: '#b81e3d',
                        }
                    },
                    fontFamily: {
                        sans: ['Poppins', 'sans-serif'],
                        display: ['Fredoka', 'sans-serif'],
                        cursive: ['Dancing Script', 'cursive'],
                    },
                    animation: {
                        'float': 'float 3s ease-in-out infinite',
                        'pulse-slow': 'pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'bounce-short': 'bounceShort 0.5s ease infinite alternate',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-10px)' },
                        },
                        bounceShort: {
                            '0%': { transform: 'translateY(0)' },
                            '100%': { transform: 'translateY(-8px)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #feada6 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Glassmorphism Styles */
        .glass-card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 2px solid rgba(255, 255, 255, 0.6);
            box-shadow: 0 20px 40px rgba(224, 54, 87, 0.15);
        }

        /* Floating background hearts */
        .bg-heart {
            position: absolute;
            opacity: 0.25;
            animation: floatHeart 6s linear infinite;
            z-index: 0;
            pointer-events: none;
        }

        @keyframes floatHeart {
            0% {
                transform: translateY(100vh) scale(0.5) rotate(0deg);
                opacity: 0.3;
            }
            100% {
                transform: translateY(-10vh) scale(1.2) rotate(360deg);
                opacity: 0;
            }
        }

        /* Transition animations for screens */
        .screen-enter {
            animation: fadeInScale 0.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
        }

        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: scale(0.8) translateY(20px);
            }
            to {
                opacity: 1;
                transform: scale(1) translateY(0);
            }
        }

        /* Custom buttons styling */
        .btn-romantic {
            background: linear-gradient(135deg, #ff4e50, #f9d423);
            background: linear-gradient(135deg, #ff758c 0%, #ff7eb3 100%);
            box-shadow: 0 8px 20px rgba(255, 117, 140, 0.4);
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .btn-romantic:hover {
            transform: translateY(-3px) scale(1.02);
            box-shadow: 0 12px 25px rgba(255, 117, 140, 0.6);
        }

        .btn-romantic:active {
            transform: translateY(1px) scale(0.98);
        }

        .btn-secondary {
            background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%);
            box-shadow: 0 8px 20px rgba(161, 196, 253, 0.4);
            transition: all 0.3s ease;
        }

        .btn-secondary:hover {
            transform: translateY(-3px) scale(1.02);
        }

        /* Escaping button smooth repositioning */
        #btn-no {
            transition: all 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
        }
    </style>
</head>
<body class="font-sans text-gray-800 flex items-center justify-center min-h-screen p-4 relative">

    <!-- Container for floating background hearts -->
    <div id="hearts-container" class="fixed inset-0 overflow-hidden pointer-events-none z-0"></div>

    <!-- Main Container -->
    <main class="w-full max-w-lg z-10">

        <!-- ÉCRAN D'ACCUEIL -->
        <div id="screen-welcome" class="glass-card rounded-3xl p-8 text-center screen-enter relative">
            <div class="inline-block p-4 rounded-full bg-pink-100 text-pink-500 mb-4 animate-float">
                <i class="fa-solid fa-heart-pulse text-5xl"></i>
            </div>
            <h1 class="font-display font-bold text-3xl md:text-4xl text-romantic-700 mb-3 leading-tight">
                Le Test d'Amour Ultimatum 💕
            </h1>
            <p class="text-gray-600 mb-8 text-sm md:text-base">
                Un mini-quiz très sérieux (ou pas) pour mesurer ta complicité avec Ammar. Es-tu prête, Sarah ? ✨
            </p>
            <button onclick="startQuiz()" class="btn-romantic text-white font-bold text-lg px-8 py-4 rounded-2xl w-full flex items-center justify-center gap-3 group">
                <span>Commencer le test</span>
                <i class="fa-solid fa-arrow-right group-hover:translate-x-1 transition-transform"></i>
            </button>
        </div>

        <!-- CONTAINER DES QUESTIONS (masqué par défaut) -->
        <div id="quiz-container" class="hidden">

            <!-- BARRE DE PROGRESSION -->
            <div class="mb-6 bg-white/50 backdrop-blur-md rounded-full p-2 border border-white/60 shadow-sm">
                <div class="flex justify-between text-xs font-semibold text-romantic-700 px-3 mb-1">
                    <span>Progression</span>
                    <span id="progress-text">Question 1 / 4</span>
                </div>
                <div class="w-full bg-pink-100 rounded-full h-3 overflow-hidden">
                    <div id="progress-bar" class="bg-gradient-to-r from-pink-400 to-romantic-600 h-full rounded-full transition-all duration-500" style="width: 25%"></div>
                </div>
            </div>

            <!-- QUESTION 1 -->
            <div id="q1" class="glass-card rounded-3xl p-6 md:p-8 text-center screen-enter">
                <span class="inline-block px-3 py-1 bg-pink-100 text-romantic-600 rounded-full text-xs font-bold mb-3">Question 1</span>
                <h2 class="font-display text-2xl md:text-3xl font-bold text-gray-800 mb-6">
                    Qui gagne en 1vs1 ? 🥊
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <button onclick="answerQ1('gorille')" class="btn-secondary text-gray-800 font-semibold p-5 rounded-2xl flex flex-col items-center gap-2 group">
                        <span class="text-4xl group-hover:scale-110 transition-transform">🦍</span>
                        <span>Un gorille</span>
                    </button>
                    <button onclick="answerQ1('ammar')" class="btn-romantic text-white font-bold p-5 rounded-2xl flex flex-col items-center gap-2 group">
                        <span class="text-4xl group-hover:scale-110 transition-transform">💪</span>
                        <span>Ammar</span>
                    </button>
                </div>
            </div>

            <!-- QUESTION 2 -->
            <div id="q2" class="glass-card rounded-3xl p-6 md:p-8 text-center screen-enter hidden">
                <span class="inline-block px-3 py-1 bg-pink-100 text-romantic-600 rounded-full text-xs font-bold mb-3">Question 2</span>
                <h2 class="font-display text-2xl md:text-3xl font-bold text-gray-800 mb-6">
                    Quelle est la plus belle femme au monde ? ✨
                </h2>
                <div class="flex justify-center">
                    <button onclick="answerQ2()" class="btn-romantic text-white font-bold text-xl p-8 rounded-3xl w-full flex flex-col items-center gap-3 animate-pulse-slow">
                        <span class="text-5xl">👑</span>
                        <span class="text-2xl">Sarah</span>
                        <span class="text-xs font-normal opacity-90">(La seule et unique option possible !)</span>
                    </button>
                </div>
            </div>

            <!-- QUESTION 3 -->
            <div id="q3" class="glass-card rounded-3xl p-6 md:p-8 text-center screen-enter hidden">
                <span class="inline-block px-3 py-1 bg-pink-100 text-romantic-600 rounded-full text-xs font-bold mb-3">Question 3</span>
                <h2 class="font-display text-2xl md:text-3xl font-bold text-gray-800 mb-6">
                    Quelle est la femme la plus douce ? 🧸
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <button onclick="answerQ3('gf')" class="btn-secondary text-gray-800 font-semibold p-5 rounded-2xl flex flex-col items-center gap-2 group">
                        <span class="text-4xl group-hover:scale-110 transition-transform">🍬</span>
                        <span>La gf d'Ammar</span>
                    </button>
                    <button onclick="answerQ3('sarah')" class="btn-romantic text-white font-bold p-5 rounded-2xl flex flex-col items-center gap-2 group">
                        <span class="text-4xl group-hover:scale-110 transition-transform">🌸</span>
                        <span>Sarah</span>
                    </button>
                </div>
            </div>

            <!-- QUESTION 4 -->
            <div id="q4" class="glass-card rounded-3xl p-6 md:p-8 text-center screen-enter hidden relative overflow-hidden min-h-[320px] flex flex-col justify-between">
                <div>
                    <span class="inline-block px-3 py-1 bg-pink-100 text-romantic-600 rounded-full text-xs font-bold mb-3">Question Finale</span>
                    <h2 class="font-display text-2xl md:text-3xl font-bold text-gray-800 mb-6">
                        Est-ce qu'Ammar t'aime ? ❤️
                    </h2>
                </div>

                <div id="q4-buttons-container" class="flex flex-col md:flex-row items-center justify-center gap-4 my-auto relative w-full h-32">
                    <button id="btn-yes" onclick="answerQ4()" class="btn-romantic text-white font-bold text-xl px-8 py-4 rounded-2xl w-full md:w-1/2 z-10 shadow-lg">
                        Oui ! 😍
                    </button>
                    <button id="btn-no" onmouseover="escapeButton()" onclick="escapeButton()" class="bg-gray-200 hover:bg-gray-300 text-gray-700 font-semibold text-lg px-8 py-4 rounded-2xl w-full md:w-1/2 z-20">
                        Non 🙈
                    </button>
                </div>
                
                <p id="escape-hint" class="text-xs text-pink-500 italic font-medium h-4"></p>
            </div>

        </div>

        <!-- ÉCRAN DE FIN / VICTOIRE -->
        <div id="screen-end" class="glass-card rounded-3xl p-8 text-center screen-enter hidden relative overflow-hidden">
            <div class="inline-block p-4 rounded-full bg-pink-100 text-romantic-600 mb-4 animate-bounce-short">
                <i class="fa-solid fa-trophy text-5xl"></i>
            </div>
            <h1 class="font-cursive text-4xl md:text-5xl font-bold text-romantic-600 mb-2">
                Score Parfait : 1000/10 ! 🎉
            </h1>
            <p class="font-display font-semibold text-xl text-gray-700 mb-6">
                Félicitations mon amour !
            </p>

            <div class="bg-white/70 backdrop-blur-sm p-6 rounded-2xl border border-pink-200 mb-8 text-left space-y-3 shadow-inner">
                <p class="text-gray-700 text-sm md:text-base leading-relaxed">
                    Tu as réussi le test ultime avec brio (bon, d'accord... les choix étaient légèrement orientés ! 😉).
                </p>
                <p class="text-gray-800 font-medium text-sm md:text-base leading-relaxed">
                    Sache qu'<strong>Ammar t'aime plus que tout au monde</strong>. Tu es la plus belle, la plus douce, et la personne la plus précieuse à ses yeux. ❤️✨
                </p>
            </div>

            <div class="flex flex-col sm:flex-row gap-3">
                <button onclick="restartQuiz()" class="btn-secondary text-gray-700 font-bold py-3.5 px-6 rounded-2xl flex-1 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-rotate-right"></i>
                    <span>Rejouer</span>
                </button>
                <button onclick="sendLove()" class="btn-romantic text-white font-bold py-3.5 px-6 rounded-2xl flex-1 flex items-center justify-center gap-2 shadow-lg">
                    <i class="fa-solid fa-heart"></i>
                    <span>Envoyer un bisou 💋</span>
                </button>
            </div>
        </div>

    </main>

    <!-- MODAL / POP-UP POUR LES MESSAGES HUMORISTIQUES -->
    <div id="modal" class="fixed inset-0 bg-black/40 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden opacity-0 transition-opacity duration-300">
        <div id="modal-content" class="bg-white rounded-3xl p-6 md:p-8 max-w-sm w-full text-center shadow-2xl transform scale-90 transition-transform duration-300">
            <div id="modal-icon" class="text-5xl mb-4"></div>
            <h3 id="modal-title" class="font-display text-xl font-bold text-gray-800 mb-2"></h3>
            <p id="modal-text" class="text-gray-600 text-sm mb-6 leading-relaxed"></p>
            <button id="modal-btn" onclick="closeModal()" class="btn-romantic text-white font-bold px-6 py-3 rounded-xl w-full">
                D'accord ! 😉
            </button>
        </div>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // Audio Synthesizer via Web Audio API (Pas besoin de fichiers externes)
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

        function playSound(type) {
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }

            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain);
            gain.connect(audioCtx.destination);

            const now = audioCtx.currentTime;

            if (type === 'pop') {
                osc.type = 'sine';
                osc.frequency.setValueAtTime(400, now);
                osc.frequency.exponentialRampToValueAtTime(800, now + 0.1);
                gain.gain.setValueAtTime(0.3, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.1);
                osc.start(now);
                osc.stop(now + 0.1);
            } else if (type === 'wrong') {
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(220, now);
                osc.frequency.setValueAtTime(180, now + 0.15);
                gain.gain.setValueAtTime(0.3, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
                osc.start(now);
                osc.stop(now + 0.3);
            } else if (type === 'win') {
                const notes = [261.63, 329.63, 392.00, 523.25];
                notes.forEach((freq, index) => {
                    const noteOsc = audioCtx.createOscillator();
                    const noteGain = audioCtx.createGain();
                    noteOsc.connect(noteGain);
                    noteGain.connect(audioCtx.destination);

                    noteOsc.type = 'sine';
                    noteOsc.frequency.setValueAtTime(freq, now + index * 0.1);
                    noteGain.gain.setValueAtTime(0.2, now + index * 0.1);
                    noteGain.gain.exponentialRampToValueAtTime(0.01, now + index * 0.1 + 0.3);

                    noteOsc.start(now + index * 0.1);
                    noteOsc.stop(now + index * 0.1 + 0.3);
                });
            }
        }

        // Background Hearts Generator
        function createBackgroundHearts() {
            const container = document.getElementById('hearts-container');
            const heartIcons = ['❤️', '💖', '💕', '💗', '✨', '🌸'];
            
            for (let i = 0; i < 15; i++) {
                const heart = document.createElement('div');
                heart.className = 'bg-heart';
                heart.innerText = heartIcons[Math.floor(Math.random() * heartIcons.length)];
                heart.style.left = `${Math.random() * 100}%`;
                heart.style.animationDuration = `${4 + Math.random() * 6}s`;
                heart.style.animationDelay = `${Math.random() * 5}s`;
                heart.style.fontSize = `${16 + Math.random() * 20}px`;
                container.appendChild(heart);
            }
        }
        createBackgroundHearts();

        // Modal Management
        let modalCallback = null;

        function showModal(icon, title, text, callback = null) {
            document.getElementById('modal-icon').innerText = icon;
            document.getElementById('modal-title').innerText = title;
            document.getElementById('modal-text').innerText = text;
            modalCallback = callback;

            const modal = document.getElementById('modal');
            const content = document.getElementById('modal-content');

            modal.classList.remove('hidden');
            setTimeout(() => {
                modal.classList.remove('opacity-0');
                content.classList.remove('scale-90');
                content.classList.add('scale-100');
            }, 10);
        }

        function closeModal() {
            playSound('pop');
            const modal = document.getElementById('modal');
            const content = document.getElementById('modal-content');

            modal.classList.add('opacity-0');
            content.classList.remove('scale-100');
            content.classList.add('scale-90');

            setTimeout(() => {
                modal.classList.add('hidden');
                if (modalCallback) {
                    modalCallback();
                    modalCallback = null;
                }
            }, 300);
        }

        // Quiz State Management
        let currentStep = 0;

        function updateProgress(step) {
            const percent = (step / 4) * 100;
            document.getElementById('progress-bar').style.width = `${percent}%`;
            document.getElementById('progress-text').innerText = `Question ${step} / 4`;
        }

        function startQuiz() {
            playSound('pop');
            document.getElementById('screen-welcome').classList.add('hidden');
            document.getElementById('quiz-container').classList.remove('hidden');
            currentStep = 1;
            updateProgress(currentStep);
        }

        function goToNextQuestion(nextQ) {
            const currentEl = document.getElementById(`q${currentStep}`);
            const nextEl = document.getElementById(`q${nextQ}`);

            currentEl.classList.add('hidden');
            nextEl.classList.remove('hidden');
            
            // Re-trigger CSS animation
            nextEl.classList.remove('screen-enter');
            void nextEl.offsetWidth; 
            nextEl.classList.add('screen-enter');

            currentStep = nextQ;
            updateProgress(currentStep);
        }

        // Question Logic
        function answerQ1(choice) {
            if (choice === 'gorille') {
                playSound('wrong');
                showModal('😤', 'Attends quoi ?! ', 'Tu doutes sérieusement du Prime Ammar ?! Il a le pouvoir de l\'amour avec lui, le gorille n\'a aucune chance ! Réessaie 🥊');
            } else {
                playSound('pop');
                confetti({ particleCount: 40, spread: 60, origin: { y: 0.7 } });
                showModal('🥊❤️', 'Victoire par K.O !', 'Évidemment ! Ammar gagne au 1er round avec le pouvoir de l\'amour !', () => {
                    goToNextQuestion(2);
                });
            }
        }

        function answerQ2() {
            playSound('pop');
            confetti({
                particleCount: 80,
                spread: 100,
                origin: { y: 0.6 },
                colors: ['#ff4d4d', '#ff758c', '#ffffff']
            });
            showModal('😍✨', 'Évidence Absolue !', 'Score de beauté : 1000/10 ! Il n\'y a même pas de débat possible.', () => {
                goToNextQuestion(3);
            });
        }

        function answerQ3(choice) {
            if (choice === 'gf') {
                playSound('pop');
                showModal('😂💕', 'Aha piégée !', 'Mais... la gf d\'Ammar C\'EST Sarah ! Tu t\'es piégée toute seule ! Tu es donc officiellement la plus douce 🧸', () => {
                    goToNextQuestion(4);
                });
            } else {
                playSound('pop');
                confetti({ particleCount: 50, spread: 70, origin: { y: 0.7 } });
                showModal('🧸🌸', 'Absolument !', 'Une douceur infinie au quotidien. Mauvaise réponse impossible ici !', () => {
                    goToNextQuestion(4);
                });
            }
        }

        // Question 4 Escaping Button Logic
        let escapeCount = 0;
        const escapeHints = [
            "Oups, le bouton a glissé ! 😜",
            "Non non non, impossible de cliquer ici ! 😂",
            "Tu insistes ? Tu n'y arriveras pas ! 🏃‍♂️",
            "Allez, clique sur Oui ! ❤️"
        ];

        function escapeButton() {
            playSound('wrong');
            const btnNo = document.getElementById('btn-no');
            const container = document.getElementById('q4-buttons-container');
            const hint = document.getElementById('escape-hint');

            // Get random offsets relative to screen width/height
            const containerRect = container.getBoundingClientRect();
            const xMax = containerRect.width / 2 - 40;
            const yMax = 60;

            const randomX = (Math.random() - 0.5) * xMax * 2;
            const randomY = (Math.random() - 0.5) * yMax * 2;

            btnNo.style.transform = `translate(${randomX}px, ${randomY}px) scale(${0.9})`;

            hint.innerText = escapeHints[escapeCount % escapeHints.length];
            escapeCount++;
        }

        function answerQ4() {
            playSound('win');
            
            // Big confetti explosion
            const duration = 3 * 1000;
            const animationEnd = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 5,
                    angle: 60,
                    spread: 55,
                    origin: { x: 0 },
                    colors: ['#ff4d4d', '#ff758c', '#ffffff', '#ffd700']
                });
                confetti({
                    particleCount: 5,
                    angle: 120,
                    spread: 55,
                    origin: { x: 1 },
                    colors: ['#ff4d4d', '#ff758c', '#ffffff', '#ffd700']
                });

                if (Date.now() < animationEnd) {
                    requestAnimationFrame(frame);
                }
            })();

            document.getElementById('quiz-container').classList.add('hidden');
            document.getElementById('screen-end').classList.remove('hidden');
        }

        function restartQuiz() {
            playSound('pop');
            
            // Reset Escaping Button
            const btnNo = document.getElementById('btn-no');
            btnNo.style.transform = 'none';
            escapeCount = 0;
            document.getElementById('escape-hint').innerText = '';

            // Reset screens
            document.getElementById('screen-end').classList.add('hidden');
            document.getElementById('q1').classList.remove('hidden');
            document.getElementById('q2').classList.add('hidden');
            document.getElementById('q3').classList.add('hidden');
            document.getElementById('q4').classList.add('hidden');

            document.getElementById('screen-welcome').classList.remove('hidden');
        }

        function sendLove() {
            playSound('win');
            confetti({
                particleCount: 100,
                spread: 100,
                origin: { y: 0.5 }
            });
            showModal('💋❤️', 'Bisou envoyé !', 'Ammar a bien reçu ton bisou virtuel ! Merci d\'être la personne fantastique que tu es au quotidien. 🥰');
        }
    </script>
</body>
</html>
