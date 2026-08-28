---
name: bison-campaign-creator
description: Create Bison email campaigns from a structured campaign sequences document. Use this skill whenever the user wants to create campaigns in Bison, upload campaign sequences, build email sequences from a document, or set up outbound campaigns for a client. Trigger when the user mentions creating campaigns, campaign sequences, Bison campaigns, email sequences from a doc, or loading campaigns into Bison — even if they don't say "Bison" explicitly but reference a campaign document or sequences file.
---

# Bison Campaign Creator

You create email campaigns in Bison by reading a structured campaign sequences document and creating each campaign with its full email sequence. This is a workflow that happens regularly for different clients and verticals, so precision and consistency matter.

## How it works

The user will point you to a campaign sequences document (usually a markdown or text file). The document contains multiple campaigns, each with email steps that include spintax, subject lines, and send timing. Your job is to parse the document, confirm the details with the user, and create all campaigns in Bison.

## Step-by-step workflow

### 1. Read the document

Read the campaign sequences file the user provides. Parse out every campaign and its email steps.

For each campaign, extract:
- **Campaign name** (e.g., "CAMPAIGN 1: GYM GROWTH CAPITAL")
- **Subject line** for each email step
- **Email body** for each email step, preserving all spintax exactly as written (curly braces, pipes, variable placeholders like `{FIRST_NAME}`, `{{company}}`, `{{personalized_idea}}`)
- **Day number** for each email step (e.g., Day 0, Day 3)
- **Whether it's a thread reply** (indicated by "thread reply" in the step header)

### 2. Ask the user to confirm the Bison client

Before creating anything, ask: **"Which Bison client should I create these campaigns under?"**

If the document contains a "Prepared for" line, suggest that name but still ask for confirmation. Use `get_bison_clients` to verify the client exists in Bison.

### 3. Show a summary for validation

Present a summary table to the user before creating campaigns. This lets them catch any issues before anything is created. The summary should show:

| # | Campaign Name | # of Emails | Days |
|---|--------------|-------------|------|
| 1 | CAMPAIGN 1: GYM GROWTH CAPITAL 03/25/2026 | 2 | 0, 3 |
| 2 | CAMPAIGN 2: MED SPA EQUIPMENT & EXPANSION 03/25/2026 | 2 | 0, 3 |

Include:
- The total number of campaigns found
- Each campaign's name (with today's date appended in MM/DD/YYYY format)
- Number of email steps per campaign
- The day schedule for each step

Ask: **"Does this look correct? Should I proceed with creating all X campaigns?"**

### 4. Create the campaigns

Once confirmed, create all campaigns using `create_bison_sequence`. For each campaign:

- **campaign_name**: Use the exact campaign name from the document + today's date in MM/DD/YYYY format (e.g., `CAMPAIGN 1: GYM GROWTH CAPITAL 03/25/2026`)
- **sequence_title**: Same as campaign_name
- **client_name**: The confirmed client name
- **steps**: Array of email step objects, each with:
  - `day`: The day number from the document
  - `subject`: The subject line, exactly as written. For thread replies (Email 2+), prepend `Re: ` to the original subject
  - `body`: The full email body with all spintax preserved exactly — every `{option1|option2}`, `{FIRST_NAME}`, `{{company}}`, `{{personalized_idea}}` must be kept verbatim

Create campaigns in parallel when possible to save time.

### 5. Report results

After creation, show a results table:

| # | Campaign Name | Campaign ID | Sequence ID | Status |
|---|--------------|-------------|-------------|--------|
| 1 | CAMPAIGN 1: GYM GROWTH CAPITAL 03/25/2026 | 409 | 336 | Created |

If any fail, note the failure and retry once. Report final status for all campaigns.

## Critical rules for parsing

- **Spintax is sacred.** Never modify, reformat, or "clean up" spintax. The `{option1|option2|option3}` format and `{{variable}}` placeholders must be preserved character-for-character.
- **Signatures are part of the body.** The sign-off block (name, company, address, license, remove line) is part of Email 1's body, not metadata.
- **Thread replies don't repeat the signature.** Email 2+ typically ends with just the sender's first name.
- **Escape characters are document artifacts.** Backslashes before underscores (`\_`) or hash signs (`\#`) in markdown are rendering escapes — strip them in the actual email body (use `_` and `#` respectively).
- **Empty spintax options are intentional.** `{Hey|Hi|}` means the third option is blank (no greeting). Preserve this.

## Document format

Campaign documents follow this structure:

```
**CAMPAIGN N: CAMPAIGN NAME**

Subject: {subject line}

Email 1 (Day 0):

{email body with spintax}

Email 2 (Day 3, thread reply):

{email body with spintax}
```

The day number and whether it's a thread reply are specified in the email step header. The number of emails per campaign may vary.
