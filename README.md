<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="CACHE-CONTROL" content="NO-CACHE" />
    <meta http-equiv="PRAGMA" content="NO-CACHE" />
    <meta http-equiv="EXPIRES" content="-1" />
    <meta name="ROBOTS" content="NONE" />
    <title>Reference DOI Finder</title>
    <link type="text/css" href="styles.css" rel="stylesheet" />
    <script type="text/javascript" src="scripts.js"></script>
</head>

<body style="text-align: center; margin: 0px;">
    <header style="background-color: #ffc72c; padding: 10px;">
        <h1>Reference DOI Finder</h1>
    </header>

    <div style="padding: 20px;">
        <form enctype="application/x-www-form-urlencoded" method="POST" name="freeTextQuery" accept-charset="UTF-8">
            <div>
                <label for="freetext">Enter text in the box below:</label><br>
                <textarea rows="10" cols="100" title="Paste your reference section here" class="input" id="freetext" name="freetext" maxlength="10000000" wrap="off"></textarea>
            </div>
            <div>
                <input type="checkbox" name="includePM" /> Include PubMed IDs in results.<br>
                <input type="checkbox" name="multihit" /> List all possible DOIs per reference.
            </div>
            <div>
                <input class="mybutton" type="submit" name="submitButton" value="Submit" onclick="setAction('submit');" />
            </div>
            <p>We now provide space to match 1,000 references per submission.</p>
        </form>
    </div>

    <footer style="background-color: #ffc72c; padding: 10px;">
        <p>Contact us if you have any questions.</p>
    </footer>
</body>

</html>
