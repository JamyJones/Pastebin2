To include `@supabase/supabase-js` version `2.49.8` as a dependency in your `package.json`, you should do one of the following:

### 1. Using `npm` command:

Run this command in your terminal within your project directory:

```bash
npm install @supabase/supabase-js@2.49.8 --save
```

This will:
- Add the specific version `2.49.8` to your `package.json` under `"dependencies"`.
- Update your `package-lock.json`.

### 2. Manually editing `package.json`

If you prefer to add it directly to `package.json`, open the file and add the dependency:

```json
{
  "dependencies": {
    "@supabase/supabase-js": "2.49.8",
    // ... other dependencies
  }
}
```

Then, run:

```bash
npm install
```

This will ensure your `node_modules` directory is updated with the specified version.

### Best practices:
- Always specify exact versions in production to prevent unexpected updates.
- Use `npm update` or `npm outdated` to manage dependency versions regularly.
- Consider using a `package-lock.json` (which `npm` generates automatically) for consistent installs.

---

**Summary:**

```bash
npm install @supabase/supabase-js@2.49.8 --save
```

or manually:

```json
// package.json
{
  "dependencies": {
    "@supabase/supabase-js": "2.49.8",
    // other dependencies
  }
}
```

Followed by:

```bash
npm install
```

to install the package.