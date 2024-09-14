<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DOI Citation Fixer</title>
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
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 10px;
    }
    .button-container a {
      display: inline-block;
      width: 60px;
      height: 30px;
      border-radius: 8px;
      background-color: #fff;
      border: 2px solid #ccc;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      transition: all 0.2s ease;
      overflow: hidden;
    }
    .button-container a img {
      width: 100%;
      height: auto;
    }
    .button-container a:hover {
      transform: translateY(-3px);
      background-color: #f9f9f9;
    }
    iframe {
      width: 100%;
      height: 600px;
      border: none;
      margin-top: 20px;
    }
    .loading {
      display: none;
      margin-top: 10px;
      font-size: 18px;
      color: #888;
    }
    h1 {
      text-align: center;
    }
    input[type="text"] {
      width: 75%;
      padding: 12px;
      font-size: 16px;
      border-radius: 5px;
      border: 1px solid #ccc;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }
    button {
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
    }
    input[type="file"] {
      padding: 8px;
      font-size: 16px;
      margin-top: 10px;
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
    textarea {
      width: 100%;
      height: 150px;
      margin-top: 20px;
      padding: 10px;
      font-size: 16px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    .save-btn {
      margin-top: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      padding: 8px 15px;
      cursor: pointer;
      border-radius: 5px;
      transition: transform 0.2s ease;
    }
    .save-btn:hover {
      transform: translateY(-3px);
    }
    h3 a {
      color: #333;
      text-decoration: none;
    }
    h3 a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <h1>DOI Citation Fixer</h1>

  <div class="container">
    <div class="left">
      <textarea id="citationInput" placeholder="Paste the citation here..."></textarea>
      <button class="save-btn" onclick="fixCitations()">Fix Citations</button>
      <textarea id="citationOutput" placeholder="Fixed citations with DOI will appear here..." readonly></textarea>
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
    // Helper function to extract DOI from a citation string
    function extractDOI(citation) {
      const doiPattern = /10\.\d{4,9}\/[-._;()/:A-Z0-9]+/i;
      return citation.match(doiPattern);
    }

    // Function to search CrossRef API for a DOI based on citation text
    async function fetchDOI(query) {
      const apiUrl = `https://api.crossref.org/works?query=${encodeURIComponent(query)}&rows=1`;
      const response = await fetch(apiUrl);
      const data = await response.json();

      if (data.message && data.message.items && data.message.items.length > 0) {
        return data.message.items[0].DOI;
      }
      return null;
    }

    // Function to fix citations by adding DOI links
    async function fixCitations() {
      const input = document.getElementById('citationInput').value.trim();
      if (!input) {
        alert('Please enter at least one citation');
        return;
      }

      const citations = input.split('\n');
      let fixedCitations = '';

      for (let citation of citations) {
        let doi = extractDOI(citation);

        if (!doi) {
          doi = await fetchDOI(citation);
        }

        if (doi) {
          citation += ` https://doi.org/${doi}`;
        }

        fixedCitations += citation + '\n';
      }

      document.getElementById('citationOutput').value = fixedCitations.trim();
    }

    // Existing right-side search functionality (unchanged)
    function searchAuthor() {
      const query = document.getElementById('searchQuery').value;
      if (!query) {
        alert('Please enter a search query');
        return;
      }

      document.getElementById('loading').style.display = 'block';

      const sanitizedQuery = query.replace(/[.,]/g, '').split(' ').join('+');
      const crossRefUrl = `https://api.crossref.org/works?query=${encodeURIComponent(sanitizedQuery)}&rows=5`;

      fetch(crossRefUrl)
        .then(response => response.json())
        .then(data => {
          document.getElementById('loading').style.display = 'none';
          const resultsContainer = document.getElementById('results');
          resultsContainer.innerHTML = '';

          const works = data.message.items || [];
          if (works.length > 0) {
            works.forEach(work => {
              const title = work.title ? work.title[0] : 'Untitled';
              const doiLink = work.DOI || null;

              const resultItem = `
                <div class="result-item">
                  <h3><a href="https://doi.org/${doiLink}" target="_blank">${title}</a></h3>
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
          document.getElementById('loading').style.display = 'none';
        });
    }
  </script>
</body>
</html>
