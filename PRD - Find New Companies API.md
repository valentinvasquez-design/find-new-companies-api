# Find New Companies API -- Product Requirements

## 1. Problem Statement

Sales teams using SI today can build dynamic lists that match their ICP using firmographic, traffic, and technographic filters across 100M+ websites -- but these lists are static snapshots. When a new company enters the market, grows into a target segment, or adopts a qualifying technology, reps have no way to know in real time. They must manually re-check their saved searches or wait for monthly email digests, by which time the opportunity window has narrowed or closed.

This gap means reps are always reacting to stale data rather than acting on fresh intent. A SaaS startup that just crossed the 50-employee threshold and installed a competitor's tool yesterday is a far better prospect today than it will be in 30 days when every other vendor has noticed. Competitors like ZoomInfo and Apollo offer list-based alerts but do not provide webhook-driven, real-time delivery of new ICP matches tied to dynamic lists -- making this a differentiation opportunity for Similarweb.

## 2. Target Audiences and Use Cases

**SDR / BDR -- Real-time prospecting pipeline:** receive webhook notifications the moment a new company matches an ICP list, enabling same-day personalized outreach ("I noticed you just expanded into the US market -- curious how you're handling X").

**AE / Sales Rep -- Pipeline acceleration:** automatically surface net-new accounts that match deal criteria without manually refreshing saved searches, so reps spend time selling rather than hunting.

**AM / CSM -- Portfolio expansion:** monitor dynamic lists for companies adjacent to existing accounts (same vertical, similar tech stack) and proactively pitch to warm referral targets the moment they appear.

**RevOps / Sales Ops -- Automated lead routing:** pipe webhook payloads directly into Salesforce, HubSpot, or internal systems so that new ICP-matching companies are automatically created as leads, scored, and assigned to the right rep without manual intervention.

## 3. Product Requirements

### R1 -- Find New Companies API card in the Settings & Integrations page

**Job / Pain:** Users need a centralized place to discover, configure, and monitor the Find New Companies API alongside existing API integrations (Signals API, Contacts API). Today, no entry point exists for this capability.

**When and Where:** A new card appears in the APIs section of the Settings & Integrations page, positioned above the Signals API card. The card displays:
- A descriptive tagline: "Discover in real time new companies matching your ICPs"
- Webhook status (Configured / Not configured)
- Number of subscribed dynamic lists (1--5)
- Count of new companies found recently
- A "Manage" button that navigates to the configuration page
- A "View documentation" link to the API reference

**Success Signals:**
- X% of SI users with active dynamic lists visit the Find New Companies API card within 30 days of launch.
- Users who configure the API have higher dynamic-list engagement (edit frequency, list count) than those who do not.

---

### R2 -- Webhook configuration via the Manage page

**Job / Pain:** Users need a simple way to connect their systems to Similarweb so that new ICP-matching companies are pushed automatically to their endpoints. Configuration should feel consistent with the existing Manage Signals API experience and require no engineering effort beyond providing a URL.

**When and Where:** Clicking "Manage" on the Find New Companies API card opens a dedicated page with:
- A "Back" link to return to Settings & Integrations
- A **Data Credits Usage** card explaining the cost model (1 Data Credit per new company found and delivered), with a visual meter showing remaining credits
- A note that only dynamic lists with up to 100K companies can be set up with the webhook
- A **Webhook** card with a table supporting up to 5 rows, each containing:
  - A URL input field for the webhook endpoint
  - A "Dynamic list" dropdown showing all of the user's dynamic lists with company counts (e.g., "ICP -- Tech Companies - 24K"). Lists exceeding 100K companies are shown but disabled with an "(exceeds 100K)" label
  - "Test" and "Delete" action buttons per row
- A "+ Add another" link to add additional webhook rows (max 5)

**Success Signals:**
- 80%+ of users who open the Manage page successfully configure at least one webhook (low drop-off).
- Average webhooks per user > 1 (users connect multiple lists to different endpoints or workflows).
- < 5% of webhook test attempts fail (endpoints are reachable and correctly configured).

---

### R3 -- Dynamic list eligibility and 100K company cap

**Job / Pain:** Delivering webhook payloads for very large lists would generate excessive credit consumption and noisy, low-signal notifications. Users need clear guardrails that keep the feature cost-effective and actionable, without requiring them to guess which lists qualify.

**When and Where:** The dynamic list dropdown in the webhook configuration table shows each list's current company count in a compact format (e.g., 24K, 1.2K, 0.6K). Lists exceeding 100K companies are:
- Visually greyed out (disabled) in the dropdown
- Annotated with "(exceeds 100K)" so the reason is immediately clear
- Not selectable until the user refines the list below the threshold

An orange warning message below the Data Credits card reinforces the constraint: "Only dynamic lists with up to 100K companies can be set up with the webhook."

**Success Signals:**
- Zero webhook configurations are created for lists exceeding 100K (enforcement is airtight).
- Users with over-limit lists refine them below 100K at a higher rate after encountering the constraint (the guardrail drives better list hygiene).
- Support tickets related to "why can't I select my list" are near-zero (the inline explanation is sufficient).

---

### R4 -- Credit-based pricing model

**Job / Pain:** Users need a transparent, predictable cost model so they can evaluate ROI before enabling the feature and monitor spend as it runs. Opaque or unlimited pricing creates distrust and blocks adoption.

**When and Where:** The Manage page displays a prominent Data Credits Usage card at the top showing:
- A clear statement: each new company costs **1 Data Credit**
- A visual ring meter showing the percentage of credits remaining in the current billing cycle
- Credits are deducted automatically when a matching company is found and delivered to the webhook endpoint

**Success Signals:**
- Users who view the pricing card proceed to configure a webhook at a rate > 60% (pricing is not a blocker).
- Credit consumption per user correlates positively with downstream conversion metrics (credits spent = leads worked).
- < 2% of users exhaust their credit balance unexpectedly (the meter provides adequate visibility).
