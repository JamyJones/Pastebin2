In JavaScript, you can convert a string to an integer or a number using several methods. Here are some common approaches:

1. **Using `parseInt()`**:
   The `parseInt()` function parses a string and returns an integer. You can also specify the radix (base) for the conversion.

   ```javascript
   let str = "123";
   let num = parseInt(str, 10); // 10 is the radix for decimal
   console.log(num); // Output: 123
   ```

2. **Using `Number()`**:
   The `Number()` function converts a string to a number. If the string cannot be converted, it returns `NaN`.

   ```javascript
   let str = "123.45";
   let num = Number(str);
   console.log(num); // Output: 123.45
   ```

3. **Using the unary plus operator (`+`)**:
   You can use the unary plus operator to convert a string to a number.

   ```javascript
   let str = "123";
   let num = +str;
   console.log(num); // Output: 123
   ```

4. **Using `parseFloat()`**:
   If you want to convert a string to a floating-point number, you can use `parseFloat()`.

   ```javascript
   let str = "123.45";
   let num = parseFloat(str);
   console.log(num); // Output: 123.45
   ```

5. **Using `Math.floor()` or `Math.ceil()`**:
   If you want to convert a string to an integer and round it down or up, you can use `Math.floor()` or `Math.ceil()` after converting it to a number.

   ```javascript
   let str = "123.45";
   let num = Math.floor(Number(str)); // Rounds down
   console.log(num); // Output: 123
   ```

Choose the method that best fits your needs based on whether you want an integer or a floating-point number.