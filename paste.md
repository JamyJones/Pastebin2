Creating dynamic cards in JavaScript where content updates periodically is a common task. To manage this effectively and avoid race conditions, especially when each card contains timers, you need to follow structured practices such as:

- Encapsulating each card’s logic inside a class or closure.
- Managing timers with proper cleanup to prevent overlaps.
- Using `setInterval` or `setTimeout` for periodic updates.
- Ensuring updates do not interfere with each other (race conditions).

### Step-by-step approach:

1. **Create a Card class/component** that manages its own DOM element and timers.
2. **Set up periodic updates** using `setInterval`.
3. **Clear existing timers** before starting new ones to avoid overlaps.
4. **Update the content inside each card safely**.

---

### Example implementation:

```html
<div id="cards-container"></div>
```

```javascript
class Card {
  constructor(container, id) {
    this.id = id;
    this.container = container;
    this.element = document.createElement('div');
    this.element.className = 'card';
    this.timers = []; // store timer IDs
    this.data = {
      count: 0,
      time: new Date()
    };

    this.render();
    this.startUpdates();
  }

  render() {
    this.element.innerHTML = `
      <h3>Card ${this.id}</h3>
      <p>Count: <span class="count">${this.data.count}</span></p>
      <p>Time: <span class="time">${this.data.time.toLocaleTimeString()}</span></p>
    `;
    this.container.appendChild(this.element);
  }

  startUpdates() {
    // Update count every second
    this.clearTimers();

    const countTimer = setInterval(() => {
      this.updateCount();
    }, 1000);

    // Update timestamp every second
    const timeTimer = setInterval(() => {
      this.updateTime();
    }, 1000);

    this.timers.push(countTimer, timeTimer);
  }

  updateCount() {
    this.data.count += 1;
    this.element.querySelector('.count').textContent = this.data.count;
  }

  updateTime() {
    this.data.time = new Date();
    this.element.querySelector('.time').textContent = this.data.time.toLocaleTimeString();
  }

  clearTimers() {
    this.timers.forEach(timer => clearInterval(timer));
    this.timers = [];
  }

  destroy() {
    this.clearTimers();
    this.container.removeChild(this.element);
  }
}

// Create multiple cards
const container = document.getElementById('cards-container');
const cards = [];

for (let i = 1; i <= 3; i++) {
  const card = new Card(container, i);
  cards.push(card);
}
```

---

### Key Points:

- **Encapsulation:** Each `Card` manages its own timers to avoid race conditions.
- **Cleanup:** `clearTimers()` ensures only one active timer per task.
- **Interval management:** Multiple `setInterval`s are used for different parts, but always cleaned up before starting new updates.

---

### Handling Race Conditions:
- Since each card manages its own timers, updates are isolated.
- Avoid shared mutable state between timers.
- If you need to fetch data asynchronously, use promises with proper cancellation logic to prevent outdated responses from overwriting newer data.

---

### Additional Tips:

- For more complex scenarios, consider using `requestAnimationFrame` for smoother UI updates.
- Use a framework like React or Vue for better state management and reactive updates, which simplifies this process significantly.
- Always cleanup timers when the element is destroyed to prevent memory leaks.

---

Would you like an example with asynchronous data fetching or additional features?