To import `ReactDOM` from the `react-dom` package in a JSX module, you can use the following syntax:

```javascript
import ReactDOM from 'react-dom';
```

This line of code should be placed at the top of your JSX file. After importing, you can use `ReactDOM` to render your React components into the DOM. For example:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

const App = () => {
    return <h1>Hello, World!</h1>;
};

ReactDOM.render(<App />, document.getElementById('root'));
```

In this example, the `App` component is rendered into the DOM element with the ID of `root`. Make sure that you have the `react` and `react-dom` packages installed in your project.