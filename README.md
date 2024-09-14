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
      width: 30px;
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
    .output {
      margin-top: 20px;
      font-size: 16px;
      line-height: 1.6;
    }
    a.doi-link {
      color: #4CAF50;
      text-decoration: none;
    }
    a.doi-link:hover {
      text-decoration: underline;
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
      <div id="citationOutput" class="output"></div>
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

    // Function to search CrossRef API for a DOI based on citation text with exact title and author match
    async function fetchDOI(query, title, authors) {
      const apiUrl = `https://api.crossref.org/works?query=${encodeURIComponent(query)}&rows=5`;
      const response = await fetch(apiUrl);
      const data = await response.json();

      if (data.message && data.message.items) {
        for (let item of data.message.items) {
          const itemTitle = item.title ? item.title[0].toLowerCase() : '';
          const itemAuthors = item.author ? item.author.map(a => `${a.given} ${a.family}`.toLowerCase()).join(', ') : '';

          // Check if both title and authors match exactly
          if (itemTitle === title.toLowerCase() && itemAuthors === authors.toLowerCase()) {
            return item.DOI;
          }
        }
      }
      return null;
    }

    // Function to fix citations by adding DOI links (only on exact matches)
    async function fixCitations() {
      const input = document.getElementById('citationInput').value.trim();
      const outputDiv = document.getElementById('citationOutput');
      if (!input) {
        alert('Please enter at least one citation');
        return;
      }

      const citations = input.split('\n');
      let fixedCitations = '';

      for (let citation of citations) {
        let doi = extractDOI(citation);

        if (!doi) {
          // Extract title and authors from the citation manually (requires proper format, can be improved)
          const titleMatch = citation.match(/, (.*?)\. /);
          const authorsMatch = citation.match(/^(.*?)\,/);

          if (titleMatch && authorsMatch) {
            const title = titleMatch[1];
            const authors = authorsMatch[1];
            doi = await fetchDOI(citation, title, authors);
          }
        }

        if (doi) {
          citation += ` <a href="https://doi.org/${doi}" class="doi-link" target="_blank">https://doi.org/${doi}</a>`;
        }

        fixedCitations += `<p>${citation}</p>`;
      }

      outputDiv.innerHTML = fixedCitations || 'No citations found.';
    }

    // Right-side functionality (unchanged, fixed to show the icons properly)
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
              const authors = work.author || [];
              const doiLink = work.DOI || null;

              const authorNames = authors.map(author => `${author.given} ${author.family}`).join(', ');

              const authorSearchQuery = encodeURIComponent(authorNames);
              const authorLinks = authors.map(author => 
                `<a href="https://scholar.google.com/scholar?q=${authorSearchQuery}" target="_blank">${author.given} ${author.family}</a>`
              ).join(', ');

              let doiButton = '';
              let scholarButton = '';
              let arxivButton = '';
              let pdfButton = '';

              if (doiLink) {
                doiButton = `<a href="https://doi.org/${doiLink}" target="_blank"><img src="https://raw.githubusercontent.com/prakashsharma19/Referee/main/Doi-removebg-preview.png" alt="DOI"></a>`;
              }

              scholarButton = `<a href="https://scholar.google.com/scholar?q=${encodeURIComponent(title)}" target="_blank"><img src="https://raw.githubusercontent.com/prakashsharma19/Referee/main/Google_scholar-removebg-preview.png" alt="Google Scholar"></a>`;
              arxivButton = `<a href="https://arxiv.org/search/?query=${encodeURIComponent(title)}&searchtype=all" target="_blank"><img src="https://raw.githubusercontent.com/prakashsharma19/Referee/main/ArXiv%20image.png" alt="ArXiv"></a>`;

              if (work['link'] && work['link'].some(link => link['content-type'] === 'application/pdf')) {
                const pdfLink = work['link'].find(link => link['content-type'] === 'application/pdf').URL;
                pdfButton = `<a href="${pdfLink}" target="_blank"><img src="https://raw.githubusercontent.com/prakashsharma19/Referee/main/PDf.jpg" alt="PDF"></a>`;
              }

              const resultItem = `
                <div class="result-item">
                  <h3><a href="https://www.google.com/search?q=${encodeURIComponent(title)}" target="_blank">${title}</a></h3>
                  <p class="author-line">by: ${authorLinks}</p>
                  <div class="button-container">
                    ${doiButton}
                    ${scholarButton}
                    ${arxivButton}
                    ${pdfButton}
                  </div>
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
