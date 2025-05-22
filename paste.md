In Supabase, when signing up a new user, you can set raw metadata by including it in the `data` parameter while calling the `signUp` method from the Supabase authentication client. This metadata is stored in the `raw_user_meta_data` field.

Here's an example using Supabase's JavaScript client:

```javascript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient('YOUR_SUPABASE_URL', 'YOUR_SUPABASE_ANON_KEY');

async function signUpUser(email, password, metadata) {
  const { data, error } = await supabase.auth.signUp({
    email,
    password,
    options: {
      data: metadata,  // Set custom metadata
    },
  });

  if (error) {
    console.error('Error signing up:', error.message);
  } else {
    console.log('User signed up successfully:', data.user);
  }
}

const metadata = { role: 'admin', preferences: { theme: 'dark' } };
signUpUser('test@example.com', 'securepassword', metadata);
```

### Explanation:
- The `signUp` method accepts user credentials along with an `options` parameter.
- The `options` object includes a `data` field where raw metadata can be stored.
- The metadata provided (e.g., user role, preferences) will be saved in Supabase's `raw_user_meta_data` field.

After user signup, you can retrieve this metadata using:

```javascript
const { data: user } = await supabase.auth.getUser();
console.log(user.user_metadata);
```

### Best Practices:
- Store only necessary metadata to avoid bloating the user's profile.
- Avoid storing sensitive information in raw metadata, as it may be accessible to the frontend.
- Ensure metadata follows a structured format for easier retrieval and processing.

Would you like guidance on updating metadata after user signup?