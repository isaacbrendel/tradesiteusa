# Architecture

High-level only. Not a rebuild guide.

## Surfaces

| Surface | Job |
| --- | --- |
| Shop door (`/`, `/site`, `/agent`, `/bids`) | Show the package and let a prospect try the agent |
| Start (`/start`) | Short intake to get a shop into the funnel |
| Trade / city pages | Long-tail discovery for trade + geography |
| Voice APIs | Multi-tenant Night Line control plane |
| Bid APIs | Drawing ingest, draft, checkout, sign, export |
| Live board | Owner metrics (pin-gated) |
| Analytics MCP | Tool access to live board numbers for AI copilots |

## Request path (typical web lead)

1. Visitor lands on shop site or `/agent` demo.
2. Message hits an App Router API route.
3. Agent tools run under allowlisted fields and rate limits.
4. Lead is persisted in Postgres; shop can get SMS / board updates.
5. Analytics collect records the event for attribution.

## Voice path (typical Night Line call)

1. Twilio / ElevenLabs hits an initiation webhook with the called DID.
2. Control plane resolves shop config and returns agent context.
3. During the call, tool webhooks ask for windows, hours, KB, or owner ping.
4. Workflow state machine allows or blocks propose / confirm by mode.
5. Post-call ingest (HMAC) writes call + lead + contact thread rows.

## Bid path

1. User uploads drawings (S3-backed).
2. Parse + draft takeoff against a rate book (model-assisted).
3. Shop reviews totals; Stripe look fee on the money path.
4. Signed draft required before any push to an external job system.

## Data ownership

- **Postgres** is the system of record for shops, leads, voice, bids, research.
- **S3** holds uploads (logos, drawings, photos).
- **Stripe** owns payment state; app reacts to webhooks.
- **First-party analytics** owns event truth; Meta / GA / Clarity are fan-out.

## Trust boundaries

- Public routes never see raw secrets or tenant voice credentials.
- Voice and Stripe webhooks verify signatures before mutating state.
- Client analytics events strip PII patterns before store / fan-out.
- Owner board and MCP are gated (pin / OAuth), not public JSON dumps.

## What is intentionally omitted

Tenant IDs, DID maps, prompt text, rate books, quality-gate weights, and outreach sequences. Those stay in the private production repo.
