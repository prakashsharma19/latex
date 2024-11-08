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
        .login-container,
        .unsubscribe-container {
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

        .font-controls .control-group,
        .unsubscribe-container .control-group {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 10px;
        }

        .font-controls label,
        .unsubscribe-container label {
            font-weight: bold;
            color: #2c3e50;
        }

        .font-controls select,
        .font-controls input,
        .unsubscribe-container input {
            border-radius: 5px;
            padding: 5px;
            border: 1px solid #e0e0e0;
            font-size: 14px;
        }

        .font-controls input[type="number"] {
            width: 50px;
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

        #deleteUnsubscribedButton {
            background-color: #e74c3c;
            border: none;
            color: white;
            padding: 8px 15px;
            font-size: 14px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }

        #deleteUnsubscribedButton:hover {
            background-color: #c0392b;
        }

        .input-container {
            display: flex;
            flex-direction: column;
            align-items: center;
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

        .text-container {
            background-color: #ffffff;
            padding: 15px;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            margin-top: 20px;
        }

        .highlight-unsubscribed {
            background-color: #f8d7da;
            color: #721c24;
            padding: 2px 5px;
            border-radius: 3px;
        }

        .highlight-added {
            background-color: #f4e542;
        }

        /* Right Sidebar for Buttons */
        #rightSidebar {
            display: flex;
            flex-direction: column;
            gap: 10px;
            align-items: flex-end;
        }
    </style>
</head>

<body>
    <h1>
        <img src="https://raw.githubusercontent.com/prakashsharma19/hosted-images/main/pphlogo.png" alt="PPH Logo">
        Advertisements-PPH
    </h1>

    <div class="login-container">
        <input type="text" id="username" placeholder="Enter your name">
        <input type="password" id="password" placeholder="Enter your password">
        <button id="loginButton" onclick="login()">Login</button>
    </div>

    <div class="unsubscribe-container" style="display: none;">
        <div class="control-group">
            <label for="unsubscribeEmails">Unsubscribed Emails:</label>
            <input type="text" id="unsubscribeEmails" placeholder="Enter email addresses separated by commas">
            <button onclick="addUnsubscribedEmails()">OK</button>
            <button id="deleteUnsubscribedButton" onclick="deleteProcessedEntriesForUnsubscribed()">Delete All Unsubscribed Entries</button>
        </div>
    </div>

    <div class="font-controls" style="display:none;">
        <div class="control-group">
            <label>
                <input type="radio" name="cutOption" value="keyboard" checked>
                Keyboard
            </label>
            <label>
                <input type="radio" name="cutOption" value="mouse">
                Mouse
            </label>

            <label for="toPrefix">Prefix "To":</label>
            <input type="radio" name="toOption" value="yes" onchange="saveToPrefixPreference()"> Yes
            <input type="radio" name="toOption" value="no" checked onchange="saveToPrefixPreference()"> No
        </div>
    </div>

    <div class="input-container" style="display:none;">
        <textarea id="inputText" rows="5" placeholder="Paste your text here..."></textarea>
        <button id="okButton" onclick="processText()">OK</button>
    </div>

    <div id="output" class="text-container" style="display:none;"></div>

    <div id="rightSidebar" style="display:none;">
        <button onclick="toggleFullScreen()">Full Screen</button>
        <button onclick="undoLastCut()">Undo Last Cut</button>
        <button onclick="toggleLock()">Lock</button>
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
        let unsubscribedEmails = [];

        function login() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username && password) {
                currentUser = `${username}_${password}`;
                document.querySelector('.login-container').style.display = 'none';
                document.querySelector('.font-controls').style.display = 'block';
                document.querySelector('.unsubscribe-container').style.display = 'block';
                document.querySelector('.input-container').style.display = 'flex';
                document.getElementById('output').style.display = 'block';
                document.getElementById('rightSidebar').style.display = 'block';
                loadPreferences();
            } else {
                alert('Please enter both username and password.');
            }
        }

        function loadPreferences() {
            const savedUnsubscribedEmails = localStorage.getItem('unsubscribedEmails');
            unsubscribedEmails = savedUnsubscribedEmails ? JSON.parse(savedUnsubscribedEmails) : [];
            const savedToPrefix = localStorage.getItem('toPrefixOption');
            document.querySelector(`input[name="toOption"][value="${savedToPrefix || 'no'}"]`).checked = true;
        }

        function saveToPrefixPreference() {
            const toPrefixOption = document.querySelector('input[name="toOption"]:checked').value;
            localStorage.setItem('toPrefixOption', toPrefixOption);
        }

        function addUnsubscribedEmails() {
            const inputEmails = document.getElementById('unsubscribeEmails').value.split(',');
            unsubscribedEmails = [...new Set([...unsubscribedEmails, ...inputEmails.map(email => email.trim())])];
            localStorage.setItem('unsubscribedEmails', JSON.stringify(unsubscribedEmails));
            document.getElementById('unsubscribeEmails').value = '';
        }

        function deleteProcessedEntriesForUnsubscribed() {
            const outputContainer = document.getElementById('output');
            const paragraphs = Array.from(outputContainer.querySelectorAll('p'));
            paragraphs.forEach(paragraph => {
                const emailLine = paragraph.innerHTML.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/);
                if (emailLine && unsubscribedEmails.includes(emailLine[0])) {
                    paragraph.remove();
                }
            });
        }

        function processText() {
            const inputText = document.getElementById('inputText').value.trim();
            const paragraphs = inputText.split(/\n\s*\n/);
            const outputContainer = document.getElementById('output');
            outputContainer.innerHTML = ''; // Clear previous output

            const toPrefixOption = document.querySelector('input[name="toOption"]:checked').value;

            paragraphs.forEach(paragraph => {
                if (paragraph) {
                    let lines = paragraph.split('\n').map(line => line.trim());
                    const emailLine = lines.find(line => line.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/));

                    // Highlight unsubscribed email addresses
                    if (emailLine && unsubscribedEmails.includes(emailLine)) {
                        paragraph = `<span class="highlight-unsubscribed">${paragraph}</span>`;
                    }

                    // Automatically add "Professor" if missing and highlight it
                    if (!lines[0].toLowerCase().startsWith('professor')) {
                        lines[0] = `<span class="highlight-added">Professor</span> ${lines[0]}`;
                    }

                    const lastName = lines[0].split(' ').pop();
                    const greeting = `Dear Professor ${lastName},`;

                    const prefixTo = toPrefixOption === 'yes' ? 'To<br>' : '';

                    const finalText = `${prefixTo}${lines.join('<br>')}<br><br>${greeting}`;
                    const p = document.createElement('p');
                    p.innerHTML = finalText;

                    outputContainer.appendChild(p);
                }
            });
        }
    </script>
</body>

</html>
