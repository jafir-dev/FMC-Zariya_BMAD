Project Brief: Zariya FMC
Executive Summary
Zariya FMC is a full-stack Progressive Web App (PWA) designed for Facility Management Companies (FMCs) to streamline the entire lifecycle of maintenance requests. The platform addresses the core problem of inefficient, non-transparent communication and workflow management between tenants, FMC staff, and vendors. The target market includes FMCs of all sizes in the UAE, their multi-role staff, building association owners, and the tenants of the properties they manage. Zariya FMC's key value proposition is a unified, user-friendly platform that digitizes the maintenance workflow, enhancing efficiency, communication, and transparency for all stakeholders through role-based access, multi-channel notifications, and powerful reporting.

Problem Statement
Currently, Facility Management Companies often rely on manual or fragmented systems (like phone calls, emails, or basic ticketing software) to manage tenant maintenance requests. This leads to significant operational inefficiencies, including:

Lack of Transparency: Tenants have no clear visibility into the status of their requests, estimated costs, or timelines.

Poor Communication: Information is often lost or miscommunicated as requests are passed between supervisors, technicians, procurement teams, and third-party vendors.

Operational Delays: Manual processes for approvals, quotations, and material procurement cause significant delays in resolving issues.

No Centralized Data: FMCs lack the data to track staff performance, identify recurring maintenance issues, or gain insights into operational costs and efficiency.

This results in tenant dissatisfaction, high operational overhead for the FMC, and an inability to perform proactive or predictive maintenance.

Proposed Solution
Zariya FMC is a comprehensive PWA that provides a centralized and automated platform for managing maintenance workflows. The solution is built around a role-based system for seven distinct user types, ensuring each user only sees relevant information and actions.

The core workflow allows tenants to submit detailed tickets with media attachments. Supervisors can then assign staff for inspection, who can report back with findings and quotes. The system manages the entire approval chain, including tenant approval for paid work and internal procurement processes. Technicians receive assignments, document their work with before/after photos, and close out the job with a secure OTP verification from the customer.

Key features include a unified notification center (in-app, email, push, SMS, WhatsApp), AI-powered analytics for predictive maintenance, online payment integration, and robust dashboards for monitoring and reporting.

Target Users
Primary User Segments:

Customer (Tenant): The end-user living in the property who initiates maintenance requests.

FMC Supervisor: Manages a building's operations, assigning tickets and overseeing staff.

FMC Technician: The staff member who inspects and carries out the maintenance work.

Secondary User Segments:

FMC Head: Manages multiple buildings under a single FMC, requiring high-level oversight.

FMC Procurement: Manages the acquisition of materials required for jobs.

Building Association Owner: Has oversight of a building and may be involved in escalations or approvals.

Third-Party Vendors: External specialists assigned to specific jobs (e.g., ELV systems).

Goals & Success Metrics
Business Objectives

Successfully launch a SaaS product with a tiered pricing model (Starter, Pro, Enterprise) to capture the UAE FMC market.

Reduce the average ticket resolution time for FMCs by 30% within the first year of use.

Achieve a 90% customer satisfaction score based on post-job ratings.

User Success Metrics

High adoption rate across all 7 user roles.

Increased first-time fix rate by technicians.

Reduced number of tenant follow-up inquiries regarding ticket status.

Key Performance Indicators (KPIs)

Monthly Active Users (MAU) and user retention rate.

SLA (Service Level Agreement) compliance rate for ticket statuses.

Average rating score per technician and per FMC.

Conversion rate from free trial (if offered) to paid plans.

MVP Scope
To ensure a focused initial launch, the Minimum Viable Product (MVP) will include the core functionality necessary to validate the workflow.

Core Features (Must Have):

User Management: Secure login and role-based access for all 7 user types. FMCs can add properties, staff, and tenants.

Core Ticket Workflow:

Tenant can create a ticket with a title, description, photo, and availability.

Supervisor can view new tickets and assign a technician for inspection.

Technician can view ticket details, inspect the issue, and submit a report (indicating if the job is free or requires a quote).

Supervisor can view the report and communicate the quote to the tenant (initially handled outside the app).

Tenant can approve or decline the work.

Technician can complete the work, upload an "after" photo, and close the ticket.

Basic Notifications: In-app and email notifications for major status changes (e.g., ticket created, technician assigned, work complete).

Property & Contract Management: FMCs can manage tenant properties and view tenancy contract expiry dates.

Simple Dashboard: A basic view for users to see their open and closed tickets.

Out of Scope for MVP:

AI Predictions & Advanced Analytics.

Integrated Online Payments & Invoicing (quotes and payments will be handled offline).

WhatsApp and SMS notification channels.

Full Procurement & Third-Party Vendor modules (can be simulated via supervisor actions).

Advanced ticket statuses, escalation, and SLA management.

Offline support and geolocation features.

In-app chat and dispute resolution flows.

A public-facing landing page with pricing (can be a separate, simple static page).

Post-MVP Vision
Phase 2 Features: Introduce integrated online payments, a full third-party vendor portal, the procurement module, advanced reporting dashboards, and the unified notification center with SMS/WhatsApp.

Long-term Vision: Implement the AI analytics engine for predictive maintenance. Build out advanced features like offline support, geo-location, dispute resolution workflows, and deeper integration with building management systems.

Expansion Opportunities: Expand into related services like property management, rental payments, or smart home integrations.

Technical Considerations
Platform Requirements: The application must be a Progressive Web App (PWA) to ensure accessibility on both mobile and desktop devices without requiring an app store installation.

Technology Preferences: A modern full-stack framework is recommended (e.g., MERN/T3 Stack with Next.js/React for the frontend and Node.js for the backend).

Architecture Considerations: A robust Role-Based Access Control (RBAC) system is a foundational requirement. The architecture must be designed to be scalable and secure.

Security/Compliance: The system must adhere to UAE's Personal Data Protection Law (PDPL). This includes secure data storage, user consent for data handling (especially media), and comprehensive audit trails for all actions.

Constraints & Assumptions
Constraints:

The system must be compliant with UAE data privacy and storage regulations.

Key Assumptions:

FMCs and their staff have access to and are willing to use a modern web application.

Tenants are comfortable interacting with a digital platform for maintenance requests.

A stable internet connection will be available for most operations in the MVP.

Risks & Open Questions
Key Risks:

Scope Creep: The extensive feature list presents a high risk of expanding the MVP beyond a manageable size.

User Adoption: Onboarding and training all seven user types will be a significant challenge.

Workflow Complexity: The real-world maintenance workflow may have nuances not captured, requiring significant iteration.

Open Questions:

What are the preferred payment gateways for the UAE market?

Are there any existing accounting or ERP systems that FMCs commonly use and would require integration?

What are the typical SLA timelines that need to be configured for ticket escalations?