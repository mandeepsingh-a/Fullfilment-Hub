# Fulfillment Hub

A fulfillment tracking app for XYZ's e-commerce warehouse operations, built for the take-home project.

## How to run it

No build step, no dependencies, no backend.

1. Open `index.html` directly in any browser (double-click it), or
2. In VS Code, install the "Live Server" extension, right-click `index.html`, and choose "Open with Live Server"

All data is sample data generated in-memory in JavaScript (`orders`, `inventory`, `exceptions`, near the top of the `<script>` tag). Nothing persists — refreshing the page regenerates a fresh sample day. Order deadlines are real timestamps, so the countdowns on screen actually count down, and the whole dashboard re-renders every 30 seconds so delays and stalls surface live.

## What it does

**Office Dashboard**
- **Fulfillment pipeline** — a live count of orders in each stage (Received → Processed → Picking → Packing → Staging → Shipped), so status is visible at a glance instead of buried in a spreadsheet.
- **Needs attention** — a single actionable list combining priority orders at risk of missing their deadline, orders blocked on stock, orders stalled too long in one stage, and low-stock SKUs — each with a direct action button (Pick now / Review / Transfer).
- **Staging & courier pickup** — every staged (packed) order is assigned a courier and a pickup cutoff; the panel flags anything overdue or due soon, so a missed courier pickup gets caught instead of forgotten. This panel also appears on the Warehouse Floor view, so packers see the same handoff status without switching tabs.
- **Exceptions** — a lightweight open/resolved log for problems that would otherwise be handled informally and forgotten (stock mismatches, picking issues, etc.).
- **Orders table** — filterable (Needs attention / Active / Shipped / All), sorted priority-first, showing item, stage, deadline, and flags for every order.
- **Inventory** — main vs. secondary warehouse stock per SKU. A low-stock SKU can be transferred over in three steps (Requested → In Transit → Received) sized to actual demand, not an arbitrary amount, and main-warehouse stock is deducted for real once an order is picked.

**Warehouse Floor**
- A simplified, large-button view for warehouse staff: priority-sorted task cards, one per order, showing the exact SKU, product name, size, and quantity to check against the physical item. A confirmation checkbox is required before the button to advance a stage becomes clickable, to cut down on wrong-item/wrong-variant shipping.
- Orders blocked on stock are visibly greyed out so pickers don't waste time on something that can't be fulfilled yet.
- Jumping here from a "Pick now" alert scrolls straight to and highlights that order's card.

**Data**
- ~250 sample orders per day, matching the volume stated in the brief, built with a controlled composition (a fixed ~15 priority orders, a fixed ~5 genuinely stock-blocked orders, the rest operationally healthy) rather than pure randomness — so the demo reads as a believable day of operations rather than noise.

## Why these problems

Of the eight pain points named in the brief, this build addresses seven: order visibility (pipeline + needs-attention view), delays going unnoticed (stalled-order detection), priority deadlines being missed (real countdowns), stock inaccuracy across two warehouses (need-based transfer flow), the wrong item/variant being shipped (explicit item check before advancing), couriers missing pickup or boxes going unaccounted for (staging + courier tracking), and problems being handled informally (the exceptions log).

## Known simplifications (deliberate)

- **Office vs. warehouse stage ownership isn't enforced.** Either side can advance any stage. The brief describes a 1–2 person office team, so this matches how a small team actually works day to day rather than imposing a rigid handoff.
- **Data resets on refresh and the generated sample orders may differ between loads** — fine for a demo, but worth mentioning on camera.
- **Exceptions aren't created automatically** when an order becomes blocked. The existing log demonstrates the concept without adding workflow complexity; auto-creation would be a natural v2 addition.
