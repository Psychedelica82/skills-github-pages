<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz: Mediengestalter Digital</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Zusätzliches Styling für die Feedback-Farben */
        .correct {
            background-color: #16a34a; /* Green-600 */
            color: white;
            border-color: #15803d; /* Green-700 */
        }
        .incorrect {
            background-color: #dc2626; /* Red-600 */
            color: white;
            border-color: #b91c1c; /* Red-700 */
        }
        /* Inter Schriftart */
        body {
            font-family: 'Inter', sans-serif;
        }
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap');
    </style>
</head>
<body class="bg-gradient-to-br from-indigo-500 via-purple-500 to-pink-500 min-h-screen flex items-center justify-center p-4">

    <div class="w-full max-w-2xl bg-white rounded-2xl shadow-2xl p-6 md:p-10 transition-all duration-300">
        
        <!-- Quiz-Container -->
        <div id="quiz-container">
            <h1 class="text-2xl md:text-3xl font-bold text-center text-gray-800 mb-2">Quiz: Mediengestalter Digital</h1>
            <p class="text-center text-gray-500 mb-4">Basierend auf der Prüfungsstruktur (Anlage 2024-25)</p>
            <div id="progress-bar-container" class="w-full bg-gray-200 rounded-full h-2.5 mb-6 overflow-hidden">
                <div id="progress-bar" class="bg-indigo-600 h-2.5 rounded-full transition-all duration-500" style="width: 0%"></div>
            </div>
            
            <h2 id="question" class="text-xl md:text-2xl font-semibold text-gray-700 mb-6 min-h-[60px]">Frage wird geladen...</h2>
            
            <div id="answer-buttons" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                <!-- Antwort-Buttons werden hier dynamisch eingefügt -->
            </div>
            
            <button id="next-btn" class="w-full bg-indigo-600 text-white font-bold py-3 px-4 rounded-lg mt-8 text-lg hover:bg-indigo-700 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50 hidden">
                Nächste Frage
            </button>
        </div>

        <!-- Ergebnis-Container -->
        <div id="score-container" class="hidden text-center">
            <h2 class="text-3xl font-bold text-gray-800 mb-4">Quiz beendet!</h2>
            <p id="score-text" class="text-2xl text-gray-700 mb-8">Dein Ergebnis: 0 von 0</p>
            <button id="restart-btn" class="w-full bg-indigo-600 text-white font-bold py-3 px-4 rounded-lg text-lg hover:bg-indigo-700 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50">
                Erneut versuchen
            </button>
        </div>

    </div>

    <script>
        // --- QUIZ FRAGEN (Digital) ---
        // Basierend auf der PDF "Verordnung Mediengestalter 2024-25"
        const questions = [
            {
                // Thema: Konzeption & Gestaltung - Digital (U11)
                question: "Welche standardisierte Sprache wird zur Strukturierung von Webinhalten verwendet?",
                answers: [
                    { text: "CSS (Cascading Style Sheets)", correct: false },
                    { text: "HTML (HyperText Markup Language)", correct: true },
                    { text: "SQL (Structured Query Language)", correct: false },
                    { text: "JavaScript", correct: false }
                ]
            },
            {
                // Thema: Medienproduktion - Alle (U5)
                question: "Wofür steht 'Semantisches HTML'?",
                answers: [
                    { text: "HTML-Tags, die nur der Gestaltung dienen (z.B. <font>).", correct: false },
                    { text: "Eine veraltete Version von HTML.", correct: false },
                    { text: "Die Verwendung von HTML-Tags, die ihre Bedeutung beschreiben (z.B. <nav>, <article>).", correct: true },
                    { text: "Ein HTML-Dokument, das keine Fehler enthält.", correct: false }
                ]
            },
            {
                // Thema: Konzeption & Gestaltung - Digital (U10)
                question: "Welches HTML-Element eignet sich am besten für eine Dropdown-Auswahlliste in einem Formular?",
                answers: [
                    { text: "<input type='list'>", correct: false },
                    { text: "<dropdown>", correct: false },
                    { text: "<select>", correct: true },
                    { text: "<input type='dropdown'>", correct: false }
                ]
            },
            {
                // Thema: Konzeption & Gestaltung - Digital (U12)
                question: "Was bedeutet die Creative-Commons-Bedingung 'NC' (NonCommercial)?",
                answers: [
                    { text: "Das Werk darf nicht verändert werden.", correct: false },
                    { text: "Das Werk darf nur für nicht-kommerzielle Zwecke genutzt werden.", correct: true },
                    { text: "Der Urheber muss immer genannt werden.", correct: false },
                    { text: "Das Werk muss unter denselben Bedingungen weitergegeben werden.", correct: false }
                ]
            },
            {
                // Thema: Medienproduktion - Digital (U11)
                question: "Was ist ein typischer Vorteil von serverseitiger Bildausgabe?",
                answers: [
                    { text: "Sie belastet den Server überhaupt nicht.", correct: false },
                    { text: "Sie funktioniert auch, wenn der Nutzer JavaScript deaktiviert hat.", correct: true },
                    { text: "Sie ist immer schneller als clientseitige Bildausgabe.", correct: false },
                    { text: "Sie verbraucht mehr Bandbreite beim Nutzer.", correct: false }
                ]
            },
            {
                // Thema: Medienproduktion - Alle (U8)
                question: "Womit validiert man ein XML-Dokument auf seine strukturelle Korrektheit?",
                answers: [
                    { text: "Mit einer CSS-Datei.", correct: false },
                    { text: "Mit einem HTML-Validator.", correct: false },
                    { text: "Mit einer DTD (Document Type Definition) oder einem XSD (XML Schema).", correct: true },
                    { text: "Mit einer JavaScript-Konsolenprüfung.", correct: false }
                ]
            },
            {
                // Thema: Konzeption & Gestaltung - Alle (U5)
                question: "Welcher der folgenden Farbkontraste ist KEINER der sieben Farbkontraste nach Itten?",
                answers: [
                    { text: "Kalt-Warm-Kontrast", correct: false },
                    { text: "Hell-Dunkel-Kontrast", correct: false },
                    { text: "Simultankontrast", correct: false },
                    { text: "Digital-Analog-Kontrast", correct: true }
                ]
            },
            {
                // Thema: Medienproduktion - Alle (U4)
                question: "Was beschreibt eine 'Cross-Site Scripting' (XSS) Attacke?",
                answers: [
                    { text: "Das Einschleusen von bösartigem Code in eine Webseite, der im Browser eines Nutzers ausgeführt wird.", correct: true },
                    { text: "Das massenhafte Senden von Anfragen, um einen Server zu überlasten (DDoS).", correct: false },
                    { text: "Das Abfangen von Daten auf dem Übertragungsweg (Man-in-the-Middle).", correct: false },
                    { text: "Das Verändern von DNS-Einträgen.", correct: false }
                ]
            },
            {
                // Thema: Medienproduktion - Digital (U10)
                question: "Was ist ein 'Glyph' im typografischen Kontext?",
                answers: [
                    { text: "Ein Synonym für eine ganze Schriftart (Font).", correct: false },
                    { text: "Die spezifische grafische Darstellung eines Zeichens (z.B. 'A' in fett).", correct: true },
                    { text: "Der Abstand zwischen zwei Buchstaben (Kerning).", correct: false },
                    { text: "Ein Absatzformat in einem Layoutprogramm.", correct: false }
                ]
            },
            {
                // Thema: Konzeption & Gestaltung - Alle (U8)
                question: "Was ist ein 'Primärschlüssel' (Primary Key) in einem Datenbank-Entwurf?",
                answers: [
                    { text: "Ein Feld (oder Felder), das einen Datensatz eindeutig identifiziert.", correct: true },
                    { text: "Das Passwort für den Datenbankzugriff.", correct: false },
                    { text: "Der erste Datensatz, der in eine Tabelle eingefügt wurde.", correct: false },
                    { text: "Ein Index, der die Suche beschleunigt.", correct: false }
                ]
            }
        ];
        // --- ENDE DER FRAGEN ---

        // DOM-Elemente
        const quizContainer = document.getElementById('quiz-container');
        const scoreContainer = document.getElementById('score-container');
        const questionElement = document.getElementById('question');
        const answerButtonsElement = document.getElementById('answer-buttons');
        const nextButton = document.getElementById('next-btn');
        const restartButton = document.getElementById('restart-btn');
        const scoreText = document.getElementById('score-text');
        const progressBar = document.getElementById('progress-bar');

        // Quiz-Status
        let currentQuestionIndex = 0;
        let score = 0;
        let shuffledQuestions = [];

        // --- FUNKTIONEN ---

        function startQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            // Fragen mischen für mehr Abwechslung
            shuffledQuestions = questions.sort(() => Math.random() - 0.5);
            quizContainer.classList.remove('hidden');
            scoreContainer.classList.add('hidden');
            nextButton.classList.add('hidden');
            nextButton.textContent = 'Nächste Frage';
            updateProgressBar();
            showQuestion();
        }

        function showQuestion() {
            resetState();
            const currentQuestion = shuffledQuestions[currentQuestionIndex];
            questionElement.textContent = currentQuestion.question;

            // Antworten mischen
            const shuffledAnswers = currentQuestion.answers.sort(() => Math.random() - 0.5);

            shuffledAnswers.forEach(answer => {
                const button = document.createElement('button');
                button.textContent = answer.text;
                button.classList.add('w-full', 'border-2', 'border-gray-300', 'text-gray-700', 'font-semibold', 'py-3', 'px-4', 'rounded-lg', 'transition-all', 'duration-300', 'hover:bg-gray-100', 'hover:border-indigo-500');
                if (answer.correct) {
                    button.dataset.correct = answer.correct;
                }
                button.addEventListener('click', selectAnswer);
                answerButtonsElement.appendChild(button);
            });
        }

        function resetState() {
            nextButton.classList.add('hidden');
            while (answerButtonsElement.firstChild) {
                answerButtonsElement.removeChild(answerButtonsElement.firstChild);
            }
        }

        function selectAnswer(e) {
            const selectedButton = e.target;
            const isCorrect = selectedButton.dataset.correct === 'true';

            if (isCorrect) {
                score++;
                selectedButton.classList.add('correct');
            } else {
                selectedButton.classList.add('incorrect');
            }

            // Alle Buttons durchgehen und Feedback anzeigen
            Array.from(answerButtonsElement.children).forEach(button => {
                if (button.dataset.correct === 'true') {
                    if (!button.classList.contains('correct')) {
                        button.classList.add('correct');
                    }
                }
                button.disabled = true; // Buttons deaktivieren
            });

            // "Nächste Frage" oder "Ergebnisse" anzeigen
            if (shuffledQuestions.length > currentQuestionIndex + 1) {
                nextButton.textContent = 'Nächste Frage';
            } else {
                nextButton.textContent = 'Ergebnisse anzeigen';
            }
            nextButton.classList.remove('hidden');
        }

        function handleNextButton() {
            currentQuestionIndex++;
            if (currentQuestionIndex < shuffledQuestions.length) {
                updateProgressBar();
                showQuestion();
            } else {
                showScore();
            }
        }

        function showScore() {
            quizContainer.classList.add('hidden');
            scoreContainer.classList.remove('hidden');
            scoreText.textContent = `Dein Ergebnis: ${score} von ${shuffledQuestions.length}`;
            progressBar.style.width = '100%'; // Finaler Fortschritt
        }
        
        function updateProgressBar() {
            const progressPercentage = ((currentQuestionIndex) / shuffledQuestions.length) * 100;
            progressBar.style.width = `${progressPercentage}%`;
        }

        // --- EVENT LISTENERS ---
        nextButton.addEventListener('click', handleNextButton);
        restartButton.addEventListener('click', startQuiz);

        // Quiz beim Laden der Seite starten
        startQuiz();
    </script>
</body>
</html>


