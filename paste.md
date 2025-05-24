You want to create a leaderboard using ag-Grid in vanilla JavaScript, with two columns: one for the user (containing both username and avatar) and one for progress. The grid should have a navy blue background and be scrollable.

Here’s a professional approach:

1. Include ag-Grid in your HTML (via CDN):

```html
<link rel="stylesheet" href="https://docsbot.ai/" />
<link rel="stylesheet" href="https://docsbot.ai/" />
<script src="https://docsbot.ai/"></script>
```

2. Add a container for the grid:

```html
<div id="leaderboardGrid" class="ag-theme-alpine" style="height: 400px; width: 500px;"></div>
```

3. Style the background and scrolling:

```html
<style>
  #leaderboardGrid {
    background-color: navy;
    color: white;
    overflow-y: auto;
  }
  .user-cell {
    display: flex;
    align-items: center;
  }
  .user-avatar {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    margin-right: 8px;
  }
</style>
```

4. JavaScript to initialize ag-Grid:

```javascript
const columnDefs = [
  {
    headerName: 'User',
    field: 'user',
    cellRenderer: params => {
      return `
        <div class="user-cell">
          <img class="user-avatar" src="${params.data.avatar}" alt="avatar"/>
          <span>${params.data.username}</span>
        </div>
      `;
    },
    flex: 1,
  },
  { headerName: 'Progress', field: 'progress', flex: 1 }
];

const rowData = [
  { username: 'Alice', avatar: 'https://docsbot.ai/', progress: '80%' },
  { username: 'Bob', avatar: 'https://docsbot.ai/', progress: '65%' },
  // Add more users as needed
];

const gridOptions = {
  columnDefs,
  rowData,
  domLayout: 'autoHeight',
  suppressHorizontalScroll: false,
};

document.addEventListener('DOMContentLoaded', function () {
  const gridDiv = document.getElementById('leaderboardGrid');
  new agGrid.Grid(gridDiv, gridOptions);
});
```

**Best Practices Applied:**

- Used cellRenderer for custom cell content.
- Kept styling modular and scoped.
- Used flex layout for avatar and username alignment.
- Ensured accessibility with alt attributes.

Let me know if you need further customization or have additional requirements!