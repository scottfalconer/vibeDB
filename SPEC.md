# vibeDB Specification

**vibeDB helps people and machines remember what matters, with context.**

Each record has six fields.  
Every field is optional. Use any combination, including none.  
The goal is to capture what was said or done, and the basic context around it - clearly and literally.

---

## Fields

Each field has a simple, literal meaning.  
Values may be compound (e.g. multiple people or tags) if that’s how a human would naturally express them.

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
It answers the question: **“What is this record about?”**

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
<p>We’ve missed our reporting deadlines for two weeks. I need to escalate this.</p>
```

```markdown
> “We should sunset the legacy billing flow by Q2.”
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
{"who": "Ravi (Enterprise Customer)", "what": "missed SLA notice", "when": "2025-01-04", "where": "Salesforce", "how": "added by AM; customer:salesforce:id=acct_987", "thing": "<p>'We’ve missed our reporting deadlines again. Please escalate.'</p>"}
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

- Records should stay close to what was actually said or done.  
- Fields are descriptive, not interpretive.  
- Fields can contain compound values when naturally phrased that way.  
- Records should be easy to write, read, or generate - by hand or by machine.  
- The point isn’t structure. The point is context.

---

## Version

**v1** - Initial release
