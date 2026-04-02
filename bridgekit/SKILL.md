---
name: bridgekit
description: BridgeKit MCP integration for Google Docs, Google Sheets, Gmail, Slack, Bison (EmailBison), and Instantly.ai. Use when interacting with Google Workspace, email platforms, Slack messaging, or cold email campaign management via MCP tools. Triggers on mentions of BridgeKit, Google Docs, Google Sheets, Gmail, Slack messages, or cross-platform workflows.
---

# BridgeKit MCP Integration

## When to use this skill
- Reading, creating, or editing Google Docs
- Reading, writing, analyzing, or formatting Google Sheets
- Searching, sending, or managing Gmail
- Sending Slack messages, reading channels, or searching Slack
- Managing Bison (EmailBison) campaigns, leads, replies, and mailbox health
- Managing Instantly.ai campaigns, leads, mailbox health, and stats
- Any cross-platform workflow combining the above

## How to access tools
All BridgeKit tools are MCP tools prefixed with `mcp__claude_ai_BiridgeKit__`. Use `ToolSearch` with query `"+BiridgeKit"` to fetch tool schemas before invoking.

## Tool Inventory

### Google Docs (19 tools)

| Tool | Purpose |
|------|---------|
| `create_google_doc` | Create a new Google Doc |
| `read_google_doc` | Read document content |
| `append_to_google_doc` | Append text to end of doc |
| `insert_into_google_doc` | Insert text at specific index |
| `replace_text_in_google_doc` | Find and replace text |
| `add_heading_to_google_doc` | Add formatted heading (H1-H6) |
| `add_comment_to_google_doc` | Add comment, optionally anchored to text |
| `reply_to_google_doc_comment` | Reply to existing comment |
| `resolve_google_doc_comment` | Resolve a comment thread |
| `list_google_doc_comments` | List all comments on a doc |
| `format_google_doc_professional` | Apply professional formatting |
| `format_google_doc_section` | Format a specific section |
| `insert_image_in_google_doc` | Insert image by URL |
| `insert_page_break_in_google_doc` | Insert page break |
| `insert_section_break_in_google_doc` | Insert section break |
| `create_table_in_google_doc` | Create a table |
| `create_named_range_in_google_doc` | Create named range |
| `delete_named_range_from_google_doc` | Delete named range |
| `list_named_ranges_in_google_doc` | List all named ranges |

### Google Sheets (31 tools)

| Tool | Purpose |
|------|---------|
| `create_spreadsheet` | Create new spreadsheet |
| `read_spreadsheet` | Read cell range data |
| `update_spreadsheet` | Write data to cells |
| `append_to_spreadsheet` | Append rows to sheet |
| `get_spreadsheet_info` | Get spreadsheet metadata |
| `analyze_spreadsheet` | Analyze data patterns |
| `list_sheets_in_spreadsheet` | List all sheets/tabs |
| `add_sheet_to_spreadsheet` | Add new sheet/tab |
| `delete_sheet_from_spreadsheet` | Delete a sheet/tab |
| `rename_spreadsheet_sheet` | Rename a sheet/tab |
| `format_spreadsheet_cells` | Format cells (colors, fonts, borders) |
| `merge_spreadsheet_cells` | Merge cell range |
| `unmerge_spreadsheet_cells` | Unmerge cells |
| `sort_spreadsheet_range` | Sort data range |
| `clear_spreadsheet_range` | Clear cell contents |
| `find_replace_in_spreadsheet` | Find and replace in sheet |
| `duplicates_in_spreadsheet` | Find duplicate rows |
| `filter_and_export_spreadsheet` | Filter and export data |
| `insert_spreadsheet_rows` | Insert rows |
| `insert_spreadsheet_columns` | Insert columns |
| `delete_spreadsheet_rows` | Delete rows |
| `delete_spreadsheet_columns` | Delete columns |
| `move_spreadsheet_rows` | Move rows |
| `freeze_spreadsheet_rows_columns` | Freeze rows/columns |
| `auto_resize_spreadsheet_columns` | Auto-resize columns |
| `protect_spreadsheet_range` | Protect a range |
| `create_spreadsheet_chart` | Create chart |
| `add_conditional_format_to_spreadsheet` | Add conditional formatting |
| `add_data_validation_to_spreadsheet` | Add data validation/dropdowns |
| `add_named_range_to_spreadsheet` | Create named range |
| `delete_named_range_from_spreadsheet` | Delete named range |

### Gmail (10 tools)

| Tool | Purpose |
|------|---------|
| `search_emails` | Search emails (Gmail query syntax) |
| `get_email_thread` | Get full email thread |
| `get_inbox_summary` | Inbox summary with counts |
| `send_email` | Send new email |
| `reply_to_email` | Reply to email |
| `reply_all_to_email` | Reply-all to email |
| `create_email_draft` | Create draft |
| `get_unreplied_emails` | Find unreplied emails |
| `get_unreplied_by_sender` | Unreplied emails grouped by sender |
| `list_connected_google_accounts` | List connected accounts |

### Slack (8 tools)

| Tool | Purpose |
|------|---------|
| `send_slack_message` | Send message to channel |
| `reply_to_slack_thread` | Reply in thread |
| `get_slack_channel_history` | Read channel history |
| `get_slack_thread_replies` | Get thread replies |
| `list_slack_channels` | List all channels |
| `search_slack_messages` | Search messages |
| `get_slack_user_info` | Get user info |
| `create_slack_group_dm` | Create group DM |

### Bison / EmailBison (16 tools)

| Tool | Purpose |
|------|---------|
| `get_bison_clients` | List all Bison clients |
| `get_active_bison_clients` | List active clients only |
| `get_bison_stats` | Campaign stats for a client |
| `list_bison_campaigns` | List campaigns |
| `get_bison_campaign_details` | Campaign detail with stats |
| `get_bison_campaign_replies` | Get campaign replies |
| `get_bison_campaign_chart` | Campaign chart data |
| `get_bison_leads` | List leads |
| `get_bison_lead` | Get single lead |
| `search_bison_leads` | Search leads |
| `get_bison_lead_sent_emails` | Emails sent to a lead |
| `get_bison_sender_email_replies` | Replies by sender email |
| `get_bison_mailbox_health` | Mailbox health report |
| `bulk_create_bison_leads` | Bulk create leads |
| `find_missed_opportunities_bison` | Find missed reply opportunities |
| `create_bison_sequence` | Create email sequence |

### Instantly.ai (14 tools)

| Tool | Purpose |
|------|---------|
| `get_instantly_clients` | List all Instantly clients |
| `get_active_instantly_clients` | List active clients only |
| `get_instantly_stats` | Campaign stats for a client |
| `list_instantly_campaigns` | List campaigns |
| `get_instantly_campaign_details` | Campaign detail |
| `get_instantly_leads` | List leads |
| `get_instantly_leads_with_status` | Leads filtered by status |
| `get_instantly_mailbox_health` | Mailbox health report |
| `get_instantly_workspace` | Workspace info |
| `add_leads_to_instantly_campaign` | Add leads to campaign |
| `update_instantly_lead_status` | Update lead status |
| `create_instantly_campaign` | Create new campaign |
| `mark_lead_as_interested` | Mark lead as interested |
| `find_missed_opportunities` | Find missed reply opportunities |

### Utility & Auth Tools

| Tool | Purpose |
|------|---------|
| `search_tools` | Search available BridgeKit tools by keyword |
| `set_account_alias` | Set alias for a connected account |
| `check_account_health` | Check connected account health |
| `start_async_job` | Start long-running async job |
| `check_job_status` | Check async job status |
| `mcp__claude_ai_Gmail__authenticate` | Authenticate Gmail account |
| `mcp__claude_ai_Google_Calendar__authenticate` | Authenticate Google Calendar |

## Common Patterns

### Google Doc/Sheet IDs
Extract from URLs:
- Docs: `https://docs.google.com/document/d/{DOCUMENT_ID}/edit`
- Sheets: `https://docs.google.com/spreadsheets/d/{SPREADSHEET_ID}/edit`

### Cross-platform workflows
1. **Campaign report to Sheet**: Pull Bison/Instantly stats -> write to Google Sheet -> format with charts
2. **Reply monitoring to Slack**: Check for missed opportunities -> post summary to Slack channel
3. **Lead import pipeline**: Read leads from Sheet -> bulk create in Bison -> add to Instantly campaign
4. **Inbox triage to Doc**: Summarize unreplied emails -> create Google Doc report

### Spreadsheet indexing
- Rows and columns use **0-based indexing**

### Gmail search syntax
Standard Gmail query syntax: `from:user@example.com after:2026/01/01 subject:invoice`

## Important Notes
- All tools are shared across agents in the OpenAgents workspace via MCP
- Tool names use the prefix `mcp__claude_ai_BiridgeKit__` (note the "BiridgeKit" spelling)
- Slack messages support markdown formatting
- Use `list_connected_google_accounts` to verify which accounts are linked before operations
