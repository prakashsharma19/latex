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
        .cut-texts-box {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 250px;
            height: 90%;
            border: 1px solid #ccc;
            background-color: #fff;
            padding: 10px;
            overflow-y: auto;
            z-index: 1000; /* Ensure it is on top of other elements */
        }
        .cut-texts-box h2 {
            font-size: 18px;
            margin-top: 0;
        }
        .cut-text {
            margin-bottom: 10px;
            padding: 5px;
            border: 1px solid #ddd;
            background-color: #f9f9f9;
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

    <!-- Box for cut texts -->
    <div id="cutTextsBox" class="cut-texts-box">
        <h2>Cut Texts</h2>
        <div id="cutTextsContainer" class="text-container"></div>
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
            "Italy", "Jamaica", "Japan", "Jordan", "Kazakhstan", "Kenya", "Kiribati", "Korea, North", "Korea, South", "Kosovo",
            "Kuwait", "Kyrgyzstan", "Laos", "Latvia", "Lebanon", "Lesotho", "Liberia", "Libya", "Liechtenstein", "Lithuania",
            "Luxembourg", "Madagascar", "Malawi", "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands", "Mauritania", "Mauritius",
            "Mexico", "Micronesia", "Moldova", "Monaco", "Mongolia", "Montenegro", "Morocco", "Mozambique", "Myanmar", "Namibia",
            "Nauru", "Nepal", "Netherlands", "New Zealand", "Nicaragua", "Niger", "Nigeria", "North Macedonia", "Norway", "Oman",
            "Pakistan", "Palau", "Panama", "Papua New Guinea", "Paraguay", "Peru", "Philippines", "Poland", "Portugal", "Qatar",
            "Romania", "Russia", "Rwanda", "Saint Kitts and Nevis", "Saint Lucia", "Saint Vincent and the Grenadines", "Samoa", "San Marino", "Sao Tome and Principe", "Saudi Arabia",
            "Senegal", "Serbia", "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands", "Somalia", "South Africa",
            "South Sudan", "Spain", "Sri Lanka", "Sudan", "Suriname", "Sweden", "Switzerland", "Syria", "Taiwan", "Tajikistan",
            "Tanzania", "Thailand", "Timor-Leste", "Togo", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan", "Tuvalu",
            "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States", "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City", "Venezuela",
            "Vietnam", "Yemen", "Zambia", "Zimbabwe"
        ];

        let adCount = 0;
        let dailyAdCount = 0;
        let cutMethod = "keyboard"; // Default to keyboard method
        let startTime = new Date();
        let cutIntervals = [];
        let timeLimit = 30; // Time limit in minutes

        function processText() {
            const inputText = document.getElementById('inputText').value;
            const output = document.getElementById('output');
            output.innerHTML = inputText.replace(/\n/g, '<br>'); // Preserve line breaks
            document.querySelector('.input-container').style.display = 'none';
            output.style.display = 'block';
            updateCounts();
            document.getElementById('remainingTime').style.display = 'block';
            startTimer();
            updateCountryCount();
            document.querySelector('.font-controls').style.display = 'none';
            document.querySelector('.copy-button').style.display = 'inline';
        }

        function startTimer() {
            const timer = setInterval(() => {
                const elapsedMinutes = (new Date() - startTime) / 60000;
                const remainingMinutes = Math.max(0, timeLimit - Math.floor(elapsedMinutes));
                document.getElementById('time').innerText = `${remainingMinutes} min`;
                if (remainingMinutes <= 0) {
                    clearInterval(timer);
                    document.getElementById('time').innerText = 'Time is up!';
                }
            }, 60000);
        }

        function updateCounts() {
            document.getElementById('adCount').innerText = `Total Advertisements: ${adCount}`;
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;
        }

        function copyRemainingText() {
            const outputText = document.getElementById('output').innerText;
            navigator.clipboard.writeText(outputText)
                .then(() => alert('Text copied to clipboard!'))
                .catch(err => alert('Failed to copy text: ', err));
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.getElementById('output').style.fontFamily = fontStyle;
            document.getElementById('output').style.fontSize = fontSize + 'px';
        }

        function updateCountryCount() {
            const count = countryList.length;
            document.getElementById('countryCount').innerText = `Number of Countries: ${count}`;
        }

        function cleanupSpaces() {
            const paragraphs = document.querySelectorAll('.text-container p');
            paragraphs.forEach(paragraph => {
                if (!paragraph.innerText.trim()) {
                    paragraph.remove();
                }
            });
        }

        function cutParagraph(paragraph) {
            const textToCopy = paragraph.innerText;
            const selection = window.getSelection();
            const range = document.createRange();
            range.selectNodeContents(paragraph);
            selection.removeAllRanges();
            selection.addRange(range);

            // Copy the text without formatting
            const tempTextarea = document.createElement('textarea');
            tempTextarea.style.position = 'fixed';
            tempTextarea.style.opacity = '0';
            tempTextarea.value = textToCopy;
            document.body.appendChild(tempTextarea);
            tempTextarea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextarea);

            // Remove the paragraph and cleanup
            paragraph.remove();
            cleanupSpaces();

            // Update the input textarea by removing the corresponding text
            const inputText = document.getElementById('inputText').value;
            const updatedText = inputText.replace(textToCopy, '').trim();
            document.getElementById('inputText').value = updatedText;

            // Update the daily ad count
            dailyAdCount++;

            // Update the count and save changes
            updateCounts();
            saveText();

            // Paste the text into the cut texts box
            const cutTextsContainer = document.getElementById('cutTextsContainer');
            const cutTextDiv = document.createElement('div');
            cutTextDiv.className = 'cut-text';
            cutTextDiv.innerText = textToCopy;
            cutTextsContainer.appendChild(cutTextDiv);
        }

        function saveText() {
            // Implement your save logic here if needed
        }

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                alert('Login successful!');
                document.querySelector('.input-container').style.display = 'block';
                document.querySelector('.font-controls').style.display = 'block';
            } else {
                alert('Please enter both username and password.');
            }
        }

        document.addEventListener('keydown', function(event) {
            if (event.key === 'ArrowDown' && cutMethod === 'keyboard') {
                // Logic to cut text using keyboard
                const selectedParagraph = document.querySelector('.text-container p');
                if (selectedParagraph) {
                    cutParagraph(selectedParagraph);
                }
            }
        });

        document.addEventListener('mousedown', function(event) {
            if (event.button === 0 && cutMethod === 'mouse') {
                // Logic to cut text using mouse
                const target = event.target;
                if (target.classList.contains('text-container') && target.tagName === 'P') {
                    cutParagraph(target);
                }
            }
        });

        document.querySelectorAll('input[name="cutOption"]').forEach((radio) => {
            radio.addEventListener('change', (event) => {
                cutMethod = event.target.value;
            });
        });
    </script>
</body>
</html>
