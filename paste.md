## JSON Web Token (JWT) and Supabase Database Policy Modification <br>

---

### **Explanation** <br>

**1. What is JWT?** <br>

A **JSON Web Token (JWT)** is a compact, URL-safe means of representing claims to be transferred between two parties. It consists of three parts:

- **Header**: Specifies the type of token (`JWT`) and the algorithm used (e.g., `HS256`).
- **Payload**: Contains the claims, typically including user information like ID and email.
- **Signature**: A hashed value that ensures the token’s integrity and authenticity.

JWTs are commonly used for **authentication** in web applications, allowing users to securely verify their identity without repeatedly submitting credentials.

---

**2. Supabase Policy and Modification** <br>

Supabase uses **Row-Level Security (RLS)** to control access to tables dynamically. In your current policy, authorization is based on the `email` extracted from the JWT using:

```sql
(select auth.jwt()) ->> 'email' = email
```

Since you want the policy to check against the `UserId` column, which stores authenticated user IDs, the modification is simple: replace `email` with `UserId`. The revised policy should look like this:

```sql
create policy "Enable update for users based on UserId"
on "public"."User Profiles"
for update using (
  (select auth.jwt()) ->> 'sub' = UserId
) with check (
  (select auth.jwt()) ->> 'sub' = UserId
);
```

---

### **Explanation of Modification** <br>

**1. `sub` in JWT** <br>
- In Supabase, the `sub` (subject) claim within JWT represents the authenticated user's **UUID (User ID)**, which is better suited for authorization than email.

**2. Column Change** <br>
- The policy now checks that the `UserId` stored in `"public"."User Profiles"` matches the `sub` from the JWT instead of email.
- This ensures that only the authenticated user can update their own profile.

---

### **Example** <br>

Assume the following JWT payload:

```json
{
  "sub": "b12345d6-7890-4abc-def1-234567890ghi",
  "email": "user@example.com",
  "role": "authenticated"
}
```

If `UserId` in `"public"."User Profiles"` is `"b12345d6-7890-4abc-def1-234567890ghi"`, the user will be **allowed** to update their profile. If it doesn’t match, the update will be **denied**.

---

### **References** <br>

## https://supabase.com/docs/guides/auth ##  
## https://jwt.io/introduction ##  

Let me know if you need further refinements! 🚀