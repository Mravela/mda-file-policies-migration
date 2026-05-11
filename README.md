# MDA File Policies → Microsoft Purview: Migration Documentation

This repository contains a **publication-ready migration article** for the deprecation of Microsoft Defender for Cloud Apps (MDA) file policies, migrating to Microsoft Purview DLP and Information Protection.

## File

| File | Description |
|---|---|
| `file-policies-deprecation.md` | The migration article, formatted to Microsoft Learn standard — ready for PR submission to MicrosoftDocs |

## How to submit a PR to MicrosoftDocs

1. Clone the target MicrosoftDocs repository (e.g., `https://github.com/MicrosoftDocs/CloudAppsSecurity`).
2. Copy `file-policies-deprecation.md` into the appropriate folder (e.g., `CloudAppsSecurity/`).
3. Update the YAML front matter: replace `<ms-alias>` and `<github-alias>` with your actual aliases.
4. Commit and push to a new branch.
5. Open a Pull Request against the `main` or `live` branch.

## Content source

- Internal SharePoint: PurviewEngineering-Fieldconnection MDA→Purview migration page
- Internal PPT: MDA to Purview migration guidance (MulticloudMIPDLP team site)
- Retirement date: **December 31, 2026**

## MS Learn doc standard applied

- YAML front matter (title, description, ms.service, ms.topic, ms.author, ms.date, ms.collection)
- Second person, active voice
- Sentence-case headings
- Standard callout syntax (`> [!NOTE]`, `> [!IMPORTANT]`, `> [!TIP]`, `> [!CAUTION]`)
- Bold UI elements, `>` navigation paths
- "Next steps" as final section
