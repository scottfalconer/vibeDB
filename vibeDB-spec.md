# vibeDB Specification

**vibeDB helps people and machines remember what matters, with context.**

Each record has six fields.  
Every field is optional. Use any combination, including none.  
The goal is to capture what was said or done, and the basic context around it - clearly and literally.

## Core Principles

- Records should stay close to what was actually said or done
- Fields are descriptive, not interpretive ("No Why in Vibe")
- Fields can contain compound values when naturally phrased that way
- Records should be easy to write, read, or generate - by hand or machine
- Records must be text-only (no images or binary data)
- Records must be self-contained (no external references or pointers)
- The point isn't structure. The point is context.

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

- Write records like you're explaining to a future teammate.
- It’s better to over-include `thing` than under-include.
- Ask: *Will this still make sense in 6 months to someone else?*
- Use tags in `how` for system context. (E.g., `auto-imported; jira:test:FOO-456`)
- Be literal. Don’t write what you *think* happened - write what was said or done.
- Don’t stress about compound values - if it feels natural, it’s fine.

## Implementation Notes

### Security & Privacy
vibeDB does not enforce access controls or privacy mechanisms. These concerns should be handled by the implementing system.

### Lifecycle Stages
vibeDB operations typically occur in three stages:

1. **previbe**: Data capture and preparation
2. **vibin**: Active use and management
3. **postvibe**: Search, archival, and forgetting

### Data Management
- Records may be archived, faded, or pruned according to implementation needs
- Multiple vibeDB instances may coexist, segmented by purpose or access level
- Implementation-specific indexing and materialization is encouraged

## Fields

Each field has a simple, literal meaning.  
Values may be compound (e.g. multiple people or tags) if that's how a human would naturally express them.

### Best Practices for Field Values

- Keep values literal and factual
- Use compound values only when naturally appropriate
- Avoid embedding metadata or IDs in content fields
- Place all system-readable tags in the `how` field
- Maintain consistent formatting within your implementation

---

### `who`

Who was involved.

**Examples:**
```
"Buzz Aldrin"
"support@acme.com"
"Lisa Rodriguez (Research Lead), User Experience Team, Steve (customer stakeholder)"
```

---

### `what`

What this record is about.

The `what` field provides a short, human-oriented description of the `thing`.  
It answers the question: **"What is this record about?"**

Think of it like a label on a folder or a sticky note on a page.  
It should be glanceable and meaningful to people.  
Use it to give semantic context - not system-level metadata.

**Examples:**
```
"feedback on onboarding flow"
"quote from stakeholder interview"
"timeout error in export job"
"support ticket escalation"
```

---

### `when`

When it happened.

Use dates or references that still make sense later.

**Examples:**
```
"2024-07-03"
"March 2024"
"the 80s"
```

---

### `where`

Where it happened.

This could be a place, tool, platform, file, or channel.

**Examples:**
```
"Zoom"
"#support-chat"
"docs/spec/v1.md"
```

---

### `how`

How the record was created or captured.

This can include traceability or system-readable tags.

**Examples:**
```
"auto-logged from API"
"pasted by support agent"
"transcribed from video; jira:test:TICKET-10422 customer:salesforce:id=acct_04213"
```

---

### `thing`

The actual content.

Use real, sourced material - not summaries. This might be a quote, HTML, code snippet, or full block of content.

**Examples:**
```html
<p>We've missed our reporting deadlines for two weeks. I need to escalate this.</p>
```

```markdown
> "We should sunset the legacy billing flow by Q2."
```

```json
{ "error": "TimeoutError", "details": "export:data job did not respond within 30s" }
```

---

## Format

vibeDB is format-agnostic.

Each record is a flat set of fields: `who`, `what`, `when`, `where`, `how`, and `thing`.

Records may be stored as:
- JSON
- JSONL (newline-delimited JSON)
- CSV
- YAML
- Markdown
- Plain text
- Any structure that clearly preserves field values

The spec defines **field meaning**, not file format.

---

## Example Records

### JSON

```json
{
  "who": "Devon Chen (QA), Mobile Team",
  "what": "regression in login flow",
  "when": "2024-11-02",
  "where": "internal Slack thread",
  "how": "manually added from Slack; jira:test:TICKET-10422 product:mobile",
  "thing": "<blockquote>Login breaks on iOS 17.1 when Face ID is enabled. Repro steps posted in the ticket.</blockquote>"
}
```

---

### JSONL

```json
{"who": "System Monitor", "what": "timeout in export service", "when": "2025-02-12", "where": "export logs", "how": "auto-ingested; sentry:issue=EXP-902", "thing": "TimeoutError: export:data:18327 did not respond within 30s"}
{"who": "Ravi (Enterprise Customer)", "what": "missed SLA notice", "when": "2025-01-04", "where": "Salesforce", "how": "added by AM; customer:salesforce:id=acct_987", "thing": "<p>'We've missed our reporting deadlines again. Please escalate.'</p>"}
```

---

### YAML

```yaml
who: Product Strategy Council
what: removal of legacy billing
when: Q4 2023
where: Jira decision log
how: parsed from Jira page; jira:decision:OPS-1921 project:billing
thing: >
  <div><strong>Decision:</strong> We will sunset legacy billing by end of Q2 2024. Stripe will be the sole pathway for invoicing.</div>
```

---

### CSV

```csv
who,what,when,where,how,thing
"Jesse, Lauren (customer)","requested call transcript","2024-08-17","Zoom","extracted from call recording; call:zoom:mtg-332-991","<p>'Can you send me the full call transcript for reference?'</p>"
```

---

## Design Philosophy

- Records should stay close to what was actually said or done  
- Fields are descriptive, not interpretive  
- Fields can contain compound values when naturally phrased that way  
- Records should be easy to write, read, or generate - by hand or by machine  
- The point isn't structure. The point is context.

---

## Version

**v1.1** - Added interpretive guidance and usage assumptions for human and AI systems

