<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #F5F5F5; /* Light gray background color */
            padding: 20px;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            height: 100vh;
            color: #333;
        }

        h1 {
            text-align: center;
            color: #004A7F;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center;
            max-width: 1200px;
            width: 100%;
        }

        .input-section {
            display: flex;
            justify-content: space-between;
            width: 100%;
            max-width: 1200px;
            margin-bottom: 20px;
            visibility: hidden;
        }

        .input-container, .extra-container {
            width: 48%;
        }

        textarea {
            width: 100%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }

        .text-container {
            margin: 20px 0;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #fff;
            cursor: text;
            white-space: pre-wrap;
            position: relative;
            width: 100%;
            max-width: 1200px;
            box-sizing: border-box;
            visibility: hidden;
        }

        .text-container p {
            margin: 10px 0;
        }

        .buttons {
            display: flex;
            justify-content: center;
            margin-top: 20px;
            visibility: hidden;
        }

        .copy-button, #okButton, #undoButton {
            background-color: #007BFF; /* Light blue */
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            font-size: 16px;
            cursor: pointer;
            transition-duration: 0.4s;
            margin: 5px;
            border-radius: 4px;
        }

        .copy-button:hover, #okButton:hover, #undoButton:hover {
            background-color: #0056b3;
        }

        #adCount, #dailyAdCount, #remainingTime, #countryCount {
            margin-top: 10px;
            font-size: 18px;
            font-weight: bold;
            color: #004A7F;
            visibility: hidden;
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
            visibility: hidden;
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
            color: #007BFF;
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
            width: 100%;
            max-width: 300px;
            box-sizing: border-box;
        }

        #loginButton {
            background-color: #007BFF;
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 10px 0;
            cursor: pointer;
            transition-duration: 0.4s;
            border-radius: 4px;
        }

        #loginButton:hover {
            background-color: #0056b3;
        }

        .hourglass {
            width: 24px;
            height: 24px;
            background-image: url('https://upload.wikimedia.org/wikipedia/commons/4/4e/Simpleicons_Interface_hourglass.svg');
            background-size: cover;
            display: inline-block;
            margin-left: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Advertisements-PPH</h1>
        <div class="login-container">
            <input type="text" id="username" placeholder="Enter your name">
            <input type="password" id="password" placeholder="Enter your password">
            <button id="loginButton" onclick="login()">Login</button>
        </div>
        <div class="input-section">
            <div class="input-container">
                <textarea id="inputText" rows="10" cols="50" placeholder="Paste your text here..."></textarea>
                <button id="okButton" onclick="processText()">OK</button>
            </div>
            <div class="extra-container">
                <textarea id="extraText" rows="10" cols="50" placeholder="Paste additional text here..."></textarea>
            </div>
        </div>
        <div id="adCount">Total Advertisements: 0</div>
        <div id="dailyAdCount">Total Ads Today: 0</div>
        <div id="remainingTime">Remaining Time: <span id="time"></span><div class="hourglass"></div></div>
        <div id="countryCount"></div>
        <div class="buttons">
            <button class="copy-button" onclick="copyRemainingText()">Copy Remaining Text</button>
            <button class="copy-button" id="undoButton" onclick="undoLastCut()">Undo Last Cut</button>
        </div>
        <div id="output" class="text-container" contenteditable="true"></div>
        <div id="credits">
            This page is developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>
        </div>
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
        }

        function updateRemainingTime() {
            const remainingTimeInSeconds = totalTimeInSeconds - (dailyAdCount * 8);
            const hours = Math.floor(remainingTimeInSeconds / 3600);
            const minutes = Math.floor((remainingTimeInSeconds % 3600) / 60);

            document.getElementById('time').innerText = hours > 0 ? `${hours}h ${minutes}m` : `${minutes}m`;
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
            const paragraphs = outputContainer.querySelectorAll('p, div');
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

        function copyRemainingText() {
            const outputContainer = document.getElementById('output');
            const remainingText = outputContainer.innerText;
            const tempTextarea = document.createElement('textarea');
            tempTextarea.style.position = 'fixed';
            tempTextarea.style.opacity = '0';
            tempTextarea.value = remainingText;
            document.body.appendChild(tempTextarea);
            tempTextarea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextarea);
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            if (username && password) {
                currentUser = `${username}_${password}`;
                document.querySelector('.login-container').style.display = 'none';

                // Show the hidden elements after successful login
                document.querySelector('.font-controls').style.visibility = 'visible';
                document.querySelector('.input-section').style.visibility = 'visible';
                document.getElementById('adCount').style.visibility = 'visible';
                document.getElementById('dailyAdCount').style.visibility = 'visible';
                document.getElementById('remainingTime').style.visibility = 'visible';
                document.getElementById('countryCount').style.visibility = 'visible';
                document.querySelector('.buttons').style.visibility = 'visible';
                document.getElementById('output').style.visibility = 'visible';

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

    </script>
</body>
</html>
