# MF Operations Desk

Internal operations dashboard for the MF advisory journey, from the calling sheet to the hand-off to the MF Advisory dashboard.

- **Source:** [`dashboard/index.html`](dashboard/index.html) is a single self-contained page. Its data lives in the artifact's shared database for now and moves to Supabase once the flow is verified.

## The process (as the team works)

1. **Calling** — call each lead from the imported sheet and offer the free one-on-one review. Interested → ask for the CAS statement.
2. **CAS & interim report** — CAS received ✓ → make the interim (unpaid) report from it ✓. Reminders here chase the CAS (WhatsApp, then a call).
3. **Pitch (unveil) call** — show how the portfolio looks and what can change; WhatsApp reminder before the call. Sold → premium client.
4. **Premium & agreement** — WhatsApp group ✓, agreement emailed ✓, reminders (WhatsApp, then a call) until the signed agreement arrives ✓.
5. **Requirement → Analyst** — requirement call, write the requirement, send requirement + CAS + details to Analyst ✓.
6. **Paid report & call** — Analyst makes the paid report ✓, paid call with the client and Analyst ✓.
7. **Paid dashboard** — CAS + paid report (zip) sent to the paid dashboard ✓. Done.

No files are stored in the dashboard; every document step is a ✓ tick.

## Sheets (Excel-style workspace)

**Sheets** is the main working screen: tabs like the team's workbook (Calling · CAS & interim report · Pitch calls · Premium sold · Requirement → Analyst · Paid report & call · Paid dashboard · Closed · All clients), each with the columns from the matching Excel sheet. Compact grid with row numbers, frozen name column, sticky headers, a filter box under every column and click-to-sort on any column. Click a cell to edit it: dropdowns for status fields (Disposition, Interim report, Call, Agreement, CAS, Paid report, Meeting done, Report sent…), text for comments, quotes, amounts and requirements, date pickers for call dates. Changing a status moves the client to the next sheet automatically (e.g. Disposition → Interested moves to Analyst calls; Call → Sold moves to Premium sold; Agreement → Signed moves to Requirements & CAS; answers + CAS received moves to Paid reports). Export one sheet or the whole workbook (one Excel sheet per tab, same columns).

## What the team sees

Three tabs: **My day**, **Clients**, **Settings**. Every client sits in one of six major steps, each with its own colour: **1. Call the lead → 2. Report & pitch → 3. Agreement → 4. Requirements & CAS → 5. Paid report → 6. Hand-off & done**. Every row says the next step as one plain sentence, for example "WhatsApp Rahul: remind them to sign the agreement emailed on 9 Oct" or "Call Rahul. They haven't replied to the WhatsApp about signing the agreement.", with one or two buttons (Open WhatsApp / Sent, Spoke to them / No answer, Log call). Opening a client shows "What to do next" and the form for that step; owner, documents, details and history are folded under "More". Import, Team overview and All reminders are reached from Settings.

## The journey (detailed stages behind the six steps)

Each client is one record that moves through these steps. There are no roles: every client has an **owner** (from the Sales / Lead column of your sheets), who gets all of that client's calls, reminders and meetings. Reports go to the client's **Reports by** person, or to an open queue that anyone can take.

| # | Stage | Exit action | Due date / reminder (set in Settings) |
|---|---|---|---|
| 1 | New lead | Give it an owner (or "Take it") | Same day |
| 2 | Calling | Interested / Follow up / Not connected (DNP) / Not interested / Wrong number | DNP retry every *N* days; flagged after *N* attempts |
| 3 | Interim (unpaid) report | Attach the report (+ standard performance report) | *N* days |
| 4 | Conversion call | Sold / paid (amount), Follow up later (date, quote, note), or Not converted | Schedule within *N* days |
| 5 | Onboarding & agreement | WhatsApp group, agreement emailed, reminder rounds, signed agreement received | Reminder rounds (below) |
| 6 | Requirement call | Requirements written down | *N* days |
| 7 | Requirements & CAS | Message sent, response recorded, CAS statement attached | Reminder rounds (below) |
| 8 | Paid report | Attach paid report | *N* days |
| 9 | Report meeting | Meeting done | Schedule within *N* days |
| 10 | Report delivery | Paid report sent on WhatsApp | Meeting date + *N* days (T+2 by default) |
| 11 | MF Advisory handoff | Client data copied to the MF Advisory dashboard | Same day |

You can close a client at any step with a reason (the list of reasons is editable). Closed clients can be reopened.

## Undo and moving a client back

- **Undo:** every change (a tick, a status, a close, a bulk action) shows a bar at the bottom with **Undo** for 12 seconds. Undo puts the client back exactly as they were. Bulk actions are undone together.
- **← Back to (previous step)** and **Move to step…** sit at the top of every client. Moving back **clears the ticks after that step** (e.g. moving a premium client back to CAS clears CAS received, the interim report, the pitch call and the agreement ticks). Moving forward keeps everything.
- **Bulk:** in Sheets, select rows → **Move to step…** → Move.
- **Closed clients:** **Reopen at (the step they were closed at)**.
- Every move and undo is written to the client's history.

## Deleting closed clients

Admins see **Delete all closed** in the Closed tab. It first saves an Excel file with every closed client (all columns, reason and full history). Clients are deleted only after that file is saved; if the save is cancelled, nothing is deleted. The delete can't be undone, so keep the file.

## What each person sees ("My day")

Everyone picks their name and sees their own work in Overdue, Due today and Next 7 days, with counts for calls to make, WhatsApp and agreement tasks, reports and overdue items. Below that is **Unassigned**: leads with no owner and reports nobody has picked up, each with a **Take it** button. Settings (rules and templates) can only be changed by the owner or an Editor; anyone can add team members and import sheets.

## Reminders: WhatsApp first, then a call

Each reminder round has two steps:

1. **WhatsApp:** the row has a WhatsApp button that opens the chat with the message already typed, plus Copy text (and Copy email for agreement reminders). Then tap **WhatsApp sent**.
2. **Call:** if the client hasn't replied within *N* days (default 1; 0 = same day), a follow-up call task appears with the number. Log **Spoke to client** or **Not connected** (agreement reminders also have **Agreement received**).

The next round starts after the gap set in Settings. After the maximum number of rounds the client is marked **Escalated** and shows under "Needs attention" on Team & funnel.

| Reminder | Starts | Escalation |
|---|---|---|
| Email the agreement | When the client pays | — |
| Agreement reminder rounds | *N* days after the agreement is emailed, until the signed copy arrives | After *N* rounds |
| First requirement message | When the requirement call is done | — |
| Requirements / CAS rounds | *N* days after the message, until both the reply and the CAS are in | After *N* rounds |
| Client meeting reminder (WhatsApp only) | The day before a scheduled conversion call, requirement call or report meeting | — |

Wording is in Settings → Message templates (placeholders `{firstName}`, `{sentDate}`, `{pending}`, `{meeting}`, `{date}`, `{time}`, `{signature}`). Nothing is sent automatically.

## Importing your existing sheets

**Import sheet** reads any tab of an .xlsx/.xls/.csv workbook and matches its headings automatically (Name, Phone / contact_number, Portfolio size, Sales / Lead / spoc, date, Time, Disposition / Call, Status / Comments, Quote, payment_amount, Date_of_Payment, Agreement, Report / Final report, the client requirements text, Shared with client, Deployed). You pick what the tab contains:

| Tab type | Examples | Where clients start |
|---|---|---|
| New leads to call | call arranged Naman, Hot leads | Calling; "interested" → interim report; "not interested" → closed |
| Call arranged / done | ANALYST - CALL OCTOBER, Analyst call September, pending Sept | Conversion call (with the call date, time and quote); Sold / Paid → onboarding |
| Paid clients | Premium_sold, MF PREMIUM PAID USERS, Client Requirements | Deployed → completed; report sent / shared with client → MF Advisory handoff; agreement sent / pending → onboarding with reminder rounds; agreement yes → requirement call; requirements written → requirements & CAS |

- Portfolio text such as "12 lakhs", "1.10 cr" or "₹ 13,68,424" is converted to rupees.
- Names in the Sales / Lead column become team members. Close spellings are matched automatically (dilsad / Dilshad / disad), and you can change each match before importing.
- Duplicate phone numbers are skipped. You can choose to **move existing clients forward** instead (e.g. import a calling sheet first, then Premium_sold).
- Imported backlog is due from the import day, not from the original dates.
- Tabs with a password column (e.g. "mastercas") can't be imported.

## Other screens

- **Pipeline:** every client with stage counts, search, filters by owner and status, and bulk "Give to…".
- **Team & funnel:** Needs attention list, funnel, closing reasons, workload per person (active clients, open, overdue, calls, interested, paid, WhatsApps, reminder calls, reports) and conversion by imported batch.
- Removing a team member makes their clients unassigned (they show under "Nobody is doing these").
- **Client file (drawer):** the action panel for the current step, reminders for the client, owner and reports-by, documents (upload a PDF or image, or paste a Drive link), editable details, activity log, back / move-to-step controls, and delete (admins).

## Data model (for the Supabase move)

| Collection | What it holds |
|---|---|
| `team/{id}` | `name`, `active` |
| `clients/{id}` | contact fields, `extra{}` (unmatched Excel columns), `batchId`, `stage`, `stageAt`, `reached` (furthest stage index), `status` (active / lost), `lost{reason,note,at,stage}`, `ownerId`, `reportById`, `importedAt`, step data `calls{}` `conversion{}` `onboarding{reminders[{wa,call,outcome}]}` `requirement{}` `data{reminders[{wa,call,outcome}]}` `meetReminders{}` `review{}` `delivery{dueAt,sentAt}` `advisory{}`, `files{unpaid,agreement,cas,paid}`, `anonId`, `activity[]` (last 150 entries) |
| `batches/{id}` | one row per imported sheet |
| `settings/main` | turnaround days, reminder intervals and limits, reasons for closing |

Tasks are not stored. They are derived from each client's stage plus the settings (`tasksFor()` in the page), so changing a rule in Settings updates every due date immediately.

## Known limits (v1)

- "You are" is not a login: anyone can pick any name. Real accounts and access control come with Supabase.
- WhatsApp and email steps are logged by hand; the WhatsApp button opens a chat with the client. Automating them comes later.
- The MF Advisory hand-off is copy-paste (a JSON block). An automatic sync comes with Supabase.
- The artifact database holds up to 25,000 documents, and the page works best with up to a few thousand clients. Archive completed or closed clients before going much beyond that.
