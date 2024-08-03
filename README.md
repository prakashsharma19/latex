<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Link Extractor Tool</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f4f4f4;
        }
        textarea, #output {
            width: 100%;
            box-sizing: border-box;
            padding: 10px;
            margin-bottom: 20px;
        }
        textarea {
            height: 150px;
            font-size: 14px;
        }
        #output {
            background-color: #fff;
            border: 1px solid #ccc;
            padding: 20px;
            font-size: 16px;
        }
        button {
            padding: 10px 20px;
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        a {
            color: #007bff;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <h1>Link Extractor Tool</h1>
    <p>Paste your webpage content below and click "Extract Links" to display only the text with URLs.</p>
    
    <textarea id="input" placeholder="Paste your webpage content here..."></textarea>
    <button onclick="extractLinks()">Extract Links</button>

    <div id="output"></div>

    <script>
        function extractLinks() {
            const input = document.getElementById('input').value;
            const parser = new DOMParser();
            const doc = parser.parseFromString(input, 'text/html');
            const links = doc.querySelectorAll('a');
            const outputDiv = document.getElementById('output');

            outputDiv.innerHTML = '';

            links.forEach(link => {
                const linkText = link.innerText.trim();
                const linkHref = link.href;

                if (linkText) {
                    const listItem = document.createElement('p');
                    listItem.innerHTML = `<a href="${linkHref}" target="_blank">${linkText}</a>`;
                    outputDiv.appendChild(listItem);
                }
            });

            if (!outputDiv.innerHTML) {
                outputDiv.innerHTML = '<p>No links found.</p>';
            }
        }
    </script>

</body>
</html>
