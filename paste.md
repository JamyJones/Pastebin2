Certainly! Here's a complete `package.json` for a standard React application. This setup includes the essential dependencies, scripts, and configurations commonly used in a React project created with Create React App or a similar setup.

```json
{
  "name": "react-app",
  "version": "1.0.0",
  "private": true,
  
  "scripts": {
    "start": "react-scripts start",           // Runs the app in development mode
    "build": "react-scripts build",           // Builds the app for production
    "test": "react-scripts test",             // Runs the test runner
    "eject": "react-scripts eject"            // Ejects configuration (optional)
  },

  "dependencies": {
    "react": "^18.2.0",                        // React core library
    "react-dom": "^18.2.0",                    // React DOM library
    "react-scripts": "^5.0.1"                  // Scripts and configuration for Create React App
  },

  "devDependencies": {
    "eslint": "^8.1.0"                         // Linting for code quality (optional but recommended)
  },

  "browserslist": [
    ">0.2%",
    "not dead",
    "not op_mini all"
  ],

  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  }
}
```

### Explanation:
- **name & version**: Basic metadata.
- **private**: Prevents accidental publication to npm registry.
- **scripts**:
  - `start`: Runs development server.
  - `build`: Creates an optimized production build.
  - `test`: Runs tests.
  - `eject`: Exposes configuration files (`use with caution`).
- **dependencies**:
  - `react` and `react-dom`: Core React libraries.
  - `react-scripts`: Development scripts provided by Create React App.
- **devDependencies**:
  - `eslint`: To maintain code quality.
- **browserslist**: Specifies target browsers for compatibility.
- **eslintConfig**: Default ESLint configuration extended from React app presets.

### How to Use:
1. Save this `package.json` in your project root.
2. Run `npm install` (or `yarn install` if you prefer Yarn).

---
If you're just starting out, I recommend using [Create React App](https://create-react-app.dev/) which automatically generates this package.json and more boilerplate for you with `npx create-react-app my-app`.

Let me know if you'd like guidance on how to set up the project from scratch or other configurations!