# Zariya FMC Product Requirements Document (PRD)

## Goals and Background Context

### Goals

* Launch a scalable SaaS product with a tiered pricing model to capture the UAE's Facility Management Company (FMC) market.
* Significantly reduce the average ticket resolution time and operational overhead for FMCs.
* Achieve high user adoption and satisfaction across all seven user roles, measured by post-job ratings and active use.
* Improve the first-time-fix rate for technicians through clear information and streamlined workflows.
* Decrease the volume of tenant follow-up inquiries by providing full transparency on ticket status.

### Background Context

Facility Management Companies currently suffer from inefficient, manual, and non-transparent processes for handling maintenance requests. This fragmentation leads to operational delays, poor communication between tenants and staff, and a lack of data-driven insights, ultimately causing tenant dissatisfaction and higher costs.

Zariya FMC solves this by providing a unified, role-based Progressive Web App (PWA) that digitizes and automates the entire maintenance lifecycle. The platform streamlines everything from ticket creation and inspection to approvals, procurement, and final, OTP-verified job completion. This creates a transparent, efficient, and communicative ecosystem for tenants, FMC staff, and associated vendors.

### Change Log

| Date | Version | Description | Author |
| :--- | :--- |:--- |:--- |
| 2025-09-07 | 1.0 | Initial PRD draft created from Project Brief. | John (PM) |

## Requirements

### Functional

* **FR1:** A secure, role-based authentication system shall be provided for 7 distinct user types (Customer, Building Association Owner, FMC Head, Supervisor, Technician, Procurement, Third-Party Vendor).
* **FR2:** Customers shall be able to create a maintenance ticket specifying the problem, a detailed description, photo/video evidence, and their availability.
* **FR3:** Supervisors shall be able to view, manage, and assign tickets to Technicians or Third-Party Vendors.
* **FR4:** Technicians/Vendors shall receive notifications for new assignments, inspect the issue, and submit a report including a cost-type (free/paid), a quote for paid work, and a list of required materials.
* **FR5:** Customers must be able to approve or reject quotes for paid work before any further action is taken.
* **FR6:** An integrated workflow shall manage the procurement of materials for approved, paid jobs.
* **FR7:** Technicians shall be required to upload "before" and "after" photos/videos for all work performed.
* **FR8:** Customers shall verify job completion by providing a one-time password (OTP) sent to their email, after which they can rate the service.
* **FR9:** The system shall support a tiered pricing and subscription model for FMC clients, presented on a public-facing landing page.
* **FR10:** All users shall have a unified notification center to view alerts from various channels (In-App, Email, Push, SMS, WhatsApp) with read/unread status.
* **FR11:** The system will generate downloadable receipts/invoices for all completed, paid maintenance work, featuring the FMC's branding.

### Non-Functional

* **NFR1:** The system must be a Progressive Web App (PWA) to ensure accessibility across mobile and desktop devices.
* **NFR2:** All user actions and status changes must be logged in an immutable audit trail for dispute resolution and compliance.
* **NFR3:** The system must comply with UAE's Personal Data Protection Law (PDPL), ensuring all user data is stored and handled securely.
* **NFR4:** The application must support both English and Arabic languages (L10N/I18N).
* **NFR5:** The system shall implement a robust Role-Based Access Control (RBAC) model to ensure data segregation and security between different roles and FMCs.
* **NFR6:** The platform should feature a clean, simple, and user-friendly interface to maximize adoption across all user types.

## User Interface Design Goals

### Overall UX Vision

The core UX vision for Zariya FMC is **effortless efficiency**. The interface should be intuitive enough for a first-time tenant to submit a ticket without any training, yet powerful enough for a supervisor to manage dozens of tasks daily. The design will be clean, uncluttered, and focused, prioritizing clarity and ease of use to reduce cognitive load on all users.

### Key Interaction Paradigms

* **Task-Driven Dashboards:** Each user role will have a dedicated dashboard that surfaces the most critical information and immediate tasks relevant to them.
* **Guided Workflows:** Submitting tickets, approving quotes, and completing jobs will follow a step-by-step, wizard-like process to ensure all necessary information is captured correctly.
* **Real-time Feedback:** The UI will provide immediate feedback for user actions, such as submitting a form or updating a ticket's status.

### Core Screens and Views

* **Login/Authentication Screen:** A simple and secure entry point.
* **Customer Dashboard:** View and manage properties, see a list of active/past tickets, and create new requests.
* **Ticket Submission Form:** A multi-step form for capturing all ticket details.
* **Supervisor Dashboard:** An overview of all building tickets, staff assignments, and pending approvals.
* **Technician/Vendor Task View:** A simple list or card view of assigned jobs with all necessary details.
* **Ticket Detail View:** A comprehensive view of a single ticket's history, communication, media, and status, tailored to the viewing user's role.

### Accessibility: WCAG AA

The application will be designed to meet WCAG 2.1 AA standards. This includes considerations for screen reader compatibility, keyboard navigation, sufficient color contrast, and support for both English and Arabic (Right-to-Left layout).

### Branding

The platform will be designed to be "white-labeled." Each FMC client will be able to upload their own logo and input their company details, which will automatically appear on customer-facing views and downloadable documents like receipts.

### Target Device and Platforms: Web Responsive

The application will be a Progressive Web App (PWA), built with a mobile-first, responsive design to ensure a seamless experience on any device, from a tenant's mobile phone to a supervisor's desktop computer.

## Technical Assumptions

### Repository Structure: Monorepo

A **monorepo** structure is recommended. This will allow us to manage both the frontend PWA and the backend API in a single repository, making it easier to share code (like data types) and manage dependencies.

### Service Architecture: Serverless

A **Serverless** architecture (e.g., using Vercel Functions, AWS Lambda) is suggested. This model is cost-effective to start, scales automatically with demand, and pairs perfectly with a modern PWA, aligning with our goal of a scalable SaaS platform.

### Testing Requirements: Unit + Integration

A testing strategy that includes both **Unit Tests** for individual functions and components, and **Integration Tests** to ensure the different parts of the application work correctly together will be established.

### Additional Technical Assumptions and Requests

The recommended technology stack is **Next.js with TypeScript for the frontend and backend, styled with Tailwind CSS, and connected to a PostgreSQL database via Prisma**.

## Epic List

1.  **Epic 1: Foundation & Core User Management:** Establish the project's technical foundation, monorepo structure, and implement a robust system for the FMC Head to create and manage all 7 user roles and their associated properties.
2.  **Epic 2: Core Ticket Creation & Initial Triage:** Enable tenants to submit detailed maintenance tickets, which supervisors can then view, manage, and assign to technicians for inspection.
3.  **Epic 3: Inspection, Reporting & Quote Approval:** Allow technicians to conduct inspections and submit detailed reports with quotes, and enable tenants to approve or reject the proposed work.
4.  **Epic 4: Job Execution & OTP-Verified Completion:** Facilitate the final workflow where technicians perform the approved work, upload evidence, and the tenant verifies completion using a secure OTP before providing a rating.

### Epic 1: Foundation & Core User Management

**Expanded Goal:** This foundational epic establishes the project's entire technical backbone. It includes setting up the monorepo, initializing the serverless backend and PWA frontend, and defining the core database schemas. The key deliverable is a functional user management system where an FMC Head can create and manage all user accounts, setting the stage for all future ticket-related functionality.

---

**Story 1.1: Project Initialization**
* **As a** Developer,
* **I want** a new monorepo initialized with a basic serverless backend and PWA frontend,
* **so that** the development team has a structured and consistent codebase to begin work.

**Acceptance Criteria:**
1.  A new monorepo is created using Turborepo.
2.  A basic Next.js PWA is created within the monorepo.
3.  A basic serverless API endpoint (e.g., a health check) is functional.
4.  Shared TypeScript and ESLint configurations are in place.
5.  The project can be installed and run locally with a single command.

---

**Story 1.2: Database & Core Schema Setup**
* **As a** Backend Developer,
* **I want** the database connected via Prisma and the initial schemas for Users, Roles, Properties, and FMCs created,
* **so that** we can store and manage the application's core data.

**Acceptance Criteria:**
1.  Prisma is configured to connect to a local PostgreSQL database.
2.  Database schemas for `User`, `Role`, `FMC`, and `Property` are defined.
3.  A migration is successfully generated and can be applied to the database.
4.  The seven user roles are seeded into the `Role` table upon migration.

---

**Story 1.3: Secure User Authentication**
* **As a** User,
* **I want** to log in securely with my email and password,
* **so that** I can access the application and my role-specific dashboard.

**Acceptance Criteria:**
1.  A secure login API endpoint is created.
2.  User credentials are validated against hashed passwords in the `User` table.
3.  On successful login, a secure JWT is returned to the client.
4.  A basic, functional login page is created on the PWA.
5.  The PWA stores the session token securely and provides a method for logout.

---

**Story 1.4: FMC Head User Management Dashboard**
* **As an** FMC Head,
* **I want** a dashboard to create, view, and manage all users (staff and tenants) for my properties,
* **so that** I can onboard my entire team and client base onto the platform.

**Acceptance Criteria:**
1.  A protected page/view is accessible only to users with the 'FMC Head' role.
2.  The page displays a list of all users associated with the FMC Head's company.
3.  A form allows the creation of new users, including assigning them a role and property.
4.  The FMC Head can activate or deactivate user accounts.

### Epic 2: Core Ticket Creation & Initial Triage

**Expanded Goal:** This epic delivers the first and most critical piece of end-user functionality. It focuses entirely on the tenant's experience of creating a detailed maintenance request and the supervisor's ability to receive and perform the initial triage on that request. By the end of this epic, the core value proposition of easily reporting issues will be fully functional.

---

**Story 2.1: Tenant Dashboard and Property View**
* **As a** Tenant,
* **I want** to see a simple dashboard with a list of my properties after I log in,
* **so that** I can select the correct property for a new maintenance request.

**Acceptance Criteria:**
1.  After login, a user with the 'Customer' role is directed to their dashboard page.
2.  The dashboard displays a list of one or more properties associated with that tenant's account.
3.  A clear and prominent button or link labeled "Create New Request" is visible.

---

**Story 2.2: Ticket Creation Form**
* **As a** Tenant,
* **I want** a user-friendly form to create a new maintenance ticket,
* **so that** I can provide all the necessary information easily.

**Acceptance Criteria:**
1.  The "Create New Request" action opens the ticket submission form.
2.  The form includes fields for: Problem Title, Description, and preferred Availability Times.
3.  The form provides an option to upload at least one photo of the issue.
4.  Upon submission, the form is validated to ensure required fields are filled.
5.  A confirmation message ("Request Submitted Successfully") is shown to the tenant after submission.
6.  The new ticket is saved to the database with a "New" status and linked to the correct tenant and property.

---

**Story 2.3: Tenant Ticket List View**
* **As a** Tenant,
* **I want** to see a list of my previously submitted tickets with their current status,
* **so that** I can track the progress of my requests.

**Acceptance Criteria:**
1.  The tenant dashboard displays a list of all tickets submitted by that user.
2.  Each ticket in the list shows its unique ID, Problem Title, Property, and current Status (e.g., "New").
3.  Clicking a ticket in the list navigates to a simple, read-only detail view of the submitted information.

---

**Story 2.4: Supervisor Ticket Triage and Assignment**
* **As a** Supervisor,
* **I want** to see a dashboard of all new tickets for the buildings I manage,
* **so that** I can review them and assign them to a technician for inspection.

**Acceptance Criteria:**
1.  A user with the 'Supervisor' role is directed to their dashboard upon login.
2.  The dashboard displays a list of all tickets with the status "New" from their assigned properties.
3.  The supervisor can click a ticket to view its full details, including any photos.
4.  The detail view includes a dropdown list of available technicians.
5.  The supervisor can select a technician and click an "Assign for Inspection" button.
6.  Upon assignment, the ticket's status is updated to "Assigned for Inspection".
7.  A basic email notification is sent to the assigned technician.

### Epic 3: Inspection, Reporting & Quote Approval

**Expanded Goal:** This epic builds directly on the triage process from Epic 2, focusing on the critical "middle" part of the workflow. It empowers technicians to provide detailed inspection reports and enables a transparent, customer-driven approval process for paid work. Completing this epic means the entire pre-work phase, from issue report to job approval, is handled within the system.

---

**Story 3.1: Technician Task View**
* **As a** Technician,
* **I want** to see a list of my assigned inspection tasks and view the full ticket details,
* **so that** I can understand the issue and prepare for the inspection visit.

**Acceptance Criteria:**
1.  After login, a 'Technician' role is directed to a "My Tasks" dashboard.
2.  The dashboard lists all tickets assigned to them with the status "Assigned for Inspection".
3.  The technician can click a task to view the full ticket details submitted by the tenant.
4.  The ticket view includes a button to "Submit Inspection Report".

---

**Story 3.2: Inspection Reporting Form**
* **As a** Technician,
* **I want** a form to submit my inspection findings,
* **so that** I can inform the supervisor of the necessary work, materials, and costs.

**Acceptance Criteria:**
1.  The "Submit Inspection Report" button opens a new form.
2.  The form allows the technician to select if the work is "Free of Charge" or "Paid".
3.  If "Paid" is selected, fields for a Quote amount and a list of Required Materials are displayed.
4.  Upon submission, the ticket status is updated to "Inspection Complete".
5.  The inspection report, including any quote, is saved and linked to the ticket.

---

**Story 3.3: Supervisor Review and Quote Forwarding**
* **As a** Supervisor,
* **I want** to review the technician's inspection report and, if applicable, forward the quote to the tenant,
* **so that** I can get customer approval before proceeding with the work.

**Acceptance Criteria:**
1.  The supervisor's dashboard shows tickets with the status "Inspection Complete".
2.  The supervisor can view the technician's full report, including the quote and materials list.
3.  If the job is "Paid", a "Send Quote to Customer" button is visible.
4.  Clicking the button updates the ticket's status to "Pending Customer Approval".
5.  A basic email notification is sent to the tenant containing the quote details.

---

**Story 3.4: Tenant Quote Approval**
* **As a** Tenant,
* **I want** to receive and be able to approve or reject a quote for paid maintenance work,
* **so that** I have control over the costs.

**Acceptance Criteria:**
1.  The tenant's dashboard shows tickets with the status "Pending Customer Approval".
2.  The ticket detail view clearly displays the quote amount and work details from the technician's report.
3.  Two prominent buttons, "Approve Quote" and "Reject Quote," are visible.
4.  Clicking "Approve Quote" updates the ticket's status to "Approved - Ready for Work".
5.  Clicking "Reject Quote" updates the ticket's status to "Closed - Rejected by Customer".
6.  The supervisor receives an email notification of the tenant's decision in both cases.

### Epic 4: Job Execution & OTP-Verified Completion

**Expanded Goal:** This final MVP epic closes the loop on the entire maintenance workflow. It covers the technician's on-site work, the critical evidence-gathering step of taking photos, and the secure, customer-verified completion process using a one-time password (OTP). This epic ensures that work is not just done, but verifiably and satisfactorily completed, providing a trustworthy and transparent experience for the tenant.

---

**Story 4.1: Technician View of Approved Jobs**
* **As a** Technician,
* **I want** to see a list of my approved jobs that are ready for work,
* **so that** I can plan my schedule and begin the maintenance.

**Acceptance Criteria:**
1.  The technician's "My Tasks" dashboard has a section or filter for tickets with the status "Approved - Ready for Work".
2.  The technician can view the full ticket details, including the approved quote and the list of required materials.
3.  A "Start Work" button is visible on the ticket detail view.

---

**Story 4.2: Job Execution & Evidence Upload**
* **As a** Technician,
* **I want** to be able to mark a job as 'In Progress' and upload before-and-after photos,
* **so that** I can document my work and provide evidence of completion.

**Acceptance Criteria:**
1.  Clicking the "Start Work" button updates the ticket status to "Work in Progress".
2.  The ticket detail view for the technician now includes fields to upload a "Before Work" photo and an "After Work" photo.
3.  Photos are successfully uploaded and linked to the ticket.
4.  A "Mark as Complete" button is available.

---

**Story 4.3: Work Completion & OTP Generation**
* **As a** Technician,
* **I want** to mark the job as complete, which triggers an OTP to be sent to the customer,
* **so that** I can get their on-site verification that the work is done to their satisfaction.

**Acceptance Criteria:**
1.  Clicking "Mark as Complete" updates the ticket status to "Pending OTP Verification".
2.  The system generates a unique, 6-digit OTP that is valid for a short period (e.g., 10 minutes).
3.  The OTP is sent to the tenant's registered email address.
4.  The technician's view now shows a field to enter the OTP received from the customer.

---

**Story 4.4: OTP Verification & Final Rating**
* **As a** Tenant,
* **I want** to verify the completed work by providing an OTP and then rate the service,
* **so that** I can confirm my satisfaction and provide valuable feedback.

**Acceptance Criteria:**
1.  The technician enters the OTP provided by the tenant into the app.
2.  The system validates the OTP. Upon success, the ticket status is updated to "Completed".
3.  If the OTP is incorrect or expired, an error message is shown.
4.  After successful validation, the tenant's view of the ticket prompts them to provide a service rating (e.g., 1-5 stars).
5.  The rating is saved and linked to the ticket.

## Checklist Results Report

I have validated the PRD against the BMad PM Master Checklist. The document is in excellent shape and ready for the next phase.

#### Category Statuses

| Category | Status | Critical Issues |
| :--- | :--- | :--- |
| 1. Problem Definition & Context | ✅ PASS | None |
| 2. MVP Scope Definition | ✅ PASS | None |
| 3. User Experience Requirements | ✅ PASS | None |
| 4. Functional Requirements | ✅ PASS | None |
| 5. Non-Functional Requirements | ✅ PASS | None |
| 6. Epic & Story Structure | ✅ PASS | None |
| 7. Technical Guidance | ✅ PASS | None |
| 8. Cross-Functional Requirements | ⚠️ PARTIAL | Data migration and specific operational needs can be further detailed during the architecture phase. |
| 9. Clarity & Communication | ✅ PASS | None |

#### Critical Deficiencies
* None. The PRD is not blocked.

#### Recommendations
* The Architect should explicitly define data seeding strategies and detailed monitoring requirements for key workflows during the architecture design phase to address the `PARTIAL` status in section 8.

#### Final Decision
* **READY FOR ARCHITECT**: The PRD and epics are comprehensive, properly structured, and ready for architectural design.

## Next Steps

This PRD is now complete and serves as the primary input for the next agents.

#### UX Expert Prompt

> "Hello Sally. The PRD for Zariya FMC is complete. Please review the 'User Interface Design Goals' and the relevant epics to create the detailed UI/UX Specification (`front-end-spec.md`)."

#### Architect Prompt

> "Hello Winston. The PRD for Zariya FMC is complete. Once the `front-end-spec.md` is available from the UX Expert, please use both documents to create the comprehensive `fullstack-architecture.md`, which will serve as the blueprint for development."