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
            overflow: hidden; /* Prevent scrolling when locked */
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

        .clear-memory-button {
            background-color: red;
            color: white;
            padding: 10px 20px;
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
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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

        .copy-button,
        #okButton,
        #undoButton,
        #lockButton,
        #startButton {
            border: none;
            color: white;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s, transform 0.1s ease;
            margin-top: 10px;
        }

        #loginButton {
            background-color: #007bff;
            margin-top: 10px;
            font-size: 16px;
            padding: 12px 24px;
            font-weight: bold;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            transition: background-color 0.3s;
        }

        #loginButton:hover {
            background-color: #0056b3;
        }

        #loginButton:active {
            transform: scale(0.95);
        }

        #lockButton {
            margin-left: 20px;
            background-color: #1171ba;
        }

        #lockButton:hover {
            background-color: #0e619f;
        }

        #undoButton {
            margin-left: 20px;
            background-color: #1171ba;
        }

        #startButton {
            margin-left: 20px;
            background-color: #28a745;
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

        .rough-container,
        .incomplete-container {
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

        #journalName {
            position: absolute;
            left: 20px;
            top: 220px;
            font-size: 16px;
            font-weight: bold;
            line-height: 1.5;
            color: #34495e;
        }

        #cursorStart {
            font-weight: bold;
            color: #3498db;
        }

        #credits {
            position: absolute;
            bottom: 20px;
            width: 100%;
            text-align: center;
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

        #usernameDisplay {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 16px;
            color: #34495e;
            cursor: pointer;
        }

        .error {
            color: #e74c3c;
            font-weight: bold;
            font-style: italic;
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
        .progress-bar {
            height: 5px;
            width: 0;
            background-color: red;
            transition: width 0.5s ease-in-out, background-color 0.5s ease-in-out;
            border-radius: 2px;
            margin-top: 10px;
        }

        /* Styles for the "Incomplete Entries" box */
        .incomplete-container {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
        }

        .incomplete-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            background-color: #e74c3c;
            color: white;
            padding: 10px;
            border-radius: 5px;
        }

        .copy-button {
            background-color: #28a745;
            margin-left: 20px;
        }

        .copy-button:hover {
            background-color: #218838;
        }

        .copy-button:active {
            transform: scale(0.95);
        }

    </style>
</head>

<body>
    <h1>Advertisements-PPH</h1>

    <!-- Clear memory button -->
    <button class="clear-memory-button" onclick="clearMemory()">Clear Memory</button>

    <!-- Username display -->
    <div id="usernameDisplay" onclick="showLogout()"></div>

    <!-- Credits in bottom-center -->
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
        <input type="text" id="journalAbbr" placeholder="Enter journal abbreviation">
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

    <!-- Incomplete Entries Box -->
    <div class="input-container" style="display:none;">
        <div class="container-header incomplete-header" onclick="toggleBox('incompleteBox')">
            Incomplete Entries
            <span id="incompleteBoxToggle">[+]</span>
        </div>
        <div id="incompleteBox" class="input-boxes incomplete-container">
            <textarea id="incompleteText" rows="5" readonly></textarea>
            <button class="copy-button" onclick="copyIncompleteEntries()">Copy</button>
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
        <button id="lockButton" style="display:none;" title="Lock to prevent accidental inputs" onmouseover="showLockHint()" onclick="toggleLock()">🔒 Lock</button>
        <button id="startButton" onclick="startProcessing()">Start</button>
    </div>

    <div id="adCount" style="display:none;">
        Total Advertisements: <span id="totalAds">0</span>
        <span id="loadingIndicator">Loading, please wait...</span>
    </div>
    <div id="dailyAdCount" style="display:none;">
        Total Ads Sent Today: 0
        <span class="info-icon" onclick="showAdHistory()">ℹ️</span>
    </div>
    <div class="progress-bar" id="progressBar"></div>
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
        <span style="font-size: 50px;">🔔</span>
        <p>Send Ads</p>
        <button onclick="dismissPopup()">OK</button>
    </div>

    <script>
        let currentUser = null;
        let dailyAdCount = 0;
        let totalTimeInSeconds = 0;
        let cutHistory = [];
        let isLocked = false;
        let isProcessing = false; // Flag to prevent multiple processing
        let journalFullName = '';
        const journalAbbreviations = {
            DM: 'Advances and Applications in Discrete Mathematics',
            AADM: 'Advances and Applications in Discrete Mathematics',
            FM: 'Advances and Applications in Fluid Mechanics',
            AAFM: 'Advances and Applications in Fluid Mechanics',
            ADAS: 'Advances and Applications in Statistics',
            DE: 'Advances in Differential Equations and Control Processes',
            ADECP: 'Advances in Differential Equations and Control Processes',
            AFSS: 'Advances in Fuzzy Sets and Systems',
            fuzzy: 'Advances in Fuzzy Sets and Systems',
            AM: 'Far East Journal of Applied Mathematics',
            FJAM: 'Far East Journal of Applied Mathematics',
            DS: 'Far East Journal of Dynamical Systems',
            FJDS: 'Far East Journal of Dynamical Systems',
            ME: 'Far East Journal of Mathematical Education',
            FJME: 'Far East Journal of Mathematical Education',
            MS: 'Far East Journal of Mathematical Sciences',
            FJMS: 'Far East Journal of Mathematical Sciences',
            TS: 'Far East Journal of Theoretical Statistics',
            FJTS: 'Far East Journal of Theoretical Statistics',
            MET: 'International Journal of Materials Engineering and Technology',
            IJMET: 'International Journal of Materials Engineering and Technology',
            NM: 'International Journal of Numerical Methods and Applications',
            IJNMA: 'International Journal of Numerical Methods and Applications',
            IJND: 'International Journal of Nutrition and Dietetics',
            ANT: 'JP Journal of Algebra, Number Theory and Applications',
            JPANTA: 'JP Journal of Algebra, Number Theory and Applications',
            Bio: 'JP Journal of Biostatistics',
            JPJB: 'JP Journal of Biostatistics',
            GT: 'JP Journal of Geometry and Topology',
            JPGT: 'JP Journal of Geometry and Topology',
            HMT: 'JP Journal of Heat and Mass Transfer',
            JPHMT: 'JP Journal of Heat and Mass Transfer',
            UJMS: 'Universal Journal of Mathematics and Mathematical Sciences',
            UJMMS: 'Universal Journal of Mathematics and Mathematical Sciences'
        };

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
            if (currentUser) {
                localStorage.setItem(`savedInput_${currentUser}`, inputText);
                localStorage.setItem(`savedRough_${currentUser}`, roughText);
                localStorage.setItem(`savedOutput_${currentUser}`, outputText);
                localStorage.setItem(`dailyAdCount_${currentUser}`, dailyAdCount);
                localStorage.setItem(`lastCutTime_${currentUser}`, Date.now());
                saveSelectedReminders();
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
                loadSelectedReminders();
                updateCounts();
                updateRemainingTime(); // Ensure remaining time is updated on login
                ensureProblemHeading();
                document.getElementById('lockButton').style.display = 'inline-block';
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
            const text = outputContainer.innerText;
            const adCount = countOccurrences(text, 'professor');
            document.getElementById('totalAds').innerText = adCount;
            document.getElementById('dailyAdCount').innerText = `Total Ads Today: ${dailyAdCount}`;

            const countryCounts = countCountryOccurrences(text);
            const sortedCountries = Object.entries(countryCounts).sort((a, b) => b[1] - a[1]);
            let countryCountText = 'Country Counts:<br>';
            sortedCountries.forEach(([country, count]) => {
                countryCountText += `<b>${country}</b>: ${count}<br>`;
            });
            document.getElementById('countryCount').innerHTML = countryCountText.trim();

            updateRemainingTime();
            updateProgressBar(dailyAdCount);
        }

        function updateProgressBar(dailyAdCount) {
            const progressBar = document.getElementById('progressBar');
            const maxCount = 1500; // Updated to 1500 ads for full bar

            const percentage = Math.min(dailyAdCount / maxCount, 1) * 100;
            progressBar.style.width = `${percentage}%`;

            // RGB transition from red to green
            const red = Math.max(255 - Math.floor((dailyAdCount / maxCount) * 255), 0);
            const green = Math.min(Math.floor((dailyAdCount / maxCount) * 255), 255);
            progressBar.style.backgroundColor = `rgb(${red},${green},0)`;
        }

        function updateRemainingTime() {
            const adCount = document.getElementById('totalAds').innerText;
            const remainingTimeInMinutes = adCount / 9; // Calculating based on total ads (9 ads/min)
            const remainingTimeInSeconds = remainingTimeInMinutes * 60;
            const hours = Math.floor(remainingTimeInSeconds / 3600);
            const minutes = Math.floor((remainingTimeInSeconds % 3600) / 60);

            document.getElementById('remainingTimeText').innerText = hours > 0 ? `${hours}h ${minutes}m` : `${minutes}m`;
        }

        function processText() {
            if (isProcessing) return; // Prevent multiple processing

            isProcessing = true;
            document.getElementById('loadingIndicator').style.display = 'inline'; // Show loading indicator

            const inputText = document.getElementById('inputText').value;
            const paragraphs = inputText.split(/\n\n/); // Separate paragraphs more reliably
            const outputContainer = document.getElementById('output');
            const incompleteContainer = document.getElementById('incompleteText');
            outputContainer.innerHTML = ''; // Clear existing content
            incompleteContainer.value = ''; // Clear existing incomplete entries

            const totalAds = countOccurrences(inputText, 'professor');
            totalTimeInSeconds = totalAds * 8;

            let index = 0;

            function processChunk() {
                const chunkSize = 10; // Reduce chunk size for better separation
                const end = Math.min(index + chunkSize, paragraphs.length);
                for (; index < end; index++) {
                    const paragraph = paragraphs[index];
                    if (paragraph.trim() !== '') {
                        const highlightedParagraph = highlightErrors(paragraph.replace(/\n/g, '<br>'));
                        if (highlightedParagraph.includes('error')) {
                            incompleteContainer.value += highlightedParagraph.replace(/<[^>]*>/g, '') + '\n\n';
                        } else {
                            const p = document.createElement('p');
                            p.innerHTML = highlightedParagraph;
                            outputContainer.appendChild(p);
                        }
                    }
                }
                if (index < paragraphs.length) {
                    requestAnimationFrame(processChunk);
                } else {
                    updateCounts();
                    saveText();
                    document.getElementById('lockButton').style.display = 'inline-block';

                    document.getElementById('loadingIndicator').style.display = 'none'; // Hide loading indicator
                    isProcessing = false; // Reset processing flag
                }
            }
            requestAnimationFrame(processChunk);
        }

        function startProcessing() {
            processText(); // Ensure it only processes the text once
        }

        function ensureProblemHeading() {
            const outputContainer = document.getElementById('output');
            if (!document.querySelector('.problem-heading')) {
                const problemHeading = document.createElement('p');
                problemHeading.className = 'problem-heading';
                problemHeading.innerText = 'Check before sent';
                outputContainer.appendChild(problemHeading);
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
            document.getElementById('inputText').value = updatedText ? updatedText + "\n\n" : updatedText;

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
                document.body.style.overflow = 'hidden'; // Lock scrolling
            } else {
                lockButton.innerHTML = '🔒 Lock';
                interactiveElements.forEach(element => {
                    if (element.id !== 'output' && element.id !== 'undoButton' && element.id !== 'lockButton') {
                        element.disabled = false;
                    }
                });
                document.body.style.overflow = ''; // Unlock scrolling
            }
        }

        function showLockHint() {
            document.getElementById('lockButton').title = 'Lock to prevent accidental inputs';
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
            const journalAbbr = document.getElementById('journalAbbr').value.toUpperCase();

            if (username && password && journalAbbr) {
                currentUser = `${username}_${password}`;
                journalFullName = journalAbbreviations[journalAbbr] || 'Unknown Journal';
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelectorAll('.input-container').forEach(container => container.style.display = 'block');
                document.querySelector('.top-controls').style.display = 'flex';
                document.getElementById('adCount').style.display = 'block';
                document.getElementById('dailyAdCount').style.display = 'block';
                document.getElementById('remainingTime').style.display = 'block';
                document.getElementById('countryCount').style.display = 'block';
                document.getElementById('output').style.display = 'block';
                document.getElementById('usernameDisplay').innerText = username;
                document.getElementById('usernameDisplay').style.display = 'block';
                document.getElementById('journalName').innerText = `Journal Name: ${journalFullName}`;
                document.getElementById('journalName').style.display = 'block';
                loadText();
            } else {
                alert('Please enter username, password, and journal abbreviation.');
            }
        }

        function showLogout() {
            const logoutConfirm = confirm('Do you want to logout?');
            if (logoutConfirm) {
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
                document.getElementById('usernameDisplay').style.display = 'none';
                document.getElementById('journalName').style.display = 'none';
            }
        }

        function copyIncompleteEntries() {
            const incompleteText = document.getElementById('incompleteText').value;
            navigator.clipboard.writeText(incompleteText).then(() => {
                alert('Incomplete entries copied to clipboard.');
            });
        }

        function showAdHistory() {
            // Implement logic to show last 5 days "total ads sent counts"
            alert('Last 5 days "total ads sent counts" will be displayed here with a small progress bar.');
        }

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
                    blinkBrowserIcon(); // Blink browser icon for attention
                }
            });
        }

        // Check reminders every minute
        setInterval(checkReminders, 60000);

        // Show the reminder popup
        function showPopup() {
            if (!isLocked) { // Only show popup if not locked
                document.getElementById('reminderPopup').style.display = 'block';
                blinkTab();
            }
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

        // Handle window close event
        window.addEventListener('beforeunload', function (e) {
            e.preventDefault();
            e.returnValue = 'Are you sure you want to close? You will lose the reminder notifications. Please minimize instead.';
        });
    </script>
</body>

</html>
