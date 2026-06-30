# WriteOS

WriteOS is a technical writing orchestration system. It connects your project management, specification, and publishing tools into a single workflow, so a technical writer can take any release from raw tickets to reviewed, published documentation without juggling tools manually.

WriteOS is built for technical writers who manage documentation across a release cycle: ingesting tickets, triaging what needs a doc, drafting from specs, coordinating reviews, and publishing to the right place at the right time.

---

## The problem WriteOS solves

Documentation for a product release touches many systems: a Jira project for tickets, a Confluence space for specs, a Google Doc for drafts, a tracker for status, and a Slack or email thread for chasing demos and sign-offs. Without orchestration, the writer context-switches constantly and important steps get missed.

WriteOS wires these systems together through a six-layer pipeline. Each layer does one job and hands off to the next. The writer stays in control at every approval gate; WriteOS handles the plumbing.

---

## Who WriteOS is for

- Technical writers managing documentation for a product release.
- Writing teams that use Jira for tickets, Confluence for specs, and Google Drive for drafts and trackers.
- Teams that want a repeatable, auditable doc pipeline without a custom codebase.

---

## The six-layer pipeline
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/6346b52a-a282-4e32-b792-c6f6a35241f7" />


### Layer 1: Connectors (live, MVP)

WriteOS connects to your tools through MCP servers: Jira, Confluence, Google Drive, Gmail, and Google Calendar. You configure each connection once. WriteOS reads and writes to these tools on your behalf, within the guardrails you set.

See [./GUARDRAILS.md](./GUARDRAILS.md) for the rules WriteOS follows when reading, writing, and sending on your behalf.

### Layer 2: Ingestion (live, MVP)

WriteOS reads every ticket in your project and stores a local Markdown snapshot in your repository. Each snapshot captures the ticket summary, description, acceptance criteria, comments, and attachments. Ingestion runs at the start of a release cycle and can be re-run at any time to pick up updates.

### Layer 3: Triage (live, MVP)

WriteOS inspects each ingested ticket and decides whether it requires documentation. Triage checks for a `doc_flag`, a UI/UX flag, a description, and acceptance criteria. Tickets that need a doc are marked for drafting. Tickets that do not are noted in the release tracker with a reason. The writer reviews the triage output before drafting begins.

### Layer 4: Drafting (live, MVP)

For each ticket flagged for documentation, WriteOS reads the Confluence spec linked in the ticket, then drafts a concept page or how-to guide in Markdown. The draft is saved locally and uploaded to Google Docs for review. Every draft includes a metadata block: source ticket, source spec, assumptions, and gaps. The writer reviews and approves the draft before it moves to outreach.

### Layer 5: Outreach (Phase 2)

WriteOS drafts targeted messages to the people named on each ticket: requesting demos, chasing missing acceptance criteria, or asking for spec updates. All messages go to a pending-approval queue. Nothing is sent without explicit writer approval. Outreach uses the tone and escalation rules defined in [./GUARDRAILS.md](./GUARDRAILS.md).

### Layer 6: Review and DDLC (Phase 2)

WriteOS manages the review cycle. It sends the Google Doc to the stakeholder list, tracks whether comments have been resolved, and prompts the writer when sign-off is overdue. When the doc is approved, WriteOS publishes it to the configured destination and updates the release tracker with the final doc link.

---

## How to use WriteOS

### Prerequisites

- A Jira project with tickets using the `doc_flag` label convention.
- A Confluence space with spec pages linked from tickets.
- A Google Drive folder for drafts and a release tracker spreadsheet.
- MCP servers for Jira, Confluence, and Google Drive connected to your Claude Code session.

### Step 1: Point WriteOS at your project

Replace the placeholders below with your own project details. You do not need to edit any code. Set these in your session or in a `.env` file:

```
PROJECT_KEY=<YOUR_PROJECT_KEY>          # Example: MYPROJ
CONFLUENCE_SPACE=<YOUR_SPACE_KEY>       # Example: DOCS
TRACKER_URL=<YOUR_TRACKER_URL>          # Example: https://docs.google.com/spreadsheets/d/<ID>/edit
RELEASE_NAME=<YOUR_RELEASE_NAME>        # Example: Q3 2026 Release
RELEASE_DATE=<YYYY-MM-DD>              # Example: 2026-09-30
```

### Step 2: Run ingestion

Ask WriteOS to ingest your project:

> "Ingest all tickets from `<YOUR_PROJECT_KEY>` and save them to `tickets/`."

WriteOS reads each ticket and saves a Markdown snapshot locally. Review the snapshots to confirm they look correct before proceeding.

### Step 3: Run triage

Ask WriteOS to triage the ingested tickets:

> "Triage the tickets in `tickets/` and update the release tracker."

WriteOS marks each ticket as requiring a doc or not, with a reason. Review the tracker at `<YOUR_TRACKER_URL>` before proceeding.

### Step 4: Run drafting

For each ticket flagged for documentation, ask WriteOS to draft:

> "Draft the concept page for `<YOUR_PROJECT_KEY>-<NUMBER>` using the linked Confluence spec."

WriteOS reads the spec, drafts in Markdown, saves to `drafts/`, and uploads to Google Docs. Review the draft and fill in any gaps listed in the metadata block before approving.

### Step 5: Review and publish (Phase 2)

Once drafting is complete, WriteOS will coordinate outreach and the review cycle. Until Phase 2 is live, the writer handles these steps manually using the release tracker and Google Docs.

---

## Architecture and design decisions

### Why MCP

WriteOS uses Model Context Protocol servers instead of custom API integrations. MCP servers are maintained by the tool vendors, handle authentication, and expose a consistent interface. Adding a new tool means connecting a new MCP server, not writing a new integration.

### Why local Markdown

Drafts are saved as Markdown in a Git repository before they go anywhere else. This gives the writer version control, a diff history, and a local backup that does not depend on any external service. Markdown is also the format that WriteOS reads from and writes to, so the pipeline is consistent end to end.

### Why Google Docs for review

Reviewers need to comment and suggest edits in a shared interface. Google Docs is where most stakeholders already work, and it supports inline comments, suggestion mode, and a clear resolution flow. The writer owns the canonical Markdown version; the Google Doc is the review surface.

### Why approval-gated outreach

Every message WriteOS drafts goes to a pending-approval queue. WriteOS does not send anything automatically. This is a deliberate design choice: outreach involves real people and real relationships, and the writer is accountable for what gets sent. The guardrails in [./GUARDRAILS.md](./GUARDRAILS.md) define the tone, escalation path, and limits WriteOS follows when drafting messages.

---

## Roadmap

### Phase 1: MVP (live)

- Connectors: Jira, Confluence, Google Drive via MCP.
- Ingestion: ticket snapshots saved as local Markdown.
- Triage: doc-flag detection and release tracker population.
- Drafting: spec-grounded concept pages with metadata, saved locally and uploaded to Google Docs.

### Phase 2: Outreach and review

- Outreach: approval-gated draft messages for demos, missing criteria, and spec updates.
- Review and DDLC: stakeholder routing, comment tracking, sign-off prompts, and final doc publishing.

### Phase 3: Scale and automation

- Multi-project support: run WriteOS across several project keys in parallel.
- Template library: configurable doc templates by type (concept, how-to, reference, release note).
- Analytics: track time from ticket to published doc, identify recurring gaps, and surface patterns across releases.

---

## Demo instance: Loyalty Programme (WROS)

This section documents the example instance WriteOS was first built and tested on. Replace it with your own project's details when you adopt WriteOS.

| Resource | Link |
|---|---|
| Jira project | https://writeos.atlassian.net/jira/software/c/projects/WROS/issues |
| Confluence spec | https://writeos.atlassian.net/wiki/spaces/Loyalty/pages/950273/Loyalty+Programme+Product+Spec |
| Release Tracker (Google Sheet) | https://docs.google.com/spreadsheets/d/1gpX8BaR_QIFPeOUixg07bZ25IU1QkQnqh3JHsiBpdwc/edit |
| First Draft (Google Doc) | https://docs.google.com/document/d/1Mak2NSay6vsWCpKU_m2_oUeSAPYUAk40Ti8TQqbAIpQ/edit |
| Docs repository | https://github.com/vigneshsrini88/writeos-docs |
| Code repository | https://github.com/vigneshsrini88/writeos-code |
