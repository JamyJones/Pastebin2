Choosing the best framework for building a Single Page Application (SPA) using JavaScript depends on your project requirements, scalability needs, and developer preferences. However, three popular frameworks dominate SPA development:

### 1. **React.js** (Library)
   - Maintained by Facebook, React is widely adopted and has a vast ecosystem.
   - Uses a virtual DOM for performance optimization.
   - Component-based architecture with hooks for managing state and effects.
   - Excellent for building interactive and dynamic UIs.

   Example:
   ```javascript
   import React, { useState } from "react";

   function App() {
     const [count, setCount] = useState(0);
     return (
       <div>
         <h1>Counter: {count}</h1>
         <button onClick={() => setCount(count + 1)}>Increment</button>
       </div>
     );
   }

   export default App;
   ```

### 2. **Vue.js** (Framework)
   - Lightweight and approachable with an easy learning curve.
   - Offers two-way data binding and reactive components.
   - Supports both Options API and Composition API.
   - Ideal for medium-sized applications and progressive enhancements.

   Example:
   ```javascript
   <template>
     <div>
       <h1>Counter: {{ count }}</h1>
       <button @click="count++">Increment</button>
     </div>
   </template>

   <script>
   import { ref } from "vue";
   export default {
     setup() {
       const count = ref(0);
       return { count };
     },
   };
   </script>
   ```

### 3. **Angular** (Full-Fledged Framework)
   - Developed by Google with built-in TypeScript support.
   - Includes features like dependency injection, RxJS, and advanced routing.
   - Great for large-scale enterprise applications.
   - Provides a structured approach with modules and services.

   Example:
   ```typescript
   import { Component } from "@angular/core";

   @Component({
     selector: "app-root",
     template: `
       <h1>Counter: {{ count }}</h1>
       <button (click)="increment()">Increment</button>
     `,
   })
   export class AppComponent {
     count = 0;
     increment() {
       this.count++;
     }
   }
   ```

### Conclusion
- If you need flexibility and strong community support, **React** is a great choice.
- If you prefer simplicity and ease of use, **Vue.js** works well.
- For large-scale applications with a structured approach, **Angular** is optimal.

Each framework has its advantages, so consider your project needs before deciding. Do you have any specific requirements for your SPA?