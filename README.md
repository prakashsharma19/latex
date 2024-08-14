<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        /* Styles omitted for brevity */
    </style>
</head>
<body>
    <h1>Advertisements-PPH</h1>
    <div class="login-container">
        <input type="text" id="username" placeholder="Enter your name">
        <input type="password" id="password" placeholder="Enter your password">
        <button id="loginButton" onclick="login()">Login</button>
    </div>
    <div class="font-controls" style="display:none;">
        <!-- Font controls omitted for brevity -->
    </div>
    <div class="input-container" style="display:none;">
        <textarea id="inputText" rows="10" cols="50" placeholder="Paste your text here..."></textarea>
        <button id="okButton" onclick="processText()">OK</button>
    </div>
    <div id="adCount" style="display:none;">Total Advertisements: 0</div>
    <div id="dailyAdCount" style="display:none;">Total Ads Today: 0</div>
    <div id="remainingTime" style="display:none;">Remaining Time: <span id="time"></span><div class="hourglass"></div></div>
    <div id="countryCount" style="display:none;"></div>
    <button class="copy-button" style="display:none;" onclick="copyRemainingText()">Copy Remaining Text</button>
    <button class="copy-button" style="display:none;" onclick="undoLastCut()">Undo Last Cut</button> <!-- Undo Button -->
    <div id="output" class="text-container" style="display:none;" contenteditable="true"></div>

    <!-- Option to choose cut method -->
    <div style="margin-top: 20px;">
        <!-- Cut options omitted for brevity -->
    </div>

    <div id="credits">
        This page is developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>
    </div>

    <script>
        const countryList = [/* Countries omitted for brevity */];
        let currentUser = null;
        let dailyAdCount = 0;
        let totalTimeInSeconds = 0;
        let cutHistory = []; // Array to store cut paragraphs

        function saveText() {
            // Functionality omitted for brevity
        }

        function loadText() {
            // Functionality omitted for brevity
        }

        function countOccurrences(text, word) {
            // Functionality omitted for brevity
        }

        function countCountryOccurrences(text) {
            // Functionality omitted for brevity
        }

        function highlightErrors(text) {
            // Functionality omitted for brevity
        }

        function updateCounts() {
            // Functionality omitted for brevity
        }

        function updateRemainingTime() {
            // Functionality omitted for brevity
        }

        function processText() {
            // Functionality omitted for brevity
        }

        function cutParagraph(paragraph) {
            const textToCopy = paragraph.innerText;

            // Store the paragraph in cutHistory before cutting it
            cutHistory.push(paragraph.outerHTML);

            const selection = window.getSelection();
            const range = document.createRange();
            range.selectNodeContents(paragraph);
            selection.removeAllRanges();
            selection.addRange(range);

            const tempTextarea = document.createElement('textarea');
            tempTextarea.style.position = 'fixed';
            tempTextarea.style.opacity = '0';
            tempTextarea.value = textToCopy;
            document.body.appendChild(tempTextarea);
            tempTextarea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextarea);

            paragraph.remove();
            cleanupSpaces();

            const inputText = document.getElementById('inputText').value;
            const updatedText = inputText.replace(textToCopy, '').trim();
            document.getElementById('inputText').value = updatedText;

            dailyAdCount++;
            updateCounts();
            saveText();
        }

        function cleanupSpaces() {
            // Functionality omitted for brevity
        }

        function undoLastCut() {
            if (cutHistory.length > 0) {
                const lastCut = cutHistory.pop(); // Get the last cut paragraph

                // Restore the paragraph to the output container
                const outputContainer = document.getElementById('output');
                const restoredElement = document.createElement('div');
                restoredElement.innerHTML = lastCut;
                const paragraph = restoredElement.firstChild;
                outputContainer.insertBefore(paragraph, outputContainer.firstChild);

                // Also restore the text to the input textarea
                const inputText = document.getElementById('inputText').value;
                document.getElementById('inputText').value = lastCut + "\n" + inputText;

                // Decrement the daily ad count
                dailyAdCount--;
                updateCounts();
                saveText();
            }
        }

        function handleCursorMovement(event) {
            // Functionality omitted for brevity
        }

        function handleMouseClick(event) {
            const cutOption = document.querySelector('input[name="cutOption"]:checked').value;
            if (cutOption === 'mouse') {
                handleCursorMovement(event);
            }
        }

        function startMonitoring() {
            const cutOption = document.querySelector('input[name="cutOption"]:checked').value;
            if (cutOption === 'keyboard') {
                document.addEventListener('keyup', handleCursorMovement);
            } else {
                document.removeEventListener('keyup', handleCursorMovement);
            }
        }

        function updateFont() {
            // Functionality omitted for brevity
        }

        function copyRemainingText() {
            // Functionality omitted for brevity
        }

        function login() {
            // Functionality omitted for brevity
        }

        document.getElementById('output').addEventListener('click', function(event) {
            if (event.target.id === 'cursorStart') {
                startMonitoring();
            } else {
                handleMouseClick(event);
            }
        });

        document.querySelectorAll('input[name="cutOption"]').forEach(option => {
            option.addEventListener('change', startMonitoring);
        });

        function checkDailyReset() {
            // Functionality omitted for brevity
        }

        setInterval(checkDailyReset, 60000);
    </script>
</body>
</html>
