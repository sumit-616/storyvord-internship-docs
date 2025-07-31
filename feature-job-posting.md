# 📂 `feature/job-posting` — Job Details & Crew Job List Feature

---

## 🚀 Overview

This feature introduces the **Job Details Page** and enhances the **Crew Job List UI** inside the **Storyvord** platform. It allows users (specifically crew members) to:

- View detailed job information via dynamic routing using the job ID.
- See a list of available jobs fetched dynamically from backend APIs.
- Experience improved UI/UX with responsive design, skeleton loading states, and fallback content.
- Access multilingual support with i18n translation integration.

---

## 🎯 Objectives

- Build a scalable job detail page accessible via dynamic URL (`/crew/jobs/:jobId`).
- Enhance job list UI for crew to show structured, clean, and responsive layout.
- Support multilingual text rendering with complete i18n integration.
- Handle loading and error states gracefully for better UX.
- Ensure consistent layout with the rest of the platform using design tokens and shared components.

---

## ⚙️ Tech Stack

- **Next.js** — routing and page generation
- **React.js** — component rendering and state management
- **TypeScript** — strong typing for safety and scalability
- **Tailwind CSS** — for modern, responsive UI styling
- **React Query** — efficient data fetching and caching
- **i18n** — internationalization support using translation keys
- **REST API** — dynamic job fetching based on `jobId`

---

## 📁 Core Structure

```
/src/app/crew/jobs/[jobId]/page.tsx                → Job Detail dynamic page
/src/components/crew/job/JobDetails.tsx            → Core Job Detail component
/src/components/crew/job/JobDetailsCard.tsx        → Structured UI for showing job data
/src/components/crew/job/CrewJobList.tsx           → UI for listing all jobs
/src/components/ui/Skeleton.tsx                    → Loading placeholder for better UX
/src/lib/api/job/job.ts                            → API service to fetch job details
/src/i18n/locales/crew/                            → Translation files for multiple languages
```

---

## 🗂️ Detailed Features

### ✅ **Dynamic Job Detail Page**

- Route: `/crew/jobs/:jobId`
- Dynamically fetches job data based on the `jobId` from the URL.
- Uses `useQuery` with React Query to handle API call.
- Proper error handling and fallback UI shown if API fails or data is missing.
- Follows responsive layout for mobile and desktop.

### ✅ **Crew Job List**

- Page route: `/crew/jobs`
- Displays a clean list of job cards with:
  - Job title
  - Organization name
  - Type of job (e.g., Remote, On-site)
  - Short description or metadata
- Each card is clickable and routes to its corresponding detail page.
- Optimized layout for small and large screens.

### ✅ **UX Improvements**

- Introduced **Skeleton loaders** while the data is being fetched.
- Added **fallback UI** for missing content or broken API responses.
- All buttons, links, and cards are **keyboard accessible**.
- Proper hover/focus states using Tailwind utility classes.
- Layout tested for consistency with Storyvord’s global design system.

### ✅ **Internationalization (i18n)**

- All static texts (labels, headings, fallback texts) use translation keys.
- Translation keys placed inside `/locales/crew/job.json`.
- Supports 7+ languages (English, Hindi, French, German, Chinese, Spanish, Italian).
- Ensures full translation coverage for job-related UI.

---

## 📡 API Integration

- **Fetch Single Job API**
  - `GET /api/jobs/:jobId`
  - Used to render full job details dynamically
- **Fetch Job List API**
  - `GET /api/crew/jobs`
  - Used to render all available jobs for the crew

> API endpoints use token-based authentication to fetch user-specific jobs if required.

---

## 🧪 Error Handling & State Management

- Wrapped API hooks in `try-catch` and exposed `isLoading`, `isError`, `data` using React Query.
- Showed `Skeleton.tsx` when loading and translated fallback UI when no jobs are found.
- Reusable utility components ensure centralized control for layout and display.

---

## 🧩 Reusability & Scalability

- Job Card and Job Detail components are built with **props abstraction** so they can be reused in admin or client views in the future.
- API logic isolated in `job.ts` for cleaner imports and scalable maintenance.

---

## 🔗 Live Demonstration

**📍 Job Details Page**

- [`/crew/jobs/377a4e37-3319-40aa-8f8a-9899d9a7a1a9`](https://dev.storyvord.io/crew/jobs/377a4e37-3319-40aa-8f8a-9899d9a7a1a9)

**📍 Crew Job List Page**

- [`/crew/jobs`](https://dev.storyvord.io/crew/jobs)

🔐 *Login is required to view the job list and detailed job pages.*

---

## ✅ Final Result

- [x] Dynamic Job Detail page implemented
- [x] Job List page redesigned for crew
- [x] Real-time API integration added
- [x] Responsive, mobile-first layout tested
- [x] i18n integration complete
- [x] Skeleton and fallback handling covered
- [x] Code structured for future scalability

---

**📌 This finalizes the `feature/job-posting` for Storyvord — scalable, multilingual, responsive, and production-ready.**

---

**🔒 Note:**  
This documentation clearly explains the **feature’s purpose, architecture, user flow, challenges, and solutions** — without exposing any private or sensitive source code.  
It serves as a **professional record** of the development approach and best practices for future reference and team knowledge sharing.
