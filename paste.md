Certainly! To create a leaderboard with the specified features using ag-Grid in vanilla JavaScript, you can follow this approach:

### Requirements:
- Two columns: 
  - `User` (combining username and avatar)
- Styling:
  - Navy blue background
  - Scrollable grid

### Implementation:

1. **HTML** - Basic container for ag-Grid and include ag-Grid scripts.
2. **CSS** - Style for background, grid height for scrollability.
3. **JavaScript** - Initialize ag-Grid with data and custom cell renderers.

---

### Full Example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>Leaderboard with ag-Grid</title>
    <!-- ag-Grid CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-grid.css" />
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ag-grid-community/styles/ag-theme-alpine.css" />

    <style>
        /* Set the background color and size for the grid container */
        body {
            margin: 0;
            padding: 0;
            background-color: navy; /* Navy blue background */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        #myGrid {
            width: 80%;
            height: 60vh; /* Fixed height for scrollability */
        }
    </style>
</head>
<body>
    <div id="myGrid" class="ag-theme-alpine"></div>

    <!-- ag-Grid JS -->
    <script src="https://cdn.jsdelivr.net/npm/ag-grid-community/dist/ag-grid-community.noStyle.js"></script>

    <script>
        // Sample Data
        const rowData = [
            {
                username: 'User1',
                avatar: 'https://randomuser.me/api/portraits/men/1.jpg',
                progress: 70
            },
            {
                username: 'User2',
                avatar: 'https://randomuser.me/api/portraits/women/2.jpg',
                progress: 85
            },
            {
                username: 'User3',
                avatar: 'https://randomuser.me/api/portraits/men/3.jpg',
                progress: 55
            },
            {
                username: 'User4',
                avatar: 'https://randomuser.me/api/portraits/women/4.jpg',
                progress: 90
            },
            // Add more data as needed
        ];

        // Column definitions with custom cell renderer for 'user' column
        const columnDefs = [
            {
                headerName: 'User',
                field: 'user',
                cellRenderer: (params) => {
                    // Create a container div
                    const container = document.createElement('div');
                    container.style.display = 'flex';
                    container.style.alignItems = 'center';

                    // Avatar Image
                    const img = document.createElement('img');
                    img.src = params.data.avatar;
                    img.alt = params.data.username;
                    img.style.width = '40px';
                    img.style.height = '40px';
                    img.style.borderRadius = '50%';
                    img.style.marginRight = '10px';

                    // Username Text
                    const nameSpan = document.createElement('span');
                    nameSpan.innerText = params.data.username;

                    // Append avatar and username to container
                    container.appendChild(img);
                    container.appendChild(nameSpan);

                    return container;
                }
            },
            {
                headerName: 'Progress',
                field: 'progress',
                width: 100,
                cellRenderer: (params) => {
                    // Optional: visualize progress
                    const progressDiv = document.createElement('div');
                    progressDiv.style.backgroundColor = '#ccc';
                    progressDiv.style.width = '100%';
                    progressDiv.style.borderRadius = '4px';
                    progressDiv.style.overflow = 'hidden';

                    const progressBar = document.createElement('div');
                    progressBar.style.backgroundColor = '#4caf50'; // green
                    progressBar.style.height = '10px';
                    progressBar.style.width = params.value + '%';

                    progressDiv.appendChild(progressBar);
                    return progressDiv;
                }
            }
        ];

        // Grid options
        const gridOptions = {
            columnDefs: columnDefs,
            rowData: rowData,
            domLayout: 'autoHeight', // or remove for fixed height with scroll
            // Uncomment below for fixed height with scroll
            // rowHeight: 60
        };

        // Initialize the grid
        document.addEventListener('DOMContentLoaded', () => {
            const eGridDiv = document.querySelector('#myGrid');
            new agGrid.Grid(eGridDiv, gridOptions);
        });
    </script>
</body>
</html>
```

---

### Explanation:
- The container `#myGrid` uses `ag-theme-alpine` with custom CSS for size and background.
- The `cellRenderer` for the `User` column combines avatar and username.
- The grid height is set with CSS (`height: 60vh`) to make it scrollable if data exceeds the visible area.
- Additional styling ensures the avatar appears as a circle and the layout looks clean.

Feel free to adapt data and styling further to fit your design!