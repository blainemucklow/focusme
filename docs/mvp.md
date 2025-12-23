# MVP High Level Requirements

**Last Updated:** 2025-12-22 (Updated after Phase 0 Planning completion)

---

## Phase 0 - Project Setup & Infrastructure ✅ (PLANNING COMPLETE)

**Status:** Planning complete (2025-12-22), ready for implementation

**Goal:** Prove technical infrastructure end-to-end with dual calendar provider support. Success = user can authenticate with either Microsoft or Google, view their events, and mark meetings as flexible.

### Finalized Decisions (from Planning Q&A)

**Calendar Integration:**
- ✅ Support **BOTH** Microsoft Outlook + Google Calendar from start (not just Outlook)
- Calendar provider abstraction pattern for extensibility
- OAuth authentication with NextAuth.js v5

**Technology Stack:**
- Frontend: Next.js 15 (App Router) + React 19 + TypeScript + Shadcn/ui
- Backend: Next.js API Routes + tRPC (type-safe API)
- Database: PostgreSQL 16 + Prisma ORM + pgvector
- Auth: NextAuth.js v5 (Microsoft + Google OAuth)
- Testing: Vitest + Playwright + MSW
- Deployment: Vercel + Neon (hosted), Podman Compose (self-hosted)

**AI/ML Strategy:**
- Dual support: OpenAI/Claude API + self-hosted Ollama (user-configurable)
- LangChain for orchestration

### Implementation Plan (9 PRs, ~40-50 hours)
1. PR #1: Repository Foundation & Build Infrastructure (4-6h)
2. PR #2: Database Schema & Migrations (3-4h)
3. PR #3: Authentication Infrastructure (6-8h)
4. PR #4: Calendar Provider Abstraction (8-10h)
5. PR #5: tRPC API Layer (4-5h)
6. PR #6: Frontend Calendar UI (6-8h)
7. PR #7: Testing Infrastructure (6-8h)
8. PR #8: Documentation (4-6h)
9. PR #9: UX Wireframes (Excalidraw) (2-3h)

### Phase 0 Acceptance Criteria
- [x] All docs are in place for the overall implementation plan *(phase0_planning_status.md)*
- [x] Tech stack chosen and documented with rationale *(See planning doc)*
- [x] Architecture patterns designed *(Calendar provider abstraction, tRPC, etc.)*
- [x] Implementation broken into logical PRs *(9 PRs defined)*
- [ ] All parts of the tech stack configured and installed *(PR #1)*
- [ ] Basic "Hello World" proving infrastructure *(PRs #1-6)*
- [ ] Build tools, scripts, and how-to docs ready *(PR #1, #8)*
- [ ] First rough draft of UX wireframes *(PR #9)*
- [ ] Epic docs for MVP capabilities *(PR #8)*

### Phase 0 "Hello World" Success Definition
1. User can login with Microsoft **OR** Google OAuth
2. User sees list of next 10 calendar events from their connected calendar
3. User can click a meeting and toggle "flexible" flag → persists to database
4. Infrastructure proven: Next.js + PostgreSQL + tRPC + both calendar providers

## MVP

There are many features I'd love to tackle, but instead focusing on the outcomes I would like to see may help us refine, narrow, etc for what we actually need.  Below is a simple bulleted list of what I think should be in our MVP (before doing competitive research, or discovering any missing, or suggested, capabilities or features). 

For MVP, we should begin building out our core capabilities and testing them, I will be test user for now. I am building this app personally on one of my computers, and I plan to act like a completely different user that is trying to use our app at work.  Key pieces of what should be in the MVP at a rough/short level:

### 1. A calendar assistant that:

#### Basic scheduling, rescheduling, optimizing working blocks

During our research phase of competitive analysis, consider features that other solutions have related to the activity of scheduling, rescheduling, and trying to maximize disruption free working periods.  If any of those features are missing, let's discuss them and see if they are MVP level, or can wait til a later phase.  The below list is also not prioritized yet, we should probably only tackle some of these for our MVP.  As we go through Phase 0 we will refine these requirements.

##### A. Is a wrapper around underlying existing mail products.  Since this is intended for my use case of using this at work, it needs to support Microsoft Outlook for MVP completion.
##### B. Eliminates the user needing to manually try and find available time slots for meetings and rooms, going one step further than what microsoft provides today, which is suggested times that all are completely free that could be like 4 weeks away.  Providing a few options based on "best" upcoming options with the highest percentage of free/tentative blocks.  The system should also ensure there is a room on the invite without the user needing to manually check all of the meeting rooms to see which ones have open slots during that time.
##### C. Provides a capability for the user to specify if a meeting is flexible or not.  If it is flexible, then it could be reorganized/rescheduled to help the user have more potential "available" calendar slots for large team planning, etc.  
##### D. Related to flexible, if the user is creating a recurring series and indicates it is flexible, the system will not try to set every single meeting to always be the same time, that might work for 3 out of 4 every month for user a, but only 1 out of 4 for user b, etc.  Looking ahead to find best time for a recurring series for the user is time consuming. Instead if they indicate for example they want a 1:1 with Joe every week and mark it flexible with a chosen time of Tuesdays at 1:30.  The system will automatically look at all tuesdays at 1:30 and if they are open (or flexible/tentative meetings) then the system will book that time, as close to Tuesday at 1:30 as possible, while also trying to maximize uninterupted time.
##### E. The application should have a way (via button press, or proactie suggestions) to constantly look for ways that flexible meetings can be shifted so that the focus time blocks are maximized for as many of the users on the invite as possible.  If any meetings can be shifted, it should show a preview of here's what it would look like for the next few weeks based on trying to maximize working blocks.  Since meetings always come in and might eat into those blocks, the system should be running this at a high frequency (if proactively making suggestions).
##### F. The user should be able to have a flag to allow others on the invite to reschedule the meeting. This way anyone in the invite can reschedule the meeting themselves if a conflict comes up for just them so that they don't have reach out to the meeting "owner" to ask them to look for another time.

### 2. Anti procrastination, reminders, etc
For users that have a fast paced environment with a lot of different items to juggle, this product will help provide some features that will help them stay as organized as possible.  The persona that captures the types of things we should consider is your ADHD office worker that is involved in 3+ projects and pulled into other discussions and meetings with other teams as well.  See features from other mail clients, popular things like snooze/remind me @ __ etc for the basics. ALso check newer products like HEY for some innovative ideas for how to keep folks on track with the clutter of a chaotic constantly moving work environment.

#### A. Allow the user to snooze reminders, or to specify when to remind them again next.
#### B. Allow the user to create "custom" reminders. For example if an invite comes to them for a large meeting with stakeholders, allow them to add a custom reminder (and ideally a cooresponding calendar block) for a time period they choose ahead of the meeting to do prep work. Or, maybe they need to schedule a meeting with someone else before that meeting.  Allowing "sub meetings/connected meetings/reminders".  This way if one of the meetings gets moved, it can alert the user (depending on if it's the parent meeting or a child/grandchild). or in the case of parent meeting moving, it will auto shift the sub meetings as well.
#### C. Allow the user to very easily and very quickly tag topics, organizers, meeting attendees for the importance of those topics/people to make it a "can't move or miss X because X, Y, and Z people are in that meeting".  Indicate to the user in a visual way which of their meetings on the calendar are high priority, medium, low, etc.  That way as they look to move and shift things, they can quickly see at a glance their options with impact of which meeting to move to make space.  The system should also learn over time which meetings the user tends not to move and see if there is a pattern of topic or people in that meeting (organized that meeting) that would indicate any new invites with that topic or including those people should be "auto-marked" from a priority perspective, but the user can always manually override it.
#### D. Give quick context to users when they are rescheduling meetings. For example, they may choose to edit/reschedule and somehow our system can indicate "This is the 3rd time you've moved this meeting, you should try not to move it again, or cancel it" or "Four of the 7 people in this invite that are your VIPs have accepted, when they are going to RSVP to the meeting.  
#### E. Advanced context.  When the user finishes a series of back to back meetings and is getting ready to go into focus time, or end of day, prompt the user to see if there were any followups or actions needed.  If they say "followup" let the user indicate if it's followup for all, or for subset, and expected timeframe for followup and let the system auto schedule that meeting with a similar topic so that the thread of meetings can be connected.  Also, allow a way for the user to add notes, either manually, or if they are using zoom AI companion or some other auto note taker tool, store those notes for each user. So if there were four people in a meeting, and a summary AI Companion notes after the meeting is received (or zoom recording information), add a link between that person and that topic/meeting.  When new meetings are sent to the user, use those notes to give the user an ability to "prep" for the meeting that take the notes and actions and reminds the user about what was discussed last/agreed to last/etc based on the notes for each invitee that may be relevant to the topic of the meeting. If not relevant, just a quick, last time I talked to X person we were discussing this or I had agreed to a deliverable for them.  This should be a quick bullet that has a link to a more detailed timeline of the notes that they can review.  In addition, when scheduling meetings, allow the user to specify expected outcome of meeting in a quick way, "Decision", "Followup", "Actions" etc.  This way when the meeting is over (eitehr right after the meeting, or in the end of meeting block review, ask the user to ask if the expected outcome occurred and based on which it was, take the appropriate action. So for example, if they select "Followup" at the beginning and at the end they specify that outcome was "actions", allow that meeting to be tagged as having actions related to it.  Create the right reminders and prompts for the user based on those actions.  If it's just followup, ask when followup should be, and with who, and attempt to autoschedule (or provide best options) for them.
#### F. Reminders and reminder fatigue.  Allow the user to indicate if they want start of the day reminders on any recent previous agreed to actions, or todos, or followups that are needed but not scheduled.  Allow the user to indicate completeness, etc. Or they can alternatively choose end of day wrap up as well.  Allow them to configure when they should be notified of upcoming meetings so they can have time to prep, if it is needed.  When that reminder comes, send them the prep information


## Phase 1

#### A. Analytics to automate determine the highest priority, or item that's been open too long, etc each day, week, etc and remind them of the expected actions and allow the user to manually adjust priority. We can use some frameworks if we want here, like an eisenhower matrix or other simple prioritization frameworks.  For phase 1, let's pick one of these priority frameworks and make it work well with calendar/meetings/suggestions/etc to help the user prioritize each day/week/etc.
#### B. Add outlook, gmail integrations.
#### C. See if we can add slack integrations
#### D. Meeting/Scheduling power tools

## Phase 2
#### A. Reports
#### B. Mobile
#### C. Deep analytics
