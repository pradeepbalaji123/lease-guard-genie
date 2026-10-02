# Lease Sentinel

Build a web app called "Lease Guard" that reviews rental agreements using a

multi-agent AI workflow with real LLM calls.

UI:

- Left: textarea to paste a lease + "Analyze" button + "Load sample lease" button.

- Right: an "Agent Pipeline" panel showing each agent as a card with status

  (Idle / Running / Done), a spinner, elapsed time, and expandable raw output.

- Bottom: final report with risk score (0-100 gauge), top 5 red flags

  (severity badges), questions to ask the landlord, and a copyable

  negotiation email.

Backend (Lovable Cloud edge functions, use Lovable AI gateway, no user API key):

1. orchestrator: reads the lease and returns JSON {agents_needed:[...],

   clause_assignments:{legal:[], financial:[], rights:[]}, reasoning}.

2. Run legal, financial, and tenant_rights agents IN PARALLEL

   (Promise.all), each with its own system prompt and JSON output schema.

3. critic: receives all findings, flags contradictions, unsupported claims,

   and missing issues; returns corrections.

4. synthesizer: produces the final report JSON.

Stream status updates to the UI after each stage so the pipeline visibly

progresses. Handle errors and rate limits with friendly messages.

Design: clean, modern, dark/light friendly, with an agent-flow diagram

at the top that highlights the active agent. Add a disclaimer: "Not legal advice."

Include a "How it works" section explaining the orchestration.

This project was built with [Lovable](https://lovable.dev).

**Live app**: https://lease-guard-genie.lovable.app

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/f165d06f-1f2c-4176-9cef-715c680abd68).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
