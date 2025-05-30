Certainly! Below is a complete `package.json` file for a standard React application. This configuration includes common dependencies and scripts that are typically used in a React project.

```json
{
  "name": "my-react-app",
  "version": "1.0.0",
  "private": true,
  "homepage": ".",
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "react-scripts": "5.0.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
```

### Explanation of Key Sections:

- **name**: The name of your application.
- **version**: The version of your application.
- **private**: If set to true, it prevents accidental publication to the npm registry.
- **homepage**: The URL of your app's homepage.
- **dependencies**: Lists the packages your app depends on. Here, `react`, `react-dom`, and `react-scripts` are included.
- **scripts**: Defines commands that can be run using `npm run <script-name>`. Common scripts include:
  - `start`: Starts the development server.
  - `build`: Builds the app for production.
  - `test`: Runs the test suite.
  - `eject`: Ejects the configuration for customization.
- **eslintConfig**: Configuration for ESLint, which helps in maintaining code quality.
- **browserslist**: Specifies which browsers your app supports.

### How to Use:

1. Create a new directory for your React app.
2. Navigate to that directory in your terminal.
3. Create a file named `package.json` and copy the above content into it.
4. Run `npm install` to install the dependencies.

This will set up a basic React application structure for you!