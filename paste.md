In a JSX module, you can import `ReactDOM` from the `react-dom` package using the `import` statement. This is typically required when rendering React components into the DOM. Here’s how you do it:

```jsx
import ReactDOM from 'react-dom';

// Example of rendering a React component
import App from './App'; // Assuming App.jsx exists

ReactDOM.render(<App />, document.getElementById('root'));
```

### **Key Points:**
- The `ReactDOM.render()` method is used to render React components into the DOM.
- The first argument is the React element (`<App />`), and the second argument is the DOM node where the component should be mounted.
- Ensure your project has `react-dom` installed, which is typically included when you install React.

### **React 18 Update**
In React 18, `ReactDOM.render()` is deprecated in favor of `ReactDOM.createRoot()`:

```jsx
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

This method improves rendering performance and enables concurrent features in React.

Let me know if you need further clarification!