# ✅ 📂 Developer Documentation — `feature/forgot-password`

---

## 1️⃣ Feature Name

`feature/forgot-password` — Complete implementation of a secure **Forgot Password & Reset Password flow** for the Storyvord platform.

---

## 2️⃣ Objective

The goal was to build a robust, secure process that allows any registered user to **safely reset their password** if they forget it — with a smooth, user-friendly flow and full multi-language support.

**How the flow works:**
- User enters their registered email and requests a reset.
- The app sends a secure reset link containing unique tokens.
- The user clicks the link → lands on the **Update Password** page.
- User sets a new password and confirms it.
- If valid, the backend updates the password.
- The user sees a success message and is redirected to **Sign In**.

---

## 3️⃣ Tech Stack

- **React.js** — for the frontend UI
- **Next.js** — for routing and page handling
- **TypeScript** — for type safety
- **React Query** — for handling API calls and mutations
- **Tailwind CSS** — for responsive styling
- **react-hook-form + Zod** — for form handling and strong validation
- **Custom toast component** — for instant user feedback
- **next-intl** — for translations (multi-language)

---

## 4️⃣ Core Structure

- **Forgot Password Page:** UI for users to enter their email and request a reset.
- **Update Password Page:** UI for users to set a new password using the secure link.
- **Reusable PasswordField Component:** Ensures consistency in password inputs.
- **API Layer:** Functions to handle the request and update password calls.
- **React Query Hooks:** Manage mutations and server state.
- **Validation:** Uses Zod schemas to enforce strong password rules.
- **Translations:** All messages and labels are stored in locale JSON files for easy i18n.

---

## 5️⃣ Detailed Flow

### 🔹 Forgot Password Page

- User sees a clean, focused form with:
  - A single **email input**.
  - A clear **submit button**.
- After submission:
  - The app sends the request to the backend.
  - If the email exists, a secure link with a unique `uidb64` and `token` is sent.
  - The user sees a success message.
  - If the email is invalid, an error toast explains what went wrong.
  - On success, the user is redirected to **Sign In**.

---

### 🔹 Update Password Page

- The page automatically extracts `uidb64` and `token` from the URL.
- Shows a form for:
  - New Password (must meet minimum length)
  - Confirm Password (must match exactly)
- Submitting:
  - Validates input on the client.
  - Sends the data to the backend.
  - On success:
    - Displays a success toast with a countdown.
    - After the countdown, redirects the user to **Sign In**.

---

## 6️⃣ API Endpoints (Documented)

- **Request Reset Password:**  
  - **Method:** POST  
  - **Purpose:** Takes user email, checks if it exists, and sends a secure reset link with unique tokens.
  - **Security:** Uses tokens to prevent misuse.

- **Reset Password Complete:**  
  - **Method:** PATCH  
  - **Purpose:** Takes the new password, `uidb64` and `token` to securely update the password in the backend.
  - **Security:** Validates that the link and tokens are valid and unused.

---

## 7️⃣ Validation Rules

- Password must meet minimum security standards (length, format).
- Confirmation must match exactly.
- Server-side and client-side both validate inputs.
- Any mismatch or tampering triggers descriptive errors.

---

## 8️⃣ Translations

- Headings, labels, success toasts, error toasts.
- Structured in `auth.json` for each supported language.
- Covers:
  - Link sent
  - Account not found
  - Password mismatch
  - Password updated successfully

---

## 9️⃣ Problems Faced & Solutions

| Problem | How I Solved It |
|---------|-----------------|
| **Invalid `uidb64` or `token` could be tampered** | ✅ Added guards to detect missing or invalid tokens → redirect user to a safe fallback page. |
| **Password confirmation mismatch** | ✅ Used schema validation (Zod) to ensure the confirm field matches the new password perfectly. |
| **Needing clear user feedback & redirect** | ✅ Built a countdown inside the success toast so users know exactly when they’ll be redirected. |
| **Translations missing for new flows** | ✅ Added missing keys, verified in all languages (English, Hindi, Spanish, etc.). |
| **Form inputs repeated in multiple places** | ✅ Created a reusable `PasswordField` for consistency. |

---

## 🔟 Final Outcome

✅ Secure, end-to-end reset password flow.  
✅ Strong validation both client & server-side.  
✅ Fully internationalized.  
✅ User-friendly with clear feedback.  
✅ Production-ready structure with reusable, maintainable components.

---

## 🌐 How to See It Live

To test:
1️⃣ Open → [https://dev.storyvord.io/auth/forget-password](https://dev.storyvord.io/auth/forget-password)  
2️⃣ Create an account first if you don’t have one.  
3️⃣ Request a reset link → check your inbox → click the link → update your password → watch the flow complete with redirect.

---

**🔒 Note:**  
This documentation is public but does not expose any private source code — only the full flow, structure, and developer choices to explain **how** it works in practice.
