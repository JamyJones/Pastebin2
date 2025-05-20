Creating a user profile system with profile picture uploads using Supabase involves both **database design** and **file storage management**. Here's a step-by-step guide to implement this professionally:

---

### 1. **Database Schema**

Create a `profiles` table to store user profile data, including a reference to the profile picture.

```sql
-- Create a profiles table linked to the auth user
CREATE TABLE profiles (
  id uuid REFERENCES auth.users ON DELETE CASCADE,
  display_name varchar(255),
  profile_image_url varchar(255),
  bio text,
  created_at timestamp with time zone DEFAULT now(),
  PRIMARY KEY (id)
);
```

- `id`: Allows linking directly to Supabase Auth user ID.
- `profile_image_url`: Stores the URL of the uploaded profile picture.

---

### 2. **Frontend: Upload Image and Save Profile**

#### a. **Initialize Supabase Client**

```javascript
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = 'https://your-project.supabase.co';
const supabaseKey = 'public-anonymous-key';
const supabase = createClient(supabaseUrl, supabaseKey);
```

---

#### b. **Handle Image Upload**

```javascript
async function uploadProfilePicture(file) {
  const user = supabase.auth.user();
  if (!user || !file) return null;

  const fileExt = file.name.split('.').pop();
  const fileName = `${user.id}/profile.${fileExt}`;
  const { data, error } = await supabase.storage
    .from('profile-pictures')
    .upload(fileName, file, {
      upsert: true,
    });

  if (error) {
    console.error('Upload error:', error);
    return null;
  }

  // Generate public URL for access
  const { publicURL, error: urlError } = supabase.storage
    .from('profile-pictures')
    .getPublicUrl(fileName);

  if (urlError) {
    console.error('URL fetch error:', urlError);
    return null;
  }

  return publicURL;
}
```

*Note*: Make sure you've created a storage bucket called `'profile-pictures'`.

---

#### c. **Save or Update Profile**

```javascript
async function saveUserProfile({ displayName, bio, file }) {
  const user = supabase.auth.user();

  // Upload image and get its URL
  const profileImageUrl = file ? await uploadProfilePicture(file) : null;

  const { data, error } = await supabase
    .from('profiles')
    .upsert({
      id: user.id,
      display_name: displayName,
      bio: bio,
      profile_image_url: profileImageUrl,
    });

  if (error) {
    console.error('Error saving profile:', error);
  } else {
    console.log('Profile saved:', data);
  }
}
```

---

### 3. **Displaying User Profile**

```javascript
async function getUserProfile() {
  const user = supabase.auth.user();
  const { data, error } = await supabase
    .from('profiles')
    .select('*')
    .eq('id', user.id)
    .single();

  if (error) {
    console.error('Error fetching profile:', error);
    return null;
  }
  return data; // contains display_name, bio, profile_image_url
}
```

---

### 4. **Best Practices**

- **Security**: Set RLS (Row Level Security) policies on your 'profiles' table to ensure users can only access their data.
- **Storage Permissions**: Configure your storage bucket to only allow authenticated users if needed.
- **Error Handling**: Always handle possible errors for both uploads and database operations.
- **Progress Indicators**: Show upload progress during image uploads for better UX.

---

### 5. **Example RLS Policy**

```sql
-- Allow users to see and update their own profile
create policy "Allow users to view their profile" on profiles
for select, update
using (auth.uid() = id);
```

---

This setup provides a secure, scalable, and professional way to link user profiles with profile pictures using Supabase's auth, storage, and database features. You can expand upon this by adding features like avatar cropping, editing profile info, or multiple profile images as needed.