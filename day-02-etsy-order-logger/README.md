# Day 2 — Etsy Order Logger

**Client brief:**
> "I run a small Etsy shop. Every time I get an order I have to manually copy it into a spreadsheet. Can you automate that?"

## What it does
Watches for new "order" email notifications, extracts the buyer, item, total, and order link from the message, then automatically appends a new row to a Google Sheet — no manual copy-paste needed.

## How it works
1. **Gmail Trigger** — polls the inbox, filtered to only match emails with "sale" in the subject line.
2. **Code node (JavaScript)** — parses the raw email snippet with regex to pull out clean fields: `date`, `buyer`, `item`, `total`, `link`.
3. **Google Sheets (Append Row)** — logs each parsed order as a new row in the tracking sheet.

## Tools used
- [n8n](https://n8n.io) (workflow automation)
- Gmail API (OAuth2)
- Google Sheets API (OAuth2)
- JavaScript (Code node, regex parsing)

## Impact
- Eliminates manual order entry — every sale is logged automatically within a minute of the notification arriving.
- Removes copy-paste errors from manual transcription.
- Sheet can be extended into a live sales dashboard, inventory tracker, or auto-generated reports.

## Production note (real client version)
This build uses Gmail as the trigger since Etsy notification emails are simple to parse and require no special access. For an actual paying client with an active Etsy shop, the production version would instead:
- Register an app via **Etsy's official API** (etsy.com/developers)
- Use **OAuth 2.0** with the shop owner's explicit consent
- Poll the **Receipts endpoint** on a schedule (Etsy has no native order webhook) instead of relying on email parsing, which is more reliable and doesn't break if Etsy changes their email template.

## Notes
- The workflow JSON has credentials stripped to references only — no API keys or tokens are included. You'll need to connect your own Gmail and Google Sheets credentials in n8n after importing.
- The JSON references a specific Google Sheet ID — swap this for your own sheet's ID after importing.

## Files
- `day-02-workflow.json` — exported n8n workflow, importable directly into any n8n instance.
