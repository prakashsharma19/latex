<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Web Scraping Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    h1 {
      color: #333;
    }
    input {
      width: 100%;
      padding: 10px;
      font-size: 16px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-top: 10px;
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #45a049;
    }
    #results {
      margin-top: 20px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px;
    }
    th {
      background-color: #f2f2f2;
      text-align: left;
    }
  </style>
</head>
<body>
  <h1>Web Scraping Tool</h1>
  <p>Enter the URL of a website to extract email addresses:</p>
  <input type="text" id="urlInput" placeholder="Enter website URL here (e.g., https://example.com)" />
  <button onclick="scrapeData()">Scrape</button>

  <div id="results">
    <h2>Extracted Data</h2>
    <table id="dataTable">
      <thead>
        <tr>
          <th>Name</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
      </tbody>
    </table>
  </div>

  <script>
    async function scrapeData() {
      const url = document.getElementById('urlInput').value;
      if (!url) {
        alert('Please enter a valid URL.');
        return;
      }

      try {
        // Fetch the HTML content from the website
        const response = await fetch(`https://api.allorigins.win/get?url=${encodeURIComponent(url)}`);
        const data = await response.json();

        // Parse the HTML response
        const parser = new DOMParser();
        const doc = parser.parseFromString(data.contents, 'text/html');

        // Extract email addresses
        const rows = [];
        doc.querySelectorAll('a[href^="mailto:"]').forEach((emailLink) => {
          const email = emailLink.getAttribute('href').replace('mailto:', '');
          const name = emailLink.textContent.trim() || 'N/A';
          rows.push({ name, email });
        });

        // Display the results in the table
        const tableBody = document.querySelector('#dataTable tbody');
        tableBody.innerHTML = ''; // Clear any previous results
        rows.forEach(({ name, email }) => {
          const row = `<tr><td>${name}</td><td>${email}</td></tr>`;
          tableBody.innerHTML += row;
        });

        if (rows.length === 0) {
          alert('No emails found on this page.');
        }
      } catch (error) {
        console.error('Error scraping data:', error);
        alert('Failed to fetch data. Please try a different URL.');
      }
    }
  </script>
</body>
</html>
