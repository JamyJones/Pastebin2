To include `@supabase/supabase-js` version `2.49.8` in your project's dependencies via `package.json`, follow these steps:

### 1. Using the Command Line

Run this command in your terminal within your project directory:

```bash
npm install @supabase/supabase-js@2.49.8 --save
```

This will add the specified version to your `package.json` dependencies automatically.

### 2. Manually Editing `package.json`

Alternatively, if you prefer to manually add it:

```json
{
  "dependencies": {
    "@supabase/supabase-js": "2.49.8"
  }
}
```

After editing, run:

```bash
npm install
```

to install the dependencies listed in `package.json`.

---

### Additional Tips:
- Ensure your project uses a supported version of Node.js and npm.
- Always prefer specifying exact versions in production to ensure stability.
- Check for updates periodically or pin to specific versions based on your project requirements.

If you're using Yarn, the equivalent command is:

```bash
yarn add @supabase/supabase-js@2.49.8
```