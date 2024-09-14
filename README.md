<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Text Query Tool</title>
  <style>
    body {
      font-family: 'Helvetica Neue', Arial, sans-serif;
      margin: 20px;
      background-color: #f0f2f5;
      color: #333;
    }
    .container {
      display: flex;
    }
    .left {
      flex: 2;
      padding-right: 20px;
    }
    .right {
      flex: 1;
      padding-left: 20px;
      border-left: 2px solid #ccc;
    }
    .search-container {
      display: flex;
      align-items: center;
      margin-bottom: 20px;
      padding: 10px;
      background-color: #ffffff;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      border-radius: 8px;
    }
    .results {
      margin-top: 20px;
    }
    .result-item {
      border: 1px solid #ddd;
      padding: 20px;
      margin-bottom: 15px;
      border-radius: 8px;
      background-color: #ffffff;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
    textarea {
      width: 100%;
      height: 150px;
      margin-top: 20px;
      padding: 10px;
      font-size: 16px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
    }
    button.search-btn {
      background-color: #4CAF50;
      color: white;
      border: none;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 5px;
      margin-left: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      transition: transform 0.2s ease;
    }
    button.search-btn:hover {
      transform: translateY(-3px);
    }
    .loading {
      display: none;
      margin-top: 10px;
      font-size: 18px;
      color: #888;
    }
  </style>
</head>
<body>
  <h1>Simple Text Query Tool</h1>

  <div class="container">
    <div class="left">
      <textarea id="referenceBox" placeholder="Paste your references here..."></textarea>
      <button class="search-btn" onclick="submitReferences()">Find DOIs</button>
    </div>

    <div class="right">
      <div class="search-container">
        <input type="text" id="searchQuery" placeholder="Enter Article Details">
        <button class="search-btn" onclick="searchAuthor()">Search</button>
      </div>
      <p class="loading" id="loading">Loading...</p>
      <div class="results" id="results"></div>
    </div>
  </div>

  <script>
    function submitReferences() {
      const references = document.getElementById('referenceBox').value.trim();
      if (!references) {
        alert('Please paste your references.');
        return;
      }

      const referencesArray = references.split('\n');
      const resultsContainer = document.getElementById('results');
      resultsContainer.innerHTML = '';
      document.getElementById('loading').style.display = 'block';

      referencesArray.forEach(ref => {
        if (ref.trim()) {
          searchForDOI(ref.trim());
        }
      });

      document.getElementById('loading').style.display = 'none';
    }

    function searchForDOI(reference) {
      const sanitizedReference = reference.replace(/[.,]/g, '').split(' ').join('+');
      const crossRefUrl = `https://api.crossref.org/works?query.bibliographic=${encodeURIComponent(sanitizedReference)}&rows=1`;

      fetch(crossRefUrl)
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          const resultsContainer = document.getElementById('results');
          const works = data.message.items || [];

          if (works.length > 0) {
            const work = works[0];
            const title = work.title ? work.title[0] : 'Untitled';
            const doiLink = work.DOI ? `<a href="https://doi.org/${work.DOI}" target="_blank">${work.DOI}</a>` : 'DOI not found';

            const resultItem = `
              <div class="result-item">
                <h3>${title}</h3>
                <p>${doiLink}</p>
              </div>
            `;
            resultsContainer.innerHTML += resultItem;
          } else {
            resultsContainer.innerHTML += `<div class="result-item"><p>No DOI found for: ${reference}</p></div>`;
          }
        })
        .catch(error => {
          console.error('Error fetching data:', error);
          alert('An error occurred while fetching data.');
        });
    }

    function searchAuthor() {
      const query = document.getElementById('searchQuery').value;
      if (!query) {
        alert('Please enter a search query');
        return;
      }

      const crossRefUrl = `https://api.crossref.org/works?query=${encodeURIComponent(query)}&rows=5`;

      fetch(crossRefUrl)
        .then(response => {
          if (!response.ok) {
            throw new Error('Network response was not ok');
          }
          return response.json();
        })
        .then(data => {
          const resultsContainer = document.getElementById('results');
          resultsContainer.innerHTML = '';

          const works = data.message.items || [];

          if (works.length > 0) {
            works.forEach(work => {
              const title = work.title ? work.title[0] : 'Untitled';
              const doiLink = work.DOI ? `<a href="https://doi.org/${work.DOI}" target="_blank">${work.DOI}</a>` : 'DOI not found';

              const resultItem = `
                <div class="result-item">
                  <h3>${title}</h3>
                  <p>${doiLink}</p>
                </div>
              `;
              resultsContainer.innerHTML += resultItem;
            });
          } else {
            resultsContainer.innerHTML = `<p>No results found.</p>`;
          }
        })
        .catch(error => {
          console.error('Error fetching data:', error);
          alert('An error occurred while fetching data.');
        });
    }
  </script>
</body>
</html>
