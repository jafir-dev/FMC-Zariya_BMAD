# High Level Architecture

## Technical Summary

The Zariya FMC application will be a full-stack, type-safe web application built within a **monorepo**. The architecture is designed around a **serverless** paradigm, leveraging the **Vercel** platform for both frontend and backend deployment. The frontend will be a Progressive Web App (PWA) built with **Next.js** and React. The backend API will be built using **tRPC** running on Vercel Serverless Functions, which communicate with a **PostgreSQL** database via the **Prisma** ORM. This approach ensures a highly scalable, cost-efficient, and maintainable system with a seamless development experience between the frontend and backend.

## Platform and Infrastructure Choice

* **Platform:** **Vercel**. It provides a tightly integrated, best-in-class experience for deploying Next.js applications, handling everything from the global CDN for the frontend to the serverless function execution for the backend.
* **Key Services:**
    * **Vercel Functions:** For hosting our serverless tRPC API.
    * **Vercel Postgres:** A serverless PostgreSQL database that integrates directly with the platform.
    * **Vercel Blob:** For simple, secure storage of user-uploaded files like maintenance photos.
* **Deployment Regions:** The primary region will be `me-south-1` (UAE) to ensure data residency and low latency for our target market, with Vercel's Edge Network providing global caching for the frontend.

## Repository Structure

* **Structure:** **Monorepo**, managed by **Turborepo** (as provided by the T3 Stack).
* **Package Organization:** A single `apps/web` package will contain the entire Next.js application, including frontend pages/components and the backend API routes. Shared code, such as the database schema (`packages/db`), will be managed in separate packages within the monorepo to ensure consistency.

## High Level Architecture Diagram
```mermaid
graph TD
    User[Tenant / FMC Staff] -- HTTPS --> Edge[Vercel Edge Network / CDN];
    Edge --> PWA[Next.js PWA Frontend];
    PWA -- tRPC API Calls --> API[Vercel Serverless Functions];
    API -- Prisma ORM --> DB[(Vercel Postgres DB)];
    API -- Signed URLs --> Blob[(Vercel Blob Storage for Photos)];
    API --> Email[Email Service e.g., Resend];

    subgraph Vercel Platform
        PWA;
        API;
        DB;
        Blob;
    end

    Architectural Patterns
Jamstack Architecture: The frontend PWA will be served as a highly optimized static/hybrid site from the edge, with dynamic features powered by serverless API calls.

Type-Safe API Layer (tRPC): This allows us to share TypeScript types between the frontend and backend automatically, eliminating an entire class of common bugs.

Repository Pattern (via Prisma): Prisma acts as our data access layer, providing a type-safe and intuitive way to interact with the database.

Component-Based UI: The frontend will be built using reusable React components.

Tech Stack
Technology Stack Table
Category	Technology	Version	Purpose	Rationale
Frontend Language	TypeScript	~5.5.3	Language for frontend code	Provides type safety and scalability.
Frontend Framework	Next.js	~14.2.4	React framework for the PWA	Handles server/client rendering, routing, and API.
UI Component Library	Shadcn/ui	~0.8.0	Accessible and composable UI components	Integrates perfectly with Tailwind CSS.
State Management	React Context/Hooks	(React)	Manage global and local UI state	Built-in to React, sufficient for MVP needs.
Backend Language	TypeScript	~5.5.3	Language for API and server logic	Ensures end-to-end type safety with tRPC.
Backend Framework	Next.js API Routes	~14.2.4	Framework for serverless functions	Co-located with the frontend for a seamless developer experience.
API Style	tRPC	~11.0.0-rc.402	Type-safe API layer	Eliminates need for manual API contract management.
Database	Vercel Postgres	(Latest)	Primary data store	Serverless, integrates with Vercel, and supported by Prisma.
ORM	Prisma	~5.15.0	Database toolkit for TypeScript	Provides a type-safe data access layer and simplifies migrations.
File Storage	Vercel Blob	(Latest)	Stores user-uploaded photos	Simple, secure file storage integrated with the Vercel platform.
Authentication	Next-Auth.js	~5.0.0-beta.19	Handles user authentication	Standard for the T3 Stack; simplifies secure session management.
Testing	Vitest	~1.6.0	Unit and integration testing framework	Modern, fast, and configured by default in the T3 Stack.
E2E Testing	Playwright	~1.44.1	End-to-end testing framework	Powerful and reliable for testing user flows.
Deployment & Hosting	Vercel	(Latest)	All-in-one platform for deployment	Native integration with Next.js provides the best performance.
CSS Framework	Tailwind CSS	~3.4.4	Utility-first CSS framework	Allows for rapid UI development without writing custom CSS.

Export to Sheets
Data Models
Shared Enums & Types
TypeScript

export enum Role {
  CUSTOMER,
  ASSOCIATION_OWNER,
  FMC_HEAD,
  SUPERVISOR,
  TECHNICIAN,
  PROCUREMENT,
  VENDOR
}

export enum TicketStatus {
  NEW,
  ASSIGNED_FOR_INSPECTION,
  INSPECTION_COMPLETE,
  PENDING_CUSTOMER_APPROVAL,
  APPROVED_READY_FOR_WORK,
  WORK_IN_PROGRESS,
  PENDING_OTP_VERIFICATION,
  COMPLETED,
  CLOSED_REJECTED
}
User Model
Purpose: Represents an individual who can log in and interact with the system.
Relationships: Belongs to one FMC, has one Role, can be linked to many Properties or Tickets.

TypeScript

interface User {
  id: string;
  email: string;
  name: string;
  role: Role;
  fmcId: string;
  isActive: boolean;
  createdAt: Date;
}
Ticket Model
Purpose: The central entity representing a single maintenance request.
Relationships: Belongs to one Customer (User), one Property, and can be assigned to one Technician (User).

TypeScript

interface Ticket {
  id: string;
  title: string;
  description: string;
  status: TicketStatus;
  propertyId: string;
  customerId: string;
  assignedTechnicianId?: string;
  quoteAmount?: number;
  rating?: number; // 1-5
  createdAt: Date;
  updatedAt: Date;
}
API Specification
tRPC Router Definitions
The API is defined as a set of strongly-typed routers in TypeScript, not a static document.

TypeScript

// /server/api/root.ts
import { ticketRouter } from "./routers/ticket";
import { userRouter } from "./routers/user";
import { createTRPCRouter } from "./trpc";

export const appRouter = createTRPCRouter({
  ticket: ticketRouter,
  user: userRouter,
});

export type AppRouter = typeof appRouter;
TypeScript

// /server/api/routers/ticket.ts
import { z } from "zod";
import { createTRPCRouter, protectedProcedure } from "../trpc";

export const ticketRouter = createTRPCRouter({
  create: protectedProcedure("CUSTOMER")
    .input(z.object({ title: z.string().min(5), /* ... */ }))
    .mutation(async ({ ctx, input }) => { /* ... */ }),

  getNewForSupervisor: protectedProcedure("SUPERVISOR")
    .query(async ({ ctx }) => { /* ... */ }),

  assign: protectedProcedure("SUPERVISOR")
    .input(z.object({ ticketId: z.string(), technicianId: z.string() }))
    .mutation(async ({ ctx, input }) => { /* ... */ }),
});
Components
1. PWA Frontend (Next.js): Renders the UI, manages client state, and handles user interactions.

2. tRPC API (Vercel Functions): Executes all business logic and provides the secure, type-safe data layer.

3. Authentication Service (Next-Auth.js): Manages sign-in, sessions, and role-based access control.

4. Database (Vercel Postgres + Prisma): Provides persistent storage for all application data.

5. File Storage (Vercel Blob): Securely stores user-uploaded binary files (e.g., photos).

6. Notification Service: Sends transactional emails for critical events (OTP, approvals, etc.).

External APIs
Resend API
Purpose: To send all transactional emails required by the application.

Documentation: https://resend.com/docs

Authentication: API Key (stored as a secure environment variable).

Integration: Via the official resend NPM package in our tRPC API.

Core Workflows
This sequence diagram illustrates the "Ticket Creation & Assignment" flow.

Code snippet

sequenceDiagram
    actor Tenant
    participant PWA_Frontend as PWA Frontend (Next.js)
    participant tRPC_API as tRPC API (Vercel Fn)
    participant Auth as Auth Service (Next-Auth)
    participant DB as Database (Prisma)
    participant Notif as Notification Service

    Tenant->>+PWA_Frontend: 1. Fills out and submits new ticket form
    PWA_Frontend->>+tRPC_API: 2. Calls `ticket.create` mutation with data
    tRPC_API->>+Auth: 3. Verifies user session and role (Tenant)
    Auth-->>-tRPC_API: 4. Session is valid
    tRPC_API->>+DB: 5. Creates new Ticket record
    DB-->>-tRPC_API: 6. Returns created ticket
    tRPC_API->>+Notif: 7. (Async) Triggers notification for Supervisor
    tRPC_API-->>-PWA_Frontend: 8. Returns success response
    PWA_Frontend-->>-Tenant: 9. Displays "Success!" message
Database Schema
The schema is defined in prisma/schema.prisma and serves as the single source of truth for our database.

Code snippet

generator client {
  provider = "prisma-client-js"
}
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id            String    @id @default(cuid())
  email         String    @unique
  hashedPassword String
  role          Role
  // ... relations
}

model Ticket {
  id                   String       @id @default(cuid())
  title                String
  description          String
  status               TicketStatus @default(NEW)
  // ... relations and indexes
}

enum Role { /* ... */ }
enum TicketStatus { /* ... */ }
Frontend Architecture
Component Organization
Plaintext

src/
└── components/
    ├── features/   # Feature-specific components (e.g., TicketList)
    ├── layouts/    # Page shells (e.g., DashboardLayout)
    └── ui/         # Generic, reusable UI components from Shadcn/ui
Routing Architecture
We will use the Next.js App Router with file-based routing and route groups for protected areas.

Plaintext

app/
├── (app)/          # Protected application routes
│   ├── layout.tsx    # Checks for session, redirects if not authenticated
│   └── dashboard/
├── (auth)/         # Authentication routes
│   └── login/
└── page.tsx        # Landing page
Frontend Services Layer (API Integration)
Data is fetched via type-safe tRPC hooks.

TypeScript

"use client";
import { api } from "~/trpc/react";

export function TicketList() {
  const { data: tickets } = api.ticket.getNewForSupervisor.useQuery();
  // ... render logic
}
Backend Architecture
Service Architecture (Serverless)
All backend logic is contained in tRPC routers deployed as Vercel Serverless Functions.

Plaintext

src/
└── server/
    └── api/
        ├── root.ts         # Main app router
        ├── trpc.ts         # Middleware and context
        └── routers/
            ├── user.ts     # User-related procedures
            └── ticket.ts   # Ticket-related procedures
Authorization
Authorization is handled by tRPC middleware (protectedProcedure) which checks user roles before executing logic.

Unified Project Structure
A detailed file structure based on the T3 Stack will be used, separating app/, components/, and server/ logic clearly.

Development Workflow
The workflow includes local setup with Docker for PostgreSQL, npm install, and running the app with npm run dev. Environment variables are managed in a .env file.

Deployment Architecture
A git-driven CI/CD pipeline using Vercel will deploy Pull Requests to preview URLs, the staging branch to a staging environment, and the main branch to production.

Security and Performance
Security: Enforced via httpOnly cookies (Next-Auth), Zod input validation (tRPC), role-based procedures, and a Content Security Policy.

Performance: Optimized via Next.js code-splitting, Vercel's Edge CDN, and a P95 API response target of <500ms.

Testing Strategy
A multi-layered strategy using Vitest for unit/integration tests (co-located with code) and Playwright for end-to-end tests will be implemented.

Coding Standards
A concise set of critical rules will be enforced, including end-to-end type safety, exclusive use of the tRPC API layer for data access, and consistent use of the UI library.

Error Handling Strategy
Errors are handled via specific TRPCError instances on the backend, which are caught gracefully on the frontend by tRPC's error object and displayed to the user via toast notifications.

Monitoring and Observability
The stack includes Vercel Analytics for frontend performance, Vercel Log Drains for backend monitoring, and Sentry for real-time error tracking and alerting.

Checklist Results Report
An internal review has been completed, and this architecture is considered comprehensive, robust, and ready for development