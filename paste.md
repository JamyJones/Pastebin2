Here’s how you can create a leaderboard table using the AG Grid JavaScript API. This example sets up three columns: usernames, avatar images, and streaks. The avatar column uses `cellRenderer` to display images correctly.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AG Grid Leaderboard</title>
    <link rel="stylesheet" href="https://unpkg.com/ag-grid-community/styles/ag-grid.css">
    <link rel="stylesheet" href="https://unpkg.com/ag-grid-community/styles/ag-theme-alpine.css">
</head>
<body>
    <div id="myGrid" class="ag-theme-alpine" style="height: 400px; width: 600px;"></div>
    
    <script src="https://unpkg.com/ag-grid-community/dist/ag-grid-community.min.js"></script>
    <script>
        // Sample leaderboard data
        const rowData = [
            { username: "Alice", avatar: "https://example.com/avatar1.png", streak: 15 },
            { username: "Bob", avatar: "https://example.com/avatar2.png", streak: 10 },
            { username: "Charlie", avatar: "https://example.com/avatar3.png", streak: 20 }
        ];

        // Column definitions
        const columnDefs = [
            { headerName: "Username", field: "username", sortable: true },
            { 
                headerName: "Avatar", 
                field: "avatar", 
                cellRenderer: params => `<img src="${params.value}" width="40" height="40" style="border-radius:50%;">`
            },
            { headerName: "Streak", field: "streak", sortable: true }
        ];

        // Grid options
        const gridOptions = {
            columnDefs: columnDefs,
            rowData: rowData,
            defaultColDef: {
                resizable: true
            }
        };

        // Initialize the grid
        document.addEventListener("DOMContentLoaded", () => {
            new agGrid.Grid(document.getElementById("myGrid"), gridOptions);
        });
    </script>
</body>
</html>
```

### Explanation:
- **AG Grid setup**: Includes styles and script from AG Grid CDN.
- **Column definitions**:
  - `username`: Standard text column.
  - `avatar`: Uses `cellRenderer` to display images in table cells.
  - `streak`: Numeric values that can be sorted.
- **Grid options**: Enables resizing for better user experience.

This approach follows industry best practices by keeping configuration structured and data-driven. Let me know if you need enhancements! [[0]](https://github.com/EleanorEllingson/web-dev/tree/b2f2a382e77a20fd6895677c8b8f402ac4bae352/7-bank-project/1-template-route/translations/README.ko.md)



> [0] [](https://github.com/EleanorEllingson/web-dev/tree/b2f2a382e77a20fd6895677c8b8f402ac4bae352/7-bank-project/1-template-route/translations/README.ko.md)