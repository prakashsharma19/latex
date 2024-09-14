<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Text Query Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
    }
    #left-side {
      width: 50%;
      padding: 20px;
    }
    #right-side {
      width: 50%;
      padding: 20px;
      background-color: #f4f4f4;
    }
    #query-box {
      width: 100%;
      height: 150px;
      margin-bottom: 20px;
    }
    #submit-btn {
      padding: 10px 20px;
      background-color: #007bff;
      color: white;
      border: none;
      cursor: pointer;
    }
    #results {
      margin-top: 20px;
    }
    .reference {
      margin-bottom: 10px;
    }
    .doi-link {
      color: #007bff;
      text-decoration: none;
    }
  </style>
</head>
<body>

  <!-- Left Side: Simple Text Query Tool -->
  <div id="left-side">
    <h1>Simple Text Query Tool</h1>
    
    <p>Paste your references below, and we will find the corresponding DOIs:</p>
    
    <textarea id="query-box" placeholder="Paste your references here..."></textarea><br>
    <button id="submit-btn">Find DOIs</button>
    
    <div id="results"></div>
  </div>

  <!-- Right Side: Existing functionality (e.g., PDF viewer or other) -->
  <div id="right-side">
    <h1>Existing Right-Side Feature</h1>
    <p>This is where your previous right-side functionality, such as PDF viewing or another feature, will remain intact.</p>
    <!-- Keep your original right-side functionality here. -->
  </div>

  <script>
    document.getElementById('submit-btn').addEventListener('click', function() {
      const queryBox = document.getElementById('query-box');
      const references = queryBox.value.split("\n").filter(line => line.trim() !== "");
      const resultsDiv = document.getElementById('results');
      resultsDiv.innerHTML = "<p>Searching for DOIs...</p>";
      resultsDiv.innerHTML = ''; // Clear the previous results
      
      references.forEach(reference => {
        // Perform a fetch for each reference using CrossRef API
        fetch(`https://api.crossref.org/works?query=${encodeURIComponent(reference)}`)
          .then(response => {
            if (!response.ok) {
              throw new Error('Network response was not ok');
            }
            return response.json();
          })
          .then(data => {
            if (data.message.items && data.message.items.length > 0) {
              const firstItem = data.message.items[0];
              const doi = firstItem.DOI;
              const title = firstItem.title ? firstItem.title[0] : "No Title Found";
              const doiLink = `https://doi.org/${doi}`;
              
              const referenceDiv = document.createElement('div');
              referenceDiv.classList.add('reference');
              referenceDiv.innerHTML = `<strong>${title}</strong><br><a href="${doiLink}" class="doi-link" target="_blank">${doiLink}</a>`;
              resultsDiv.appendChild(referenceDiv);
            } else {
              const referenceDiv = document.createElement('div');
              referenceDiv.classList.add('reference');
              referenceDiv.innerHTML = `<strong>No DOI found for:</strong> ${reference}`;
              resultsDiv.appendChild(referenceDiv);
            }
          })
          .catch(error => {
            console.error('Error fetching DOI:', error);
            const errorDiv = document.createElement('div');
            errorDiv.classList.add('reference');
            errorDiv.innerHTML = `<strong>Error finding DOI for:</strong> ${reference}`;
            resultsDiv.appendChild(errorDiv);
          });
      });
    });
  </script>

</body>
</html>
