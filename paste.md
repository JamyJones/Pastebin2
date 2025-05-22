In Supabase, when signing up a new user, you can include custom user metadata—commonly referred to as `user_metadata`—by passing it as part of the `additional fields` parameter during the sign-up process. This metadata is stored within the user object and can hold custom information such as user roles, preferences, or any other application-specific data.

### How to set raw user metadata during signup

#### 1. Using the Supabase JavaScript Client

Suppose you want to sign up a user with email and password and also attach custom metadata, for example, `display_name` and `role`.

```js
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = 'https://your-project.supabase.co';
const supabaseKey = 'public-anonymous-key';
const supabase = createClient(supabaseUrl, supabaseKey);

async function signUpUser(email, password, displayName, role) {
  const { user, session, error } = await supabase.auth.signUp(
    {
      email,
      password,
    },
    {
      data: {
        display_name: displayName,
        role: role,
      },
    }
  );

  if (error) {
    console.error('Error during sign-up:', error);
    return null;
  }
  
  console.log('User signed up:', user);
  return user;
}
```

> **Note:** The `data` object in the second parameter corresponds to `user_metadata`.

#### 2. Using the REST API directly

You can also send a POST request to the `/auth/v1/signup` endpoint with the user data, including `user_metadata` in the request body.

```bash
curl -X POST "https://your-project.supabase.co/auth/v1/signup" \
-H "Content-Type: application/json" \
-H "apikey: your_public_api_key" \
-d '{
  "email": "newuser@example.com",
  "password": "password123",
  "options": {
    "data": {
      "display_name": "John Doe",
      "role": "editor"
    }
  }
}'
```

### Important considerations:
- The `user_metadata` is stored in the `user.user_metadata` object.
- Metadata fields are flexible but best to keep to a predictable schema.
- Sensitive data should **not** be stored in `user_metadata` as it is exposed client-side.

### Best Practices
- Validate the metadata before setting it.
- Remember that `user_metadata` is accessible on the client side, so avoid storing sensitive information there.
- Use server-side functions or security rules if you need to modify metadata after signup or guard the data access.

---

Let me know if you want an example of setting or updating user metadata post-signup or integrating with specific backend functions!