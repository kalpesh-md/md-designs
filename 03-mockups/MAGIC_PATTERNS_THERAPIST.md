# Magic Patterns — therapist portal

`kalpesh-md/md-designs` is already tagged. Open a **new** chat. Keep that repo tag. Paste the prompt below once. The pages are already in this repo. Magic Patterns should restyle them. It should not invent new files.

## Prompt — all therapist pages (paste this)

The repo kalpesh-md/md-designs is already tagged. Restyle the therapist pages that are already in 03-mockups. Do not invent new pages. Do not edit any client-*.html or admin-*.html file.

These files are the structure. Keep every block that is already on the page. You may reshape layout inside a card, hierarchy, spacing, chips, and buttons so each page is easier to use.

Visual system: navy #1E3A5F, mid #2D5A8B, sky #0EA5E9, live green #3B7A5C, from 02-tokens/tokens.css. Inter. White rounded cards, hairline borders, soft shadow. Status is a pill with a dot.

Files, in this order:
1. 03-mockups/therapist-a-professional.html — dashboard. Then apply that same component look to therapist-b-engagement.html and therapist-c-task-oriented.html. Keep A as two columns, B as the live-session hero, C as the day timeline.
2. therapist-a-availability.html — stats, calendar, add slot, bulk editor, available slots
3. therapist-a-sessions.html — stats, filters, session table
4. therapist-a-session-detail.html — details, notes, MSE, report, join, intake, cancel, client rail
5. therapist-a-clients.html — search and client list
6. therapist-a-client-detail.html — identity, session history, assessments
7. therapist-a-messaging.html — conversation list and chat
8. therapist-a-assessments.html — search, status, response table
9. therapist-a-assessment-response.html — client, scores, answers
10. therapist-a-activities.html — Big Five card only
11. therapist-a-big-five.html and therapist-a-big-five-results.html — question step and five trait bars
12. therapist-a-profile.html — identity, stats, basic / professional / reviews
13. therapist-a-profile-edit.html — basic, professional, banking, password

Start with Dashboard Design A, then the other Design A pages, then Dashboard B and C.
Do not add charts, new nav items, or new booking types.

---

`kalpesh-md/md-designs` is already tagged. The prompts below are the same job split one page at a time, if the single prompt above tries to restyle the client files.

Do not edit `client-*.html` or `admin-*.html`. Tokens stay in `02-tokens/tokens.css`: navy `#1E3A5F`, `#2D5A8B`, `#0EA5E9`, live green `#3B7A5C`.

The Design A pages are already in `03-mockups`. Use the single prompt above. The numbered prompts below are only if you want to restyle one page per chat.

---

## Prompt 1 — Dashboard (paste this first)

I am attaching screenshots of the LIVE therapist dashboard. That is the current product.

The HTML mockups are the structure to restyle. Do not invent a new dashboard. Keep this page:

DASHBOARD
Files:
03-mockups/therapist-a-professional.html
03-mockups/therapist-b-engagement.html
03-mockups/therapist-c-task-oriented.html
Intent: “what does my practice need from me right now?” This page is the practice overview — booking counts, the next sessions, and whether there are open slots. Not a calendar editor, not a client directory, not a chart. Must keep:
Greeting (“Welcome back, {name}” + “Here's your practice overview”)
Four stat cards — Total Bookings, Completed, Upcoming, Cancelled
Upcoming Sessions — avatar, client name, email, date and time. A session in the join window is a LIVE row (green, live dot, Open). Other rows show Video or Phone plus a status pill (confirmed, scheduled)
Availability card — slot count, Manage Availability, Next 7 days, Avg per day

Design A is a clean two-column layout (sessions wide, availability narrow). Design B makes the live session the hero. Design C is a compact day timeline with stats and availability in a side rail. Keep those three layouts. Restyle the components inside them.

What to do:

The screenshots show how the live product looks. The HTML mockups show the structure. Take these same components and redesign them so they look more attractive and easier to use (UI/UX). You may reshape layout inside a card, hierarchy, spacing, chips, and buttons.

Do not:

Add charts, quick actions, pending-items, or a second sidebar
Move the weekly calendar, client list, or messages onto this page
Invent new pages or new features
Touch any client-*.html or admin-*.html file
Change brand navy (#1E3A5F, #2D5A8B, #0EA5E9) or live green (#3B7A5C) from 02-tokens/tokens.css

Start with Dashboard Design A, then apply the same component look to B and C.

---

## Prompt 2 — Availability (after Dashboard looks right)

I am attaching screenshots of the LIVE therapist Availability page. That is the current product.

Create one new page. Copy the sidebar, header, and tokens from 03-mockups/therapist-a-professional.html. Set Availability active in the nav.

AVAILABILITY
File to create:
03-mockups/therapist-a-availability.html
Intent: “when can clients book me?” This page is the slot editor. Must keep:
Header — “Availability” + “Open slots clients can book this week”
Four stat cards — Total Slots, Booked, Available, Session Type (Video)
Three tabs — Calendar View, Bulk Editor, Available Slots
Calendar View — week pager, days × hours, click an empty cell to add a video slot. Booked cells cannot be deleted
Add-slot dialog — date, time, Video Session, Add Slot
Bulk Editor — start date, end date, weekdays, hours, Add or Remove, apply
Available Slots — table of open slots, select-all, bulk delete, pages of 50. Empty state points back to Calendar View or Bulk Editor

What to do:

Redesign these same tools so a week of slots is easier to scan and edit. You may reshape the grid, the selected state, and the dialog. Selected slot = navy border + soft navy fill. Booked looks different from open.

Do not:

Replace this with a generic month calendar
Drop a tab
Invent new session types
Change brand navy (#1E3A5F, #2D5A8B, #0EA5E9) or live green (#3B7A5C)

---

## Prompt 3 — Sessions list

I am attaching screenshots of the LIVE therapist Sessions page. That is the current product.

Create 03-mockups/therapist-a-sessions.html. Same shell as Design A. Set Sessions active.

SESSIONS
Intent: “what is on my schedule, and what already happened?” Must keep:
Header — “My Sessions” + short description, Refresh, Show / Hide filters
Four stat cards — Upcoming, Completion Rate, Missed, Completed
Filter panel — search client name or email, status (All, Upcoming, Completed, No Show, Cancelled), Clear Filters
Table — Client (name + email), Date & Time, Status pill, Actions. Row opens the session. Actions: view, and mark no-show when allowed
Empty, loading, and error states
Pagination

Video vs phone stays visible on the row. Status is a pill with a dot.

Do not invent a calendar view here. That lives on Availability.

---

## Prompt 4 — Session detail

I am attaching screenshots of a LIVE therapist session. That is the current product.

Create 03-mockups/therapist-a-session-detail.html. Same shell as Design A.

SESSION DETAIL
Intent: “I am about to see this client, or I am in the session.” Must keep:
Back to sessions
Header — client name, date, time, video or phone, status pill, countdown, session id
Tabs — Details, Notes, MSE Form, Report
Details — cancellation notice when cancelled, pre-session notes, follow-up notes, Join Session when the window is open, short advisory
Notes — textarea + save
MSE Form — the mental status exam, same fields
Report — session report
Right rail — Client Intake (collapsible), Session Actions (cancel, with the note that the client gets a full credit refund), Client Info, Client's Messages, Clinical Assessments

Join is the primary action when the session is live. Cancel stays secondary. Do not merge notes into the message thread.

---

## Prompt 5 — Clients

I am attaching screenshots of the LIVE Clients page.

Create 03-mockups/therapist-a-clients.html. Same shell. Set Clients active.

CLIENTS
Intent: “who have I seen?” Must keep:
Header — “My Clients” + “People you have seen or will see”, Refresh
Search by name or email
Client list — name, email, and the existing columns. Row opens the client
Empty state when there are no clients, and when search has no matches

Do not add a booking widget on this page.

---

## Prompt 6 — Client detail

I am attaching screenshots of a LIVE client profile inside the therapist portal.

Create 03-mockups/therapist-a-client-detail.html. Same shell.

CLIENT DETAIL
Intent: “what is this person’s history with me?” Must keep:
Back to Clients
Identity strip — initial, name, client since, session count, assessment count
Tabs — Session History, Assessments, each with a count
Session history — date and time, video or phone, status pill, View
Assessments — name, type, progress (current / total), status pill, date. Row opens the response
Empty states for both tabs

---

## Prompt 7 — Messaging

I am attaching screenshots of LIVE therapist Messages.

Create 03-mockups/therapist-a-messaging.html. Same shell. Set Messaging active.

MESSAGING
Intent: “talk to this client.” Keep a two-pane chat. Must keep:
Header — “Messages” + “Private chats and session notes with your clients”
Left pane — search, rows with avatar, name, preview, time, unread, pin. Selected row is navy. Empty: “No client messages yet”
Right pane — client header, thread. Own messages and client messages look different. Session notes look different from direct chat
Composer — text, emoji, attachment. Show a rate-limit state
On a narrow screen, list or thread, not both squeezed together

Do not turn this into email.

---

## Prompt 8 — Assessments

I am attaching screenshots of the LIVE Client Assessments page.

Create 03-mockups/therapist-a-assessments.html. Same shell. Set Assessments active.

ASSESSMENTS
Intent: “what have my clients completed?” Must keep:
Header — “Client Assessments”, Refresh
Search by assessment name, status (All, Completed, In Progress, Not Started, Expired), Search
Table — Client (name + email), Assessment, Type pill, progress bar with current/total, status pill, date, View
Pagination
Empty and error states

---

## Prompt 9 — Assessment response

I am attaching screenshots of a LIVE assessment response.

Create 03-mockups/therapist-a-assessment-response.html. Same shell.

RESPONSE
Intent: “read this clinical result.” Read-only. Must keep:
Back + “Response Details” + assessment name
Client Information — avatar, name, email, phone
Assessment Info — type, status, started, completed, progress
Assessment Results — scores and interpretation
User Responses — each question and the client’s answer, in order

Desktop: client and assessment info on the side, results and answers in the main column. Do not hide answers.

---

## Prompt 10 — Activities

I am attaching a screenshot of the LIVE Activities page.

Create 03-mockups/therapist-a-activities.html. Same shell. Set Activities active.

ACTIVITIES
Intent: “assessments I take for my own profile.” Must keep one card only:
“Big Five Personality Assessment”
Description of BFI-10 (Openness, Conscientiousness, Extraversion, Agreeableness, Neuroticism) used for client matching
Start activity

Do not invent extra activities.

---

## Prompt 11 — Big Five

I am attaching screenshots of the LIVE Big Five flow.

Create:
03-mockups/therapist-a-big-five.html
03-mockups/therapist-a-big-five-results.html
Same shell.

BIG FIVE
Intent: “complete my own BFI-10 and see the five traits.” Must keep:
Landing — back to Activities, short explanation, Start, previous attempts (name, status, date)
Question — one at a time, Likert options, progress, back / next, submit on the last item
Results — “Your Big Five Results”, five labelled bars: Openness, Conscientiousness, Extraversion, Agreeableness, Neuroticism

Do not replace the five bars with a donut.

---

## Prompt 12 — Profile

I am attaching screenshots of the LIVE therapist Profile.

Create 03-mockups/therapist-a-profile.html. Same shell. Set Profile active.

PROFILE
Intent: “this is the record clients and the team see, plus my performance.” Must keep:
Header — “My Profile”, Edit Profile
Identity — photo or initials, display name, specialization pills (first 3, then +N more), Active / Inactive, verification (Verified, Pending, Rejected), email, phone, city
Statistics — average rating, Total Sessions, Active Clients, Completed, Upcoming, View Dashboard
Tabs — Basic Information, Professional Details, Reviews & Feedback

Do not add a Session Preferences tab.

---

## Prompt 13 — Edit profile

I am attaching screenshots of LIVE Edit Profile.

Create 03-mockups/therapist-a-profile-edit.html. Same shell.

EDIT PROFILE
Intent: “update my record and how I get paid.” Must keep these tabs:
Basic Information — personal fields, contact, profile photo
Professional Details — qualifications and expertise
Banking Details — account name, account number, IFSC, bank name, branch, UPI, plus the payout notice
Security — current password, new password, confirm, and the password rules

Save stays obvious. Errors sit on the field. Do not put banking on the public profile page.

---

## Rules for every prompt

- Name the component (“upcoming session row”, “weekly slot cell”), then use Select Mode on that card.
- /Polish after a pass.
- /Inspiration only for one component.
- Stop if it starts editing client or admin files, or adding features that are not in the must-keep list.
