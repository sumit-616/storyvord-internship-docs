# ✅ 📂 Developer Documentation — feature/network

---

## 1️⃣ Feature Name

`feature/network` — Enhancements and fixes to the chat/messaging UI, improving responsive layouts, conversation list toggling, and header behavior.

---

## 2️⃣ Objective

To make the chat section fully responsive and user-friendly:
- Toggling the conversation list on small screens.
- Improving spacing and alignment of the **Chat Header**.
- Ensuring layout adapts dynamically to screen sizes.
- Adding logic to handle navbar height and viewport scaling.

---

## 3️⃣ Tech Stack

- React.js (component structure)
- Next.js (rendering)
- TypeScript
- Tailwind CSS (responsive styling)
- `react-icons` (UI icons)
- Dynamic layout calculations using `useEffect` hooks

---

## 4️⃣ Key Files

```
/src/components/message/ChatHeader.tsx → Chat header UI  
/src/components/message/ChatWindow.tsx → Main chat container with conversation list logic  
/src/components/user-dashboard/dashboard/DashboardNavbar.tsx → Navbar updated with ID for layout logic  
```

---

## 5️⃣ Detailed Flow

### 🔹 ChatHeader Component

- Added new prop: `isConversationListVisible` to control layout on small screens.
- Adjusted **hamburger menu icon**:
  - Only shows if `isConversationListVisible` is `false` (for toggling).
- Updated header spacing:
  ```tsx
  <div className={`flex relative pb-2 bg-white p-3 sm:gap-0 ${isConversationListVisible ? 'gap-0' : 'gap-6'}`}>
  ```
- Updated profile icon + receiver name display:
  ```tsx
  <CgProfile className="w-9 h-9 text-gray-500" />
  <h1 className="w-full pl-3 sm:pl-2 font-poppins-semibold text-lg flex items-center gap-2">
    {receiverName} <span className={`inline-block w-2 h-2 rounded-full ${isReceiverOnline ? "bg-green-500" : "bg-gray-400"}`}></span>
  </h1>
  ```

---

### 🔹 ChatWindow Component

- New **state**: `isConversationListVisible` to manage list toggle.
- Added `useEffect` to set `isConversationListVisible` based on window width:
  ```ts
  useEffect(() => {
    const updateVisibility = () => setIsConversationListVisible(window.innerWidth >= 640);
    updateVisibility();
    window.addEventListener("resize", updateVisibility);
    return () => window.removeEventListener("resize", updateVisibility);
  }, []);
  ```
- New logic to handle **navbar height** and **extra viewport scaling**:
  ```ts
  useEffect(() => {
    const navbar = document.getElementById("navbar");
    if (navbar) {
      setNavbarHeight(navbar.offsetHeight);
    }
    // Get breakpoints from Tailwind config
    const screens = tailwindConfig.theme?.extend?.screens ?? {};
    const md = parseInt(screens.md.replace("px", ""));
    const lg = parseInt(screens.lg.replace("px", ""));
    const updateExtraVH = () => {
      const width = window.innerWidth;
      if (width < md) setExtraVH(1.5);
      else if (width >= md && width <= lg) setExtraVH(1.7);
      else setExtraVH(1.2);
    };
    updateExtraVH();
    window.addEventListener("resize", updateExtraVH);
    return () => window.removeEventListener("resize", updateExtraVH);
  }, []);
  ```
- Applied **dynamic minHeight** to main container:
  ```tsx
  <main
    className="flex overflow-y-hidden overflow-x-auto"
    style={{
      minHeight: `calc(100vh - (${navbarHeight}px + ${extraVH}vh))`,
    }}
  >
  ```

- Toggle function for conversation list:
  ```ts
  const toggleConversationList = () => setIsConversationListVisible(prev => !prev);
  ```

- Conditional rendering for **ChatHeader**:
  ```tsx
  {receiverName ? (
    <>
      <ChatHeader
        receiverName={receiverName}
        isReceiverOnline={isReceiverOnline}
        onMenuClick={toggleConversationList}
        isConversationListVisible={isConversationListVisible}
      />
      <DisplayMessage ... />
      <MessageInput ... />
    </>
  ) : (
    <div className="sm:hidden flex relative bg-white px-3 py-5 pb-2">
      <RxHamburgerMenu onClick={toggleConversationList} className="w-6 h-6 sm:hidden block cursor-pointer" />
    </div>
  )}
  ```

---

### 🔹 Navbar Updates

- Added `id="navbar"` to `DashboardNavbar` for layout height calculations:
  ```tsx
  <nav id="navbar" className="flex justify-between w-full mx-auto max-w-[2000]">
  ```

---

## 6️⃣ Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Conversation list toggle not behaving responsively | Added `useEffect` to track `window.innerWidth` and set state |
| Dynamic spacing for header | Used `isConversationListVisible` prop with conditional `gap` classes |
| Layout height overlaps | Added `navbarHeight` and `extraVH` calculation with Tailwind breakpoints |
| Unexpected layout shifts | Adjusted `minHeight` using inline `style` with `navbarHeight` + `extraVH` |

---

## 7️⃣ Final Outcome

- Fully responsive chat section with toggle-able conversation list.
- Smooth layout resizing for mobile and desktop.
- Clean UI for header and receiver presence.
- Uses dynamic props and Tailwind utilities for consistent styling.

---

## 🌐 Demonstration

To test this feature:
1. Go to: [https://dev.storyvord.io/dashboard/message](https://dev.storyvord.io/dashboard/message)
2. Make sure you are **logged in** to access the chat and network messaging section.

---

