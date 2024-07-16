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
    </style>
</head>
<body>
    <h1>Microsoft Equation 3.0 to LaTeX Converter</h1>
    <textarea id="equationInput" rows="10" placeholder="Paste your equation here..."></textarea>
    <br>
    <button onclick="convertToLatex()">Convert to LaTeX</button>
    <h2>LaTeX Code:</h2>
    <textarea id="latexOutput" rows="10" readonly></textarea>

    <script>
        function convertToLatex() {
            const input = document.getElementById('equationInput').value;
            const latexCode = parseAndConvert(input);
            document.getElementById('latexOutput').value = latexCode;
        }

        function parseAndConvert(input) {
            // This is a placeholder function for the conversion logic.
            // Add your own parsing logic here to handle the Microsoft Equation 3.0 format.
            // For demonstration purposes, let's assume simple replacements.
            let latex = input;

            // Example replacements for demonstration
            latex = latex.replace(/frac/g, '\\frac'); // Example: convert 'frac' to '\frac'
            latex = latex.replace(/sqrt/g, '\\sqrt'); // Example: convert 'sqrt' to '\sqrt'
            latex = latex.replace(/sum/g, '\\sum');   // Example: convert 'sum' to '\sum'

            // Add more replacement rules as needed
            // Return the converted LaTeX code
            return latex;
        }
    </script>
</body>
</html>
