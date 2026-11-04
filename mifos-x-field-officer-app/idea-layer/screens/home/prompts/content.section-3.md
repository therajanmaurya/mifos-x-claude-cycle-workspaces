# home — content state — section 3/3

> Composition fragment. Compose into the parent (content.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
5. **card** (#portfolio_card) — title: "Portfolio at a glance", subtitle: "1,098 active clients · 60 active loans · MX$1,284,500 outstanding · PAR 7.5%", items: [Active clients, Active loans, Outstanding, Overdue, Loans in arrears, PAR, Savings balance, Groups, Centres] (render EXACTLY these, in this order — do not rename, add, or drop any)
6. **action_grid** (#quick_actions) "Quick actions" — 2 items: "New client", "New group" …and 5 more similar cards
7. **list** (#recent_card) — "Recently opened" (repeated rows; no demo rows for this state)
