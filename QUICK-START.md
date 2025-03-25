# Quick Start

Take 3 seconds to read this sentence:

> You just opened this page and read the first few lines.

Now here’s what you just did - written as a vibeDB record:

```json
{
  "who": "a reader",
  "what": "started the quick start walkthrough",
  "when": "a few seconds ago and still going",
  "where": "quick-start.md in the vibeDB repo on GitHub",
  "how": "url:https://github.com/scottfalconer/vibedb/blob/main/QUICK-START.md",
  "thing": "# Quick Start\n\nTake 3 seconds to read this sentence:\n\n> You just opened this page and read the first few lines.\n\nNow here’s what you just did - written as a vibeDB record:"
}
```

This is vibeDB.

---

We didn’t extract, summarize, or label anything.  
We just recorded what happened - with the full context attached.

---

## 🧠 Try It in Your LLM

Copy the record above and paste it into your LLM of choice - Claude, GPT-4, etc.

Then try prompts like:

- “What happened?”  
- “Why might this be useful?”  
- “Explain this in plain language.”  
- “Is there anything missing from this record?”  
- “What could this be used for if I had a bunch of them?”

You're not writing for a database.  
You're writing for someone - or something - that needs to understand later.

---

## Sample Records to Explore

Want to try more?

- [First Moon Landing](./samples/moon-landing.json)  
- [A critical escalation](./samples/escalation.json)  
- [A customer quote from a demo](./samples/demo-quote.json)  
- [A changelog entry](./samples/changelog.json)  
- [A conversation about a decision](./samples/internal-decision.json)

Each one is a moment.  
Each one is stored in the same shape.

You can paste them into an LLM - or stack them up and start building memory.

---

## 🛠️ What’s Next?

You probably want to operationalize this.

- Pipe in Slack messages  
- Extract from support tools  
- Generate records with AI  
- Store them in `.jsonl`, a spreadsheet, or a Snowflake table  
- Start building reasoning, summaries, and timelines on top

vibeDB gives you the shape.  
You decide where it goes - and what comes next.
