# Griffin Figma Description

**Date:** May 10, 2026
**Type:** PRD addendum from Figma walkthrough
**Purpose:** Capture the current Figma UI patterns and page-level requirements in structured form without losing the earlier walkthrough context.
**Source:** Consolidated from the earlier Griffin Figma description plus the later walkthrough covering patients, orders, notifications, and shared modal behavior.

## Summary

This document consolidates the earlier notes on the global shell, offerings, pricing profiles, and coupons with later walkthrough details for patients, orders, notifications, and modal patterns. The design language is consistent across pages: a persistent left sidebar, a main content pane with a large page header and muted supporting copy, repeated table/list patterns, simple text tabs with a bottom border for the active state, dashed empty states, right-side drawers for create/edit/link flows, and multi-card detail pages for record-level screens.

## Global Layout Patterns

* Every page appears to use a persistent left sidebar and a main content pane.
* The main content pane generally starts with a non-card page header using large title text with smaller muted descriptive text underneath.
* Search inputs and filters are typically placed directly under the page header, aligned toward the left.
* Tables and list pages share repeated helper text such as `Showing X out of Y store offerings` and should likely support pagination.
* Detail views commonly use simple text-only tabs with muted labels and a black bottom border on the active tab.
* Create, edit, configure, and link flows commonly use a right-side drawer over a dimmed or blurred page background.
* Drawers generally have white backgrounds, a footer separated by a rule, and `Cancel` / `Save changes` actions.
* Empty states are frequently represented as larger dashed cards with an icon, supporting text, and a CTA when relevant.
* Toasts or notifications appear in the upper-right after some actions such as saving a pricing profile.

## Sidebar

### Top Identity Area

* The top of the sidebar shows the title text for the platform or clinic plus a logo beside it.
* The example shown appears to be something like `Clinic 1` with a logo and decently sized text.
* Directly underneath is a dropdown that appears to represent the active workspace or clinic.
* This needs clarification because the platform is currently modeled as multi-tenant: one tenant can have multiple workspaces, and each workspace can have multiple clinics.
* In the Figma, the dropdown appears clinic-based rather than tenant-based.

### Navigation Sections

* `Core`
	* `Dashboards`
	* `Patients`
	* `Coupons`
	* `Teleforms`
	* `Orders`
* `Products`
	* `Offerings`
	* `Pricing Profiles`
* `Communication`
	* `Messages`
	* `Notifications`
* `Networks`
	* `Provider Networks`
	* `Pharmacies`
* `Configuration`
	* `Settings`

### Sidebar Footer User Card

* At the bottom of the sidebar there is a muted-background user card.
* Left side: profile picture.
* Middle: user name with muted email beneath it.
* Right side: a three-ellipsis trigger that likely opens actions such as logout, settings, or related account options.

## Offerings

### Offerings List Page

* Under the page header there is a search box aligned left.
* Next to the search is a status dropdown/filter.
* Below that is a table.
* Observed table columns:

| Column | Notes |
|---|---|
| Name | Row includes an icon, the product/offering name, and muted descriptive copy beneath the name. |
| Product Code | Product identifier. |
| Medications | Appears to represent the number of medications linked to the offering. |
| Billing Plans | Count or list of billing plans linked to the offering. |
| Provider Network | Which provider network the offering routes to. |
| Pharmacies | Which pharmacies the offering can route to. |
| Status | Active/inactive style state. |

* Example offering shown: `Semaglutide injection`.
* Beneath the table is helper text such as `Showing 5 out of 5 store offerings`.
* Pagination is likely needed alongside this helper text.

### Offering Detail Page

* The detail page keeps the standard page header.
* Under the header is a simple tab bar.
* Observed tabs:

`Overview`, `Pharmacies`, `Provider Networks`, `States`, `Fulfillment`

* Tabs are text-only, muted, and use a black bottom border to indicate the selected tab.

### Overview Tab Layout

* The page appears to use a two-column flex layout.
* Left side is roughly two-thirds width.
* Right side is roughly one-third width.

### Overview Tab: Right Column

* A status card with a status dropdown.
* A medications card with supporting copy similar to `Available medications and pharmacy items`.
* Inside the medications card, the content is shown as nested list-item style rows.
* Example medication item:

An icon tile with a purple background and white `S`, medication name similar to `Semaglutide/peroxidine`, and a green `Active` pill on the right.

* A pharmacies card using the same repeated list-item visual pattern.
* A provider networks card using the same repeated list-item visual pattern.
* A dosage plans card using the same repeated list-item visual pattern.
* An organization card showing category and type.
* The organization card appears to show `Base offering`, but the exact meaning needs clarification.
* A states control that appears to be a multi-select dropdown.
* State abbreviations render as chips inside the input after selection.

### Overview Tab: Left Column

* A title and description card at the top.
* A display/preview style card below showing product name, description, image, and possibly the number of billing plans.
* A billing plans card below the preview card.

### Billing Plans Card

* Card title: `Billing Plans`.
* Supporting text: configure pricing tiers and profiles for the offering.
* Top-right CTA: `Add plan`.
* The plan rows are large card-style items split visually into two horizontal halves.
* Upper half:

Muted gray background, plan name such as `One month supply`, active status chip, muted secondary text such as `One dose`, and actions on the far right.

* Observed row actions:

Delete icon button and gear icon button, both with muted backgrounds and rounded square borders.

* Lower half:

White background, muted label such as `Plan pricing`, large price such as `$199`, and muted `Base price` text aligned to the right.

* This card pattern repeats for each billing plan attached to the offering.

## Billing Plan Drawer

### Drawer Layout

* Clicking the gear icon appears to open a right-side drawer.
* The rest of the page is dimmed or blurred behind it.
* The drawer header includes the product image, plan name, price, and supporting dose text.
* Under the header is another tab row.

### Drawer Tabs

`Billing Plan Details`, `Pricing Profiles`

### Billing Plan Details Tab

* Input: plan name.
* Pricing configuration area.
* Pricing type is selected via radio button between `Price per dose` and `Total price`.
* Below that is a numeric input.
* The numeric input shows currency on the left.
* The right side of the input shows contextual muted text such as `One dose` when `Price per dose` is selected.
* Below that is a summary card that looks input-like but behaves more like a computed preview.
* The summary card shows dose information and the calculated total.
* There is a status dropdown with states that appear to include `Active` and `Inactive`, likely with colored dots such as green and red.
* Supporting disclaimer text explains status behavior:

`Active` plans are available to customers, `Inactive` plans are hidden, and `Archived` plans are permanently hidden but can be restored.

* The bottom of the drawer has a separated footer area with `Cancel` and `Save changes`.

### Pricing Profiles Tab Within the Billing Plan Drawer

* Initial state can show that no pricing profile is linked.
* There is an `Edit` affordance and a `Link profile` button.
* Empty state is a dashed placeholder card.
* Empty state copy indicates that no pricing profiles are linked and instructs the user to link a pricing profile to configure custom pricing for the billing plan.
* Placeholder icon appears to be a price tag.

### Link Pricing Profile Drawer

* If no pricing profiles exist, clicking `Link profile` opens a drawer titled `Link pricing profile`.
* The drawer can show an empty state with a price tag icon and copy such as `No pricing profiles available` plus a `Create pricing profile` CTA.
* If pricing profiles do exist, the drawer shows:

A search input with a magnifying glass icon and a list of selectable card-style rows.

* Each row includes a checkbox, price tag icon, pricing profile name, and the ability to select the profile to link.
* If a profile is already linked, the row appears to show an `Unlink` action in red on the far right.
* Standard drawer footer actions remain `Cancel` and `Save changes`.

## Pricing Profiles

### Pricing Profiles List Page

* Page uses the standard large title and muted supporting copy.
* Under the header is a search input. The placeholder observed said `Search offerings`, though this may need copy review because the page is for pricing profiles.
* To the right is a list/grid view toggle.
* The toggle appears as a gray container with icon-only options.
* The active toggle appears white with subtle emphasis.
* To the right of the toggle is an `Add pricing profile` button.

### Empty State

* If no pricing profiles exist, the page shows a large dashed card.
* Copy is similar to:

`No pricing profiles yet. Create your first pricing profile to start customizing billing plans and pricing for your store.`

* Placeholder loading-state style rows appear above the empty state.

### Add Pricing Profile Drawer

* Right-side drawer title: `Add pricing profile`.
* Fields:

`Name`, `Description`

* Footer actions: `Cancel`, `Save changes`.

### Pricing Profile List Item / Table Row

* After save, a toast/notification appears in the upper-right.
* The row includes:

| Column | Notes |
|---|---|
| Name | Includes a price tag icon followed by the profile name. |
| Billing Plans | Appears to be a count, for example `0 plans`. |
| Status | Active shown as a green pill. |
| Created Date | Date created. |
| Actions | Delete icon and gear icon. |

* Footer/helper text appears similar to `Showing 1 of 1 store offerings`, though this copy may also need review for pricing-profile context.

### Pricing Profile Detail Page

* Clicking the gear icon appears to open a detail page rather than another drawer.
* Header includes the price tag icon, the pricing profile name, and fallback text such as `No description provided`.
* Observed tabs:

`Billing Plans`, `Codes`, `Settings`

### Billing Plans Tab Empty State

* Shows dashed placeholder content when nothing is linked.
* Copy indicates no billing plans are linked yet.
* Supporting text explains that no billing plans are linked to the pricing profile.
* A `Link offering` button appears in the top-right of the empty state area.

### Link Offering Drawer

* Right-side drawer title: `Link offering`.
* Supporting text indicates the user should select offerings to link and that all billing plans for selected offerings will be linked.
* Includes a search input.
* Selectable rows appear as card-style items with checkboxes, product image, and offering name.
* Footer actions: `Cancel`, `Save changes`.

### Linked Offerings Presentation

* Once offerings are linked, the page shows repeating grouped sections by offering.
* Each offering block includes:

| Area | Notes |
|---|---|
| Header left | Product image, product name, and muted text such as `3 billing plans linked`. |
| Header right | `Unlink offering` action. |
| Divider | Horizontal rule separating header from linked billing plan table. |

* Each offering then contains a table.
* Observed columns:

| Column | Notes |
|---|---|
| Billing Plan | Gray rounded-square credit-card icon, plan name, and muted subtext such as `Paying monthly...`. |
| Doses | Example: `One dose`. |
| Pricing Type | Pill such as `Base price`. |
| Base Price | Example: `$99.00` with muted `per dose`. |
| Override Price | Empty dash when unset. Has an info icon / tooltip in the column header. |
| Display Mode | Pill such as `Total` with an icon. |
| Strikethrough | Dash when unset. |
| Override Display | Dash when unset. |
| Added | Date added. |
| Actions | Includes edit icon plus two additional icons that look like a color palette and a refresh icon. Their exact behavior is unclear. |

## Display Configuration Drawer

* Clicking `Edit` on a linked billing plan appears to open a right-side drawer.
* Header area includes the product image and a title section.
* Large header text appears to say `Display configuration`.
* Muted supporting copy includes the plan name, such as `One month supply`.
* The right side of the header shows dose information such as `One dose`.
* Below that is another compact summary of the plan with plan name, supporting cycle text, and price such as `$519`.

### Drawer Controls

* A checkbox card labeled `Set as default`.
* Supporting copy: make this the default pricing profile for the billing plan in checkout.
* A display mode section rendered as card-style radio options.
* Observed options:

`Total price` with supporting text `Show full cycle price`
`Monthly breakdown` with supporting text `Show per month price with suffix`

* A separate checkbox section labeled `Enable strikethrough price`.
* This is marked as optional.
* Supporting copy explains that it displays a crossed-out original price alongside the current price.
* A `Subtext` textarea follows.
* Supporting copy explains that this is small descriptive text shown under the price and defaults to billing-interval text when left empty.
* A `Badge` text input follows with placeholder similar to `BEST_VALUE`.
* Supporting copy explains that the badge text is displayed on the pricing option.
* Standard drawer footer actions: `Cancel`, `Save changes`.

## Coupons

### Coupons List Page

* Standard page header with title `Coupons` and muted copy similar to `Manage discount codes and promotional offers for your customers`.
* Below the header is a search box.
* There is an `All coupons` dropdown filter, though the actual filter dimensions/options need clarification.
* On the right is a `Create coupon` button.
* The list page currently appears table-based.
* If empty, this should likely use the same dashed-card pattern used elsewhere for consistency.

### Coupons Table Columns

| Column | Notes |
|---|---|
| Code | Coupon code, example similar to `TEST002`. |
| Type | Example: percentage. |
| Value | Large value such as `100%` with muted supporting text such as `Max of $100`. |
| Usage | Example `0/20`, implying usage count out of total limit. |
| Applicability | Chip such as `All`. |
| Valid Until | Date. |
| Status | Chips such as `Expired` (red), `Deactivated` (black), or `Active` (green). |
| Actions | Ellipsis menu. |

### Coupon Row Actions Menu

* `View detail`
* `Edit`
* `Duplicate`
* `Deactivate`
* `Reactivate` or similar status action may exist depending on state, though the transcript sounded like `Read Text` and should be verified against Figma.
* `Delete`

* All menu items appear to have icons.

### Coupon Detail / View Page

* This is the first observed place using breadcrumbs.
* Observed breadcrumb looked like `Patients > Coupon detail: [coupon code]`, which likely needs verification because the page is coupon-related.
* Page header shows the coupon code name and a status pill such as `Active`.
* Top-right actions include `Deactivate`, `Duplicate`, `Edit`, and `Delete`.
* `Delete` is red.
* Other buttons are gray and icon-based.

### Coupon Metrics Cards

* Three inline metric cards are shown:

| Metric | Example |
|---|---|
| Total Uses | `0 / 20` |
| Unique Patients | `0` |
| Total Discount | `$0` |

### Coupon Detail Panels

* The lower section uses a two-column layout with cards.
* Left card: `Coupon details`.
* Right card: `Applicability`.

### Coupon Details Card

* Shows repeated label/value rows including:

`Discount`
`Minimum order`
`Maximum discount`
`Uses per patient`
`Valid from`
`Valid until`
`Created date`

* Example discount value shown: `100% off`.
* Example minimum order shown in the transcript as `$50 off`, which should be verified because the label sounded like a threshold rather than a discount value.

### Applicability Card

* Card title: `Applicability`.
* Supporting label: `Restrictions`.
* Example large text: `Applies to all customers and products`.

### Create / Edit Coupon Page

* Header text: `Create coupon`.
* Supporting copy: `Set up a discount code with custom limits and applicability rules.`
* The page is composed of large section cards / collapsible sections.
* Inputs generally use a label above the control and the field beneath it.

### Basic Information Section

* Section title: `Basic information`.
* Supporting copy: setup the basic details of the coupon code.
* Two inline inputs:

`Coupon code`, `Description`

* Three evenly spaced toggles:

`Active immediately`
`Show in suggestions`
`First time customers only`

### Discount Details Section

* Section title: `Discount details`.
* Supporting copy: configure the discount type and value.
* First row:

`Discount type` dropdown, value input such as `Percentage off`

* Second row:

`Minimum order amount`, `Maximum discount`

### Usage Limits Section

* Section title: `Usage limits`.
* Supporting copy: set limits on how many times the coupon can be used.
* Inputs:

`Total usage limit`, `Usage limit per patient`

### Validity Period Section

* Section title: `Validity period`.
* Supporting copy: set when this coupon is valid.
* Inputs:

`Valid from`, `Valid until`

### Applicability Restrictions Section

* Section title: `Applicability restrictions`.
* Supporting copy explains that the coupon can optionally be limited to specific patients, products, categories, or treatments, that multiple types can be selected, and that if nothing is selected the coupon applies to every product and customer.

### Specific Patients Subsection

* Uses a subsection card pattern.
* Includes a search box for patient name or email.
* Below that is a selectable list/table with columns for name and email.
* Rows appear checkbox-selectable.
* Example names mentioned: `Henry Tran`, `Mike`.

### Specific Products, Variations, and Pricing Options Subsection

* Uses a tree-style checkbox structure.
* Top level is the product.
* Second level is the variation, with `Variations` shown as muted copy.
* Third level is pricing options, with `Pricing options` shown as muted copy.
* Example hierarchy captured from the walkthrough:

Top level: `Semaglutide orals`
Variation: `Semaglutide orals - 100mg injection 2 units`
Pricing options: `One month - $250 one time`, `Two month - $450 one time`

### Specific Categories Subsection

* Similar in structure to the specific patients section.
* Includes a search input and a selectable list/table.
* Observed fields appear to be category name and category slug.

### Specific Treatments Subsection

* Similar in structure to categories/patients.
* Includes a search input and selectable list of treatments.

### Create Coupon Action

* The bottom of the page includes a `Create coupon` button.
* The large major sections appear collapsible.
* When collapsed, the section header appears to summarize the current selections.
* Example collapsed summary chips:

`1 product`, `1 variation`, `1 pricing option`
`1 selected`

## Patients

### Patients List Page

* Standard page header with title `Patients` and muted copy `View and manage all registered patients.`
* Top-right CTA: `Add patient`.
* The next row contains a search input for patient name, email, or phone number.
* To the right of search is an `All patients` dropdown that likely filters the list, though the exact options need clarification.
* Below that is a standard table.
* Observed table columns:

| Column | Notes |
|---|---|
| Name | Patient name, example `Henry Tran`. |
| Contact | Primary email with muted phone number beneath it. |
| Gender | Example value `Male`. |
| Medical Record | Currently shown as a dash in the walkthrough; meaning needs clarification. |
| Orders | Count. |
| Prescriptions | Count. |
| Treatments | Count. |
| Registered | Date field. |
| Actions | Delete, edit, and an eye/view action. |

### Add Patient Page

* Standard detail-style header.
* Title: `Add Patient`.
* Supporting copy: `Create a New Patient Record`.

### Basic Information Section

* Card title: `Basic information`.
* Supporting copy: `Enter the patient's personal details.`
* Fields appear in rows:

`First name`, `Last name`
`Email`, `Phone number`
`Date of birth`, `Gender`, `Biological gender`, `Medical record number`
`Height (inches)`, `Weight (pounds)`

### Insurance Information Section

* Card title: `Insurance information`.
* Supporting copy: `Enter the patient's insurance details.`
* Inline fields:

`Insurance provider`, `Policy number`, `Group number`

### Addresses Section

* Card title: `Addresses`.
* Supporting copy: `Add patient addresses`.
* The section appears to use a generic empty-list or empty-table pattern when no addresses have been added.
* Top-right CTA: `Add Address`.
* Page footer actions: `Cancel` and `Create Patient`.

### Add Address Subform

* Clicking `Add Address` appears to open an inline subcard rather than a separate drawer.
* First row includes an address-type dropdown that currently shows `Shipping`.
* A red trash icon on the far right removes the pending address entry.
* Additional fields:

`Address line 1`, `Address line 2`
`City`, `State`, `Zip code`, `Country`

* There does not appear to be a dedicated save/add/confirm action inside the subform, so this behavior likely needs clarification.

### Patient Detail Page

* Standard header uses the patient's name as the page title.
* Supporting copy: `Patient detail`.
* Layout appears to use a two-pane structure:
	* Left side is a narrow in-page section navigation rail.
	* Right side is the main content area.

### Patient Detail Metrics

* The top row appears to contain six metric cards.
* Observed metrics include:

`Total orders` or order volume wording that needs verification
`Total spent` in dollars
`Active prescriptions`
`Active treatments`
`Active subscriptions`
`Latest blood pressure reading`

* The blood pressure metric may be intentionally excluded from scope and should be confirmed.

### Patient Detail: Overview Section

* The first content section is `Overview`.
* The overview row contains two inline cards.

### Personal Information Card

* Card title: `Personal information`.
* Content appears structured in two columns.
* Left column includes email and phone.
* Right column includes medical record value, date of birth, and gender.

### Shipping Address Card

* Card title: `Shipping address`.
* Content displays the patient's shipping address in muted text.

### Prescriptions Section

* Subsection title and card title: `Prescriptions`.
* Supporting copy: `All prescriptions for this patient`.
* Empty state appears to show `No prescriptions found`.

### Ongoing Treatments Section

* Subsection title: `Ongoing treatments`.
* Card title appears to match the subsection.
* Supporting copy: `Active and past treatments`.

### Orders Section

* Subsection title: `Orders`.
* Card title: `Recent orders`.
* Supporting copy: `Last five orders placed by this patient.`

### Intake Form Responses Section

* Subsection title and card title: `Intake form responses`.
* Supporting copy: `Submitted medical forms and questionnaires.`

## Orders

### Orders List Page

* Standard page header title: `Order management`.
* Supporting copy: `Track, update, and fulfill customer orders.`
* A `Create Order` button appears beneath or to the right of the header region.
* The filter row includes:

`Search by order ID, patient name, or tracking number`
`All Statuses` dropdown
`All Sources` dropdown

* The exact filter values for status and source need clarification.
* The main list uses a standard table and empty state.
* Empty state icon appears to be a shopping-style icon in a bordered rounded square.
* Empty state copy is similar to:

`No orders yet`
`Orders will appear here once a customer starts purchasing.`

### Orders Table Columns

| Column | Notes |
|---|---|
| Order ID | Numeric or short identifier. |
| Patient | Patient name with muted email beneath it. |
| Item | Large text such as `1 item` or `2 items`, with muted product summary beneath; product list appears truncated with ellipsis. |
| Source | Example values include `Direct purchase` or `Treatment`. |
| Total | Total dollar amount. |
| Status | Colored chip. |
| Tracking | Appears as a dash in empty cases; likely tracking number or shipment reference. |
| Date | Order date. |
| Actions | Edit pencil and view eye action. |

### Order Status Chips

* `Processing` uses a blue chip.
* `Paid` uses a light green chip.
* `Shipped` uses a darker green chip.
* `Delivered` uses a strong green chip.
* `Pending` uses a yellow chip.
* `Canceled` uses a red chip.

### Create Order Page

* Standard detail-style header.
* Title: `Create new order`.
* Supporting copy: `Create a new order for a patient.`
* Main layout is a two-column flex split.
* Left column contains the primary form sections.
* Right column contains an order summary card.

### Customer Information Section

* Card title: `Customer information`.
* Primary control appears to be a searchable patient dropdown or autocomplete.
* After selection, a preview subcard shows the patient's name and email on a light gray background.

### Order Type Section

* Card title: `Order type`.
* Includes an `Order source` dropdown.

### Order Items Section

* Card title: `Order items`.
* Top-right CTA: `Add item`.
* Items render as a vertical list of nested cards on a light gray background.
* Each item row includes:

`Product` dropdown, likely searchable
`Variation` dropdown, likely searchable
`Quantity` stepper with minus and plus controls around the centered value
Delete action on the far right

### Addresses Section

* Card title: `Addresses`.
* First subsection is `Shipping address`.
* Fields appear in rows:

`Address line 1`, `Address line 2`
`City`, `State`
`Zip code`, `Country`

* A divider separates the shipping and billing portions.
* Second subsection is `Billing address`.
* A `Copy from shipping` button with a copy icon appears on the right.
* Billing address fields repeat the same structure as shipping.

### Order Notes Section

* Card title: `Order notes`.
* Supporting copy: `Add any notes or special instructions for this order.`
* Includes a textarea with placeholder copy similar to `Enter any notes about this order.`

### Order Summary Card

* Card title: `Order summary`.
* Repeats selected order items as line items.
* Each row shows product name plus quantity on the left and subtotal on the right.
* A divider separates items from the summary total.
* Footer area includes a bold `Total` row and a `Create order` button.

### Order Detail Page

* Standard header with the order identifier as title.
* Supporting copy includes the placed timestamp, such as `Placed on April 29, 2026 at 11:21 p.m.`
* Top-right includes the current order status chip.
* Main layout is a two-column detail view.

### Order Detail: Left Column

* Contains order items and the order timeline.

### Order Items Card

* Card title: `Order items`.
* Items render as a vertical list of nested cards.
* Each item includes:

Product name and quantity in the primary title line
Muted metadata such as SKU, size, and brand
Item pricing on the right, including line total

* A divider separates the item list from the order total row.

### Order Timeline Card

* Card title: `Order timeline`.
* Top-right CTA: `Add note`.
* Timeline is vertical.
* Each entry includes:

An origin chip such as `Internal`
Primary event title or note text
Muted supporting text such as the customer name or actor
Timestamp aligned on the right

### Order Detail: Right Column

* Contains quick actions, customer information, shipping address, and payment.

### Quick Action Card

* Card title: `Quick action`.
* Buttons are stacked vertically.
* Observed actions:

`Update status`
`Update tracking`
`Cancel order`

* `Cancel order` is styled as the destructive action.

### Customer Information Card

* Card title: `Customer information`.
* Shows customer name, email, and phone number.
* Includes a `View patient profile` button.

### Shipping Address Card

* Card title: `Shipping address`.
* Displays the order shipping address as muted text.

### Payment Card

* Card title: `Payment`.
* Includes a row showing total amount.
* The next row currently reads `No payment record.`
* Supporting warning copy indicates Stripe integration is required to charge orders.
* Example warning: `Connect your Stripe account to charge orders.`

## Notifications

### Notifications List Page

* Sidebar item label appears to be `Notifications`.
* Standard page header title: `Notification Management`.
* Supporting copy: `Customize notifications for your patient.`
* Top-right actions:

`Load missing template`
`Create template`

* Below the header is a search input for templates.
* Next to search is an `All events` dropdown, though the available filter values need clarification.
* The page uses the standard table pattern plus an empty state.
* Empty state icon appears to be a bell inside a bordered rounded square.

### Notifications Table Columns

| Column | Notes |
|---|---|
| Template Name | Plain text template name. |
| Event Type | Event chip. |
| Subject | Email subject. |
| Delay | Delay or reminder timing configuration. |
| Status | Active/inactive style chip. |
| Default | Blue `Default` chip. |
| Actions | Ellipsis menu. |

### Notification Values Observed

* Event types mentioned in the walkthrough included examples such as `Account verification`, `Checkout reminder`, `Intake form`, and `Abandoned`-style reminder states, though the exact event taxonomy should be verified in Figma.
* Delay values appeared to include:

`Immediate`
`60 minute delay`
`2 times at 120 minutes`

* Status appears to use a green `Active` chip.
* `Default` appears as a blue chip in its own column.

### Create Notification Template Page

* Standard detail-style header.
* Title: `Create Notification`.
* Supporting copy: `Design a new notification template for your patient communications.`
* First content row is a two-column layout with two cards.

### Template Details Card

* Card title: `Template details`.
* Supporting copy: `Basic information about your notification template.`
* Observed fields and toggles:

`Event type` dropdown
`Template name` field or dropdown
`Email subject`

* The email subject field supports variables using double curly braces.
* Helper text indicates variables can be used in the subject line.
* Additional toggle rows:

`Active` toggle with helper copy similar to `Enable this template for sending`
`Default template` toggle with similar helper copy

* Additional numeric inputs:

`Initial delay in minutes`
`Max reminder`

* Helper text for max reminder is similar to `How many times to send this notification?`

### Available Variables Card

* Card title: `Available variables`.
* Supporting copy: `Variables you can use in this template.`
* Default state is an informational nested card on a light gray background.
* Default copy is similar to `Select an event type to see the available variables.`
* Once an event type is selected, the helper copy changes to guidance such as `Click on any variable to copy it or use the variables button in the editor to insert them directly.`
* The card then shows a scrollable list of variables.
* Each row includes:

Variable token in double-curly format, such as a patient field
Muted description explaining what the variable represents

### Email Content Section

* Separate full-width card below the top two-column row.
* Card title: `Email content`.
* Supporting copy: `Design your email template using this editor.`
* Includes a content-type toggle with:

`HTML email`
`Plain text`

* The editor appears to support both visual editing and HTML source mode.

## Shared Modal Pattern

* When a modal opens, the page background becomes darker gray.
* The modal itself is a white rounded rectangle.
* Modal structure appears consistent:

Header/title row
Body content or form inputs
Primary confirmation action near the bottom
Close `X` in the top-right corner

## Clarifications Needed

| Topic                            | Question                                                                                                                     |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Tenant/workspace/clinic selector | Should the sidebar dropdown switch tenants, workspaces, or clinics given the current multi-tenant model?                     |
| Base offering                    | What exactly does `Base offering` mean in the organization card?                                                             |
| Display mode                     | What is the intended business meaning of `Total price` vs `Monthly breakdown`, and where is this shown to users?             |
| Badge                            | What is the intended use of badge text like `BEST_VALUE`, and is it optional per billing plan display config?                |
| Pricing profile actions          | What do the color-palette and refresh icons do in linked billing plan rows?                                                  |
| Pricing profile list copy        | Should `Search offerings` and `Showing X of Y store offerings` be renamed for pricing-profile context?                       |
| Coupons filter                   | What options should exist under `All coupons`?                                                                               |
| Coupon action menu               | Verify the exact status-related action label in the ellipsis menu.                                                           |
| Coupon breadcrumb                | Should the breadcrumb start with `Coupons` rather than `Patients`?                                                           |
| Coupon detail values             | Verify labels and example values such as `Minimum order` vs the transcript wording that sounded like `$50 off`.              |
| Patients filter                  | What should `All patients` filter by?                                                                                        |
| Medical record                   | What does the `Medical Record` column/value represent, and should it be required?                                            |
| Patient list view action         | What does the eye icon do on patient rows if the row itself is also clickable?                                               |
| Patient address type             | Should the address type be limited to shipping/billing, or can a patient store multiple labeled addresses?                   |
| Patient address subform behavior | Should there be an explicit save/add action for a newly entered address row?                                                 |
| Patient metrics                  | Confirm the exact wording and scope of the top metric cards, especially total orders/order volume and latest blood pressure. |
| Orders filters                   | What are the allowed values for `All Statuses` and `All Sources`?                                                            |
| Order tracking                   | Is the tracking field only a shipment tracking number, or can it also represent an internal fulfillment reference?           |
| Order payment card               | What actions should the payment card support beyond showing Stripe-connect guidance?                                         |
| Notifications filter             | What options should exist under `All events`?                                                                                |
| Notification event taxonomy      | Confirm the exact event types and naming used for templates.                                                                 |
| Notification actions menu        | What actions are available from the ellipsis menu on a template row?                                                         |
| Delay semantics                  | Confirm whether values like `2 times at 120 minutes` represent retries, reminder cadence, or a composed schedule.            |
| Template name control            | Is `Template name` a free-text field or a dropdown/select of predefined template types?                                      |
| Copy verification                | Confirm exact product, medication, and event strings where transcript recognition may have been imperfect.                   |

## Follow-Up Recommendations

* Review the Figma with Stanton specifically for tenant/workspace/clinic switching behavior.
* Confirm data model implications for offerings, billing plans, pricing profiles, coupon applicability trees, and patient-specific restrictions.
* Normalize repeated empty-state, table-footer, modal, and drawer-footer patterns into reusable UI conventions.
* Verify pricing copy, coupon terminology, patient metrics, and notification event labels before PRD finalization.
* Decide whether blood pressure and other clinical metrics are in scope for the patient detail view in this admin surface.
