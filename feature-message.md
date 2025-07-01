# ✅ 📂 Developer Documentation — `feature/message` (Messaging Section)

---

## 1️⃣ Feature Name

`feature/message` — Responsive enhancements and layout improvements for the **Chat/Messaging UI** in the Storyvord platform.

---

## 2️⃣ Objective

This feature focused on making the **chat window and messaging experience** fully responsive, intuitive, and adaptable across all device sizes.  
**Key goals:**
- Allow users to **toggle the conversation list** on small screens for better usability.
- Improve the spacing and alignment of the **Chat Header**.
- Dynamically adjust the layout based on the **navbar’s height** and screen breakpoints.
- Ensure smooth resizing and prevent layout overlaps or jumps.

---

## 3️⃣ Tech Stack

- **React.js** — reusable component-based structure
- **Next.js** — page rendering and routing
- **TypeScript** — strict type safety for props and state
- **Tailwind CSS** — modern responsive styling
- **react-icons** — for icons like the hamburger menu and profile icon
- **React Hooks** (`useEffect`, `useState`) — for window resize tracking and layout calculations

---

## 4️⃣ Core Structure

```
/src/components/message/ChatHeader.tsx   → The chat header: profile, toggle, receiver info  
/src/components/message/ChatWindow.tsx   → The main chat container: handles layout & toggles  
/src/components/user-dashboard/dashboard/DashboardNavbar.tsx → Navbar ID for dynamic height calculations
```

---

## 5️⃣ Detailed Flow

### ✅ **ChatHeader Component**

- Displays the **receiver’s profile name** and **online/offline status dot**.
- Includes a **hamburger menu icon** to toggle the conversation list on smaller screens.
- Accepts a prop `isConversationListVisible`:
  - Controls whether the toggle icon appears.
  - Adjusts spacing (`gap`) based on whether the list is open or closed.
- Uses **Tailwind CSS conditional classes** for responsive spacing and clean alignment.

---

### ✅ **ChatWindow Component**

- Acts as the **parent container** for the entire chat section.
- Manages:
  - `isConversationListVisible` — shows/hides the conversation list.
  - `navbarHeight` — tracks the dynamic height of the navbar.
  - `extraVH` — extra viewport height factor for smoother scaling.
- Uses `useEffect` hooks to:
  - Listen for window resize and auto-toggle the conversation list based on screen width.
  - Calculate and update `navbarHeight` by targeting the element with `id="navbar"`.
  - Parse Tailwind config breakpoints to adjust `extraVH` for different screen widths.
- Applies dynamic `minHeight` to ensure the chat window never overlaps the navbar.

---

### ✅ **Dashboard Navbar**

- Minor update:
  - Added `id="navbar"` so that `ChatWindow` can read its height dynamically.
  - Keeps layout calculations robust as the navbar height changes across devices.

---

## 6️⃣ Challenges & How I Solved Them

| Problem | How It Was Solved |
|---------|--------------------|
| **Conversation list toggle failed on window resize** | Added a `window.resize` listener with `useEffect` to automatically adjust `isConversationListVisible`. |
| **Header spacing looked broken when toggling the list** | Used Tailwind’s conditional class logic to change `gap` based on the toggle state. |
| **Main chat window overlapped with the navbar** | Pulled dynamic navbar height using `document.getElementById` and subtracted it in the layout’s `minHeight` style. |
| **Unexpected layout jumps while resizing** | Implemented `extraVH` logic that uses breakpoints to smooth out the container’s scaling. |

---

## 7️⃣ Final Outcome

✅ A **responsive**, mobile-friendly chat and messaging UI.  
✅ Seamless toggle for conversation list on smaller screens.  
✅ Consistent header alignment regardless of toggle state.  
✅ Robust layout that auto-adjusts to navbar changes.  
✅ Clean, maintainable, modular component structure.

---

## 🌐 Demonstration

To test this feature:
- Visit → [https://dev.storyvord.io/dashboard/message](https://dev.storyvord.io/dashboard/message)
- Make sure you’re **logged in** to see the messaging section.
- Try resizing your browser window or using a mobile device:
  - Open and close the conversation list.
  - Observe header spacing and how the chat container adapts smoothly.

---

**🔒 Note:**  
This documentation clearly explains the **feature’s purpose, architecture, user flow, challenges, and solutions** — without exposing any private or sensitive source code.  
It serves as a **professional record** of the development approach and best practices for future reference and team knowledge sharing.
