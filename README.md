<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Equation to LaTeX Converter</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        textarea {
            width: 100%;
            margin-top: 10px;
            margin-bottom: 10px;
        }
        #output {
            border: 1px solid #ddd;
            padding: 10px;
            margin-top: 10px;
        }
    </style>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
    <script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
</head>
<body>
    <h1>Microsoft Equation to LaTeX Converter</h1>
    <textarea id="equationInput" rows="10" placeholder="Paste your equation here..."></textarea>
    <br>
    <button onclick="convertToLatex()">Convert to LaTeX</button>
    <h2>LaTeX Code:</h2>
    <textarea id="latexOutput" rows="5" readonly></textarea>
    <h2>Rendered Output:</h2>
    <div id="output"></div>

    <script>
        function convertToLatex() {
            const input = document.getElementById('equationInput').value;
            const latexCode = parseAndConvert(input);
            document.getElementById('latexOutput').value = latexCode;
            renderLatex(latexCode);
        }

        function parseAndConvert(input) {
            // Placeholder for actual conversion logic
            // For demonstration, let's assume the input is already in a simple format
            // Add your actual conversion logic here
            return input;  // For now, simply returning the input as LaTeX code
        }

        function renderLatex(latexCode) {
            document.getElementById('output').innerHTML = `$$${latexCode}$$`;
            MathJax.typeset();
        }
    </script>
</body>
</html>
