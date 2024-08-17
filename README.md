<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        body {
            font-family: 'Helvetica Neue', Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
            margin: 0;
            color: #333;
        }

        h1 {
            color: #1171ba;
            text-align: center;
            margin-bottom: 30px;
            font-size: 28px;
        }

        .font-controls,
        .login-container {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }

        .text-container {
            background-color: #ffffff;
            padding: 15px;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            white-space: pre-wrap;
            position: relative;
            margin-top: 20px;
            z-index: 2;
        }

        .text-container p {
            margin: 0;
            padding-bottom: 10px;
            border-bottom: 1px solid #e0e0e0;
            line-height: 1.5;
        }

        .copy-button,
        #okButton,
        #loginButton,
        #undoButton,
        #lockButton {
            background-color: #1171ba;
            border: none;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
            margin-top: 10px;
        }

        .copy-button:hover,
        #okButton:hover,
        #loginButton:hover,
        #undoButton:hover,
        #lockButton:hover {
            background-color: #0e619f;
        }

        .input-container {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }

        .input-container textarea {
            width: 100%;
            border-radius: 5px;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #e0e0e0;
            margin-top: 10px;
        }

        .input-container .container-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            background-color: #1171ba;
            color: white;
            padding: 10px;
            border-radius: 5px;
        }

        .rough-container {
            width: 30%;
            margin-left: 2%;
        }

        .input-boxes {
            display: none;
        }

        #okButton {
            align-self: flex-end;
            margin-top: 10px;
        }

        #adCount,
        #dailyAdCount,
        #remainingTime,
        #countryCount {
            margin-top: 15px;
            font-size: 18px;
            font-weight: bold;
            color: #2c3e50;
        }

        #remainingTime .hourglass {
            vertical-align: middle;
        }

        #countryCount {
            position: absolute;
            left: 20px;
            top: 150px;
            font-size: 16px;
            font-weight: bold;
            line-height: 1.5;
            color: #34495e;
        }

        #cursorStart {
            font-weight: bold;
            color: #e74c3c;
        }

        #credits {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 16px;
            color: #34495e;
        }

        #credits a {
            color: #1171ba;
            text-decoration: none;
        }

        #credits a:hover {
            text-decoration: underline;
        }

        .error {
            color: #e74c3c;
            font-weight: bold;
        }

        .login-container input {
            width: 100%;
            margin: 5px 0;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #e0e0e0;
            border-radius: 5px;
        }

        .hourglass {
            width: 24px;
            height: 24px;
            background-image: url('https://upload.wikimedia.org/wikipedia/commons/4/4e/Simpleicons_Interface_hourglass.svg');
            background-size: cover;
            display: inline-block;
            margin-left: 10px;
        }

        .option-buttons {
            text-align: center;
            margin-bottom: 30px;
        }

        .option-buttons label {
            margin-right: 20px;
        }

        #undoButton {
            margin-left: 20px;
        }

        #lockButton {
            margin-left: 20px;
        }

        .top-controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .blurred {
            filter: blur(5px);
            pointer-events: none;
        }

        .popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 80%;
            max-height: 80%;
            overflow-y: auto;
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            z-index: 3;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 2;
        }
    </style>
</head>

<body>
    <h1>Advertisements-PPH</h1>

    <!-- Option to choose cut method -->
    <div class="option-buttons">
        <label>
            <input type="radio" name="cutOption" value="keyboard" checked>
            Operate by Keyboard (Down Arrow Key)
        </label>
        <label>
            <input type="radio" name="cutOption" value="mouse">
            Operate by Mouse (Left Button)
        </label>
    </div>

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
        <div class="container-header" onclick="toggleBox('pasteBox')">
            Paste your text here
            <span id="pasteBoxToggle">[+]</span>
        </div>
        <div id="pasteBox" class="input-boxes">
            <textarea id="inputText" rows="5" placeholder="Paste your text here..."></textarea>
            <button id="okButton" onclick="processText()">OK</button>
        </div>
    </div>

    <div class="input-container" style="display:none;">
        <div class="container-header" onclick="toggleBox('roughBox')">
            Rough Work
            <span id="roughBoxToggle">[+]</span>
        </div>
        <div id="roughBox" class="input-boxes rough-container">
            <textarea id="roughText" rows="5" placeholder="Rough Work..."></textarea>
        </div>
    </div>

    <div class="top-controls" style="display:none;">
        <div id="remainingTime">Remaining Time: <span id="time"></span>
            <div class="hourglass"></div>
        </div>
        <div id="adCount">Advertisements Count: <span id="count">0</span></div>
        <div id="dailyAdCount">Daily Ads Remaining: <span id="dailyCount">0</span></div>
        <div id="countryCount">Countries: <span id="countries">0</span></div>
    </div>

    <div id="credits">
        Credits: <a href="https://www.example.com">Example.com</a>
    </div>

    <button id="undoButton" onclick="undo()">Undo</button>
    <button id="lockButton" onclick="toggleLock()">🔒 Lock</button>

    <div id="overlay" class="overlay" style="display:none;"></div>
    <div id="output" class="popup" style="display:none;">
        <p>Here is your output...</p>
        <button onclick="closePopup()">Close</button>
    </div>

    <script>
        let isLocked = false;
        let currentFontSize = 16;
        let currentFontStyle = 'Arial';

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.input-container').style.display = 'block';
                document.querySelector('.top-controls').style.display = 'block';
                document.querySelector('.login-container').style.display = 'none';
                document.getElementById('username').value = '';
                document.getElementById('password').value = '';
            } else {
                alert('Please enter both username and password.');
            }
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.body.style.fontFamily = fontStyle;
            document.body.style.fontSize = fontSize + 'px';
            currentFontSize = fontSize;
            currentFontStyle = fontStyle;
        }

        function toggleBox(id) {
            const box = document.getElementById(id);
            const toggle = document.getElementById(id + 'Toggle');
            if (box.style.display === 'none') {
                box.style.display = 'block';
                toggle.innerHTML = '[-]';
            } else {
                box.style.display = 'none';
                toggle.innerHTML = '[+]';
            }
        }

        function processText() {
            const text = document.getElementById('inputText').value;
            if (text) {
                document.getElementById('output').innerHTML = `<p>${text}</p><button onclick="closePopup()">Close</button>`;
                document.getElementById('overlay').style.display = 'block';
                document.getElementById('output').style.display = 'block';
            }
        }

        function closePopup() {
            document.getElementById('overlay').style.display = 'none';
            document.getElementById('output').style.display = 'none';
        }

        function undo() {
            // Implement undo functionality here
        }

        function toggleLock() {
            const lockButton = document.getElementById('lockButton');
            const outputContainer = document.getElementById('output');
            const overlay = document.getElementById('overlay');
            isLocked = !isLocked;

            if (isLocked) {
                lockButton.innerHTML = '🔓 Unlock';
                document.body.classList.add('blurred');
                outputContainer.classList.add('popup');
                overlay.style.display = 'block';
            } else {
                lockButton.innerHTML = '🔒 Lock';
                document.body.classList.remove('blurred');
                outputContainer.classList.remove('popup');
                overlay.style.display = 'none';
            }
        }
    </script>
</body>

</html>
