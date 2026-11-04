# home — offline state — section 1/2

> Composition fragment. Compose into the parent (offline.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
1. **header** (#header) — title: "Good morning, Irving", subtitle: "CENTRAL · Mon 26 Oct 2026 · Offline · Updated 2 h ago", right_actions: [Profile, settings]
2. **card** (#collections_card) — title: "Today's collections", subtitle: "14 clients due · MX$18,450 due · MX$6,200 collected · 3 overdue", items: [Clients due today, Due today, Collected, Overdue clients] (render EXACTLY these, in this order — do not rename, add, or drop any), right_actions: [Open collection sheet]
3. **card** (#work_queue_card) — title: "Work queue", items: [Checker inbox tasks, Loans awaiting approval, Approved, awaiting disbursal, Clients pending activation, Pending reschedule requests, My unsynced drafts] (render EXACTLY these, in this order — do not rename, add, or drop any)
