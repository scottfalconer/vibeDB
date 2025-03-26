# vibeDB FAQ

## What is vibeDB?
**vibeDB** is a minimalist, text-based memory system designed to naturally store and recall important events. It uses six optional fields (`who`, `what`, `when`, `where`, `how`, `thing`) to capture factual context clearly, deferring interpretation for later use or analysis.

**Quick Links:** [Quickstart Guide](https://github.com/scottfalconer/vibeDB/blob/main/QUICK-START.md) | [Technical Spec](https://github.com/scottfalconer/vibeDB/blob/main/vibeDB-spec.md) | [GitHub Repo](https://github.com/scottfalconer/vibeDB)

---

## Why Use vibeDB?
vibeDB mirrors how people naturally remember and share information, providing clear, adaptable structures bridging informal conversations and structured records.

### Core Features:
- **No "Why" Field**: Records objective events, deferring interpretation.
- **Text-Based Simplicity**: No images, binaries, or external pointers.
- **Fully Optional Fields**: Supports incomplete or evolving information.
- **Strongly Supports Hashing**: Best practices and consistent structure enable reliable hashing.

---

## Why no 'why' field? (“No Why in Vibe”)
vibeDB primarily aims to capture **what happened** rather than **why** it happened. We recognize human and machine records are fallible and subjective, and we structure vibeDB to maintain factual clarity while accommodating these realities.

---

## How does hashing work in vibeDB?
While hashing isn't strictly a core feature, vibeDB's best practices and consistent structure strongly support and expect hashing to be used for flexible referencing. The specific order of fields (`who`, `what`, `when`, `where`, `how`, `thing`) is part of the vibeDB specification and must remain consistent for hashing reliability.

**Recommended hashing approach (early tests):**
- Hash each individual field's content (using SHA-1 or similar).
- Concatenate field hashes in the specified field order.
- Hash the combined result to create a unique hash for the entire record.

Other hashing mechanisms can also be used if consistently calculated.

**Best practices to maintain hash integrity:**
- Always maintain the specified field ordering.
- Avoid embedding tags or metadata within content fields (e.g., using `Matt (customer 1234)` in the `who` field).
- Use structured tagging exclusively in the `how` field (e.g., `customer:matt=1234`) to ensure consistent hashing and facilitate filtering without affecting hash values.

---

## Why exclude images or binary data?
Using exclusively text ensures portability, easy searching, and compatibility, avoiding complexities associated with handling specialized data formats.

---

## Why exclude external references or pointers?
vibeDB captures complete content directly within records for maximum portability and preservation of original context. This simplicity ensures records remain reliable and self-contained.

---

## Privacy and Access Considerations
vibeDB itself does not enforce access controls or privacy mechanisms. Users should carefully manage access and privacy separately during the `previbe`, `vibin`, or `postvibe` stages. A practical approach might involve creating personal vibeDB instances based on individual permissions and API access.

**Common Concerns:**
- **Data Overload?**: Archive, fade, or prune data according to preferences.
- **Security?**: Implement security and privacy through infrastructure and database choices.

---

## Real-World Examples of vibeDB Usage
vibeDB can be practically used for:
- Daily standup summaries.
- Detailed meeting notes and action items.
- Capturing customer support interactions.
- Archiving important Slack conversations.

---

## Design Principles and Decisions
vibeDB is guided by clear design principles:
- **Simplicity and Portability**: Effortless integration through text-based records.
- **Context Preservation**: Accurate original details capture.
- **Deferred Interpretation**: Keeping records factual.
- **Flexibility**: Optional fields accommodate evolving data.
- **Future-Oriented**: Facilitating easy integration with emerging technologies, especially AI.

These principles ensure vibeDB remains practical, adaptable, and useful across contexts.

---

## How Humans and AI Can Use vibeDB Records

**For Humans:**
- Quickly retrieve historical context.
- Easily reference exact details from past events.
- Support onboarding, training, and knowledge sharing.

**For AI & LLMs:**
- Provide structured, factual training data.
- Improve conversational and analytical accuracy.
- Facilitate precise information retrieval.

---

## Integrating vibeDB with Other Systems
vibeDB easily integrates across platforms:
- **CSV/Spreadsheets**: Capture or import structured records.
- **JSON**: Data exchange, API integrations, and AI use.
- **SQL Databases**: Robust storage, querying, analytics.
- **AI & ML Tools**: High-context training data or conversational prompts.

---

## Processes Around vibeDB
We plan to build tools and scripts across three defined stages (examples coming soon):

### previbe: Capturing and Preparing Data
- **Initialization Scripts**: Set up vibeDB on platforms like MySQL, Databricks, Cloudflare KV.
- **Extractors**: Pull structured data from Jira, Salesforce, Slack, etc.
- **Transformers**: Standardize and normalize data.
- **Parsers**: Convert notes or transcripts.
- **AI Tools**: Automate data enrichment.
- **Linters and Validators**: Ensure consistency and completeness.

### vibin: Using and Managing Data
- **Specialized Queries**: Efficient, hash-based data retrieval.
- **Custom Indexing**: Optimize search and linking.
- **Real-time Enhancements**: Automated record updates.

### postvibe: Managing, Searching, and Forgetting
- **Hash-based Search**: Quick content retrieval.
- **Materialized Tables**: Efficient queries and frequent access.
- **Archiving and Forgetting**: Automated fading, pruning, and data lifecycle management.

---

## Managing Multiple vibeDB Databases
vibeDB's hash-based referencing supports multiple databases:
- Separate short-term and long-term storage databases.
- Segment databases by department or topic.
- Flexibly recombine records using consistent hashes.
- Generate new hashes for structured forgetting and memory archival.

This ensures scalable, efficient data management across your organization.

---

## Open Source and Community Contribution
vibeDB is open-source and encourages your contributions:
- Enhanced integrations and tools.
- Optimizations for specific platforms and use cases.
- Ideas and implementations for improved data lifecycle management.

**[Learn How to Contribute](https://github.com/scottfalconer/vibeDB)**

---

## Visual Overview

```
[previbe] → [vibin] → [postvibe]
  │             │              │
  ├─ Setup      ├─ Query       ├─ Search
  ├─ Extract    ├─ Index       ├─ Archive
  ├─ Transform  ├─ Enhance     ├─ Forget
```

---

## Conclusion
vibeDB offers a practical, flexible approach to capturing clear and factual records. It enhances human-AI collaboration and integrates seamlessly with existing and future technologies. Always remember: **"No Why in Vibe"—interpretation and deeper analysis happen later.**

