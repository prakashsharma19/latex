<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text Selector and Copier</title>
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
        }
        .text-container {
            margin: 20px 0;
            padding: 10px;
            border: 1px solid #ccc;
            background-color: #fff;
            cursor: text;
            white-space: pre-wrap; /* Maintain text format */
        }
        .text-container p {
            margin: 10px 0;
        }
        #adCount {
            margin-left: 20px;
            font-size: 18px;
            font-weight: bold;
        }
        #dailyAdCount, #countryCount, #remainingTime {
            margin-top: 10px;
            font-size: 16px;
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
        .country-name {
            font-weight: bold;
        }
        .hourglass {
            font-size: 24px;
            margin-right: 10px;
            display: inline-block;
        }
        .hourglass::before {
            content: '⌛';
            animation: rotateHourglass 2s linear infinite;
        }
        @keyframes rotateHourglass {
            0% { transform: rotate(0deg); }
            50% { transform: rotate(180deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <h1>Text Selector and Copier</h1>
    <div class="font-controls">
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
    <div class="input-container">
        <textarea id="inputText" rows="10" cols="50" placeholder="Paste your text here..."></textarea>
        <button id="okButton" onclick="processText()">OK</button>
        <div id="adCount">Total Advertisements: 0</div>
    </div>
    <div id="output" class="text-container" contenteditable="true">
        <p id="cursorStart"><b>Place your cursor here</b></p>
    </div>
    <div id="dailyAdCount">Total Advertisements Today: 0</div>
    <div id="remainingTime">
        <span class="hourglass"></span>
        Remaining Time: Calculating...
    </div>
    <div id="countryCount"></div>
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
            "Vietnam", "Yemen", "Zambia", "Zimbabwe"
        ];

        let startTime;
        let cutCount = 0;

        function countOccurrences(text, word) {
            const regex = new RegExp(`\\b${word}\\b`, 'gi');
            return (text.match(regex) || []).length;
        }

        function updateCounts() {
            const outputContainer = document.getElementById('output');
            const text = outputContainer.innerText;
            const adCount = countOccurrences(text, 'professor');
            document.getElementById('adCount').innerText = `Total Advertisements: ${adCount}`;

            const countryCounts = {};
            const paragraphs = outputContainer.querySelectorAll('p');
            paragraphs.forEach(paragraph => {
                const text = paragraph.innerText.split(/\n/);
                for (let i = 0; i < text.length; i++) {
                    if (text[i].includes('@')) {
                        break;
                    }
                    countryList.forEach(country => {
                        if (text[i].toLowerCase().includes(country.toLowerCase())) {
                            countryCounts[country] = (countryCounts[country] || 0) + 1;
                        }
                    });
                }
            });

            let countryCountText = '';
            for (const country in countryCounts) {
                countryCountText += `<span class="country-name">${country}:</span> ${countryCounts[country]}; `;
            }
            document.getElementById('countryCount').innerHTML = countryCountText;
        }

        function processText() {
            const inputText = document.getElementById('inputText').value;
            const outputContainer = document.getElementById('output');
            outputContainer.innerHTML = '<p id="cursorStart"><b>Place your cursor here</b></p>'; // Clear previous content

            const paragraphs = inputText.split('\n\n');
            paragraphs.forEach(paragraphText => {
                const paragraph = document.createElement('p');
                paragraph.innerHTML = paragraphText.replace(/\n/g, '<br>');
                outputContainer.appendChild(paragraph);
            });

            updateCounts();
            document.getElementById('output').focus();
            const range = document.createRange();
            const sel = window.getSelection();
            range.setStart(outputContainer.childNodes[1], 0);
            range.collapse(true);
            sel.removeAllRanges();
            sel.addRange(range);
        }

        function updateFont() {
            const fontStyle = document.getElementById('fontStyle').value;
            const fontSize = document.getElementById('fontSize').value;
            document.getElementById('output').style.fontFamily = fontStyle;
            document.getElementById('output').style.fontSize = `${fontSize}px`;
        }

        document.getElementById('output').addEventListener('click', function(event) {
            if (event.target.id === 'cursorStart') {
                startMonitoring();
            }
        });

        function startMonitoring() {
            document.addEventListener('keyup', handleCursorMovement);
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

                if (paragraph && paragraph.textContent.toLowerCase().includes('professor')) {
                    cutParagraph(paragraph);
                    document.getElementById('output').focus();
                }
            }
        }

        function cutParagraph(paragraph) {
            if (!startTime) {
                startTime = new Date();
            }

            const selection = window.getSelection();
            const range = document.createRange();
            range.selectNodeContents(paragraph);
            selection.removeAllRanges();
            selection.addRange(range);

            const tempDiv = document.createElement('div');
            tempDiv.appendChild(range.cloneContents());
            const textToCopy = tempDiv.innerHTML;
            document.body.appendChild(tempDiv);

            const tempTextarea = document.createElement('textarea');
            tempTextarea.style.position = 'fixed';
            tempTextarea.style.opacity = '0';
            tempTextarea.value = paragraph.innerHTML.replace(/<br>/g, '\n');

            document.body.appendChild(tempTextarea);
            tempTextarea.select();
            document.execCommand('copy');
            document.body.removeChild(tempTextarea);
            document.body.removeChild(tempDiv);

            paragraph.remove();
            cleanupSpaces();
            updateCounts();
            updateDailyCount();
            updateRemainingTime();
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

        function updateDailyCount() {
            const today = new Date().toISOString().split('T')[0];
            const dailyCount = JSON.parse(localStorage.getItem('dailyAdCount')) || {};
            if (dailyCount.date !== today) {
                dailyCount.date = today;
                dailyCount.count = 0;
            }
            dailyCount.count += 1;
            localStorage.setItem('dailyAdCount', JSON.stringify(dailyCount));
            document.getElementById('dailyAdCount').innerText = `Total Advertisements Today: ${dailyCount.count}`;
        }

        function updateRemainingTime() {
            cutCount += 1;
            const elapsedTime = (new Date() - startTime) / 1000;
            const remainingAds = document.querySelectorAll('#output p').length;
            const speed = cutCount / elapsedTime; // ads per second
            const remainingTime = remainingAds / speed; // seconds
            const hours = Math.floor(remainingTime / 3600);
            const minutes = Math.floor((remainingTime % 3600) / 60);
            const seconds = Math.floor(remainingTime % 60);
            document.getElementById('remainingTime').innerHTML = `<span class="hourglass"></span>Remaining Time: ${hours}h ${minutes}m ${seconds}s`;
        }

        // Initialize daily count on page load
        document.addEventListener('DOMContentLoaded', () => {
            const dailyCount = JSON.parse(localStorage.getItem('dailyAdCount')) || { date: '', count: 0 };
            const today = new Date().toISOString().split('T')[0];
            if (dailyCount.date !== today) {
                dailyCount.date = today;
                dailyCount.count = 0;
                localStorage.setItem('dailyAdCount', JSON.stringify(dailyCount));
            }
            document.getElementById('dailyAdCount').innerText = `Total Advertisements Today: ${dailyCount.count}`;
        });
    </script>
</body>
</html>
