---
title: Projector Product Specification
version: 3.0
updated: 2026-09-06
status: build-specification
platform: React PWA
---

# Projector Product Specification

**Version 3.0 · 6 September 2026 · Product and engineering source of truth**

Michael Martin owns product scope and acceptance. The responsible engineer owns architecture review, migrations, security, payment integrity, and clock correctness. This document specifies intended behaviour. It does not certify that any feature has shipped.

## 00. How to build from this document

This is the public build copy; the private engineering agreement remains outside this repository. Keep this file in Obsidian or copy it into the application repository. Each build module has a stable `Bxx` ID. Reference that ID in a prompt instead of a page number. Complete dependencies before dependent modules. Build one module or a named slice of a module per task; do not interpret a module request as permission to build the entire roadmap.

### 00.1 Source hierarchy and portability

Use current explicit founder decisions first, this specification for scope and behaviour, the completed design contract in section 03 for appearance, and the wireframe guide for screen references. Use Klaus’s supplied SOW for contractor scope and the engineer brief for technical context and sequencing. Use the investor deck for business hypotheses and future direction, not implementation claims or current traction.

Companion files, resolved beside this file in Obsidian or through the repository's documented paths:

- `Projector-Wireframe-Guide-v2.md`: baseline journey and R01–R12 retention boards.
- `Projector-Engineer-Brief.md`: broader technical context; its clock/payments scope is not part of Klaus’s initial SOW.
- The engineer’s private SOW governs the engagement; section 09 summarises the implementation boundary.
- `Projector-Investor-Deck.md`: creator economics, acquisition hypotheses, and future enterprise motion.
- `Projector-Future-Roadmap.md`: expanded-MVP inventory, integration investigations, and F01–F14 experiments.

The module contracts below are sufficient to identify product behaviour without this conversation. A missing companion wireframe must not lead an agent to invent a design direction. An agent can complete logic, fixtures, and tests while it records missing visual references. Use repository-relative paths when copying this specification; no build requires access to Michael's home directory.

### 00.2 Reusable build prompt

```text
Implement module BXX from Projector-Product-Spec.md.
Read sections 00–07 and the target module, then inspect the existing repository and its agent instructions. Read the completed design contract in section 03 and the target wireframes. Verify the listed module dependencies from code and tests; do not assume that a checked box proves completion.
Build the smallest complete implementation that satisfies the module's behaviour, permissions, failure states, and acceptance criteria. Reuse existing components and services. Include migrations, authorisation, fixtures, instrumentation, and relevant tests. Keep unrequested roadmap features out of scope. Use real integrations in the deployable path and labelled fixtures in tests.
Run the module checks and the shared release checks relevant to the change. Review the screens against the chosen design at the required viewport sizes. Report changed files, test evidence, remaining blockers, and any decision that requires product input. Update the build record in section 11. Do not mark a module accepted while required tests or design checks remain unresolved. Production release follows the repository's established release process.
```

Replace `BXX` with an ID, such as `B04`, or specify a scoped slice and retain the module's invariants. Dependencies are reusable shared contracts; do not rebuild them inside each feature.

### 00.3 Definition of a complete module

A complete module includes its working user journey, persistent data, server-side permissions, loading/empty/error/recovery states, measurable events, and acceptance evidence. Its tests exercise consequential behaviour, including unauthorised access and retries when relevant. It has no unlabelled mock checkout, fake attendance, invented recommendation reason, or temporary bypass in the deployed route. An engineer reviews changes to money, identity, clock state, and access control before live use.

### 00.4 Decisions and estimates

Specific defaults in this spec are implementation choices for a pilot, not measured product outcomes. Section 12 identifies unresolved launch decisions and their owners. An unresolved decision blocks the affected release path, not unrelated implementation. Do not guess provider credentials, production refund promises, or a selected visual direction. The original engineer estimate covers a narrower engagement; re-estimate the expanded MVP rather than copying old dates into new commitments.

## 01. Product purpose and commercial context

Projector helps a film curator programme a live night, sell seats, and host an audience through timed Liner Notes and conversation. Viewers play their own copy of the film on a separate screen. They use Projector on a phone as a companion.

The first audience comes through five founding curators, each asked to host three ticketed screenings. The team needs evidence that curators can attract attendees, prepare without founder assistance, recover from ordinary device interruptions, and persuade people to return. Treat the five-curator/fifteen-screening plan as a test design, not verified traction.

### 01.1 People and jobs

| Person | Job | Product evidence |
|---|---|---|
| Curator | Prepare a coherent night, fill the room, host it, and earn from the work | Preparation time, paid attendance, repeat hosting, amount owed |
| Audience member | Choose a film night, attend without technical friction, and find hosts and people worth returning to | Reservation-to-attendance, second attendance, curator follows, satisfaction with the night |
| Founder/operator | Run the pilot, resolve failures, reconcile money, and learn from sessions they did not attend | Session postmortems, payment reconciliation, audited interventions |

Use `curator` as the domain role and the default product label. Older documents use `projectionist` for the same role. A later copy decision can change the displayed label through one shared terminology file; it does not create another role or change permissions. A curator may also attend another curator's screening.

### 01.2 Commercial rules

The pilot sells a hosted seat for USD 0.99 through web checkout. A curator's first three eligible founding screenings use a 100% ticket revenue share; subsequent screenings use 70%. Store the applicable agreement and rate on each session/order line so a later policy change cannot rewrite past amounts. The founders must confirm the fee/refund basis and founding eligibility rules in decision D02 before live payments.

Follow the engineer brief: record curator liabilities and pay the first five curators through manual transfer. Do not build Stripe Connect for the pilot. Show gross ticket receipts, refunds, processor fees, platform amount, and curator payable as separate ledger values; never label gross receipts as profit.

Seasons reduce repeated booking work; encores reduce repeated preparation; groups, votes, commissioning, and foyers create reasons to return. Personalisation matches viewers to curator programmes and hosting styles. Treat these as hypotheses to measure.

Enterprise tooling for publishers, distributors, festivals, and cinemas is a future commercial motion. Keep domain identities and ownership explicit so an organisation model can be added later. Do not build enterprise tenancy, SSO, sponsorship inventory, white-label publishing, or contract billing for the creator pilot. Investor conversion rates, market sizes, and revenue scenarios are not performance requirements.

### 01.3 Product invariants

1. Projector does not host, embed, capture, or control the feature film. It carries authored notes, permitted pre-show material, and conversation. The viewer presses play and pause on their own source.
2. The server owns room time and state. A browser timer never becomes the source of truth after sleep or disconnection.
3. A viewer can browse, buy a seat, and attend without installing the PWA or creating a persistent social account.
4. A payment-confirmed seat, a vote, an expression of interest, and a group RSVP are different records and different promises.
5. A curator owns their drafts and publishing controls. An attendee cannot discover private drafts by changing an ID or subscribing to a channel.
6. The viewer controls personal taste inputs and optional notifications. Watched history does not mean liked history or Projector attendance.
7. The live phone experience must leave room for watching the film. No growth prompts, foyer alerts, or demand for engagement during playback.
8. Product claims about rights, provider partnerships, and film availability require their own review. The no-player architecture is a technical boundary, not a blanket legal conclusion about supplied images, clips, or public events.

## 02. Phases and scope

Klaus’s SOW determines the foundation order and contractor boundary; the engineer brief informs subsequent technical work. The wireframe guide determines the journeys. The expanded MVP includes the approved retention additions even where the contract engineer's original engagement excludes them.

| Phase | Outcome | Modules | Exit gate |
|---|---|---|---|
| P0 · Foundation | Secure, deployable repository and shared identities | B01–B02 | Isolated environments, tested permissions, migration replay, identity preservation |
| P1 · Curator authoring beta | Five curators can author and rehearse without an audience | B03–B05, B10a | Notes survive failures; server clock and harness pass; complete rehearsals |
| P2 · Paid screening pilot | Founders can run and reconcile fifteen hosted nights | B06–B09, B10b | Paid guest journey, phone hosting, recoverable live room, refund path, postmortems |
| P3 · Expanded retention MVP | Audience can discover, return, contribute, and refine taste | B11–B20; B21 provisional | Approved retention flows, real import fixtures, permissions, mobile-browser/PWA validation |
| P4 · Validated extensions | Test integrations and future commercial/product motions | Section 10 | Separate approved experiment or implementation brief |

P2 can run before P3 completes. Do not call the full expanded MVP complete after P2. Review work throughout P0–P3; Klaus reviews during his engagement, and Michael must arrange any later specialist review. Do not defer high-risk review to a final week. The initial pilot capacity is 100 concurrent clients in one room; set saleable audience capacity below that limit to reserve host/operator connections (default: 95 audience seats). Test larger rooms before increasing the published capacity; the deck's thousands-of-seats examples do not establish infrastructure capability.

### 02.1 Ownership

Klaus delivers B01–B02 within the agreed SOW schema inventory, in Foundation → Data → Guardrails → Identity order, and reviews commits during his engagement. Michael and coding agents build B03–B20 and provisional B21 on that base. Clock, money, and access-control changes need a named reviewer; arrange that review after the foundation engagement rather than assuming ongoing availability. The foundation engagement excludes the subsequent product build.

### 02.2 Scope boundaries

The core pilot includes manual timestamping, basic chat moderation, intermission with pause acknowledgements, reconnect/resync, ticket refunds, pre-show, and Lights up. Keep the three Room arrangements as one component with different presentation modes. Basic recap and saved notes support the pilot; the complete Passport and discovery features arrive in P3.

Deferred: research agent, expert-request workflow, automatic timestamp discovery, quote checking, telestrator, native video intermission, automated social posting, push as a required channel, Netflix import, Trakt connection, automated payouts, and F01–F14 experiments. Store compatible identifiers where needed, but do not prebuild empty subsystems. Younify linking is provisionally included as B21 with a provider-validation gate; it must not block the base MVP. Text intermission satisfies the pilot; a drawn camera or telestrator control does not authorise its implementation.

## 03. Design contract · fill once before visual implementation

The audience uses a React PWA. Curator authoring uses a desktop web workspace; Go live and On air also support phones. The visual direction remains open. Existing wireframes describe actions and hierarchy; they do not select fonts, colours, effects, or layout styling for the new build.

### 03.1 Design handoff fields

Fill these fields with repository-relative paths or stable URLs. Keep design tokens in a single source and link to it from this table. A token revision should propagate through shared components rather than require editing each module.

| Key | Fill-in value | Required for |
|---|---|---|
| DESIGN_STATUS | `[DESIGN: pending / approved]` | Visual acceptance |
| DESIGN_DIRECTION | `[DESIGN: selected direction name and short rationale]` | UI work |
| DESIGN_GUIDE | `[DESIGN: path to approved DESIGN.md]` | UI work |
| DESIGN_TOKENS | `[DESIGN: path to token source consumed by frontend]` | UI work |
| COMPONENT_REFERENCE | `[DESIGN: path/URL to approved shared components]` | UI work |
| SCREEN_REFERENCES | `[DESIGN: directory/URL with references named by wireframe ID]` | Each module's visual acceptance |
| LOGO_ASSETS | `[DESIGN: licensed logo/icon asset directory]` | Branded shell |
| TYPE_ASSETS | `[DESIGN: font files, licences, type scale reference]` | Branded typography |
| MOTION_RULES | `[DESIGN: durations, easing, reduced-motion alternatives]` | Live transitions |
| CONTENT_RULES | `[DESIGN: voice, terminology, long-copy examples]` | UI copy |
| DESIGN_REVIEWER | `[DESIGN: approver and approved revision/date]` | Visual acceptance |

After filling the fields, an agent validates paths, token loading, font assets, reference coverage, and reduced-motion rules. Do not substitute an older design file merely because it exists. Nonvisual modules can proceed while these fields remain pending. A module with UI can pass functional checks and remain `design-pending` until its chosen references exist.

### 03.2 Stable UX requirements across design directions

Use 390×844 as the primary phone reference and test at 320px width, a larger phone, tablet, and desktop. Desktop authoring targets 1440×900 and supports 1280px width. Below the supported authoring width, offer a saved-work message and a return-on-desktop path; do not block phone hosting, audience pages, or account controls.

Use readable type in dim conditions, visible focus, labelled controls, sufficient contrast, keyboard access, and touch targets meeting a 44 CSS-pixel product target. Respect reduced motion. Do not express state by colour alone. Provide accessible countdown text without screen-reader announcements every second. Let screen-reader users choose chat announcements; do not announce a flood of historical messages on reconnect.

Keep live controls thumb-reachable and destructive actions distinct. Confirm ending/cancelling a session; do not interrupt a normal note save with confirmation. Give long text, missing images, loading, empty, error, offline, and permission-denied states the same design attention as the happy path. Existing curtain and lighting transitions require a selected visual reference and a nonanimated equivalent.

## 04. Shared architecture, data, and access contracts

### 04.1 Stack and boundaries

Use React with TypeScript for the audience PWA and curator web frontend. Use Supabase for Postgres, Auth, Realtime, and private object storage, Stripe for web payments, and a deploy target such as Vercel. Confirm the deployment choice in P0. Add a server job runner appropriate to the deployed environment for timed events, webhooks, imports, and email. A platform with short-lived request handlers needs a durable scheduling solution; do not run a two-hour film in a request handler.

Keep business operations in server-side functions with validated input, authenticated actor, authorisation, transaction boundaries, and typed output. Route components call those operations. Provider adapters handle email, payments, and permitted metadata. Development fixtures implement the same interfaces but cannot serve production requests. Do not introduce microservices or a machine-learning pipeline for the pilot.

### 04.2 Identity and permission model

Create an anonymous Auth identity for a guest. Use its stable person ID for seats, contributions, chat, and saved notes. Curator privileges require an operator-controlled grant plus Google sign-in; Google sign-in alone never grants curator access. Audience accounts use Google initially; Apple is an optional later extension, outside Klaus’s supplied SOW. A verified email token can recover a seat or establish eligibility for a vote without creating a public profile.

When a guest signs into an existing account, merge ownership in a server transaction after proving both identities. Deduplicate seats and votes under their domain constraints. Retain the financial order trail. Do not merge people by an unverified email string. Handle interrupted linking and already-linked retries. A guest who moves to another device recovers access through a verified email link; possession of the public screening URL conveys no entitlement.

| Actor | Permitted access |
|---|---|
| Public/anonymous visitor | Published programme summaries and permitted foyer previews; own guest records |
| Paid attendee | Own seat and order; entitled room and recap; own messages, ratings, and saved notes |
| Signed-in audience | Own Passport/imports/preferences; joined groups/foyers under their visibility rules |
| Curator | Own drafts, authored content, own session operations, attendance aggregates, permitted contributions and regulars records |
| Operator | Audited support actions, configuration, refunds/payout reconciliation, moderation escalation |
| Worker | Narrowly scoped scheduled operations; no public service credentials |

Apply row-level security and storage policies; test with another user and direct requests, not only hidden buttons. Restrict realtime subscriptions to authorised rooms. Public projections must not expose raw seat emails, private notes, taste histories, payment identifiers, or account tokens. Curator access to their audience is not an unrestricted export of personal data; the MVP uses consented notifications and external handoffs.

### 04.3 Core records

Use UUIDs for internal identities, UTC timestamps for instants, IANA time zones for display and scheduling, integer seconds for film offsets, and integer cents plus currency for money. Store date-only imported diary dates as dates with source precision. Do not reinterpret them as known watch timestamps.

| Entity | Minimum fields and constraints |
|---|---|
| Person | ID, auth linkage, display name, verified contact references, role grants, lifecycle state |
| Curator profile | Person ID, public slug, bio, hosting/film interests, approved status, outbound links |
| Film | ID, title, year, optional metadata IDs, media type, manually entered provenance; titles alone are not unique |
| Film edition | Film ID, edition label, runtime; session references the edition used to author notes |
| Session | ID, curator, film/edition, UTC showtime, display time zone, status, capacity, price, agreement version, one-sheet, publication revision |
| Availability | Session/film, country, service/access type, source URL, checked-at time, manual/provider source |
| Liner Note | ID, session, offset, body, optional still/source, armed flag, revision, deleted state |
| Pre-show item | ID, session, negative offset, URL, preview/embed status, revision |
| Intermission plan | Session, planned offset, proposed duration, message; execution references room clock state |
| Room state | Session, run ID, media anchor, server anchor time, running flag, state version, last event sequence, film-ended time |
| Room event | ID, session/run, sequence, kind, effective time, media offset, payload revision; unique sequence per run |
| Seat | Session/person unique, order line, status, paid/entered timestamps; attendance intervals stored separately |
| Order and order line | Person, currency, immutable unit price/share terms, Stripe references, payment/refund state, session allocation |
| Ledger entry | Order line, type, integer amount, source event, agreement version; append-only adjustments |
| Chat/contribution/question | Session, author, content, created-at, moderation state; question links to an optional wrap answer |
| Follow, saved note, rating | Person/target uniqueness; rating separates film and night scores |
| Promo link and touch | Target type/ID, channel, random link ID; timestamped clicks and attributable order/seat reference |
| Delivery/job/audit record | Idempotency key, state, attempts, next retry, error code; actor/action/target for sensitive operations |

Create migrations as modules need tables. Keep a schema inventory in the repository; agents must not invent parallel film, person, or payment tables to unblock a later feature.

### 04.4 Retention records

| Module | Records and invariant |
|---|---|
| B12 repertory | Source session ID, independent duplicate draft, encore interest unique per person/source |
| B13 seasons | Season, ordered session links, description, publication revision; one curator per season |
| B14 groups | Group, membership, invite, one active screening proposal, RSVP; RSVP never grants a seat |
| B15 ballots | Ballot, options, votes; one active ballot per curator and one vote per eligible person |
| B16 regulars | Recognition grant per person/curator, curator-private notebook entry; revocation removes notebook access |
| B17 commissioning | Proposal, threshold/deadline, candidate dates, unique interest, selected availability dates |
| B18 requests | Person/film watchlist, scoped alert subscriptions, curator requests; imported watchlist does not create consent |
| B19 foyer | Foyer, membership, thread/reply, report, moderation action; one foyer per curator |
| B20 taste | Explicit preference, imported record/batch, source signal, curator feedback, model version; explicit correction outranks inferred preference |

### 04.5 Operation and event conventions

An operation returns a typed result or one of: unauthenticated, forbidden, not-found, invalid-input, version-conflict, capacity-changed, payment-pending, retryable-provider-error, or permanent-provider-error. Return safe user copy and a support correlation ID; keep stack traces and secrets in restricted logs.

Mutations carry an idempotency key where retries can duplicate money, content publication, or imports. Editable records carry an expected revision. Reject stale writes and let the user reconcile changes; do not use last-write-wins for an evening of notes. A failed request must leave the last confirmed record readable.

Broadcast committed changes through a durable event/outbox path. Consumers deduplicate event IDs and recover from a snapshot plus sequence. Do not promise exactly-once network delivery. Achieve one visible effect by deduplication and database constraints. Clients cannot issue privileged broadcasts as if they were server events.

### 04.6 PWA behaviour

Provide a web app manifest, icons, HTTPS delivery, and a service worker with an explicit cache policy. Support normal browser and installed modes from the same routes. Installation remains optional; offer platform guidance from settings or after a completed night, never over checkout or the leader. Detect share and push capability rather than assuming it. Use copy-link and email/in-app fallbacks.

Cache the shell and agreed public assets. Do not cache raw imports, tokens, payment responses, or private notebook records in the service worker. Private cached data must be user-scoped and cleared on sign-out. Offline pages show what is unavailable; an offline click cannot claim that a purchase, vote, or post succeeded. Reconcile pending writes by stable IDs after reconnect. New service-worker versions wait until the active screening ends before activation.

External browser returns for sign-in, Stripe, file exports, and B21 recover their destination and state through server records. A browser tab and installed PWA may not share the same local state; authenticate and recover rather than assuming a return URL restores it. A locked or backgrounded phone suspends UI work; foreground return follows section 05 snapshot recovery. Ask for notification permission at a user-chosen action, retain a denied state, and keep push optional.

## 05. Room clock and session state contract

### 05.1 Lifecycle

`draft → published → lobby → live ↔ intermission → lights_up → ended`; cancellation is available before live. During live, an operator/curator may abort through an explicit failure flow that records the reason and starts refund review. Publishing is a booking action; it is distinct from arming notes and starting the film. This permits ticket sales while the curator finishes preparation.

Publication requires title/edition/runtime, showtime/time zone, price/capacity, one-sheet, and film-access information or an explicit unknown state. Going live requires at least one valid armed note, a reviewed queue, and host readiness. Cancelled, ended, and aborted sessions cannot restart under the same run ID. Rehearsals use isolated run IDs and never issue real seats, messages, or analytics attendance.

### 05.2 Time calculation

For a running room, media position equals `anchor_media_ms + (estimated_server_now_ms - anchor_server_ms)`. For a paused room it equals `anchor_media_ms`. The server atomically replaces both anchors, the running flag, and the state version at start, pause, and resume. Intermission time therefore does not advance film time. Do not derive progress from wall time since the advertised showtime after a delay or pause.

Clients estimate server offset with timestamp exchanges and round-trip measurements, using monotonic time for local interpolation. Refresh on connection, foreground return, and at a bounded interval while active. The implementation documents the chosen interval and offset-filter method in its architecture decision record. Ignore stale state versions. The server stores planned UTC showtime; time-zone display never changes the event's instant.

At the agreed start, the prepared host confirms the countdown. If the host is not ready, the room remains waiting with an explanation. A late host selects a new effective start; connected viewers receive the same future start instant. The fifteen-second leader ends on that instant. A client arriving mid-leader renders the remaining duration. The authoritative clock starts at zero even if a particular attendee presses play late; that viewer uses resync.

### 05.3 Notes and interruptions

Scheduled note events cross their mark against authoritative media time. A worker commits the firing record with uniqueness on run/note/fire generation; the client renders each event once. Choose and document a scheduler capable of the B04 timing target before production. Manual fire commits a distinct command and suppresses that note's pending scheduled firing for the run. A deliberate later repeat must be a new note, not a replay caused by reconnect.

A live edit changes only unfired notes. Fired content stays in the historical event snapshot; the curator can publish a labelled correction. Moving an unfired note behind the current clock asks whether to fire now or keep it unscheduled. Removing an unfired note cancels its pending event. Optimistic revisions prevent two host tabs from overwriting each other.

After sleep or reconnect, fetch current state and missing events. Add missed notes to history without a burst of notifications. Show the room's current film position and one **Rejoin here** action with instructions for the viewer's television. Projector cannot seek or verify the external film. If a viewer chooses to remain behind, show them as away from live sync and allow quiet note-history browsing; do not claim they are synchronised.

### 05.4 Intermission and end

A host pause fixes the media anchor. The room shows a proposed break countdown and **I've paused my TV**. One acknowledgement per present person updates the host's aggregate; acknowledgement does not prove a TV paused. The countdown invites the host to resume; the film clock resumes only after a host command and shared resume countdown. A disconnected host leaves a paused room paused. Operator recovery requires an audited action.

The host ends the film; runtime alone does not end it. Set `film_ended_at` once and stop future notes. Lights up lasts five minutes from that server instant: questions and next-screening booking at entry, optional continuation link at minute three, default account invitation at minute four, chat closure at minute five. Create the recap and postmortem through retryable jobs. A retry must not create another end time or duplicate messages.

## 06. Money, notifications, and data handling

### 06.1 Checkout and entitlement

Server-created checkout calculates the total from current session records, never a browser amount. The pilot allows one seat per person per session. Stripe webhook signature verification and a unique processed-event record establish payment state; a success-page redirect does not grant entitlement. Support wallet methods where available and a card fallback.

Use a short-lived inventory allocation during checkout to avoid overselling; this is not a confirmed seat. Set the allocation expiry to the documented payment-provider checkout expiry, with a pilot target of no more than 30 minutes. Confirm the supported expiry range during B06 rather than hardcoding an unsupported duration. Expired or delayed successful payments need reconciliation: confirm only if capacity permits, otherwise refund and notify. Never mark a paid order as simply lost because its allocation expired.

For a season, allocate all selected sessions as one purchase. Recheck before payment, exclude existing seats, and require confirmation of changed selection/price. Persist per-session amounts. If a race prevents fulfilment after payment, refund unfulfilled lines and explain the partial result; never substitute another screening. Display pending confirmation while webhook processing continues, with reload-safe status lookup.

Cancellation, duplicate payment, and failed fulfilment require a refund path. Operator refund commands carry a reason and idempotency key. Mirror refund results into the ledger from verified provider events; handle pending and failed refunds. A paid seat remains historically visible even after cancellation/refund, with status. Publish discretionary no-show/refund terms only after D02 approval.

### 06.2 Reminders and attribution

Send a receipt and material reservation changes as transactional messages. Offer reminders through an explicit preference. Initial reminder schedule: 24 hours and 10 minutes before the session, skipping times in the past. A reschedule invalidates pending reminders and schedules replacements. Optional promotional, group, watchlist, and foyer notices have independent consent and mute settings.

Attribution measures a tracked link click through a reservation and attendance. Initial model: last eligible tracked click within seven days, recorded as a versioned rule. Store raw tracked clicks and session-level deduplicated browser visits separately. Bot filtering is approximate. Do not label clicks as unique people or treat a follower count as measured reach. Record the source/date of curator-supplied audience-size estimates.

### 06.3 Content, imports, and privacy

Render user text as text or a strictly sanitised supported format. Validate link schemes and use safe external-link handling. Preview fetching runs server-side with private-network URL blocking, response limits, and timeouts. Do not let a preview request access internal services. Accept uploaded stills only through validated image types/size limits and ownership policies. Link/embed failure degrades to a usable link card.

Keep imports private. Parse recognised files and columns, exclude unrelated archive content, and show review before persistence. Delete raw import files after completion or cancellation; expire abandoned staging after 24 hours as an implementation default. Account deletion removes profile, taste, imports, and community membership; pseudonymise retained contributions and retain only financial/security records required by the approved retention policy. D03 approves production retention periods and user-facing terms before launch.

A viewer can revoke recognition, leave a group/foyer, disconnect a future provider, remove imported signals, and mute messages without cancelling paid seats. Do not send engagement notifications to a deleted or opted-out contact. Keep an auditable preference change and a suppression check at dispatch time.

## 07. Shared quality and release gates

These are proposed pilot acceptance targets. Measure them in a named environment and record browser versions, client count, and network conditions. Do not claim service-level guarantees from a laboratory pass.

| Area | Gate |
|---|---|
| Clock | 100 simulated clients in a two-hour run; active connected clients render a given note within a one-second spread under the harness's documented network profile; no duplicate effects |
| Interruptions | Suspend/resume at least 20% of simulated clients; recover authoritative position/history within three seconds after a healthy connection returns; do not assess backgrounded clients as if they rendered while suspended |
| Real phones | At least one iPhone and Android device complete start, pause/resume, lock/unlock, reconnect, checkout return, and sign-in return in browser and installed-PWA modes |
| Writes | A stale second-tab edit cannot erase the first tab's save; retrying a confirmed mutation does not duplicate it |
| Payments | Invalid/replayed/out-of-order webhooks, concurrent last-seat purchase, late success, failed refund, and partial season fulfilment have deterministic tested outcomes |
| Permissions | Cross-user, cross-curator, anonymous, blocked, revoked, and operator access checked through direct database/API/channel paths |
| Performance | Target public detail-page LCP ≤2.5 seconds in the recorded mobile test profile; API read/write p95 ≤1 second excluding provider jobs; document failures before wider release |
| Accessibility | Keyboard and screen-reader checks for critical flows, contrast/focus review, 200% text zoom, reduced motion, labelled error recovery |
| Operations | Staging migration replay; backup/restore rehearsal; secret checks; functioning alerts; previous deploy rollback; feature disable path without stopping unrelated modules |

Automate type checking, linting, relevant tests, production build, and migration checks in CI. Fail the deployment check on failures; never swallow a nonzero exit. Keep test-mode Stripe and fixture accounts separate from production. Do not reload active rooms to activate a new service worker or deploy version. Maintain compatibility with the prior frontend while live sessions finish.

Every UI module references the design revision used for its screenshots. Do not mark visual acceptance while the design contract is pending. Validate risky behaviours with meaningful integration tests; avoid tests that merely repeat labels or implementation structure.

## 08. Build modules · foundation and paid pilot

Each module inherits sections 03–07. “Owner” describes implementation responsibility, not an expansion of the contractor's SOW. Klaus owns only the foundation modules within the accepted schema inventory. Michael and coding agents own subsequent modules; specialist review beyond the initial engagement requires a separate arrangement.

### B01 · Repository, data foundation, and development guardrails

**Phase:** P0. **Owner:** Klaus. **Dependencies:** approved foundation schema inventory, deployment access. **Screens:** a minimal development session editor for acceptance, not finished product design.

**Outcome.** Michael can clone the repository, run a seeded local environment, make a branch, open a pull request, view its preview, and rely on failed tests/builds to prevent deployment.

**Contract.** Follow the SOW sequence: Foundation, Data, Guardrails, Identity. Configure Supabase, local/deployed environment templates, secrets separation, preview deployments per PR, GitHub Flow, GitHub Actions linting, test runner, and deploy guard. Implement the agreed schema through migrations with seed fixtures and RLS tests. Scaffold Playwright MCP and integration tests for cross-user read/write isolation. Supply `CLAUDE.md`, recommendations as agent skills/documentation/setup prompts, and commit review during the engagement.

The minimum acceptance schema contains identities/role assignments, films, sessions, notes, seats, and testable ownership. Include representative guest-owned records in fixtures to prove later linking. Section 04 describes the full product model; use the foundation inventory in section 09 to agree which tables Klaus creates now. Michael adds later-phase migrations against the same conventions. No finished live room, payment processing, or recommendation engine belongs to this module.

**Failure handling.** A missing secret produces a safe setup error. A clean migration failure blocks deployment. Failed build/test commands must propagate their exit status. A preview uses isolated test data and credentials.

**Acceptance.** On a clean environment, migrations and seed data run with documented commands and no manual database edits. A failed test and a broken build each block deployment. User A cannot read or write B's session, notes, or seats through direct requests. A new PR produces a working preview. Required setup documents exist and a clean checkout can follow them. Record exact commands and CI run references.

### B02 · Google identity, anonymous continuity, and ownership

**Phase:** P0. **Owner:** Klaus. **Dependencies:** B01. **Screens:** minimal sign-in and anonymous-session demonstration.

**Outcome.** A guest keeps their records after Google sign-in and reload; one user cannot take over another's records.

**Operations.** Create anonymous identity; sign in with Google; link or merge a proven guest identity; read current person/role; sign out. Use Supabase Auth with server-validated ownership. The supplied SOW commits Google and anonymous support. Apple sign-in and email seat-recovery features are later extensions implemented under B06/B11 if approved, not acceptance conditions added to Klaus's identity work.

**Rules.** Link to a new account and merge into an existing account without dropping notes, seats, or saved guest records. A public Google login grants an audience account, not curator privilege. Provide a development operator mechanism to grant curator privileges. Enforce RLS before and after linking. Preserve a financial reference rather than deleting it when a duplicate person/session seat needs reconciliation.

**Failure handling.** Cancelled OAuth returns to the originating page; expired/replayed linking tokens cannot mutate ownership. Interrupted linking can be retried. A guest who signs out sees no previous user's private data on a shared browser. Do not implement an email-string ownership shortcut.

**Acceptance.** A user signs in, creates a session, and reloads it. Two authenticated users fail cross-user reads and writes. An anonymous fixture with session-linked records signs into a new and an existing account without loss; both paths retain access isolation. A forged merge request fails. This directly implements the SOW's identity and isolation criteria.

### B03 · Curator workspace and note authoring

**Phase:** P1. **Owner:** Michael/agents. **Dependencies:** B01–B02, completed design contract for UI. **Screens:** CuratorPrep 1J①, CuratorNotes 1J④, CuratorQueue 1J⑤.

**Outcome.** A curator creates a film session, writes timed notes, and returns to durable work.

**Operations/data.** Create/update session draft and film edition; create/update/arm/delete note with expected revision; add/update pre-show item and intermission plan. The curator enters title/year, edition/runtime, showtime/time zone, pitch, access information, and optional external handoff. Manual `mm:ss` accepts minutes beyond 59; reject negative note marks and marks outside runtime. Support optional still/source and show save status.

Queue notes by timestamp, with stable tie ordering by creation ID; warn about close marks without prohibiting them. Pre-show marks range from −30:00 to −2:00, and use link/preview rows. Research controls, expert tools, timestamp inference, quote check, and telestrator stay absent. The curator can save incomplete drafts; the server validates publication and launch requirements at their own transitions.

**Recovery.** Preserve unsaved text in the current editing session, with a retry/copy option after failure. Use revision conflicts for two tabs, showing server and local values. Retry an image upload without losing note text. Maintain a visible last-saved time; do not claim success before acknowledgement.

**Acceptance.** Author at least 40 notes, reload, and confirm content/ordering. Reject invalid marks and cross-curator mutations. Simulate failed save, failed upload, and a stale tab; no acknowledged note disappears. Test daylight-saving scheduling with a zone-aware input and a visible local/UTC confirmation. Record `draft_created`, `note_saved`, and `authoring_error` with IDs rather than note bodies.

### B04 · Clock, firing engine, and simulation harness

**Phase:** P1. **Owner:** Michael/agents with a named engineering reviewer. **Dependencies:** B03. **Screens:** development harness and clock adapter used by 1J⑥/⑦/⑨. **Outside Klaus's supplied SOW.**

**Outcome.** A shared state machine coordinates a two-hour run despite client suspension and retries.

Implement section 05 as a tested server domain service: prepare/start run, read snapshot/events, pause/resume, fire note, revise unfired note, and finish/abort. Require curator ownership or audited operator recovery for state commands. Serialize competing commands through expected state version and database transactions. Use a durable scheduler and outbox; document its deployment/runtime cost and failure recovery.

Create a deterministic accelerated test harness plus a real-duration soak. Simulate 100 clients with varied clock offsets and network delay, suspend at least 20%, reconnect, replay duplicate events, drop broadcasts, and fail/restart the scheduler. Define the network profile in the test fixture and report active-client timing distributions and excluded suspended intervals.

**Acceptance.** Pass section 07 timing gates; no duplicate fires after retries; pause time never advances media time; stale commands fail; missing broadcasts recover from history; a crashed worker resumes without missing or repeating committed notes. Test a manual fire racing a scheduled fire and an edit moving a note into the past. Persist the test report. Real-phone evidence is required again in B08; simulation alone does not certify mobile behaviour.

### B05 · Dry run and curator beta handoff

**Phase:** P1. **Owner:** Michael/agents. **Dependencies:** B04. **Screens:** CuratorLive 1J⑨.

**Outcome.** A curator rehearses a complete programme before selling an audience experience.

Start a private rehearsal from a draft queue at normal or 8× speed. Reuse production clock/note semantics with a rehearsal clock adapter and isolated run. Preview pre-show, note timing, and intermission; let the curator correct notes and restart. Rehearsal controls cannot publish a session or send notifications. Store rehearsal results separately from live attendance and commerce.

**Recovery.** A disconnected rehearsal can recover its state or start a new run. Edits save through the authoring revision path. Changes to runtime flag out-of-bounds notes. Show missing preview assets without stopping text notes.

**Acceptance.** A curator rehearses the 40-note fixture, corrects a mark, and sees the correction in a new rehearsal. Normal/8× modes produce the same event order. A second curator cannot read the run. No real mail, seats, or financial records appear. Complete a hands-on beta with up to five design partners and record friction/issues; this research gate does not claim recruitment is complete.

### B06 · Published screening, guest checkout, and seat recovery

**Phase:** P2. **Owner:** Michael/agents with payments/identity review. **Dependencies:** B02, B03; D02 before live charges. **Screens:** Discover 1G①/②, confirmation/status states.

**Outcome.** A viewer buys a hosted seat and can return to it through a phone browser.

Publish a validated session through a unique share URL. Show film, edition/runtime, curator, local showtime/time zone, pitch, price, capacity, and manually supplied region/service access. Unknown access is explicit. Metadata/provider access is not required for the pilot. Offer a normal web checkout with supported wallets and card fallback; implement section 06 allocations, webhook verification, price integrity, refunds, and pending-state recovery.

After payment, offer two optional prompts: contribution and question. A guest can skip both. Implement an expiring single-use email recovery link scoped to that guest's seats with rate limits and no account-enumerating response. This extends Klaus's foundation; do not assume the SOW includes mail delivery or seat recovery. A confirmed guest may attend without saving a Passport.

**States.** Draft/unavailable link, sold out, cancelled, changed showtime, payment pending/failed/confirmed, allocation expired, recovery expired, refunded. Refunds update entitlement according to the approved policy; historical receipt remains accessible.

**Acceptance.** Test malicious price alteration, duplicate seat attempts, two buyers competing for the last allocation, a closed browser during checkout, delayed/out-of-order webhooks, and a recovery link on another device. Grant no seat from a fabricated success URL. Demonstrate one refund through provider confirmation and ledger reconciliation. Record `checkout_started`, `payment_confirmed`, `seat_confirmed`, and `refund_state_changed` from authoritative records.

### B07 · Lobby, pre-show, chat, and presence

**Phase:** P2. **Owner:** Michael/agents. **Dependencies:** B04, B06. **Screens:** TheNight 1D①/②, Room chat arrangement 1C.

**Outcome.** Paid attendees enter a hosted space before the film and share a readable conversation.

Open the Lobby at T−30 for entitled attendees and host. Show film-access instructions, programme time, next dated screening, and the curator's pre-show links. Calls appear at T−10 and T−2. Pre-show links remain in history for late arrivals; do not autoplay sound or replay missed embeds. Mount one embed at a time and fall back to a preview/link when a provider fails. Honour the final two-minute quiet window.

Implement paginated chat, presence heartbeats, and moderation: host/operator may mute or remove a participant's posting rights and remove a message; members may report and block. Posting removal does not invent a refund policy or erase a receipt. Rate-limit sends and validate text length; initial defaults are 2,000 characters and ten messages per ten seconds per person. Recover an optimistic pending message by client-generated ID, avoiding duplicates after retry. Presence expires after missed heartbeats; distinguish connected count from paid seats.

**Acceptance.** An unpaid user cannot subscribe to private chat. A removed message stays removed after reconnect. Blocking hides the blocked person's contributions for that viewer. A muted account fails a direct send request. Two tabs count as one person in presence. A failed embed does not stop chat or the clock. Measure `room_joined`, `room_left`, `message_sent`, `moderation_action`, and connection faults without copying chat into analytics.

### B08 · Live Room, phone hosting, intermission, and resync

**Phase:** P2. **Owner:** Michael/agents with clock review. **Dependencies:** B04, B07. **Screens:** 1J⑥/⑦ phone and desktop; 1D③–⑨ excluding telestrator; 1A/1B/1C.

**Outcome.** A curator hosts from a phone while attendees watch their own televisions.

Implement the leader and launch handshake in section 05. Provide one Room component with chat-forward, note-history, and single-note modes. Preserve preference and history when switching. Do not use unread counters to pull attention from the film. Host controls show current time, present count, next note, fire-now, unplanned note, pause/intermission, resume, and end. Confirm end, keep normal controls reachable with a thumb, and expose state conflicts from another host tab.

Intermission stops media time, collects unique pause acknowledgements, and resumes through a shared countdown. Text hosting is sufficient; native video/telestrator controls remain deferred. Personal resync shows the current room timestamp and instructions, with **Rejoin here** or **Stay away**. It does not promise automatic television control.

**Acceptance.** Three real devices show the same note within the target under a healthy network; validate iPhone and Android lock/unlock and a mid-intermission reconnect. A host disconnect cannot cause a second start or auto-resume. An attendee misses notes while asleep, then sees them in history without a notification burst. End closes the firing engine. Save notes against stable IDs and preserve them after account linking. Record latency, state version, and reconnect outcome rather than inferred TV progress.

### B09 · Lights up, recap, ratings, and follow-through

**Phase:** P2. **Owner:** Michael/agents. **Dependencies:** B08. **Screens:** LightsUp 1D⑩, AfterTheShow 1H and basic 1I.

**Outcome.** Attendees finish a conversation, keep useful notes, and reserve the next night.

Use the server-timed five-minute sequence in section 05. Show the submitted questions and host's text answers. Pin a dated next screening using the same B06 checkout. At minute three, offer the host's external destination if configured; label a profile link as a profile. At minute four, invite eligible guests to save an account, without repeating a dismissed invitation. Persistent features in P3 may invite sign-in earlier at the chosen action.

Create an entitled recap with fired note snapshots, saved notes, host-selected discussion highlights, answered questions, three optional curator-entered discovery tags, and the next session. Do not publish the attendee roster or private contributions to the public web. Record separate film and night ratings on a 1–5 scale with labelled ends; either rating may be skipped. No Letterboxd write-back.

**Acceptance.** A delayed end uses actual `film_ended_at`. Reloading at minute four does not restart the window. Chat closes at minute five on server and client. A failed recap job retries without duplicate content. Guests can recover their recap; a stranger cannot read private notes/questions. Disliking the film does not lower the curator's night score. Later P3 prompts occupy one secondary action, not competing modals.

### B10 · Promo kit, postmortems, operator tools, and manual payouts

**Phase:** B10a in P1; B10b in P2. **Owner:** Michael/agents; financial/reliability review for B10b. **Dependencies:** B03 for B10a; B06–B09 for B10b. **Screens:** CuratorShip 1J⑧; operator and session-report screens to add to the design reference.

**Outcome.** A curator can share the night and inspect results; Michael can operate it without attending every session.

**B10a, curator beta promo tools.** Generate a share preview, distinct tracked links for channels, and editable deterministic draft copy. Share through copy/link or user-invoked device sharing. Do not auto-post to social at zero; The Howl is a manual reminder/share action in this release. Preview reminder copy during the authoring beta; activate consented delivery after B06/B07 through section 06. Beta draft links use a private preview and cannot accept payment before B06. Show channel clicks, attributed seats, and attendance with the attribution model label.

**B10b, paid operations.** Create a postmortem after a run: paid/refunded seats, unique presence and presence duration, note-firing timing distribution, missed/duplicate-event diagnostics, reconnects, state changes, and errors. Separate simulated data. The curator receives their report; operators have cross-session access. Redact chat bodies, tokens, and private preferences from diagnostics.

Implement a restricted operator view for session cancellation/abort, refunds, failed jobs, support lookup, moderation escalation, and payout reconciliation. Record curator payable from the ledger, allow manual transfer reference/date/amount entry, and prevent double marking. Do not integrate Stripe Connect. Keep audited adjustments for later refunds after a payout.

**Acceptance.** For B10a, save and reload distinct channel links and edit/share preview copy without sending real reminders from a draft. For B10b, produce reports from a healthy and an intentionally faulted run. Retry job/email delivery without duplicate financial effects. Trace a tracked visit to a confirmed seat and attendance; show unattributed traffic as such. Reconcile payment/refund/provider fees and a manual payout against order lines. An ordinary curator cannot invoke operator actions. The P2 release must include a support contact and failure/refund runbook.

### B11 · Curator profiles, discovery, and Passport foundation

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B09–B10. **Screens:** CuratorProfile 1K, Discover 1E/1F, Passport 1I.

**Outcome.** A viewer finds a curator, follows their programme, and returns to their own record.

Publish a profile with bio, social links, prior public screenings, upcoming bookable sessions, and curator-selected links. Preview generation is a background job with link fallback. Show public room sizes only as aggregate counts. Build the Marquee's On now, Tonight, This week, For you, and Following views. Start with date/service/follow filtering; B20 adds taste ranking. A curator without a scheduled session remains followable.

Implement optional region/service onboarding with rental/other-access preference. Saving a follow or Passport asks for account sign-in; guest checkout remains available. Provide Passport sections My screenings, Saved notes, Want to watch, My taste, and My communities. Later modules fill these destinations; disabled features must not appear as working empty tools. Account settings include contact preferences, display name, sign-out, and deletion request.

**Acceptance.** Follow/unfollow updates the feed; deleting a link cannot break a profile; blocked or unpublished content never appears in discovery. Empty supply offers browse-all/change-access controls. Onboarding can be skipped. A new device recovers the account's records. Validate server-side pagination, time zones, and shared cache boundaries. Record profile views, follows, discovery-to-seat conversion, and Passport returns.

### B12 · Repertory shelf and encores

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B05, B09, B11. **Screens:** R05a–c.

**Outcome.** A curator hosts another performance using preparation they have completed.

List their past sessions with edition/runtime, note count, attendance, and unique encore interest. **Create an encore** opens copy review for authored notes, pre-show, intermissions, and promotional copy. Create an independent unpublished draft with new IDs and tracking links; no prior seats, chat, questions, or finances carry over. Copied notes start unarmed. Confirm edition/runtime and review timing in rehearsal before launch.

An attendee can request an encore and select optional time windows. One request per person/source session counts toward interest. A published encore can notify those who opted in. Preserve the original recap's fired content when the copy changes. Show missing assets and invalid offsets.

**Acceptance.** Mutating or deleting the duplicate cannot corrupt the source. A changed runtime invalidates relevant note marks. Duplicate-request retries do not inflate interest. An encore purchase uses B06 and no old seat implies access. Measure preparation time, request-to-attendance, and repeat curator hosting.

### B13 · Seasons and multi-session checkout

**Phase:** P3. **Owner:** Michael/agents with payment review. **Dependencies:** B06, B11. **Screens:** R01a–b, R02a–c.

**Outcome.** A curator sells a connected programme and viewers can reserve the run or chosen nights.

Create a season with title, premise, ordered sessions, and optional connection text. One curator owns all included sessions. Permit incomplete drafts; published bookable seasons require dated published sessions with non-overlapping runtime windows. Display actual calendar order to viewers. A prior or sold-out screening stays visible with its state but is not purchasable. Reserving remaining sessions excludes existing seats.

Charge the sum of selected session prices with no automatic renewal, subscription, or hidden discount. Follow B06 multi-line inventory and refund semantics. Calendar export uses stable event IDs and explicit time zones. Added sessions require a new purchase; date changes trigger reservation notices. Cancelled sessions refund their allocated amounts under policy. Show per-night attendance and continued participation across the season.

**Acceptance.** Test mixed existing/new/sold-out selections, a last-seat race on one line, a payment retry, cancellation of one night, and a viewer joining mid-season. The customer reviews a changed total before payment. No repeated charge or subscription exists. Record season views, selected/paid nights, and actual subsequent attendance.

### B14 · Persistent friend groups and next-night plans

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B06, B11. **Screens:** R03a–c.

**Outcome.** A viewer makes a plan with friends and carries the group to another curator's screening.

From confirmation or detail, create a named group and invite through a revocable random link. The organiser chooses open-link or approval-required membership. An unjoined recipient sees inviter/name/proposal without the roster. They may signal interest with verified email; persistent membership requires an account. Joined members see Interested, Reserved, and Can't make it as distinct states. Purchase remains per person.

Any member can propose a dated screening; one proposal stays active. Members respond and book through B06. The organiser closes/replaces a proposal, approves joins, revokes links, or removes a member. A member can mute/leave. If the organiser leaves, require transfer to a consenting member or archive the group. No address-book upload or group chat. Show group plans in Passport and a compact Lobby summary; defer live-film notifications.

**Acceptance.** An invite grants no seat and exposes no private roster. Revoked links fail. Removed members lose group access. Accepting and retrying an invite produces one membership. A sold-out proposal cannot imply a held seat. Test organiser exit and cross-curator proposal. Measure invitation acceptance, booked pairs/groups, and second attendance.

### B15 · Programming ballots

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B09, B11; foyer eligibility activates after B19. **Screens:** R04a–c.

**Outcome.** A curator hears from eligible viewers before choosing a programme.

Create one active ballot with two or three film options, reasons, deadline, and eligibility: attendees of a named session or joined foyer members. One verified person may vote once, change their choice before close, and add a short argument. Show counts after voting. Result notifications require opt-in. A submitted vote is not a purchase or demand guarantee.

At close the curator selects a winner. Require an explanation for a tie resolution or choosing another film. Convert to a session draft; show **Chosen; date to follow** until publication. Material option changes after voting require a new ballot. Preserve closed results and publish a contributor's name only with consent.

**Acceptance.** Reject ineligible or duplicate direct votes, changes after deadline, and a second active ballot. Retry closing without duplicate announcements. Cover no votes, tie, cancelled ballot, and a winner without a date. Test sign-in merging without double vote count. Measure vote-to-booking and attendance rather than vote count alone.

### B16 · Regulars notebook and recognition controls

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B09, B11. **Screens:** R06a–c, On air drawer.

**Outcome.** A host can remember a returning attendee who has agreed to recognition.

Recognition defaults off per viewer/curator. The viewer can grant/revoke it in Passport. Explain that the host can see that viewer's attendance and contributions to their own screenings and keep a private hosting note. Show the host a returning-attendee list for the upcoming session, count of first-timers, and drill-down with links to eligible prior contributions. Permit a short private note and phone lookup.

A curator cannot read another curator's notebook or the viewer's imported taste, groups, or external film history. Revocation removes access to linked history and notebook text, including cached copies through application invalidation. Operational payment/attendance records retain their separate access rules; recognition consent does not erase invoices. No automated public greetings or public regular ranking.

**Acceptance.** Default-off viewers are absent from named recognition lists. Grant exposes only the permitted relationship. Revocation while the host has a page open clears it on refresh/invalidation and denies subsequent API reads. Cross-curator access fails. Test display-name changes. Measure optional use and return without publishing individual attendance in analytics.

### B17 · Audience commissioning

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B11, B15 shared eligibility/identity utilities. **Screens:** R07a–c.

**Outcome.** A curator tests a proposed film or programme against an interest threshold before preparing it.

Create a pitch, intended price, unique-person threshold, deadline, and up to three candidate dates. Viewers express interest and select any workable dates through a verified identity. They may edit or withdraw. The public count shows unique interested people; date choices remain private to the host. No deposit, seat, or charge occurs.

At threshold or deadline the host confirms a date, extends with notice, or closes. Show date splits rather than assuming all interested people can attend one date. Confirmation creates a draft; publication opens ordinary checkout. A film/price/date change appears in the subsequent invitation. A season proposal links to B13 when confirmed.

**Acceptance.** Concurrent/repeated interest remains one person. Withdrawal updates totals. Threshold achievement does not publish or charge. Cover no interest, split dates, deadline expiry, extension, cancellation, and publication. Record interest-to-confirmation, booking, and attendance separately.

### B18 · Watchlist, film requests, and screening alerts

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B11; B15/B17 for optional curator actions. **Screens:** R08a–c.

**Outcome.** A viewer hears when a film they want receives a hosted screening.

Search canonical films and add Want to watch. Offer separate actions for **Tell me when someone hosts this** with followed/all-curator scope, and **Ask this curator to host it**. Store consent and unique demand separately. Show **No screening scheduled** before a match, without implying a commitment. Curators see aggregate film demand and can create a ballot, proposal, or session.

On publication, match film identity, alert scope, and access preferences; show current date, price, host, and known region/service access. Deduplicate a notice that also matches a follow or group plan. Suppress a booking prompt after reservation and recheck consent when sending. Changing services or including rentals updates eligibility. Imported watchlists create no alerts without a separate action.

**Acceptance.** Same-title different-year films do not cross-match. Withdrawn requests and muted alerts stop future dispatch. A retry produces one notice per person/session/purpose. Cancelled sessions no longer offer checkout. Sparse or unknown access offers a clear check-source action. Measure alert-to-reservation and attendance.

### B19 · Curator foyer and moderation

**Phase:** P3. **Owner:** Michael/agents. **Dependencies:** B07 moderation foundation, B11. **Screens:** R09a–c.

**Outcome.** A community has a place to talk between screenings without requiring the host to maintain another live broadcast.

One foyer per curator, with a description, text threads/replies, one pinned item, and next programme. The host chooses public preview or member-only reading. Account membership permits replies; following and joining remain separate actions. Host can post/close a prompt, pin a ballot/proposal/session, remove a post, mute/remove a member, and escalate a report. Members can report, block, mute, and leave.

Support digest, curator-post-only, and muted delivery. Default to an email digest only with consent; otherwise in-app updates. Do not email per reply. Keep notifications out of the live Room. At Lights up, the host chooses an external handoff or foyer destination; Projector does not force an outside community into the foyer. No DMs, voice rooms, subchannels, or paid tiers.

**Acceptance.** A private foyer cannot leak through public previews or realtime. Removed/blocked content stays hidden after pagination and reconnect. Closed threads reject direct replies. Leaving stops membership notices. Apply B07 rate limits, report queue, and safe text rendering. Measure participation-to-screening return and curator moderation effort.

### B20 · Letterboxd import, taste training, and curator ranking

**Phase:** P3. **Owner:** Michael/agents with import/privacy review. **Dependencies:** B11, B18. **Screens:** R10a–d, R11a–d, R12a–b. **Build slices:** B20a manual training; B20b import; B20c ranking.

**Outcome.** A viewer receives relevant curator suggestions, with editable inputs whether or not they use Letterboxd.

**B20a.** Offer Import Letterboxd, Pick films, or Skip. Search a varied catalogue and mark Love it, Like it, Not for me, Want to watch, or Haven't seen it. Suggest five to ten opinions with no minimum. Let viewers undo and find other titles. Imported-title review also offers **Someone else watched this**, which excludes that record from taste signals. Ask optional hosting preferences: craft/history interests, quiet notes/discussion, familiar films/discovery, plus separate time availability. A guest can try picks; saving requires an account. Never treat an unseen film or inconvenient time as dislike.

**B20b.** Guide the viewer to export through Letterboxd website Settings, download a ZIP in their phone browser, return, and upload through Files/Downloads. Support recognised individual CSV files if the OS extracts the archive. Validate against a current consented export fixture; do not assume inbound-import documentation describes exported columns. Accept selected ratings, watched history, diary/rewatches, and watchlist. Exclude review prose, private lists, deleted-content folders, account settings, and unrelated files.

Review category counts, duplicates, and unmatched films before commit. Match stable identifiers through the approved catalogue where available, then title/year with an ambiguity choice. Retain unresolved entries as skipped, never guessed matches. Preserve rating scale/source and diary date precision. Reimport deduplicates records; missing rows do not delete prior data. Explicit Projector preferences outrank imports. A source removal deletes its derived signals, leaving actual Projector attendance and explicit picks. Initial limits: 25 MB upload, 100 MB expanded archive, 100,000 recognised rows; validate these defaults against fixtures before enabling public import. Use safe archive paths and section 06 staging deletion.

**B20c.** Use a deterministic, versioned weighted ranking model with tests. Suggested v1 score: explicit film/theme affinity weight 4, hosting match 3, watchlist overlap 2, followed curator 2, positive night feedback 3; use normalised feature values and clamp each source's contribution. Imported ratings contribute to film affinity; repeated episode/watch rows cannot dominate. Scheduling/access govern session eligibility, not curator quality. Log the contributing features and derive displayed reasons from them. Do not show invented match percentages. Reserve one of each five recommendation slots for a relevant discovery curator where supply permits, and cap a curator at two cards per ten results. Treat these as tuneable defaults, not proven weights.

Controls include More/Less like this, Hide curator, Bad time, edit picks, source removal, pause behavioural learning, and reset. Pausing retains explicit preferences but stops new behavioural signals. Reset explains which signals it clears and preserves seats, attendance, and optional retained follows. A hidden curator may remain visible on the viewer's booked-session page. Cold start shows available programmes, not fake matches.

**Acceptance.** Complete manual setup and reach useful results with five curators and no import. Test corrupt/oversized/archive-traversal files, interrupted upload, unsupported rows, duplicate import, partial match, cancellation, and source removal. Test film disliked/night liked, shared-profile correction **Someone else watched this**, and bad-time feedback. Imported viewing never creates a Projector attendance. Explain ranking from actual features and demonstrate hidden-curator suppression. Complete download/upload on iPhone and Android before claiming mobile import support. Record setup/import completion, recommendation version, follows, and subsequent attendance.

### B21 · Younify streaming-history connection · provisional

**Phase:** P3 provisional extension. **Owner:** Michael/agents with integration/identity review. **Dependencies:** B02, B11, B20; provider keys and verified browser flow. **Screens:** proposed Y01 connect services, Y02 browser handoff, Y03 return/status, Y04 review/manage connection. These are new requirements, not existing wireframe artboards.

**Outcome.** A viewer can connect a streaming history source from the React PWA, complete provider steps in a browser, and return to review taste inputs. Michael approved this provisional approach; browser linking and a return hook remain integration assumptions until tested with Younify.

**Y01, CTA.** In My taste, offer **Connect streaming services** with supported services supplied by a verified capability list. Require a saved Projector account to attach a durable connection. Explain the data requested and offer Letterboxd import or manual picks as alternatives. Do not imply that choosing a streamer grants Projector film playback access.

**Y02, browser handoff.** The Projector backend creates a short-lived linking attempt tied to person, selected service, random state nonce, allowed return destination, and expiry. The frontend opens Younify's supported hosted/browser flow through a user-invoked action. Preserve the originating route. If the provider requires an external browser, show **Continue in browser** and **I've finished linking**. On a regular mobile browser, the same tab or a new tab may suffice; do not promise that a PWA can force a particular external browser or automatically reopen its installed window.

**Y03, callback and hook.** Use the provider's documented mechanism: an authenticated callback or verified server webhook reports completion to the backend; a redirect only brings the user back. Validate the state, expiry, person binding, and callback signature or token exchange as applicable. If Younify offers neither a suitable completion signal nor a verified status query, record the integration as blocked rather than fabricating a hook. Use PKCE if the chosen flow is OAuth and supports/requires it; do not describe Younify as OAuth without its contract.

The return URL is a Projector HTTPS route with an allowlisted destination. It may open in a browser rather than the installed PWA. Show **Return to Projector** and a status page that either surface can read from the server. Do not put streamer credentials, provider secrets, or long-lived access tokens into URLs or browser storage. Reauthentication in a different browser must prove the same Projector account before attaching data. If the viewer returns before the webhook, show **Connection pending** and poll a rate-limited status endpoint; never show success from a `success=true` query parameter alone.

**Y04, data review.** After verified connection, fetch available history/ratings/watchlist through the server adapter. Show service, selected profile where supported, import counts, unavailable fields, date precision, and last successful sync. Let the viewer deselect categories and remove titles marked **Someone else watched this** before applying taste signals. Watched means familiarity; ratings provide preference; episodes remain outside film recommendations. Reuse B20 matching, source provenance, deduplication, explicit overrides, and imported-source removal. Connecting a streamer does not opt the viewer into film alerts.

**States and management.** Not connected, connecting, browser action required, pending verification, syncing, review ready, connected, reauthentication required, provider unavailable, denied/cancelled, and disconnected. Closing the browser, blocking a popup, expiring the attempt, or receiving a duplicate callback leaves a recoverable status. Retry creates or reuses an appropriate attempt without duplicating source records. Disconnect revokes provider access where supported, stops scheduled refresh, and offers removal of imported signals. Keep Projector seats and direct preferences intact. The backend, not a sleeping PWA, schedules any approved future sync.

**Operations/data.** `createConnectionAttempt`, `verifyConnectionReturn`, `receiveProviderCallback`, `getConnectionStatus`, `syncConnection`, `commitSelectedSignals`, `disconnectConnection`. Store attempt ID/person/service/state hash/expiry/status, provider account reference and encrypted server credentials, last sync/error, consent version, and import provenance. Give the viewer a status endpoint restricted to their person ID. Provider event IDs and batch keys enforce idempotency. Callback bodies and tokens do not enter analytics logs.

**Activation gate.** Confirm Younify's supported hosted/browser authentication, callback or status contract, profile handling, credential model, data permissions, pricing, refresh, revocation, and regional service coverage. Test with a real consented account on iPhone Safari and Android Chrome, from both browser and installed PWA. Demonstrate linking without a native Projector app; requiring another native app is a product decision, not an invisible implementation substitution. Scaffold the adapter and labelled test fixtures before access exists, but hide the customer CTA in production until the gate passes.

**Acceptance.** Complete CTA → browser → verified callback/status → return → selective import → useful curator suggestions. Test cancelled login, missing callback, duplicate/out-of-order webhook, state mismatch, expired attempt, wrong Projector account, reconnect, unsupported profile, and source removal. Return after app closure recovers from server state. Missing completion/history fields display as unknown. Record attempt-to-verified-connection, review completion, sync error rate, and recommendation-to-attendance without storing viewing titles in analytics. A provisional module cannot be marked accepted using only fixture callbacks.

## 09. Klaus's foundation engagement and founder handoff

### 09.1 Contract boundary

The private engineering agreement governs the planned foundation engagement. This public copy omits compensation, dates, and execution details. The scope summary below does not amend that agreement.

| SOW stage | Klaus's deliverables | Evidence Michael should receive |
|---|---|---|
| Foundation | Repo, Supabase, local/deployed environments, secrets, deploy target, PR previews, GitHub Flow, GitHub Actions linting, stack/tooling advice as skills/docs/setup prompts | Repository access, setup walkthrough, sample PR/preview, environment variable inventory without secret values |
| Data | Agreed product schema, reproducible migrations, local seed data, RLS on applicable tables, RLS tests | Schema inventory with migration IDs; clean migration/seed run; direct read/write denial tests |
| Guardrails | Test runner, deploy guard, CLAUDE.md, Playwright MCP scaffolding, cross-user integration tests | Failed build and failed test each block deploy; documented test commands; runnable browser-test example |
| Identity | Google OAuth, anonymous sessions, RLS, retention of anonymous records on sign-in | New/existing-account linking evidence and reload persistence; no cross-user ownership leak |
| During engagement | Review of commits made during the engagement | Reviewed PR/commit references and unresolved findings |

The SOW does not commit Klaus to the session clock/harness, firing engine, chat/presence, intermission, Stripe/ticketing/refunds, financial ledger, paid pilot operations, or P3 features. It also does not establish ongoing review after the engagement ends. These remain product requirements owned by Michael/agents or a later engineering engagement. Mark the responsible reviewer before releasing their high-risk paths.

### 09.2 Schema inventory at the boundary

The SOW says “database schema per the product specification.” This rewrite expands the product beyond the initial setup brief. Before Klaus starts Data, Michael and Klaus should pin the spec revision and table inventory covered by his estimate. Do not treat the full eventual table list as an unpriced contract amendment.

Proposed foundation inventory: people/auth ownership, curator grants/profiles, canonical films/editions, sessions, Liner Notes, seats, and minimal guest-owned fixtures needed for the four acceptance criteria. Note that seed seats are fixtures and do not represent a payment implementation. If Klaus includes more tables, list them explicitly in the handoff manifest. Michael owns migrations for records outside that accepted inventory. Those migrations must follow Klaus's RLS, naming, and test conventions.

The foundation can establish ownership patterns before designing each later feature's schema. Do not create permissive catch-all tables or disable RLS to let agents move faster. A table's absence is a named dependency for a later module, not permission for an agent to assume the table exists.

### 09.3 Handoff manifest

Complete this table from the actual delivery; these entries are operational placeholders, separate from the design placeholders.

| Item | Recorded value |
|---|---|
| Accepted foundation spec revision and table inventory | `[HANDOFF: revision and inventory path]` |
| Repository and default branch | `[HANDOFF: repo URL and branch]` |
| Local setup and seed commands | `[HANDOFF: setup document path]` |
| Supabase environments and migration baseline | `[HANDOFF: project references, no secret values]` |
| Preview/staging/production deployment mapping | `[HANDOFF: deployment document path]` |
| Test, build, and RLS test commands | `[HANDOFF: package scripts/document path]` |
| Agent rules, supplied skills, setup prompts | `[HANDOFF: paths]` |
| Identity-linking operation and tests | `[HANDOFF: code/test paths]` |
| Playwright MCP setup and example | `[HANDOFF: configuration/document path]` |
| Known limitations and open findings | `[HANDOFF: issue list]` |
| Ownership/access transfer and support contact | `[HANDOFF: responsible accounts/contact path]` |
| Acceptance evidence and delivery commit | `[HANDOFF: test run and commit]` |

### 09.4 Handoff gate before Michael builds P1

Demonstrate the SOW's four acceptance criteria: sign in/create session/reload; cross-user read and write denial for sessions/notes/seats; anonymous-to-authenticated continuity; migrations from a clean environment without manual steps. Record them separately so a working sign-in screen cannot stand in for the entire delivery.

Then Michael runs the setup and creates a small branch using the supplied prompts. He can see a preview, intentionally fail a test, correct it, and find the policy/test governing an owned record. This walkthrough is a recommended handoff exercise, not an added contractual acceptance criterion. Missing documentation should be recorded before Michael relies on the base. Preserve Klaus's guardrails when later agents work; changes to them require an explicit rationale and review.

## 10. Future roadmap and integration gates

### 10.1 Approved MVP versus experiments

B01–B20 define the committed product scope across P0–P3; B21 adds the user-approved provisional Younify path. The eight approved retention additions map as follows: seasons B13, friend groups B14, ballots B15, repertory B12, regulars B16, commissioning B17, hosted-film requests B18, and foyer B19. Taste Passport/discovery spans B11/B20; Letterboxd upload is B20b. PWA behaviour applies throughout.

The separate feature roadmap describes these fourteen experiments. Do not build them from this spec without a named request and an experiment/implementation brief.

| ID | Experiment | Reuse before adding software |
|---|---|---|
| F01 | Curator's guest seat | B03 notes and B06 contribution prompt; host reviews before publishing |
| F02 | You asked, I found it | B09 recap question follow-up |
| F03 | A film I changed my mind about | B13 season and discussion prompt |
| F04 | Curator relay | B10 attribution and B11 profiles |
| F05 | First-timers' club | B13 beginner-friendly season |
| F06 | Bring your sceptic | B14 friend invitations |
| F07 | The room's alternate ending | B19 interpretation prompt after the film |
| F08 | Audience-made season zine | B09 notes and consented contributions |
| F09 | The same film, two minds | Linked separate sessions; cross-curator season checkout needs new design |
| F10 | Missed-night rescue | Manual approved transfer/refund policy before automation |
| F11 | Curator office hours | Foyer text discussion or external destination |
| F12 | Programme a night for us | Group-initiated brief; differs from B17 curator-initiated proposal |
| F13 | Secret screening | Confirm reveal/access/refund rules before taking money |
| F14 | Trust-me seat | Interest in a recurring date before subscriptions |

Research agent, expert contribution outreach, quote checking, timestamp inference, telestrator, and intermission video each need a separate technical/UX brief and quality gate. Sponsorship and enterprise licensing need commercial requirements, roles, attribution, and operations before implementation. TV-series support is a future content expansion; B20 must filter imported TV episodes out of film-only recommendations without pretending they are films.

### 10.2 Import and connection candidates

Netflix documents per-profile CSV viewing export. Trakt documents browser OAuth and access to user-authorised history. Both are candidates beyond B20b; neither is part of Klaus's foundation or a committed additional importer. Test current data shapes, account requirements, refresh behaviour, revocation, and platform returns before approval. [Netflix export](https://help.netflix.com/en/node/101917) · [Trakt authorisation](https://docs.trakt.tv/docs/authentication-oauth)

Letterboxd documents a website account export; API access is request-only and its policy excludes recommendation projects. B20b therefore uses user-provided files and does not depend on profile scraping, write-back, or continuous sync. Recheck the policy before considering a partnership. [Letterboxd export](https://letterboxd.zendesk.com/hc/en-us/articles/15179196880911-Can-I-get-a-copy-of-my-account-data) · [Letterboxd API](https://letterboxd.com/api-beta/)

### 10.3 Younify and the React PWA · provisional B21

Evidence checked on 6 September 2026: Trakt documented Lite as a PWA consuming synchronised history while requiring mobile apps to change tracking connections. Cineverse announced Younify integration for its cineSearch web product. These are relevant precedents, not verification that Projector can perform the whole connection in a browser. Younify's public SDK list names native platforms and React Native; it does not establish React web compatibility.

Before activating B21, obtain a supported browser or hosted-linking demo and test Safari, Chrome, installed-PWA return, profile choice, expired connection, reauthentication, and revocation without requiring a native Projector app. Confirm per-service history/ratings coverage, date accuracy, allowed uses, pricing, and support. Do not expose a working-looking **Connect streamer** action until that flow exists. The intended user flow is CTA → browser linking → verified completion hook → Projector return. No outreach or authenticated provider test occurred during this specification work.

[Trakt PWA precedent](https://forums.trakt.tv/t/try-out-trakt-lite-your-new-go-to-for-a-better-faster-and-simpler-experience/47712) · [Cineverse announcement](https://s202.q4cdn.com/484194886/files/doc_news/Cineverse-Enhances-Content-Recommendations-via-Younify-Connect-Integration-into-cineSearch-Platform-2024.pdf) · [Younify SDK](https://www.younify.tv/product/developer-sdk/)

## 11. Build record, traceability, and release checklist

### 11.1 Module record

Allowed status: not-assessed, not-started, in-progress, functional, design-pending, blocked, accepted. Record implementation evidence from the repository; this specification starts all modules as not-assessed because the rewrite did not inspect an app checkout. Replace not-assessed when the first build task audits the module. Acceptance applies to a specific commit and environment.

| Module | Depends on | Primary screen IDs | Status / evidence |
|---|---|---|---|
| B01 | Foundation inventory | Minimal acceptance screens | not-assessed |
| B02 | B01 | Sign-in/guest upgrade | not-assessed |
| B03 | B01–B02 | 1J①/④/⑤ | not-assessed |
| B04 | B03 | Clock/harness for 1J⑥/⑦/⑨ | not-assessed |
| B05 | B04 | 1J⑨ | not-assessed |
| B06 | B02/B03 | 1G①/② | not-assessed |
| B07 | B04/B06 | 1D①/②, 1C | not-assessed |
| B08 | B04/B07 | 1J⑥/⑦, 1D③–⑨ except telestrator, 1A/B/C | not-assessed |
| B09 | B08 | 1D⑩, 1H, basic 1I | not-assessed |
| B10a/B10b | B03 / B06–B09 | 1J⑧, operator/report references | not-assessed |
| B11 | B09/B10 | 1E/1F/1I/1K | not-assessed |
| B12 | B05/B09/B11 | R05a–c | not-assessed |
| B13 | B06/B11 | R01a–b, R02a–c | not-assessed |
| B14 | B06/B11 | R03a–c | not-assessed |
| B15 | B09/B11 | R04a–c | not-assessed |
| B16 | B09/B11 | R06a–c | not-assessed |
| B17 | B11/B15 | R07a–c | not-assessed |
| B18 | B11 | R08a–c | not-assessed |
| B19 | B07/B11 | R09a–c | not-assessed |
| B20 | B11/B18 | R10a–d, R11a–d, R12a–b | not-assessed |
| B21 provisional | B02/B11/B20; provider gate | Y01–Y04 | not-assessed |

Each module completion entry adds commit, migrations, test commands/results, design revision/screenshots, instrumentation, known issues, and reviewer. Keep detailed logs in the repository and link them here. Do not store secrets, customer imports, or private chat in build evidence.

### 11.2 Product measurement definitions

| Metric | Definition |
|---|---|
| Confirmed seats | Unique session/person entitlements from verified successful payment, reported with refunds apart |
| Attendance | At least one authorised room entry during live/intermission; report early departures and accumulated foreground presence separately |
| Reservation show rate | Unique paid attendees / eligible confirmed seats, with cancellation/refund exclusions documented |
| Second attendance | First-time attendees with another hosted session within 30 days / first-time attendees with a full 30-day observation window |
| Same/cross-curator return | Split second attendance by whether the next host is the same curator |
| Curator continuation | Curators hosting a fourth eligible session / curators who completed the three founding screenings |
| Preparation effort | Curator-reported preparation minutes plus labelled observed editing time; do not equate idle browser time with work |
| Link conversion | Attributed confirmed reservations / eligible tracked visits under the versioned model; show raw counts |
| Film/night satisfaction | Separate optional ratings with response counts; never merge them into a curator score |
| Reliability | Note render timing among reporting active clients, recovery success, failed commands, missing telemetry; unknown is not zero |
| Curator economics | Gross, refunds, fees, accrued payable, paid transfers, and balance; founding/standard periods separate |

The platform cannot measure external-film completion. Call any room-presence-derived proxy exactly that, and never present it as verified film watch-through. Report small cohorts and missing observations. Select retention success thresholds after baseline evidence rather than inventing investor-ready numbers.

### 11.3 Release checklist

- [ ] Required phase modules accepted against a commit, with no unresolved money/identity/clock/access failure.
- [ ] Named reviewer for post-foundation high-risk code; do not assume Klaus provides continuing review.
- [ ] Design contract and relevant screen references complete for public UI.
- [ ] Real iPhone/Android browser and installed-PWA critical journeys checked.
- [ ] Currency, founding terms, fee allocation, refund rules, and contact/support copy approved.
- [ ] Permissions, secrets, uploads, moderation, and notification suppression tests pass.
- [ ] Restore/rollback and failed-job replay tested in staging; active-room update behaviour checked.
- [ ] Pilot room cap enforced and load evidence recorded before paid dates open.
- [ ] Provider outage, abandoned host, failed payment/refund, and lost-seat runbooks available to operators.
- [ ] Feature flags hide unimplemented integrations/experiments; customer-facing data comes from production records.

## 12. Decision register

Only DESIGN and HANDOFF tokens are intentional fill-in placeholders. The decisions below have owners and explicit defaults or release boundaries; they must not become silent assumptions in generated code.

| ID | Decision | Default / required action | Owner / gate |
|---|---|---|---|
| D00 | Klaus's schema boundary | Pin exact table inventory and this spec revision; do not expand fixed-fee scope through later modules | Michael + Klaus, before SOW Data |
| D01 | Visual direction | Fill section 03; nonvisual work may continue | Michael, before visual acceptance |
| D02 | Live commercial terms | USD 0.99 and 100% first three/70% thereafter are the product inputs; confirm fee basis, founding eligibility, cancellations/reschedules/no-shows, and rounding. Test with fixtures until approved | Michael, before live checkout |
| D03 | Data/content policies | Confirm retention periods, account deletion treatment, attendee consent, moderation escalation, rights/permission for supplied stills/clips, and launch availability | Michael with appropriate advisers, before public launch |
| D04 | Film catalogue source | Manual film/edition/access entry for pilot. Approve metadata source/licence and mapping fixtures before B20 matching | Michael, before import/ranking release |
| D05 | Clock scheduler and reviewer | Choose durable scheduler through B04 proof; appoint reviewer beyond Klaus's SOW | Michael + responsible engineer, before live use |
| D06 | Deployment and jobs | Supabase plus React/TypeScript, Stripe; Vercel or equivalent selected in B01. Document worker execution/retry mechanism | Klaus for foundation; later engineer for jobs |
| D07 | Expanded-MVP calendar | Estimate B03–B20 after foundation handoff; old pilot dates are not commitments in this rewrite | Michael, before new schedule |
| D08 | External connections | Netflix/Trakt remain P4 candidates. Younify B21 is provisionally approved, pending a verified browser/callback contract; no base-MVP launch dependency | Michael, before B21 activation |
| D09 | Auth beyond foundation | Google and anonymous are contracted. Add email seat recovery in B06; Apple login optional after provider setup and testing | Michael, relevant module |
| D10 | Larger rooms and enterprise | Cap pilot at tested capacity; larger rooms, org roles, SSO, sponsorship and automatic payouts require new acceptance scope | Michael + engineer, P4 |

## 13. Source and change record

This is a full replacement of the prior accumulated spec, organised for section-by-section agent builds. It uses the wireframe guide for the screening and retention flows; the engineer brief for the reliability problem; the supplied Klaus SOW for the actual foundation boundary; the investor deck for commercial hypotheses; and the feature roadmap for committed versus deferred scope.

Source dates: engineer brief 2 September 2026; expanded wireframe guide/roadmap 6 September 2026; draft investor deck supplied in this project; private engineering agreement supplied for scope alignment. The SOW takes precedence over the broader engineer brief for contractor responsibilities. The new spec does not amend the SOW or claim execution.

The published wireframe URL could not be retrieved by the research tool during this rewrite. Screen mapping comes from the supplied local wireframe guide; no visual inspection of live artboards is claimed. Register R01–R12 and the new operator/acceptance screens in the selected design references before visual build. Current external-provider findings are dated research inputs and must be revalidated when their integrations are selected.

Preserve a pre-rewrite copy before replacing the canonical `Projector-Product-Spec.md`. Update companion roadmap/wireframe references to the stable Bxx IDs, section 03 design contract, section 09 foundation handoff, and section 10 roadmap. Preserve the original investor draft and engineering agreements as historical sources. Do not copy pitch rhetoric, speculative revenue, or unverified partnership claims into acceptance criteria.
