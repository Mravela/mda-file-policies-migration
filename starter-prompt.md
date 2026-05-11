# Agency Starter Prompt — Generate a Microsoft Learn Article

Copy and paste this into Agency. Replace the bracketed placeholders with your actual content.

---

```
I need to create a publication-ready Microsoft Learn article.

Here are my source materials:
- SharePoint page: [paste your internal SharePoint URL]
- Internal PPT: [paste your SharePoint PPT URL]

Please do the following:

1. Use WorkIQ to read both documents above — extract all key information,
   scenarios, steps, dates, and tables.

2. Connect to the Microsoft Learn MCP server (https://learn.microsoft.com/api/mcp)
   and search for the correct structure of a how-to migration article.

3. Apply the full Microsoft Learn publishing standard to produce the article:
   - YAML front matter: title, description, ms.service, ms.topic, ms.author,
     author, ms.date, ms.collection
   - H1: action-oriented, sentence case, matches YAML title exactly
   - Applies to block immediately after H1
   - [!IMPORTANT] callout if there is a deadline or critical action
   - Standard section order: What's changing → Before you begin →
     Step-by-step tasks → Gaps/limitations → Verify → Next steps
   - Callout syntax: > [!NOTE], > [!IMPORTANT], > [!TIP], > [!CAUTION]
   - Bold all UI elements, use > for navigation paths
   - Numbered steps start with action verbs (Select, Go to, Enter, Review)
   - Each step = one action only
   - Next steps as the final section with 4–8 links

4. Save the output as a .md file ready for PR submission to MicrosoftDocs.

5. Build an HTML preview that visually matches learn.microsoft.com —
   using the real CSS design tokens from the live site.

6. Create a GitHub repo with the .md file and a README with PR instructions,
   so I can hand it directly to the docs team.
```

---

## Tips

- Run this prompt **after** setting up the MS Learn MCP server in your Agency agent
  (Tools → Add a tool → Model Context Protocol → https://learn.microsoft.com/api/mcp)
- Load your `context.md` at the start of the session so you don't repeat context
- If you have multiple scenarios (e.g. SharePoint + 3P SaaS apps), mention them explicitly
- After the .md is generated, ask: "Now check this against the MS Learn publishing checklist"
