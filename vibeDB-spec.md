## vibeDB Specification

**vibeDB helps people and machines remember what matters, with context.**

Each record has six fields. Every field is optional. Use any combination, including none. The goal is to capture what was said or done, and the basic context around it - clearly and literally.

---

## Core Principles

- Records should stay close to what was actually said or done
- Fields are descriptive, not interpretive ("No Why in Vibe")
- Fields can contain compound values when naturally phrased that way
- Records should be easy to write, read, or generate - by hand or machine
- Records must be text-only (no images or binary data)
- Records must be self-contained (no external references or pointers)
- The point isn't structure. The point is context.
- Every record is centered on a specific **thing**

---

## Interpretive Assumptions

### A Social Contract

vibeDB isn’t just a schema - it’s a shared memory protocol. It works because:

- **People try to be honest**
- **AI systems stay grounded**
- **Tools are interoperable**
- **Everyone leaves room for contradiction**

This means:
- Don’t assume a single truth. Contradictions may reveal drift, change, or multiple perspectives.
- Be generous with context. Write for someone else who wasn’t there.
- Keep reasoning anchored in real content - especially in the `thing` field.

> Ask yourself: If someone else saw what you wrote - or asked the same thing of another AI - would they get the same result?

That’s the vibe.


### "Thing-first" Mindset

Think of every record as answering: **"What is this a thing about?"**

- Encourage prompts and UI to emphasize *"this is a thing about..."* over *"X happened"*
- The `thing` field should contain actual, referenceable content - it's the anchor
- All other fields describe this `thing` - not general events or summaries

---

## Field Semantics

### `thing` - The Actual Content

This is the anchor. It’s what the record is *about* - a quote, a document, a log line, a transcript, a block of source code, etc. 

- Preserve structure and formatting (HTML, Markdown, JSON, etc.)
- Minimal cleanup only (e.g. redaction, basic trimming)
- Don't summarize, rephrase, or interpret

**Good human prompt:** "Paste the actual thing you want to remember or reference."

**Good machine prompt:** "Extract the full source content, keeping original structure. Don’t summarize or rephrase."

---

### `what` - What This Thing Is

A short, glanceable label describing the `thing`.

- Human-readable, like a sticky note or folder label
- Not a summary - a *pointer* or identifier
- Helps categorize or scan records quickly

**Examples:**
- "quote from stakeholder interview"
- "Ben’s comment on the outage thread"

**Relationship to `thing`:** The `what` field gives a semantic handle; the `thing` field holds the full source.

**Good human prompt:** "What is this thing? Label it for your future self."

**Good machine prompt:** "Give a short, human-oriented label for the content. Avoid summarizing."

---

### `who` - Who Was Involved

People, roles, or entities connected to the `thing`.

- Mix individuals, roles, and groups if helpful
- Include context like roles or relationships (e.g. "Lisa (PM)", "Steve (tech lead at Acme)")
- Be specific: name the people and organizations clearly. If multiple groups are involved, list them all (e.g. "customers from Acme, Wizco, and Google")

**Examples:**
- "Buzz Aldrin"
- "Support team, Lisa Rodriguez (Research Lead), Steve (customer)"

**Good human prompt:** "Who was involved? Include names, roles, or groups."

**Good machine prompt:** "Extract names, roles, or teams mentioned as being involved with the content."

---

### `when` - When It Happened

Use **anchored** time expressions. Make sure it’ll still make sense in 6 months.

**Prefer:**
- "2024-07-03"
- "March 2024"
- "Q1 2025"

**Avoid:**
- "Yesterday"
- "Last week"

**For recurring/ongoing things:**
- Use natural ranges: "April–June 2024"
- Use descriptions: "Every Friday in Q2"

**Good human prompt:** "When did this happen? Use clear, calendar-based phrasing."

**Good machine prompt:** "Extract dates or time ranges that situate the event clearly in time."

---

### `where` - Where It Happened

Not just physical space - use tools, platforms, locations, files, etc.

**Examples:**
- "Zoom"
- "Slack #support-chat"
- "docs/spec/v1.md"

**For distributed/multichannel things:**
- Combine sources: "Zoom + Slack"
- Use conceptual labels: "Hybrid offsite"

**Good human prompt:** "Where did this occur? Mention tools, locations, or platforms."

**Good machine prompt:** "Extract location, channel, or context where the content originated."

---

### `how` - How This Was Captured or Created

Describe process, tools, systems, or tags relevant to the record’s creation.

- Use structured traceability (e.g. `jira:test:TICKET-10422`)
- Include methods: "auto-imported", "transcribed via Otter.ai"

**Examples:**
- "manually copied from email"
- "transcribed from video; jira:test:TICKET-10422"
- "summarized by AI assistant"

**Focus on:**
- Methods of creation
- Source systems
- Traceable states

**Good human prompt:** "How was this record created or captured? Include any systems or tags."

**Good machine prompt:** "Extract traceable system metadata or method of capture. Use semicolon-separated tags if needed."

---

## Security, Privacy, and Lifecycle

### Security & Privacy
vibeDB does not enforce access controls or privacy mechanisms. These concerns should be handled by the implementing system, depending on the use case and context. Records may contain sensitive information and should be stored, shared, and processed accordingly.

### Lifecycle Stages
vibeDB operations typically occur in three stages:

1. **previbe** – data capture and preparation
2. **vibin** – active use and interaction
3. **postvibe** – archival, retrieval, and forgetting

### Data Management
- Records may be archived, faded, or pruned depending on implementation design
- Multiple vibeDB instances may coexist, segmented by purpose, audience, or retention
- Implementation-specific indexing, filtering, and summarization are encouraged for performance and usability

## AI & Code Implementation Guidance

### Tips if You're an AI

- **Use `thing` as ground truth** - always anchor reasoning in the actual content.
- **Fields are literal** - do not reinterpret `who`, `what`, `when`, `where`, or `how`.
- **Avoid fabricating intent** - there is no `why` field; inference should come from context across records.
- **Expect gaps** - not all fields will be present; treat missing info as normal.
- **Contradictions are meaningful** - differing records can signal change, disagreement, or drift.
- **Identity is contextual** - no global IDs; don't assume sameness across records unless it’s natural.
- **Look across time** - patterns and insights often come from seeing multiple records, not just one.

