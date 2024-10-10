<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Author Details Formatter</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f9f9f9;
        }
        h2 {
            color: #333;
        }
        textarea {
            width: 100%;
            height: 200px;
            margin-bottom: 20px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
            resize: none;
        }
        .button {
            display: inline-block;
            padding: 10px 20px;
            background-color: #007BFF;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        .button:hover {
            background-color: #0056b3;
        }
        .output {
            border: 1px solid #ccc;
            padding: 10px;
            white-space: pre-wrap;
            background-color: #fff;
            border-radius: 4px;
        }
    </style>
</head>
<body>

<h2>Author Details Formatter</h2>

<textarea id="inputText" placeholder="Paste author details here..."></textarea>
<button class="button" onclick="formatDetails()">Format</button>

<h3>Formatted Output:</h3>
<div class="output" id="outputText"></div>

<script>
    function formatDetails() {
        // Get the input text
        let inputText = document.getElementById("inputText").value;

        // Split the text into lines
        let lines = inputText.split('\n').map(line => line.trim());

        let formattedText = '';
        for (let i = 0; i < lines.length; i++) {
            let line = lines[i];

            if (line.includes("Department")) {
                formattedText += line + '\n'; // Department in one line
            } else if (line.includes("University")) {
                formattedText += line + '\n'; // University in one line
            } else if (line.includes("Laboratory")) {
                formattedText += line + '\n'; // Laboratory in one line
            } else if (line.includes(",")) {
                // If it's an address, split it into one line
                let parts = line.split(',');
                formattedText += parts[0].trim() + '\n' + parts[1].trim() + '\n';
            } else if (line.includes("USA")) {
                formattedText += "USA\n"; // Put USA in one line before email
            } else {
                formattedText += line + '\n'; // Keep other lines as is
            }
        }

        // Set the formatted text in the output div
        document.getElementById("outputText").innerText = formattedText;
    }
</script>

</body>
</html>
