# Los_racioinales_en_la_selva_by_ElkinArteaga.html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Aventura Amazónica: Exploradores de Números</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Comic Sans MS', cursive, Arial, sans-serif;
            background: linear-gradient(135deg, #1a4d2e 0%, #2d5a3d 50%, #0f3a1f 100%);
            min-height: 100vh;
            color: #fff;
            overflow-x: hidden;
            position: relative;
        }

        /* Animaciones de fondo */
        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .leaf {
            position: absolute;
            font-size: 20px;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(10deg); }
        }

        /* Header */
        .header {
            background: rgba(0,0,0,0.3);
            padding: 15px;
            text-align: center;
            backdrop-filter: blur(10px);
            border-bottom: 3px solid #4CAF50;
        }

        .title {
            font-size: clamp(18px, 5vw, 28px);
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            color: #4CAF50;
        }

        .subtitle {
            font-size: clamp(12px, 3vw, 16px);
            opacity: 0.9;
            margin-top: 5px;
        }

        /* Pantalla de inicio */
        .start-screen {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: calc(100vh - 120px);
            padding: 20px;
            text-align: center;
        }

        .explorer-name {
            background: rgba(255,255,255,0.1);
            border: 2px solid #4CAF50;
            border-radius: 15px;
            padding: 15px;
            font-size: 18px;
            color: #fff;
            text-align: center;
            width: 100%;
            max-width: 300px;
            margin: 20px 0;
            backdrop-filter: blur(10px);
        }

        .explorer-name::placeholder {
            color: rgba(255,255,255,0.7);
        }

        .start-btn {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            border: none;
            border-radius: 25px;
            padding: 15px 40px;
            font-size: 20px;
            font-weight: bold;
            color: white;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            transition: all 0.3s;
            margin-top: 20px;
            min-height: 50px;
        }

        .start-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 7px 20px rgba(0,0,0,0.4);
        }

        /* Nivel selector */
        .level-selector {
            display: none;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
        }

        .levels-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .level-card {
            background: rgba(255,255,255,0.1);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            backdrop-filter: blur(10px);
            border: 2px solid transparent;
            transition: all 0.3s;
            cursor: pointer;
            min-height: 150px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .level-card:hover {
            border-color: #4CAF50;
            transform: translateY(-3px);
            box-shadow: 0 5px 20px rgba(76, 175, 80, 0.3);
        }

        .level-icon {
            font-size: 40px;
            margin-bottom: 10px;
        }

        .level-title {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 10px;
            color: #4CAF50;
        }

        .level-progress {
            font-size: 14px;
            opacity: 0.8;
        }

        .completed {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.2);
        }

        /* Pantalla de juego */
        .game-screen {
            display: none;
            padding: 20px;
            max-width: 600px;
            margin: 0 auto;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .level-info {
            font-size: 16px;
            font-weight: bold;
            color: #4CAF50;
        }

        .progress-info {
            font-size: 14px;
            text-align: center;
        }

        .back-btn {
            background: rgba(244, 67, 54, 0.8);
            border: none;
            border-radius: 20px;
            padding: 8px 15px;
            color: white;
            cursor: pointer;
            font-size: 14px;
            min-height: 40px;
        }

        .problem-container {
            background: rgba(255,255,255,0.1);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 20px;
            backdrop-filter: blur(10px);
            text-align: center;
        }

        .problem-text {
            font-size: clamp(16px, 4vw, 20px);
            line-height: 1.6;
            margin-bottom: 20px;
            text-align: left;
        }

        .math-expression {
            font-size: clamp(20px, 5vw, 28px);
            font-weight: bold;
            color: #4CAF50;
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 10px;
            margin: 15px 0;
            font-family: 'Courier New', monospace;
        }

        .answer-input {
            width: 100%;
            max-width: 200px;
            padding: 15px;
            font-size: 20px;
            text-align: center;
            border: 2px solid #4CAF50;
            border-radius: 15px;
            background: rgba(255,255,255,0.1);
            color: #fff;
            backdrop-filter: blur(10px);
            margin: 20px 0;
        }

        .answer-input::placeholder {
            color: rgba(255,255,255,0.7);
        }

        .submit-btn {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            border: none;
            border-radius: 25px;
            padding: 15px 30px;
            font-size: 18px;
            font-weight: bold;
            color: white;
            cursor: pointer;
            margin: 10px;
            transition: all 0.3s;
            min-height: 50px;
            min-width: 120px;
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .submit-btn:disabled {
            opacity: 0.6;
            transform: none;
            cursor: not-allowed;
        }

        .feedback {
            margin-top: 20px;
            padding: 15px;
            border-radius: 15px;
            font-size: 16px;
            font-weight: bold;
            text-align: center;
            transition: all 0.5s;
        }

        .correct {
            background: rgba(76, 175, 80, 0.8);
            color: white;
        }

        .incorrect {
            background: rgba(244, 67, 54, 0.8);
            color: white;
        }

        /* Pantalla de completado */
        .completion-screen {
            display: none;
            text-align: center;
            padding: 40px 20px;
            max-width: 600px;
            margin: 0 auto;
        }

        .completion-icon {
            font-size: 80px;
            margin-bottom: 20px;
            animation: bounce 1s infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-20px); }
            60% { transform: translateY(-10px); }
        }

        .completion-text {
            font-size: 24px;
            margin-bottom: 30px;
            color: #4CAF50;
        }

        .final-stats {
            background: rgba(255,255,255,0.1);
            border-radius: 15px;
            padding: 25px;
            margin: 20px 0;
            backdrop-filter: blur(10px);
        }

        .continue-btn {
            background: linear-gradient(45deg, #2196F3, #1976D2);
            border: none;
            border-radius: 25px;
            padding: 15px 30px;
            font-size: 18px;
            font-weight: bold;
            color: white;
            cursor: pointer;
            margin: 10px;
            min-height: 50px;
        }

        /* Responsivo */
        @media (max-width: 480px) {
            .game-header {
                flex-direction: column;
                text-align: center;
            }
            
            .levels-grid {
                grid-template-columns: 1fr;
            }
            
            .math-expression {
                font-size: 18px;
            }
        }

        /* Progress bar */
        .progress-bar {
            width: 100%;
            height: 10px;
            background: rgba(255,255,255,0.2);
            border-radius: 5px;
            overflow: hidden;
            margin: 10px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(45deg, #4CAF50, #45a049);
            transition: width 0.5s ease;
            border-radius: 5px;
        }

        /* Fraction display */
        .fraction {
            display: inline-block;
            vertical-align: middle;
            text-align: center;
        }

        .fraction .numerator {
            display: block;
            border-bottom: 1px solid currentColor;
            padding-bottom: 2px;
        }

        .fraction .denominator {
            display: block;
            padding-top: 2px;
        }
    </style>
</head>
<body>
    <!-- Animaciones de fondo -->
    <div class="bg-animation" id="bgAnimation"></div>
    
    <!-- Header -->
    <div class="header">
        <div class="title">🌿 Aventura Amazónica: Exploradores de Números 🌊</div>
        <div class="subtitle">Descubre los secretos de los números racionales en la selva amazónica</div>
    </div>

    <!-- Pantalla de inicio -->
    <div class="start-screen" id="startScreen">
        <div style="font-size: 60px; margin-bottom: 20px;">🦜🌿🐆</div>
        <h2 style="margin-bottom: 20px;">¡Bienvenido, Explorador!</h2>
        <p style="font-size: 16px; text-align: center; margin-bottom: 20px; opacity: 0.9;">
            Únete a una expedición única por la Amazonía donde deberás resolver desafíos matemáticos 
            para descubrir los secretos ocultos de la selva y explorar las profundidades de los ríos.
        </p>
        <input type="text" class="explorer-name" id="explorerName" placeholder="Escribe tu nombre, explorador..." maxlength="20">
        <button class="start-btn" onclick="startAdventure()">🚀 Comenzar Aventura</button>
    </div>

    <!-- Selector de niveles -->
    <div class="level-selector" id="levelSelector">
        <h2 style="text-align: center; margin-bottom: 10px;">Selecciona tu Misión</h2>
        <p style="text-align: center; opacity: 0.8; margin-bottom: 30px;">Todos los niveles están disponibles. ¡Completa cada misión para convertirte en un Maestro Explorador!</p>
        
        <div class="levels-grid">
            <div class="level-card" onclick="startLevel(1)">
                <div>
                    <div class="level-icon">➕</div>
                    <div class="level-title">Nivel 1: El Sendero de las Sumas</div>
                    <p style="font-size: 14px; opacity: 0.8;">Encuentra plantas medicinales sumando fracciones</p>
                </div>
                <div class="level-progress" id="progress1">0/12 completados</div>
            </div>

            <div class="level-card" onclick="startLevel(2)">
                <div>
                    <div class="level-icon">➖</div>
                    <div class="level-title">Nivel 2: El Río de las Restas</div>
                    <p style="font-size: 14px; opacity: 0.8;">Navega el río restando fracciones</p>
                </div>
                <div class="level-progress" id="progress2">0/12 completados</div>
            </div>

            <div class="level-card" onclick="startLevel(3)">
                <div>
                    <div class="level-icon">✖️</div>
                    <div class="level-title">Nivel 3: El Bosque de las Multiplicaciones</div>
                    <p style="font-size: 14px; opacity: 0.8;">Descubre especies multiplicando fracciones</p>
                </div>
                <div class="level-progress" id="progress3">0/12 completados</div>
            </div>

            <div class="level-card" onclick="startLevel(4)">
                <div>
                    <div class="level-icon">➗</div>
                    <div class="level-title">Nivel 4: Las Cataratas de las Divisiones</div>
                    <p style="font-size: 14px; opacity: 0.8;">Explora cascadas dividiendo fracciones</p>
                </div>
                <div class="level-progress" id="progress4">0/12 completados</div>
            </div>

            <div class="level-card" onclick="startLevel(5)">
                <div>
                    <div class="level-icon">🏆</div>
                    <div class="level-title">DESAFÍO FINAL: El Templo Perdido</div>
                    <p style="font-size: 14px; opacity: 0.8;">Operaciones mixtas con decimales y fracciones</p>
                </div>
                <div class="level-progress" id="progress5">0/12 completados</div>
            </div>
        </div>

        <div style="text-align: center; margin-top: 30px;">
            <button class="continue-btn" onclick="showCertificate()" id="certificateBtn" style="display: none;">
                🎖️ Ver Certificado de Maestro Explorador
            </button>
        </div>
    </div>

    <!-- Pantalla de juego -->
    <div class="game-screen" id="gameScreen">
        <div class="game-header">
            <div class="level-info" id="levelInfo">Nivel 1: El Sendero de las Sumas</div>
            <div class="progress-info">
                <div id="questionCounter">Pregunta 1 de 15</div>
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill" style="width: 0%"></div>
                </div>
                <div id="scoreInfo">Correctas: 0/12 necesarias</div>
            </div>
            <button class="back-btn" onclick="backToLevels()">← Volver</button>
        </div>

        <div class="problem-container">
            <div class="problem-text" id="problemText"></div>
            <div class="math-expression" id="mathExpression"></div>
            <div style="text-align: center;">
                <input type="number" step="any" class="answer-input" id="answerInput" placeholder="Tu respuesta">
                <div>
                    <button class="submit-btn" onclick="checkAnswer()" id="submitBtn">Verificar</button>
                    <button class="submit-btn" onclick="nextQuestion()" id="nextBtn" style="display: none;">Siguiente →</button>
                </div>
            </div>
            <div class="feedback" id="feedback"></div>
        </div>
    </div>

    <!-- Pantalla de completado -->
    <div class="completion-screen" id="completionScreen">
        <div class="completion-icon">🎉</div>
        <div class="completion-text" id="completionText"></div>
        <div class="final-stats" id="finalStats"></div>
        <div>
            <button class="continue-btn" onclick="backToLevels()">🔄 Continuar Explorando</button>
        </div>
    </div>

    <script>
        // Variables globales
        let currentLevel = 1;
        let currentQuestion = 1;
        let correctAnswers = 0;
        let currentAnswer = 0;
        let explorerName = '';
        let levelProgress = {1: 0, 2: 0, 3: 0, 4: 0, 5: 0};

        // Función para crear animaciones de fondo
        function createBackgroundAnimations() {
            const bgAnimation = document.getElementById('bgAnimation');
            const leaves = ['🌿', '🍃', '🦋', '🐛', '🌸'];
            
            for(let i = 0; i < 15; i++) {
                const leaf = document.createElement('div');
                leaf.className = 'leaf';
                leaf.innerHTML = leaves[Math.floor(Math.random() * leaves.length)];
                leaf.style.left = Math.random() * 100 + '%';
                leaf.style.animationDelay = Math.random() * 6 + 's';
                leaf.style.animationDuration = (4 + Math.random() * 4) + 's';
                bgAnimation.appendChild(leaf);
            }
        }

        // Función para iniciar la aventura
        function startAdventure() {
            const nameInput = document.getElementById('explorerName');
            if(nameInput.value.trim() === '') {
                alert('¡No olvides escribir tu nombre, explorador!');
                return;
            }
            
            explorerName = nameInput.value.trim();
            document.getElementById('startScreen').style.display = 'none';
            document.getElementById('levelSelector').style.display = 'block';
            updateProgressDisplay();
        }

        // Función para actualizar la visualización del progreso
        function updateProgressDisplay() {
            for(let i = 1; i <= 5; i++) {
                const progressElement = document.getElementById(`progress${i}`);
                const levelCard = progressElement.parentElement.parentElement;
                
                if(levelProgress[i] >= 12) {
                    progressElement.textContent = '✅ COMPLETADO';
                    levelCard.classList.add('completed');
                } else {
                    progressElement.textContent = `${levelProgress[i]}/12 completados`;
                }
            }

            // Mostrar botón de certificado si todos los niveles están completados
            const allCompleted = Object.values(levelProgress).every(p => p >= 12);
            document.getElementById('certificateBtn').style.display = allCompleted ? 'block' : 'none';
        }

        // Función para iniciar un nivel
        function startLevel(level) {
            currentLevel = level;
            currentQuestion = 1;
            correctAnswers = 0;
            
            document.getElementById('levelSelector').style.display = 'none';
            document.getElementById('gameScreen').style.display = 'block';
            
            updateGameHeader();
            generateQuestion();
        }

        // Función para actualizar el header del juego
        function updateGameHeader() {
            const levelNames = {
                1: "Nivel 1: El Sendero de las Sumas",
                2: "Nivel 2: El Río de las Restas", 
                3: "Nivel 3: El Bosque de las Multiplicaciones",
                4: "Nivel 4: Las Cataratas de las Divisiones",
                5: "DESAFÍO FINAL: El Templo Perdido"
            };
            
            document.getElementById('levelInfo').textContent = levelNames[currentLevel];
            document.getElementById('questionCounter').textContent = `Pregunta ${currentQuestion} de 15`;
            document.getElementById('scoreInfo').textContent = `Correctas: ${correctAnswers}/12 necesarias`;
            
            const progress = (currentQuestion - 1) / 15 * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        // Función para generar fracciones aleatorias
        function generateFraction(positive = true, simple = true) {
            let numerators, denominators;
            
            if (simple) {
                numerators = [1, 2, 3, 4, 5, 6, 7, 8, 9];
                denominators = [2, 3, 4, 5, 6, 8, 9, 10, 12];
            } else {
                numerators = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15];
                denominators = [2, 3, 4, 5, 6, 7, 8, 9, 10, 12, 15, 16, 18, 20];
            }
            
            let num = numerators[Math.floor(Math.random() * numerators.length)];
            let den = denominators[Math.floor(Math.random() * denominators.length)];
            
            // Asegurar que la fracción no sea impropia para casos simples
            if (simple && num >= den) {
                num = Math.max(1, den - 1);
            }
            
            // Aplicar signo negativo si es necesario
            if (!positive && Math.random() < 0.5) {
                num = -num;
            }
            
            return {numerator: num, denominator: den};
        }

        // Función para simplificar fracciones
        function gcd(a, b) {
            a = Math.abs(a);
            b = Math.abs(b);
            while (b !== 0) {
                let temp = b;
                b = a % b;
                a = temp;
            }
            return a;
        }

        function simplifyFraction(num, den) {
            const divisor = gcd(num, den);
            return {
                numerator: num / divisor,
                denominator: den / divisor
            };
        }

        // Función para convertir fracción a decimal
        function fractionToDecimal(num, den, precision = 4) {
            return Math.round((num / den) * Math.pow(10, precision)) / Math.pow(10, precision);
        }

        // Función para generar preguntas según el nivel
        function generateQuestion() {
            document.getElementById('answerInput').value = '';
            document.getElementById('feedback').textContent = '';
            document.getElementById('submitBtn').style.display = 'inline-block';
            document.getElementById('nextBtn').style.display = 'none';
            document.getElementById('submitBtn').disabled = false;

            let problemText, mathExpression, answer;

            switch(currentLevel) {
                case 1: // Sumas
                    ({problemText, mathExpression, answer} = generateAdditionProblem());
                    break;
                case 2: // Restas
                    ({problemText, mathExpression, answer} = generateSubtractionProblem());
                    break;
                case 3: // Multiplicaciones
                    ({problemText, mathExpression, answer} = generateMultiplicationProblem());
                    break;
                case 4: // Divisiones
                    ({problemText, mathExpression, answer} = generateDivisionProblem());
                    break;
                case 5: // Desafío final
                    ({problemText, mathExpression, answer} = generateFinalChallenge());
                    break;
            }

            document.getElementById('problemText').innerHTML = problemText;
            document.getElementById('mathExpression').innerHTML = mathExpression;
            currentAnswer = answer;

            // Verificación triple del cálculo
            console.log(`Pregunta ${currentQuestion}, Respuesta esperada: ${answer}`);
        }

        // Problemas de suma
        function generateAdditionProblem() {
            const contexts = [
                "Un biólogo encontró {frac1} de especies nuevas de mariposas en la mañana y {frac2} en la tarde.",
                "Una exploradora recolectó {frac1} de su capacidad de muestras de agua y luego {frac2} más.",
                "Un equipo de investigación fotografió {frac1} de las aves del área y después {frac2} adicionales.",
                "Los botánicos catalogaron {frac1} de las plantas medicinales y más tarde {frac2} más.",
                "Un grupo encontró {frac1} del tesoro escondido por la mañana y {frac2} por la tarde."
            ];

            const frac1 = generateFraction();
            const frac2 = generateFraction();
            
            const context = contexts[Math.floor(Math.random() * contexts.length)];
            const problemText = context
                .replace('{frac1}', `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span>`)
                .replace('{frac2}', `<span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span>`) + 
                " ¿Cuál es el total que encontraron?";

            const mathExpression = `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span> + <span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span> = ?`;

            // Triple verificación del cálculo
            const commonDen = frac1.denominator * frac2.denominator;
            const num1 = frac1.numerator * frac2.denominator;
            const num2 = frac2.numerator * frac1.denominator;
            const resultNum = num1 + num2;
            
            const simplified = simplifyFraction(resultNum, commonDen);
            const answer = fractionToDecimal(simplified.numerator, simplified.denominator);

            // Verificaciones
            console.log(`Suma verificación 1: ${frac1.numerator}/${frac1.denominator} + ${frac2.numerator}/${frac2.denominator}`);
            console.log(`Suma verificación 2: ${num1}/${commonDen} + ${num2}/${commonDen} = ${resultNum}/${commonDen}`);
            console.log(`Suma verificación 3: Simplificado = ${simplified.numerator}/${simplified.denominator} = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        // Problemas de resta
        function generateSubtractionProblem() {
            const contexts = [
                "Un explorador tenía {frac1} de provisiones y gastó {frac2} durante la expedición.",
                "Una bióloga marina observó {frac1} de las especies y {frac2} se alejaron nadando.",
                "Los investigadores tenían {frac1} de combustible y consumieron {frac2} en el viaje.",
                "Un equipo recolectó {frac1} de muestras de suelo pero perdió {frac2} en el río.",
                "Los exploradores habían recorrido {frac1} del sendero y retrocedieron {frac2}."
            ];

            let frac1, frac2;
            
            // Asegurar que frac1 > frac2 para resultado positivo
            do {
                frac1 = generateFraction();
                frac2 = generateFraction();
            } while (frac1.numerator * frac2.denominator <= frac2.numerator * frac1.denominator);

            const context = contexts[Math.floor(Math.random() * contexts.length)];
            const problemText = context
                .replace('{frac1}', `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span>`)
                .replace('{frac2}', `<span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span>`) + 
                " ¿Cuánto le queda?";

            const mathExpression = `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span> - <span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span> = ?`;

            // Triple verificación del cálculo
            const commonDen = frac1.denominator * frac2.denominator;
            const num1 = frac1.numerator * frac2.denominator;
            const num2 = frac2.numerator * frac1.denominator;
            const resultNum = num1 - num2;
            
            const simplified = simplifyFraction(resultNum, commonDen);
            const answer = fractionToDecimal(simplified.numerator, simplified.denominator);

            // Verificaciones
            console.log(`Resta verificación 1: ${frac1.numerator}/${frac1.denominator} - ${frac2.numerator}/${frac2.denominator}`);
            console.log(`Resta verificación 2: ${num1}/${commonDen} - ${num2}/${commonDen} = ${resultNum}/${commonDen}`);
            console.log(`Resta verificación 3: Simplificado = ${simplified.numerator}/${simplified.denominator} = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        // Problemas de multiplicación
        function generateMultiplicationProblem() {
            const contexts = [
                "Un área de la selva tiene {frac1} de biodiversidad y se expandió {frac2} veces.",
                "Una planta medicinal crece {frac1} metros por día durante {frac2} días.",
                "Los investigadores encontraron {frac1} de las especies esperadas en {frac2} de la zona explorada.",
                "Un río transporta {frac1} toneladas de sedimento y aumenta {frac2} veces en temporada lluviosa.",
                "Una comunidad indígena usa {frac1} de sus plantas medicinales {frac2} veces al mes."
            ];

            const frac1 = generateFraction();
            const frac2 = generateFraction();
            
            const context = contexts[Math.floor(Math.random() * contexts.length)];
            const problemText = context
                .replace('{frac1}', `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span>`)
                .replace('{frac2}', `<span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span>`) + 
                " ¿Cuál es el resultado total?";

            const mathExpression = `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span> × <span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span> = ?`;

            // Triple verificación del cálculo
            const resultNum = frac1.numerator * frac2.numerator;
            const resultDen = frac1.denominator * frac2.denominator;
            
            const simplified = simplifyFraction(resultNum, resultDen);
            const answer = fractionToDecimal(simplified.numerator, simplified.denominator);

            // Verificaciones
            console.log(`Multiplicación verificación 1: ${frac1.numerator}/${frac1.denominator} × ${frac2.numerator}/${frac2.denominator}`);
            console.log(`Multiplicación verificación 2: ${resultNum}/${resultDen}`);
            console.log(`Multiplicación verificación 3: Simplificado = ${simplified.numerator}/${simplified.denominator} = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        // Problemas de división
        function generateDivisionProblem() {
            const contexts = [
                "Un equipo de {frac2} investigadores debe repartirse {frac1} de las muestras recolectadas.",
                "Una reserva natural de {frac1} hectáreas se divide en {frac2} de sección para cada especie.",
                "Los biólogos tienen {frac1} kilogramos de alimento para animales que dura {frac2} días.",
                "Una expedición recorre {frac1} del territorio en {frac2} parte del tiempo planeado.",
                "Los científicos dividen {frac1} de sus descubrimientos entre {frac2} de los laboratorios."
            ];

            const frac1 = generateFraction();
            let frac2 = generateFraction();
            
            // Asegurar que no dividamos por cero
            if (frac2.numerator === 0) frac2.numerator = 1;
            
            const context = contexts[Math.floor(Math.random() * contexts.length)];
            const problemText = context
                .replace('{frac1}', `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span>`)
                .replace('{frac2}', `<span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span>`) + 
                " ¿Cuánto corresponde a cada parte?";

            const mathExpression = `<span class="fraction"><span class="numerator">${frac1.numerator}</span><span class="denominator">${frac1.denominator}</span></span> ÷ <span class="fraction"><span class="numerator">${frac2.numerator}</span><span class="denominator">${frac2.denominator}</span></span> = ?`;

            // Triple verificación del cálculo (a/b ÷ c/d = a/b × d/c)
            const resultNum = frac1.numerator * frac2.denominator;
            const resultDen = frac1.denominator * frac2.numerator;
            
            const simplified = simplifyFraction(resultNum, resultDen);
            const answer = fractionToDecimal(simplified.numerator, simplified.denominator);

            // Verificaciones
            console.log(`División verificación 1: ${frac1.numerator}/${frac1.denominator} ÷ ${frac2.numerator}/${frac2.denominator}`);
            console.log(`División verificación 2: ${frac1.numerator}/${frac1.denominator} × ${frac2.denominator}/${frac2.numerator} = ${resultNum}/${resultDen}`);
            console.log(`División verificación 3: Simplificado = ${simplified.numerator}/${simplified.denominator} = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        // Desafío final con operaciones mixtas, decimales y números mixtos
        function generateFinalChallenge() {
            const challenges = [
                () => generateMixedOperationProblem(),
                () => generateDecimalProblem(),
                () => generateMixedNumberProblem(),
                () => generateComplexProblem()
            ];

            const challengeType = Math.floor(Math.random() * challenges.length);
            return challenges[challengeType]();
        }

        function generateMixedOperationProblem() {
            const problemText = "🏛️ En el templo perdido, un explorador encuentra tres cámaras con tesoros: " +
                "la primera contiene <span class=\"fraction\"><span class=\"numerator\">3</span><span class=\"denominator\">4</span></span> de oro, " +
                "la segunda <span class=\"fraction\"><span class=\"numerator\">2</span><span class=\"denominator\">5</span></span> de oro, " +
                "y en la tercera pierde <span class=\"fraction\"><span class=\"numerator\">1</span><span class=\"denominator\">3</span></span> del total encontrado. " +
                "¿Cuánto oro tiene al final?";

            const mathExpression = "(<span class=\"fraction\"><span class=\"numerator\">3</span><span class=\"denominator\">4</span></span> + <span class=\"fraction\"><span class=\"numerator\">2</span><span class=\"denominator\">5</span></span>) - <span class=\"fraction\"><span class=\"numerator\">1</span><span class=\"denominator\">3</span></span> × (<span class=\"fraction\"><span class=\"numerator\">3</span><span class=\"denominator\">4</span></span> + <span class=\"fraction\"><span class=\"numerator\">2</span><span class=\"denominator\">5</span></span>)";

            // Triple verificación
            // Paso 1: 3/4 + 2/5 = 15/20 + 8/20 = 23/20
            const sum = fractionToDecimal(23, 20); // 1.15
            
            // Paso 2: 1/3 × 23/20 = 23/60
            const loss = fractionToDecimal(23, 60); // ≈ 0.3833
            
            // Paso 3: 23/20 - 23/60 = 69/60 - 23/60 = 46/60 = 23/30
            const answer = fractionToDecimal(23, 30); // ≈ 0.7667

            console.log(`Desafío mixto verificación 1: 3/4 + 2/5 = ${sum}`);
            console.log(`Desafío mixto verificación 2: pérdida = 1/3 × ${sum} = ${loss}`);
            console.log(`Desafío mixto verificación 3: resultado = ${sum} - ${loss} = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        function generateDecimalProblem() {
            const decimals = [0.25, 0.5, 0.75, 1.25, 1.5, 2.25, 0.125, 0.375, 0.625, 0.875];
            const dec1 = decimals[Math.floor(Math.random() * decimals.length)];
            const dec2 = decimals[Math.floor(Math.random() * decimals.length)];

            const problemText = `🌊 Un biólogo marino mide la profundidad de dos pozas: la primera tiene ${dec1} metros de profundidad y la segunda ${dec2} metros. Si la diferencia entre ellas se multiplica por 1.5, ¿cuál es el resultado?`;

            const mathExpression = `|${dec1} - ${dec2}| × 1.5 = ?`;

            const difference = Math.abs(dec1 - dec2);
            const answer = difference * 1.5;

            console.log(`Decimales verificación 1: |${dec1} - ${dec2}| = ${difference}`);
            console.log(`Decimales verificación 2: ${difference} × 1.5 = ${answer}`);
            console.log(`Decimales verificación 3: confirmado = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        function generateMixedNumberProblem() {
            const problemText = "🦋 Una investigadora observa mariposas durante 2¼ horas en la mañana y 1¾ horas en la tarde. Si cada hora registra en promedio ⅝ de especies nuevas, ¿cuántas especies nuevas registró en total?";

            const mathExpression = "(2¼ + 1¾) × ⅝ = ?";

            // Convertir números mixtos a fracciones impropias
            // 2¼ = 9/4, 1¾ = 7/4
            const time1 = fractionToDecimal(9, 4); // 2.25
            const time2 = fractionToDecimal(7, 4); // 1.75
            const totalTime = time1 + time2; // 4.0
            const rate = fractionToDecimal(5, 8); // 0.625
            const answer = totalTime * rate; // 2.5

            console.log(`Números mixtos verificación 1: 2¼ + 1¾ = ${time1} + ${time2} = ${totalTime}`);
            console.log(`Números mixtos verificación 2: ${totalTime} × ⅝ = ${totalTime} × ${rate} = ${answer}`);
            console.log(`Números mixtos verificación 3: confirmado = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        function generateComplexProblem() {
            const problemText = "🏛️ El tesoro final del templo se reparte así: ⅓ para el museo, ¼ para la comunidad indígena, y el resto se divide equitativamente entre los 5 exploradores. ¿Qué fracción del tesoro total recibe cada explorador?";

            const mathExpression = "(1 - ⅓ - ¼) ÷ 5 = ?";

            // Triple verificación
            // 1 - 1/3 - 1/4 = 12/12 - 4/12 - 3/12 = 5/12
            const remaining = fractionToDecimal(5, 12); // ≈ 0.4167
            
            // 5/12 ÷ 5 = 5/12 × 1/5 = 1/12
            const answer = fractionToDecimal(1, 12); // ≈ 0.0833

            console.log(`Complejo verificación 1: 1 - 1/3 - 1/4 = ${remaining}`);
            console.log(`Complejo verificación 2: ${remaining} ÷ 5 = ${answer}`);
            console.log(`Complejo verificación 3: 1/12 = ${answer}`);

            return {problemText, mathExpression, answer};
        }

        // Función para verificar respuesta
        function checkAnswer() {
            const userAnswer = parseFloat(document.getElementById('answerInput').value);
            const feedback = document.getElementById('feedback');
            const tolerance = 0.01; // Tolerancia para decimales

            if (isNaN(userAnswer)) {
                feedback.innerHTML = "⚠️ Por favor ingresa un número válido";
                feedback.className = "feedback incorrect";
                return;
            }

            const isCorrect = Math.abs(userAnswer - currentAnswer) <= tolerance;

            if (isCorrect) {
                correctAnswers++;
                feedback.innerHTML = `🎉 ¡Correcto! La respuesta es ${currentAnswer}`;
                feedback.className = "feedback correct";
            } else {
                feedback.innerHTML = `❌ Incorrecto. La respuesta correcta es ${currentAnswer}`;
                feedback.className = "feedback incorrect";
            }

            document.getElementById('submitBtn').style.display = 'none';
            document.getElementById('nextBtn').style.display = 'inline-block';
            document.getElementById('submitBtn').disabled = true;

            updateGameHeader();
        }

        // Función para siguiente pregunta
        function nextQuestion() {
            if (currentQuestion < 15) {
                currentQuestion++;
                updateGameHeader();
                generateQuestion();
            } else {
                // Completar nivel
                levelProgress[currentLevel] = correctAnswers;
                showCompletionScreen();
            }
        }

        // Función para mostrar pantalla de completado
        function showCompletionScreen() {
            document.getElementById('gameScreen').style.display = 'none';
            document.getElementById('completionScreen').style.display = 'block';

            const levelNames = {
                1: "El Sendero de las Sumas",
                2: "El Río de las Restas", 
                3: "El Bosque de las Multiplicaciones",
                4: "Las Cataratas de las Divisiones",
                5: "El Templo Perdido"
            };

            let completionText, stats;

            if (correctAnswers >= 12) {
                completionText = `🎉 ¡Felicitaciones ${explorerName}!<br>Has completado: ${levelNames[currentLevel]}`;
                stats = `
                    <h3>🏆 ¡MISIÓN COMPLETADA!</h3>
                    <p><strong>Preguntas correctas:</strong> ${correctAnswers}/15</p>
                    <p><strong>Porcentaje de éxito:</strong> ${Math.round(correctAnswers/15*100)}%</p>
                    <p><strong>Estado:</strong> ✅ APROBADO</p>
                `;
            } else {
                completionText = `💪 ¡Buen intento ${explorerName}!<br>Necesitas más práctica en: ${levelNames[currentLevel]}`;
                stats = `
                    <h3>📚 Sigue intentando</h3>
                    <p><strong>Preguntas correctas:</strong> ${correctAnswers}/15</p>
                    <p><strong>Necesitas:</strong> ${12 - correctAnswers} respuestas más para aprobar</p>
                    <p><strong>Estado:</strong> ❌ Necesita más práctica</p>
                `;
            }

            document.getElementById('completionText').innerHTML = completionText;
            document.getElementById('finalStats').innerHTML = stats;
        }

        // Función para volver a niveles
        function backToLevels() {
            document.getElementById('gameScreen').style.display = 'none';
            document.getElementById('completionScreen').style.display = 'none';
            document.getElementById('levelSelector').style.display = 'block';
            updateProgressDisplay();
        }

        // Función para mostrar certificado
        function showCertificate() {
            const totalQuestions = Object.values(levelProgress).reduce((a, b) => a + b, 0);
            const certificate = `
                <div style="background: linear-gradient(135deg, #FFD700, #FFA500); color: #333; padding: 40px; border-radius: 20px; text-align: center; box-shadow: 0 10px 30px rgba(0,0,0,0.3);">
                    <h1 style="font-size: 28px; margin-bottom: 20px;">🏆 CERTIFICADO DE MAESTRO EXPLORADOR 🏆</h1>
                    <div style="font-size: 60px; margin: 20px 0;">🌿🦋🏛️</div>
                    <h2 style="margin: 20px 0;">Se certifica que</h2>
                    <h1 style="font-size: 32px; color: #2E7D32; margin: 20px 0; text-transform: uppercase;">${explorerName}</h1>
                    <h2 style="margin: 20px 0;">Ha completado exitosamente</h2>
                    <h3 style="color: #1565C0; margin: 15px 0;">LA AVENTURA AMAZÓNICA DE NÚMEROS RACIONALES</h3>
                    <div style="margin: 30px 0; font-size: 16px;">
                        <p><strong>Niveles completados:</strong> 5/5</p>
                        <p><strong>Problemas resueltos correctamente:</strong> ${totalQuestions}/75</p>
                        <p><strong>Porcentaje total:</strong> ${Math.round(totalQuestions/75*100)}%</p>
                        <p><strong>Especialidades dominadas:</strong></p>
                        <p>✅ Suma de fracciones • ✅ Resta de fracciones</p>
                        <p>✅ Multiplicación de fracciones • ✅ División de fracciones</p>
                        <p>✅ Operaciones mixtas con decimales</p>
                    </div>
                    <div style="margin-top: 30px; font-size: 14px; opacity: 0.8;">
                        <p>Fecha: ${new Date().toLocaleDateString()}</p>
                        <p>Aventura Amazónica: Exploradores de Números - Grados 6° y 7°</p>
                    </div>
                </div>
            `;

            document.getElementById('levelSelector').innerHTML = certificate + 
                '<div style="text-align: center; margin-top: 30px;"><button class="continue-btn" onclick="location.reload()">🔄 Nueva Aventura</button></div>';
        }

        // Función para manejar Enter en el input
        document.addEventListener('DOMContentLoaded', function() {
            createBackgroundAnimations();
            
            document.getElementById('answerInput').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    if (document.getElementById('submitBtn').style.display !== 'none') {
                        checkAnswer();
                    } else {
                        nextQuestion();
                    }
                }
            });

            document.getElementById('explorerName').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    startAdventure();
                }
            });
        });
    </script>
</body>
</html>
