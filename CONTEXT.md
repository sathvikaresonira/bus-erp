# System Context: Bus ERP (ERP-BMS)

This document acts as the definitive source of truth for the codebase structure, patterns, and deployment workflow. It should be used as context for all feature requests and bug fixes.

---

## 1. Project Mission
A centralized **Bus Management System** designed to bridge the gap between school administrators, parents, and drivers. The platform provides real-time visibility into student safety and fleet efficiency.

---

## 2. Core Architecture & Tech Stack

### Frontend Foundations
- **React 18 + Vite**: Chosen for lightning-fast development and optimized production builds.
- **TypeScript**: Strict typing across the entire codebase for enhanced developer experience and error prevention.
- **Tailwind CSS + shadcn/ui**: Modern design system using accessible Radix UI primitives and utility-first styling.

### Specialized Libraries
- **Leaflet + React-Leaflet**: Used for high-performance interactive maps. Custom SVG markers are implemented for buses with dynamic rotation (headings).
- **TanStack Query (React Query)**: Manages server-side state (currently with mock/simulated data) and caching.
- **Lucide React**: Primary icon set for a clean, consistent UI.

---

## 3. Directory Breakdown

### `/src`
- **`/components`**:
    - `Map.tsx`: The "Heart" of the app. Handles bus rendering, route polylines, and auto-centering logic.
    - `/ui`: Atomic shadcn components (Buttons, Inputs, Dialogs).
    - `/auth`: Logic for multi-role login.
- **`/context`**:
    - `DataContext.tsx`: The "Brain". Orchestrates the global state for 500+ students and 50+ buses. Includes a **real-time simulation engine** for movement.
- **`/pages`**:
    - `/admin`: High-density data views (Live Tracking, Student CRUD, Fleet Management).
    - `/parent`: Consumer-focused views (Child Tracking, Alerts).
    - `/driver`: Navigation and shift-focused views.
- **`/layouts`**: Defines structural wrappers for the three user roles, handling sidebars and high-level navigation.
- **`/types`**: Centralized TypeScript interfaces (Student, Bus, Route, Driver).

---

## 4. Operational Logic

### Role-Based Access Control (RBAC)
- Routing is protected via a `ProtectedRoute` component in `App.tsx`.
- User roles (admin, parent, driver) determine the sidebar availability and data visibility.

### Data Simulation
The system is designed for **offline-first simulation**.
- `DataContext` initializes from `localStorage`.
- A 3-second heartbeat updates bus coordinates, speeds, and statuses (e.g., "On Route", "Delayed") to mimic a live GPS feed.

---

## 5. Deployment & Infrastructure

### Version Control
- **GitHub Repository**: `https://github.com/sathvikaresonira/bus-erp.git`
- **Primary Branch**: `main`

### Hosting (Netlify)
- **Automatic Deploys**: Configured via `netlify.toml`.
- **SPA Support**: `public/_redirects` ensures no 404s on browser refreshes.
- **Environment**: Linked to GitHub for CI/CD.

---

## 6. Development Guidelines
- **Aesthetics First**: Every new component must match the premium, glassmorphic design system.
- **Type Safety**: Avoid `any` at all costs; extend existing interfaces in `/src/types`.
- **Simulated Real-time**: When adding new bus features, ensure they integrate with the `useEffect` simulation in `DataContext`.

---
*Last Updated: 2025-12-27T12:18:00+05:30*
*Author: sathvikaresonira*
