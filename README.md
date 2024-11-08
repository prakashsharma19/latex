<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        /* Add your original styles here to support layout and all elements */
    </style>
</head>

<body>
    <h1>
        <img src="https://raw.githubusercontent.com/prakashsharma19/hosted-images/main/pphlogo.png" alt="PPH Logo">
        Advertisements-PPH
    </h1>

    <!-- Login Section -->
    <div class="login-container">
        <input type="text" id="username" placeholder="Enter your name">
        <input type="password" id="password" placeholder="Enter your password">
        <button id="loginButton" onclick="login()">Login</button>
    </div>

    <!-- Unsubscribed Emails Field -->
    <div class="unsubscribe-container" style="display:none;">
        <div class="control-group">
            <label for="unsubscribeEmails">Unsubscribed Emails:</label>
            <input type="text" id="unsubscribeEmails" placeholder="Enter emails separated by commas">
            <button onclick="addUnsubscribedEmails()">OK</button>
            <button id="deleteUnsubscribedButton" onclick="deleteProcessedEntriesForUnsubscribed()">Delete All Unsubscribed Entries</button>
        </div>
    </div>

    <!-- Font and Effects Control Panel -->
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
            <div>
                <label for="gapOption">Gap:</label>
                <select id="gapOption" onchange="saveGapPreferences()">
                    <option value="default">Default</option>
                    <option value="nil">Nil</option>
                </select>
            </div>
            <div>
                <label>Prefix "To":</label>
                <input type="radio" name="toOption" value="yes" onclick="saveToPrefixPreference()"> Yes
                <input type="radio" name="toOption" value="no" checked onclick="saveToPrefixPreference()"> No
            </div>
        </div>
    </div>

    <!-- Paste Text Container -->
    <div class="input-container" style="display:none;">
        <div class="container-header" onclick="toggleBox('pasteBox')">
            Paste your text here
            <span id="pasteBoxToggle">[+]</span>
        </div>
        <div id="pasteBox" class="input-boxes">
            <textarea id="inputText" rows="5" placeholder="Paste your text here..."></textarea>
            <button id="okButton" onclick="processText()">Process</button>
        </div>
    </div>

    <!-- Output Container with Cursor Start Point -->
    <div id="output" class="text-container" style="display:none;" contenteditable="true">
        <p id="cursorStart">Place your cursor here</p>
    </div>

    <!-- Sidebar with Reminder Slots and Buttons -->
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
        <div class="reminder-note">(Select your slots to get reminders)</div>
        <div id="rightSidebar" style="display:none;">
            <button class="fullscreen-button" onclick="toggleFullScreen()">Full Screen</button>
            <button id="undoButton" style="display:none;" onclick="undoLastCut()">Undo Last Cut</button>
            <button id="lockButton" onclick="toggleLock()">Lock</button>
        </div>
    </div>

    <!-- Progress Bar -->
    <div class="progress-bar-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <!-- Popup Reminder -->
    <div id="reminderPopup" class="popup">
        <span style="font-size: 50px;">🔔</span>
        <p>Send Ads</p>
        <button onclick="dismissPopup()">OK</button>
    </div>

    <!-- Credit -->
    <div id="credit">
        This Web-App is Developed by <a href="https://prakashsharma19.github.io/prakash/" target="_blank">Prakash</a>
    </div>

    <script>
        const countryList = ["Afghanistan", "Albania", "Algeria", /* add all countries */ "Zimbabwe"];
        let currentUser = null;
        let unsubscribedEmails = [];
        let dailyAdCount = 0;
        let totalParagraphs = 0;
        let cutHistory = [];

        // Login Functionality
        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                currentUser = `${username}_${password}`;
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.unsubscribe-container').style.display = 'block';
                document.getElementById('output').style.display = 'block';
                document.getElementById('rightSidebar').style.display = 'block';
                loadPreferences();
            } else {
                alert('Please enter both username and password.');
            }
        }

        function loadPreferences() {
            unsubscribedEmails = JSON.parse(localStorage.getItem('unsubscribedEmails') || '[]');
            const savedToPrefix = localStorage.getItem('toPrefixOption');
            document.querySelector(`input[name="toOption"][value="${savedToPrefix || 'no'}"]`).checked = true;
        }

        function addUnsubscribedEmails() {
            const emails = document.getElementById('unsubscribeEmails').value.split(',').map(email => email.trim());
            unsubscribedEmails.push(...emails);
            localStorage.setItem('unsubscribedEmails', JSON.stringify([...new Set(unsubscribedEmails)]));
            document.getElementById('unsubscribeEmails').value = '';
        }

        function deleteProcessedEntriesForUnsubscribed() {
            const outputContainer = document.getElementById('output');
            const paragraphs = Array.from(outputContainer.querySelectorAll('p'));
            paragraphs.forEach(paragraph => {
                const email = (paragraph.innerText.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/) || [])[0];
                if (email && unsubscribedEmails.includes(email)) paragraph.remove();
            });
        }

        function saveToPrefixPreference() {
            const toOption = document.querySelector('input[name="toOption"]:checked').value;
            localStorage.setItem('toPrefixOption', toOption);
        }

        function processText() {
            const inputText = document.getElementById('inputText').value;
            const paragraphs = inputText.split(/\n\s*\n/);
            totalParagraphs = paragraphs.length;
            const outputContainer = document.getElementById('output');
            outputContainer.innerHTML = '';

            const toOption = localStorage.getItem('toPrefixOption') === 'yes';
            paragraphs.forEach(paragraph => {
                const lines = paragraph.trim().split('\n');
                if (!lines[0].toLowerCase().startsWith('professor')) {
                    lines[0] = `<span class="highlight-added">Professor</span> ${lines[0]}`;
                }
                const lastName = lines[0].split(' ').pop();
                const greeting = `Dear Professor ${lastName},`;
                const processedText = `${toOption ? 'To<br>' : ''}${lines.join('<br>')}<br><br>${greeting}`;
                const p = document.createElement('p');
                p.innerHTML = processedText;
                const email = (processedText.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/) || [])[0];
                if (email && unsubscribedEmails.includes(email)) {
                    p.classList.add('highlight-unsubscribed');
                }
                outputContainer.appendChild(p);
            });
        }
    </script>
</body>

</html>
