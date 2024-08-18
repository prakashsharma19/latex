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
            position: relative;
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
            display: flex;
            align-items: center;
        }

        .font-controls select,
        .font-controls input {
            margin-left: 10px;
        }

        .fullscreen-button {
            background-color: #1171ba;
            border: none;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            margin-left: 10px;
        }

        .fullscreen-button:hover {
            background-color: #0e619f;
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
            transition: background-color 0.3s, transform 0.1s ease;
            margin-top: 10px;
        }

        .copy-button:hover,
        #okButton:hover,
        #loginButton:hover,
        #undoButton:hover,
        #lockButton:hover {
            background-color: #0e619f;
        }

        .copy-button:active,
        #okButton:active,
        #loginButton:active,
        #undoButton:active,
        #lockButton:active {
            transform: scale(0.95);
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
            top: 250px;
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

        .right-content {
            position: absolute;
            top: 250px;
            right: 20px;
            width: 150px;
        }

        #currentTime {
            font-size: 16px;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            text-align: right;
        }

        #remainingTimeText {
            font-size: 16px;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            text-align: right;
        }

        .reminder-heading {
            font-size: 16px;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            text-align: right;
        }

        .reminder-slots {
            list-style-type: none;
            padding: 0;
            margin: 0;
            text-align: right;
        }

        .reminder-slots li {
            background-color: #d3eaf7;
            color: #333;
            padding: 5px;
            border-radius: 5px;
            margin-bottom: 5px;
            cursor: pointer;
            font-size: 12px;
            transition: background-color 0.3s;
        }

        .reminder-slots li:hover,
        .reminder-slots li.selected {
            background-color: #1171ba;
            color: white;
        }

        .popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            padding: 20px;
            background-color: #ffffff;
            border: 1px solid #e0e0e0;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            text-align: center;
        }

        .popup button {
            background-color: #1171ba;
            border: none;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s, transform 0.1s ease;
            margin-top: 10px;
        }

        .popup button:hover {
            background-color: #0e619f;
        }

        .popup button:active {
            transform: scale(0.95);
        }

        .problem-heading {
            color: #e74c3c;
            font-style: italic;
            margin-top: 10px;
            font-size: 16px;
        }

        .reminder-note {
            font-style: italic;
            font-size: 12px;
            text-align: right;
            margin-top: 5px;
            color: #333;
        }

        /* Progress bar */
        .progress-bar {
            height: 5px;
            width: 0;
            background-color: red;
            transition: width 0.5s ease-in-out, background-color 0.5s ease-in-out;
            border-radius: 2px;
            margin-top: 10px;
        }
    </style>
</head>

<body>
    <h1>Advertisements-PPH</h1>

    <!-- Credits in upper-right corner -->
    <div id="credits">
        This tool is developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>
    </div>

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
        <button class="fullscreen-button" onclick="toggleFullScreen()">Full Screen</button>
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
        <div id="remainingTime">File completed by: <span id="remainingTimeText"></span>
            <div class="hourglass"></div>
        </div>
        <button id="undoButton" style="display:none;" onclick="undoLastCut()">Undo Last Cut</button>
        <button id="lockButton" style="display:none;" onclick="toggleLock()">🔒 Lock</button>
    </div>

    <div id="adCount" style="display:none;">Total Advertisements: 0</div>
    <div class="progress-bar" id="progressBar"></div>
    <div id="dailyAdCount" style="display:none;">Total Ads Sent Today: 0</div>
    <div id="countryCount" style="display:none;"></div>

    <div id="output" class="text-container" style="display:none;" contenteditable="true">
        <p id="cursorStart">Place your cursor here</p>
    </div>

    <div class="right-content">
        <div id="currentTime"></div>
        <div class="reminder-heading">Ad Slots:</div>
        <ul class="reminder-slots">
            <li data-time="09:00">9:00-9:30 AM</li>
            <li data-time="10:35">10:35-10:45 AM</li>
            <li data-time="11:50">11:50-12:00 PM</li>
            <li data-time="13:05">1:05-1:10 PM</li>
            <li data-time="14:20">2:20-2:30 PM</li>
            <li data-time="15:40">3:40-3:45 PM</li>
            <li data-time="16:50">4:50-5:00 PM</li>
        </ul>
        <div class="reminder-note">(Select your slots to get reminder)</div>
    </div>

    <div id="reminderPopup" class="popup">
        <p>Send Ads</p>
        <button onclick="dismissPopup()">OK</button>
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
            "Serbia", "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands", "Somalia", "South Africa", "South Korea",
            "South Sudan", "Spain", "Sri Lanka", "Sudan", "Suriname", "Sweden", "Switzerland", "Syria", "Taiwan", "Tajikistan",
            "Tanzania", "Thailand", "Timor-Leste", "Togo", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan", "Tuvalu",
            "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States", "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City", "Venezuela",
            "Vietnam", "Yemen", "Zambia", "Zimbabwe", "UK", "USA", "U.S.A.", "Korea", "UAE"
        ];

        let currentUser = null;
        let dailyAdCount = 0;
        let totalTimeInSeconds = 0;
        let cutHistory = [];
        let isLocked = false;

        function saveText() {
            const inputText = document.getElementById('inputText').value;
            const roughText = document.getElementById('roughText').value;
            const outputText = document.getElementById('output').innerHTML;
            if (currentUser) {
                localStorage.setItem(`savedInput_${currentUser}`, inputText);
                localStorage.setItem(`savedRough_${currentUser}`, roughText);
                localStorage.setItem(`savedOutput_${currentUser}`, outputText);
                localStorage.setItem(`dailyAdCount_${currentUser}`, dailyAdCount);
                localStorage.setItem(`lastCutTime_${currentUser}`, Date.now());
            }
        }

        function loadText() {
            if (currentUser) {
                const savedInput = localStorage.getItem(`savedInput_${currentUser}`);
                const savedRough = localStorage.getItem(`savedRough_${currentUser}`);
                const savedOutput = localStorage.getItem(`savedOutput_${currentUser}`);
                const savedDailyAdCount = localStorage.getItem(`dailyAdCount_${currentUser}`);
                const lastCutTime = localStorage.getItem(`lastCutTime_${currentUser}`);
                if (savedInput) {
                    document.getElementById('inputText').value = savedInput;
                }
                if (savedRough) {
                    document.getElementById('roughText').value = savedRough;
                }
                if (savedOutput) {
                    document.getElementById('output').innerHTML = savedOutput;
                }
                if (savedDailyAdCount && lastCutTime) {
                    const lastCutDate = new Date(parseInt(lastCutTime, 10));
                    const currentDate = new Date();
                    if (lastCutDate.toDateString() === currentDate.toDateString()) {
                        dailyAdCount = parseInt(savedDailyAdCount, 10);
                    }
                }
                updateCounts();
            }
        }

        function countOccurrences(text, word) {
            const regex = new RegExp(`\\b${word}\\b`, 'gi');
            return (text.match(regex) || []).length;
        }

        function countCountryOccurrences(text) {
            const lines = text.split('\n');
            const countryCounts = {};

            for (let i = 0; i < lines.length - 1; i++) {
                const line = lines[i].trim();
                const nextLine = lines[i + 1].trim();

                if (nextLine.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
                    countryList.forEach(country => {
                        if (line.includes(country)) {
                            countryCounts[country] = (countryCounts[country] || 0) + 1;
                        }
                    });
                }
            }
            return countryCounts;
        }

        function highlightErrors(text) {
            return text.replace(/(\w+\?\w+)/g, '<span class="error">$1</span>');
        }

        function updateCounts() {
            const outputContainer = document.getElementById('output');
            const text = outputContainer.innerText;
            const adCount = countOccurrences(text, 'professor');
            document.getElementById('adCount').innerText = `Total Advertisements: ${adCount}`;
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;

            const countryCounts = countCountryOccurrences(text);
            const sortedCountries = Object.entries(countryCounts).sort((a, b) => b[1] - a[1]);
            let countryCountText = 'Country Counts:<br>';
            sortedCountries.forEach(([country, count]) => {
                countryCountText += `<b>${country}</b>: ${count}<br>`;
            });
            document.getElementById('countryCount').innerHTML = countryCountText.trim();

            updateRemainingTime();
            updateProgressBar(adCount);
        }

        function updateProgressBar(adCount) {
            const progressBar = document.getElementById('progressBar');
            const maxCount = 1200; // Number of entries for the bar to be fully filled

            const percentage = Math.min(adCount / maxCount, 1) * 100;
            progressBar.style.width = `${percentage}%`;

            // RGB transition from red to green
            const red = Math.max(255 - Math.floor((adCount / maxCount) * 255), 0);
            const green = Math.min(Math.floor((adCount / maxCount) * 255), 255);
            progressBar.style.backgroundColor = `rgb(${red},${green},0)`;
        }

        function updateRemainingTime() {
            const remainingTimeInSeconds = totalTimeInSeconds - (dailyAdCount * 8);
            const hours = Math.floor(remainingTimeInSeconds / 3600);
            const minutes = Math.floor((remainingTimeInSeconds % 3600) / 60);

            document.getElementById('remainingTimeText').innerText = hours > 0 ? `${hours}h ${minutes}m` : `${minutes}m`;
        }

        function processText() {
            const inputText = document.getElementById('inputText').value;
            const paragraphs = inputText.split('\n\n');
            const outputContainer = document.getElementById('output');
            outputContainer.innerHTML = '<p id="cursorStart">Place your cursor here</p>';

            const totalAds = countOccurrences(inputText, 'professor');
            totalTimeInSeconds = totalAds * 8;

            let index = 0;

            function processChunk() {
                const chunkSize = 100;
                const end = Math.min(index + chunkSize, paragraphs.length);
                for (; index < end; index++) {
                    const paragraph = paragraphs[index];
                    if (paragraph.trim() !== '') {
                        const p = document.createElement('p');
                        p.innerHTML = highlightErrors(paragraph.replace(/\n/g, '<br>'));
                        outputContainer.appendChild(p);
                    }
                }
                if (index < paragraphs.length) {
                    requestAnimationFrame(processChunk);
                } else {
                    updateCounts();
                    saveText();
                    document.getElementById('lockButton').style.display = 'inline-block';

                    // Move entries with 'Russia' to the end, followed by problem entries
                    moveEntriesToEnd('Russia', outputContainer);
                }
            }
            requestAnimationFrame(processChunk);
        }

        function moveEntriesToEnd(keyword, outputContainer) {
            const paragraphs = Array.from(outputContainer.querySelectorAll('p'));

            const paragraphsWithKeyword = [];
            const paragraphsWithProblems = [];
            const otherParagraphs = [];

            paragraphs.forEach(paragraph => {
                const text = paragraph.innerText;
                if (text.includes(keyword)) {
                    paragraphsWithKeyword.push(paragraph);
                } else if (text.includes('?') || !text.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
                    paragraphsWithProblems.push(paragraph);
                } else {
                    otherParagraphs.push(paragraph);
                }
            });

            outputContainer.innerHTML = '<p id="cursorStart">Place your cursor here</p>';
            otherParagraphs.forEach(paragraph => {
                outputContainer.appendChild(paragraph);
            });

            paragraphsWithKeyword.forEach(paragraph => {
                outputContainer.appendChild(paragraph);
            });

            if (paragraphsWithProblems.length > 0) {
                const problemHeading = document.createElement('p');
                problemHeading.className = 'problem-heading';
                problemHeading.innerText = 'Check before sent';
                outputContainer.appendChild(problemHeading);

                paragraphsWithProblems.forEach(paragraph => {
                    outputContainer.appendChild(paragraph);
                });
            }
        }

        function cutParagraph(paragraph) {
            const textToCopy = paragraph.innerText;
            cutHistory.push(textToCopy);

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

            document.getElementById('undoButton').style.display = 'block';
        }

        function undoLastCut() {
            if (cutHistory.length > 0) {
                const lastCutText = cutHistory.pop();

                const outputContainer = document.getElementById('output');
                const p = document.createElement('p');
                p.innerText = lastCutText;
                outputContainer.insertBefore(p, outputContainer.firstChild);

                const inputText = document.getElementById('inputText').value;
                document.getElementById('inputText').value = `${lastCutText}\n${inputText}`.trim();

                dailyAdCount--;

                updateCounts();
                saveText();

                if (cutHistory.length === 0) {
                    document.getElementById('undoButton').style.display = 'none';
                }
            }
        }

        function cleanupSpaces() {
            const outputContainer = document.getElementById('output');
            const paragraphs = outputContainer.querySelectorAll('p');
            paragraphs.forEach(paragraph => {
                if (!paragraph.innerText.trim()) {
                    paragraph.remove();
                }
            });
        }

        function handleCursorMovement(event) {
            const selection = window.getSelection();
            if (selection.rangeCount > 0) {
                const range = selection.getRangeAt(0);
                const container = range.commonAncestorContainer;

                let paragraph = container;
                while (paragraph && paragraph.nodeName !== 'P') {
                    paragraph = paragraph.parentNode;
                }

                if (paragraph && paragraph.textContent.includes('Professor')) {
                    cutParagraph(paragraph);

                    document.getElementById('output').focus();
                }
            }
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
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.getElementById('output').style.fontFamily = fontStyle;
            document.getElementById('output').style.fontSize = `${fontSize}px`;
        }

        function toggleLock() {
            const lockButton = document.getElementById('lockButton');
            const interactiveElements = document.querySelectorAll('input, button, textarea, select');
            isLocked = !isLocked;

            if (isLocked) {
                lockButton.innerHTML = '🔓 Unlock';
                interactiveElements.forEach(element => {
                    if (element.id !== 'output' && element.id !== 'undoButton' && element.id !== 'lockButton') {
                        element.disabled = true;
                    }
                });
            } else {
                lockButton.innerHTML = '🔒 Lock';
                interactiveElements.forEach(element => {
                    if (element.id !== 'output' && element.id !== 'undoButton' && element.id !== 'lockButton') {
                        element.disabled = false;
                    }
                });
            }
        }

        function toggleBox(boxId) {
            const box = document.getElementById(boxId);
            const toggleSymbol = document.getElementById(boxId + 'Toggle');

            if (box.style.display === 'none' || box.style.display === '') {
                box.style.display = 'block';
                toggleSymbol.innerText = '[-]';
            } else {
                box.style.display = 'none';
                toggleSymbol.innerText = '[+]';
            }
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            if (username && password) {
                currentUser = `${username}_${password}`;
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelectorAll('.input-container').forEach(container => container.style.display = 'block');
                document.querySelector('.top-controls').style.display = 'flex';
                document.getElementById('adCount').style.display = 'block';
                document.getElementById('dailyAdCount').style.display = 'block';
                document.getElementById('remainingTime').style.display = 'block';
                document.getElementById('countryCount').style.display = 'block';
                document.getElementById('output').style.display = 'block';
                loadText();
            } else {
                alert('Please enter both username and password.');
            }
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
            const now = new Date();
            const lastCutTime = localStorage.getItem(`lastCutTime_${currentUser}`);
            if (lastCutTime) {
                const lastCutDate = new Date(parseInt(lastCutTime, 10));
                if (lastCutDate.toDateString() !== now.toDateString()) {
                    dailyAdCount = 0;
                    localStorage.setItem(`dailyAdCount_${currentUser}`, dailyAdCount);
                }
            }
        }

        setInterval(checkDailyReset, 60000);

        // Function to display the current time
        function updateTime() {
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            const seconds = now.getSeconds().toString().padStart(2, '0');
            document.getElementById('currentTime').textContent = `${hours}:${minutes}:${seconds}`;
        }

        // Update time every second
        setInterval(updateTime, 1000);

        // Function to check if the selected time slot matches the current time
        function checkReminders() {
            const now = new Date();
            const currentTime = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}`;

            document.querySelectorAll('.reminder-slots li.selected').forEach(slot => {
                if (slot.dataset.time === currentTime) {
                    showPopup();
                    showNotification('Ad Reminder', `It's time to send ads for ${slot.dataset.time}`);
                }
            });
        }

        // Check reminders every minute
        setInterval(checkReminders, 60000);

        // Show the reminder popup
        function showPopup() {
            document.getElementById('reminderPopup').style.display = 'block';
            blinkTab();
        }

        // Dismiss the reminder popup
        function dismissPopup() {
            document.getElementById('reminderPopup').style.display = 'none';
            document.title = originalTitle;
            clearInterval(blinkInterval);
        }

        // Handle slot selection
        document.querySelectorAll('.reminder-slots li').forEach(slot => {
            slot.addEventListener('click', () => {
                slot.classList.toggle('selected');
            });
        });

        // Blink tab title when minimized
        let originalTitle = document.title;
        let blinkInterval;

        function blinkTab() {
            let isOriginalTitle = true;
            blinkInterval = setInterval(() => {
                document.title = isOriginalTitle ? '🔔 Reminder: Send Ads!' : originalTitle;
                isOriginalTitle = !isOriginalTitle;
            }, 1000);
        }

        // Toggle Fullscreen Mode
        function toggleFullScreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen();
                document.querySelector('.fullscreen-button').textContent = 'Normal Screen';
            } else if (document.exitFullscreen) {
                document.exitFullscreen();
                document.querySelector('.fullscreen-button').textContent = 'Full Screen';
            }
        }

        // Show Desktop Notification
        function showNotification(title, body) {
            if (Notification.permission === 'granted') {
                new Notification(title, { body });
            } else if (Notification.permission !== 'denied') {
                Notification.requestPermission().then(permission => {
                    if (permission === 'granted') {
                        new Notification(title, { body });
                    }
                });
            }
        }

        // Request Notification permission on page load
        document.addEventListener('DOMContentLoaded', () => {
            if (Notification.permission !== 'granted') {
                Notification.requestPermission();
            }
        });
    </script>
</body>

</html>
