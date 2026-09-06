# Projector: Wireframe Guide v2

**6 September 2026 · Expanded MVP definition · Wireframe requirements, not a record of shipped features**

This version retains the original screening journey and adds eight retention features plus Taste Passport personalisation. The original guide remains intact in `Projector-Wireframe-Guide.md`. The designer can use this document to extend the boards; the engineer can use the behaviours and review checks to scope the build. Product spec version 3 now maps these requirements to stable build modules B01–B21 and governs phase placement. This document update does not change HTML wireframes, application code, the investor deck, or the delivery calendar.

## Platform requirement

The audience product is a React PWA. Support mobile-browser use and optional home-screen installation with the same account and bookings. Installation is optional. Native iOS/Android SDKs and React Native libraries do not establish browser compatibility. Keep Letterboxd file upload and manual taste setup as the approved routes. Track Netflix import and Trakt connection as candidates. Younify browser linking is provisionally included as B21, with a provider-validation gate. See product spec section 04.6 for PWA behaviour, section 03 for design, section 09 for Klaus’s foundation handoff, and section 10 for integration evidence.

## Scope and reading order

Read the existing boards for the core evening, then the new board specifications for the additions. Where an addition changes an existing board, use the extension as the v2 requirement. New IDs beginning `R` are proposed IDs for this document. The product spec now records them; the team must register them in the visual-board source inventory before implementation; they do not refer to existing published screens.

The user approved these additions for the expanded MVP:

1. Curator seasons.
2. Persistent friend groups and shared screening invitations.
3. Programming ballots.
4. A repertory shelf with screening duplication and encores.
5. A private regulars notebook for curators, with attendee recognition preferences.
6. Audience commissioning through interest thresholds and date preferences.
7. Film requests and hosted-screening alerts inside the Taste Passport.
8. A persistent curator foyer between screenings.
9. Mobile Letterboxd file import and personal taste training, including curator recommendations.

The curator still chooses and hosts the programme. Projector ranks relevant curators and their scheduled screenings for each audience member. The team should retain the core dry-run beta as a milestone and estimate these additions before promising a revised audience launch date. The product spec’s phase table governs build scope. Research, automatic timestamping, telestrator, native intermission video, and automated social posting remain deferred; text intermission and manual sharing support the pilot. Older descriptive boards may show deferred controls; their presence does not authorise a build. Use “curator” as the domain role and default UI label; “projectionist” in older material refers to the same role.

## New board index

| Board | Proposed screens | Existing touchpoints |
|---|---|---|
| SeasonStudio | R01a editor; R01b publish review | CuratorPrep, CuratorShip, CuratorProfile |
| SeasonDetail | R02a programme; R02b reservation review; R02c confirmation | Discover, TheNight, LightsUp |
| WatchTogether | R03a invitation; R03b group; R03c propose a screening | Session detail, Lobby, LightsUp, Taste Passport |
| ProgrammeVote | R04a curator ballot; R04b audience vote; R04c result | CuratorPrep, LightsUp, recap, foyer |
| RepertoryShelf | R05a library; R05b duplicate review; R05c encore requests | CuratorPrep, CuratorQueue, dry run |
| RegularsNotebook | R06a returning attendees; R06b attendee detail; R06c recognition preferences | CuratorPrep, CuratorLive, Taste Passport |
| CommissionProgramme | R07a proposal editor; R07b interest/date selection; R07c confirmation | CuratorProfile, foyer, Marquee |
| PassportRequests | R08a watchlist; R08b request/alert controls; R08c matched screening | Taste Passport, Session detail, CuratorPrep |
| CuratorFoyer | R09a discussion; R09b prompt editor; R09c moderation | CuratorProfile, Lobby, LightsUp, recap |
| TasteSetup | R10a entry; R10b film picks; R10c hosting preferences; R10d curator preview | Discover, Taste Passport |
| LetterboxdImport | R11a mobile instructions; R11b upload; R11c review; R11d completion | TasteSetup, Taste Passport |
| MarqueeTaste | R12a personalised feed; R12b recommendation reason/feedback | Marquee, CuratorProfile, Taste Passport |

# Existing boards: the screening journey

A reader's guide to the thirteen original wireframe boards, with new retention boards detailed below. What happens on each screen, what the person on it is trying to do, and why it exists. Nothing here describes how anything looks, so all of it stays true if the whole thing is redrawn.

Screen IDs match `Projector-Product-Spec.md`. Boards are at https://beingmtm714.github.io/projector-docs/wireframes/

**The two people.** A **curator** programmes a night: picks the film, writes notes pinned to moments in it, sets a showtime, fills the room, and hosts. An **audience member** buys a seat, watches the film on their own television on whatever service they already pay for, and holds the app on their phone, where the curator's notes arrive in time with the film alongside everyone else in the room. The product never touches the film. It runs on a shared start time, which is why it works against any service and needs nobody's permission.

---

## Main · the cover

Not a screen. It states the premise and explains how to read the rest, for anyone opening the set cold.

---

# The curator's boards

## CuratorPrep · 1J① and 1J②

**What she does.** Opens the workspace for one session. The film, the showtime and the current seat count are here, and so are the three things she can do next: write her notes, record a short piece to camera about why this film tonight, and go live. Going live stays unavailable until she has at least one armed note and a showtime, so the screen enforces the minimum rather than trusting her to remember it. She also sets, once, where she will send everyone when the film ends, which most sessions never touch because it carries over.

**Her goal.** To know whether the night is ready, without opening four other screens to find out.

**Why it exists.** It is the only place that holds a session as a whole. Everything else in her tools is one task on one part of it.

**1J② is deferred.** The research agent that reads around the film, and asking other experts, are drawn on this board and are not in the first build. She writes from what she knows. Both come back after the raise, and neither is required to test whether a curator can author a night.

## CuratorNotes · 1J③ and 1J④

**What she does.** Writes one Liner Note. A note is a piece of text, sometimes with a frame from the film attached, pinned to a moment in the runtime. She types the moment as minutes and seconds. Later she will also be able to upload a frame and have the moment found for her, or describe it in words, but the typed field is the base path and is never removed.

**Her goal.** To get the note onto the right second. The whole product turns on this: a note about the costume arriving during the credits is worse than no note, so the moment matters more than the prose.

**Why it exists.** This is where a curator spends her evening. If writing forty notes is tedious, there is no product, regardless of how good the night is.

**1J③ is deferred** with the research agent. It is the screen that turns a finding from that agent into a note.

## CuratorQueue · 1J⑤ and 1J⑥

**What she does.** Sees every note for the night in the order it will fire, each with its moment and its first line. Intermissions sit in the same list, so she can read the shape of the evening in one pass. The things she wants to play before the film starts sit at the top of the same list on negative marks, half an hour of her own clips and links running down to the showtime. She reorders by changing a moment rather than dragging, because the moment is the only real ordering. Then she goes live.

**Her goal.** To see the night as a night rather than as a pile of notes, and to catch the two in a row at 41:00 and 41:12 before an audience does.

**Why it exists.** Notes written one at a time have no rhythm. This is the only screen where pacing is visible.

## CuratorLive · 1J⑦ and 1J⑨

**Two screens that look at the same clock from opposite sides.**

**The dry run (1J⑨)** lets her watch her own session play against a running clock with no audience present, at real speed or accelerated, with her notes firing exactly as someone in the room would receive them. She catches a mistimed note and fixes it without leaving the screen.

**Her goal there.** To find out the night works before anybody is watching. It is also what makes a two-week curator beta possible with nobody in the room: five curators can rehearse and give real feedback before an audience exists.

**On air (1J⑦)** is the live panel while the film runs. Chat is the main thing. She can see the session clock and how many people are seated, the next note and how long until it fires, fire one early or late when the room has drifted, and write one that was never planned. She can pause the room, call an intermission, mark up a still for everyone, and end the session.

**Her goal there.** To host. The queue does the work she planned; this screen is for everything she did not plan, which is most of what makes a night good.

## CuratorPhone · 1J⑥ and 1J⑦ on a phone

**Not new screens.** The same going-live and on-air screens, in the one place they are actually used.

**Why it exists.** Every other curator screen is desk work and can assume a laptop. Hosting cannot. She is watching the film on her television with the app in her hand, exactly like everyone in her audience, so she is an audience member with extra controls rather than an operator at a console. A control she cannot reach with a thumb in the dark is a control she does not have.

## CuratorShip · 1J⑧

**What she does.** Gets the link, and everything around it. A preview of how the screening will look when posted. A separate tracked link for each place she posts, so her Instagram bio, her story, her TikTok and her newsletter each have their own. Draft posts per channel that she rewrites in her own voice. A reminder sequence she arms once and forgets. After the screening, what each channel actually delivered.

**Her goal.** To find out which of her channels fills a room. She has never been able to learn this. Being told her newsletter converts six times better than her TikTok changes what she does next week, and nobody else in her life can tell her.

**Why it exists.** This is the first link in the entire chain and nothing on the audience side happens without it. It is also where the number the business turns on gets measured: reach to reservation, with a real denominator instead of a guess.

## CuratorProfile · 1K

**What it holds.** Who she is and what she programmes. Everything she has screened, with dates and room sizes. Everything coming up, each bookable. And things she wants people to see: a piece she wrote, a video she made, a season she programmed somewhere else.

**Her goal.** A durable place for the link in her bio. A single screening page is the right target for one night and the wrong one for a permanent link, because it expires. This does not.

**The audience's goal.** To decide whether to trust her. Thirty screenings behind someone is an argument that does not need making.

**Why it exists.** It turns the promo kit from a per-event tool into a standing funnel, and it is where a stranger who followed one link becomes someone with a seat at the next thing.

---

# The audience's boards

## Discover · 1E, 1F, 1G

**Three steps in sequence.**

**Onboarding (1E)** explains the premise, lets someone follow curators, and asks which streaming services they actually have. No account is required to go further.

**Their goal.** To understand what this is in about ten seconds. It is an unfamiliar shape and the answer to "so where do I watch the film" has to arrive immediately.

**Why the services question is not a preference survey:** a screening of a film on a service they do not have is a screening they cannot attend, so it sorts what they are shown. Service access remains the starting filter. In this version, an optional Taste Passport setup adds film preferences and curator hosting preferences to the Marquee. See TasteSetup and MarqueeTaste below.

**The Marquee (1F)** is home. What is on now, tonight, and this week, across every curator rather than only the ones they follow.

**Their goal.** To find a night worth turning up to.

**Session detail and the two prompts (1G)** is the screen a shared link opens: the film, the curator, the showtime, her pitch for why this film, whether it can be played on a service they have, and the seat. Reserving costs $0.99 and takes an email address, no account. On the way in, two optional questions: what would you add, and what do you want to ask.

**Their goal at the prompts.** To be heard before the night rather than only during it. What they add reaches the curator while she can still use it, and what they ask comes back in the wrap conversation after the credits, answered in front of the people who asked.

**Why the reservation matters more than one seat.** It leaves behind an identity and an email, which is how somebody who came for one curator finds out what every other curator is programming. Every seat is an acquisition for the whole platform, not for one screening.

## TheNight · 1D① to 1D⑨

**The evening in order, from doors to the last frame.**

**Doors, half an hour early (1D①).** Chat opens with the curator. Her other dated screenings sit here, each bookable. And a pre-show runs: her own clips and links firing on a countdown, a piece she made about this film, a review she wrote, a trailer. Nothing fires in the last two minutes. Nothing plays sound until somebody asks for it. Anything already fired stays in the conversation, so arriving late means scrolling rather than missing.

**Their goal.** To be somewhere rather than waiting. A cinema does not hold you in an empty room for thirty minutes.

**Her goal.** This is the best moment in the entire product to book a second night. Everyone present has already proved they will turn up for her, and the film has not started, so nothing is being interrupted.

**The calls (1D②), the leader (1D③) and zero (1D④).** Two reminders, then a fifteen-second shared countdown, then everyone presses play at the same moment and the session clock starts.

**Their goal.** To start the film on the same second as everyone else, without being told to concentrate. Everything the rest of the night promises depends on this one action landing together.

**Falling behind (1D⑨).** Someone who drifts is shown what they missed, how far behind they are, and given one action to catch up. It is never called an error, because pausing to answer the door is not a mistake.

**Their goal.** To rejoin without feeling they broke something.

## TheRoom · 1A, 1B, 1C

**One screen with three arrangements**, swapped by the person holding it, not three products.

**What happens.** Chat runs the whole way through. Notes arrive on their moments and stay in the conversation afterwards, so someone who was looking at their television reads it a moment later and nothing is lost. One arrangement keeps the conversation front and centre, one keeps a scrollable history of every note so far, and one shows a single note at a time for somebody who wants the room quiet.

**Their goal.** To watch the film. The phone is a companion and the moment it competes with the television the product has failed, which is why nothing here demands attention and why there are no unread counters chasing anyone.

**Two things the curator can do into this screen.** Call an intermission, where the clock stops, the room gets a countdown, and she can come on camera alone for as long as she wants. And mark up a frame from the film for everybody at once.

**Why intermission is honest about its limits.** The product cannot pause anybody's television. It is a social contract with good instrumentation: people tap to say they have paused, and the curator can see how much of the room is actually with her.

## LightsUp · 1D⑩

**The five minutes after the film ends.** The notes stop. Nothing else does. The questions people left when they reserved open for the curator to answer live, in front of the room that asked them. Her next screening is bookable right there. Three minutes in, she can send everyone to wherever she is going to carry on. Four minutes in, anyone without an account who has not dismissed or completed the invitation is asked whether they want one. Someone who chose to save a Taste Passport or join a persistent group may have signed in before the screening.

**Their goal.** To talk about what they just watched, with the people they watched it with, while it is still fresh.

**Her goal.** To leave with the room. Some of these people arrived through the platform rather than through her, and this is where they become hers.

**The account invitation.** Guest booking and attendance remain available. Lights up is the default invitation after a first screening. A person who chooses a persistent feature, such as a saved Taste Passport or group membership, can sign in at that moment. Declining returns them to the screening journey.

## AfterTheShow · 1H and 1I

**The recap (1H)** is what is left when the room empties: who was there, the notes worth keeping, the questions and how she answered them, three tags for what to watch next, and what she is running next. Two separate ratings, because how the film was and how the night was are different questions and a curator can programme a bad film beautifully.

**Their goal.** To come back to it later, or to catch up if they missed the five minutes.

**Her goal.** Only the second rating is hers to act on. It tells her whether the room worked, which nothing else does.

**The Taste Passport (1I)** is a record of curators followed, sessions attended and notes saved. A library card rather than a trophy case: proof of having been in the room, not points.

**Their goal.** Somewhere their taste accumulates. It is also the quiet argument for having made an account.


---

# New boards and extensions

## SeasonStudio · R01a–b

**The curator's goal.** Programme a connected run of films and promote the run through one link.

**R01a, the editor.** From CuratorPrep or her profile, she chooses **Create a season**, enters a title and a short premise, and adds existing draft sessions or creates new ones. Each row shows the film, showtime, runtime, readiness, and its place in the season. She can order the programme and write one sentence explaining each film's connection to the others. Example: “Bad Marriages, Great Cinema,” three Thursday screenings. She can edit the order before publication; dates determine the audience's chronological schedule.

**R01b, publish review.** She reviews the complete programme, ticket total, film-access information, and dates. She can save an incomplete draft. Publishing a bookable season requires dated, bookable sessions and no overlapping screenings. She can share an individual film or the whole programme through CuratorShip, with separate attribution for those destinations.

**After publication.** She sees reserved and attended counts per session and returning attendance across the season. Adding a film creates a new purchase choice; it does not charge existing attendees. Rescheduling or cancelling a session requires a review of affected reservations and a notice to those attendees. Cancelled sessions receive the existing session refund treatment, including their portion of a season purchase.

**MVP boundary.** One curator per season. The audience pays the sum of the included session prices. Subscription billing, discounts, and automatic enrolment sit outside this flow.

## SeasonDetail · R02a–c

**The audience's goal.** Understand the run, check access and dates, and reserve the films they want to attend.

**R02a, programme.** From a profile, shared link, Marquee card, or session page, the viewer sees the curator's premise followed by the ordered screenings. Each row includes local date/time, service access in their country, individual price, and reservation state. Primary action: **Reserve the season**. Secondary action: **Choose screenings**. A viewer joining halfway through sees remaining screenings and a separate recap link for past nights.

**R02b, reservation review.** The viewer checks selected sessions, the total, and any film they must rent or source elsewhere. Projector charges for the hosted experience; the viewer arranges film access. Existing reservations appear as reserved and do not enter the total. Sold-out or cancelled sessions leave the purchase selection before payment, with an explanation. If availability changes during checkout, the viewer reviews the revised selection and price before paying.

**R02c, confirmation.** The attendee receives individual reservations under one season receipt, calendar actions, and a link to invite friends. Reserving one film remains available. The next season date appears in the Lobby, LightsUp, and recap. The curator can leave a written question to carry into that screening.

**States to draw.** Draft/private link; open programme; part-attended season; existing reservations; sold-out session; changed date; failed payment with retry; successful reservation. A retry must not create duplicate charges or seats.

## WatchTogether · R03a–c

**The audience's goal.** Make a plan with friends and carry that group into another screening.

**R03a, invitation.** From reservation confirmation or session detail, the attendee chooses **Watch with friends**, names a group, and copies an invitation link or opens the phone's share sheet. They choose whether the invite permits link holders to join or requires organiser approval. Projector does not send messages to contacts without a user action.

**R03b, group.** A recipient sees the inviter, group name, proposed screening, price, and access requirements. They can accept the invitation with an email verification link; someone who wants a persistent group saves it through an account. Group members see display names and distinct states: **Interested**, **Reserved**, and **Can't make it**. Accepting an invitation does not buy a seat. A guest can reserve without joining the group.

**R03c, the next plan.** In LightsUp, the recap, or the group page, any member can propose another dated screening, including one from another curator. Other members accept or decline that proposal and complete their own checkout. One active proposal per group keeps the MVP flow small. The organiser can close a proposal and start another.

**Controls.** Members can leave or mute a group. The organiser can remove a member, revoke an invite link, or approve join requests. Only joined members see the membership roster. No address-book upload or private messaging in this version. If a screening sells out, the group page shows that state without implying that an invitation holds seats.

**Existing boards.** Add a compact group reservation summary in the Lobby and a **Plan our next screening** action after the film. Keep group notifications out of the film's timed-note experience.

## ProgrammeVote · R04a–c

**The curator's goal.** Choose among films she wants to host after hearing from her audience.

**R04a, ballot editor.** She selects up to three films, writes a sentence about each, sets a closing date, and chooses an eligible audience: attendees of a named session or members of her foyer. She previews the ballot before publishing. One active ballot per curator in the MVP. A programming ballot chooses a film; the separate commissioning flow tests a proposal against an interest threshold.

**R04b, vote.** The attendee sees the options and deadline. They choose one film, add an optional short argument, and opt into a result notice. They can change their vote before closing. An email-verified identity or signed-in account permits one vote; guest session eligibility follows the verified reservation. Vote totals appear after voting, with a label explaining that votes express interest rather than paid reservations.

**R04c, result.** The curator sees the tally and arguments, selects the result, and adds a short explanation if she chooses a different film or resolves a tie. She can create a session draft from the selected title. Before she publishes a dated session, the audience sees **Chosen; date to follow**. After publication, voters can reserve through the result page. Any public credit for an audience argument requires that contributor's agreement.

**States to draw.** Open, voted, vote changed, closed with no votes, tie awaiting curator decision, chosen without a date, published, and cancelled. Editing film options after votes arrive requires closing the ballot and starting a new one; preserve the prior result.

**Existing boards.** Offer the ballot during LightsUp and in the recap or foyer. Place the next-screening reservation first when the curator has a dated programme. Do not stack several competing full-screen prompts after the credits.

## RepertoryShelf · R05a–c

**The curator's goal.** Reuse preparation while checking that the next performance works for its audience and film edition.

**R05a, library.** From CuratorPrep, she opens **My repertory**. Rows show title, last screening date, version/runtime, note count, prior attendance, and encore requests. She can open the old recap or choose **Create an encore**.

**R05b, duplicate review.** She names the new session and sets its showtime. She chooses which authored material to copy: Liner Notes, pre-show, intermissions, and promotional text. Projector creates an independent draft. Past chat, audience questions, attendee lists, reservations, payment records, and analytics stay with the original session. Copied tracking links receive new session identifiers when she publishes.

**Timing check.** She confirms film edition/runtime and checks copied timestamps in the dry run. If she uses a different cut, she must review the timing before publishing. She sees expired links, missing attachments, and notes outside the entered runtime. The new session starts unpublished; the system does not arm copied notes until she reviews the queue. Editing an encore leaves the earlier recap intact.

**R05c, demand.** A visitor to a past screening can choose **Tell me about an encore**. The curator sees unique interested viewers and their preferred time windows, if supplied. She can notify those who opted in after publishing an encore; repeated clicks do not increase demand counts.

**States to draw.** Empty library, duplicate in progress, new draft, missing media, changed cut, invalid timestamp, no encore scheduled, and encore bookable. Keep this separate from a recording or an on-demand replay: the curator hosts another live night.

## RegularsNotebook · R06a–c

**The curator's goal.** Prepare for people she has met through her screenings and remember their contributions.

**R06a, returning attendees.** In CuratorPrep, she opens **People coming back**. She sees the current session's returning attendees who permit recognition, each with display name, number of attended screenings with her, and a prior question or contribution. First-timers receive a separate count so she can prepare a welcome without a public hierarchy.

**R06b, attendee detail.** She sees that person's attendance with her and contributions to her sessions. She can add a short private hosting note, such as “Asked about production design.” A link returns to the original contribution. She does not see their Letterboxd history, private taste profile, other groups, or attendance with other curators. Private notes stay with the curator who wrote them.

**R06c, recognition preferences.** The attendee controls **Let this curator recognise me across screenings**, default off. The description explains which attendance and contribution history the curator will see. They can revoke permission from the Taste Passport; the curator then loses access to the linked notebook entry and its private notes. Display-name changes propagate to this view.

**On-air extension.** A collapsible regulars drawer lets the curator find a prior question on her phone. She chooses whether and when to greet someone. Projector does not insert automated public greetings into chat. Draw the empty, permission-disabled, and permission-revoked states.

## CommissionProgramme · R07a–c

**The curator's goal.** Test demand for a programme before preparing it.

**R07a, proposal editor.** From her profile or CuratorPrep, she chooses **Propose a screening**. She enters a film or defined programme, her pitch, a minimum number of interested people, an interest deadline, and up to three candidate dates. She displays the intended ticket price and known film-access requirements. Example: “If 20 people are interested, I'll choose a date for this programme.” She must not describe expressions of interest as ticket sales.

**R07b, audience interest.** The viewer reads the proposal, selects any dates they could attend, and chooses **I'm interested**. They verify an email address or use their account. No payment or seat reservation occurs. The count represents unique interested viewers; they can edit their dates or withdraw. Their date choices remain private to the organiser. A notice explains that the curator will confirm whether the screening will proceed.

**R07c, curator decision.** At the threshold or deadline, the curator reviews total interest and the count available for each date. Reaching the threshold invites a decision; it does not create a public session. She can confirm a date and create a draft, extend the proposal with a notice, or close it. She reviews the chosen date and price before publication. Interested viewers receive a booking invitation according to their opt-in and pay through the normal checkout.

**States to draw.** Open below threshold, threshold met, deadline passed, awaiting curator decision, confirmed/bookable, declined, extended, and withdrawn interest. If demand splits across dates, show that split. If the curator changes the film or price, show the change in the booking invitation; prior interest does not constitute acceptance.

**MVP boundary.** No crowdfunding balance, deposits, automatic charges, or guaranteed production. A defined single screening can serve as the first commissioning test; a season proposal can link to SeasonStudio when confirmed.

## PassportRequests · R08a–c

**The audience's goal.** Ask for a film they want someone to host and hear when a suitable screening opens.

**R08a, watchlist.** In the Taste Passport, the viewer searches Projector's film catalogue and chooses **Want to watch**. Imported Letterboxd watchlist entries appear here with an import label. Watching a film and liking a film remain distinct signals. An imported watchlist entry does not subscribe the viewer to messages.

**R08b, request and alert controls.** On a watchlist film, the viewer chooses **Tell me when someone hosts this** and selects followed curators or any curator. They can send a programme request to one curator through **Ask this curator to host it**. The curator sees aggregated demand, not a public list of requesters. The viewer can withdraw the request and edit alert preferences. One viewer counts once per film/curator request.

**R08c, matched screening.** After a curator publishes a matching film, an opted-in viewer sees the session date, curator, price, region/access information, and **Reserve a seat**. Match the canonical film, not a similar title. In-app matches remain visible when alerts are muted. Suppress repeat notices for the same screening and stop booking prompts after reservation. Show “No screening scheduled” while the request has no match; do not imply that a curator has agreed to host it.

**Curator extension.** In CuratorPrep, add **Requested by your audience**, with unique request counts and **Make a ballot**, **Propose a screening**, or **Create a session**. Show service/time information only in aggregate. A request does not create a commission, vote, or reservation without a separate action.

**Country and service changes.** Recheck access when a match appears. If access remains unknown, show that status and let the viewer check the source. Offer an explicit **Include films I could rent** preference; do not silently remove those screenings from discovery.

## CuratorFoyer · R09a–c

**The audience's goal.** Continue a conversation with the curator's community between screenings.

**R09a, foyer.** From a curator profile, recap, or Taste Passport, a visitor sees the curator's description, current prompt, recent replies, and a pinned next screening or season. A signed-in member can join and reply. The curator chooses whether visitors can preview posts or must join to read. Joining the foyer and following the curator are separate choices with visible states.

**R09b, prompt editor.** The curator writes an optional weekly prompt, such as “Bring one film you watched and one sentence about it.” She previews and publishes it, or pins a ballot, programme proposal, or session. She can close replies on an old prompt. She does not need to post on a fixed schedule to keep her screenings available.

**R09c, moderation.** The curator can remove a post, close replies, mute a participant, or remove a member. Members can report a post, block another member, mute the foyer, or leave. A blocked person's posts disappear for the blocking member. Reports enter a curator/platform review queue; removal states explain that a moderator removed a post without reproducing its contents.

**Notifications.** Members choose a digest, curator posts only, or mute. Default to a digest with email consent, and in-app updates otherwise. Replies do not each send a notification. Keep foyer updates out of the Room while a screening runs.

**Existing handoff.** Preserve the curator's external destination at LightsUp. Offer **Continue in the foyer** as another destination or recap link. The curator chooses the main continuation link. Projector does not force her to move her outside community.

**MVP boundary.** One foyer per curator, text posts and replies, one pinned item, and basic moderation. No direct messages, voice rooms, paid community tiers, or member-created channels. Draw an empty foyer with a suggested prompt, a joined foyer, a muted foyer, a closed thread, and removed content.

# Taste Passport personalisation

## Product decision

Provide two routes: **Import Letterboxd data** and **Build my taste profile**. An importer can refine their preferences through the same training flow. A person without Letterboxd can reach the same curator feed. Import supplies film signals; the viewer supplies their preferences for hosts and discussion styles.

A guest can explore and try film picks without signing in. Ask them to create or sign into an account when they choose to save a persistent profile or commit an import. Declining preserves access to guest reservation and attendance. Do not put account creation between a shared screening link and checkout.

The Taste Passport now has five destinations: **My screenings**, **Saved notes**, **Want to watch**, **My taste**, and **My communities**. My taste holds explicit preferences, imported data controls, and recommendation feedback. My communities holds followed curators, joined foyers, and friend groups. These are sections within the Passport, not five new bottom-navigation tabs.

## TasteSetup · R10a–d

**R10a, entry.** From optional onboarding or **My taste**, the viewer chooses **Import Letterboxd data**, **Pick some films**, or **Skip for now**. State the benefit: “Find curators who programme films you care about.” Show region and streaming services alongside an option to include rentals or other access. People can edit these choices later.

**R10b, film picks.** Show a varied set of searchable films. On each film, the viewer can choose **Love it**, **Like it**, **Not for me**, **Want to watch**, or **Haven't seen it**. Suggest five to ten opinions, with no required minimum. Include **Show different films** and a search field so the viewer does not need to recognise the initial selection. Avoid treating an unseen film as a dislike. Let them undo a pick.

**R10c, hosting preferences.** Ask optional questions with examples: film craft versus history/context; quiet notes versus active discussion; familiar favourites versus discoveries. Let the viewer choose both or skip. Ask for preferred days and time windows as scheduling preferences, separate from taste. A viewer can enjoy a curator while being unable to attend their current programme.

**R10d, curator preview.** Show a short list of relevant curators with a reason, hosting-style description, sample Liner Note, and next session if scheduled. Actions: **Follow**, **See programme**, **Less like this**, and **Change my picks**. Explain a recommendation using a concrete input: “You chose an interest in cinematography; this curator programmes films through camera work.” Do not invent a matching interest to fill the card.

**States.** No picks, a few picks, no matching curator, no upcoming matching session, loading, and saved profile. In a small launch roster, show the available curators and explain the limited choice. Do not present a percentage match or imply precision the system has not earned.

## LetterboxdImport · R11a–d

### Verified capability and limits

Letterboxd documents an account export from its website Settings as a ZIP containing CSV files. The proposed Projector mobile flow uses that user-downloaded archive. The team has not completed an authenticated iPhone or Android export test. Treat the mobile-browser handoff and exact Settings labels as release checks, rather than claiming support from a tested native app integration. [Letterboxd FAQ](https://embed.letterboxd.com/about/faq/) · [Account export help](https://letterboxd.zendesk.com/hc/en-us/articles/15179196880911-Can-I-get-a-copy-of-my-account-data)

Letterboxd grants API access by request and states that it does not grant access for recommendation projects under its current policy. Projector must not depend on an API connection or promise continuous sync. The MVP uses files that the user chooses to upload. The team should recheck the policy if it pursues a partnership. Research checked 6 September 2026. [Letterboxd API access policy](https://letterboxd.com/api-beta/)

### R11a, mobile instructions

The viewer sees these steps:

1. Open Letterboxd in your phone's browser and sign in there.
2. Open Settings and find the account export option.
3. Download the ZIP and save it in Files or Downloads.
4. Return to Projector and choose **Upload Letterboxd export**.

Provide **Open Letterboxd**, **I have my file**, and **Pick films instead**. Open the website in another browser tab so the viewer can return to Projector. They enter Letterboxd credentials on Letterboxd, never into a Projector form. If their phone extracts the ZIP, offer a supported CSV upload path. State that this copies selected data once and that they can repeat the import to update it.

### R11b, choose file and inspect

Open the phone's file picker. Accept a Letterboxd ZIP or supported individual CSV files. Show the file name and processing state with **Cancel**. The importer reads recognised film ratings, watched-film history, diary/rewatch history, and watchlist data when present. Build against a current export fixture before finalising filenames and column mappings; the official export help does not document a complete schema. Do not reuse Letterboxd's inbound CSV-import specification as proof of the outbound archive structure.

Keep review text, comments, private lists, account settings, deleted-content folders, and unrelated archive data outside the MVP import. Allowlist recognised files and columns. Reject unsupported or oversized files with a clear retry path. Apply compressed and expanded size limits, safe archive paths, and a row limit; agree numeric limits after testing representative archives. One failed file must not erase a saved taste profile.

### R11c, review before saving

Show counts by supported category, selected categories, unmatched films, and duplicate entries. A viewer can deselect categories. Explain that watched history means familiarity, ratings express preference, and watchlist films express intent. Display imported ratings on their source scale and preserve the original value. Do not label a watched film as liked in the absence of a rating or explicit preference.

Match films through available stable identifiers; use title/year as a fallback and ask for a choice when matches conflict. Show unresolved titles in a separate list with **Find film** or **Skip**. Do not fetch Letterboxd profile pages or scrape a film catalogue to fill gaps. The engineer must supply a film-catalogue mapping through an approved metadata source. Projector does not require an API from Letterboxd to parse the viewer's file.

Primary action: **Save selected data**. Secondary actions: **Back** and **Cancel import**. Show the categories that will contribute to recommendations. Keep source film history distinct from Projector attendance; an imported diary entry never becomes a hosted screening attended.

### R11d, completion and future imports

Confirm the counts saved and offer **Find my curators** or **Refine my taste**. Store source attribution and import date. Reimport merges by person, film, and record identity where available; repeated diary watches remain distinct history without multiplying preference weight. An import must not overwrite an explicit Projector preference. Missing rows in a later archive do not delete prior data without a separate removal action.

In My taste, offer **Import a newer file** and **Remove imported data**. Removing an import clears its derived recommendation signals while preserving Projector attendance and explicit preferences. Delete the uploaded archive after processing; retain selected structured records, not the entire account export. An import cancellation discards staged records and the archive. The team must define and disclose a short expiry for abandoned staging jobs before release.

**Failure states to draw.** Wrong file, missing supported data, corrupt ZIP, size limit, permission/file-picker cancellation, interrupted upload, expired session, partial matching, duplicate import, and processing failure. In each case show **Try again** and **Build my taste profile**. A successful partial import must state the saved and skipped counts.

## MarqueeTaste · R12a–b

**R12a, feed.** Keep **On now**, **Tonight**, and **This week**, and add **For you** and **Following** filters. Within For you, show curator recommendations and their upcoming screenings. Booked nights and friend-group plans remain reachable through **My screenings**. A curator without a dated session can appear as someone to follow, with “No screening scheduled,” rather than a dead booking card.

**Initial ranking.** Implement an explainable weighted model using explicit film preferences, curator-declared programme and hosting interests, watchlist overlap, and the viewer's chosen hosting style. Use permitted metadata to connect liked films with relevant themes or makers. Combine that relevance with service/region access, date suitability, and explicit follows for screening order. Keep a portion of recommendations open to discovery and prevent one curator from filling the entire view. The team can tune weights from beta evidence without introducing a machine-learning training pipeline into the MVP.

**Separate film and host feedback.** Preserve the recap's two ratings. “I disliked this film” updates film preference; “I enjoyed this curator's night” updates curator affinity. Attendance is a weak positive signal; a missed event is not a dislike. Treat the film player's watch-through as unknown because Projector does not control it. Room presence does not prove the viewer watched the film.

**R12b, explanation and correction.** Each recommendation offers **Why this?** with the real contributing preferences and **More like this**, **Less like this**, **Hide curator**, or **Bad time for me**. Feedback about a time slot changes scheduling preferences without downgrading the curator's taste match. In My taste, the viewer can edit preferences, review hidden curators, remove imported data, pause behavioural personalisation, or reset recommendations. Resetting clears derived taste and feedback signals with a confirmation; it leaves reservations and attendance records intact and lets the viewer choose whether to keep explicit follows.

**States.** New user with no preferences; import in progress; sparse roster; nothing available on chosen services; no suitable dates; hidden curator; and personalisation paused. Offer **Browse all curators**, **Change services**, or **Include rentals** as relevant. Keep explicit access constraints in force until the viewer changes them. Avoid presenting an empty feed as evidence that nobody fits their taste.

# Cross-board implementation and review

## Prompts, identity, and notifications

Keep the film as the audience's main focus. Put new decisions in prep, the Lobby, LightsUp, recap, and Passport. Preserve quiet notes and resync during the film. At LightsUp, prioritise the booked next date or next dated screening, then one curator-chosen action such as a ballot or group plan. Put other options in the recap.

Use guest checkout for seats. Use verified identity for unique votes and expressions of interest. Require an account to save a taste profile, persistent group membership, or foyer membership. Merge verified guest reservations into the same person's account so account creation does not inflate attendance or demand counts.

Separate reservation notices from optional curator, watchlist, group, and foyer updates. Ask for channel consent at the relevant action. Support email and in-app delivery first; offer push only where supported and enabled. Use one preferences page and deduplicate notices when a single screening matches a follow, watchlist alert, and season interest. The viewer can mute a feature without losing their reservation notices.

## Minimum shared records

The engineer will need relationships for season/session membership; group/membership/invitation/proposal; ballot/option/vote; source-session/encore; recognition permission/private curator note; commissioning proposal/date/interest; film request/alert subscription; foyer/post/reply/moderation; taste signal/source/import batch; and recommendation feedback. Reuse the same person, film, curator, and session identities across these records. Preserve existing payment and attendance records as the sources of truth for purchases and participation.

## Review checks before the team calls these flows complete

| Area | Demonstration required |
|---|---|
| Seasons | Reserve selected remaining nights, exclude an existing reservation, and handle a cancellation without charging twice. |
| Groups | Accept an invitation without buying a seat; buy a seat as a separate step; leave the group and revoke an invite. |
| Ballots | Change one vote, close a tie, and turn the curator's choice into a dated booking page. |
| Repertory | Copy a session into an independent draft, catch a runtime mismatch, and preserve the source recap. |
| Regulars | Opt into recognition, show only that curator's history, and revoke notebook access. |
| Commissioning | Count unique interest, show date splits, and require checkout after confirmation. |
| Film requests | Match a canonical film, respect alert consent, and suppress duplicate notices. |
| Foyer | Join, mute, report, remove a post, and leave without losing a screening reservation. |
| Mobile import | Complete export/download/upload on an iPhone browser and an Android browser using a consented test account; record browser/version and the actual Settings labels. |
| Import integrity | Review a current export fixture, handle unmatched films and corrupt files, reimport without duplicates, and remove imported signals. |
| Taste feed | Produce a useful no-import flow, explain a curator recommendation, and separate “bad time” from “dislike.” |
| Sparse supply | Show a helpful route when the launch roster has no matching upcoming programme. |
| Guest path | Reserve and attend with no taste setup or persistent account requirement. |

## Beta measurement

Track second attendance within 30 days among first-time attendees with a full observation window, with same-curator and different-curator returns reported apart. Show reserved-to-attended conversion for season seats and invited groups. For ballots, commissions, and alerts, measure the path from interest to reservation to attendance.

Track curator preparation time for first runs and encores, and the share who host a fourth session after the three requested founding screenings. Report the promotional and standard revenue-share periods apart. Measure import starts, successful reviews, saved imports, manual taste completion, curator follows, and attendance after a recommendation. Count a room join as attendance under a documented rule; report room presence separately from estimated film watch-through.

The five-curator beta can produce useful case studies and directional comparisons. Do not describe differences between self-selected season buyers, importers, or group members as a proven causal retention lift.

## Companion documents

- Original baseline: `Projector-Wireframe-Guide.md`.
- Product specification: `Projector-Product-Spec.md`; version 3 incorporates the IDs and flows in B01–B21; sections 03, 09, and 10 cover design, the foundation handoff, and the roadmap.
- Investor framing: `Projector-Investor-Deck.md`; the writer should update the roadmap only after the team estimates this scope.
- Deferred experiments: `Projector-Future-Roadmap.md`.


## Provisional streaming connection boards · Y01–Y04

These boards follow product spec module B21 and do not change the React PWA requirement. Their customer-facing activation depends on a verified Younify browser flow.

- **Y01, connect.** In My taste, choose Connect streaming services, read the requested data scope, and select an available service. Keep file import and manual picks available.
- **Y02, browser handoff.** Choose Continue in browser to complete the supported provider flow. Preserve the original route and show an I've finished linking action for a manual return.
- **Y03, return/status.** Recover a server-owned linking attempt. Show pending verification, syncing, cancellation, retry, or verified completion. A redirect alone does not establish success. If the return opens a browser tab, offer Return to Projector without promising automatic installed-PWA reopening.
- **Y04, review/manage.** Review profile, selected categories, matched/skipped records, and last sync. Correct shared-profile titles, commit selected signals, reconnect an expired source, or disconnect and remove its data.

Draw expired attempt, wrong Projector account, browser closed, blocked popup, provider outage, incomplete callback, and duplicated return states. See B21 for server operations, callback verification, source provenance, acceptance tests, and activation criteria.
