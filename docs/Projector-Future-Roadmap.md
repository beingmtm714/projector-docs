# Projector: Feature Roadmap

**6 September 2026 · Approved MVP, integration investigations, and deferred experiments · No delivery dates**

Michael approved the first six retention ideas and the two closing additions for the expanded MVP. `Projector-Wireframe-Guide-v2.md` covers those eight features, mobile Letterboxd file import, and Taste Passport personalisation. This document captures the other fourteen ideas from the brainstorm. The approved MVP inventory below records the user-approved scope. Integration candidates and F01–F14 remain uncommitted; none carries a proven retention benefit.

## Approved build scope and phases

`Projector-Product-Spec.md` version 3 is the build source of truth. Use its stable module IDs to prompt an agent. P0 is Klaus's foundation under the supplied SOW; P1 is curator authoring/rehearsal; P2 is the paid pilot; P3 completes the expanded retention MVP. The SOW does not include the later clock, payments, or retention builds. Section 09 of the spec records the handoff, and section 03 holds the design placeholders.

| Feature | Phase/module | Wireframe IDs |
|---|---|---|
| Repository, data, guardrails, Google/anonymous identity | P0, B01–B02; Klaus's agreed foundation | Acceptance screens |
| Authoring, clock/harness, rehearsal, promo preparation | P1, B03–B05/B10a; founder/agents | 1J①/④/⑤/⑧/⑨ |
| Paid live screening, recap, operations, manual payouts | P2, B06–B09/B10b; founder/agents | 1G, 1D, 1A/B/C, 1H |
| Profiles, Marquee, Passport foundation | P3, B11 | 1E/1F/1I/1K |
| Repertory and encores | P3, B12 | R05 |
| Curator seasons | P3, B13 | R01–R02 |
| Persistent friend groups | P3, B14 | R03 |
| Programming ballots | P3, B15 | R04 |
| Opt-in regulars notebook | P3, B16 | R06 |
| Audience commissioning | P3, B17 | R07 |
| Film requests and screening alerts | P3, B18 | R08 |
| Curator foyer | P3, B19 | R09 |
| Taste training, Letterboxd import, curator ranking | P3, B20a–c | R10–R12 |
| Younify streaming-history browser handoff | P3 provisional, B21; provider validation before activation | Proposed Y01–Y04 |

The React PWA is the audience platform across phases. Approval establishes intended scope, not implementation status or a delivery date. The base expanded MVP does not depend on B21 activation.

## Integration candidates, not committed build scope

| Candidate | Evidence and next decision |
|---|---|
| Netflix CSV import | Netflix documents a per-profile viewing-activity download. Validate a fixture, mobile download/upload, title matching, and film-only filtering before approving the adapter. |
| Trakt authorisation | Trakt documents browser OAuth. Test a read of consented history, current API terms and limits, source availability, revocation, and account-level subscription requirements. A Trakt connection does not mean a viewer has connected their streamers. |


## Provisional Younify module B21 · evidence checked 6 September 2026

**A documented PWA precedent exists.** Trakt's February 2025 announcement describes Trakt Lite as an installable PWA and says Younify tracking continues to supply it with history. The same announcement requires mobile apps for tracking changes. This demonstrates a PWA consuming synchronised data with a separate mobile setup step. It does not establish a browser-only Younify account-linking flow. The team has not tested the current signed-in experience. [Trakt Lite announcement](https://forums.trakt.tv/t/try-out-trakt-lite-your-new-go-to-for-a-better-faster-and-simpler-experience/47712)

**A web-product lead exists.** Cineverse announced cineSearch on the web in October 2024 with streaming-account connection and a mobile app still planned. Its December 2024 announcement names Younify Connect for viewing-history integration. These announcements justify asking Younify about cineSearch's web implementation. They do not establish that cineSearch is a PWA or that its current linking flow stays in a browser. The public cineSearch site remains accessible; no authenticated account connection was tested. [Public preview announcement](https://s202.q4cdn.com/484194886/files/doc_news/Cineverse-Launches-cineSearch-For-Public-Preview-Revolutionizing-Content-Discovery-2024.pdf) · [Younify integration announcement](https://s202.q4cdn.com/484194886/files/doc_news/Cineverse-Enhances-Content-Recommendations-via-Younify-Connect-Integration-into-cineSearch-Platform-2024.pdf)

Younify's public SDK list names iOS, Android, React Native, and .NET MAUI. A React Native SDK does not establish React browser compatibility. Its privacy policy mentions partner websites, but that description does not document browser authentication. Search results for a Younify e-commerce agency concern a different company and provide no evidence about this SDK. [Developer SDK](https://www.younify.tv/product/developer-sdk/) · [Privacy policy](https://www.younify.tv/privacy/)

Michael approved the provisional CTA → browser linking → verified completion hook → return flow. Before activating B21, obtain a working browser demo and confirm: supported Safari/Chrome and installed-PWA return flows; whether a separate native app is required; profile selection and reauthentication; historical coverage and missing dates by service; consent and source removal; commercial cost and support obligations. Request a named browser implementation, with cineSearch as the concrete lead. No provider contact or account connection has occurred during this documentation work.

[Netflix export instructions](https://help.netflix.com/en/node/101917) · [Trakt browser authorisation](https://docs.trakt.tv/docs/authentication-oauth)


## Roadmap boundaries

The expanded MVP includes seasons, friend groups, programming ballots, repertory duplication, the regulars notebook, audience commissioning, hosted-film alerts, and curator foyers. Use those foundations to test the ideas below with a small programme before adding infrastructure. The order groups experiments by the work they need; it does not promise a calendar.

Keep guest booking, the shared film clock, quiet viewing, and the curator's choice of external community destination. The team should compare repeat attendance and curator effort with the cost of each addition. Small audiences can offer evidence through interviews and observed behaviour; avoid assigning causal lift to a handful of self-selected participants.

## First experiments: use the expanded MVP foundations

### F01 · The curator's guest seat

**Experience.** An attendee submits one Liner Note for an upcoming screening. The curator reviews the text, attribution, source, and timestamp before adding it to the queue. The contributor chooses whether to receive a public credit.

**Retention hypothesis.** An audience member returns to see their contribution, and the curator learns who can contribute useful knowledge.

**First test.** Invite one attendee through the existing pre-screening contribution prompt. The curator adds the approved note by hand. Build a contributor submission/review state only after repeated use.

**Dependencies and limits.** Note editor, contribution prompt, and consent for credit. The curator keeps publishing control. Track contributor return, audience response, and review time. Broad co-curator editing remains a separate decision.

### F02 · “You asked, I found it”

**Experience.** A curator returns to an unanswered question after a screening and adds an answer to the recap. The questioner can receive a notice and reply in the foyer.

**Retention hypothesis.** The attendee has a reason to reopen Projector and sees that the curator values their question.

**First test.** Let the curator mark a question **I'll follow up**, then post one answer with an optional related screening link. Avoid imposing a response-time promise.

**Dependencies and limits.** Recap questions and notification preferences. Track follow-up views, replies, next attendance, and time spent answering.

### F03 · A film I changed my mind about

**Experience.** A curator programmes a pair of films, or a film and a later rewatch, around a change in their own judgment. Attendees discuss how their responses changed between nights.

**Retention hypothesis.** The curator's personal account gives viewers a reason to complete the pair.

**First test.** Use SeasonStudio and a shared discussion prompt. No custom feature required until curators request a reusable format.

**Dependencies and limits.** Seasons, recaps, foyer. Track attendance across both nights and preparation effort.

### F04 · Curator relay

**Experience.** At the end of a programme, one curator introduces another curator's next screening through a short personal recommendation. The recipient sees who made the introduction.

**Retention hypothesis.** Viewers try a second curator because a trusted host recommended them; curators gain audience from peers.

**First test.** Add a curator-selected recommendation to a recap with an attributed link. Preserve the host's own next-screening booking option.

**Dependencies and limits.** Curator profiles and attribution. Both curators agree to the introduction. Track cross-curator booking, attendance, and subsequent returns; referral compensation needs a separate proposal.

### F05 · First-timers' club

**Experience.** A curator programmes films many viewers feel they should have seen, with beginner-friendly introductions and explicit spoiler expectations. Viewers can arrive without prior knowledge.

**Retention hypothesis.** Beginners return to a group where they can ask basic questions.

**First test.** Run a named three-film season with a welcoming pre-show and spoiler guidance. Use optional self-identification as a first-time viewer.

**Dependencies and limits.** Seasons and foyer moderation. Track first-to-second attendance and ask viewers whether the conversation felt accessible.

### F06 · Bring your sceptic

**Experience.** A curator programmes an introduction to a genre or style for viewers who tend to avoid it. Regulars invite a friend through the existing group flow.

**Retention hypothesis.** The invitation gives friends a shared reason to attend and an occasion to compare reactions.

**First test.** Run “Horror for people who avoid horror” or another curator-chosen programme. Ask both viewers about the night without requiring them to change their opinions.

**Dependencies and limits.** Group invitations, film access information, and relevant content information. Track invited-friend attendance and whether the pair books again.

### F07 · The room's alternate ending

**Experience.** After the credits, the curator asks an interpretive question. Attendees choose an answer and revisit the discussion at the next screening.

**Retention hypothesis.** A continuing conversation helps connect separate nights.

**First test.** Use a foyer prompt with a small poll. The title refers to alternative interpretations, not changing or distributing film footage.

**Dependencies and limits.** Post-film prompts and seasons. Keep interpretation separate from trivia scoring. Measure next attendance and the curator's effort to sustain the discussion.

### F08 · An audience-made season zine

**Experience.** At the end of a season, the curator collects selected attendee reflections and their own notes into a page participants can keep or share.

**Retention hypothesis.** Contributors value their shared record and may join another season.

**First test.** Assemble one page by hand from submissions people agreed to publish. Give contributors a preview and a choice of attribution.

**Dependencies and limits.** Seasons, saved notes, contribution consent. Start with text and authorised images. Track contributor participation, sharing, and return for a later programme.

## Next experiments: add targeted workflow support

### F09 · The same film, two minds

**Experience.** Two curators host separate screenings of the same film through different perspectives, such as cinematography and costume design. Attendees can reserve either or both.

**Retention hypothesis.** Viewers return to a familiar film for a different host's perspective, and curators reach each other's audiences.

**First test.** Link two existing sessions from a shared programme page. Each curator retains their own room and checkout attribution.

**Dependencies and limits.** Cross-curator programme links. A joint paid bundle or shared hosting permissions requires further design; the MVP season model has one curator. Track overlap between audiences and second-curator returns.

### F10 · Missed-night rescue

**Experience.** Someone who missed a reserved screening can transfer its value to an eligible encore or another session from the same curator.

**Retention hypothesis.** A missed night becomes an opportunity for the attendee to make another plan.

**First test.** Offer a limited manual transfer to a small group of no-shows, with curator agreement and visible eligibility rules.

**Dependencies and limits.** Reservation, payment, refund, and capacity handling. Define eligibility, expiry, price differences, and abuse prevention before offering a button. Track replacement attendance and curator net proceeds; do not equate issuing credit with a retained attendee.

### F11 · Curator office hours

**Experience.** Members join a short monthly conversation about the films they have watched. A pair of curators can share the hosting work.

**Retention hypothesis.** Members maintain a relationship between film nights and discover another curator.

**First test.** Schedule one text discussion in a foyer, or link to an agreed external live session. Avoid building native audio/video for the initial test.

**Dependencies and limits.** Foyer, scheduling, moderation, and guest-host permissions if needed. Track participation followed by screening attendance, plus the hosts' preparation and moderation time.

### F12 · Programme a night for us

**Experience.** A friend group requests a programme for a birthday, long-distance gathering, or another occasion. The curator can accept, ask for more detail, or decline, and choose a public or private format with the group.

**Retention hypothesis.** Groups return to a curator who hosted a meaningful occasion; curators gain a new programming opportunity.

**First test.** Add a request form and coordinate one event by hand. This differs from MVP commissioning: a named group initiates a custom brief, while the MVP curator proposes a programme to the wider audience.

**Dependencies and limits.** Group identity, availability, pricing agreement, and private-room access if promised. Film access remains each attendee's responsibility. Track repeat group bookings and the curator's time per engagement.

## Later experiments: test trust and access before new commerce

### F13 · Secret screening

**Experience.** An audience reserves a curator-led mystery programme with agreed clues, runtime, and access requirements. The curator reveals the film with time for attendees to obtain it.

**Retention hypothesis.** Viewers return for the pleasure of trusting a particular curator's judgment.

**First test.** Use a small invited group and reveal the title before checkout. Test a paid mystery only after defining reveal timing, access failure handling, and cancellation terms.

**Dependencies and limits.** Region and service availability checks. Because Projector does not supply the film, an unrevealed title can prevent a viewer from confirming access. Do not promise that a service subscription alone guarantees access. Track repeat bookings and access-related drop-off.

### F14 · A “trust me” seat

**Experience.** A viewer reserves a recurring time with a curator before the curator announces the film. The date and host anchor the plan.

**Retention hypothesis.** Viewers commit to the curator's taste across several programmes, giving the host evidence of demand beyond a single title.

**First test.** Collect interest in one monthly slot without charging, then invite participants to book after the title reveal. Compare attendance with announced-title events.

**Dependencies and limits.** Recurring schedules, access checks, and clear reveal/cancellation rules. Automatic renewal, subscriptions, and stored payment mandates require a separate commerce design. Keep this separate from the MVP season purchase of known films and dates.

## Prior deferrals that remain outside this update

The product spec retains research-agent work, research-to-note workflow, expert consultation, automatic timestamp discovery, quote check, and telestrator tooling as deferred. The rewritten spec stages the basic recap in P2 and the profile, Marquee, and complete Passport in P3. Section 02 defines phases and section 10 defines future scope. The team must estimate a calendar after the foundation handoff; the spec does not reuse old sprint dates.

Letterboxd API-based continuous sync remains a dependency-led possibility, not a scheduled feature. The v2 guide specifies user-uploaded files and editable taste preferences. Letterboxd's current API access policy excludes recommendation projects; do not place an API connection on a committed roadmap without an approved path. [Letterboxd API policy](https://letterboxd.com/api-beta/), checked 6 September 2026.

## Decision record for an experiment

Before running an experiment, name an owner, participating curators, audience cohort, and the behaviour to observe. Record curator preparation time, first and repeat attendance, participant feedback, and any payment/access problems. After the test, choose one disposition: repeat by hand, build a small supporting flow, redesign, or stop. Add delivery dates only when the team agrees scope and capacity.
