# Griffin Figma Description

**Date:** May 10, 2026
**Type:** PRD addendum from Figma walkthrough
**Purpose:** Capture the current Figma UI patterns and page-level requirements in structured form without losing implementation detail.

## Summary

This document captures a detailed walkthrough of the Figma designs, starting with the global shell, sidebar, offerings, pricing profiles, and coupons. The design language is consistent across pages: a persistent left sidebar, a main content pane with a large page header and muted supporting copy, repeated table/list patterns, simple text tabs with a bottom border for the active state, empty states shown as dashed placeholder cards, and right-side drawers for create/edit/link workflows.

## Global Layout Patterns

* Every page appears to use a persistent left sidebar and a main content pane.
* The main content pane generally starts with a non-card page header using large title text with smaller muted descriptive text underneath.
* Search inputs and filters are typically placed directly under the page header, aligned toward the left.
* Tables and list pages share repeated helper text such as "showing X out of Y store offerings" and should likely support pagination.
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
* `Reactivate` or similar status action may exist depending on state, though the transcript sounded like `Read Text` and should be verified against Figma
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

## Clarifications Needed

| Topic | Question |
|---|---|
| Tenant/workspace/clinic selector | Should the sidebar dropdown switch tenants, workspaces, or clinics given the current multi-tenant model? |
| Base offering | What exactly does `Base offering` mean in the organization card? |
| Display mode | What is the intended business meaning of `Total price` vs `Monthly breakdown`, and where is this shown to users? |
| Badge | What is the intended use of badge text like `BEST_VALUE`, and is it optional per billing plan display config? |
| Pricing profile actions | What do the color-palette and refresh icons do in linked billing plan rows? |
| Pricing profile list copy | Should `Search offerings` and `Showing X of Y store offerings` be renamed for pricing-profile context? |
| Coupons filter | What options should exist under `All coupons`? |
| Coupon action menu | Verify the exact status-related action label in the ellipsis menu. |
| Coupon breadcrumb | Should the breadcrumb start with `Coupons` rather than `Patients`? |
| Empty states | Should the coupons page adopt the same dashed-card empty state pattern used elsewhere? |
| Copy verification | Confirm the exact product/medication strings shown in Figma where transcript recognition may have been imperfect. |

## Follow-Up Recommendations

* Review the Figma with Stanton specifically for tenant/workspace/clinic switching behavior.
* Confirm data model implications for offerings, billing plans, pricing profiles, and coupon applicability trees.
* Normalize repeated empty-state, table-footer, and drawer-footer patterns into reusable UI conventions.
* Verify pricing copy and coupon terminology before PRD finalization.
