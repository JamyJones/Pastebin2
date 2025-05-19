## Creating a User Profile in Supabase <br>
---

### **Understanding the Code** <br>
This code snippet is an **asynchronous function** named `createUserProfile` that inserts a user profile into a Supabase database table named `profile`. Below is a detailed breakdown of how it works.

---

#### **1. Function Definition & Parameters** <br>
```javascript
async function createUserProfile(userId, name) {
```
- **`async`**: Declares the function as asynchronous, allowing the use of `await` for handling promises.
- **`userId` and `name`**: These parameters are passed when the function is called, representing the user's unique ID and their name.

---

#### **2. Inserting Data into Supabase** <br>
```javascript
const { data, error } = await supabase
  .from('profile')
  .insert([
    { user_id: userId, name: name, streak_hours: 0, last_seen: new Date().toISOString() }
  ]);
```
- **`supabase.from('profile')`**: Specifies the table to interact with (`profile`).
- **`.insert([...])`**: Inserts a new row into the table, structured as an object:
  - `user_id: userId` → Stores the user ID.
  - `name: name` → Stores the user's name.
  - `streak_hours: 0` → Initializes a streak counter at **0**.
  - `last_seen: new Date().toISOString()` → Sets the current timestamp in ISO format.

---

#### **3. Handling Errors & Logging Results** <br>
```javascript
if (error) console.error(error);
else console.log('Profile created:', data);
```
- **Error Handling**:
  - If `error` exists, it is logged to the console (`console.error(error);`).
  - Otherwise, `data` (the response from Supabase) is logged (`console.log('Profile created:', data);`).

---

### **Example Usage** <br>
```javascript
createUserProfile('user_123', 'Alice');
```
**Expected Output (if successful):**
```
Profile created: [ { user_id: 'user_123', name: 'Alice', streak_hours: 0, last_seen: '2025-05-19T18:42:00.000Z' } ]
```
**Error Output (if something goes wrong):**
```
Error: [Supabase error message]
```
---

### **Key Takeaways**
- This function **automatically** inserts user profiles into Supabase.
- **Error handling** ensures issues are reported.
- **`async` and `await`** enable smooth asynchronous data handling.
- The **timestamp** field (`last_seen`) updates dynamically.

Let me know if you need modifications or further explanations! 🚀