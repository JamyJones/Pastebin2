## Summary
**Understanding JWT and modifying Supabase database policy to use UserId for authentication checks**

---

### What is JWT?

**JWT (JSON Web Token)** is a compact, URL-safe means of representing claims between two parties. It is widely used for authentication and authorization purposes in modern web applications:

- Composed of **three parts**: Header, Payload, and Signature
- **Header** specifies the token type and signing algorithm
- **Payload** contains the claims, such as user identity and permissions
- **Signature** ensures the token's integrity, created using the header and payload with a secret or private key

**JWTs** are issued by an authentication server after login and can be passed with each request, allowing stateless verification of user identity.

---

### Modifying Supabase Policy to use UserId Instead of Email

Supabase policies use PostgreSQL functions like `auth.jwt()` to extract information from the JWT token. Your current policy checks the email:

```sql
select auth.jwt() ->> 'email'
```

You want to **modify it to use "UserId"** (which is the primary key), assuming the JWT contains a claim like `"sub"` or `"UserId"` representing the user identity. Typically, in JWT standards:

- The claim `"sub"` (subject) is used to store the user ID or principal
- Alternatively, custom claims can be added and checked

---

### Revised Policy Using "UserId"

Assuming the JWT contains a claim `"sub"` with the user ID matching `UserId`, the policy should be:

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update
using (
  (select auth.jwt()) ->> 'sub' = UserId
)
with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

---

### Explanation:

- **Policy Name**: Changed to reflect usage of UserId.
- **`using`**: Allows the update if the `sub` claim matches the `UserId` in the table.
- **`with check`**: Ensures the user can only update their own profile.

---

### Important Notes:
- Make sure **`auth.jwt()`** is correctly configured and includes the **`sub`** claim.
- If your JWT uses a different claim like `"UserId"` directly instead of `"sub"`, replace `'sub'` with `'UserId'`.
- Confirm the JWT payload contains the necessary claim by decoding your token or inspecting it in your auth setup.

---

### References:
##https://supabase.com/docs/auth/auth-helpers/postgrest#policies-and-permissions  
##https://datatracker.ietf.org/doc/html/rfc7519 (JWT Standard Claims)