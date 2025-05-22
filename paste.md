You’d like to create a leaderboard for your study app that displays each student’s daily ranking, total hours studied, and number of Pomodoros completed. Here’s a professional approach covering both front-end and back-end development:

## 1. Database Design

Create a table to store daily study stats:

```sql
CREATE TABLE study_stats (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    date DATE NOT NULL,
    hours_studied DECIMAL(4,2) DEFAULT 0,
    pomodoros_completed INTEGER DEFAULT 0
);
```

## 2. Back-End: API Endpoint

Example using Node.js (Express) and PostgreSQL:

```js
// GET /api/leaderboard?date=YYYY-MM-DD
app.get('/api/leaderboard', async (req, res) => {
  const { date } = req.query;
  const result = await db.query(
    `SELECT u.username, s.hours_studied, s.pomodoros_completed
     FROM study_stats s
     JOIN users u ON s.user_id = u.id
     WHERE s.date = $1
     ORDER BY s.hours_studied DESC, s.pomodoros_completed DESC`,
    [date]
  );
  res.json(result.rows);
});
```

**Best Practices:**
- Use parameterized queries to prevent SQL injection.
- Paginate results if the user base is large.

## 3. Front-End: Displaying the Leaderboard

Example using React:

```jsx
import React, { useEffect, useState } from 'react';

function Leaderboard({ date }) {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch(`/api/leaderboard?date=${date}`)
      .then(res => res.json())
      .then(setData);
  }, [date]);

  return (
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
        {data.map((entry, idx) => (
          <tr key={entry.username}>
            <td>{idx + 1}</td>
            <td>{entry.username}</td>
            <td>{entry.hours_studied}</td>
            <td>{entry.pomodoros_completed}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

**Best Practices:**
- Use semantic HTML for accessibility.
- Handle loading and error states.
- Consider caching leaderboard data for performance.

## 4. Additional Recommendations

- Update study stats in real-time or at regular intervals.
- Allow filtering by date or time range.
- Secure endpoints to prevent unauthorized access.

Would you like a more detailed example for a specific tech stack or additional features?