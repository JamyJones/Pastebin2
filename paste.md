You’d like to create a leaderboard table using ag-Grid’s JavaScript API with three columns: usernames, avatar images, and streaks. Below is a professional implementation using ag-Grid’s community edition, including custom cell rendering for avatar images.

HTML:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Leaderboard Table</title>
  <link rel="stylesheet" href="https://docsbot.ai/">
  <link rel="stylesheet" href="https://docsbot.ai/">
  <style>
    .avatar-img {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      object-fit: cover;
    }
    .ag-theme-alpine {
      height: 400px;
      width: 600px;
    }
  </style>
</head>
<body>
  <div id="myGrid" class="ag-theme-alpine"></div>
  <script src="https://docsbot.ai/"></script>
  <script src="leaderboard.js"></script>
</body>
</html>
```

JavaScript (leaderboard.js):
```javascript
// Sample data
const rowData = [
  { username: 'alice', avatar: 'https://docsbot.ai/', streak: 12 },
  { username: 'bob', avatar: 'https://docsbot.ai/', streak: 9 },
  { username: 'carol', avatar: 'https://docsbot.ai/', streak: 15 }
];

// Column definitions
const columnDefs = [
  { headerName: 'Username', field: 'username', sortable: true, filter: true },
  {
    headerName: 'Avatar',
    field: 'avatar',
    cellRenderer: params => `<img class="avatar-img" src="${params.value}" alt="avatar">`,
    width: 80,
    suppressMenu: true
  },
  { headerName: 'Streak', field: 'streak', sortable: true, filter: true }
];

// Grid options
const gridOptions = {
  columnDefs,
  rowData,
  domLayout: 'autoHeight'
};

// Initialize the grid
document.addEventListener('DOMContentLoaded', function () {
  const gridDiv = document.getElementById('myGrid');
  new agGrid.Grid(gridDiv, gridOptions);
});
```

Best Practices:

- Use cellRenderer for custom cell content (e.g., images).
- Define columnDefs clearly for maintainability.
- Enable sorting and filtering for better user experience.
- Use CSS classes for consistent image styling.

Let me know if you need further customization or integration details.