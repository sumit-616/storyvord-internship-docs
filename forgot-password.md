# ✅ 📂 Documentation — feature/forgot-password

---

## 1️⃣ Feature Name

`feature/forgot-password` — Implementation of the Forgot Password & Reset Password functionality.

---

## 2️⃣ Objective

The goal was to let a user reset their password securely if they forget it.

**Flow:**

- User enters their registered email → app sends them a reset link with `uidb64` & `token`.
- User clicks the link → lands on Update Password page.
- User sets new password + confirms it → backend validates & updates password.
- User sees success toast + redirect to Sign In page.

---

## 3️⃣ Tech Stack

- React.js (client rendering)
- Next.js (`useRouter`, `useSearchParams` for routing)
- TypeScript
- React Query (`useMutation` for API calls)
- Tailwind CSS (styling)
- react-hook-form + Zod (form validation)
- use-toast (custom toast component)
- i18n (`next-intl`) for translation

---

## 4️⃣ Key Files

```
/src/app/auth/forget-password/page.tsx → ForgetPassword page  
/src/app/auth/update-password/page.tsx → UpdatePassword page  
/src/lib/api/auth/auth.ts → API functions: requestResetPassword + resetPasswordComplete  
/src/lib/react-query/queriesAndMutations/auth/auth.ts → React Query hooks  
/src/lib/validation/auth.ts → Zod schema for UpdatePasswordFormData  
/src/components/auth/PasswordField.tsx → Reusable input field for passwords  
/src/i18n/locales/*/auth.json → Translation strings for multi-language  
```

---

## 5️⃣ Detailed Flow

### 🔹 ForgetPassword Page

- Displays a form with:
  - Email input (`<Input />` component)
  - Submit button (`<Button />`)

- Uses React Query Mutation (`useResetPasswordRequest`) for `requestResetPassword`:

```ts
export const useResetPasswordRequest = () => {
  return useMutation({
    mutationFn: (email: string) => requestResetPassword(email),
  });
};
```

- **On submit:**
  1. Calls the mutation → backend sends reset link to email.
  2. Shows success toast:

  ```ts
  toast({
    title: t("toast.success.title"),
    description: t("toast.success.description"),
  });
  ```

  3. Redirects to `/auth/sign-in` on success.
  4. Handles error toast if email is invalid.

---

### 🔹 UpdatePassword Page

- Extracts `uidb64` & `token` from URL using `useSearchParams`:

```ts
const uidb64 = searchParams.get("uidb64");
const token = searchParams.get("token");
```

- Uses react-hook-form + Zod for:
  - `newPassword` → min 8 chars.
  - `confirmPassword` → must match `newPassword`.

- **On submit:**
  1. Calls `resetPasswordComplete` API:

  ```ts
  await resetPasswordComplete({
    password: data.newPassword,
    token,
    uidb64,
  });
  ```

  2. Shows success toast with countdown:

  ```ts
  let countdown = 5;
  const interval = setInterval(() => {
    countdown -= 1;
    // Update toast with remaining seconds
  }, 750);
  ```

  3. After countdown → redirect to `/auth/sign-in`.

---

## 6️⃣ APIs Used

- `POST /accounts/v2/request-reset-password/`  
  - Body: `{ email }`  
  - Response: email sent → backend handles OTP & link.

- `PATCH /accounts/v2/reset-password-complete/`  
  - Body: `{ password, token, uidb64 }`  
  - Updates password in backend.

---

## 7️⃣ Validation & Forms

**Zod Schema:**

```ts
export const updatePasswordSchema = z
  .object({
    newPassword: z.string().min(8),
    confirmPassword: z.string().min(8),
  })
  .refine((data) => data.newPassword === data.confirmPassword, {
    message: "Passwords do not match",
    path: ["confirmPassword"],
  });
```

**Form Hook:**

```ts
const { register, handleSubmit } = useForm<UpdatePasswordFormData>({
  resolver: zodResolver(updatePasswordSchema),
});
```

---

## 8️⃣ Translations

- `forgotPasswordSection` in `auth.json` → heading, description, labels.
- Toast messages for:
  - Link sent ✅
  - Account not found ❌
  - Password updated successfully ✅
  - Mismatch error ❌

---

## 9️⃣ Challenges & How I Tackled Them

- **Problem:** Handling invalid `uidb64` or `token` → user could hit `/update-password` directly.  
  ✅ **Solution:** Added `useEffect` to check params → redirect to `/error` if missing.

- **Problem:** Form field mismatch.  
  ✅ **Solution:** Used Zod `refine` to enforce match.

- **Problem:** Toast auto-redirect with countdown.  
  ✅ **Solution:** Wrote a `setInterval` loop to update toast every second → clear interval → push to Sign In page.

---

## 1️⃣0️⃣ Final Outcome

- Fully functional forgot password & update password system.
- Secure, validated, user-friendly.
- Multi-language ready.
- Clean reusable components (`PasswordField`).
- Fully styled with Tailwind.
- Reusable API hooks with React Query.

---

## 🌐 Demonstration

To test this feature:
1. Go to: [https://dev.storyvord.io/auth/forget-password](https://dev.storyvord.io/auth/forget-password)
2. **Create an account** first to receive the reset link.
3. Use the flow to request a reset, click the email link, and update your password.

---
