In Supabase, you can set raw metadata when signing up a new user by utilizing the `data` field within the `signUp` method of the Supabase Auth client. The `data` field allows you to store custom user attributes that will be accessible within the `auth.users` table.

Here's an example of how to set raw metadata when signing up a user in Supabase using JavaScript:

```javascript
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = 'https://YOUR_SUPABASE_URL';
const supabaseKey = 'YOUR_ANON_KEY';

const supabase = createClient(supabaseUrl, supabaseKey);

async function signUpUser() {
  const { data, error } = await supabase.auth.signUp({
    email: 'user@example.com',
    password: 'securepassword',
    options: {
      data: {
        role: 'admin',
        preferences: {
          theme: 'dark',
          notifications: true
        }
      }
    }
  });

  if (error) {
    console.error('Error signing up:', error.message);
    return;
  }

  console.log('User signed up:', data);
}

signUpUser();
```

### Explanation:
- `signUp` is used to register a new user.
- The `options` object contains a `data` field where you can store custom metadata.
- In this example, the metadata includes the user’s `role` and `preferences`.
- The data will be stored within the `auth.users` table and can be accessed later.

To retrieve the metadata later, you can query the user's session:

```javascript
const { data: { user } } = await supabase.auth.getUser();
console.log(user.user_metadata);
```

### Best Practices:
1. **Keep metadata minimal**: Avoid storing large objects, as excessive metadata could affect performance.
2. **Ensure security**: Do not store sensitive data (e.g., passwords or API keys) within metadata.
3. **Use structured data**: Keep metadata organized and easy to parse.

This method allows for flexible user management and customization within Supabase. Let me know if you need further clarification!