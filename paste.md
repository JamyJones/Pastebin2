Creating a leaderboard for your study app involves several steps, from designing the data model, storing user activity, and calculating daily rankings, to displaying the leaderboard in the front-end. Here's a detailed, professional approach:

---

### **1. Data Modeling**

**Database Tables/Collections:**

- **Users:** Stores student info.
- **StudySessions:** Stores each study period, including timestamp, duration, and pomodoros count.
- **DailyStats:** (Optional) aggregations for quick leaderboard calculations.

---

### **2. Data Collection**

During the study session, capture:
- Start time
- End time
- Number of Pomodoros completed 
- Total hours studied

---

### **3. Backend Implementation**

Assuming a typical REST API with Node.js and Express, and a relational database like PostgreSQL.

**Sample schema:**

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50),
  -- other user info
);

CREATE TABLE study_sessions (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  start_time TIMESTAMP NOT NULL,
  end_time TIMESTAMP NOT NULL,
  pomodoros INTEGER NOT NULL
);
```

---

### **4. Recording Study Sessions**

Create an API endpoint to record a new session:

```javascript
// POST /api/study-sessions
app.post('/api/study-sessions', async (req, res) => {
  const { userId, startTime, endTime, pomodoros } = req.body;
  // Validate input here
  
  await db.query(
    'INSERT INTO study_sessions (user_id, start_time, end_time, pomodoros) VALUES ($1, $2, $3, $4)',
    [userId, startTime, endTime, pomodoro]
  );
  res.status(201).send({ message: 'Session recorded' });
});
```

---

### **5. Calculating Daily Rankings**

To generate daily rankings, aggregate total hours and pomodoros per user for a specific day.

**Example SQL query:**

```sql
SELECT
  u.id,
  u.username,
  SUM(EXTRACT(EPOCH FROM (ss.end_time - ss.start_time)) / 3600) AS hours_studied,
  SUM(ss.pomodoros) AS total_pomodoros
FROM users u
JOIN study_sessions ss ON u.id = ss.user_id
WHERE DATE(ss.start_time) = CURRENT_DATE
GROUP BY u.id, u.username
ORDER BY hours_studied DESC;
```

You can run this query in your backend endpoint to fetch the daily leaderboard data.

---

### **6. API Endpoint for Leaderboard:**

```javascript
app.get('/api/leaderboard', async (req, res) => {
  const { date } = req.query || { date: new Date().toISOString().slice(0, 10) };

  const leaderboardData = await db.query(
    `
    SELECT u.id, u.username,
           SUM(EXTRACT(EPOCH FROM (ss.end_time - ss.start_time)) / 3600) AS hours_studied,
           SUM(ss.pomodoros) AS total_pomodoros
    FROM users u
    JOIN study_sessions ss ON u.id = ss.user_id
    WHERE DATE(ss.start_time) = $1
    GROUP BY u.id, u.username
    ORDER BY hours_studied DESC
    `,
    [date]
  );

  res.json(leaderboardData.rows);
});
```

---

### **7. Front-End Display**

Use a React component or similar framework to fetch and display the leaderboard:

```jsx
import React, { useEffect, useState } from 'react';

function Leaderboard() {
  const [leaderboard, setLeaderboard] = useState([]);

  useEffect(() => {
    fetch('/api/leaderboard')
      .then(res => res.json())
      .then(data => setLeaderboard(data))
      .catch(err => console.error('Error fetching leaderboard:', err));
  }, []);

  return (
    <div>
      <h2>Today's Study Leaderboard</h2>
      <table>
        <thead>
          <tr>
            <th>Rank</th>
            <th>Student</th>
            <th>Hours Studied</th>
            <th>Pomodoros</th>
          </tr>
        </thead>
        <tbody>
          {leaderboard.map((user, index) => (
            <tr key={user.id}>
              <td>{index + 1}</td>
              <td>{user.username}</td>
              <td>{user.hours_studied.toFixed(2)}</td>
              <td>{user.total_pomodoros}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

export default Leaderboard;
```

---

### **8. Best Practices & Optimization**

- **Indexing:** Index `study_sessions(start_time)` for faster date queries.
- **Caching:** For large datasets, cache daily leaderboard results.
- **Timezone Handling:** Store timestamps in UTC, convert to local time as needed.
- **Security:** Authenticate user requests; prevent manipulation.
- **Pagination:** For large leaderboards, implement pagination.

---

### **Summary**

- Collect user study sessions with timestamps and pomodoro counts.
- Aggregate hours and pomodoros daily with SQL queries.
- Provide a REST API to serve leaderboard data.
- Implement a user-friendly front-end to display rankings.

This professional approach ensures reliable, scalable, and maintainable leaderboard functionality suitable for your study app.