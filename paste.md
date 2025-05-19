## How to Get Today’s Date in JavaScript

---

**Explanation:**

JavaScript provides built-in functions and objects to work with dates and times. The most common way to get the current date is by using the `Date` object.

### 1. Using the `Date` Object
- JavaScript’s `Date` constructor creates a new date object representing the current date and time based on the system clock.

### 2. Creating a new Date instance
```javascript
const today = new Date();
```
- This line creates a new date object called `today`.

### 3. Extracting specific parts of the date
You can extract various components of the current date:
- Year: `getFullYear()` — returns the 4-digit year.
- Month: `getMonth()` — returns the month (0-11). Note: January is 0, December is 11.
- Day: `getDate()` — returns the day of the month (1-31).

**Example:**
```javascript
const year = today.getFullYear(); // e.g., 2024
const month = today.getMonth() + 1; // e.g., 4 for April, add 1 since months are zero-indexed
const day = today.getDate(); // e.g., 27
```

### 4. Formatting the date as a string
You can combine the components to display the date in a preferred format:
```javascript
const formattedDate = `${year}-${month.toString().padStart(2, '0')}-${day.toString().padStart(2, '0')}`;
```
- `.padStart(2, '0')` ensures two digits for months and days, adding leading zeros if necessary.

---

**Example: Getting Today's Date in YYYY-MM-DD Format**
```javascript
// Get current date
const today = new Date();

// Extract components
const year = today.getFullYear();
const month = (today.getMonth() + 1).toString().padStart(2, '0');
const day = today.getDate().toString().padStart(2, '0');

// Format date
const currentDate = `${year}-${month}-${day}`;
console.log(currentDate); // e.g., "2024-04-27"
```

---

**References:**  
## MDN Web Docs on Date Object: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date