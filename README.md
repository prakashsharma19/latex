<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Author Details Sorter</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
            max-width: 600px;
            margin: auto;
        }
        textarea {
            width: 100%;
            height: 200px;
        }
        button {
            margin-top: 10px;
        }
        .result {
            margin-top: 20px;
        }
    </style>
</head>
<body>

    <h1>Author Details Sorter</h1>
    <textarea id="authorInput" placeholder="Enter author details here..."></textarea>
    <button id="sortButton">Sort Authors</button>

    <div class="result" id="result"></div>

    <script>
        document.getElementById('sortButton').addEventListener('click', function() {
            const inputText = document.getElementById('authorInput').value.trim();
            const authorDetails = parseInput(inputText);
            const sortedAuthors = sortAuthorDetails(authorDetails);
            displayResults(sortedAuthors);
        });

        function parseInput(inputText) {
            const authorBlocks = inputText.split('\n\n').filter(block => block.trim() !== '');
            return authorBlocks.map(block => ({
                info: block
            }));
        }

        function sortAuthorDetails(authors) {
            const sortedAuthors = authors.map(author => {
                const lines = author.info.split('\n');

                // Extract relevant information
                const name = lines[1] ? lines[1].trim() : '';  // Assuming the second line contains the name
                const departmentUniversity = lines[2] ? lines[2].trim() : '';  // Department/University info
                const address = lines[3] ? lines[3].trim() : '';  // Address
                const country = lines[4] ? lines[4].trim() : '';  // Country (assuming it's on the next line)
                const email = lines[lines.length - 1].trim();  // Email (assuming it's the last line)

                return {
                    name,
                    departmentUniversity,
                    address,
                    country,
                    email
                };
            });

            // Sort authors by name
            sortedAuthors.sort((a, b) => a.name.localeCompare(b.name));

            return sortedAuthors;
        }

        function displayResults(authors) {
            const resultDiv = document.getElementById('result');
            resultDiv.innerHTML = ''; // Clear previous results

            authors.forEach(author => {
                const authorInfo = `
                    <div>
                        <strong>Name:</strong> ${author.name}<br>
                        <strong>Department/University:</strong> ${author.departmentUniversity}<br>
                        <strong>Address:</strong> ${author.address}<br>
                        <strong>Country:</strong> ${author.country}<br>
                        <strong>Email:</strong> ${author.email}<br>
                        <hr>
                    </div>
                `;
                resultDiv.innerHTML += authorInfo;
            });
        }
    </script>

</body>
</html>
