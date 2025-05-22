In Supabase, when signing up a new user via the Auth API, you can include custom metadata by passing the `user_metadata` parameter. This allows you to attach custom key-value pairs that will be stored alongside the user record, accessible through the `user_metadata` property in the user object.

### How to set raw user metadata during signup:

**Using the Supabase JavaScript client:**

```js
const { createClient } = require('@supabase/supabase-js');

// Initialize your Supabase client
const supabaseUrl = 'https://your-project.supabase.co'
const supabaseKey = 'public-anonymous-key'
const supabase = createClient(supabaseUrl, supabaseKey);

async function signUpUser(email, password, userMetadata) {
  const { user, session, error } = await supabase.auth.signUp({
    email,
    password,
  }, {
    data: userMetadata // This is where you pass custom metadata
  });

  if (error) {
    console.error('Error during sign up:', error);
  } else {
    console.log('User signed up:', user);
  }
}

// Example usage:
signUpUser('newuser@example.com', 'securePassword123', {
  first_name: 'John',
  last_name: 'Doe',
  role: 'member'
});
```

### Important considerations:
- The second argument to `signUp` can include a `data` object which is stored as `user_metadata`.
- Make sure your Supabase project’s authentication configuration allows `user_metadata` to be set and retrieved.

### Additional notes:
- **Custom metadata cannot contain nested objects:** As per current Supabase behavior, nested objects in `user_metadata` might not serialize properly — stick to flat key-value pairs.
- **After sign-up, you can access `user_metadata` from the user object:**

```js
console.log(user.user_metadata); // { first_name: 'John', last_name: 'Doe', role: 'member' }
```

### Summary:
- Pass a `data` object as the second parameter for `signUp` to include raw metadata.
- Use plain key-value pairs, preferably flat structures.
- Ensure your Supabase settings permit user_metadata to be written.

Let me know if you want a code snippet for server-side signup (using SDKs in other languages) or further customization!