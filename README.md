function processText() {
    if (isProcessing) return;

    isProcessing = true;
    document.getElementById('loadingIndicator').style.display = 'inline';

    const inputText = document.getElementById('inputText').value;
    const paragraphs = inputText.split(/\n\s*\n/);
    totalParagraphs = paragraphs.length;
    const outputContainer = document.getElementById('output');
    const incompleteContainer = document.getElementById('incompleteText');
    outputContainer.innerHTML = '<p id="cursorStart">Place your cursor here</p>';
    incompleteContainer.value = '';

    let index = 0;
    const nonRussiaEntries = [];
    const russiaEntries = [];

    const gapOption = document.getElementById('gapOption').value;

    function processChunk() {
        const chunkSize = 10;
        const end = Math.min(index + chunkSize, paragraphs.length);
        for (; index < end; index++) {
            let paragraph = paragraphs[index].trim();
            if (paragraph !== '') {
                const lines = paragraph.split('\n');
                let firstLine = lines[0].trim();
                let lastName = firstLine.split(' ').pop();

                // Check if the toggle is ON and add "Dear Professor" after the email
                if (includeDearProfessor) {
                    const emailRegex = /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/;
                    const emailLineIndex = lines.findIndex(line => emailRegex.test(line));
                    if (emailLineIndex !== -1) {
                        const greeting = `Dear Professor ${lastName},`;
                        if (gapOption === 'nil') {
                            lines.splice(emailLineIndex + 1, 0, greeting); // Insert with no gap
                        } else {
                            lines.splice(emailLineIndex + 1, 0, '', greeting); // Insert with gap
                        }
                    }
                }

                let processedParagraph = lines.join('\n');
                const highlightedText = highlightErrors(processedParagraph.replace(/\n/g, '<br>'));
                const hasError = highlightedText.includes('error');

                if (hasError) {
                    incompleteContainer.value += `${highlightedText.replace(/<br>/g, '\n').replace(/<[^>]+>/g, '')}\n\n`;
                } else {
                    const p = document.createElement('p');
                    p.innerHTML = highlightedText;

                    if (paragraph.includes('Russia')) {
                        russiaEntries.push(p);
                    } else {
                        nonRussiaEntries.push(p);
                    }
                }
            }
        }
        if (index < paragraphs.length) {
            requestAnimationFrame(processChunk);
        } else {
            nonRussiaEntries.forEach(entry => outputContainer.appendChild(entry));
            russiaEntries.forEach(entry => outputContainer.appendChild(entry));

            updateCounts();
            saveText();
            document.getElementById('lockButton').style.display = 'inline-block';
            document.getElementById('loadingIndicator').style.display = 'none';
            isProcessing = false;
        }
    }
    requestAnimationFrame(processChunk);
}
