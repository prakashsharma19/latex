<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>पर्यायवाची शब्द अभ्यास</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; background-color: #f8f8f8; }
        h1 { color: #333; }
        #modeSelection { margin-bottom: 20px; }
        .button { padding: 10px 20px; margin: 5px; font-size: 18px; cursor: pointer; border: none; border-radius: 5px; }
        .quiz-mode { background: #007bff; color: white; }
        .practice-mode { background: #28a745; color: white; }
        .flashcard { width: 300px; height: 200px; margin: 20px auto; display: flex; align-items: center; justify-content: center; font-size: 22px; background: white; border: 1px solid #ccc; border-radius: 10px; cursor: pointer; transition: transform 0.3s; }
        .hidden { display: none; }
        #flashcardContainer button { display: block; margin: 10px auto; padding: 10px 20px; font-size: 18px; border-radius: 5px; border: none; cursor: pointer; }
        .known { background: #28a745; color: white; }
        .unknown { background: #dc3545; color: white; }
        .option { display: block; margin: 10px auto; padding: 10px; width: 300px; font-size: 18px; cursor: pointer; background: #fff; border: 1px solid #ccc; border-radius: 5px; }
        .option:hover { background: #e0e0e0; }
        #result { font-size: 20px; margin-top: 20px; font-weight: bold; }
        #nextBtn { display: none; margin-top: 20px; padding: 10px 20px; font-size: 18px; background: #28a745; color: white; border: none; cursor: pointer; border-radius: 5px; }
        #progress { position: absolute; top: 10px; right: 10px; font-size: 18px; font-weight: bold; }
    </style>
</head>
<body>
    <h1>पर्यायवाची शब्द अभ्यास</h1>
    <div id="progress">Your Progress: 0/0</div>
    <div id="modeSelection">
        <button class="button practice-mode" onclick="startPractice()">प्रैक्टिस मोड</button>
        <button class="button quiz-mode" onclick="startQuiz()">टेस्ट मोड</button>
    </div>
    
    <div id="flashcardContainer" class="hidden">
        <div class="flashcard" onclick="flipCard()" id="flashcard">Loading...</div>
        <button class="known" onclick="markKnown()">✅ ज्ञात</button>
        <button class="unknown" onclick="markUnknown()">❌ अज्ञात</button>
    </div>
    
    <div id="quizContainer" class="hidden">
        <p id="question">Loading...</p>
        <div id="options"></div>
        <p id="result"></p>
        <button id="nextBtn" onclick="loadQuestion()">अगला प्रश्न</button>
    </div>
    
    <script>
        const words = [
            { word: "सूर्य", synonyms: ["भानु", "रवि", "दिनकर", "अर्क"] },
            { word: "चंद्र", synonyms: ["सोम", "शशि", "निशाकर", "इंदु"] },
            { word: "अग्नि", synonyms: ["पावक", "वह्नि", "अनल", "दहन"] }
        ];
        let practiceWords = JSON.parse(localStorage.getItem("practiceWords")) || [...words];
        let rememberedCount = parseInt(localStorage.getItem("rememberedCount")) || 0;
        document.getElementById("progress").textContent = `Your Progress: ${rememberedCount}/${words.length}`;
        let currentFlashcard = null;
        let showSynonyms = false;

        function startPractice() {
            document.getElementById("modeSelection").classList.add("hidden");
            document.getElementById("flashcardContainer").classList.remove("hidden");
            loadFlashcard();
        }
        
        function startQuiz() {
            document.getElementById("modeSelection").classList.add("hidden");
            document.getElementById("quizContainer").classList.remove("hidden");
            loadQuestion();
        }
        
        function loadFlashcard() {
            if (practiceWords.length === 0) {
                document.getElementById("flashcard").textContent = "सभी शब्द सीख लिए गए!";
                return;
            }
            currentFlashcard = practiceWords[Math.floor(Math.random() * practiceWords.length)];
            document.getElementById("flashcard").textContent = currentFlashcard.word;
            showSynonyms = false;
        }
        
        function flipCard() {
            if (!currentFlashcard) return;
            document.getElementById("flashcard").textContent = showSynonyms ? currentFlashcard.word : currentFlashcard.synonyms.join(", ");
            showSynonyms = !showSynonyms;
        }
        
        function markKnown() {
            practiceWords = practiceWords.filter(w => w.word !== currentFlashcard.word);
            rememberedCount++;
            localStorage.setItem("practiceWords", JSON.stringify(practiceWords));
            localStorage.setItem("rememberedCount", rememberedCount);
            document.getElementById("progress").textContent = `Your Progress: ${rememberedCount}/${words.length}`;
            loadFlashcard();
        }
        
        function markUnknown() {
            loadFlashcard();
        }
        
        function loadQuestion() {
            let wordObj = words[Math.floor(Math.random() * words.length)];
            let correctAnswer = wordObj.synonyms[0];
            let wrongAnswers = words.filter(w => w.word !== wordObj.word).slice(0, 3).map(w => w.synonyms[0]);
            let options = [correctAnswer, ...wrongAnswers].sort(() => Math.random() - 0.5);
            document.getElementById("question").textContent = `"${wordObj.word}" का पर्यायवाची क्या है?`;
            document.getElementById("options").innerHTML = options.map(option => `<button class="option" onclick="checkAnswer('${option}', '${correctAnswer}')">${option}</button>`).join('');
        }
        
        function checkAnswer(selected, correct) {
            document.getElementById("result").textContent = selected === correct ? "सही उत्तर!" : "गलत! सही उत्तर: " + correct;
            document.getElementById("nextBtn").style.display = "block";
        }
    </script>
</body>
</html>
