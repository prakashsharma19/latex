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
        }
        .text-container p {
            margin: 10px 0;
        }
        .copy-button {
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
        .copy-button:hover {
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
        #okButton {
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
        #okButton:hover {
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
        #loginButton {
            background-color: #4CAF50; /* Green */
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
        }
        #loginButton:hover {
            background-color: white;
            color: black;
            border: 2px solid #4CAF50;
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
            "New Zealand", "Nicaragua", "Niger", "Nigeria", "North Macedonia", "Norway", "Oman", "Pakistan", "Palau", "Panama",
            "Papua New Guinea", "Paraguay", "Peru", "Philippines", "Poland", "Portugal", "Qatar", "Romania", "Russia", "Rwanda",
            "Saint Kitts and Nevis", "Saint Lucia", "Saint Vincent and the Grenadines", "Samoa", "San Marino", "Sao Tome and Principe", "Saudi Arabia", "Senegal", "Serbia", "Seychelles",
            "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands", "Somalia", "South Africa", "South Sudan", "Spain", "Sri Lanka",
            "Sudan", "Suriname", "Sweden", "Switzerland", "Syria", "Taiwan", "Tajikistan", "Tanzania", "Thailand", "Timor-Leste",
            "Togo", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan", "Tuvalu", "Uganda", "Ukraine", "United Arab Emirates",
            "United Kingdom", "United States", "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City", "Venezuela", "Vietnam", "Yemen", "Zambia",
            "Zimbabwe"
        ];

        let cutHistory = [];
        let cutOption = "keyboard"; // default cut option

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.input-container').style.display = 'block';
            } else {
                alert('Please enter both username and password.');
            }
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.getElementById('output').style.fontFamily = fontStyle;
            document.getElementById('output').style.fontSize = fontSize + 'px';
        }

        function processText() {
            const inputText = document.getElementById('inputText').value;
            const outputDiv = document.getElementById('output');
            outputDiv.style.display = 'block';
            outputDiv.innerHTML = inputText;
            document.querySelector('.copy-button').style.display = 'inline-block';
            document.getElementById('adCount').style.display = 'block';
            document.getElementById('dailyAdCount').style.display = 'block';
            document.getElementById('remainingTime').style.display = 'block';
            document.getElementById('countryCount').style.display = 'block';
            document.getElementById('adCount').textContent = `Total Advertisements: ${countAdvertisements(inputText)}`;
            document.getElementById('dailyAdCount').textContent = `Total Ads Today: ${countDailyAds(inputText)}`;
            document.getElementById('countryCount').innerHTML = getCountryCount(inputText);
        }

        function countAdvertisements(text) {
            // Logic to count advertisements
            return text.split(' ').length; // Example logic
        }

        function countDailyAds(text) {
            // Logic to count ads for today
            return text.split(' ').length; // Example logic
        }

        function getCountryCount(text) {
            // Count occurrences of each country in the text
            const counts = countryList.reduce((acc, country) => {
                const regex = new RegExp(`\\b${country}\\b`, 'gi');
                const match = text.match(regex);
                acc[country] = match ? match.length : 0;
                return acc;
            }, {});

            // Sort countries by count in descending order
            const sortedCountries = Object.keys(counts).sort((a, b) => counts[b] - counts[a]);
            let result = '';

            sortedCountries.forEach(country => {
                if (counts[country] > 0) {
                    result += `${country}: ${counts[country]}<br>`;
                }
            });

            return result;
        }

        function copyRemainingText() {
            const outputDiv = document.getElementById('output');
            const range = document.createRange();
            range.selectNode(outputDiv);
            window.getSelection().removeAllRanges();
            window.getSelection().addRange(range);
            document.execCommand('copy');
            window.getSelection().removeAllRanges();
        }

        function cutText(startPos, endPos) {
            const outputDiv = document.getElementById('output');
            const text = outputDiv.innerText;
            const beforeText = text.substring(0, startPos);
            const cutText = text.substring(startPos, endPos);
            const afterText = text.substring(endPos);

            cutHistory.push({ cutText, startPos, endPos }); // Save cut operation

            outputDiv.innerText = beforeText + afterText;
            return cutText;
        }

        function undoCut() {
            if (cutHistory.length > 0) {
                const lastCut = cutHistory.pop();
                const outputDiv = document.getElementById('output');
                const text = outputDiv.innerText;
                const beforeText = text.substring(0, lastCut.startPos);
                const afterText = text.substring(lastCut.startPos);

                outputDiv.innerText = beforeText + lastCut.cutText + afterText;
            }
        }

        document.addEventListener('keydown', function(event) {
            if (event.ctrlKey && event.key === 'z') {
                event.preventDefault();
                undoCut();
            }
        });

        document.querySelectorAll('input[name="cutOption"]').forEach(radio => {
            radio.addEventListener('change', (event) => {
                cutOption = event.target.value;
            });
        });

        function handleMouseCut(event) {
            // Example logic for mouse cut handling
            const outputDiv = document.getElementById('output');
            const text = outputDiv.innerText;
            const selection = window.getSelection();
            const range = selection.getRangeAt(0);
            const startOffset = range.startOffset;
            const endOffset = range.endOffset;
            const cutText = cutText(startOffset, endOffset);
            // Handle cutText as needed
        }

        function handleKeyboardCut(event) {
            // Example logic for keyboard cut handling
            if (event.key === 'ArrowDown') {
                const outputDiv = document.getElementById('output');
                const selection = window.getSelection();
                const range = selection.getRangeAt(0);
                const startOffset = range.startOffset;
                const endOffset = range.endOffset;
                const cutText = cutText(startOffset, endOffset);
                // Handle cutText as needed
            }
        }

        document.addEventListener('mousedown', function(event) {
            if (cutOption === 'mouse') {
                handleMouseCut(event);
            }
        });

        document.addEventListener('keydown', function(event) {
            if (cutOption === 'keyboard') {
                handleKeyboardCut(event);
            }
        });

        // Additional functions for remaining time, etc.
    </script>
</body>
</html>
