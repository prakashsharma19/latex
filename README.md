<!DOCTYPE html>
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

    <button class="clear-memory-button" onclick="clearMemory()">Clear Memory</button>

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

    <!-- Unsubscribe Email Management Section -->
    <div class="input-container">
        <div class="container-header" onclick="toggleBox('unsubscribeBox')">
            Manage Unsubscribed Emails
            <span id="unsubscribeBoxToggle">[+]</span>
        </div>
        <div id="unsubscribeBox" class="input-boxes">
            <input type="text" id="unsubscribeEmail" placeholder="Enter email to unsubscribe">
            <button onclick="addUnsubscribedEmail()">Add to Unsubscribed</button>
            <button onclick="deleteUnsubscribedEmails()">Delete All Unsubscribed Emails</button>
            <textarea id="unsubscribeList" rows="5" readonly placeholder="Unsubscribed emails..."></textarea>
        </div>
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

    <!-- Additional Controls, Remaining Time Section, Country Count, etc. -->

    <div id="output" class="text-container" contenteditable="true">
        <p id="cursorStart">Place your cursor here</p>
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
            "Vietnam", "Yemen", "Zambia", "Zimbabwe", "UK", "USA", "U.S.A.", "U. S. A.", "Korea", "UAE", "Hong Kong", "Ivory Coast", "Cote d'Ivoire", "Macau", "Macao", "Macedonia"
        ];

        let unsubscribedEmails = JSON.parse(localStorage.getItem('unsubscribedEmails')) || [];

        function addUnsubscribedEmail() {
            const email = document.getElementById('unsubscribeEmail').value.trim();
            if (email && !unsubscribedEmails.includes(email)) {
                unsubscribedEmails.push(email);
                localStorage.setItem('unsubscribedEmails', JSON.stringify(unsubscribedEmails));
                updateUnsubscribeList();
                alert(`Added ${email} to unsubscribe list.`);
                document.getElementById('unsubscribeEmail').value = '';
            } else {
                alert('Email is already unsubscribed or empty.');
            }
        }

        function deleteUnsubscribedEmails() {
            if (confirm('Are you sure you want to delete all unsubscribed emails?')) {
                unsubscribedEmails = [];
                localStorage.removeItem('unsubscribedEmails');
                updateUnsubscribeList();
                alert('All unsubscribed emails deleted.');
            }
        }

        function updateUnsubscribeList() {
            document.getElementById('unsubscribeList').value = unsubscribedEmails.join('\n');
        }

        updateUnsubscribeList();

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

        function processText() {
            if (isProcessing) return;

            isProcessing = true;
            document.getElementById('loadingIndicator').style.display = 'inline';

            const inputText = document.getElementById('inputText').value;
            const paragraphs = inputText.split(/\n\s*\n/);
            const outputContainer = document.getElementById('output');
            outputContainer.innerHTML = '<p id="cursorStart">Place your cursor here</p>';
            const incompleteContainer = document.getElementById('incompleteText');
            incompleteContainer.value = '';

            let index = 0;

            function processChunk() {
                const chunkSize = 10;
                const end = Math.min(index + chunkSize, paragraphs.length);

                for (; index < end; index++) {
                    let paragraph = paragraphs[index].trim();
                    if (paragraph !== '') {
                        const lines = paragraph.split('\n');
                        let firstLine = lines[0].trim();
                        let lastName = firstLine.split(' ').pop();

                        // Add "To" prefix and "Professor" title if missing
                        if (!firstLine.toLowerCase().startsWith('professor')) {
                            firstLine = `<span class="highlight-added">Professor</span> ${firstLine}`;
                            lines[0] = firstLine;
                        }
                        const processedParagraph = "To\n" + lines.join('\n');
                        const greeting = `Dear Professor ${lastName},\n`;

                        const fullText = processedParagraph + '\n\n' + greeting;
                        let highlightedText = highlightErrors(fullText.replace(/\n/g, '<br>'));

                        // Highlight unsubscribed emails
                        unsubscribedEmails.forEach(email => {
                            if (highlightedText.includes(email)) {
                                highlightedText = highlightedText.replace(
                                    new RegExp(email, 'g'),
                                    `<span class="error">${email}</span>`
                                );
                            }
                        });

                        const p = document.createElement('p');
                        p.innerHTML = highlightedText;
                        outputContainer.appendChild(p);
                    }
                }

                if (index < paragraphs.length) {
                    requestAnimationFrame(processChunk);
                } else {
                    saveText();
                    isProcessing = false;
                    document.getElementById('loadingIndicator').style.display = 'none';
                }
            }

            requestAnimationFrame(processChunk);
        }

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
            const outputText = document.getElementById('output').innerHTML;
            if (currentUser) {
                localStorage.setItem(`savedInput_${currentUser}`, inputText);
                localStorage.setItem(`savedOutput_${currentUser}`, outputText);
            }
        }
    </script>
</body>

</html>
