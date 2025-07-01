# ✅ 📂 Documentation — feature/network

---

## 1️⃣ Feature Name

`feature/network` — Complete implementation of the **Network Section** including **My Network**, **Send Request**, **Connection Requests (Sent & Received)**, **Suggestions**, and **Message Summary** integration for the **Storyvord** dashboard.

---

## 2️⃣ Objective

To build a complete **professional networking module** inside Storyvord’s platform where users can:
- View all current connections.
- Send new connection requests with a custom message.
- Manage Sent & Received requests.
- Accept or decline incoming requests.
- Get suggested connections.
- See a summary of connections/messages on the Dashboard & Crew pages.

---

## 3️⃣ Tech Stack

- React.js (components)
- Next.js (pages & routing)
- TypeScript
- Tailwind CSS (responsive styling)
- React Query (`useQuery`, `useMutation`)
- API endpoints for connection actions
- Reusable Avatar and UI components

---

## 4️⃣ Key Files

```
/src/components/network/MyNetworkSection.tsx → Main “My Network” UI  
/src/components/network/RequestCard.tsx → Sent & Received Request Cards  
/src/components/network/SendRequestModal.tsx → Modal to send new connection requests  
/src/components/network/SimilarSuggestions.tsx → Suggested users carousel  
/src/components/user/UserAvatar.tsx → Reusable avatar component  
/src/app/dashboard/network/page.tsx → Full Network page  
/src/app/crew/network/page.tsx → Crew Network page  
/src/app/dashboard/page.tsx → Dashboard with right-side network summary  
/src/app/crew/home/page.tsx → Crew home with right-side network summary  
/src/lib/api/network/network.ts → API functions (getConnections, sendRequest, acceptRequest, rejectRequest)  
/src/lib/react-query/queriesAndMutations/network/network.ts → React Query hooks  
```

---

## 5️⃣ Detailed Flow

### 🔹 **My Network Section**

- Fetches the user’s **existing connections**.
- Displays them as **cards** with `UserAvatar`, name, role.
- Uses `useQuery` hook:
  ```ts
  const { data: connections } = useGetMyConnectionsQuery();
  ```

---

### 🔹 **Send Request Modal**

- Triggered by a **“Connect”** button on user cards.
- Opens `SendRequestModal`:
  - Form with **custom message** field.
  - Submit calls `useSendConnectionRequestMutation`:
    ```ts
    const { mutate: sendRequest } = useSendConnectionRequestMutation();
    sendRequest({ receiverId, message });
    ```
  - Shows toast for success or failure.
  - Closes modal on success.

---

### 🔹 **Connection Requests (Sent & Received)**

- Separate tabs for **Sent Requests** & **Received Requests**.
- `RequestCard` component:
  - Displays avatar, name, role, and status.
  - If received: buttons for **Accept** or **Decline**.
  - Accept: `useAcceptConnectionRequestMutation`.
  - Decline: `useRejectConnectionRequestMutation`.

---

### 🔹 **Similar Suggestions**

- Fetches **users you may know** with `useGetSuggestedConnectionsQuery`.
- Displayed in a horizontal **carousel** or grid.
- Each suggestion includes:
  - `UserAvatar`
  - Name, role
  - “Connect” button → opens `SendRequestModal`.

---

### 🔹 **Reusable `UserAvatar`**

- Shared across:
  - My Network
  - Suggestions
  - Request Cards
- Supports fallback initials or placeholder if image is missing.

---

### 🔹 **Right Panel Message Summary**

- On:
  - `/dashboard/` → right sidebar
  - `/crew/home/` → right sidebar
- Shows **number of connections**, pending requests, messages.
- Links to **Full Network Page** or **Full Crew Network**.

---

### 🔹 **Full Pages**

- `/dashboard/network/` → Full **My Network** for dashboard users.
- `/crew/network/` → Full **Crew Network**.
- Both reuse `MyNetworkSection` + `SimilarSuggestions` + Requests.

---

## 6️⃣ APIs Used

| Method | Endpoint | Description |
|--------|-----------|--------------|
| `GET` | `/network/my-connections` | Get user’s current connections |
| `POST` | `/network/send-request` | Send new connection request |
| `GET` | `/network/sent-requests` | List sent requests |
| `GET` | `/network/received-requests` | List incoming requests |
| `PATCH` | `/network/accept-request` | Accept a connection |
| `DELETE` | `/network/reject-request` | Decline a connection |
| `GET` | `/network/suggestions` | Get suggested connections |

---

## 7️⃣ State & Hooks

- `useQuery` for:
  - Connections
  - Suggestions
  - Requests (sent & received)
- `useMutation` for:
  - Send request
  - Accept request
  - Reject request

Example:
```ts
export const useSendConnectionRequestMutation = () => {
  return useMutation({
    mutationFn: (data: SendRequestInput) => sendConnectionRequest(data),
  });
};
```

---

## 8️⃣ Challenges & How I Tackled Them

- ✅ **Dynamic Modals:** Ensured only 1 modal opens per click, handled closing on success.
- ✅ **API Cache Updates:** Used React Query `invalidateQueries` to refresh lists on accept/reject.
- ✅ **Fallback Avatars:** Added fallback initials when profile images fail.
- ✅ **Cross-page Consistency:** Reused `UserAvatar` and card components for Dashboard, Crew, Network pages.
- ✅ **Responsive Layout:** Tailwind CSS breakpoints for cards & grid layout.

---

## 9️⃣ Final Outcome

- Fully functional **professional networking** inside Storyvord.
- Users can:
  - See connections.
  - Send requests.
  - Accept/decline requests.
  - Discover new connections.
- Responsive, reusable UI across **Dashboard**, **Crew**, **Network** pages.
- Clean React Query logic for data sync.

---

## 🌐 Demonstration

- **Right-Bottom Panel**:
  - [https://dev.storyvord.io/dashboard/](https://dev.storyvord.io/dashboard/)
  - [https://dev.storyvord.io/crew/home/](https://dev.storyvord.io/crew/home/)
- **Full Page**:
  - [https://dev.storyvord.io/dashboard/network/](https://dev.storyvord.io/dashboard/network/)
  - [https://dev.storyvord.io/crew/network/](https://dev.storyvord.io/crew/network/)

Login required to test full features.
