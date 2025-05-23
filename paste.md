Certainly! To create a table using **ag-Grid** with three columns—`Usernames`, `Avatar Images`, and `Streaks`—you need to set up your grid with proper column definitions, data, and cell rendering where necessary. Here's an example demonstrating how to do this professionally.

### 1. Include ag-Grid in your project

Ensure you have included ag-Grid's library in your project. For example, via CDN in HTML:

```html
<!-- Ag-Grid CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-grid.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-theme-alpine.css" />

<!-- Ag-Grid JavaScript -->
<script src="https://cdn.jsdelivr.net/npm/ag-grid-community/dist/ag-grid-community.noStyle.js"></script>
```

### 2. Set up the HTML container

```html
<div id="myGrid" class="ag-theme-alpine" style="height: 500px; width: 700px;"></div>
```

### 3. JavaScript code to initialize ag-Grid

```js
// Column definitions with custom cell renderers for avatar images
const columnDefs = [
  { headerName: 'Username', field: 'username', sortable: true, filter: true },
  { 
    headerName: 'Avatar', 
    field: 'avatar', 
    cellRenderer: params => {
      return `<img src="${params.value}" alt="avatar" style="width:50px; height:50px; border-radius:50%;">`;
    }
  },
  { headerName: 'Streaks', field: 'streaks', sortable: true, filter: true }
];

// Sample row data
const rowData = [
  {
    username: 'user1',
    avatar: 'https://randomuser.me/api/portraits/men/1.jpg',
    streaks: 5
  },
  {
    username: 'user2',
    avatar: 'https://randomuser.me/api/portraits/women/2.jpg',
    streaks: 10
  },
  {
    username: 'user3',
    avatar: 'https://randomuser.me/api/portraits/men/3.jpg',
    streaks: 7
  }
];

// Grid options
const gridOptions = {
  columnDefs: columnDefs,
  rowData: rowData,
  defaultColDef: {
    flex: 1,
    minWidth: 100,
    editable: false,
  }
};

// Initialize the grid
document.addEventListener('DOMContentLoaded', () => {
  const gridDiv = document.querySelector('#myGrid');
  new agGrid.Grid(gridDiv, gridOptions);
});
```

---

### Summary:
- **Column Definitions**: Include `headerName` and `field`. Use `cellRenderer` for custom rendering (avatar images).
- **Row Data**: Provide data with appropriate URLs for avatar images.
- **Grid Initialization**: Instantiate `agGrid.Grid` with container and options.
- **Styling**: Use CSS for avatar size and border-radius for rounded images.

Feel free to customize further — for pagination, sorting, styling, or adding editing capabilities.