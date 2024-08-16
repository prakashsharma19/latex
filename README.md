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
            "Croatia", "Cuba", "Cyprus", "Czech Republic", "Denmark", "Djibouti", "Dominica", "Dominican Republic", "East Timor", "Ecuador",
            "Egypt", "El Salvador", "Equatorial Guinea", "Eritrea", "Estonia", "Eswatini", "Ethiopia", "Fiji", "Finland", "France",
            "Gabon", "Gambia", "Georgia", "Germany", "Ghana", "Greece", "Grenada", "Guatemala", "Guinea", "Guinea-Bissau",
            "Guyana", "Haiti", "Honduras", "Hungary", "Iceland", "India", "Indonesia", "Iran", "Iraq", "Ireland",
            "Israel", "Italy", "Jamaica", "Japan", "Jordan", "Kazakhstan", "Kenya", "Kiribati", "Korea, North", "Korea, South",
            "Kosovo", "Kuwait", "Kyrgyzstan", "Laos", "Latvia", "Lebanon", "Lesotho", "Liberia", "Libya", "Liechtenstein",
            "Lithuania", "Luxembourg", "Madagascar", "Malawi", "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands", "Mauritania",
            "Mauritius", "Mexico", "Micronesia", "Moldova", "Monaco", "Mongolia", "Montenegro", "Morocco", "Mozambique", "Myanmar",
            "Namibia", "Nauru", "Nepal", "Netherlands", "New Zealand", "Nicaragua", "Niger", "Nigeria", "North Macedonia", "Norway",
            "Oman", "Pakistan", "Palau", "Palestine", "Panama", "Papua New Guinea", "Paraguay", "Peru", "Philippines", "Poland",
            "Portugal", "Qatar", "Romania", "Russia", "Rwanda", "Saint Kitts and Nevis", "Saint Lucia", "Saint Vincent and the Grenadines", "Samoa", "San Marino",
            "Sao Tome and Principe", "Saudi Arabia", "Senegal", "Serbia", "Seychelles", "Sierra Leone", "Singapore", "Slovakia", "Slovenia", "Solomon Islands",
            "Somalia", "South Africa", "South Sudan", "Spain", "Sri Lanka", "Sudan", "Suriname", "Sweden", "Switzerland", "Syria",
            "Taiwan", "Tajikistan", "Tanzania", "Thailand", "Togo", "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan",
            "Tuvalu", "Uganda", "Ukraine", "United Arab Emirates", "United Kingdom", "United States", "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City",
            "Venezuela", "Vietnam", "Yemen", "Zambia", "Zimbabwe"
        ];

        let cutHistory = [];
        let currentCutIndex = -1;
        let adCount = 0;
        let dailyAdCount = 0;
        let isLocked = false;

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.getElementById('inputText').style.fontFamily = fontStyle;
            document.getElementById('inputText').style.fontSize = fontSize + 'px';
        }

        function processText() {
            const textArea = document.getElementById('inputText');
            const output = document.getElementById('output');
            const text = textArea.value.trim();

            if (text) {
                output.innerHTML += `<p>${text}</p>`;
                cutHistory.push(text);
                dailyAdCount++;
                updateCounts();
                saveText();
                textArea.value = '';  // Clear the textarea
                output.style.display = 'block';
                adCount++;
                document.getElementById('undoButton').style.display = 'inline-block';
            }
        }

        function updateCounts() {
            document.getElementById('adCount').textContent = `Total Advertisements: ${adCount}`;
            document.getElementById('dailyAdCount').textContent = `Total Ads Today: ${dailyAdCount}`;
        }

        function saveText() {
            // Implement saving logic if needed
        }

        function undoLastCut() {
            if (cutHistory.length > 0) {
                const lastCut = cutHistory.pop();
                document.getElementById('inputText').value += `\n\n${lastCut}`;
                document.getElementById('undoButton').style.display = 'none';
                dailyAdCount--;
                updateCounts();
                saveText();
            } else {
                alert('No cuts to undo');
            }
        }

        function toggleLock() {
            isLocked = !isLocked;
            const lockIcon = document.querySelector('.lock-icon');
            const fontControls = document.querySelector('.font-controls');
            const inputContainer = document.querySelector('.input-container');
            const roughContainer = document.querySelector('.rough-container');
            const topControls = document.querySelector('.top-controls');
            const output = document.getElementById('output');

            if (isLocked) {
                lockIcon.textContent = '🔓';
                fontControls.style.display = 'none';
                inputContainer.style.display = 'none';
                roughContainer.style.display = 'none';
                topControls.style.display = 'none';
                output.style.pointerEvents = 'none';
            } else {
                lockIcon.textContent = '🔒';
                fontControls.style.display = 'block';
                inputContainer.style.display = 'block';
                roughContainer.style.display = 'block';
                topControls.style.display = 'block';
                output.style.pointerEvents = 'auto';
            }
        }

        function login() {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value.trim();

            if (username === '' || password === '') {
                alert('Please enter both username and password');
                return;
            }

            // Here you would normally handle the login process
            document.querySelector('.login-container').style.display = 'none';
            document.querySelector('.font-controls').style.display = 'block';
            document.querySelector('.input-container').style.display = 'block';
            document.querySelector('.rough-container').style.display = 'block';
            document.querySelector('.top-controls').style.display = 'flex';
        }

        document.addEventListener('keydown', function (event) {
            if (event.key === 'ArrowDown' && !isLocked) {
                processText();
            }
        });

        document.addEventListener('mousedown', function (event) {
            if (event.button === 0 && !isLocked) {
                processText();
            }
        });
    </script>
</body>

</html>
