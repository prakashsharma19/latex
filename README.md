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
            display: flex;
            align-items: center;
            justify-content: center;
        }

        h1 img {
            margin-right: 10px;
            height: 28px;
        }

        .font-controls,
        .login-container {
            background-color: #ffffff;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            display: flex;
            flex-direction: column;
            align-items: flex-start;
            width: 100%;
        }

        .font-controls .control-group {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            gap: 10px;
        }

        .font-controls label {
            margin-right: 10px;
            font-weight: bold;
            color: #2c3e50;
        }

        .font-controls select,
        .font-controls input {
            border-radius: 5px;
            padding: 5px;
            border: 1px solid #e0e0e0;
            font-size: 14px;
        }

        .font-controls input[type="number"] {
            width: 50px;
        }

        .fullscreen-button {
            background-color: #1171ba;
            border: none;
            color: white;
            padding: 10px 15px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            margin-top: 10px;
            width: 100%;
        }

        .fullscreen-button:hover {
            background-color: #0e619f;
        }

        .clear-memory-button {
            background-color: red;
            color: white;
            padding: 10px 15px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            border: none;
            position: absolute;
            top: 20px;
            left: 20px;
        }

        .clear-memory-button:hover {
            background-color: darkred;
        }

        .text-container {
            background-color: #ffffff;
            padding: 15px;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            white-space: pre-wrap;
            position: relative;
            margin-top: 20px;
            z-index: 2;
        }

        .text-container p {
            margin: 0 0 10px;
            border-bottom: 1px solid #e0e0e0;
            line-height: 1.5;
        }

        #undoButton,
        #lockButton {
            border: none;
            color: white;
            padding: 10px 15px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s, transform 0.1s ease;
            margin-top: 10px;
            width: 100%;
        }

        #loginButton {
            background-color: #007bff;
            margin-top: 10px;
            font-size: 16px;
            border: none;
            color: white;
            padding: 10px 15px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }

        #loginButton:hover {
            background-color: #0056b3;
        }

        #loginButton:active {
            transform: scale(0.95);
        }

        #lockButton {
            background-color: #1171ba;
        }

        #lockButton.locked {
            background-color: #d9534f;
        }

        #lockButton:hover {
            background-color: #0e619f;
        }

        #undoButton {
            background-color: #1171ba;
        }

        .input-container {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            flex-direction: column;
            align-items: center;
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
            background-color: #1171ba;
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

        #loadingIndicator {
            color: red;
            margin-left: 10px;
            font-size: 16px;
            font-weight: bold;
            display: none;
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
            color: #3498db;
        }

        #userControls {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 16px;
            color: #34495e;
            display: flex;
            align-items: center;
        }

        #userControls img {
            margin-right: 10px;
            height: 28px;
        }

        #userControls span {
            margin-right: 10px;
            font-weight: bold;
        }

        #logoutButton {
            background-color: #e74c3c;
            border: none;
            color: white;
            padding: 5px 10px;
            font-size: 14px;
            cursor: pointer;
            border-radius: 5px;
        }

        #logoutButton:hover {
            background-color: #c0392b;
        }

        .error {
            color: #e74c3c;
            font-weight: bold;
            font-style: italic;
        }

        .highlight-added {
            background-color: #f4e542;
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

        .top-controls {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
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
            font-size: 18px;
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
            padding: 30px;
            background-color: #2c3e50;
            color: white;
            border: 2px solid #e74c3c;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
            z-index: 1000;
            text-align: center;
            font-size: 24px;
            font-weight: bold;
        }

        .popup button {
            background-color: #e74c3c;
            border: none;
            color: white;
            padding: 15px 30px;
            font-size: 18px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s, transform 0.1s ease;
            margin-top: 20px;
        }

        .popup button:hover {
            background-color: #c0392b;
        }

        .popup button:active {
            transform: scale(0.95);
        }

        .popup img {
            width: 50px;
            height: 50px;
            margin-bottom: 20px;
        }

        .problem-heading {
            color: #e74c3c;
            font-style: italic;
            margin-top: 10px;
            font-size: 16px;
            font-weight: bold;
        }

        .reminder-note {
            font-style: italic;
            font-size: 12px;
            text-align: right;
            margin-top: 5px;
            color: #333;
        }

        /* Progress bar */
        .progress-bar-container {
            width: 100%;
            height: 5px;
            background-color: #e0e0e0;
            border-radius: 5px;
            margin-top: 20px;
            overflow: hidden;
        }

        .progress-bar {
            height: 100%;
            width: 0;
            background-color: #f00;
            transition: width 0.5s ease-in-out, background-color 0.5s ease-in-out;
        }

        .scroll-locked {
            overflow: hidden;
        }

        .scroll-lock-notice {
            position: fixed;
            bottom: 10px;
            left: 10px;
            background-color: #e74c3c;
            color: white;
            padding: 10px;
            border-radius: 5px;
            z-index: 10000;
            font-size: 14px;
            display: none;
        }

        /* Animations */
        @keyframes fadeOut {
            0% {
                opacity: 1;
            }

            100% {
                opacity: 0;
            }
        }

        @keyframes vanish {
            0% {
                transform: scale(1);
                opacity: 1;
            }

            100% {
                transform: scale(0);
                opacity: 0;
            }
        }

        @keyframes explode {
            0% {
                transform: scale(1);
                opacity: 1;
            }

            100% {
                transform: scale(3);
                opacity: 0;
            }
        }

        .fadeOut {
            animation: fadeOut 0.3s forwards;
        }

        .vanish {
            animation: vanish 0.3s forwards;
        }

        .explode {
            animation: explode 0.3s forwards;
        }

        .highlight-added {
            background-color: #f4e542;
        }

        /* Credit Section */
        #credit {
            position: fixed;
            bottom: 10px;
            right: 10px;
            font-size: 12px;
            color: #34495e;
        }

        #credit a {
            color: #1171ba;
            text-decoration: none;
        }

        #credit a:hover {
            text-decoration: underline;
        }

        /* Right Sidebar for Buttons */
        #rightSidebar {
            margin-top: 20px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            align-items: flex-end;
            z-index: 999;
        }

        /* Options in the font control pane */
        .gap-control {
            display: flex;
            align-items: center;
            justify-content: flex-end;
            margin-top: 10px;
        }
    </style>
</head>

<body>
    <h1>
        <img src="https://raw.githubusercontent.com/prakashsharma19/hosted-images/main/pphlogo.png" alt="PPH Logo">
        Advertisements-PPH
    </h1>

    <!-- Clear memory button -->
    <button class="clear-memory-button" onclick="clearMemory()">Clear Memory</button>

    <!-- User Controls in upper-right corner -->
    <div id="userControls" style="display: none;">
        <img src="https://raw.githubusercontent.com/prakashsharma19/hosted-images/main/pphlogo.png" alt="PPH Logo">
        <span id="loggedInUser"></span>
        <button id="logoutButton" onclick="logout()">Logout</button>
    </div>

    <div class="login-container">
        <input type="text" id="username" placeholder="Enter your name">
        <input type="password" id="password" placeholder="Enter your password">
        <button id="loginButton" onclick="login()">Login</button>
    </div>

    <div class="font-controls" style="display:none;">
        <div class="control-group">
            <div>
                <label>
                    <input type="radio" name="cutOption" value="keyboard" checked>
                    Keyboard
                </label>
                <label>
                    <input type="radio" name="cutOption" value="mouse">
                    Mouse
                </label>
            </div>

            <div>
                <label for="effectsToggle">Effects:</label>
                <input type="checkbox" id="effectsToggle" onchange="saveEffectPreferences()">
            </div>

            <div>
                <label for="effectType">Effect:</label>
                <select id="effectType" onchange="saveEffectPreferences()">
                    <option value="none">None</option>
                    <option value="fadeOut">Fade Out</option>
                    <option value="vanish">Vanish</option>
                    <option value="explode">Explode</option>
                </select>
            </div>

            <div>
                <label for="fontStyle">Font:</label>
                <select id="fontStyle" onchange="updateFont()">
                    <option value="Arial">Arial</option>
                    <option value="Times New Roman">Times New Roman</option>
                    <option value="Courier New">Courier New</option>
                    <option value="Georgia">Georgia</option>
                    <option value="Calibri Light">Calibri Light</option>
                </select>
            </div>

            <div>
                <label for="fontSize">Size:</label>
                <input type="number" id="fontSize" value="16" onchange="updateFont()">px
            </div>

            <div class="gap-control">
                <label for="gapOption">Gap:</label>
                <select id="gapOption" onchange="saveGapPreferences()">
                    <option value="default">Default</option>
                    <option value="nil">Nil</option>
                </select>
            </div>
        </div>
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

    <!-- Incomplete Entries Box -->
    <div class="input-container" style="display:none;">
        <div class="container-header" onclick="toggleBox('incompleteBox')">
            Incomplete Entries
            <span id="incompleteBoxToggle">[+]</span>
        </div>
        <div id="incompleteBox" class="input-boxes">
            <textarea id="incompleteText" rows="5" placeholder="Incomplete entries will be shown here..."></textarea>
            <button onclick="copyIncompleteEntries()">Copy</button>
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
        <div id="remainingTime">File completed by: <span id="remainingTimeText"></span> (<span id="completionPercentage">0%</span>)
            <div class="hourglass"></div>
        </div>
    </div>

    <div id="adCount" style="display:none;">
        Total Advertisements: <span id="totalAds">0</span>
        <span id="loadingIndicator">Loading, please wait...</span>
    </div>
    <div id="dailyAdCount" style="display:none;">Total Ads Sent Today: 0</div>
    <div class="progress-bar-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>
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

        <!-- Button Container -->
        <div id="rightSidebar" style="display:none;">
            <button class="fullscreen-button" onclick="toggleFullScreen()">Full Screen</button>
            <button id="undoButton" style="display:none;" onclick="undoLastCut()">Undo Last Cut</button>
            <button id="lockButton" onclick="toggleLock()">🔒 Lock</button>
        </div>
    </div>

    <div id="reminderPopup" class="popup">
        <span style="font-size: 50px;">🔔</span>
        <p>Send Ads</p>
        <button onclick="dismissPopup()">OK</button>
    </div>

    <!-- Scroll Lock Notice -->
    <div id="scrollLockNotice" class="scroll-lock-notice">Scrolling is locked. Unlock to scroll.</div>

    <!-- Credit Section -->
    <div id="credit">
        This Web-App is Developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>.
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
            "Vietnam", "Yemen", "Zambia", "Zimbabwe", "UK", "USA", "U.S.A.", "U. S. A.", "Korea", "UAE", "Hong Kong", "Ivory Coast", "Cote d'Ivoire"
        ];

        let currentUser = null;
        let dailyAdCount = 0;
        let cutHistory = [];
        let isLocked = false;
        let isProcessing = false;
        let totalParagraphs = 0;
        let cutCooldown = false;

        function clearMemory() {
            const password = prompt('Please enter the password to clear memory:');
            if (password === 'cleanall') {
                localStorage.clear();
                alert('Memory cleared!');
            } else {
                alert('Incorrect password. Memory not cleared.');
            }
        }

        function saveText() {
            const inputText = document.getElementById('inputText').value;
            const roughText = document.getElementById('roughText').value;
            const outputText = document.getElementById('output').innerHTML;
            const incompleteText = document.getElementById('incompleteText').value;
            if (currentUser) {
                localStorage.setItem(`savedInput_${currentUser}`, inputText);
                localStorage.setItem(`savedRough_${currentUser}`, roughText);
                localStorage.setItem(`savedOutput_${currentUser}`, outputText);
                localStorage.setItem(`savedIncomplete_${currentUser}`, incompleteText);
                localStorage.setItem(`dailyAdCount_${currentUser}`, dailyAdCount);
                localStorage.setItem(`lastCutTime_${currentUser}`, Date.now());
                localStorage.setItem(`totalParagraphs_${currentUser}`, totalParagraphs);
                saveSelectedReminders();
                saveEffectPreferences();
                saveOperationPreferences();
                saveFontPreferences();
                saveGapPreferences();
            }
        }

        function loadText() {
            if (currentUser) {
                const savedInput = localStorage.getItem(`savedInput_${currentUser}`);
                const savedRough = localStorage.getItem(`savedRough_${currentUser}`);
                const savedOutput = localStorage.getItem(`savedOutput_${currentUser}`);
                const savedIncomplete = localStorage.getItem(`savedIncomplete_${currentUser}`);
                const savedDailyAdCount = localStorage.getItem(`dailyAdCount_${currentUser}`);
                const lastCutTime = localStorage.getItem(`lastCutTime_${currentUser}`);
                const savedTotalParagraphs = localStorage.getItem(`totalParagraphs_${currentUser}`);
                const savedFontStyle = localStorage.getItem(`fontStyle_${currentUser}`);
                const savedFontSize = localStorage.getItem(`fontSize_${currentUser}`);
                const savedGapOption = localStorage.getItem(`gapOption_${currentUser}`);
                if (savedInput) {
                    document.getElementById('inputText').value = savedInput;
                }
                if (savedRough) {
                    document.getElementById('roughText').value = savedRough;
                }
                if (savedOutput) {
                    document.getElementById('output').innerHTML = savedOutput;
                }
                if (savedIncomplete) {
                    document.getElementById('incompleteText').value = savedIncomplete;
                }
                if (savedDailyAdCount && lastCutTime) {
                    const lastCutDate = new Date(parseInt(lastCutTime, 10));
                    const currentDate = new Date();
                    if (lastCutDate.toDateString() === currentDate.toDateString()) {
                        dailyAdCount = parseInt(savedDailyAdCount, 10);
                    }
                }
                if (savedTotalParagraphs) {
                    totalParagraphs = parseInt(savedTotalParagraphs, 10);
                }
                if (savedFontStyle) {
                    document.getElementById('fontStyle').value = savedFontStyle;
                }
                if (savedFontSize) {
                    document.getElementById('fontSize').value = savedFontSize;
                }
                if (savedGapOption) {
                    document.getElementById('gapOption').value = savedGapOption;
                }
                loadEffectPreferences();
                loadOperationPreferences();
                loadSelectedReminders();
                updateCounts();
                updateFont();
                document.getElementById('rightSidebar').style.display = 'block';
                document.getElementById('lockButton').style.display = 'inline-block';
            }
        }

        function saveFontPreferences() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            if (currentUser) {
                localStorage.setItem(`fontStyle_${currentUser}`, fontStyle);
                localStorage.setItem(`fontSize_${currentUser}`, fontSize);
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
            let modifiedText = text.replace(/\?/g, '<span class="error">?</span>');
            if (!text.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
                modifiedText += ' <span class="error">Missing email</span>';
            }
            if (!countryList.some(country => text.includes(country))) {
                modifiedText += ' <span class="error">Missing country</span>';
            }
            return modifiedText;
        }

        function updateCounts() {
            const outputContainer = document.getElementById('output');
            const paragraphs = outputContainer.querySelectorAll('p');
            let adCount = 0;

            paragraphs.forEach(paragraph => {
                if (paragraph.innerText.split('\n')[0].startsWith('Professor')) {
                    adCount += 1;
                }
            });

            document.getElementById('totalAds').innerText = adCount;
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;

            const text = outputContainer.innerText;
            const countryCounts = countCountryOccurrences(text);
            const sortedCountries = Object.entries(countryCounts).sort((a, b) => b[1] - a[1]);
            let countryCountText = 'Country Counts:<br>';
            sortedCountries.forEach(([country, count]) => {
                countryCountText += `<b>${country}</b>: ${count}<br>`;
            });
            document.getElementById('countryCount').innerHTML = countryCountText.trim();

            updateProgressBar(dailyAdCount);
            updateRemainingTime(dailyAdCount);
        }

        function updateProgressBar(dailyAdCount) {
            const progressBar = document.getElementById('progressBar');
            const maxCount = 1200;

            const percentage = Math.min(dailyAdCount / maxCount, 1) * 100;
            progressBar.style.width = `${percentage}%`;

            const red = Math.max(255 - Math.floor((dailyAdCount / maxCount) * 255), 0);
            const green = Math.min(Math.floor((dailyAdCount / maxCount) * 255), 255);
            progressBar.style.backgroundColor = `rgb(${red},${green},0)`;
        }

        function updateRemainingTime(dailyAdCount) {
            const remainingEntries = totalParagraphs - dailyAdCount;
            const remainingTimeInMinutes = remainingEntries / 15;
            const remainingTimeInSeconds = remainingTimeInMinutes * 60;
            const hours = Math.floor(remainingTimeInSeconds / 3600);
            const minutes = Math.floor((remainingTimeInSeconds % 3600) / 60);

            const percentageCompleted = Math.min((dailyAdCount / totalParagraphs) * 100, 100).toFixed(2);

            document.getElementById('remainingTimeText').innerText = hours > 0 ? `${hours}h ${minutes}m` : `${minutes}m`;
            document.getElementById('completionPercentage').innerText = `${percentageCompleted}%`;
        }

        function processText() {
            if (isProcessing) return;

            isProcessing = true;
            document.getElementById('loadingIndicator').style.display = 'inline';

            const inputText = document.getElementById('inputText').value;
            const paragraphs = inputText.split(/\n\s*\n/);
            totalParagraphs = paragraphs.length;
            const outputContainer = document.getElementById('output');
            const incompleteContainer = document.getElementById('incompleteText');
            outputContainer.innerHTML = '<p id="cursorStart">Place your cursor here</p>';
            incompleteContainer.value = '';

            let index = 0;
            const nonRussiaEntries = [];
            const russiaEntries = [];

            const gapOption = document.getElementById('gapOption').value;

            function processChunk() {
                const chunkSize = 10;
                const end = Math.min(index + chunkSize, paragraphs.length);
                for (; index < end; index++) {
                    let paragraph = paragraphs[index].trim();
                    if (paragraph !== '') {
                        const lines = paragraph.split('\n');
                        let firstLine = lines[0].trim();
                        let lastName = firstLine.split(' ').pop();

                        if (!firstLine.toLowerCase().startsWith('professor')) {
                            // Add "Professor" if it's missing, and highlight it in yellow
                            firstLine = `<span class="highlight-added">Professor</span> ${firstLine}`;
                            lines[0] = firstLine;
                        }

                        const processedParagraph = lines.join('\n');
                        const greeting = `Dear Professor ${lastName},\n`;

                        // Check the gap option and apply it appropriately
                        const fullText = gapOption === 'nil' ?
                            processedParagraph + '\n' + greeting : processedParagraph + '\n\n' + greeting;

                        const highlightedText = highlightErrors(fullText.replace(/\n/g, '<br>'));
                        const hasError = highlightedText.includes('error');

                        if (hasError) {
                            incompleteContainer.value += `${highlightedText.replace(/<br>/g, '\n').replace(/<[^>]+>/g, '')}\n\n`;
                        } else {
                            const p = document.createElement('p');
                            p.innerHTML = highlightedText;

                            if (paragraph.includes('Russia')) {
                                russiaEntries.push(p);
                            } else {
                                nonRussiaEntries.push(p);
                            }
                        }
                    }
                }
                if (index < paragraphs.length) {
                    requestAnimationFrame(processChunk);
                } else {
                    nonRussiaEntries.forEach(entry => outputContainer.appendChild(entry));
                    russiaEntries.forEach(entry => outputContainer.appendChild(entry));

                    updateCounts();
                    saveText();
                    document.getElementById('lockButton').style.display = 'inline-block';
                    document.getElementById('loadingIndicator').style.display = 'none';
                    isProcessing = false;
                }
            }
            requestAnimationFrame(processChunk);
        }

        function cutParagraph(paragraph) {
            if (cutCooldown) return;
            cutCooldown = true;

            const textToCopy = paragraph.innerText;
            cutHistory.push(textToCopy);

            const effectType = document.getElementById('effectType').value;
            const effectsEnabled = document.getElementById('effectsToggle').checked;

            if (effectsEnabled && effectType !== 'none') {
                paragraph.classList.add(effectType);
                paragraph.addEventListener('animationend', () => {
                    copyAndRemoveParagraph(paragraph, textToCopy);
                });
            } else {
                copyAndRemoveParagraph(paragraph, textToCopy);
            }

            setTimeout(() => {
                cutCooldown = false;
            }, 500);
        }

        function copyAndRemoveParagraph(paragraph, textToCopy) {
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
            const remainingText = inputText.replace(textToCopy.split('\nDear Professor')[0], '').trim();
            document.getElementById('inputText').value = remainingText;

            dailyAdCount++;

            updateCounts();
            saveText();

            document.getElementById('undoButton').style.display = 'block';

            document.getElementById('output').focus();
        }

        function undoLastCut() {
            if (cutHistory.length > 0) {
                const lastCutText = cutHistory.pop();

                const outputContainer = document.getElementById('output');
                const p = document.createElement('p');
                p.innerText = lastCutText;
                outputContainer.insertBefore(p, outputContainer.firstChild);

                const inputText = document.getElementById('inputText').value;
                document.getElementById('inputText').value = `${lastCutText}\n\n${inputText}`.trim();

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
            saveFontPreferences();
        }

        function saveGapPreferences() {
            const gapOption = document.getElementById('gapOption').value;
            if (currentUser) {
                localStorage.setItem(`gapOption_${currentUser}`, gapOption);
            }
        }

        function toggleLock() {
            const lockButton = document.getElementById('lockButton');
            const interactiveElements = document.querySelectorAll('input, button, textarea, select');
            isLocked = !isLocked;

            if (isLocked) {
                lockButton.innerHTML = '🔓 Unlock';
                lockButton.classList.add('locked');
                interactiveElements.forEach(element => {
                    if (element.id !== 'output' && element.id !== 'undoButton' && element.id !== 'lockButton') {
                        element.disabled = true;
                    }
                });
                document.body.classList.add('scroll-locked');
            } else {
                lockButton.innerHTML = '🔒 Lock';
                lockButton.classList.remove('locked');
                interactiveElements.forEach(element => {
                    if (element.id !== 'output' && element.id !== 'undoButton' && element.id !== 'lockButton') {
                        element.disabled = false;
                    }
                });
                document.body.classList.remove('scroll-locked');
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
                document.getElementById('userControls').style.display = 'flex';
                document.getElementById('loggedInUser').innerText = username;
                loadText();
            } else {
                alert('Please enter both username and password.');
            }
        }

        function logout() {
            currentUser = null;
            document.querySelector('.login-container').style.display = 'block';
            document.querySelector('.font-controls').style.display = 'none';
            document.querySelectorAll('.input-container').forEach(container => container.style.display = 'none');
            document.querySelector('.top-controls').style.display = 'none';
            document.getElementById('adCount').style.display = 'none';
            document.getElementById('dailyAdCount').style.display = 'none';
            document.getElementById('remainingTime').style.display = 'none';
            document.getElementById('countryCount').style.display = 'none';
            document.getElementById('output').style.display = 'none';
            document.getElementById('userControls').style.display = 'none';
        }

        document.getElementById('output').addEventListener('click', function(event) {
            if (event.target.id === 'cursorStart') {
                startMonitoring();
            } else {
                handleMouseClick(event);
            }
        });

        document.querySelectorAll('input[name="cutOption"]').forEach(option => {
            option.addEventListener('change', saveOperationPreferences);
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
                    blinkBrowserIcon();
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

        // Handle slot selection and saving
        document.querySelectorAll('.reminder-slots li').forEach(slot => {
            slot.addEventListener('click', () => {
                slot.classList.toggle('selected');
                saveSelectedReminders();
            });
        });

        function saveSelectedReminders() {
            const selectedSlots = [];
            document.querySelectorAll('.reminder-slots li.selected').forEach(slot => {
                selectedSlots.push(slot.dataset.time);
            });
            localStorage.setItem(`selectedReminders_${currentUser}`, JSON.stringify(selectedSlots));
        }

        function loadSelectedReminders() {
            const savedSlots = localStorage.getItem(`selectedReminders_${currentUser}`);
            if (savedSlots) {
                const selectedSlots = JSON.parse(savedSlots);
                document.querySelectorAll('.reminder-slots li').forEach(slot => {
                    if (selectedSlots.includes(slot.dataset.time)) {
                        slot.classList.add('selected');
                    }
                });
            }
        }

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

        // Blink browser icon
        function blinkBrowserIcon() {
            if (document.hidden) {
                const favicon = document.querySelector('link[rel="icon"]');
                const originalIcon = favicon.href;
                let isOriginalIcon = true;
                const attentionIcon = 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/Alarm_bell.png/600px-Alarm_bell.png';

                const blinkFavicon = setInterval(() => {
                    favicon.href = isOriginalIcon ? attentionIcon : originalIcon;
                    isOriginalIcon = !isOriginalIcon;
                }, 500);

                document.addEventListener('visibilitychange', () => {
                    if (!document.hidden) {
                        clearInterval(blinkFavicon);
                        favicon.href = originalIcon;
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

        // Copy incomplete entries to clipboard
        function copyIncompleteEntries() {
            const incompleteText = document.getElementById('incompleteText').value;
            const tempTextarea = document.createElement('textarea');
            tempTextarea.style.position = 'fixed';
            tempTextarea.style.opacity = '0';
            tempTextarea.value = incompleteText;
            document.body.appendChild(tempTextarea);
            tempTextarea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextarea);
            alert('Incomplete entries copied to clipboard!');
        }

        // Handle scrolling lock and display notice
        document.addEventListener('wheel', function(event) {
            if (isLocked) {
                event.preventDefault();
                const scrollLockNotice = document.getElementById('scrollLockNotice');
                scrollLockNotice.style.display = 'block';
                setTimeout(() => {
                    scrollLockNotice.style.display = 'none';
                }, 2000);
            }
        }, { passive: false });

        function saveEffectPreferences() {
            const effectsEnabled = document.getElementById('effectsToggle').checked;
            const effectType = document.getElementById('effectType').value;
            if (currentUser) {
                localStorage.setItem(`effectsEnabled_${currentUser}`, effectsEnabled);
                localStorage.setItem(`effectType_${currentUser}`, effectType);
            }
        }

        function loadEffectPreferences() {
            const savedEffectsEnabled = localStorage.getItem(`effectsEnabled_${currentUser}`);
            const savedEffectType = localStorage.getItem(`effectType_${currentUser}`);
            if (savedEffectsEnabled) {
                document.getElementById('effectsToggle').checked = savedEffectsEnabled === 'true';
            }
            if (savedEffectType) {
                document.getElementById('effectType').value = savedEffectType;
            }
        }

        function saveOperationPreferences() {
            const selectedOption = document.querySelector('input[name="cutOption"]:checked').value;
            if (currentUser) {
                localStorage.setItem(`operationMode_${currentUser}`, selectedOption);
            }
        }

        function loadOperationPreferences() {
            const savedOperationMode = localStorage.getItem(`operationMode_${currentUser}`);
            if (savedOperationMode) {
                document.querySelector(`input[name="cutOption"][value="${savedOperationMode}"]`).checked = true;
            }
        }
    </script>
</body>

</html>
