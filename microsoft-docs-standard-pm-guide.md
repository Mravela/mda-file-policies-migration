# Microsoft Learn documentation standard — PM authoring guide

> **Purpose:** This guide teaches product managers how to write migration and deprecation documentation that meets the Microsoft Learn publishing standard. Use it when authoring any article destined for `learn.microsoft.com`.

---

## Why the standard matters

Articles on Microsoft Learn are read by customers, field engineers, MVPs, and support teams worldwide. Microsoft enforces a consistent structure so readers can:

- Quickly determine whether an article applies to them.
- Find the steps they need without reading the entire article.
- Trust that the content is accurate, current, and complete.

Content that does not follow this standard will not pass editorial review and will not be published.

---

## The two document types you will use most

| Type | When to use | `ms.topic` value |
|---|---|---|
| **How-to** | Step-by-step instructions to complete a specific task, including migrations | `how-to` |
| **Concept** | Background explanation of what something is and why it matters | `concept` |

Migration and deprecation articles are almost always **how-to** articles. The structure below applies to how-to articles.

---

## Required structure for a how-to / migration article

Every article must follow this section order. Do not add, rename, or reorder these sections without editorial approval.

```
YAML front matter          ← machine-readable metadata (not visible to readers)
H1 title                   ← one sentence, action-oriented
Applies to block           ← products and plans this article covers
Opening paragraph          ← what the article does, one short paragraph
[!IMPORTANT] callout       ← if there is a deadline or critical action (deprecations only)
## What changed            ← for deprecations: describe exactly what was retired
## Who is affected         ← help readers self-identify
## Feature mapping table   ← old capability → new capability
## Before you begin        ← prerequisites, roles, licenses
## <Task name>             ← the main how-to steps (can be split into sub-steps)
  ### Step 1: ...
  ### Step 2: ...
## Frequently asked questions   ← optional but recommended for deprecation articles
## Next steps              ← always the final section; 4–8 links maximum
```

---

## YAML front matter (required)

Every article begins with a YAML block between `---` lines. This is metadata used by the publishing system. Readers do not see it.

```yaml
---
title: <Action verb> from <source> to <destination>
description: <One sentence. What the reader will accomplish. 160 characters max.>
ms.service: <service-slug>          # e.g., defender-cloud-apps
ms.topic: how-to                    # concept | how-to | overview | reference | tutorial
ms.author: <Microsoft alias>        # your Microsoft email alias without @microsoft.com
author: <GitHub username>
ms.date: MM/DD/YYYY                 # date of last substantive edit
ms.collection:
  - m365-security
  - tier2
---
```

**Rules:**
- `title` must match the H1 heading exactly.
- `description` must be unique and must not duplicate the title.
- `ms.date` must be updated every time you make a substantive change.
- Do not add fields that are not in the approved list. Extra fields cause build failures.

---

## H1 title

- One per article. Written in sentence case (capitalize only the first word and proper nouns).
- Action-oriented for how-to articles: starts with a verb.
- Must match the `title` field in YAML front matter exactly.

✅ `# Migrate from Microsoft Defender for Cloud Apps file policies to Microsoft Purview DLP`  
❌ `# File Policies Deprecation and Migration to Microsoft Purview` ← title case, not action-oriented

---

## Applies to block

Immediately after the H1, list the products this article covers. Use bold product names linked to their overview articles where possible.

```markdown
**Applies to:**
- Microsoft Defender for Cloud Apps
- Microsoft Purview Data Loss Prevention
- Microsoft Purview Information Protection
```

This is not a callout box. It is a plain bold label followed by a list.

---

## Opening paragraph

- One short paragraph (3–5 sentences maximum).
- Describes what the article covers and what the reader will be able to do after reading it.
- Written in second person: use **you**, not "the user" or "administrators".
- Does not repeat the title.

✅ `File policies in Microsoft Defender for Cloud Apps that use the built-in DLP content inspection engine are deprecated. This article explains what changed, who is affected, and how to migrate your existing file policies to Microsoft Purview DLP.`  
❌ `This document provides comprehensive guidance on the deprecation of File Policies...` ← passive, wordy

---

## Callout syntax

Microsoft Docs uses four standard callout types. Use them exactly as shown — the `[!TYPE]` syntax is required for the rendering engine.

```markdown
> [!NOTE]
> Use for supplementary information that is not critical but helpful.

> [!TIP]
> Use for optional best practices or shortcuts.

> [!IMPORTANT]
> Use for information the reader must act on to avoid problems.

> [!CAUTION]
> Use for actions that could cause data loss, security risk, or irreversible changes.

> [!WARNING]
> Use for conditions that will break something or cause serious harm.
```

**Rules:**
- Use `[!IMPORTANT]` for deprecation deadlines. Do not use it for every piece of information.
- Do not nest callouts inside each other.
- Do not use callouts as a substitute for proper paragraph writing.

---

## Heading hierarchy

| Level | Use for |
|---|---|
| H1 (`#`) | Article title. One per article. |
| H2 (`##`) | Major sections. These appear in the in-page TOC. |
| H3 (`###`) | Sub-steps or sub-sections within an H2. |
| H4 (`####`) | Use sparingly. Only when H3 is insufficient. |

Never skip levels. Do not go from H2 to H4.

---

## Writing numbered steps

Use numbered lists for all procedures. Each step must be a single action.

```markdown
1. In the Microsoft Defender portal, go to **Cloud Apps** > **Policies** > **Policy management**.
1. Select the **Information Protection** tab.
1. Filter by **File policy** type.
```

**Rules:**
- All list items start with `1.` — the publishing system auto-increments. This makes reordering easier.
- Bold all UI element names: button labels, menu items, tab names, field names.
- Use `>` for navigation paths: **Cloud Apps** > **Policies** > **Policy management**.
- Each step starts with an action verb: *Select*, *Go to*, *Enter*, *Review*, *Verify*.
- Do not combine two actions into one step.

✅ `1. Select the **Information Protection** tab.`  
❌ `1. Select the **Information Protection** tab and then filter by File policy.` ← two actions

---

## Tables

Use tables for:
- Feature mapping (old capability → new capability)
- Prerequisite requirements (capability → license)
- Comparison of two approaches

```markdown
| Column header | Column header |
|---|---|
| Row content | Row content |
```

**Rules:**
- Every table must have a header row.
- Use `|---|---|` as the separator. Alignment characters (`:---:`) are optional.
- Bold the first column when it names the item being described.
- Do not use tables for simple lists of items — use bullet points instead.

---

## Voice and tone

| ✅ Do | ❌ Don't |
|---|---|
| Write in second person: **you**, **your** | Write "the user", "administrators", "one should" |
| Use active voice: "Select **Save**" | Use passive voice: "The policy should be selected" |
| Use present tense: "Purview DLP supports..." | Use future tense: "Purview DLP will support..." |
| Be direct: "This policy is deprecated." | Soften unnecessarily: "This policy may be considered deprecated." |
| Sentence case for headings | Title Case For Every Word In Headings |
| Spell out abbreviations on first use: "data loss prevention (DLP)" | Use acronyms without defining them |

---

## Links

```markdown
[Link text](URL)
```

**Rules:**
- Link text must describe the destination: `[Learn about DLP](url)`, not `[click here](url)`.
- Use relative links for articles within the same docset (same `ms.service`).
- Use absolute URLs for articles in different docsets.
- Do not use bare URLs as link text.
- Do not link every occurrence of a term — link on first use in a section, then use plain text.

---

## "Next steps" section

The **Next steps** section is always the last section of every article. It helps readers continue their journey.

```markdown
## Next steps

- [Create and deploy DLP policies](https://learn.microsoft.com/...)
- [Learn about Microsoft Purview DLP](https://learn.microsoft.com/...)
- [Get started with Activity Explorer](https://learn.microsoft.com/...)
```

**Rules:**
- 4–8 links maximum. More than 8 is overwhelming.
- Each link must point to a logical next action or deeper reading — not back to the current article.
- Use action-oriented link text: "Create and deploy..." not "DLP policies".
- No introductory paragraph needed. Just the list.

---

## Common mistakes to avoid

| Mistake | Correct approach |
|---|---|
| Using a custom callout box style (colored div, bold label) | Use standard `> [!NOTE]` syntax only |
| Including a visual timeline graphic | Use a table or a numbered list with dates |
| Writing "please" or "simply" | Remove these words — they add no meaning |
| Using "click" | Use "select" — not all users have a mouse |
| Including screenshots for every step | Include screenshots only when the UI is complex or non-obvious |
| Starting a step with "You need to..." | Start with the action verb: "Select...", "Go to...", "Enter..." |
| Saying "as mentioned above" | Link directly to the relevant section |
| Ending an article with "Summary" | End with "Next steps" — always |

---

## Checklist before submitting

Run through this checklist before sending your article for editorial review.

- [ ] YAML front matter is complete and all required fields are filled in.
- [ ] H1 title matches the `title` field in YAML exactly.
- [ ] "Applies to" block is present immediately after the H1.
- [ ] Opening paragraph is 3–5 sentences in second person.
- [ ] All callouts use `> [!NOTE]` / `> [!IMPORTANT]` / `> [!TIP]` / `> [!CAUTION]` syntax.
- [ ] All headings are in sentence case.
- [ ] All numbered steps start with `1.` and contain one action each.
- [ ] All UI element names are in **bold**.
- [ ] All navigation paths use `>` notation.
- [ ] Tables have header rows and bold first column.
- [ ] No bare URLs — all links have descriptive link text.
- [ ] Last section is "Next steps" with 4–8 links.
- [ ] No "click" — use "select".
- [ ] No "please" or "simply".
- [ ] `ms.date` reflects today's date.

---

## Reference

- [Microsoft Learn contributor guide](https://learn.microsoft.com/en-us/contribute/)
- [Markdown reference for Microsoft Learn](https://learn.microsoft.com/en-us/contribute/markdown-reference)
- [Microsoft Writing Style Guide](https://learn.microsoft.com/en-us/style-guide/welcome/)
- [Article types on Microsoft Learn](https://learn.microsoft.com/en-us/contribute/content-templates)
