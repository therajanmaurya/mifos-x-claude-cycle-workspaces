# home — offline state — section 2/2

> Composition fragment. Compose into the parent (offline.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
4. **list** (#meetings_card) — title: "Meetings today"
5. **card** (#portfolio_card) — title: "Portfolio at a glance", subtitle: "1,098 active clients · 60 active loans · MX$1,284,500 outstanding · PAR 7.5%", items: [Active clients, Active loans, Outstanding, Overdue, Loans in arrears, PAR, Savings balance, Groups, Centres] (render EXACTLY these, in this order — do not rename, add, or drop any)
6. **action_grid** (#quick_actions) — title: "Quick actions", items: [New client (person_add), New group (groups), New centre (domain), Collection sheet (fact_check), Run reports (bar_chart), Search (search), Path Tracker (person_pin_circle)] (render EXACTLY these, in this order — do not rename, add, or drop any)
7. **list** (#recent_card) — title: "Recently opened"
