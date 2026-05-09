# PRD: Multi-Tenant Telehealth Commerce and Operations Platform with White-Labeled Customer Portal

## 1. Document Overview

### Working Title
Multi-Tenant Telehealth Commerce and Operations Platform with White-Labeled Customer Portal

### Document Purpose
This PRD defines the product vision, scope, core concepts, platform modules, user roles, lifecycle models, MVP scope, and open questions for a multi-tenant platform that enables clinics to launch and manage health-related product programs by connecting to third-party doctor/provider networks and third-party pharmacy partners.

### Product Summary
The platform is not intended to be a primary clinical system or full care-delivery platform. Instead, it acts as a commerce, operations, orchestration, and program management layer that helps clinics launch and scale health-related offerings through configurable intake, product catalog management, pricing, subscriptions, order synchronization, provider/pharmacy routing, customer portal experiences, and analytics.

The platform operates as two connected surfaces:
* a shared internal admin and operations platform used by platform teams, clinic admins, support, finance, and operators
* a white-labeled customer-facing experience used by end customers to enroll, view and manage their purchases, medications, subscriptions, and progress
	
The platform performs the operational middle work between clinics, customers, doctor networks, pharmacies, and payments infrastructure.

### Background
The business has already proven the operating model through prior work across a single platform, telehealth companies, and an e-pharmacy. The next phase is to generalize and expand those capabilities into a reusable software product that supports multiple tenants, clinics, branded experiences, programs, and partner networks.

---

## 2. Product Definition

### Product Vision
Enable clinics and telehealth operators to launch and operate branded telehealth-enabled product programs without having to build and maintain their own intake workflows, customer portal, product and pricing engine, subscription logic, order operations layer, provider/pharmacy integration stack, or revenue-share reporting workflows.

### Product Positioning
This platform is best positioned as a **multi-tenant telehealth commerce and operations platform for clinics with a white-labeled customer-facing experience**.

It is designed for organizations that want to:
* launch branded health-related offerings
* manage products and subscriptions
* connect to external providers and pharmacies
* operationalize intake-to-order workflows
* improve visibility into performance and costs
* scale across multiple programs and brands
	
### Core Value Proposition
Clinics use the platform to centralize and standardize the operational, commercial, financial, and growth layers of telehealth-enabled product programs while continuing to rely on third-party doctor/provider networks and pharmacy partners for clinical decisioning and fulfillment.

### What the Platform Offers
The platform provides:
* multi-tenant deployment
* a shared internal admin and operations platform
* a white-labeled customer-facing portal and storefront experience
* productized program management
* configurable intake and qualification flows
* customer portal and dashboard experiences
* catalog, pricing, discount, subscription, and billing management
* provider network and pharmacy partner orchestration
* order synchronization and exception handling
* clinic, customer, and support operations tooling
* analytics, cost visibility, and revenue-share reporting
* conversion optimization, reminders, and marketing orchestration
	
### What the Platform Is Not
The platform is not intended in its initial scope to:
* function as a full EHR
* replace provider clinical systems
* replace pharmacy dispensing systems
* directly deliver care
* own deep clinical documentation workflows beyond what is needed to support partner coordination and product operations
* provide fully custom white-labeled internal admin experiences for each tenant in MVP
	
---

## 3. Goals and Non-Goals

### Goals
* Support a multi-tenant model for multiple clinics and branded customer experiences
* Support a white-labeled customer-facing portal model for clinics
* Standardize how health-related programs are configured and launched
* Centralize product, pricing, discount, subscription, and promotional management
* Provide a reusable orchestration layer for provider and pharmacy partners
* Improve operational visibility across enrollments, orders, subscriptions, and partner sync events
* Reduce manual work for clinic operations and support teams
* Improve conversion, retention, and program performance through analytics and lifecycle marketing
* Create a scalable software product from an already proven operating model
	
### Non-Goals
* Building a comprehensive clinical care delivery platform
* Replacing provider scheduling, charting, or clinical record systems
* Building a pharmacy dispensing system
* Supporting every possible customization via custom code in V1
* Creating a broad healthcare network marketplace in the first release
* Owning insurance claims, payer adjudication, or revenue cycle management in the initial phase
* White-labeling the internal admin, support, and operations platform in MVP
	
---

## 4. Target Users and Personas

### Platform Admin
Owns platform-wide configuration, tenant creation, feature controls, partner templates, support escalations, and system oversight.

### Tenant Admin
Manages a tenant’s configuration, users, permissions, partner assignments, platform settings, analytics scope, and operational configuration.

### Clinic Admin
Manages the clinic’s setup, branded customer experience, active programs, staff users, reporting access, and operational settings.

### Clinic Operator
Manages day-to-day commercial and operational activity for a clinic-branded experience, including products, pricing, discounts, subscriptions, customer views, order visibility, and issue handling.

### Support / Operations User
Handles customer support, order issues, subscription issues, sync failures, timeline review, and operational exception management.

### Marketing / Growth User
Reviews program performance, funnel analytics, promotional performance, merchandising configuration, reminder flows, and lifecycle marketing performance.

### Finance / Analytics User
Reviews revenue, Stripe Connect activity, platform percentages owed, clinic share, costs, discounts, partner performance, subscription metrics, and exportable operational reporting.

### External Partner User (Optional Phase)
Limited visibility role for provider or pharmacy partner contacts where needed.

### End Customer
Completes intake, enrolls in programs, views offerings, manages subscriptions, views medications and plan details, tracks progress, and monitors order status.

---

## 5. Core Concepts and Object Model

This section defines the primary entities that make up the platform and the relationship model between them.

### 5.1 Core Business Hierarchy

#### Tenant
The top-level account and isolation boundary.
A tenant contains configuration, users, programs, pricing settings, partner assignments, analytics scope, and operational data.
The tenant is the account that can enable and manage multiple clinics under a single shared account boundary.

#### Clinic
A clinic operated within a tenant account.
A clinic is a clinic-level operational and customer-facing unit under the tenant and can operate its own branded experience in the platform.

#### Branded Experience
A clinic-specific customer-facing storefront, intake funnel, and portal experience presented to end customers under the clinic’s brand.
A branded experience manages how offerings are displayed and sold, how the intake flow is presented, and how the authenticated customer portal is themed and experienced.

In MVP, a clinic is generally expected to have a single branded experience and corresponding customer portal, even if the model is left flexible for future expansion.

A branded experience owns customer-facing branding such as:
* logo
* colors
* domain or subdomain
* messaging
* legal text and disclaimers
* portal presentation and content
	
#### Program
A sellable health-related offering or service line.
Examples may include weight management, skincare, ED, hair loss, wellness membership, or other productized programs.
A program groups the core configuration needed to operate an offering, including intake, products, pricing, subscriptions, partner routing, communications, and analytics.

### 5.2 Customer Flow Objects

#### Customer
The end user / patient / buyer participating in one or more programs.
Stores profile, contact information, history, enrollments, subscriptions, orders, communications, and portal-visible medication and progress state.

#### Intake Form
A configurable form or workflow used to collect customer information for a program.

#### Form Submission
A specific submitted instance of an intake form by a customer.
Includes answers, timestamps, status, version reference, and downstream routing results.

#### Program Enrollment
The customer’s participation record within a program.
Represents their relationship to the offering and may include status, timeline, partner routing state, and current eligibility or approval outcome.

#### Approved Product Plan
A normalized record representing the approved or recommended product configuration for a customer within a program.
This is intentionally lighter than a deep clinical treatment object and focuses on product operations and fulfillment alignment.

In the customer portal, this may be presented as a medication plan or medications view rather than exposing internal terminology directly.

### 5.3 Commerce Objects

#### Product
A sellable item within the platform.
May map to one or more external provider or pharmacy representations.

#### Product Variant
A specific version or option of a product, such as dosage, size, duration, or package type.

#### Category
A merchandising and organizational grouping for products.

#### Bundle
A sellable grouping of products or components.

#### Price Rule
A configurable rule that determines how pricing is applied.
May support one-time pricing, recurring pricing, tiered pricing, intro pricing, or overrides.

#### Discount Code
A promotional or pricing adjustment entity with scope, time window, and eligibility rules.

#### Subscription
A recurring purchase or fulfillment agreement tied to a customer, program, and product/product plan.
Includes cadence, status, renewal logic, and history.

### 5.4 Partner and Integration Objects

#### Provider Partner
A third-party provider organization or telehealth partner connected to the platform.

#### Pharmacy Partner
A third-party pharmacy or fulfillment partner connected to the platform.

#### Partner Connection
A configuration object that defines how a given tenant, clinic, branded experience, or program connects to a provider or pharmacy partner.
Includes mapping, routing, credentials references, and supported scope.

#### Sync Event
A normalized record of an outbound or inbound integration event.
Includes payload references, source system, destination system, status, retries, timestamps, and error details.

### 5.5 Operations Objects

#### Order
A customer purchase or fulfillment-triggering transaction linked to products, subscriptions, programs, and external partner states.

#### Fulfillment Event
A recorded update related to order processing, pharmacy handoff, shipment, delivery, refill, or exception handling.

#### Support Case
An internal service or operations record used to track issues, follow-up, and resolution.

#### Analytics Event
A tracked business or operational event used for reporting, dashboards, and funnel analysis.

#### Campaign
A marketing or lifecycle communication initiative targeted to a customer segment, program, or commercial goal.

#### Reminder / Notification Rule
A configuration object that defines when and how reminders, follow-up prompts, renewal nudges, refill prompts, or promotional messages are sent.

#### Audience Segment
A reusable customer grouping used for campaigns, reminders, conversion efforts, and retention initiatives.

---

## 6. Proposed Object Hierarchy and Relationship Model

### High-Level Hierarchy
* Tenant
	* Clinic
		* Branded Experience
			* Program
				* Intake Forms
				* Products
				* Price Rules
				* Discount Codes
				* Provider Partner Connections
				* Pharmacy Partner Connections
			* Customers
				* Form Submissions
				* Program Enrollments
				* Approved Product Plans
				* Subscriptions
				* Orders
	
### Core Relationship Principles
* One tenant can have many clinics.
* Tenant is the primary account boundary, and clinics are enabled and managed within that tenant.
* One clinic can have one branded experience in MVP.
* One branded experience can have many programs.
* One program can have many products, forms, price rules, and partner connections.
* One customer can participate in multiple programs.
* One program enrollment can be associated with one or more approved product plans over time.
* One subscription may generate multiple orders over its lifecycle.
* One internal product may map to multiple external partner SKUs or representations.
* Provider and pharmacy partners may be assigned at different scopes depending on configuration needs.
	
### Key Relationship Questions to Confirm Later
* Whether the branded experience layer should remain structurally optional in future phases or be required for all clinics
* Whether partner connections should primarily live at the tenant, clinic, branded experience, or program level
* Whether pricing rules are inherited top-down or assigned only at the program/product level
* Whether customers are unique platform-wide within a tenant or unique per branded experience context
	
---

## 7. Product Modules and Functional Requirements

### 7.1 Multi-Tenant Management

#### Purpose
Provide the foundation for tenant isolation, shared internal platform operation, and branded customer deployment.

#### Functional Requirements
* Create and manage tenants
* Support tenant-scoped users, permissions, and feature access
* Support tenant-specific legal text, disclaimers, and communication templates
* Support tenant-level settings for programs, products, pricing, and integrations
* Support environment or sandbox configuration for testing and onboarding
	
#### Key Considerations
* Maintain clear tenant data separation
* Support customer-facing brand configuration without requiring white-labeling of internal admin surfaces
* Avoid unbounded custom UI requests through configuration controls
	
### 7.2 Clinic and Branded Experience Management

#### Purpose
Manage clinic customers and the customer-facing branded experiences they operate within the platform.

#### Functional Requirements
* Create and manage clinics
* Create and manage branded experiences under clinics
* Store business metadata, contacts, operational status, and contract metadata
* Store payout and revenue-share metadata for clinics
* Assign programs, users, and partner connections
* Track onboarding and launch readiness
* Support clinic-level reporting and visibility
* Support branded customer portals, storefront-like experiences, and intake entry points under clinics
* Configure branded experience elements including domain/subdomain, logo, colors, customer-facing messaging, and legal text
	
#### Key Considerations
* In MVP, a clinic is generally expected to have one customer-facing branded experience
* Define ownership of pricing and operational settings between clinic and branded experience scopes
	
### 7.3 Program Management

#### Purpose
Make programs the central operational and commercial abstraction for sellable offerings.

#### Functional Requirements
* Create and manage programs
* Assign products, forms, pricing, subscriptions, and partner connections to programs
* Define program status and availability
* Configure communications and customer flow logic per program
* Support program-level analytics and performance reporting
* Support upsell, cross-sell, or multi-program relationships
	
#### Key Considerations
* Program should be treated as a first-class object, not just a tag on products
* Program scope will likely drive most merchandising, routing, and reporting behavior
	
### 7.4 Intake and Form Builder

#### Purpose
Collect customer inputs and support qualification, routing, and conversion workflows.

#### Functional Requirements
* Drag-and-drop form builder
* Field templates and reusable form components
* Conditional logic and branching
* Program-specific and tenant-specific form versions
* Validation rules and attestation capture
* Save draft and resume
* File upload support if needed
* Submission history and version-aware rendering
* Form completion analytics and abandonment visibility
	
#### Key Considerations
* Treat intake as both a data collection and conversion system
* Versioning and downstream compatibility will be important
	
### 7.5 White-Labeled Customer Portal, Customer, Enrollment, and Medication Visibility

#### Purpose
Provide the customer-facing portal experience and a normalized operational view of customer participation, approved product outcomes, medication details, and progress through the fulfillment lifecycle.

#### Functional Requirements
* White-labeled authenticated customer dashboard presented at the branded experience level
* Customer dashboard overview with medications, plans, orders, and subscription status
* Purchases and order history visibility
* Medication visibility including prescribed medications, dosage/strength, plan details, shipment status, refill status, and basic instructions where available
* Billing and payments visibility including invoices, receipts, and upcoming payment schedule
* Secure chat or messaging visibility with providers/support where enabled
* Customer profile and history view
* Program enrollment records and statuses
* Intake submission history
* Approved product plan visibility
* Progress visibility showing where the customer is in the operational workflow, including statuses such as intake submitted, awaiting provider review, approved, sent to pharmacy, in fulfillment, shipped, delivered, refill upcoming, or follow-up needed
* Timeline of customer and operational events
* Communication history visibility
* Relationship to subscriptions and orders
	
#### Key Considerations
* Favor a practical operational model instead of recreating deep clinical treatment records
* The portal should show customers what they were prescribed, what is active, what is in process, and what happens next
* Progress in MVP should focus on medication/order/workflow progress rather than broader health outcome tracking
* Patient portal capabilities should align with the documented flow from payment through dashboard activation
	
### 7.6 Product Catalog Management

#### Purpose
Manage the sellable catalog across programs, tenants, clinics, and partner mappings.

#### Functional Requirements
* Create and manage products and variants
* Create categories and bundles
* Assign products to programs
* Store product metadata, content, instructions, and tags
* Support internal-to-external SKU mapping
* Support visibility controls and availability states
* Support archived/inactive product handling
* Store standard cost data for analytics
	
#### Key Considerations
* Products may need multiple external representations
* Product, variant, and bundle modeling should remain flexible without becoming overly custom
	
### 7.7 Pricing, Promotions, and Subscription Management

#### Purpose
Support monetization models across one-time and recurring offerings.

#### Functional Requirements
* Configure one-time and subscription pricing
* Configure intro offers and recurring pricing
* Define price rules by tenant, clinic, branded experience, program, or product scope as allowed
* Create discount codes with effective dates and constraints
* Support bundles, promotional windows, and recurring plan structures
* Support subscription pause, skip, cancel, and renewal logic
* Maintain pricing and subscription history over time
	
#### Key Considerations
* This module can become one of the most complex in the platform
* Clear rules on overrides, inheritance, and grandfathering are needed
	
### 7.8 Provider Partner Management

#### Purpose
Manage connections to external provider organizations and normalize their role in the workflow.

#### Functional Requirements
* Register provider partners
* Assign provider partners to supported programs or scopes
* Configure payload mappings and submission workflows
* Track request status and partner responses
* Support fallback routing or reassignment where needed
* Track partner health and SLA metrics
	
#### Key Considerations
* Focus on operational integration, not clinical ownership
* Standardization across partners will reduce support burden
	
### 7.9 Pharmacy Partner Management

#### Purpose
Manage fulfillment-oriented connections to external pharmacy partners.

#### Functional Requirements
* Register pharmacy partners
* Configure partner-specific product and SKU mappings
* Assign pharmacy partners to programs or routing scopes
* Transmit orders and receive updates
* Track shipment and fulfillment status when available
* Track refill-related status when available
* Monitor partner sync health and exceptions
	
#### Key Considerations
* Product mapping and status normalization are likely key complexity areas
* Support for fallbacks and out-of-stock logic may become important later
	
### 7.10 Order Management and Synchronization

#### Purpose
Provide operational visibility and control for purchases, subscriptions, and external order workflows.

#### Functional Requirements
* Create and manage orders
* Maintain internal order status timelines
* Normalize external partner statuses
* Support subscription-generated orders
* Handle retries, duplicates, and synchronization exceptions
* Provide reconciliation dashboards and intervention queues
* Support refunds, replacements, and manual issue resolution
	
#### Key Considerations
* A canonical internal order model is required
* This is likely one of the highest-value modules for internal operations
* Order and fulfillment states should be translatable into understandable customer-facing progress states in the portal
	
### 7.11 Analytics and Reporting

#### Purpose
Turn operational, commercial, and marketing data into actionable visibility for tenants, clinics, and internal teams.

#### Functional Requirements
* Tenant, clinic, and program dashboards
* Revenue and order reporting
* Intake and conversion funnel reporting
* Subscription retention and churn reporting
* Discount and promotion reporting
* Reminder and campaign performance reporting
* Cost and margin visibility where available
* Partner performance and error reporting
* Export capabilities and scheduled reporting support later
	
#### Key Considerations
* Analytics can be a major differentiator
* Define event instrumentation early
	
### 7.12 Conversion Optimization and Marketing Orchestration

#### Purpose
Help tenants and clinics improve conversion, retention, reorder behavior, and customer lifetime value through configurable reminders, promotional messaging, and lifecycle marketing.

#### Functional Requirements
* Create and manage reminder and marketing campaigns
* Define trigger-based reminders for incomplete intake, abandoned checkout, pending renewal, refill timing, subscription reactivation, and reorder prompts
* Support audience segmentation by tenant, clinic, program, customer state, subscription state, order history, and campaign behavior
* Configure message templates and channel rules for email, SMS, push, or internal notification integrations where supported
* Support time-based and event-based campaign triggers
* Support promotional messaging tied to products, programs, discounts, and seasonal offers
* Track campaign delivery, open, click, conversion, unsubscribe, and suppression states where available
* Associate campaigns to commercial goals such as conversion lift, renewal lift, reorder lift, or cross-sell
* Support basic experimentation such as A/B variants in later phases
	
#### Key Considerations
* This module should balance growth functionality with compliance and customer experience controls
* Segmentation, suppression rules, frequency limits, and opt-in/opt-out handling will be important
* The platform should distinguish operational reminders from promotional marketing flows
* Customer-facing communications should align with branded experience theming and messaging rules
	
### 7.13 Admin and Support Tooling

#### Purpose
Support internal teams and clinic operators in managing exceptions and customer issues.

#### Functional Requirements
* Global and scoped search
* Timeline inspection
* Order and subscription support actions
* Support notes and reason tagging
* Safe impersonation or read-as views where allowed
* Retry and resend actions for sync-related tasks
* Internal audit log access based on permissions
	
#### Key Considerations
* Good support tools reduce labor and improve reliability
* This should not be treated as an afterthought
* These internal tools do not require white-labeling in MVP
	
---

## 8. Lifecycle and State Models

### 8.1 Program Enrollment Lifecycle (Draft)
Potential states:
* Draft
* Intake In Progress
* Submitted
* Under Review / Pending Partner
* Approved
* Requires Follow-Up
* Rejected / Not Eligible
* Converted to Active Product Plan
* Inactive / Closed
	
### 8.2 Approved Product Plan Lifecycle (Draft)
Potential states:
* Proposed
* Approved
* Active
* Updated
* Replaced
* Expired
* Closed
	
### 8.3 Subscription Lifecycle (Draft)
Potential states:
* Pending Activation
* Active
* Paused
* Past Due
* Renewal Pending
* Cancelled
* Completed
	
### 8.4 Order Lifecycle (Draft)
Potential states:
* Draft
* Submitted
* Sent to Partner
* Confirmed
* In Fulfillment
* Shipped
* Delivered
* Delayed / Exception
* Cancelled
* Refunded
* Closed
	
### 8.5 Sync Event Lifecycle (Draft)
Potential states:
* Queued
* Sent
* Acknowledged
* Succeeded
* Partial Success
* Failed
* Retry Scheduled
* Escalated
* Resolved
	
### Notes
These lifecycle states are intentionally early drafts and should be refined during product and engineering design.

Customer-facing progress states in the portal may be derived from these underlying lifecycle models and simplified for clarity.

Additional customer-frontend shell guidance for how `BrandedExperience` and `Program` should shape the future portal experience should be documented when that customer-facing slice is scoped.

---

## 9. Permissions and Access Model

### Core Role Groups
* Platform-level administrators
* Tenant administrators
* Clinic administrators
* Clinic operators
* Support / operations users
* Analytics / finance users
* Limited partner users (optional)
* End customers
	
### Access Principles
* Access should be scoped by role and organizational level
* Sensitive customer and health-adjacent data should be limited by least privilege
* Support and admin actions should be logged
* Read and write permissions should be separable where useful
* End customer access should be restricted to the branded experience and their own records, subscriptions, orders, medication visibility, and progress information
	
### Questions to Resolve
* Whether support users can act across all clinics within a tenant
* Whether analytics users can access customer-level records or only aggregated reporting
* Whether external partner users require portal access in early phases
	
---

## 10. Non-Functional Requirements

### Multi-Tenancy
* Strict tenant isolation
* Tenant-scoped configuration and data access
* Support for future tenant-level feature flags and rollout controls
	
### Reliability
* Resilient integration handling
* Retries and reconciliation for sync failures
* Monitoring for partner connectivity issues
	
### Auditability
* Record operational actions, status changes, and integration events
* Maintain historical visibility for pricing, forms, and subscription changes
	
### Scalability
* Support more tenants, clinics, programs, and integrations without requiring new custom code for each launch
	
### Security
* Secure access controls
* Secure handling of customer and health-adjacent data
* Secure partner credentials and integration secrets management
	
### Performance
* Responsive admin and operator experiences
* Searchable operational records
* Support dashboards that remain usable at scale
* Responsive customer-facing portal experiences across devices
	
### White-Label Delivery
* Support branded customer-facing configuration at the branded experience level
* Support domain or subdomain mapping for customer-facing experiences
* Support configurable customer-facing theming within bounded design controls
* Do not require white-labeling of internal admin, support, or operator interfaces in MVP
	
---

## 11. MVP Scope

### MVP Objective
Deliver the first reusable version of the platform foundation that supports multi-tenant accounts, clinics within each tenant, branded experiences under clinics, program structure under branded experiences, operator access control, and the shared internal workspace needed to expand into intake, commerce, partner routing, and customer-facing portal operations.

### In Scope for Current Foundation Slice
* Multi-tenant account model
* Shared internal admin and operations platform
* Tenant management
* Tenant membership and operator access control
* Clinic management under tenant
* Clinic membership and clinic-scoped access control
* Authentication, session bootstrap, and initial tenant onboarding
* Simple operator workspace shell and navigation
* Invitation and membership management APIs
* One branded experience per clinic for the current foundation slice
* Branded experience management with first-pass customer-facing brand fields
* Program structure management under branded experiences
* Permission-aware workspace route guards for tenant, clinic, branded-experience, and program routes
* Deterministic seed data and browser coverage for the current workspace foundation
	
### Deferred To Later Product Phases
* White-labeled customer-facing routing and host-based branded resolution
* Intake form builder with conditional logic
* Customer profiles and enrollment records
* Approved product plan visibility
* Product catalog and variant management
* Pricing rules and discount codes
* Subscription basics
* Provider and pharmacy partner connection management
* Order management and synchronization visibility
* Admin/support tools for search, timeline, and exception handling
* Foundational dashboards and reporting
* White-labeled customer portal for purchases, medications, subscriptions, billing, and progress visibility
* Branded customer-facing domain or subdomain setup, messaging surfaces, and theming beyond the first branded-experience fields
* White-labeled internal admin interfaces
* Deep UI page-builder level customization
* Extensive external partner self-service portals
* Advanced workflow automation builder
* Broad marketplace/discovery features
* Complex insurance or payer workflows
* Full video visit or synchronous care delivery experiences
* Sophisticated financial forecasting or invoice automation
* Deep health outcomes tracking or full clinical charting within the customer portal
* Multiple branded customer portals per clinic in MVP
	
---

## 12. Phase 2 / Future Opportunities

* More advanced pricing engine and promotion logic
* More advanced subscription lifecycle tools
* Richer analytics and benchmarking
* Automated partner routing optimization
* More self-service onboarding for clinics
* More configurable notification and campaign tooling
* More robust partner-facing portals
* Advanced segmentation, experimentation, merchandising, and campaign optimization tools
* Deeper APIs / headless commerce support
* More sophisticated exception automation and workflow rules
* Support for multiple branded customer experiences per clinic where strategically useful
* Expanded customer portal features for richer self-service and longitudinal progress tracking
	
---

## 13. Risks and Constraints

### Product Risks
* Over-customization may reduce repeatability and increase implementation burden
* Partner variability may create operational edge cases that are hard to generalize
* Undefined ownership of pricing, routing, and operational rules may create confusion
* Without a strong canonical status model, reporting and support will become inconsistent
* Unclear separation between internal platform UX and customer-facing branded UX may create product and engineering complexity
	
### Operational Risks
* Manual intervention may remain high if sync and exception tooling are weak
* Data inconsistencies across partner systems can erode trust in dashboards and statuses
* If customer-facing progress states are not translated clearly from internal states, the portal may confuse customers
	
### Strategic Risks
* Product messaging may drift toward clinical platform expectations if positioning is not clear
* Attempting to satisfy too many one-off tenant or clinic requests can compromise the platform model
* Excessive white-label customization requests may undermine repeatability if not bounded by a clear theming model
	
---

## 14. Open Questions and Research Backlog

### Business and Hierarchy
* Is the clinic layer always distinct from other possible business layers in future phases?
* Should the branded experience remain modeled separately even if there is one per clinic in MVP?
* Are customers unique within a tenant, branded experience, or program scope?
	
### Program Model
* What exact configuration belongs to a program by default?
* Should programs support inheritance or cloning from templates?
* How should multi-program or cross-sell journeys be represented?
	
### Pricing and Commerce
* What pricing scopes are allowed in V1?
* Can multiple price rules stack?
* How should grandfathering and price migrations be handled?
	
### Partner Model
* Should partner connections be primarily configured at the tenant, clinic, branded experience, or program level?
* What common abstraction is needed to make new provider/pharmacy integrations repeatable?
* How much visibility do external partners need in the platform?
	
### Customer and Enrollment Model
* Is Approved Product Plan the final term, or should another term better reflect the operational model?
* Should there be a separate object for treatment recommendation versus fulfillment-ready product plan?
* How should prescribed medication details, dosage, instructions, refill status, and shipment state be normalized for customer-facing visibility?
	
### Analytics and Marketing
* What dashboards are required for clinics on day one?
* Which metrics are most important for commercial success versus internal operations?
* What events must be instrumented at launch to avoid later reporting gaps?
* Which lifecycle reminders and campaign types are required in MVP?
* Which channels are in scope first: email, SMS, push, or external integrations?
* What segmentation capabilities are required in the first release?
* How should operational reminders differ from promotional marketing communications?
	
### White-Label Model
* How much customer-facing frontend theming and customization is needed in MVP?
* Is the platform portal-first, embedded, API-first, or hybrid?
* What exact elements of the customer portal should be themeable versus fixed?
* What communication surfaces must inherit branded experience theming in MVP?
	
### Customer Portal and Progress Model
* What exact customer-facing language should be used for Approved Product Plan versus Medication Plan?
* Which internal statuses should be shown directly to customers versus translated into simpler progress steps?
* Which support, messaging, or self-service actions should be available in the customer portal at launch?
	
---

## 15. Recommended Next Steps

1. Confirm the hierarchy and object naming model
2. Confirm which configuration is owned at tenant, clinic, branded experience, and program levels
3. Refine lifecycle states for enrollment, subscription, order, sync, and customer-facing progress objects
4. Define MVP boundaries more explicitly for product, engineering, and go-to-market alignment
5. Convert this PRD into detailed requirements tables and user flows
6. Define the customer portal information architecture and status mapping model
7. Define the bounded white-label theming model for customer-facing experiences
	
---

## 16. One-Paragraph PRD Summary

The platform is a multi-tenant telehealth commerce, growth, and operations platform that enables clinics to launch and manage branded health-related programs through configurable intake, product and pricing management, subscription commerce, conversion optimization, reminders, marketing orchestration, provider/pharmacy partner orchestration, order synchronization, support tooling, analytics, and a white-labeled customer-facing portal. It is designed to transform an already proven single-platform operating model into a scalable, reusable product that standardizes commercial and operational workflows while continuing to rely on third-party providers and pharmacy partners for clinical and fulfillment execution. The internal admin and operations platform remains shared and platform-standard in MVP, while the customer-facing storefront and portal are branded at the branded experience level and allow customers to view and manage purchases, medications, subscriptions, and operational progress.