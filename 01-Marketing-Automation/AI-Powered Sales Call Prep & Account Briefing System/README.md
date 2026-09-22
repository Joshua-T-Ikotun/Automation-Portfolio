# AI-Powered Sales Call Prep & Account Briefing System

## Business Problem

Sales reps often walk into calls under-prepared, not because they are careless, but because pulling together a client's full history takes real time. Deal stage, contract value, past notes, and the last time contact was made all exist somewhere in a CRM, but assembling it into a usable summary before every single call rarely happens consistently. The result is reps walking into high-value conversations without the context they need to move the deal forward.

## System Solution

On a daily schedule, the system checks a CRM sheet for any calls happening that day. For each one, it pulls the associated contact and deal record, passes it to an AI agent that synthesizes everything into a clean, structured pre-call briefing, and delivers that briefing to the rep 30 minutes before the call is due to start. The rep receives a full briefing covering who they are talking to, the current deal status, key context from past interactions, and specific suggested talking points, timed to arrive exactly when it is useful.

## Tools Used

- n8n (workflow orchestration)
- Google Sheets (CRM data source and contact records)
- Google Gemini AI (briefing generation)
- Slack (internal team channel notification)
- Gmail (direct briefing delivery to the rep)

## How to Use

1. Populate the CRM sheet with contact records including name, company, email, deal stage, deal value, currency, last contact date, notes, and scheduled call date and time.
2. The Schedule Trigger fires daily at 7am and generates today's date.
3. The Google Sheets node filters all rows where Call Scheduled Date matches today.
4. For each matched row, the AI agent generates a structured pre-call briefing based on the CRM record.
5. A Code node parses the AI output, extracts each briefing section, and calculates how many minutes remain until 30 minutes before the call.
6. A Wait node holds the workflow until that notification window arrives.
7. The Slack node posts the briefing to the sales channel and the Gmail node delivers the full AI briefing directly to the rep's inbox.

## Key Features

- Calendar-aware scheduling that filters only today's calls rather than processing the entire CRM
- AI agent that synthesizes scattered CRM data into one structured, human-readable briefing
- Timed delivery logic that calculates and waits until exactly 30 minutes before each call
- Four-section briefing covering who the contact is, deal status, key context, and suggested talking points
- Dual delivery via Slack for team visibility and Gmail for the rep's personal inbox
- Handles multiple calls in a single day, processing each contact row independently

## Business Impact

- Reps walk into every call prepared without spending time manually digging through CRM history
- Consistent prep quality across the team regardless of who the rep is or how organized their process is
- High-value calls get the same quality of preparation as routine ones automatically
- Briefing arrives at exactly the right moment, 30 minutes before the call, not hours earlier when it gets forgotten

## Known Limitations

- Briefing quality depends entirely on how complete and up to date the underlying CRM notes are
- The system reads CRM data but does not write back to it, there is no two-way sync
- Only processes calls scheduled for the current day, does not look ahead to future dates

## Planned Improvements

- Add a Slack shortcut letting reps request an on-demand briefing for any contact outside of scheduled calls
- Pull in recent email thread summaries alongside CRM notes for fuller context
- Add a post-call prompt that updates the Notes field automatically after a call ends
