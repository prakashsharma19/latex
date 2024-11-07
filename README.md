<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advertisements-PPH</title>
    <style>
        /* (CSS styling to control layout, colors, animations, and various UI components) */
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
        .input-container {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            flex-direction: column;
            align-items: center;
        }
        .input-container textarea, .input-container input {
            width: 100%;
            border-radius: 5px;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #e0e0e0;
            margin-top: 10px;
        }
        .error {
            color: #e74c3c;
            font-weight: bold;
            font-style: italic;
        }
    </style>
</head>
<body>
    <!-- Header Section -->
    <h1>
        <img src="https://raw.githubusercontent.com/prakashsharma19/hosted-images/main/pphlogo.png" alt="PPH Logo">
        Advertisements-PPH
    </h1>

    <!-- Clear Memory Button -->
    <button class="clear-memory-button" onclick="clearMemory()">Clear Memory</button>

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

    <!-- Input Section for Text Processing -->
    <div class="input-container">
        <textarea id="inputText" rows="5" placeholder="Enter or paste text to process..."></textarea>
        <button onclick="processText()">Process Text</button>
    </div>

    <!-- Output Section for Processed Text -->
    <div id="output" class="text-container" contenteditable="true">
        <p id="cursorStart">Place your cursor here</p>
    </div>

    <script>
        // JavaScript for Unsubscribe Feature, Processing Text, Highlighting, and Saving to Local Storage

        // Unsubscribe email list, stored in localStorage
        let unsubscribedEmails = JSON.parse(localStorage.getItem('unsubscribedEmails')) || [];

        // Function to add an email to the unsubscribe list
        function addUnsubscribedEmail() {
            const email = document.getElementById('unsubscribeEmail').value.trim();
            if (email && !unsubscribedEmails.includes(email)) {
                unsubscribedEmails.push(email);
                localStorage.setItem('unsubscribedEmails', JSON.stringify(unsubscribedEmails));
                updateUnsubscribeList();
                alert(`Added ${email} to unsubscribe list.`);
                document.getElementById('unsubscribeEmail').value = ''; // Clear input
            } else {
                alert('Email is already unsubscribed or empty.');
            }
        }

        // Function to delete all unsubscribed emails
        function deleteUnsubscribedEmails() {
            if (confirm('Are you sure you want to delete all unsubscribed emails?')) {
                unsubscribedEmails = [];
                localStorage.removeItem('unsubscribedEmails');
                updateUnsubscribeList();
                alert('All unsubscribed emails deleted.');
            }
        }

        // Function to update the unsubscribe list display
        function updateUnsubscribeList() {
            document.getElementById('unsubscribeList').value = unsubscribedEmails.join('\n');
        }

        // Initialize the unsubscribe list on page load
        updateUnsubscribeList();

        // Main function to process text and display in output
        function processText() {
            // Prevent re-processing if already in progress
            if (isProcessing) return;

            // Retrieve input text and prepare for output
            const inputText = document.getElementById('inputText').value;
            const paragraphs = inputText.split(/\n\s*\n/);
            const outputContainer = document.getElementById('output');
            outputContainer.innerHTML = '<p id="cursorStart">Place your cursor here</p>';

            // Function to process each paragraph with "To" prefix and check for unsubscribed emails
            paragraphs.forEach(paragraph => {
                if (paragraph.trim()) {
                    const lines = paragraph.split('\n');
                    let firstLine = lines[0].trim();
                    let lastName = firstLine.split(' ').pop();

                    // Prefix "Professor" if missing in first line
                    if (!firstLine.toLowerCase().startsWith('professor')) {
                        firstLine = `<span class="highlight-added">Professor</span> ${firstLine}`;
                        lines[0] = firstLine;
                    }

                    // Add "To" prefix to processed paragraph
                    const processedParagraph = "To\n" + lines.join('\n');
                    const greeting = `Dear Professor ${lastName},\n`;

                    // Prepare final text with greeting
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

                    // Display in output container
                    const p = document.createElement('p');
                    p.innerHTML = highlightedText;
                    outputContainer.appendChild(p);
                }
            });

            // Update counts and save state
            updateCounts();
            saveText();
        }

        // Function to check for errors in each paragraph
        function highlightErrors(text) {
            // Highlight ? symbols as errors
            let modifiedText = text.replace(/\?/g, '<span class="error">?</span>');

            // Highlight missing emails
            if (!text.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
                modifiedText += ' <span class="error">Missing email</span>';
            }
            return modifiedText;
        }

        // Function to save processed text and unsubscribe data to localStorage
        function saveText() {
            const outputText = document.getElementById('output').innerHTML;
            if (outputText) {
                localStorage.setItem('outputText', outputText);
                localStorage.setItem('unsubscribedEmails', JSON.stringify(unsubscribedEmails));
            }
        }

        // Function to clear all saved data from localStorage
        function clearMemory() {
            if (confirm("Are you sure you want to clear all saved data?")) {
                localStorage.clear();
                alert("All saved data has been cleared.");
            }
        }

        // Function to toggle visibility of an input box section
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
        
        // Call this function when the document loads
        document.addEventListener('DOMContentLoaded', () => {
            updateUnsubscribeList();
            if (Notification.permission !== 'granted') {
                Notification.requestPermission();
            }
        });
    </script>
</body>
</html>
