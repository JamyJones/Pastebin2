## How to Get the Current Date in JavaScript

---

Explanation:

**JavaScript provides built-in classes and methods to work with dates.** To get the current date, you typically use the `Date` object, which represents a single moment in time. The `Date` object is part of JavaScript's core language features and doesn't require any additional libraries.

---

### Creating a Date object for the current date

```javascript
const today = new Date();
```

- **`new Date()`**: This constructor creates a new Date object set to the current date and time according to the system's clock.
- This object, `today`, now stores the precise moment the code was executed.

---

### Extracting Different Parts of the Date

You can extract specific parts of the date, such as the year, month, and day using built-in methods:

```javascript
const year = today.getFullYear(); // 4-digit year, e.g., 2024
const month = today.getMonth() + 1; // Month index starts at 0 (January), so add 1
const day = today.getDate(); // Day of the month
```

- **`getFullYear()`**: Returns the year as a four-digit number.
- **`getMonth()`**: Returns the month as a zero-based index (0 for January, 11 for December); adding 1 makes it more human-readable.
- **`getDate()`**: Gets the day of the month (1-31).

---

### Formatting the Date as a String

To format the date as a string in a common format like `YYYY-MM-DD`:

```javascript
const formattedDate = `${year}-${month.toString().padStart(2, '0')}-${day.toString().padStart(2, '0')}`;
```

- **`padStart(2, '0')`**: Ensures that month and day are always two digits, adding a leading zero when necessary.

---

### Complete Practical Example

```javascript
const today = new Date();
const year = today.getFullYear();
const month = (today.getMonth() + 1).toString().padStart(2, '0');
const day = today.getDate().toString().padStart(2, '0');

const currentDate = `${year}-${month}-${day}`;
console.log(currentDate); // Output: e.g., 2024-04-27
```

This code outputs the current date in `YYYY-MM-DD` format.

---

### References:
## MDN Web Docs - Date ##