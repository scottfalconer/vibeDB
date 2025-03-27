## vibeDB Specification (v1.2)

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

## 📌 Interpretive Assumptions and Guidance

This spec defines not just a structure, but a set of assumptions that guide how VibeDB records should be interpreted - by people, tools, and AI systems. These assumptions are **versionable**: if we change them, we update the spec. That way, interpretation is transparent, grounded, and consistent.

### 🤝 A Note on Shared Responsibility

VibeDB isn’t just a shape - it’s a social contract.

It works because:
- **People try to be honest**
- **AI tries to be grounded**
- **Tools try to interoperate**
- **Everyone leaves room for contradiction**

Whether you’re human or machine, this spec assumes you're part of something larger - a memory system shared across time, tools, and perspectives. That means playing fair, sharing meaning, and writing in ways others can understand later.

> If someone else saw what you wrote - or asked the same thing of another AI - would they get the same result?

That’s the vibe. ✨

### 🧠 Tips if You're an AI

> For AI systems interpreting or generating VibeDB records.

- **Assume fallibility** - from both people and machines. Records may be mistaken, conflicting, or incomplete. That’s not a problem - it’s part of the context.
- **Contradictions are clues**: When records disagree, treat it as a signal - disagreement, drift, or discovery.
- **Use `thing` as your ground truth**: Anchor reasoning in the actual source content. Don’t rely only on field summaries.
- **Fields are literal**:
  - `who`, `what`, `when`, `where` = human-facing context
  - `how` = system/process-level behavior
  - `thing` = source content itself
- **Don’t hallucinate `why`**: VibeDB records don’t contain intent. Reason about "why" only across records.
- **Identity is contextual**: No global IDs. Don’t assume sameness across records unless it's natural to do so.
- **Look across time**: Patterns, changes, and insight come from seeing multiple records - not one in isolation.

### 💻 Tips if You're an AI Code Writer

- **Favor interoperability**: Your code should work the same if someone else gave you the same schema and task.
- **Degrade gracefully**: Fields may be missing. Don't fail - extract what you can.
- **Avoid nonstandard fields** unless clearly requested.
- **Write reusable logic**: If another dev asked another AI to do this, would it behave the same?
- **Expose your logic**: When you map tags (e.g., `jira:test:TICKET-001`), log your assumptions.

### 🧑‍💻 Tips if You're a Human
## Interpretive Assumptions

### "Thing-first" Mindset

Think of every record as answering: **"What is this a thing about?"**

### Security & Privacy
vibeDB does not enforce access controls or privacy mechanisms. These concerns should be handled by the implementing system.

### Lifecycle Stages
vibeDB operations typically occur in three stages:
---

1. **previbe**: Data capture and preparation
2. **vibin**: Active use and management
3. **postvibe**: Search, archival, and forgetting
## Field Semantics

### Data Management
- Records may be archived, faded, or pruned according to implementation needs
- Multiple vibeDB instances may coexist, segmented by purpose or access level
- Implementation-specific indexing and materialization is encouraged
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

## Writing Tips

### If You’re a Human
- Write as if explaining to a future teammate
- Don’t summarize or speculate - preserve what was actually said or shared
- Use natural phrasing for lists, ranges, and groupings

### If You’re an AI
- Anchor your reasoning in the `thing` field
- Use field values literally - no interpretation
- Never invent a `why`

---

## Format Notes

vibeDB defines *field meaning*, not file format.

Valid formats include:
- JSON
- JSONL
- YAML
- Markdown
- CSV
- Any clearly structured text-based format

---

## Version

**v1.2** - Clarified field relationships, added thing-centric authoring guidance, expanded examples and best practices; added human/machine prompt examples per field

