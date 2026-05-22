---
title: Migrate Microsoft Defender for Cloud Apps file policies to Microsoft Purview
description: Learn how to migrate file policies from Microsoft Defender for Cloud Apps to Microsoft Purview Data Loss Prevention and Information Protection auto-labeling policies before the December 31, 2026 retirement date.
ms.service: defender-cloud-apps
ms.topic: how-to
ms.author: <ms-alias>
author: <github-alias>
ms.date: 05/11/2025
ms.collection:
  - m365-security
  - tier2
---

# Migrate Microsoft Defender for Cloud Apps file policies to Microsoft Purview

**Applies to:**
- Microsoft Defender for Cloud Apps
- Microsoft Purview Data Loss Prevention
- Microsoft Purview Information Protection

Data security capabilities in Microsoft Defender for Cloud Apps (MDA), including file policies, are being retired on **December 31, 2026**. After that date, file policies configured in Defender for Cloud Apps will no longer be supported or enforced. This article explains what's changing, what's affected, and how to migrate your file policies to Microsoft Purview before the retirement date.

> [!IMPORTANT]
> File policies in Microsoft Defender for Cloud Apps will stop being enforced after **December 31, 2026**. No new investments will be made in these capabilities. Migrate your policies to Microsoft Purview to avoid gaps in data protection.

## What's changing

Microsoft is consolidating data loss prevention (DLP) and information protection capabilities into Microsoft Purview. Future investments in data security — including DLP policies, auto-labeling, and compliance reporting — will be made in Purview. Defender for Cloud Apps will focus on SaaS protection through discovery, posture management, and threat detection as part of Microsoft Defender XDR.

The following capabilities are being retired in Defender for Cloud Apps:

| What's going away in MDA | What to use in Microsoft Purview |
|---|---|
| File policies for files stored in SharePoint Online and OneDrive for Business | Purview DLP policies and Information Protection auto-labeling policies targeting SharePoint and OneDrive for Business |
| File policies for files stored in non-Microsoft SaaS applications (connected sources) | Purview DLP policies and Information Protection auto-labeling policies targeting connected applications |

> [!NOTE]
> Third-party policies in MDA and Purview cannot coexist. Running equivalent policies in both products simultaneously creates enforcement conflicts. Disable MDA policies only after your Purview policies are validated and turned on.

## How to migrate: three steps

Migration follows a simple three-step process:

1. **Review** — Identify your current file policies in Defender for Cloud Apps.
1. **Recreate** — Build equivalent policies in Microsoft Purview.
1. **Turn off** — Disable the original policies in Defender for Cloud Apps.

## Before you begin

Before you recreate your policies in Microsoft Purview, confirm the following:

- You have the required Microsoft Purview roles to create and manage DLP and auto-labeling policies. For the complete set of required roles, see [Permissions for DLP policies](https://learn.microsoft.com/en-us/purview/dlp-create-deploy-policy#permissions) and [Permissions for sensitivity labels](https://learn.microsoft.com/en-us/purview/get-started-with-sensitivity-labels#permissions-required-to-create-and-manage-sensitivity-labels).
- Sensitivity labels are created and published in Microsoft Purview Information Protection (required for label-based conditions and auto-labeling policies).
- Auditing is enabled in your Microsoft 365 tenant (required for Activity Explorer and DLP reporting).
- You've exported or documented your existing MDA file policies, including their conditions, actions, and scoped apps.

## Migrate file policies for SharePoint Online and OneDrive for Business

### Create a DLP policy in Microsoft Purview

Use the following steps to recreate MDA file policies that detect sensitive content or enforce actions such as blocking external sharing, restricting access, or notifying users.

1. Go to [Microsoft Purview](https://purview.microsoft.com) > **Solutions** > **Data loss prevention** > **Policies** > **Create policy**.
1. Choose a compliance template (such as GDPR or HIPAA) or select **Custom policy**.
1. Enter a name and description for the policy.
1. Optionally, assign admin units to scope policy management access.
1. Select the workloads: **SharePoint Online**, **OneDrive for Business**, **Enterprise applications & devices**, or a combination. Exclude other workloads if they're not needed.
1. Define the policy scope (all users, specific sites, or specific groups).
1. Create a rule and configure conditions:
   - Choose **Sensitive information types**, **Sensitivity labels**, or both as content conditions.
   - Add **Content is shared externally** if the policy should trigger on external sharing.
1. Configure actions. For SharePoint and OneDrive, available actions include **Restrict access or encrypt the content in Microsoft 365 locations** (block everyone, or block only people outside your organization), **Allow with override**, and **Audit only**. For the complete list of supported actions, see [Supported actions – SharePoint](https://learn.microsoft.com/en-us/purview/dlp-policy-reference#supported-actions-sharepoint) and [Create a DLP policy for SharePoint and OneDrive](https://learn.microsoft.com/en-us/purview/dlp-create-policy-spo-odb-external#steps-to-create-policy).
1. Configure **User notifications** (policy tips) and **Incident reports** with alert recipients and severity.
1. Select **Simulation mode** to test the policy before enforcing it.
1. Review matched results in **Activity explorer**, then set the policy to **On** when ready.

> [!TIP]
> Run the policy in simulation mode for at least one to two weeks before switching to enforce mode to minimize false positives. To access and interpret simulation results, see [Simulation results](https://learn.microsoft.com/en-us/purview/dlp-simulation-mode-learn#simulation-results).

### Replace or apply sensitivity labels with an auto-labeling policy

Use auto-labeling policies to recreate MDA file policies that applied or replaced sensitivity labels on files at rest.

> [!NOTE]
> Sensitivity labels must be created and published before you create an auto-labeling policy.

**To apply or upgrade labels:**

1. Go to [Microsoft Purview](https://purview.microsoft.com) > **Solutions** > **Information protection** > **Policies** > **Auto-labeling policies** > **Create policy**.
1. Select **Automatically apply labels only**, then choose a template or create a custom policy.
1. Select the sensitivity label to apply.
1. Optionally, assign admin units.
1. Select locations: **SharePoint Online**, **OneDrive for Business**, or both.
1. Configure rules and conditions (for example, content contains a specific sensitive information type). Note that **existing label** is not a supported condition in Purview auto-labeling policies.
1. Under **Additional label settings**, configure whether the policy should override existing labels:
   - Select **Override** to replace lower-priority labels regardless of whether the previous label was applied manually or automatically.
   - Override applies to Exchange, SharePoint, and OneDrive only.
   - If the label includes encryption settings, enter an admin account as the Rights Management owner.
1. Run the policy in **Simulation mode**, review the items matched, then turn on the policy.

> [!NOTE]
> For detailed guidance on configuring auto-labeling policies for SharePoint and OneDrive, see [How to configure auto-labeling policies for SharePoint, OneDrive, and Exchange](https://learn.microsoft.com/en-us/purview/apply-sensitivity-label-automatically?tabs=remove-label#how-to-configure-auto-labeling-policies-for-sharepoint-onedrive-and-exchange).

**To auto-remove labels:**

1. Go to [Microsoft Purview](https://purview.microsoft.com) > **Solutions** > **Information protection** > **Policies** > **Auto-labeling policies** > **Create policy**.
1. Select **Automatically remove labels only**.
1. Enter a name for the policy.
1. Select the label to remove (this is auto-populated and can't be removed from the rule).
1. Select locations: **SharePoint Online** and **OneDrive for Business** only.
1. Add any additional conditions to the rule.
1. Run the policy in **Simulation mode**, review results, then turn on the policy.

## Migrate file policies for non-Microsoft SaaS applications

If your MDA file policies apply to third-party cloud apps (such as Box, Salesforce, or Google Workspace) connected via API connectors, you need to onboard those connectors in the Microsoft Defender portal and then create policies in Microsoft Purview.

> [!NOTE]
> App connector setup, management, and error monitoring remain in the **Microsoft Defender portal**. Only policy creation and evaluation results move to Microsoft Purview. If a connector fails or disconnects, alerts and error notifications will continue to surface in Microsoft Defender for Cloud Apps as before.

### Step 1: Onboard a connector in the Microsoft Defender portal

> [!NOTE]
> This step is required only for apps that are not already connected to Defender for Cloud Apps.

1. Go to [Microsoft Defender portal](https://security.microsoft.com) > **Settings** > **Connected apps** > **App connectors**.
1. Select **Connect an app** and choose the app from the list.
1. Enter the required instance name and credentials to complete the connection.

### Step 2: Create a DLP policy for connected sources

1. Go to [Microsoft Purview](https://purview.microsoft.com) > **Solutions** > **Data loss prevention** > **Policies** > **Create policy**.
1. When prompted, select **Data stored in connected sources**.
1. Enter a name and description for the policy.
1. Keep the admin units selection as **Full directory**.
1. Select the workload location and the specific connected app instance to scope the policy.
1. Create a rule with a name, conditions (such as sensitive information types), and actions.
1. Review and save the policy.

### Step 3: Create an auto-labeling policy for connected sources

1. Go to [Microsoft Purview](https://purview.microsoft.com) > **Solutions** > **Information protection** > **Policies** > **Auto-labeling policies** > **Create policy**.
1. Select **Custom** policy template.
1. Enter a name and description.
1. Select the label to apply.
1. Keep admin units as **Full directory**.
1. Select the connected app workload and instance.
1. Define rules and conditions.
1. Set the policy mode to **On** or leave it turned off until ready.

## What isn't available in Microsoft Purview

Some MDA file policy conditions and actions don't have equivalents in Microsoft Purview. Review the following gaps before migrating.

**Conditions with no Purview equivalent:**

| MDA condition | Status in Purview |
|---|---|
| Apply to folder hierarchy (include or exclude specific folders) | Not available |
| Parent folder (single-level folder scoping) | Not available |
| Quarantined = true or false | Not available |
| File in recycle bin or trash | Not available |
| File ID | Not available |
| Matched policy | Not available |

**Actions with no direct Purview equivalent:**

| MDA action | Purview recommendation |
|---|---|
| Automated file restore action after quarantine | Security admins can enable file owners to manually restore files from admin quarantine. Full parity not yet available. |
| User quarantine (file placed in user's personal quarantine folder) | Not available |
| Remove a collaborator | Not available |
| Expire shared link | Not available |
| Reduce public access | Partial equivalent available; full parity not yet available |

> [!NOTE]
> The gaps listed above cover **first-party (1P) workloads** (SharePoint Online and OneDrive for Business) only. Equivalent gap documentation for third-party connected apps is not yet available.

> [!NOTE]
> For scenarios that require these conditions or actions, work with your Microsoft account team to review alternative approaches or submit feedback via the Microsoft Purview feedback channel.

## Verify your migration

After you've created and validated your Purview policies, complete the following steps before disabling your MDA policies:

1. Confirm that Purview DLP alerts are being generated and delivered to the correct recipients.
1. Verify that policy tips are appearing for end users as expected.
1. Check that any Power Automate flows or SIEM integrations are receiving events from Purview DLP (event schemas differ from MDA alert schemas — update your flows accordingly).
1. Review the **Activity explorer** in Purview to confirm matches align with your expectations.
1. Once confirmed, go to Defender for Cloud Apps > **Policies** > **Policy management** and disable each migrated file policy.

> [!CAUTION]
> Don't delete MDA policies immediately. Retain them in a disabled state until you've confirmed your Purview policies are fully enforced and any audit or compliance records from the MDA policies are no longer needed.

## Next steps

- [Create and deploy a DLP policy in Microsoft Purview](https://learn.microsoft.com/en-us/microsoft-365/compliance/dlp-create-deploy-policy)
- [Learn about auto-labeling policies for sensitivity labels](https://learn.microsoft.com/en-us/microsoft-365/compliance/apply-sensitivity-label-automatically)
- [Learn about Microsoft Purview Data Loss Prevention](https://learn.microsoft.com/en-us/microsoft-365/compliance/dlp-learn-about-dlp)
- [Get started with Activity Explorer](https://learn.microsoft.com/en-us/microsoft-365/compliance/data-classification-activity-explorer)
- [Connect apps to Defender for Cloud Apps](https://learn.microsoft.com/en-us/defender-cloud-apps/enable-instant-visibility-protection-and-governance-actions-for-your-apps)
- [Plan for data loss prevention](https://learn.microsoft.com/en-us/microsoft-365/compliance/dlp-overview-plan-for-dlp)
