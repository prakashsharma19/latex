<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            text-align: center;
        }
        .login-container,
        .font-controls,
        .input-container {
            margin: 20px auto;
            max-width: 300px;
            display: flex;
            flex-direction: column;
        }
        .login-container input,
        .font-controls input,
        .input-container textarea {
            margin-bottom: 10px;
            padding: 8px;
            border-radius: 4px;
            border: 1px solid #ccc;
        }
        .login-container button,
        .input-container button,
        .copy-button,
        .undo-button {
            padding: 8px;
            border: none;
            border-radius: 4px;
            background-color: #007bff;
            color: white;
            cursor: pointer;
        }
        .login-container button:hover,
        .input-container button:hover,
        .copy-button:hover,
        .undo-button:hover {
            background-color: #0056b3;
        }
        #adCount,
        #dailyAdCount,
        #remainingTime,
        #countryCount,
        #output {
            margin-top: 20px;
            text-align: center;
        }
        #output {
            padding: 10px;
            background-color: white;
            border-radius: 4px;
            border: 1px solid #ccc;
            max-width: 600px;
            margin: 20px auto;
            word-wrap: break-word;
            white-space: pre-wrap;
        }
        .hourglass {
            display: inline-block;
            margin-left: 10px;
            border: 5px solid #ccc;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        #credits {
            text-align: center;
            margin-top: 50px;
        }
        #credits a {
            color: #007bff;
            text-decoration: none;
        }
        #credits a:hover {
            text-decoration: underline;
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
    <button class="undo-button" style="display:none;" onclick="undoLastEntry()">Undo Last Entry</button>
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
            "Serbia", "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands", "Somalia", "South Africa", "South Korea",
            "South Sudan", "Spain", "Sri Lanka", "Sudan", "Suriname", "Sweden", "Switzerland", "Syria", "Taiwan", "Tajikistan",
            "Tanzania", "Thailand", "Timor-Leste", "Togo", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan", "Tuvalu",
            "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States", "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City", "Venezuela",
            "Vietnam", "Yemen", "Zambia", "Zimbabwe", "UK", "USA", "U.S.A.", "Korea", "UAE"
        ];

        let currentUser = null;
        let dailyAdCount = 0;
        let totalTimeInSeconds = 0;
        let historyStack = [];

        function saveText() {
            localStorage.setItem('outputText', document.getElementById('output').innerHTML);
        }

        function loadText() {
            const savedText = localStorage.getItem('outputText');
            if (savedText) {
                document.getElementById('output').innerHTML = savedText;
            }
        }

        function countOccurrences(text, word) {
            return (text.match(new RegExp(word, 'gi')) || []).length;
        }

        function countCountryOccurrences(text) {
            const lines = text.split('\n');
            const countryCounts = {};

            for (let line of lines) {
                // Skip email addresses to avoid false positives
                if (!line.match(/[a-zA-Z0-9._+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
                    countryList.forEach(country => {
                        const regex = new RegExp(`\\b${country}\\b`, 'gi');
                        if (line.match(regex)) {
                            if (!countryCounts[country]) {
                                countryCounts[country] = 0;
                            }
                            countryCounts[country]++;
                        }
                    });
                }
            }

            let output = '';
            for (const [country, count] of Object.entries(countryCounts)) {
                output += `${country}: ${count} occurrences<br>`;
            }

            return output;
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            if (username && password) {
                currentUser = username;
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.input-container').style.display = 'block';
                document.querySelector('.copy-button').style.display = 'block';
                document.querySelector('.undo-button').style.display = 'block';
                document.getElementById('adCount').style.display = 'block';
                document.getElementById('dailyAdCount').style.display = 'block';
                document.getElementById('remainingTime').style.display = 'block';
                loadText();
            }
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            const textContainer = document.getElementById('output');
            textContainer.style.fontFamily = fontStyle;
            textContainer.style.fontSize = fontSize + 'px';
        }

        function processText() {
            const inputText = document.getElementById('inputText').value;
            let emailCount = countOccurrences(inputText, '@');
            let totalCount = emailCount;

            const countryOccurrences = countCountryOccurrences(inputText);

            historyStack.push(inputText);
            totalTimeInSeconds += totalCount;
            dailyAdCount += emailCount;

            document.getElementById('output').innerHTML += inputText.replace(/\n/g, '<br>');
            document.getElementById('inputText').value = '';

            updateCounts();
            saveText();

            // Display country occurrences
            document.getElementById('countryCount').innerHTML = countryOccurrences;
            document.getElementById('countryCount').style.display = 'block';

            updateRemainingTime();
        }

        function updateCounts() {
            document.getElementById('adCount').innerText = `Total Advertisements: ${dailyAdCount}`;
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;
        }

        function updateRemainingTime() {
            let timeLeft = totalTimeInSeconds;
            const hours = Math.floor(timeLeft / 3600);
            timeLeft %= 3600;
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;

            document.getElementById('time').innerText = `${hours}h ${minutes}m ${seconds}s`;
        }

        function copyRemainingText() {
            const outputText = document.getElementById('output').innerText;
            const tempInput = document.createElement('textarea');
            tempInput.value = outputText;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);
            alert('Text copied to clipboard!');
        }

        function undoLastEntry() {
            if (historyStack.length > 0) {
                const lastEntry = historyStack.pop();
                document.getElementById('inputText').value = lastEntry;

                const outputText = document.getElementById('output').innerHTML;
                const newOutputText = outputText.substring(0, outputText.lastIndexOf(lastEntry.replace(/\n/g, '<br>')));
                document.getElementById('output').innerHTML = newOutputText;

                let emailCount = countOccurrences(lastEntry, '@');
                dailyAdCount -= emailCount;

                updateCounts();
                saveText();
            }
        }

        document.addEventListener('keydown', function (event) {
            if (document.querySelector('input[name="cutOption"]:checked').value === 'keyboard' && event.key === 'ArrowDown') {
                processText();
            }
        });

        document.addEventListener('click', function (event) {
            if (document.querySelector('input[name="cutOption"]:checked').value === 'mouse' && event.button === 0) {
                processText();
            }
        });

    </script>
</body>
</html>
