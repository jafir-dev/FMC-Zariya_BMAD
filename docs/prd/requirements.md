# Requirements

## Functional

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

## Non-Functional

* **NFR1:** The system must be a Progressive Web App (PWA) to ensure accessibility across mobile and desktop devices.
* **NFR2:** All user actions and status changes must be logged in an immutable audit trail for dispute resolution and compliance.
* **NFR3:** The system must comply with UAE's Personal Data Protection Law (PDPL), ensuring all user data is stored and handled securely.
* **NFR4:** The application must support both English and Arabic languages (L10N/I18N).
* **NFR5:** The system shall implement a robust Role-Based Access Control (RBAC) model to ensure data segregation and security between different roles and FMCs.
* **NFR6:** The platform should feature a clean, simple, and user-friendly interface to maximize adoption across all user types.
