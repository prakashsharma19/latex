<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #ADD8E6; /* Light blue background color */
            padding: 20px;
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
        }
        .input-container {
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            flex-direction: column;
        }
        .text-container {
            margin: 20px 0;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #fff;
            cursor: text;
            white-space: pre-wrap; /* Maintain text format */
            position: relative;
            width: 60%;
        }
        .text-container p {
            margin: 10px 0;
        }
        .copy-button, #okButton, #loginButton {
            background-color: #4CAF50; /* Green */
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            cursor: pointer;
            transition-duration: 0.4s;
            margin: 5px;
        }
        .copy-button:hover, #okButton:hover, #loginButton:hover {
            background-color: white;
            color: black;
            border: 2px solid #4CAF50;
        }
        #adCount, #dailyAdCount, #remainingTime, #countryCount {
            margin-top: 10px;
            font-size: 18px;
            font-weight: bold;
        }
        #countryCount {
            font-size: 16px;
            font-weight: bold;
            line-height: 1.5;
        }
        #remainingTime {
            margin-top: 10px;
        }
        .font-controls {
            margin-bottom: 10px;
        }
        #cursorStart {
            font-weight: bold;
            color: red;
        }
        #credits {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 16px;
        }
        #credits a {
            color: #0000EE;
            text-decoration: none;
        }
        #credits a:hover {
            text-decoration: underline;
        }
        .error {
            color: red;
            font-weight: bold;
        }
        .login-container {
            margin-bottom: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .login-container input {
            margin: 5px 0;
            padding: 10px;
            font-size: 16px;
        }
        .hourglass {
            width: 24px;
            height: 24px;
            background-image: url('https://upload.wikimedia.org/wikipedia/commons/4/4e/Simpleicons_Interface_hourglass.svg');
            background-size: cover;
            display: inline-block;
            margin-left: 10px;
        }
        #right-box, #rough-work-box {
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #fff;
            width: 30%;
            position: relative;
        }
        #right-box {
            position: absolute;
            right: 20px;
            top: 120px;
        }
        #rough-work-box {
            margin-top: 20px;
        }
        .text-box-content {
            white-space: pre-wrap;
            padding: 10px;
            border: 1px solid #ddd;
            background-color: #f9f9f9;
            height: 150px;
            overflow-y: auto;
        }
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
        <label for="fontStyle">Font Style:</label>
        <select id="fontStyle" onchange="updateFont()">
            <option value="Arial">Arial</option>
            <option value="Times New Roman">Times New Roman</option>
            <option value="Courier New">Courier New</option>
            <option value="Georgia">Georgia</option>
            <option value="Calibri Light">Calibri Light</option>
        </select>
        <label for="fontSize">Font Size:</label>
        <input type="number" id="fontSize" value="16" onchange="updateFont()">px
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
        <label>
            <input type="radio" name="cutOption" value="keyboard" checked>
            Operate by Keyboard (Down Arrow Key)
        </label>
        <label>
            <input type="radio" name="cutOption" value="mouse">
            Operate by Mouse (Left Button)
        </label>
    </div>

    <!-- Right-side box for last cut paragraph -->
    <div id="right-box">
        <h3>Last Cut Paragraph</h3>
        <div id="lastCutParagraph" class="text-box-content"></div>
    </div>

    <!-- Rough work box -->
    <div id="rough-work-box">
        <h3>Rough Work</h3>
        <textarea id="roughWork" class="text-box-content" placeholder="Paste your rough work here..."></textarea>
    </div>

    <div id="credits">
        This page is developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>
    </div>

    <script>
        const countryList = [
            "Afghanistan", "Albania", "Algeria", "Andorra", "Angola", "Antigua and Barbuda", "Argentina", "Armenia", "Australia", "Austria",
            // (rest of the countries)
        ];

        let currentUser = null;
        let dailyAdCount = 0;
        let totalTimeInSeconds = 0;
        let cutHistory = []; // Array to store cut paragraphs

        // Function to save text to localStorage for the current user
        function saveText() {
            const inputText = document.getElementById('inputText').value;
            const outputText = document.getElementById('output').innerHTML;
            if (currentUser) {
                localStorage.setItem(`savedInput_${currentUser}`, inputText);
                localStorage.setItem(`savedOutput_${currentUser}`, outputText);
                localStorage.setItem(`dailyAdCount_${currentUser}`, dailyAdCount);
                localStorage.setItem(`lastCutTime_${currentUser}`, Date.now());
            }
        }

        // Function to load text from localStorage for the current user
        function loadText() {
            if (currentUser) {
                const savedInput = localStorage.getItem(`savedInput_${currentUser}`);
                const savedOutput = localStorage.getItem(`savedOutput_${currentUser}`);
                const savedDailyAdCount = localStorage.getItem(`dailyAdCount_${currentUser}`);
                const lastCutTime = localStorage.getItem(`lastCutTime_${currentUser}`);
                if (savedInput) {
                    document.getElementById('inputText').value = savedInput;
                }
                if (savedOutput) {
                    document.getElementById('output').innerHTML = savedOutput;
                }
                if (savedDailyAdCount && lastCutTime) {
                    const lastCutDate = new Date(parseInt(lastCutTime, 10));
                    const currentDate = new Date();
                    const diffDays = Math.floor((currentDate - lastCutDate) / (1000 * 60 * 60 * 24));
                    if (diffDays === 0) {
                        dailyAdCount = parseInt(savedDailyAdCount, 10);
                    } else {
                        dailyAdCount = 0;
                    }
                }
                updateAdCount();
            }
        }

        function processText() {
            const text = document.getElementById('inputText').value;
            const output = document.getElementById('output');
            output.style.display = 'block';
            output.innerHTML = text.replace(/\n/g, '<br>'); // Preserve new lines

            saveText();
        }

        function copyRemainingText() {
            const outputText = document.getElementById('output').innerText;
            navigator.clipboard.writeText(outputText)
                .then(() => alert('Text copied to clipboard'))
                .catch(err => alert('Failed to copy text: ' + err));
        }

        function undoLastCut() {
            if (cutHistory.length > 0) {
                const lastCut = cutHistory.pop();
                document.getElementById('lastCutParagraph').innerHTML = lastCut;
                document.getElementById('roughWork').value = lastCut;
                updateAdCount();
            }
        }

        function updateAdCount() {
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value + 'px';
            document.querySelector('.text-container').style.fontFamily = fontStyle;
            document.querySelector('.text-container').style.fontSize = fontSize;
        }

        function updateRemainingTime() {
            const remainingTime = document.getElementById('remainingTime');
            const timeSpan = document.getElementById('time');
            totalTimeInSeconds += 1;
            const minutes = Math.floor(totalTimeInSeconds / 60);
            const seconds = totalTimeInSeconds % 60;
            timeSpan.innerText = `${minutes}m ${seconds}s`;
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                currentUser = username;
                loadText();
                document.querySelector('.input-container').style.display = 'block';
                document.querySelector('.font-controls').style.display = 'block';
                document.getElementById('adCount').style.display = 'block';
                document.getElementById('dailyAdCount').style.display = 'block';
                document.getElementById('remainingTime').style.display = 'block';
                document.getElementById('countryCount').style.display = 'block';
                document.getElementById('right-box').style.display = 'block';
                document.getElementById('rough-work-box').style.display = 'block';
            } else {
                alert('Please enter both username and password.');
            }
        }

        document.addEventListener('keydown', function(event) {
            if (event.key === 'ArrowDown') {
                // Cut text functionality
                const outputText = document.getElementById('output').innerHTML;
                const paragraphEnd = outputText.indexOf('</p>', 0);
                if (paragraphEnd !== -1) {
                    const paragraph = outputText.substring(0, paragraphEnd + 4);
                    cutHistory.push(paragraph); // Save cut paragraph to history
                    document.getElementById('lastCutParagraph').innerHTML = paragraph;
                    document.getElementById('roughWork').value = paragraph;
                    document.getElementById('output').innerHTML = outputText.substring(paragraphEnd + 4);
                    dailyAdCount++;
                    updateAdCount();
                }
            }
        });

        document.addEventListener('mousedown', function(event) {
            if (event.button === 0) { // Left mouse button
                const outputText = document.getElementById('output').innerHTML;
                const paragraphEnd = outputText.indexOf('</p>', 0);
                if (paragraphEnd !== -1) {
                    const paragraph = outputText.substring(0, paragraphEnd + 4);
                    cutHistory.push(paragraph); // Save cut paragraph to history
                    document.getElementById('lastCutParagraph').innerHTML = paragraph;
                    document.getElementById('roughWork').value = paragraph;
                    document.getElementById('output').innerHTML = outputText.substring(paragraphEnd + 4);
                    dailyAdCount++;
                    updateAdCount();
                }
            }
        });

        document.addEventListener('DOMContentLoaded', () => {
            setInterval(updateRemainingTime, 1000);
        });
    </script>
</body>
</html>
