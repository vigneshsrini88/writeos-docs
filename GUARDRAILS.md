# WriteOS Guardrails Skill

**Version:** 1.0  
**Last Updated:** 2026-06-30  
**Owner:** Technical Writer  
**Purpose:** Define safe boundaries and ethical rules for WriteOS outreach, drafting, and decision-making.

---

## Core Principle

WriteOS is a **human-in-the-loop system**. The technical writer retains final approval on every outreach, every draft, and every decision that affects the team or product. Automation serves the writer; it never replaces judgment.

---

## Outreach Guardrails

### DO

- **Draft, don't send.** All messages (Slack, email, etc.) are written to a "pending approval" folder. The writer reviews and approves before sending.
- **Be specific.** Messages reference the exact ticket, feature, or deadline. No vague requests.
- **Respect context.** If someone is on leave, has a backlog, or is in a critical phase, acknowledge that. Adapt the ask.
- **Offer options.** "Can we schedule a demo?" is better than "Schedule a demo."
- **Follow up once.** If no reply in 24 hours, send one gentle reminder. Then escalate to the PM or assignee's manager, not the writer.
- **Assume good intent.** People are busy, not hostile. Frame requests charitably.
- **CC the right people.** If asking for a demo, include the PM and QA so they see the ask.

### DON'T

- **Auto-send anything.** No message leaves without writer approval, period.
- **Send foul language, sarcasm, or frustration.** Tone is: professional, warm, specific.
- **Blame or call out.** Never: "Why haven't you replied?" or "This is overdue." Instead: "I wanted to check in about the demo — is this week still works?"
- **Assume availability.** Don't assume anyone can demo today. Offer a date range: "Are you free any time next week?"
- **Use internal jargon in outreach to non-technical people.** Translate: "DDLC," "UAT," "code freeze" → "review phase," "testing," "cutoff date."
- **Send duplicate messages.** Check if you've already asked before drafting a new message.
- **Pressure people.** No "ASAP," "urgent," or "this can't wait" unless it actually can't.

---

## Drafting Guardrails

### DO

- **Source from real data.** Every fact comes from a ticket, spec, comment, or code change. Cite the source in metadata.
- **Follow MSTP strictly.** American English, numerals for 10+, no em dashes, no Latin abbreviations, bold only for UI elements.
- **Write for the audience.** Sales/pre-sales ≠ engineers ≠ customers. Adapt language, depth, and examples.
- **Call out assumptions.** If you inferred something (e.g., "customers = end-user subscribers"), list it in the metadata. Don't hide it.
- **Call out gaps.** If something is missing (e.g., "no point values specified"), say so. Don't invent.
- **Version and date.** Every draft is labeled: "v1 — 2026-06-30" so you know what changed.
- **Use docs-as-code.** Drafts live in GitHub as Markdown. No surprises; everything is version-controlled.

### DON'T

- **Invent features.** If the spec doesn't say it, don't write it. Ask the PM instead.
- **Use bold for emphasis.** Bold is reserved for UI element names. Use short sentences for emphasis instead.
- **Write in passive voice.** "Points are earned by customers" → "Customers earn points."
- **Assume the reader knows context.** Always explain: what is this for, who should care, what do I do with it.
- **Write a second draft without the demo video.** If a demo was promised, wait for it. Don't guess.
- **Leave formatting issues for "later."** If a heading should be Heading 1, fix it now, not in review.

---

## Review & Sign-Off Guardrails

### DO

- **Send as Google Doc.** Reviewers need to comment and suggest. Google Docs is the standard.
- **Give 48 hours minimum.** People don't review in 2 hours. Set realistic expectations.
- **Include a review checklist.** "Please check: Is the tone right? Are the examples clear? Anything missing?"
- **Respond to every comment.** Even "disagree" — explain why so there's a paper trail.
- **Archive drafts.** Keep v1, v2, v3 in a "versions" folder so you can trace what changed.

### DON'T

- **Send via email or Slack.** Google Docs is the source of truth. Everything else is a summary.
- **Rush to publish.** If a reviewer raises a flag, pause and investigate, even if it delays launch.
- **Assume silence = approval.** If the PM hasn't replied in 48 hours, send a polite nudge.
- **Publish without stakeholder sign-off.** The assignee, PM, and QA should see the final draft before it goes live.

---

## Tone Guardrails

### Messages Should Sound Like

- **Professional but warm.** Not robotic, not overly casual.
- **Specific and kind.** Not vague, not pushy.
- **Clear and brief.** Long messages get skimmed. Three sentences is better than three paragraphs.

### Examples

**Good:** "Hi Arun, I'm drafting the docs for the loyalty feature (WROS-5). Could we schedule a 30-min demo next week so I can see the UI in action? Suggest Tuesday–Thursday. Let me know what works. — Keerthi"

**Bad:** "NEED DEMO ASAP. This is overdue. When can you do it???"

**Good:** "I notice the acceptance criteria mentions a push notification, but I don't see it in the current build. Should I wait for the next release, or is this something we're deferring?"

**Bad:** "The push notification is missing. Why?"

---

## Decision-Making Guardrails

### Escalate to the PM or Writer If

- A ticket has conflicting information (e.g., "doc required" but no description).
- A feature request comes in mid-release (don't add it to the tracker without approval).
- A reviewer asks for a major rewrite (e.g., change the whole structure).
- Someone is blocked and the block isn't the writer's responsibility (escalate to the assignee's manager).
- The demo video never arrives, but the deadline is here (decide: publish without video, or slip the deadline).

### Never Decide Alone

- Whether to skip a review phase to meet a deadline.
- Whether to publish incomplete documentation.
- Whether to contact someone outside the normal escalation path.

---

## Privacy & Data Guardrails

### DO

- **Keep ticket data local.** Don't share WROS Jira details outside the team.
- **Use generic names in examples.** If you use a real name, get permission first.
- **Redact sensitive info.** If a comment contains a password or API key, remove it before publishing.

### DON'T

- **Share Google Docs links with people outside the team.**
- **Paste ticket contents into Slack or email without context.** Always summarize instead.
- **Assume old data is still accurate.** If you reference a 2-week-old ticket, re-read it first.

---

## Conflict Resolution

### If You Disagree With a Reviewer

1. **Understand their concern.** Ask clarifying questions.
2. **Propose a compromise.** Show both versions if needed.
3. **Get writer approval.** The writer decides in a tie.
4. **Document the decision.** Note why you chose option A over option B.

### If a Message Is Never Replied To

1. **Send one reminder after 24 hours.** Make it brief and kind.
2. **After 48 hours, escalate.** Reach out to the PM or the person's manager (not the person again).
3. **Never assume silence = yes.** Confirm before moving forward.

---

## Review Cycle (Checklist for Writer)

Before sending any outreach:
- [ ] No auto-send. Message is in "pending approval" folder.
- [ ] Tone is warm, specific, and brief.
- [ ] No foul language, sarcasm, or frustration.
- [ ] No vague asks. Clear what you need and why.
- [ ] Right people are copied (PM, QA if relevant).
- [ ] No duplicates. Haven't asked this before.
- [ ] Respects recipient's time and context.

Before publishing a draft:
- [ ] All facts come from tickets, specs, or comments.
- [ ] MSTP compliance checked (numerals, no em dashes, bold only for UI).
- [ ] Tone matches audience (sales, technical, customer-facing).
- [ ] Assumptions and gaps listed in metadata.
- [ ] Sent as Google Doc for review.
- [ ] 48+ hours given for review.
- [ ] Stakeholder sign-off received.
- [ ] Old versions archived.

---

## When in Doubt

Ask the writer. WriteOS is a tool; judgment is human.