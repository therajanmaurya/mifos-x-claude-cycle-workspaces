# home — partial_failure state — section 1/3

> Composition fragment. Compose into the parent (partial_failure.md). DESIGN.md is the contract.

## Composition (top → bottom, continued)
1. **header** (#header) — title: "Good morning, Irving", subtitle: "CENTRAL · Mon 26 Oct 2026 · Mifos field officer gateway", right_actions: [Profile, settings]
2. **error_state** (#card_error_retry) — "Couldn't load this card" (repeated rows; no demo rows for this state)
3. **card** (#collections_card) — title: "Today's collections", subtitle: "Couldn't load this card · Retry", items: [Clients due today, Due today, Collected, Overdue clients] (render EXACTLY these, in this order — do not rename, add, or drop any), right_actions: [Open collection sheet]
