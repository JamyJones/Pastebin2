It sounds like you have a great project going on! To avoid using `window.location.reload()` and to handle updates more efficiently, you can implement a more dynamic approach using JavaScript. Here are some suggestions to improve your app:

### 1. Use AJAX or Fetch API
Instead of reloading the entire page, you can use AJAX or the Fetch API to fetch new GIFs and update the cards dynamically. This way, you can update only the parts of the page that need to change.

### Example using Fetch API:
```javascript
function updateGifs() {
    fetch('/path/to/your/api/for/gifs')
        .then(response => response.json())
        .then(data => {
            data.forEach((gif, index) => {
                const card = document.getElementById(`card-${index}`);
                const img = card.querySelector('img');
                img.src = gif.url; // Update the GIF source
                // Update progress bar
                const progressBar = card.querySelector('.progress-bar');
                progressBar.style.width = `${gif.progress}%`; // Update progress
            });
        })
        .catch(error => console.error('Error fetching GIFs:', error));
}

// Call updateGifs every 10 seconds
setInterval(updateGifs, 10000);
```

### 2. Use WebSockets
If you want real-time updates without polling, consider using WebSockets. This allows your server to push updates to the client whenever new GIFs are available.

### 3. Manage State with JavaScript
Instead of relying on the DOM to manage the state of your cards, maintain a JavaScript object that holds the state of each card. This can help you avoid race conditions.

### Example State Management:
```javascript
let cardsState = {};

function updateCardState(index, gifUrl, progress) {
    cardsState[index] = { gifUrl, progress };
    renderCard(index);
}

function renderCard(index) {
    const card = document.getElementById(`card-${index}`);
    const img = card.querySelector('img');
    const progressBar = card.querySelector('.progress-bar');

    img.src = cardsState[index].gifUrl;
    progressBar.style.width = `${cardsState[index].progress}%`;
}

// Call this function to update the state and render
function updateGifs() {
    fetch('/path/to/your/api/for/gifs')
        .then(response => response.json())
        .then(data => {
            data.forEach((gif, index) => {
                updateCardState(index, gif.url, gif.progress);
            });
        })
        .catch(error => console.error('Error fetching GIFs:', error));
}
```

### 4. Use a Timer for Progress Bars
Instead of updating the progress bar every second in a race condition, you can set a timer for each card that updates its progress independently.

### Example Timer for Progress Bar:
```javascript
function startProgressBar(index, duration) {
    let progress = 0;
    const interval = setInterval(() => {
        if (progress < 100) {
            progress++;
            updateCardState(index, cardsState[index].gifUrl, progress);
        } else {
            clearInterval(interval);
        }
    }, duration / 100); // Adjust the duration as needed
}
```

### Conclusion
By using AJAX or WebSockets, managing state with JavaScript, and handling progress bars with independent timers, you can create a more efficient and responsive web app without the need for full page reloads. This will also help you avoid race conditions and improve the user experience.