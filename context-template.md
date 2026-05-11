# context.md — Session Context Template

Save this file as `context.md` and load it at the start of every Agency session.
This prevents you from re-explaining the same background every time.

Fill in each section before starting your session.

---

## Feature / article type

What are you documenting?
- [ ] Migration (old feature → new feature)
- [ ] Deprecation (feature being retired)
- [ ] New feature how-to
- [ ] Concept / overview

**One-line description:**
> [e.g. "Migration of MDA File Policies to Microsoft Purview DLP — retirement Dec 31 2026"]

---

## Source material

| Source | URL or location |
|---|---|
| SharePoint page | [paste URL] |
| Internal PPT | [paste URL] |
| Spec / design doc | [paste URL or "N/A"] |
| Prior docs article | [paste URL or "N/A"] |

---

## Scope

**In scope (what this article covers):**
- [e.g. SharePoint Online file policies]
- [e.g. OneDrive for Business file policies]
- [e.g. 3P SaaS apps connected via API connectors]

**Out of scope (what to explicitly exclude):**
- [e.g. Session policies]
- [e.g. On-premises scenarios]

---

## Key dates and facts

| Item | Value |
|---|---|
| Retirement / GA date | [e.g. December 31, 2026] |
| Feature name (old) | [e.g. MDA File Policies] |
| Feature name (new) | [e.g. Microsoft Purview DLP] |
| Coexistence allowed? | [Yes / No — and explain if No] |

---

## YAML front matter values

```yaml
ms.service: [e.g. defender-cloud-apps]
ms.topic: how-to
ms.author: [your Microsoft alias]
author: [your GitHub username]
ms.collection:
  - [e.g. m365-security]
  - [e.g. tier2]
```

---

## Known gaps or limitations

List any known cases where the new feature does NOT fully replace the old one:
- [e.g. No folder hierarchy scoping in Purview]
- [e.g. No user quarantine action]

---

## Next steps links to include

List 4–8 Microsoft Learn articles to link in the Next steps section:
1. [Title] — [URL]
2. [Title] — [URL]
3. [Title] — [URL]
4. [Title] — [URL]

---

## Notes for Agency

Any additional instructions:
- [e.g. "Do not include session policies"]
- [e.g. "Tone should match the existing article at [URL]"]
