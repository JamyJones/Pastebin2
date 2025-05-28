In JavaScript, the `switch` statement allows you to execute different blocks of code based on the value of an expression. It provides a clear way to handle multiple conditional branches based on a single variable or expression.

### Basic Structure of a `switch` Statement

```javascript
switch (expression) {
  case value1:
    // code to execute if expression === value1
    break;
  case value2:
    // code to execute if expression === value2
    break;
  default:
    // code to execute if no case matches
}
```

### Flow of Execution

1. **Evaluate the expression:** The expression inside `switch` is evaluated once.
2. **Compare with case values:** The value of the expression is compared (using strict equality `===`) to each `case` value.
3. **Matching case:** When a match is found:
   - The code within that `case` block executes.
   - If there is no `break`, execution **flows through** to the subsequent cases (called *fall-through behavior*).
   - If a `break` (or other terminating statement like `return`) is encountered, the `switch` statement terminates.
4. **No matching case:** If no `case` matches, the `default` block is executed (if provided).
5. **End of switch:** Once a `break` or termination occurs, control transfers outside the `switch` block.

### Example with Explanation

```javascript
let fruit = 'apple';

switch (fruit) {
  case 'banana':
    console.log('Banana is yellow.');
    break;  // Exit after this block
  case 'apple':
    console.log('Apple is red.');
    // No break here, so execution will fall through to the next case
  case 'pear':
    console.log('Pear is green.');
    break;
  default:
    console.log('Unknown fruit.');
}
```

**Output:**

```
Apple is red.
Pear is green.
```

**Explanation:**  
- The `fruit` is `'apple'`, so the second case matches.
- It logs `'Apple is red.'`.
- Since there's no `break` after `'apple'`, it falls through to the next case (`'pear'`) and logs `'Pear is green.'`.
- The `break` after `'pear'` terminates the switch.

---

### Summary of key points:

- Use `break` to prevent fall-through.
- Remove `break` intentionally if you want multiple cases to execute.
- The comparison is strict (`===`).
- The `default` case is optional but useful for handling unmatched cases.

---

If you'd like, I can provide more complex examples or discuss advanced topics like grouping cases, fall-through techniques, or using switch with different data types.