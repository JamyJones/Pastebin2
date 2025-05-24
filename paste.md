Let's solve this with a more efficient approach than reloading the entire page. Here's a professional solution that uses modern web practices:

```javascript
class StreamCard {
    constructor(streamData) {
        this.streamId = streamData.id;
        this.startTime = new Date(streamData.startTime);
        this.gifUrl = streamData.gifUrl;
        this.element = null;
    }

    createCard() {
        this.element = document.createElement('div');
        this.element.className = 'stream-card';
        this.element.id = `card-${this.streamId}`;
        
        this.element.innerHTML = `
            <img src="${this.gifUrl}" alt="Stream GIF" class="stream-gif">
            <div class="progress-container">
                <div class="progress-bar" id="progress-${this.streamId}"></div>
            </div>
            <div class="stream-duration" id="duration-${this.streamId}"></div>
        `;

        return this.element;
    }

    updateProgress() {
        const progressBar = document.getElementById(`progress-${this.streamId}`);
        const durationElement = document.getElementById(`duration-${this.streamId}`);
        const duration = Math.floor((new Date() - this.startTime) / 1000);
        
        progressBar.style.width = `${(duration % 600) / 6}%`; // 600 seconds = 10 minutes
        durationElement.textContent = this.formatDuration(duration);
    }

    formatDuration(seconds) {
        const hours = Math.floor(seconds / 3600);
        const minutes = Math.floor((seconds % 3600) / 60);
        const secs = seconds % 60;
        return `${hours}:${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
    }

    updateGif(newGifUrl) {
        const imgElement = this.element.querySelector('.stream-gif');
        imgElement.src = newGifUrl;
    }
}

class StreamManager {
    constructor() {
        this.streams = new Map();
        this.container = document.getElementById('streams-container');
    }

    async fetchUpdates() {
        try {
            const response = await fetch('/api/streams');
            const streams = await response.json();
            
            this.updateStreams(streams);
        } catch (error) {
            console.error('Failed to fetch stream updates:', error);
        }
    }

    updateStreams(streamData) {
        // Handle new streams
        streamData.forEach(data => {
            if (!this.streams.has(data.id)) {
                const streamCard = new StreamCard(data);
                this.streams.set(data.id, streamCard);
                this.container.appendChild(streamCard.createCard());
            } else {
                // Update existing stream
                const streamCard = this.streams.get(data.id);
                if (data.gifUrl !== streamCard.gifUrl) {
                    streamCard.updateGif(data.gifUrl);
                }
            }
        });

        // Remove ended streams
        const currentIds = new Set(streamData.map(s => s.id));
        [...this.streams.keys()].forEach(id => {
            if (!currentIds.has(id)) {
                const element = document.getElementById(`card-${id}`);
                element?.remove();
                this.streams.delete(id);
            }
        });
    }

    startUpdates() {
        // Update progress bars every second
        setInterval(() => {
            this.streams.forEach(stream => stream.updateProgress());
        }, 1000);

        // Fetch new GIFs every 10 minutes
        setInterval(() => {
            this.fetchUpdates();
        }, 600000); // 10 minutes
    }
}

// Initialize
const manager = new StreamManager();
manager.fetchUpdates();
manager.startUpdates();
```

This solution addresses several key points:

1. **Avoid Page Reloads**: Instead of reloading the entire page, we update only the necessary components.

2. **Race Condition Prevention**: 
   - Using a `Map` to track streams
   - Atomic updates for each stream card
   - Clear separation between progress updates and content updates

3. **Performance Optimization**:
   - DOM manipulation is minimized
   - Progress bars update independently
   - GIF updates happen only when new content is available

4. **Memory Management**:
   - Proper cleanup of ended streams
   - Event listener management
   - Clear object references

To complement this, add this CSS for smooth transitions:

```css
.stream-card {
    margin: 10px;
    padding: 15px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.stream-gif {
    width: 100%;
    height: auto;
    transition: opacity 0.3s ease;
}

.progress-container {
    height: 4px;
    background: #eee;
    margin-top: 10px;
}

.progress-bar {
    height: 100%;
    background: #2196F3;
    transition: width 0.3s linear;
}
```

For the backend API endpoint, ensure you're sending properly structured data:

```javascript
// Example API response structure
{
    streams: [
        {
            id: "stream1",
            startTime: "2023-05-24T08:00:00Z",
            gifUrl: "path/to/gif.gif"
        },
        // ... more streams
    ]
}
```

This solution provides better scalability and maintainability while avoiding race conditions. The modular class structure makes it easier to add features or modify behavior in the future.