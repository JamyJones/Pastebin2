To include `@supabase/supabase-js` version `v2.49.8` as a dependency in your project, you need to specify it in your `package.json` file under the `dependencies` section.

### Step-by-step instructions:

1. **Using npm (recommended if your project uses npm):**

Run the following command in your project directory:

```bash
npm install @supabase/supabase-js@2.49.8 --save
```

This will:
- Add `@supabase/supabase-js` with version `2.49.8` to your `package.json` dependencies.
- Install it into your `node_modules` directory.

2. **Manually add to `package.json`:**

Alternatively, you can manually add it under `dependencies`:

```json
{
  "dependencies": {
    "@supabase/supabase-js": "2.49.8",
    // other dependencies...
  }
}
```

Then run:

```bash
npm install
```

### Example of `package.json` snippet:

```json
{
  "name": "your-project-name",
  "version": "1.0.0",
  "dependencies": {
    "@supabase/supabase-js": "2.49.8"
  }
}
```

### Summary:

- Use `npm install @supabase/supabase-js@2.49.8 --save` for automatic update.
- Or manually specify the version in `package.json` and then run `npm install`.

---

### Bonus:

If you're using yarn, the equivalent command is:

```bash
yarn add @supabase/supabase-js@2.49.8
```

This will automatically update your `package.json`.