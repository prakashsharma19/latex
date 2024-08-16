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
            text-align: center;
            color: #2c3e50;
            margin-bottom: 30px;
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
        }

        .text-container p {
            margin: 0;
            padding-bottom: 10px;
            border-bottom: 1px solid #e0e0e0;
        }

        .lock-icon {
            position: absolute;
            top: -10px;
            right: -10px;
            cursor: pointer;
            font-size: 24px;
            color: #2980b9;
            background-color: #ffffff;
            padding: 5px;
            border-radius: 50%;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .copy-button,
        #okButton,
        #loginButton,
        #undoButton {
            background-color: #2c3e50;
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
        #undoButton:hover {
            background-color: #34495e;
        }

        .input-container {
            display: flex;
            flex-direction: column;
            margin-bottom: 20px;
        }

        .input-container textarea {
            width: 100%;
            border-radius: 5px;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #e0e0e0;
        }

        .rough-container {
            width: 100%;
            margin-top: 20px;
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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
            color: #2980b9;
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

        .top-controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
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
        <textarea id="inputText" rows="10" cols="50" placeholder="Paste your text here..."></textarea>
        <button id="okButton" onclick="processText()">OK</button>
    </div>

    <div class="rough-container" style="display:none;">
        <textarea id="roughText" rows="10" cols="50" placeholder="Rough Work..."></textarea>
    </div>

    <div class="top-controls" style="display:none;">
        <div id="remainingTime">Remaining Time: <span id="time"></span>
            <div class="hourglass"></div>
        </div>
        <button id="undoButton" style="display:none;" onclick="undoLastCut()">Undo Last Cut</button>
    </div>

    <div id="adCount" style="display:none;">Total Advertisements: 0</div>
    <div id="dailyAdCount" style="display:none;">Total Ads Today: 0</div>
    <div id="countryCount" style="display:none;"></div>

    <div class="lock-icon" style="display:none;" onclick="toggleLock()">🔒</div>
    <div id="output" class="text-container" style="display:none;" contenteditable="true"></div>

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
            const outputText = document.getElementById('output').innerHTML;
            if (currentUser) {
                localStorage.setItem(savedInput_${currentUser}, inputText);
                localStorage.setItem(savedOutput_${currentUser}, outputText);
                localStorage.setItem(dailyAdCount_${currentUser}, dailyAdCount);
                localStorage.setItem(lastCutTime_${currentUser}, Date.now());
            }
        }

        function loadText() {
            if (currentUser) {
                const savedInput = localStorage.getItem(savedInput_${currentUser});
                const savedOutput = localStorage.getItem(savedOutput_${currentUser});
                const savedDailyAdCount = localStorage.getItem(dailyAdCount_${currentUser});
                const lastCutTime = localStorage.getItem(lastCutTime_${currentUser});
                if (savedInput) {
                    document.getElementById('inputText').value = savedInput;
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
            const regex = new RegExp(\\b${word}\\b, 'gi');
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
            document.getElementById('adCount').innerText = Total Advertisements: ${adCount};
            document.getElementById('dailyAdCount').innerText = Total Ads Today: ${dailyAdCount};

            const countryCounts = countCountryOccurrences(text);
            const sortedCountries = Object.entries(countryCounts).sort((a, b) => b[1] - a[1]);
            let countryCountText = 'Country Counts:<br>';
            sortedCountries.forEach(([country, count]) => {
                countryCountText += <b>${country}</b>: ${count}<br>;
            });
            document.getElementById('countryCount').innerHTML = countryCountText.trim();

            updateRemainingTime();
        }

        function updateRemainingTime() {
            const remainingTimeInSeconds = totalTimeInSeconds - (dailyAdCount * 8);
            const hours = Math.floor(remainingTimeInSeconds / 3600);
            const minutes = Math.floor((remainingTimeInSeconds % 3600) / 60);

            document.getElementById('time').innerText = hours > 0 ? ${hours}h ${minutes}m : ${minutes}m;
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

                        const gap = document.createElement('div');
                        gap.innerHTML = '<br><br>';
                        outputContainer.appendChild(gap);
                    }
                }
                if (index < paragraphs.length) {
                    requestAnimationFrame(processChunk);
                } else {
                    updateCounts();
                    saveText();
                    document.querySelector('.lock-icon').style.display = 'block';
                }
            }
            requestAnimationFrame(processChunk);
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
                const lastCut = cutHistory.pop();
                document.getElementById('inputText').value += `\n\n${lastCut}`;
                document.getElementById('undoButton').style.display = 'none';
                dailyAdCount--;
                updateCounts();
                saveText();
            }
        }

        function toggleLock() {
            isLocked = !isLocked;
            document.getElementById('inputText').disabled = isLocked;
            document.getElementById('output').contentEditable = !isLocked;
            document.querySelector('.lock-icon').innerText = isLocked ? '🔓' : '🔒';
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                currentUser = username;
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.input-container').style.display = 'block';
                document.querySelector('.rough-container').style.display = 'block';
                document.querySelector('.top-controls').style.display = 'flex';
                document.getElementById('adCount').style.display = 'block';
                document.getElementById('dailyAdCount').style.display = 'block';
                document.getElementById('countryCount').style.display = 'block';
                document.getElementById('credits').style.display = 'block';
                loadText();
            } else {
                alert('Please enter both username and password');
            }
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.getElementById('output').style.fontFamily = fontStyle;
            document.getElementById('output').style.fontSize = fontSize + 'px';
        }

        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowDown' && document.querySelector('input[name="cutOption"][value="keyboard"]').checked) {
                processText();
            }
        });

        document.addEventListener('click', (e) => {
            if (e.target && e.target.matches('.lock-icon')) {
                toggleLock();
            }
        });
    </script>
</body>

</html>
