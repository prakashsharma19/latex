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
        }
        .input-container, .rough-work-container {
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
        }
        .text-container p {
            margin: 10px 0;
        }
        .copy-button, .rough-button {
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
        .copy-button:hover, .rough-button:hover {
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
            position: absolute;
            left: 20px;
            top: 150px;
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
        #okButton, #loginButton {
            background-color: #4CAF50; /* Green */
            border: none;
            color: white;
            padding: 15px 32px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            transition-duration: 0.4s;
        }
        #okButton:hover, #loginButton:hover {
            background-color: white;
            color: black;
            border: 2px solid #4CAF50;
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
        .rough-work-container {
            margin-top: 20px;
            display: flex;
            align-items: center;
            flex-direction: column;
        }
        .rough-work-container textarea {
            width: 300px;
            height: 150px;
        }
        #roughWork {
            display: none; /* Hidden by default */
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

    <!-- Rough Work Box -->
    <div class="rough-work-container" id="roughWork">
        <textarea id="roughText" placeholder="Paste your rough work here..."></textarea>
        <button class="rough-button" onclick="pasteRoughWork()">Paste Text from Rough Work</button>
    </div>

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

    <div id="credits">
        This page is developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>
    </div>

    <script>
        const countryList = [
            "Afghanistan", "Albania", "Algeria", "Andorra", "Angola", "Antigua and Barbuda", "Argentina", "Armenia", "Australia", "Austria",
            "Azerbaijan", "Bahamas", "Bahrain", "Bangladesh", "Barbados", "Belarus", "Belgium", "Belize", "Benin", "Bhutan",
            "Bolivia", "Bosnia and Herzegovina", "Botswana", "Brazil", "Brunei", "Bulgaria", "Burkina Faso", "Burundi", "Cabo Verde", "Cambodia",
            "Cameroon", "Canada", "Central African Republic", "Chad", "Chile", "China", "Colombia", "Comoros", "Congo", "Costa Rica",
            "Croatia", "Cuba", "Cyprus", "Czech Republic", "Denmark", "Djibouti", "Dominica", "Dominican Republic", "Ecuador", "Egypt",
            "El Salvador", "Equatorial Guinea", "Eritrea", "Estonia", "Eswatini", "Ethiopia", "Fiji", "Finland", "France", "Gabon",
            "Gambia", "Georgia", "Germany", "Ghana", "Greece", "Grenada", "Guatemala", "Guinea", "Guinea-Bissau", "Guyana",
            "Haiti", "Honduras", "Hungary", "Iceland", "India", "Indonesia", "Iran", "Iraq", "Ireland", "Israel",
            "Italy", "Jamaica", "Japan", "Jordan", "Kazakhstan", "Kenya", "Kiribati", "Kuwait", "Kyrgyzstan", "Laos",
            "Latvia", "Lebanon", "Lesotho", "Liberia", "Libya", "Liechtenstein", "Lithuania", "Luxembourg", "Madagascar", "Malawi",
            "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands", "Mauritania", "Mauritius", "Mexico", "Micronesia", "Moldova",
            "Monaco", "Mongolia", "Montenegro", "Morocco", "Mozambique", "Myanmar", "Namibia", "Nauru", "Nepal", "Netherlands",
            "New Zealand", "Nicaragua", "Niger", "Nigeria", "North Korea", "North Macedonia", "Norway", "Oman", "Pakistan", "Palau",
            "Palestine", "Panama", "Papua New Guinea", "Paraguay", "Peru", "Philippines", "Poland", "Portugal", "Qatar", "Romania",
            "Russia", "Rwanda", "Saint Kitts and Nevis", "Saint Lucia", "Saint Vincent and the Grenadines", "Samoa", "San Marino", "Sao Tome and Principe", "Saudi Arabia", "Senegal",
            "Serbia", "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands", "Somalia", "South Africa", "South Sudan",
            "Spain", "Sri Lanka", "Sudan", "Suriname", "Sweden", "Switzerland", "Syria", "Taiwan", "Tajikistan", "Tanzania",
            "Thailand", "Timor-Leste", "Turkey", "Turkmenistan", "Tuvalu", "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States",
            "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City", "Venezuela", "Vietnam", "Yemen", "Zambia", "Zimbabwe"
        ];

        let cutHistory = [];
        let dailyAdCount = 0;
        let currentUser = null;
        let roughWorkBoxVisible = false;

        function processText() {
            const text = document.getElementById('inputText').value;
            const outputContainer = document.getElementById('output');
            const paragraphs = text.split('\n');

            outputContainer.innerHTML = '';
            paragraphs.forEach(paragraph => {
                if (paragraph.trim() !== '') {
                    const paragraphElement = document.createElement('div');
                    paragraphElement.innerHTML = paragraph;
                    outputContainer.appendChild(paragraphElement);
                }
            });

            outputContainer.style.display = 'block';
            document.getElementById('adCount').innerText = `Total Advertisements: ${paragraphs.length}`;
            updateCounts();
            saveText();
        }

        function copyRemainingText() {
            const outputContainer = document.getElementById('output');
            const range = document.createRange();
            range.selectNode(outputContainer);
            const selection = window.getSelection();
            selection.removeAllRanges();
            selection.addRange(range);
            document.execCommand('copy');
            selection.removeAllRanges();
            alert('Text copied to clipboard!');
        }

        function updateCounts() {
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;
        }

        function saveText() {
            const text = document.getElementById('inputText').value;
            localStorage.setItem('savedText', text);
        }

        function loadText() {
            const savedText = localStorage.getItem('savedText');
            if (savedText) {
                document.getElementById('inputText').value = savedText;
                processText();
            }
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            const outputContainer = document.getElementById('output');
            outputContainer.style.fontFamily = fontStyle;
            outputContainer.style.fontSize = fontSize + 'px';
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            if (username && password) {
                currentUser = `${username}_${password}`;
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.input-container').style.display = 'block';
                document.getElementById('adCount').style.display = 'block';
                document.getElementById('dailyAdCount').style.display = 'block';
                document.getElementById('remainingTime').style.display = 'block';
                document.getElementById('countryCount').style.display = 'block';
                document.querySelector('.copy-button').style.display = 'block';
                document.getElementById('output').style.display = 'block';
                document.getElementById('roughWork').style.display = 'block'; // Show rough work box
                loadText();
                roughWorkBoxVisible = true;
            } else {
                alert('Please enter both username and password.');
            }
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

        function pasteRoughWork() {
            const roughText = document.getElementById('roughText').value;
            document.getElementById('inputText').value = roughText;
            processText();
        }

        function handleKeyUp(event) {
            if (event.ctrlKey && event.key === 'z') {
                undoLastCut();
            }
        }

        document.addEventListener('keyup', handleKeyUp);

        function getRandomCountry() {
            const randomIndex = Math.floor(Math.random() * countryList.length);
            return countryList[randomIndex];
        }

        function updateCountryCount() {
            const countryCountElement = document.getElementById('countryCount');
            countryCountElement.innerHTML = `<strong>Countries Mentioned:</strong> ${getRandomCountry()}`;
        }

        // Update country count every 10 seconds
        setInterval(updateCountryCount, 10000);
    </script>
</body>
</html>
