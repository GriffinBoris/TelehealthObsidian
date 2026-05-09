**Date:** 2026-05-08
**Attendees:** Stanton, Griffin

## Summary

Reviewed Stanton's current telehealth workflow, patient portal, and admin tooling to better define the SaaS platform scope. The main takeaway was that the initial build is narrower than originally expected: the product is primarily a multi-tenant middle layer between brands/clinics, doctor networks, and pharmacies, with branded intake, patient/refill workflows, and billing controls.

## Key Points

1. **Current portal / operational workflow**
	 * Stanton showed the existing patient portal and lead management flow.
	 * The current system tracks lead source, contact info, intake responses, and whether a lead converted into a patient.
	 * "Recent clinical encounters" are effectively used as a sales/transaction view, though clinically they represent doctor-patient interactions.

2. **Current business metrics**
	 * Stanton reported roughly `442` total patients and `339` active subscriptions.
	 * "Active subscription" means a live recurring billing relationship, not just a historically active patient.
	 * Subscription cadences include monthly, 3-month, 6-month, and 12-month plans.
	 * Stanton estimated current telehealth profit at roughly `$20k-$25k/month`, with marketing revenue above that.

3. **Refill automation**
	 * Refill requests are automated through the patient portal.
	 * Patients receive a refill prompt based on plan timing, such as around day 21 for monthly plans.
	 * Refill questions come from the doctor network and include current weight, dose, weight lost, and side effects.
	 * For longer plans, refill forms are still collected on a recurring cadence.

4. **Intended SaaS platform role**
	 * The planned product is a software layer for telehealth brands/clinics rather than a clinic operator itself.
	 * Core flow discussed:
		 `Patient -> Intake -> Brand/Clinic Backend -> Doctor Network -> Pharmacy -> Patient`
	 * On approval, the pharmacy fulfills medication and returns tracking information for display in the patient portal.
	 * Existing patient bases could be migrated either by having patients re-enter through intake or by CSV import.
	 * Intake forms should be brandable per clinic/merchant.

5. **Multi-brand strategy**
	 * Stanton wants the option to support multiple brands under one platform.
	 * Different brands may exist for different marketing approaches, niches, product focuses, or demographic targeting.
	 * The platform could be used both for third-party brands and for brands Stanton operates directly.

6. **Admin / billing model inspiration**
	 * Uniloop was referenced as a useful multi-tenant SaaS example.
	 * Desired admin concepts include:
		 * Super admin dashboard across all brands/merchants
		 * Per-brand subscription plans
		 * Per-transaction application fees
		 * Merchant-specific fee overrides for volume discounts
	 * Example pricing discussed was a monthly SaaS fee plus a per-order fee such as `$5/order`.
	 * Billing should sync cleanly with Stripe.

7. **Product scope clarification**
	 * Griffin noted the system has fewer requirements than originally outlined in the earlier PRD.
	 * The clarified MVP is more operational and workflow-focused than the earlier broader vision.

8. **Design / documentation**
	 * Stanton may have his designer resume Figma work, especially around communication and notification screens.
	 * Griffin mentioned using Obsidian canvas-style tools for mapping flows and requirements.

9. **Technical stack discussion**
	 * Griffin shared the current implementation stack as Python/Django on the backend, Vue/TypeScript on the frontend, and Postgres for the database.
	 * There was a short discussion about JavaScript ecosystem/security tradeoffs; no changes were requested based on this.

## Decisions / Confirmed Direction

* The product should be built as a multi-tenant telehealth SaaS layer, not as a clinic-specific internal tool.
* Brands/clinics should have branded intake and patient workflows.
* Existing patients should be supportable via intake re-entry or CSV import.
* Billing should support both a SaaS subscription fee and per-transaction fees.
* Per-brand fee overrides are important for negotiation and volume pricing.
* Refill workflows should be automated and tied to plan timing.
* The current implementation scope is narrower and more manageable than the original PRD suggested.

## Action Items

| Action | Owner | Status |
|---|---|---|
| Send the flow chart / whiteboard workflow image | Stanton | Pending |
| Rework requirements into the simpler clarified workflow format | Griffin | Pending |
| Review Uniloop admin patterns for platform inspiration | Griffin | Pending |
| Confirm billing model requirements: SaaS fee, per-order fee, Stripe sync, fee overrides | Griffin + Stanton | Pending |
| Have designer revisit communication / notification designs if needed | Stanton | Pending |

## Open Questions

* What exact objects and statuses define a "transaction" for billing purposes?
* What is the minimum viable super admin feature set for launch?
* Which parts of patient migration should be self-serve vs admin-assisted?
* How much configurability should brands get over intake forms, notifications, and pricing plans?

## Build Implications

* Prioritize the workflow from intake through doctor review, pharmacy fulfillment, tracking, and refill processing.
* Model the app around tenants/brands first.
* Treat billing as two layers: base SaaS subscription plus usage-based order fees.
* Leave room for override logic at the merchant/brand level.
* Plan for patient portal notifications and refill prompts as core product functionality.
