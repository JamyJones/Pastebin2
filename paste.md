In Supabase, you can set raw metadata for a new user during signup using the `data` field in the `auth.signUp` method. This metadata is stored in the `auth.users` table under the `raw_user_meta_data` column.

### Example: Setting Raw Metadata During Signup
Here’s how you can do it using Supabase's JavaScript client:

```javascript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient('https://your-project-ref.supabase.co', 'your-anon-key');

async function signUpUser() {
    const { data, error } = await supabase.auth.signUp({
        email: 'newuser@example.com',
        password: 'strongpassword',
        options: {
            data: {
                first_name: 'John',
                last_name: 'Doe',
                role: 'user',
                subscribed: true
            }
        }
    });

    if (error) {
        console.error('Error signing up:', error);
    } else {
        console.log('User signed up successfully:', data);
    }
}

signUpUser();
```

### Explanation:
- The `options.data` object allows you to store custom metadata for the user.
- Metadata is saved in the `auth.users` table under `raw_user_meta_data`.
- This data remains accessible whenever you fetch the user's session or profile.

#### Best Practices:
- Always validate metadata before storing it to prevent unwanted or incorrect data.
- Consider restricting metadata updates to authenticated users only.
- Avoid storing sensitive information in metadata fields.

Would you like a follow-up on retrieving or updating this metadata later?