# home — partial_failure state — section 2/3

> Composition fragment. Compose into the parent (partial_failure.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
4. **card** (#work_queue_card) — title: "Work queue", items: [Checker inbox tasks, Loans awaiting approval, Approved, awaiting disbursal, Clients pending activation, Pending reschedule requests, My unsynced drafts] (render EXACTLY these, in this order — do not rename, add, or drop any)
5. **list** (#meetings_card) "Meetings today" — 2 items: "Centro Arin", "MARIPOSAS MONARCAS" …and 1 more similar cards
6. **card** (#portfolio_card) — title: "Portfolio at a glance", subtitle: "1,098 active clients · 60 active loans · MX$1,284,500 outstanding · PAR 7.5%", items: [Active clients, Active loans, Outstanding, Overdue, Loans in arrears, PAR, Savings balance, Groups, Centres] (render EXACTLY these, in this order — do not rename, add, or drop any)
