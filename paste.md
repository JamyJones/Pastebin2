In Bootstrap, the tabs component (implemented via `bootstrap-tab` or similar JavaScript) is primarily a client-side UI change. When you switch between tabs, the default behavior is to simply hide the inactive tab content and show the active one through CSS toggling (`display: none` or similar). 

### Key points:
- **Timers (`setTimeout`, `setInterval`)**: These are managed by JavaScript on your page. Switching tabs **does not automatically** pause or stop timers. They will continue to run unless explicitly cleared.
- **Progress bars or animations**: CSS animations or JavaScript-driven progress bars will also continue executing unless you programmatically pause or reset them.

### What actually happens:
- The content for hidden tabs is **still in the DOM** but hidden via CSS.
- Any ongoing JavaScript timers or animations remain active unless you explicitly handle their pausing/stopping behavior.

### Best practices:
To prevent performance issues or unintended behavior, **it's recommended to pause or reset timers, animations, or ongoing processes** when a tab is hidden and resume them when shown.

### Example:
Suppose you have a timer in a tab. To ensure it pauses when switching tabs, you can:

1. Listen to tab show/hide events.
2. Pause/clear timers when a tab is hidden.
3. Resume or restart them when the tab is shown.

```javascript
// Example: Using Bootstrap's tab events
$('#myTab').on('shown.bs.tab', function (event) {
    const targetTabId = $(event.target).attr('href');

    if (targetTabId === '#tab1') {
        // Resume/start timer
        startTimer();
    } else if (targetTabId === '#tab2') {
        // Pause/stop timer
        clearTimer();
    }
});

// Assume these functions manage your timers
let timerId;
function startTimer() {
    timerId = setInterval(() => {
        console.log('Timer tick');
        // Update progress or perform actions
    }, 1000);
}

function clearTimer() {
    clearInterval(timerId);
}
```

### Summary:
- **Switching Bootstrap tabs alone does not pause timers or processes.**
- To **pause animations or timers**, you need to implement event handlers on `shown.bs.tab` or `hide.bs.tab` to manage state accordingly.
- Properly managing this behavior ensures smooth UX and reliable application performance.

---

If you'd like, I can provide a more comprehensive example tailored to your specific application!