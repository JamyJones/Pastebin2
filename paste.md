You’d like to create a leaderboard table using the ag-Grid JavaScript API with three columns: usernames, avatar images, and streaks. Here’s a professional approach using plain JavaScript and ag-Grid best practices.

**HTML:**
```html
<!-- Include ag-Grid styles and scripts -->
<link rel="stylesheet" href="https://docsbot.ai/" />
<link rel="stylesheet" href="https://docsbot.ai/" />
<div id="myGrid" class="ag-theme-alpine" style="height: 400px; width: 600px;"></div>
<script src="https://docsbot.ai/"></script>
<script src="leaderboard.js"></script>
```

**JavaScript (leaderboard.js):**
```javascript
// Sample data
const rowData = [
  { username: 'alice', avatar: 'https://docsbot.ai/', streak: 15 },
  { username: 'bob', avatar: 'https://docsbot.ai/', streak: 12 },
  { username: 'charlie', avatar: 'https://docsbot.ai/', streak: 10 }
];

// Column definitions
const columnDefs = [
  { headerName: 'Username', field: 'username', sortable: true, filter: true },
  {
    headerName: 'Avatar',
    field: 'avatar',
    cellRenderer: params => `<img src="${params.value}" alt="avatar" style="width:32px;height:32px;border-radius:50%;" />`,
    width: 80,
    suppressMenu: true
  },
  { headerName: 'Streak', field: 'streak', sortable: true, filter: true }
];

// Grid options
const gridOptions = {
  columnDefs,
  rowData,
  domLayout: 'autoHeight',
  defaultColDef: {
    resizable: true,
    flex: 1
  }
};

// Initialize the grid after the page loads
document.addEventListener('DOMContentLoaded', function () {
  const gridDiv = document.getElementById('myGrid');
  new agGrid.Grid(gridDiv, gridOptions);
});
```

**Best Practices Demonstrated:**
- Use of cellRenderer for custom avatar rendering.
- Responsive column sizing with flex and resizable columns.
- Sorting and filtering enabled for relevant columns.
- Clean separation of data, column definitions, and grid options.

Let me know if you need this adapted for a specific framework or additional features.