Certainly! Here's a professional approach to creating a simple leaderboard using ag-Grid with the specifications:

- Two columns:
  - `user`: which combines the username and avatar.
- Navy blue background.
- Scrollable grid.

### Step-by-step solution:

1. **Include ag-Grid styles and scripts:**

Make sure you include ag-Grid's CSS and JS in your HTML file:

```html
<!-- ag-Grid Styles -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-grid.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-theme-alpine-dark.css" />

<!-- ag-Grid Script -->
<script src="https://cdn.jsdelivr.net/npm/ag-grid-community/dist/ag-grid-community.min.js"></script>
```

2. **HTML Structure:**

```html
<div id="myGrid" class="ag-theme-alpine-dark" style="height: 600px; width: 100%;"></div>
```

3. **JavaScript for grid setup:**

```js
// Sample data
const rowData = [
  {
    user: {
      username: 'Player1',
      avatarUrl: 'https://example.com/avatar1.png'
    },
    progress: 75
  },
  {
    user: {
      username: 'Player2',
      avatarUrl: 'https://example.com/avatar2.png'
    },
    progress: 50
  },
  // Add more data as needed
];

// Column Definitions
const columnDefs = [
  {
    headerName: "User",
    field: "user",
    cellRenderer: function(params) {
      const { username, avatarUrl } = params.value;
      return `
        <div style="display: flex; align-items: center;">
          <img src="${avatarUrl}" alt="${username}" style="width:40px; height:40px; border-radius:50%; margin-right:10px;">
          <span>${username}</span>
        </div>
      `;
    },
    minWidth: 200
  },
  {
    headerName: "Progress",
    field: "progress",
    cellRenderer: function(params) {
      return `
        <div style="width: 100%; background-color: #ddd;">
          <div style="width: ${params.value}%; background-color: #4CAF50; height: 20px;"></div>
        </div>
      `;
    },
    cellStyle: { textAlign: "center" }
  }
];

// Grid Options
const gridOptions = {
  columnDefs: columnDefs,
  rowData: rowData,
  defaultColDef: {
    resizable: true,
    sortable: true
  },
  // Enable vertical scrolling
  domLayout: 'autoHeight',
  suppressHorizontalScroll: false,
};

// Get the div and initialize the grid
const eGridDiv = document.getElementById('myGrid');
new agGrid.Grid(eGridDiv, gridOptions);
```

4. **Styling the background:**

The `ag-theme-alpine-dark` (used in the `class` of your container div) already has a dark background, but to ensure navy blue:

You can override grid background styles in CSS:

```css
.ag-theme-alpine-dark {
  background-color: navy !important;
}
```

### Final HTML snippet:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Leaderboard with ag-Grid</title>
<!-- ag-Grid CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-grid.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-theme-alpine-dark.css" />
<style>
  /* Override grid background color */
  .ag-theme-alpine-dark {
    background-color: navy !important;
  }
</style>
</head>
<body>
<div id="myGrid" class="ag-theme-alpine-dark" style="height: 600px; width: 100%;"></div>

<!-- ag-Grid JS -->
<script src="https://cdn.jsdelivr.net/npm/ag-grid-community/dist/ag-grid-community.min.js"></script>
<script>
  const rowData = [
    {
      user: {
        username: 'Player1',
        avatarUrl: 'https://via.placeholder.com/40/0000FF/FFFFFF?text=P1'
      },
      progress: 75
    },
    {
      user: {
        username: 'Player2',
        avatarUrl: 'https://via.placeholder.com/40/FF0000/FFFFFF?text=P2'
      },
      progress: 50
    },
    // Add more data as needed
  ];

  const columnDefs = [
    {
      headerName: "User",
      field: "user",
      cellRenderer: function(params) {
        const { username, avatarUrl } = params.value;
        return `
          <div style="display: flex; align-items: center;">
            <img src="${avatarUrl}" alt="${username}" style="width:40px; height:40px; border-radius:50%; margin-right:10px;">
            <span>${username}</span>
          </div>
        `;
      },
      minWidth: 200
    },
    {
      headerName: "Progress",
      field: "progress",
      cellRenderer: function(params) {
        return `
          <div style="width: 100%; background-color: #ddd;">
            <div style="width: ${params.value}%; background-color: #4CAF50; height: 20px;"></div>
          </div>
        `;
      },
      cellStyle: { textAlign: "center" }
    }
  ];

  const gridOptions = {
    columnDefs: columnDefs,
    rowData: rowData,
    defaultColDef: {
      resizable: true,
      sortable: true,
    },
    domLayout: 'autoHeight',
  };

  document.addEventListener('DOMContentLoaded', () => {
    const eGridDiv = document.getElementById('myGrid');
    new agGrid.Grid(eGridDiv, gridOptions);
  });
</script>
</body>
</html>
```

---

### Notes:
- The `domLayout: 'autoHeight'` makes the grid height adapt to the content, but with a fixed container height set to enable scrolling.
- To ensure scrollability, you can set a fixed height (like `height: 600px`) on the container div.
- Adjust the avatar size and progress bar as needed to match your design.

This setup creates a professional, visually styled leaderboard with avatars, user names, progress bars, dark theme, and scrolling capabilities.