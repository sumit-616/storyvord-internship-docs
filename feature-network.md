# 📂 `feature/network` — Storyvord Professional Networking

---

## 🚀 Overview

This module implements the complete **Network System** for **Storyvord**, enabling users to:

- Build and manage their professional network.
- Send and manage connection requests.
- Discover and connect with suggested users.
- See message summaries right inside their **Dashboard** and **Crew Home** pages.
- Search connections in both quick panels and full pages.
- Use the system across multiple supported languages.

---

## 🎯 Objectives

- Centralize **query and mutation** logic in parent components for easy maintenance.
- Reuse UI components for **client-side** and **crew-side** views.
- Provide smooth **UX** with smart loading states, fallback avatars, and accessible modals.
- Add **search functionality** in:
  - Dashboard quick view.
  - Full Network pages.
  - Message Summary widget.
- Ensure responsive design with scrollable panels for large networks.
- Improve translations and empty states for all supported locales.

---

## ⚙️ Tech Stack

- **React.js** (Components)
- **Next.js** (Routing & Pages)
- **TypeScript** (Type safety)
- **Tailwind CSS** (Responsive styling)
- **React Query** (`useQuery`, `useMutation`)
- **i18n** for multilingual support

---

## 📁 Key Structure

/src/components/network/NetworkPage.tsx → Parent wrapper
/src/components/network/MyNetwork.tsx → Dashboard/Crew right panel
/src/components/network/RequestCard.tsx → Sent & Received requests
/src/components/network/SendRequestForm.tsx → Modal for new requests
/src/components/network/SimilarSuggestions.tsx → Suggestions carousel/grid
/src/components/network/MessageSummary.tsx → Right-bottom quick panel
/src/components/user/UserAvatar.tsx → Fallback avatars
/src/lib/api/network/network.ts → API handlers
/src/lib/react-query/queriesAndMutations/network/ → React Query hooks
/src/i18n/locales/ → Multi-language keys
/src/app/dashboard/network/page.tsx → Full Dashboard Network
/src/app/crew/network/page.tsx → Full Crew Network

yaml
Copy
Edit

---

## 🗂️ Detailed Features

### ✅ **Centralized Data Flow**

- All `useQuery` and `useMutation` logic lifted to parent pages.
- Props passed down for **connections**, **requests**, **actions**, **handlers**.
- No duplicated logic — only one source of truth.

---

### ✅ **Send Request**

- `SendRequestForm` handles modal flow.
- Removed obsolete **Full Name** field for cleaner UX.
- Request submission:
  - Validates receiver’s email.
  - Calls `useSendConnectionRequestMutation`.
  - Shows success/error toast.
  - Closes modal automatically.

---

### ✅ **Connection Requests**

- `RequestCard` shows:
  - Avatar, name, job title.
  - Buttons for **Accept** and **Decline**.
  - Loading state on action.
- Accepts/declines handled via React Query mutations.

---

### ✅ **Similar Suggestions**

- Displays a carousel/grid of recommended connections.
- Each card has `Connect` → opens `SendRequestForm`.
- Layout updated for long job titles with proper truncation.

---

### ✅ **Message Summary**

- Right-bottom widget on:
  - `/dashboard/`
  - `/crew/home/`
- Shows quick list of connections.
- Added **Search Bar** inside widget for instant filtering.
- Applied max-height with scroll for large lists.
- Fixed layout overflow bugs.

---

### ✅ **Full Network Pages**

- `/dashboard/network/`
- `/crew/network/`
- Reuse:
  - `MyNetwork`
  - `ConnectionRequest`
  - `SimilarSuggestions`
  - `MessageSummary`
- Includes **search**, **filter**, **empty states**, and full interactions.

---

### ✅ **Internationalization**

- Multi-language keys added for:
  - English, Hindi, Spanish, French, German, Italian, Chinese.
- Translations updated for:
  - Empty states
  - Actions
  - Button labels
  - Toast messages
- Consistent fallback text when data is empty or search returns no results.

---

## 🔎 Search Improvements

- `SearchBar` integrated in:
  - Dashboard panel
  - Full Network pages
  - Message Summary
- Real-time filtering of connections by name.
- `noResultsFound` text shown if no match.

---

## ✅ Fixes & Polishing

- Truncation for long job titles in **Similar Suggestions**.
- Consistent padding and scroll for quick lists.
- Better form handling with single input (Email only).
- Navigation in sidebars updated to include **Network** link.
- Loading animations for sending, accepting, rejecting requests.
- Fallback avatars if user photo is missing.

---

## 🔗 Live Demonstration

**📍 Right-Bottom Panel**

- [`/dashboard/`](https://dev.storyvord.io/dashboard/)
- [`/crew/home/`](https://dev.storyvord.io/crew/home/)

**🌐 Full Pages**

- [`/dashboard/network/`](https://dev.storyvord.io/dashboard/network/)
- [`/crew/network/`](https://dev.storyvord.io/crew/network/)

🔐 *You must be logged in to test the full experience.*

---

## ✅ Final Checklist

- [x] Centralized query & mutation logic.
- [x] Client & Crew page support.
- [x] Search added to all sections.
- [x] Overflow & layout bugs fixed.
- [x] Navigation updated.
- [x] i18n keys reviewed.
- [x] Demonstration verified.

---

**🎉 This completes the `feature/network` module for Storyvord!**
