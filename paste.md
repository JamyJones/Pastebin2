You’d like to create a leaderboard table using ag-Grid’s JavaScript API with three columns: usernames, avatar images, and streaks. Here’s a professional approach using ag-Grid in plain JavaScript:

HTML:
```html
<!-- Include ag-Grid styles and scripts -->
<link rel="stylesheet" href="https://docsbot.ai/" />
<link rel="stylesheet" href="https://docsbot.ai/" />
<div id="myGrid" class="ag-theme-alpine" style="height: 400px; width: 600px;"></div>
<script src="https://docsbot.ai/"></script>
<script src="leaderboard.js"></script>
```

JavaScript (leaderboard.js):
```javascript
// Column definitions
const columnDefs = [
  { headerName: 'Username', field: 'username', sortable: true, filter: true },
  {
    headerName: 'Avatar',
    field: 'avatar',
    cellRenderer: params => `<img src="${params.value}" alt="avatar" style="width:32px;height:32px;border-radius:50%;" />`,
    width: 80
  },
  { headerName: 'Streak', field: 'streak', sortable: true, filter: true }
];

// Sample row data
const rowData = [
  { username: 'alice', avatar: 'https://docsbot.ai/', streak: 12 },
  { username: 'bob', avatar: 'https://docsbot.ai/', streak: 8 },
  { username: 'carol', avatar: 'https://docsbot.ai/', streak: 15 }
];

// Grid options
const gridOptions = {
  columnDefs,
  rowData,
  domLayout: 'autoHeight'
};

// Initialize the grid after the page loads
document.addEventListener('DOMContentLoaded', function () {
  const gridDiv = document.getElementById('myGrid');
  new agGrid.Grid(gridDiv, gridOptions);
});
```

Best Practices Demonstrated:

- Use cellRenderer for custom cell content (avatars).
- Enable sorting and filtering for relevant columns.
- Use semantic HTML and scoped CSS for maintainability.
- Separate data and configuration for clarity.

Let me know if you need this adapted for a specific framework or additional features.