## Logging in a User with Supabase JavaScript Client and Setting Redirect URL <br>
---
### **Using Supabase Authentication for Login** <br>
Supabase provides authentication methods that allow users to log in using email/password or third-party providers. The JavaScript client includes a `signIn` method that supports redirecting users after authentication.

---
### **Setting Up Redirect URLs** <br>
When using Supabase authentication, you can specify a redirect URL using the `redirectTo` parameter. By default, users are redirected to the `SITE_URL` configured in Supabase settings, but you can modify this behavior.

---
### **Implementation in JavaScript** <br>
To log in a user and set a redirect URL, use the following code:

```javascript
import { createClient } from '@supabase/supabase-js';

// Initialize Supabase client
const supabaseUrl = 'https://your-project.supabase.co';
const supabaseKey = 'your-anon-key';
const supabase = createClient(supabaseUrl, supabaseKey);

// Function to log in user with email and password
async function loginUser(email, password) {
    const { user, error } = await supabase.auth.signInWithPassword({
        email,
        password
    });

    if (error) {
        console.error('Login failed:', error.message);
        return;
    }

    console.log('User logged in:', user);
}

// Function to log in user with OAuth provider and redirect
async function loginWithProvider(provider) {
    const { error } = await supabase.auth.signInWithOAuth({
        provider,
        options: {
            redirectTo: 'https://your-redirect-url.com/dashboard'
        }
    });

    if (error) {
        console.error('Login failed:', error.message);
    }
}

// Example usage
loginUser('user@example.com', 'password123');
loginWithProvider('google');
```

---
### **Explanation of Code** <br>
- **Import Supabase Client**: The `createClient` function initializes the Supabase client with the project URL and API key.
- **Login with Email/Password**: The `signInWithPassword` method authenticates users using their credentials.
- **Login with OAuth Provider**: The `signInWithOAuth` method allows users to log in via third-party providers (Google, GitHub, etc.).
- **Redirect URL**: The `redirectTo` parameter ensures users are redirected to a specified page after authentication.

---
### **Configuring Redirect URLs in Supabase** <br>
To allow redirects, you must configure the allowed URLs in Supabase:
1. Go to **Supabase Dashboard** → **Authentication** → **Settings**.
2. Set the **SITE_URL** to your main application URL.
3. Add additional redirect URLs under **Additional Redirect URLs**.

---
### **Example Scenario** <br>
If your application is hosted at `https://myapp.com`, and you want users to be redirected to `/dashboard` after login:
- Set `SITE_URL` to `https://myapp.com`
- Add `https://myapp.com/dashboard` to **Additional Redirect URLs**
- Use `redirectTo: 'https://myapp.com/dashboard'` in your authentication request.

---
### **References** <br>
## https://supabase.com/docs/guides/auth/redirect-urls ##
## https://stackoverflow.com/questions/69401106/how-to-handle-redirect-from-supabase-signin ##
## https://github.com/orgs/supabase/discussions/6088 ##
