You can achieve this using vanilla JavaScript along with HTML and CSS. Below is a structured example:

### **Implementation**
#### **1. HTML**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Leaderboard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: navy;
            color: white;
        }
        .leaderboard-container {
            width: 50%;
            margin: auto;
            overflow-y: scroll;
            height: 300px;
            border: 2px solid white;
            padding: 10px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            padding: 10px;
            text-align: left;
            border-bottom: 1px solid white;
        }
        .user {
            display: flex;
            align-items: center;
        }
        .user img {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            margin-right: 10px;
        }
    </style>
</head>
<body>

<div class="leaderboard-container">
    <table>
        <thead>
            <tr>
                <th>User</th>
                <th>Progress</th>
            </tr>
        </thead>
        <tbody id="leaderboard">
        </tbody>
    </table>
</div>

<script>
    // Sample Data
    const users = [
        { name: "Alice", avatar: "https://via.placeholder.com/40", progress: "85%" },
        { name: "Bob", avatar: "https://via.placeholder.com/40", progress: "90%" },
        { name: "Charlie", avatar: "https://via.placeholder.com/40", progress: "75%" },
        { name: "Diana", avatar: "https://via.placeholder.com/40", progress: "95%" }
    ];

    const leaderboard = document.getElementById("leaderboard");

    // Populate Table
    users.forEach(user => {
        const row = document.createElement("tr");
        row.innerHTML = `
            <td class="user">
                <img src="${user.avatar}" alt="${user.name}'s avatar">
                <span>${user.name}</span>
            </td>
            <td>${user.progress}</td>
        `;
        leaderboard.appendChild(row);
    });
</script>

</body>
</html>
```

### **Explanation**
- **HTML Structure:** Defines a table inside a scrollable container (`.leaderboard-container`).
- **CSS Styling:**
  - The background is set to **navy blue** (`background-color: navy`).
  - The table is styled with white borders for visibility.
  - The leaderboard is **scrollable** (`overflow-y: scroll`).
  - The avatars are **rounded** and displayed alongside usernames.
- **JavaScript Functionality:**
  - **An array of user objects** holds details about the username, avatar, and progress.
  - **JavaScript dynamically populates** the leaderboard with rows.

### **Enhancements**
- You can replace placeholder avatars (`https://via.placeholder.com/40`) with real URLs.
- Implement sorting functionality to order users based on progress dynamically.
- Include hover effects or animations for a better user experience.

Would you like additional customizations? [[0]](https://github.com/buribalazs/smooth-drag-order/tree/7b40d21d076c3e31765f61481f537beaf4c5ec9f/README.md) [[1]](https://github.com/Sirjoseph94/hngleaderboard/tree/7ed621bcda562ed3159de8a27bf29c338b61ea15/resources/views/layouts/base.blade.php)



> [0] [](https://github.com/buribalazs/smooth-drag-order/tree/7b40d21d076c3e31765f61481f537beaf4c5ec9f/README.md)
>
> [1] [](https://github.com/Sirjoseph94/hngleaderboard/tree/7ed621bcda562ed3159de8a27bf29c338b61ea15/resources/views/layouts/base.blade.php)