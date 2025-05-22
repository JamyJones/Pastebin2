In Supabase, you can set raw metadata for a new user during signup by using the `data` parameter in the `signUp` function. Supabase allows you to pass custom metadata as part of the user's profile, which can then be retrieved later.

Here's an example using Supabase's JavaScript client:

```javascript
import { createClient } from '@supabase/supabase-js';

// Initialize Supabase client
const supabase = createClient('https://your-project-url.supabase.co', 'your-public-anon-key');

async function signUpUser(email, password) {
  const { data, error } = await supabase.auth.signUp({
    email,
    password,
    options: {
      data: {
        role: 'admin', // Custom metadata
        preferences: {
          theme: 'dark',
        },
      },
    },
  });

  if (error) {
    console.error('Error signing up:', error.message);
  } else {
    console.log('User signed up:', data);
  }
}

signUpUser('user@example.com', 'securepassword');
```

### Explanation:
- The `data` parameter inside `options` allows you to store custom user metadata.
- In this example, metadata includes `role` and `preferences`, which can be accessed later.
- Ensure your Supabase project's authentication settings allow custom metadata storage.

Later, you can retrieve the metadata using `supabase.auth.getUser()`:

```javascript
async function getUserMetadata() {
  const { data, error } = await supabase.auth.getUser();

  if (error) {
    console.error('Error fetching user:', error.message);
  } else {
    console.log('User metadata:', data.user?.user_metadata);
  }
}

getUserMetadata();
```

Would you like a more detailed breakdown or additional considerations for securing metadata?