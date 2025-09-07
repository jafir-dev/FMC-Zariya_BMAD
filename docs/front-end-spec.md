# Zariya FMC UI/UX Specification

## Introduction

This document defines the user experience goals, information architecture, user flows, and visual design specifications for Zariya FMC's user interface. It serves as the foundation for visual design and frontend development, ensuring a cohesive and user-centered experience.

### Overall UX Goals & Principles

#### Target User Personas
While there are seven roles, our primary focus will be on the core users in the workflow:
* **The Tenant (Customer):** Needs a quick, simple, and reassuring way to report issues and track their status with minimal friction.
* **The Technician/Vendor:** Needs a clear, mobile-friendly view of their assigned tasks with all necessary details to perform their job efficiently.
* **The Supervisor:** Needs a powerful, at-a-glance dashboard to manage multiple tickets, oversee staff, and make quick decisions.

The experience for other roles (FMC Head, Procurement, etc.) will be optimized for their specific, less frequent tasks.

#### Usability Goals
* **Ease of Learning:** A new tenant should be able to submit their first ticket in under 2 minutes.
* **Efficiency of Use:** A supervisor should be able to triage and assign 10 new tickets in under 5 minutes.
* **Error Prevention:** The design will use guided workflows and clear confirmations to prevent incorrect data entry or accidental approvals.
* **Transparency:** At any point, a user should be able to understand the current status of a ticket and what the next step is.

#### Design Principles
1.  **Clarity Above All:** Prioritize clear, unambiguous language and visuals. Avoid jargon and complex layouts.
2.  **Role-Focused Simplicity:** Each user's interface will be tailored to their specific role, hiding irrelevant information to reduce cognitive load.
3.  **Transparent Progress:** Always make the status of a task or ticket obvious and easy to find.
4.  **Guided Actions:** Nudge users toward the next logical step in any workflow.
5.  **Trust Through Evidence:** Use features like photo uploads and OTP verification to build trust in the process for both tenants and FMCs.

### Change Log

| Date | Version | Description | Author |
| :--- | :--- |:--- |:--- |
| 2025-09-07 | 1.0 | Initial draft of the UI/UX Specification. | Sally (UX) |

## Information Architecture (IA)

### Site Map / Screen Inventory

This diagram shows the high-level relationship between the core screens of the application, branching out based on user roles after authentication.

```mermaid
graph TD
    A[Unauthenticated User] --> B(Login Screen);
    B --> C{Role-Based Redirect};

    C --> D[Tenant Dashboard];
    D --> D1(Property List);
    D --> D2(Create New Ticket);
    D --> D3(Ticket List & Details);

    C --> E[Supervisor Dashboard];
    E --> E1(All Tickets List);
    E --> E2(Technician Assignment View);
    E --> E3(Report & Quote Review);

    C --> F[Technician Dashboard];
    F --> F1(Assigned Tasks List);
    F --> F2(Inspection Report Form);
    F --> F3(Evidence Upload);

    C --> G[FMC Head Dashboard];
    G --> G1(User Management);
    G --> G2(Property Management);
    G --> G3(High-Level Analytics);

    subgraph Shared Screens
        S1(Account Settings);
        S2(Notification Center);
        S3(Logout);
    end

    D --> S1;
    E --> S1;
    F --> S1;
    G --> S1;

    BMad - Full Stack Team
Custom Gem

Show thinking
Of course. Here is the complete and final UI/UX Specification for Zariya FMC.

Please copy the text below and save it as docs/front-end-spec.md in your project folder. This is the document the Architect will need.

Markdown

# Zariya FMC UI/UX Specification

## Introduction

This document defines the user experience goals, information architecture, user flows, and visual design specifications for Zariya FMC's user interface. It serves as the foundation for visual design and frontend development, ensuring a cohesive and user-centered experience.

### Overall UX Goals & Principles

#### Target User Personas
While there are seven roles, our primary focus will be on the core users in the workflow:
* **The Tenant (Customer):** Needs a quick, simple, and reassuring way to report issues and track their status with minimal friction.
* **The Technician/Vendor:** Needs a clear, mobile-friendly view of their assigned tasks with all necessary details to perform their job efficiently.
* **The Supervisor:** Needs a powerful, at-a-glance dashboard to manage multiple tickets, oversee staff, and make quick decisions.

The experience for other roles (FMC Head, Procurement, etc.) will be optimized for their specific, less frequent tasks.

#### Usability Goals
* **Ease of Learning:** A new tenant should be able to submit their first ticket in under 2 minutes.
* **Efficiency of Use:** A supervisor should be able to triage and assign 10 new tickets in under 5 minutes.
* **Error Prevention:** The design will use guided workflows and clear confirmations to prevent incorrect data entry or accidental approvals.
* **Transparency:** At any point, a user should be able to understand the current status of a ticket and what the next step is.

#### Design Principles
1.  **Clarity Above All:** Prioritize clear, unambiguous language and visuals. Avoid jargon and complex layouts.
2.  **Role-Focused Simplicity:** Each user's interface will be tailored to their specific role, hiding irrelevant information to reduce cognitive load.
3.  **Transparent Progress:** Always make the status of a task or ticket obvious and easy to find.
4.  **Guided Actions:** Nudge users toward the next logical step in any workflow.
5.  **Trust Through Evidence:** Use features like photo uploads and OTP verification to build trust in the process for both tenants and FMCs.

### Change Log

| Date | Version | Description | Author |
| :--- | :--- |:--- |:--- |
| 2025-09-07 | 1.0 | Initial draft of the UI/UX Specification. | Sally (UX) |

## Information Architecture (IA)

### Site Map / Screen Inventory

This diagram shows the high-level relationship between the core screens of the application, branching out based on user roles after authentication.

```mermaid
graph TD
    A[Unauthenticated User] --> B(Login Screen);
    B --> C{Role-Based Redirect};

    C --> D[Tenant Dashboard];
    D --> D1(Property List);
    D --> D2(Create New Ticket);
    D --> D3(Ticket List & Details);

    C --> E[Supervisor Dashboard];
    E --> E1(All Tickets List);
    E --> E2(Technician Assignment View);
    E --> E3(Report & Quote Review);

    C --> F[Technician Dashboard];
    F --> F1(Assigned Tasks List);
    F --> F2(Inspection Report Form);
    F --> F3(Evidence Upload);

    C --> G[FMC Head Dashboard];
    G --> G1(User Management);
    G --> G2(Property Management);
    G --> G3(High-Level Analytics);

    subgraph Shared Screens
        S1(Account Settings);
        S2(Notification Center);
        S3(Logout);
    end

    D --> S1;
    E --> S1;
    F --> S1;
    G --> S1;
Navigation Structure
Primary Navigation: After login, most users will see a simple, persistent navigation bar (a sidebar on desktop, a tab bar on mobile). The links will be role-specific.

Tenant: Dashboard, My Tickets, Notifications, Settings.

Supervisor: Dashboard, All Tickets, Staff, Notifications, Settings.

Technician: My Tasks, Notifications, Settings.

Secondary Navigation: Contextual navigation will appear within specific sections. For example, on the main ticket list pages, users will have tabs or filters for different ticket statuses (e.g., "New", "In Progress", "Completed").

Breadcrumb Strategy: On desktop, breadcrumbs will be used for nested views (e.g., Home > Tickets > Ticket #12345) to provide clear context and easy navigation back to parent pages.

User Flows
Tenant Creates a Maintenance Ticket
User Goal: "As a Tenant, I want a user-friendly form to create a new maintenance ticket, so that I can provide all the necessary information easily."

Entry Points: Tenant Dashboard.

Success Criteria: A new ticket is saved with a "New" status, linked to the correct tenant and property, and the tenant sees a confirmation message.

Flow Diagram
Code snippet

graph TD
    A[Start] --> B[Tenant logs in];
    B --> C[Views Tenant Dashboard];
    C --> D[Clicks 'Create New Request'];
    D --> E[Fills in ticket details (Title, Description, Availability)];
    E --> F[Uploads photo of the issue];
    F --> G[Submits the form];
    G --> H{Is form valid?};
    H -- Yes --> I[Ticket is created in the system];
    I --> J[Displays 'Success!' confirmation message to Tenant];
    J --> K[End];
    H -- No --> L[Displays validation errors on the form];
    L --> E;
Edge Cases & Error Handling:
Invalid Data: If the user submits the form with missing required fields, inline error messages will appear.

Photo Upload Failure: If the photo fails to upload, a clear error message will be shown, allowing the user to retry without losing other entered data.

Submission Failure: If the ticket fails to submit due to a server or network error, a notification will appear asking the user to try again.

Supervisor Triage & Ticket Assignment
User Goal: "As a Supervisor, I want to see a dashboard of all new tickets for the buildings I manage, so that I can review them and assign them to a technician for inspection."

Entry Points: Supervisor Dashboard.

Success Criteria: A ticket with a "New" status is successfully assigned to a technician, its status updates to "Assigned for Inspection," and the technician is notified.

Flow Diagram
Code snippet

graph TD
    A[Start] --> B[Supervisor logs in];
    B --> C[Views Supervisor Dashboard];
    C --> D[Selects a 'New' ticket from the list];
    D --> E[Reviews ticket details (description, photo, etc.)];
    E --> F[Selects an available Technician from a dropdown list];
    F --> G[Clicks 'Assign for Inspection' button];
    G --> H{Is assignment valid?};
    H -- Yes --> I[System updates ticket status to 'Assigned for Inspection'];
    I --> J[System sends notification to the assigned Technician];
    J --> K[Displays 'Assignment Successful' confirmation to Supervisor];
    K --> L[End];
    H -- No --> M[Displays error message (e.g., 'Technician not available')];
    M --> E;
Edge Cases & Error Handling:
No Available Technicians: The assignment UI will clearly indicate if no technicians are available.

Ticket Already Assigned: The system will prevent duplicate assignments if two supervisors act simultaneously.

Submission Failure: A network or server error during assignment will result in a retryable error message.

Technician Inspection & Reporting
User Goal: "As a Technician, I want a form to submit my inspection findings, so that I can inform the supervisor of the necessary work, materials, and costs."

Entry Points: Technician's "My Tasks" dashboard.

Success Criteria: The technician successfully submits a complete inspection report, the ticket status updates to "Inspection Complete," and the supervisor is notified.

Flow Diagram
Code snippet

graph TD
    A[Start] --> B[Technician logs in];
    B --> C[Views 'My Tasks' Dashboard];
    C --> D[Selects an assigned ticket];
    D --> E[Views ticket details and clicks 'Submit Inspection Report'];
    E --> F[Fills out inspection form];
    F --> G{Is the work paid?};
    G -- Yes --> H[Enters Quote and Materials List];
    G -- No --> I[Confirms 'Free of Charge'];
    H --> J[Submits Report];
    I --> J;
    J --> K{Is form valid?};
    K -- Yes --> L[System updates ticket status to 'Inspection Complete'];
    L --> M[System notifies Supervisor];
    M --> N[Displays 'Report Submitted' confirmation to Technician];
    N --> O[End];
    K -- No --> P[Displays validation errors];
    P --> F;
Edge Cases & Error Handling:
Missing Information: The form will have required fields (e.g., a quote is required if "Paid" is selected).

Network Issues: The app should ideally save report data locally and sync when a connection is available (a post-MVP feature).

Quote Approval & Job Completion
User Goal: To provide a seamless and transparent process for tenants to approve work, and for technicians to execute the job and get final, verified confirmation of completion.

Entry Points: Supervisor Dashboard (with a ticket in "Inspection Complete" status).

Success Criteria: An approved job is completed by the technician, verified via OTP by the tenant, and the ticket is moved to a "Completed" status with a final rating.

Flow Diagram
Code snippet

graph TD
    subgraph Supervisor
        A[Start: Supervisor reviews Inspection Report] --> B{Is work 'Paid'?};
    end

    subgraph Tenant
        C[Receives notification with Quote] --> D[Views Quote in App];
        D --> E{Approve or Reject?};
        H[Receives OTP via Email] --> I[Gives OTP to Technician];
        K[Rates the service (1-5 stars)];
    end

    subgraph Technician
        F[Receives 'Job Approved' notification] --> G[Starts work & uploads 'before/after' photos];
        G --> J[Marks work as complete, triggering OTP];
        J --> L[Enters OTP to verify];
    end

    B -- No (Free) --> F;
    B -- Yes (Paid) --> C;
    E -- Reject --> M[End: Ticket Closed];
    E -- Approve --> F;
    L --> K;
    K --> N[End: Ticket Completed];
Edge Cases & Error Handling:
No Tenant Response: A reminder notification will be sent after a set period.

Incorrect OTP: The system will allow a limited number of retries before locking and notifying a supervisor.

Tenant Unhappy: For the MVP, if the tenant refuses to provide the OTP, the ticket remains open for the supervisor to handle manually.

Wireframes & Mockups
The final, high-fidelity visual design and prototypes will be created and maintained in an external design tool (e.g., Figma). This document provides the foundational UX, but the design tool will be the source of truth for all visual specifications.

Component Library / Design System
Design System Approach
A pre-built, production-ready component library (e.g., Shadcn/ui, Material UI) will be used to accelerate development and ensure consistency and accessibility. A custom component library will not be built for the MVP.

Core Components
The MVP will require at least the following components:

Button

Input Fields (Text, Password, Text Area, File Upload)

Card

Modal / Dialog

Data Table

Dropdown / Select

Notification / Toast

Branding & Style Guide
This section is to be determined. The Architect and Developers will use a default theme from the chosen component library until a final brand identity is provided.

Visual Identity & Color Palette: TBD

Typography: TBD (Recommendation: Inter or Poppins)

Iconography: TBD (Recommendation: Lucide Icons)

Accessibility Requirements
Compliance Target
The application will be developed to meet the Web Content Accessibility Guidelines (WCAG) 2.1 Level AA standard.

Key Requirements
Visual: Minimum color contrast of 4.5:1, visible keyboard focus indicators, and support for text resizing up to 200%.

Interaction: Full keyboard navigability, screen reader compatibility, and minimum touch target sizes of 44x44 pixels.

Content: All meaningful images will have descriptive alt text, pages will use a logical heading structure, and all form inputs will have associated labels.

Testing Strategy
Accessibility will be checked via automated tools (e.g., Axe), manual keyboard testing, and periodic manual screen reader testing of key flows.

Responsiveness Strategy
Breakpoints
Breakpoint	Min Width	Target Devices
Mobile	(default)	Most smartphones
Tablet	768px	iPads, tablets
Desktop	1024px	Laptops, desktop monitors
Wide	1440px	Large desktop monitors

Export to Sheets
Adaptation Patterns
Layout: A single-column mobile layout will expand to multi-column layouts on larger screens.

Navigation: A mobile bottom tab bar will expand to a desktop sidebar.

Content Priority: The mobile view will prioritize critical content and actions.

Animation & Micro-interactions
Motion Principles
Functional & Purposeful: Animations will be used to guide attention or provide feedback.

Subtle & Quick: Motion will be fast (under 300ms) to feel responsive.

Consistent: Animation patterns will be used consistently.

Key Animations & Micro-interactions
State Transitions: Gentle cross-fades for status changes.

Loading States: Skeleton loaders will be used when fetching data.

Action Feedback: Subtle visual changes on buttons when clicked.

Modal Entry: Dialogs will gently scale into view.

Performance Considerations
Performance Goals
Page Load (LCP): < 2.5 seconds.

Interaction Response (INP): < 100 milliseconds.

Animation FPS: 60 FPS.

Design Strategies to Achieve Goals
Image Optimization: User-uploaded images will be compressed and served in modern formats.

Lazy Loading: Off-screen images and UI components will be loaded on demand.

Code Splitting: The application code will be split by route/page.

Skeleton Screens: Used to improve perceived performance during data loading.