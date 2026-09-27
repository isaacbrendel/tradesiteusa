# Engineering decisions

Short notes on choices that show how the product thinks. Useful interview fodder.

## 1. Server-enforced voice workflow

**Choice:** Call stages and booking modes live in application code. The model proposes; the server allows or refuses.

**Why:** Prompt-only agents skip steps under pressure. A trade shop cannot have a phantom appointment. Modes (`autonomous` / `qualify` / `assist`) encode how much autonomy the owner wants.

**Tradeoff:** More webhook surface and eval maintenance. Worth it for correctness.

## 2. Signed draft before Jobber

**Choice:** Bid machine can draft freely. Export / push requires an explicit signed draft after review (and the look fee path where applicable).

**Why:** A wrong number on paper burns trust faster than a slow bid. Human gate is the product feature, not a bug.

## 3. Copy and prices as typed modules

**Choice:** Owner-facing strings and cents live in one product layer. Components import them. Lint fails slop patterns.

**Why:** Vertical SaaS dies when the UI and the offer disagree. Pricing drift is a support ticket and a legal risk.

## 4. First-party analytics as source of truth

**Choice:** Collect events yourself. Fan out to Meta / GA / Clarity. Expose a board (and MCP) on that store.

**Why:** Pixel-only dashboards lie when ad blockers and consent cut half the funnel. Owner decisions need a number you can defend.

## 5. Quality gate on outreach research

**Choice:** Research pipeline can fail closed. Low-confidence dossiers do not become proposals.

**Why:** AI makes it cheap to send garbage. The business goal is booked looks, not send volume. Gate on quality before generate.

## 6. Private monorepo, public case study

**Choice:** Production stays private. This write-up + live demos prove the work.

**Why:** Opening the repo would leak tenants, prompts, rate books, and ops data. Recruiters need evidence of judgment and shipping, not a cloneable SaaS.

## 7. Vertical depth over generic CMS

**Choice:** Trade-specific offer (site + agent + bids) instead of a white-label website builder for everyone.

**Why:** Differentiation is workflow (phone desk, drawings, shop hours), not themes. Depth beats template breadth for a solo builder.
