Certainly! To create a simple, scrollable leaderboard with a navy blue background, using only vanilla JavaScript and CSS, you don't necessarily need external libraries. However, if you want to enhance your development experience with styling or layout tools, libraries like Bootstrap or Tailwind CSS could help, but here I'll give you a pure vanilla implementation based on your specifications.

### Approach:
- Create a container with a navy blue background.
- Make the leaderboard scrollable.
- Display each user with their avatar and username under a single `user` column.
- Show progress within each entry.

### Example Implementation

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Leaderboard</title>
<style>
  body {
    margin: 0;
    font-family: Arial, sans-serif;
  }
  /* Main container with navy blue background and fixed height for scrolling */
  .leaderboard-container {
    background-color: #000080; /* Navy blue */
    max-height: 600px; /* or whatever height you want */
    overflow-y: auto; /* Enable vertical scroll */
    padding: 10px;
  }

  /* Individual user item styles */
  .user-entry {
    display: flex;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ffffff33; /* Light separator */
    transition: background-color 0.2s;
  }

  .user-entry:hover {
    background-color: #ffffff22;
  }

  /* Avatar styles */
  .avatar {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    object-fit: cover;
    margin-right: 15px;
  }

  /* User info (name and progress) styles */
  .user-info {
    display: flex;
    flex-direction: column;
  }

  .username {
    font-weight: bold;
    font-size: 1.1em;
    color: #fff;
  }

  /* Progress bar container */
  .progress-container {
    width: 200px;
    height: 10px;
    background-color: #ffffff33;
    border-radius: 5px;
    margin-top: 5px;
  }

  /* Progress bar fill */
  .progress-bar {
    height: 100%;
    background-color: #4caf50; /* green for progress */
    width: 0%;
    border-radius: 5px;
    transition: width 0.3s;
  }
</style>
</head>
<body>

<div class="leaderboard-container" id="leaderboard">
  <!-- User entries will be inserted here dynamically -->
</div>

<script>
  // Sample data - replace or fetch from your backend
  const users = [
    { username: "Alice", avatar: "https://i.imgur.com/8Km9tLL.png", progress: 70 },
    { username: "Bob", avatar: "https://i.imgur.com/6b6IB0w.png", progress: 45 },
    { username: "Charlie", avatar: "https://i.imgur.com/T9EZ7jM.png", progress: 85 },
    { username: "David", avatar: "https://i.imgur.com/lG2sL7M.png", progress: 30 },
    // Add more users as needed
  ];

  const leaderboard = document.getElementById('leaderboard');

  // Function to create user entry
  function createUserEntry(user) {
    const entry = document.createElement('div');
    entry.className = 'user-entry';

    // Avatar image
    const avatarImg = document.createElement('img');
    avatarImg.src = user.avatar;
    avatarImg.alt = `${user.username}'s avatar`;
    avatarImg.className = 'avatar';

    // User info container
    const userInfo = document.createElement('div');
    userInfo.className = 'user-info';

    // Username
    const username = document.createElement('div');
    username.className = 'username';
    username.textContent = user.username;

    // Progress bar container
    const progressContainer = document.createElement('div');
    progressContainer.className = 'progress-container';

    // Progress fill
    const progressBar = document.createElement('div');
    progressBar.className = 'progress-bar';
    progressBar.style.width = user.progress + '%';

    // Append progress fill into container
    progressContainer.appendChild(progressBar);

    // Append username and progress to user info
    userInfo.appendChild(username);
    userInfo.appendChild(progressContainer);

    // Append avatar and info to entry
    entry.appendChild(avatarImg);
    entry.appendChild(userInfo);

    return entry;
  }

  // Populate the leaderboard
  users.forEach(user => {
    const userEntry = createUserEntry(user);
    leaderboard.appendChild(userEntry);
  });
</script>

</body>
</html>
```

---

### How it works:
- The `.leaderboard-container` is styled to have a navy blue background, fixed max height, and vertical scrolling enabled.
- Each user entry is a flex container with an avatar on the left and user details on the right.
- The user details include the username and a progress bar indicating progress percentage.
- JavaScript dynamically creates each user card from the `users` array, making it easy to update or fetch data.

### Customization:
- Replace the sample data with real data fetched via API or server.
- Adjust styling, sizes, colors, or layout as per your design requirements.
- Add features like rankings, search, or sorting if needed.

---

Let me know if you'd like me to include sorting, dynamic data fetch, or any additional features!