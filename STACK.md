# Stack

## Application

- **Next.js 15** App Router for pages and API routes
- **React 18** + **TypeScript**
- **Tailwind CSS** for UI
- **Zod** + React Hook Form for intake validation
- **NextAuth v5** for authenticated surfaces

## Data and infra

- **PostgreSQL** with **Prisma**
- **Vercel** for deploy and previews
- **AWS S3** for uploads (presigned where needed)
- **AWS SES / SNS** for email and SMS notify paths

## Money

- **Stripe** Checkout sessions
- Webhook handlers for subscription / payment lifecycle

## AI and voice

- **Anthropic Claude** for chat, research, and bid drafting (AI SDK)
- **ElevenLabs** conversational agents for Night Line
- **Twilio** for DIDs and SMS follow-up after calls
- Server-side workflow + evals around voice tools (not prompt-only)

## Analytics and ops

- First-party event collection and attribution
- GA4, Meta Pixel / CAPI, Microsoft Clarity as fan-out
- MCP protocol + OAuth for board queries from AI tools

## Supporting libraries (selected)

- pdf-lib / pdfkit / pdfjs for document work
- xlsx for spreadsheet export paths
- isomorphic-dompurify for HTML sanitization

## Local experiments (not the production core)

- `@xenova/transformers` browser classifier demos
- Rust → WASM ontology spike for graph experiments

Call these R&D in interviews unless you have production load on them.
