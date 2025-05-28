In a Bootstrap tabbed interface, when you switch between tabs, the content of the inactive tab is typically hidden from view but remains in the DOM. This means that any JavaScript timers or progress indicators running in the inactive tab will continue to run in the background, as they are not paused or stopped automatically when you switch tabs.

For your Pomodoro app, if you want to ensure that timers or progress indicators are paused when the user switches tabs, you will need to implement this behavior manually. Here are some steps you can take:

1. **Event Listeners**: Add event listeners to detect when a tab is shown or hidden. You can use Bootstrap's tab events, such as `shown.bs.tab`, to trigger your pause and resume logic.

2. **Pause Timers**: When a tab is hidden, pause any active timers or progress indicators. You can store the current state of the timer and the elapsed time so that you can resume it later.

3. **Resume Timers**: When the tab is shown again, resume the timer from where it left off.

Here is a simple example of how you might implement this:

```javascript
let timer;
let elapsedTime = 0;
let isRunning = false;

function startTimer() {
    isRunning = true;
    timer = setInterval(() => {
        elapsedTime++;
        // Update your UI with the elapsed time
    }, 1000);
}

function pauseTimer() {
    isRunning = false;
    clearInterval(timer);
}

$('#myTab a').on('shown.bs.tab', function (e) {
    // Check which tab is being shown
    const targetTab = $(e.target).attr('href');

    if (targetTab === '#pomodoroTab') {
        // Resume timer if the Pomodoro tab is shown
        if (!isRunning) {
            startTimer();
        }
    } else {
        // Pause timer if switching away from the Pomodoro tab
        pauseTimer();
    }
});
```

In this example, the timer starts when the Pomodoro tab is shown and pauses when the user switches to another tab. You can adjust the logic based on your specific requirements.