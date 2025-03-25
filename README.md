# vibeDB

**A foundational database for shared memory - for you and emerging intelligence.**

---

## Try the 10-Second Quick Start

Want to see how it works?

[Quick Start →](QUICK-START.md)

No setup. No boilerplate.  
Just a few fields. Then you’ll get it.

---

## Or explore the full spec

[Spec →](vibeDB-spec.md)

---

**vibeDB is a shared structure for storing moments that matter - with just enough shape to be useful later.**  
What matters isn’t how you store it - it’s that the fields and structure mean something.

---

It reflects how we naturally make sense of the world.

When we explain what happened, we instinctively answer:  
> **Who, what, when, where, how.**

vibeDB takes the human way of explaining things - and turns it into a shape machines can understand.

You’re not building a dataset.  
You’re not writing a summary.  
You’re just saving a moment - in a format that can be reasoned over later.

---

> **As humans, we remember what feels important - and we remember it with context.**  
> Later, that context is what helps us understand, explain, and act.  
>
> vibeDB is a way to do the same thing, on purpose - so that both people and models can pick up the thread.

---

## What’s in a vibeDB Record?

Only six fields - all optional:

- `who`: the person, system, or team involved  
- `what`: the action or event  
- `when`: when it happened - written so it still makes sense later (e.g. "2024-07-03", "March 2024", "the 80s")  
- `where`: the surface, channel, or context  
- `how`: the behavior or mechanism - how it happened or progressed over time  
- `thing`: the actual content - what was said, shown, or shared  

You can log just a `thing`.  
Or just a `who`.  
Or wrap a moment in a full shape with all six.

You don’t extract, summarize, or label early.  
You just capture what was present - clean, contextual, and ready to evolve.

---

## What Goes in `thing`?

Use the part of reality you’d actually share if someone asked:  
> “What happened in the meeting?”

You wouldn’t say:  
> *“I sat down in a chair.”*

You wouldn’t just summarize either:  
> *“We rolled back the release.”*

You’d probably say:  
> *“There was a lot of debate - here, read the transcript.”*

> If you’d say, *“Here, read this - it explains it,”*  
> that’s your `thing`.

You’re not trying to extract the meaning or simplify the content - you’re capturing the source.  
That’s the memory. That’s what goes in `thing`.

---

## What About `how`?

`how` answers the question of behavior - the nature of the process, or the cause behind a sequence of events.  
It’s often useful for traceability or understanding flow across systems.

---

## No `why`

There’s no `why` field in vibeDB.  
Why is interpretive.

It belongs in a layer above - not embedded in the record itself.

---

## No IDs, No Graphs

vibeDB doesn’t assign global IDs.  
It doesn’t build a graph.  
It doesn’t create relationships.

But it’s structured enough to support all of that - if you want it.

---

## What About Hashing?

vibeDB doesn’t include hashing - but it enables it.

Because every record is flat and structured, you can:

- Generate hashes of any field (`thing`, `who`, etc.)  
- Hash combinations (`who+what+when`)  
- Track shared content across time  

---

## Format-Agnostic

vibeDB records can live in JSON, YAML, Markdown, CSV, or any other human- or machine-readable format.

Structure matters. File type doesn’t.

---

## Why It’s Called vibeDB

Yes, it’s a nod to “vibe coding.”

Can you use vibeDB to vibe code? Yes.  
Can you use it for something serious? Also yes.

vibeDB gives you shared structure - light enough to drop into an AI IDE, durable enough to support meaning.
