<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Reference DOI Finder</title>
    <style>
        body {
            text-align: center;
            margin: 0px;
            font-family: Arial, sans-serif;
        }

        header {
            background-color: #ffc72c;
            padding: 10px;
        }

        .container {
            padding: 20px;
        }

        .mybutton {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            font-size: 16px;
        }

        .mybutton:hover {
            background-color: #45a049;
        }

        #results {
            padding: 20px;
            text-align: left;
            border: 1px solid #ccc;
            margin-top: 20px;
            white-space: pre-wrap; /* Preserves whitespace formatting */
        }
    </style>
</head>

<body>
    <header>
        <h1>Reference DOI Finder</h1>
    </header>

    <div class="container">
        <form id="referenceForm">
            <div>
                <label for="freetext">Enter text in the box below:</label><br>
                <textarea rows="10" cols="100" title="Paste your reference section here" id="freetext" name="freetext" maxlength="10000000" wrap="off"></textarea>
            </div>
            <div>
                <input type="checkbox" id="includePM" name="includePM"> Include PubMed IDs in results.<br>
                <input type="checkbox" id="multihit" name="multihit"> List all possible DOIs per reference.
            </div>
            <div>
                <button class="mybutton" type="submit">Submit</button>
            </div>
        </form>
        <div id="results"></div>
    </div>

    <script>
        document.getElementById('referenceForm').addEventListener('submit', function(event) {
            event.preventDefault();

            const freetext = document.getElementById('freetext').value;
            const includePM = document.getElementById('includePM').checked ? 'true' : 'false';
            const multihit = document.getElementById('multihit').checked ? 'true' : 'false';

            const formData = new URLSearchParams();
            formData.append('freetext', freetext);
            formData.append('includePM', includePM);
            formData.append('multihit', multihit);

            fetch('https://doi.crossref.org/simpleTextQuery', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                },
                body: formData.toString()
            })
            .then(response => response.text())
            .then(data => {
                document.getElementById('results').textContent = data;
            })
            .catch(error => {
                console.error('Error:', error);
                document.getElementById('results').textContent = 'An error occurred: ' + error;
            });
        });
    </script>
</body>

</html>
