Certainly! To create a leaderboard table using ag-Grid in JavaScript with the specified columns, follow these steps:

### 1. Include ag-Grid in your project:
You can include the ag-Grid library via CDN for simplicity:

```html
<!-- Include ag-Grid styles -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-grid.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-theme-alpine.css" />

<!-- Include ag-Grid JavaScript -->
<script src="https://cdn.jsdelivr.net/npm/ag-grid-community/dist/ag-grid-community.min.js"></script>
```

### 2. Create HTML container:
Set up a `div` placeholder for the grid:

```html
<div id="leaderboardGrid" class="ag-theme-alpine" style="height: 500px; width: 600px;"></div>
```

### 3. Initialize the grid with column definitions and data:
Here's a JavaScript example that defines the columns and data, including rendering images in the avatar column:

```javascript
// Column definitions
const columnDefs = [
  { headerName: "Username", field: "username" },
  { 
    headerName: "Avatar", 
    field: "avatar", 
    cellRenderer: function(params) {
      return `<img src="${params.value}" alt="avatar" style="width:50px; height:50px; border-radius:50%;">`;
    },
    width: 70
  },
  { headerName: "Streaks", field: "streaks" }
];

// Sample data
const rowData = [
  {
    username: "User1",
    avatar: "https://via.placeholder.com/50",
    streaks: 5
  },
  {
    username: "User2",
    avatar: "https://via.placeholder.com/50",
    streaks: 12
  },
  {
    username: "User3",
    avatar: "https://via.placeholder.com/50",
    streaks: 3
  }
];

// Grid options
const gridOptions = {
  columnDefs: columnDefs,
  rowData: rowData,
  defaultColDef: {
    sortable: true,
    filter: true,
    resizable: true
  }
};

// Initialize the grid after the page loads
document.addEventListener('DOMContentLoaded', () => {
  const gridDiv = document.querySelector('#leaderboardGrid');
  new agGrid.Grid(gridDiv, gridOptions);
});
```

### **Explanation of key parts:**

- **Avatar column rendering:** uses `cellRenderer` to include an `<img>` tag with styling for circular avatars.
- **Column widths:** set explicitly for consistent appearance.
- **Default column definitions:** set sortable, filterable, and resizable to enhance user experience.
- **Data:** structured with `username`, `avatar (URL)`, and `streaks`.

### **Result:**
This will produce a sortable, filterable leaderboard with user avatars, usernames, and streak counts.

---

If you want to dynamically update the data or include additional features, you can modify `rowData` or call `gridOptions.api.setRowData(newData)` when needed.