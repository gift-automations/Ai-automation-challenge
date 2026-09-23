# Day 1 — Email Urgency Classifier

**Client brief:**
> "Hey, I get like 50 emails a day and I'm drowning. Can you set something up that reads new emails and labels them by urgency (urgent / normal / spam-ish) automatically?"

## What it does
Watches a Gmail inbox for new messages, sends the subject + snippet to an AI model for classification, then automatically applies a Gmail label (`Urgent`, `Normal`, or `Spam-ish`) based on the result — no manual sorting needed.

## How it works
1. **Gmail Trigger** — polls the inbox for new messages.
2. **OpenAI (GPT-4o-mini)** — classifies the email as `Urgent`, `Normal`, or `Spam-ish` based on subject and body snippet.
3. **Switch node** — routes the result to the matching branch.
4. **Gmail (Add Label)** — applies the correct label to the original message.

## Tools used
- [n8n](https://n8n.io) (workflow automation)
- Gmail API (OAuth2)
- OpenAI API (`gpt-4o-mini`)

## Impact
- Removes manual email triage entirely for incoming messages.
- Runs continuously in the background — every new email gets sorted within a minute of arrival.
- Easily extendable: more categories, auto-drafted replies, or Slack alerts for "Urgent" emails could be added on top.

## Notes
- The workflow JSON in this folder has credentials stripped to references only — no API keys or tokens are included. You'll need to connect your own Gmail and OpenAI credentials in n8n after importing.
- Gmail labels (`Urgent`, `Normal`, `Spam-ish`) must exist in the target Gmail account before running, since the workflow references their label IDs.

## Files
- `day-01-workflow.json` — exported n8n workflow, importable directly into any n8n instance.
