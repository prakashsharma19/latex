<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>पर्यायवाची शब्द अभ्यास</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; background-color: #f8f8f8; }
        h1 { color: #333; }
        #question { font-size: 22px; margin: 20px 0; }
        .option { 
            display: block; margin: 10px auto; padding: 10px; width: 300px; 
            font-size: 18px; cursor: pointer; background: #fff; border: 1px solid #ccc; border-radius: 5px;
        }
        .option:hover { background: #e0e0e0; }
        #result { font-size: 20px; margin-top: 20px; font-weight: bold; }
        #nextBtn { 
            display: none; margin-top: 20px; padding: 10px 20px; font-size: 18px; 
            background: #28a745; color: white; border: none; cursor: pointer; border-radius: 5px; 
        }
    </style>
</head>
<body>

    <h1>पर्यायवाची शब्द अभ्यास</h1>
    <p id="question">Loading...</p>
    <div id="options"></div>
    <p id="result"></p>
    <button id="nextBtn" onclick="loadQuestion()">अगला प्रश्न</button>

    <script>
        const words = [
            { word: "सूर्य", synonyms: ["भानु", "रवि", "दिनकर", "अर्क"] },
            { word: "चंद्र", synonyms: ["सोम", "शशि", "निशाकर", "इंदु"] },
            { word: "अग्नि", synonyms: ["पावक", "वह्नि", "अनल", "दहन"] },
            { word: "जल", synonyms: ["नीर", "वारि", "तोय", "पय"] },
            { word: "पृथ्वी", synonyms: ["धरा", "भूमि", "वसुधा", "मही"] },
            { word: "हवा", synonyms: ["पवन", "वायु", "अनिल", "समीर"] },
            { word: "कमल", synonyms: ["पद्म", "अम्बुज", "सरोज", "नीरज"] },
            { word: "सिंह", synonyms: ["केशरी", "मृगेंद्र", "शेर", "व्याघ्र"] },
            { word: "हाथी", synonyms: ["गज", "द्विप", "मतंग", "हस्ति"] },
            { word: "सागर", synonyms: ["समुद्र", "अर्णव", "जलधि", "रत्नाकर"] },
            { word: "गंगा", synonyms: ["भागीरथी", "जाह्नवी", "पयस्विनी", "मंदाकिनी"] },
            { word: "अंधकार", synonyms: ["तम", "ध्वांत", "अवसान", "तिमिर"] },
            { word: "असुर", synonyms: ["दानव", "राक्षस", "निशाचर", "दैत्य"] },
            { word: "विद्या", synonyms: ["ज्ञान", "बुद्धि", "शिक्षा", "पाण्डित्य"] },
            { word: "स्वर्ग", synonyms: ["देवलोक", "सुरलोक", "बैखुंठ", "अमरावती"] },
            { word: "रात", synonyms: ["निशा", "रजनी", "यामिनी", "शर्वरी"] },
            { word: "अश्व", synonyms: ["घोड़ा", "हय", "तुरंग", "सप्ताश्व"] },
            { word: "नेत्र", synonyms: ["चक्षु", "नयन", "लोचन", "आंख"] },
            { word: "मृत्यु", synonyms: ["काल", "यम", "अंत", "मर"] },
            { word: "अन्न", synonyms: ["भोजन", "खाद्य", "धान्य", "शाक"] },
            { word: "हंस", synonyms: ["राजहंस", "कलहंस", "मराल", "पंक्षीराज"] }
        ];

        function getRandomIndex(array) {
            return Math.floor(Math.random() * array.length);
        }

        function shuffleArray(array) {
            return array.sort(() => Math.random() - 0.5);
        }

        function loadQuestion() {
            document.getElementById("result").textContent = "";
            document.getElementById("nextBtn").style.display = "none";

            let wordObj = words[getRandomIndex(words)];
            let correctAnswer = wordObj.synonyms[0];
            let wrongAnswers = [];

            while (wrongAnswers.length < 3) {
                let randomWord = words[getRandomIndex(words)];
                let randomSynonym = randomWord.synonyms[getRandomIndex(randomWord.synonyms)];
                if (randomSynonym !== correctAnswer && !wrongAnswers.includes(randomSynonym)) {
                    wrongAnswers.push(randomSynonym);
                }
            }

            let options = shuffleArray([correctAnswer, ...wrongAnswers]);

            document.getElementById("question").textContent = "${wordObj.word}" का पर्यायवाची क्या है?;
            let optionsHTML = "";
            options.forEach(option => {
                optionsHTML += <button class="option" onclick="checkAnswer('${option}', '${correctAnswer}')">${option}</button>;
            });

            document.getElementById("options").innerHTML = optionsHTML;
        }

        function checkAnswer(selected, correct) {
            if (selected === correct) {
                document.getElementById("result").textContent = "सही उत्तर!";
                document.getElementById("result").style.color = "green";
            } else {
                document.getElementById("result").textContent = "गलत! सही उत्तर: " + correct;
                document.getElementById("result").style.color = "red";
            }
            document.getElementById("nextBtn").style.display = "block";
        }

        loadQuestion();
    </script>

</body>
</html>
