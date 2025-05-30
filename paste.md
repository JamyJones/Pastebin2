The `createRoot()` method is part of the React 18 API, which introduced concurrent features and a new root API for rendering. If you are missing `createRoot()` in your `ReactDOM` class, it could be due to a few reasons:

1. **React Version**: Ensure that you are using React 18 or later. You can check your React version in your `package.json` file or by running the following command in your project directory:

   ```bash
   npm list react
   ```

   If you are using an older version, you will need to upgrade React and ReactDOM to version 18 or later:

   ```bash
   npm install react@latest react-dom@latest
   ```

2. **Import Statement**: Make sure you are importing `ReactDOM` correctly. The import statement should look like this:

   ```javascript
   import ReactDOM from 'react-dom/client';
   ```

   Note that `createRoot()` is available in the `react-dom/client` package, not in the main `react-dom` package.

3. **TypeScript Definitions**: If you are using TypeScript, ensure that your type definitions are up to date. You may need to install the latest types for React:

   ```bash
   npm install @types/react @types/react-dom
   ```

4. **Build Configuration**: If you are using a build tool (like Webpack or Babel), ensure that your configuration is set up to handle the latest JavaScript features and React 18.

If you have checked all of the above and are still facing issues, please provide more details about your setup, and I can help you troubleshoot further.