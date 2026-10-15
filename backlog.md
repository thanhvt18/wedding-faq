# Wedding Guest Guide - Implementation Backlog

Last updated: 2026-10-15, Asia/Ho_Chi_Minh.
Specification: [requirements.md](requirements.md).
Status: Planning complete; implementation not started.

## 1. Delivery rules

- P0: required for the first guest release. P1: useful follow-up, not a release blocker. P2: future work only if requested.
- Keep the selected stack: semantic HTML, CSS, optional small vanilla JavaScript, and GitHub Pages publishing `main:/docs`.
- Public passenger information is aggregate counts only. The user explicitly chose private named rosters managed by leaders outside this repository.
- All visible guest content is Vietnamese. Technical documentation, comments, and commit messages are English.
- Use the existing repository `thanhvt18/wedding-faq`; the expected URL is `https://thanhvt18.github.io/wedding-faq/`.
- Local shell commands follow the repository's RTK instruction. Use `gh-axi` for GitHub operations after inspecting current command help.
- Keep temporary fixtures, screenshots, logs, and test reports under `/tmp`; do not commit them or private event information by accident.
- Do not manually modify generated files or changelogs. Do not automatically add an agent co-author to commits.
- For defects found during implementation, reproduce the guest-visible failure in a browser first, then fix and recheck that flow. Fix encountered broken tests and clear visual defects as part of completion.
- No application implementation, commit, push, Pages activation, or publication has been performed by this planning task. The deployment steps below describe the subsequent implementation task.

## 2. Verified starting point

Read-only checks on 2026-10-15 confirmed authenticated GitHub user `thanhvt18`, public repository `thanhvt18/wedding-faq`, and admin/push access. Local branch is `main`, with no commits, and the remote has no branches yet. Pages is not configured. `requirements.md` and `backlog.md` were initially empty.

Account authentication and remote ownership are known; actual Git push and live hosting are not yet verified. No account switch, repository creation, paid plan, or custom domain is currently needed.

## 3. Delivery sequence and dependencies

| Order | Item | Priority | Depends on | Can proceed with draft content? |
| --- | --- | --- | --- | --- |
| 1 | B-01 Collect and validate public event content | P0 | None | Yes; track unresolved C-items. |
| 2 | B-02 Create static structure and visual foundation | P0 | Requirements | Yes. |
| 3 | B-03 Welcome, navigation, and families | P0 | B-02 | Yes. |
| 4 | B-04 Locations and schedule | P0 | B-02 | Yes. |
| 5 | B-05 Outbound transport and aggregate counts | P0 | B-02 | Yes. |
| 6 | B-06 Return transport | P0 | B-05 | Yes. |
| 7 | B-07 FAQ, contacts, and update states | P0 | B-03 to B-06 | Yes. |
| 8 | B-08 Responsive, accessibility, performance, and privacy review | P0 | B-03 to B-07 | Yes; rerun affected checks after final content. |
| 9 | B-09 Owner editing and release guide | P0 | B-03 to B-07 | Yes. |
| 10 | B-10 Final content and guest-journey acceptance | P0 | B-01, B-08, B-09 | Requires release-content gates. |
| 11 | B-11 Publish and verify GitHub Pages | P0 | B-10 | Publish guest-ready content. |
| Later | B-12 Copy helpers and print layout | P1 | B-08 | Yes. |
| Later | B-13 Share QR and calendar convenience | P1 | B-11; confirmed event details | No for final downloadable artifacts. |
| Later | B-14 Repeatable browser smoke tests | P1 | B-08 | Yes, with synthetic data. |
| Optional | B-15 Approved couple photo | P2 | Owner-provided asset | No asset invention. |

B-03, B-04, and B-05 are logically independent once the foundation is ready, but share `docs/index.html`; coordinate edits sequentially unless file ownership is explicitly separated. This backlog does not require multiple agents.

Milestones:

1. **Local draft:** B-02 through B-07 complete, with real information where available and explicit pending states elsewhere.
2. **Guest-ready candidate:** B-01 and B-08 through B-10 complete, with only explicitly allowed operational pending states.
3. **Live release:** B-11 complete, with verified URL, deployment evidence, and owner handoff.

## 4. P0 work items

### B-01. Collect and validate the public event content

Outcome: The implementation uses correct owner-approved information and contains no private passenger records.

Requirements: FR-02 through FR-10; C-01 through C-14.

Work:

- Collect the date(s), couple/parent names, home addresses, map pins, and event-specific venues.
- Confirm the afternoon interpretation of "1h30" and explain the distinction between lunch at 11:00 and the celebration at 13:30.
- Collect each outbound vehicle, leader, pickup stop, boarding/departure time, capacity where available, and aggregate count.
- Collect the return meeting point/date/time, vehicle/leader, and drop-off plan independently.
- Obtain public support contacts, transport registration/change instructions, and the approved optional FAQ guidance.
- Keep unresolved content keyed by the C-identifiers in requirements; do not require optional FAQ details before implementation can begin.
- Confirm public suitability of the actual content during the normal final review. Passenger privacy has already been decided; do not ask the same preference again.

Acceptance:

- [ ] C-01 through C-12 are resolved or use only the explicitly permitted pending/omission rules.
- [ ] The owner verifies both home pins and all pickup/return meeting pins.
- [ ] The schedule's dates, ceremony names, venues, and 13:30 interpretation are confirmed.
- [ ] Trip totals reconcile privately before public aggregate counts are entered.
- [ ] No named passenger roster is requested for upload, added to the repository, or linked publicly.

Evidence: A non-sensitive completion checklist. Private source material remains outside the repository. Blocked facts do not prevent B-02 through B-09 draft work.

### B-02. Create the static structure and visual foundation

Outcome: A small, working static page with the agreed soft wedding style and no build dependency.

Requirements: FR-01, FR-11, FR-12; section 8; NFR-01 through NFR-03.

Primary files: `docs/index.html`, `docs/assets/styles.css`, `docs/assets/favicon.svg`, `docs/.nojekyll`.

Work:

- Create semantic page landmarks, UTF-8, Vietnamese language metadata, viewport, and section anchors.
- Establish the ivory/pink/sage palette with dark text and measured button/link contrast.
- Implement mobile-first spacing, typography, cards, schedule list, and navigation styling.
- Use relative asset paths and an empty `.nojekyll` file.
- Put English comments around editable content sections; preserve all essential content as HTML.
- Include title/description and best-effort `noindex, nofollow` metadata. Add production canonical metadata only when its URL is verified.

Acceptance:

- [ ] A simple local HTTP server renders the page without installing packages or running a build.
- [ ] The page works when served at both a root path and a nested prefix.
- [ ] There are no runtime framework, font CDN, map iframe, or analytics requests.
- [ ] The page has a single main heading, a skip link, proper landmarks, and no duplicate IDs.
- [ ] Skeleton states are Vietnamese and clearly incomplete; no realistic invented wedding data is used.

Evidence: Initial mobile/desktop browser inspection and resource-path check, with temporary captures under `/tmp`.

### B-03. Implement welcome, navigation, and family information

Outcome: Guests immediately recognize the wedding and can navigate to practical information.

Requirements: FR-01, FR-02; AT-01, AT-02, AT-14.

Primary files: `docs/index.html`, relevant styles.

Work:

- Add couple names, confirmed date or draft pending text, a short Vietnamese welcome, and navigation.
- Render groom-side and bride-side family blocks, including approved parent names.
- Keep family blocks equal in visual importance and avoid long decorative introductions.
- Add stable anchors and scroll spacing that accommodates any sticky navigation.

Acceptance:

- [ ] Guests reach schedule, transport, locations, FAQ, and contacts through visible links.
- [ ] Both families and the couple/parents appear according to the approved content and omissions.
- [ ] Long names wrap without cropping, overlap, or loss of Vietnamese accents.
- [ ] Direct hash links, browser back/forward, keyboard navigation, and the skip link work.
- [ ] No date is inferred from the current day or visitor timezone.

Evidence: AT-01, AT-02, and family portion of AT-14.

### B-04. Implement verified locations and the wedding schedule

Outcome: Guests understand exactly where and when each event takes place.

Requirements: FR-03, FR-04; AT-03, AT-04, AT-18.

Primary files: `docs/index.html`, relevant styles.

Work:

- Add distinct home cards, complete addresses, Maps links, and approved landmarks.
- Add other venues only if supplied, and connect each event to its actual location anchor.
- Render 09:00, 11:00, and provisional 13:30 in a clear vertical schedule; resolve the provisional value before release.
- Use explicit dates and Vietnam-offset machine-readable timestamps once confirmed.
- Include optional transfer instructions without inventing duration or transport arrangements.

Acceptance:

- [ ] All three events have confirmed dates, times, labels, and matching venue links by release.
- [ ] Both home map links and any other venue links resolve to owner-verified destinations.
- [ ] Written addresses are useful even if Google Maps cannot open.
- [ ] Maps links have encoded parameters when constructed, no API key, and clear accessible names.
- [ ] Missing draft locations create pending text, never a generic or incorrect clickable map.
- [ ] An unusual travel/ceremony sequence is surfaced to the owner rather than silently corrected.

Evidence: AT-03, AT-04, and address fallback portion of AT-18; real mobile app/browser handoff check when available.

### B-05. Implement outbound transport and aggregate counts

Outcome: A Hanoi guest can identify a pickup stop, vehicle, time, and trip leader.

Requirements: FR-05, FR-06, FR-09; AT-05, AT-06, AT-10.

Primary files: `docs/index.html`, relevant styles.

Work:

- Create repeatable trip and stop markup with stable IDs and clear headings.
- Show vehicle label/type/plate or approved pending state, leader name/phone, date, route, and destination.
- For each stop, display address, Maps link, landmark, timing, and aggregate registered count.
- Separate meeting/boarding/departure labels when the organizer provides different times.
- Show totals and explain that registration or changes must be confirmed privately by the leader.
- Document count reconciliation and capacity checks in the editing guide. Do not introduce a roster data store.

Acceptance:

- [ ] Every offered stop has enough confirmed information for a guest to reach it and call the leader.
- [ ] Each trip total equals the sum of known boarding-stop counts; unknown counts are not shown as zero.
- [ ] Capacity conflicts are corrected before release when a capacity is supplied.
- [ ] Two vehicles at one stop remain distinguishable without relying on color alone.
- [ ] Zero, unknown, one-stop, multi-stop, and multi-vehicle cases are reviewed using synthetic temporary fixtures where needed.
- [ ] No passenger name, personal assignment, or passenger phone number exists in source, comments, assets, or committed evidence.

Evidence: AT-05, AT-06, and passenger privacy checks in AT-10. Temporary scenarios belong under `/tmp`.

### B-06. Implement the return journey

Outcome: Guests know how and when to return from Nam Dinh to Hanoi.

Requirements: FR-06, FR-07; AT-06, AT-07.

Primary files: `docs/index.html`, relevant styles.

Work:

- Add a distinct return section with date, meeting point, Maps link, meeting/departure time, vehicle, and leader.
- List Hanoi drop-offs in the provided order and label supplied arrival estimates.
- Maintain return counts separately; do not copy outbound assignments or imply a guaranteed seat.
- Handle a still-unconfirmed return departure only through the explicit approved pending/contact exception.

Acceptance:

- [ ] A guest can distinguish outbound pickup, return boarding, and Hanoi drop-off information.
- [ ] Return date/time, vehicle, and contact are independently confirmed or explicitly pending under FR-07.
- [ ] Different outbound/return counts and different routes are supported.
- [ ] Boarding totals do not include drop-off counts a second time.
- [ ] Any transfer between the last event and return meeting point is explained when relevant.

Evidence: AT-07 and the return-specific portion of AT-06.

### B-07. Implement FAQ, contacts, and update states

Outcome: Guests get practical answers and know whom to contact when plans change.

Requirements: FR-08 through FR-11; AT-08, AT-09, AT-11, AT-14.

Primary files: `docs/index.html`, relevant styles.

Work:

- Implement the required FAQ questions with native disclosure elements.
- Link answers to canonical details instead of repeating addresses, time values, and phone numbers.
- Add approved public contacts with valid `tel:` targets and a backup contact if supplied.
- Add a real content-update timestamp, optional change notice, and consistent Vietnamese pending text.
- Include practical optional FAQ topics only with confirmed answers or an appropriate contact fallback.

Acceptance:

- [ ] Required questions 1-7 and 12 from requirements section 7 have useful answers.
- [ ] FAQ disclosure controls work by mouse, touch, and keyboard with JavaScript disabled.
- [ ] Phone targets match verified contacts and no empty/fake contact link is present.
- [ ] No answer invents parking, meals, accessibility, child seating, or transport guarantees.
- [ ] Update time represents an actual organizer content change, not the visitor's page-open time.
- [ ] Draft fields are explicit, optional empty fields do not create broken controls, and permitted pending fields have actionable contact guidance.

Evidence: AT-08, AT-09, AT-11, and FAQ portion of AT-14.

### B-08. Review responsive behavior, accessibility, performance, and privacy

Outcome: The page remains comfortable and reliable for real wedding guests on phones.

Requirements: NFR-01 through NFR-08; AT-09 through AT-12, AT-14, AT-15, AT-18. Check AT-13 path behavior locally here; final HTTPS/deployment acceptance belongs to B-11.

Primary files: Existing application files; temporary reports only under `/tmp`.

Work:

- Inspect 320, 375/390, 768, and 1440 pixel layouts, long content, and 200% zoom.
- Check heading order, focus, skip link, touch size, contrast, readable addresses, and native FAQ behavior.
- Verify current Chrome/Safari guest flows and desktop Firefox; document device availability accurately.
- Disable JavaScript and block third-party access to verify core functionality and address fallback.
- Check paths, IDs, internal links, HTTPS URLs, console errors, and resource failures.
- Measure file sizes and a representative mobile Lighthouse audit; optimize any added image assets.
- Inspect public source and assets for passenger information, secrets, and accidental private links.
- Fix clear visual defects and encountered test failures before acceptance.

Acceptance:

- [ ] No horizontal page scroll, overlapping labels, clipped buttons, hidden anchor headings, or broken Vietnamese glyphs.
- [ ] Contrast and keyboard checks pass; primary controls meet the 44-pixel project target.
- [ ] Core content/FAQ remains usable without JavaScript or external services.
- [ ] Required HTML/CSS/JS is at most 100 KiB uncompressed; optional JS at most 10 KiB; photo/transfer budgets hold.
- [ ] Mobile performance evidence meets the target or identifies a specific environmental limit with supporting measurements; product regressions are fixed.
- [ ] No unresolved critical guest-flow, accessibility, privacy, or asset-path failure remains.

Evidence: Results for the applicable local AT scenarios, audit environment/results, and manually reviewed mobile/desktop screenshots in `/tmp`. Leave deployment-dependent scenarios pending until B-11. Do not claim unavailable physical-device tests passed.

### B-09. Write the owner editing and release guide

Outcome: The owner can keep the page accurate without learning a framework.

Requirements: FR-12; NFR-08; AT-16.

Primary file: `README.md` in English.

Work:

- Explain the file layout and map content sections to their HTML comments/anchors.
- Document editing through GitHub's file editor and optional local preview using a simple HTTP server.
- Provide worked editing steps for times, map destinations, phone numbers, vehicle plates, stops, vehicles, counts, and the update timestamp.
- Explain public content boundaries, lack of live booking, noindex limitations, and private roster handling.
- Document `main:/docs`, expected URL, HTTPS, deployment verification, propagation, and rollback.
- Explain that local checks precede publication because branch deployment has no custom quality gate.

Acceptance:

- [ ] A basic time/address/count change requires only `docs/index.html`, without build or package installation.
- [ ] The guide explains linked text versus `href`/`datetime` values that need coordinated edits.
- [ ] A second stop or vehicle can be added without inventing a new architecture or duplicating IDs.
- [ ] Troubleshooting covers missing `main`, missing `index.html`, wrong Pages folder, wrong URL prefix, and relative asset paths.
- [ ] Rollback uses a targeted revert and preserves unrelated history.

Evidence: Walk through one content edit and local preview; during B-11 verify the publish cycle. Do not publish fake changes merely to demonstrate editing.

### B-10. Complete final content and guest-journey acceptance

Outcome: The release candidate is accurate enough to send to guests.

Requirements: All P0 requirements, C-items, AT-01 through AT-12, AT-14, AT-15, AT-17, AT-18.

Work:

- Replace draft values with approved content and remove realistic test data.
- Confirm dates, venues, map pins, phone numbers, counts, and the 13:30 interpretation with the owner.
- Review permitted pending fields explicitly, with a contact and communication plan where needed.
- Recheck layouts using actual names/addresses and rerun affected checks after content changes.
- Walk through three complete scenarios: independent traveler, outbound coach passenger, and returning passenger.
- Review all files destined for the public repository, including documentation and assets.

Acceptance:

- [ ] C-01 through C-12 satisfy the release rules; C-13/C-14 are answered, omitted, or given a clear contact fallback.
- [ ] No fake phone, placeholder date, guessed location, or accidental passenger record remains.
- [ ] A guest can determine the time/place, their route to the event, the return plan, and whom to call.
- [ ] The current public text is reviewed for accuracy, warmth, and clarity in Vietnamese.
- [ ] B-08 issues are resolved and the editing guide matches the implemented structure.

Evidence: Non-sensitive acceptance checklist and release-ready file review. If content is missing, report "draft complete, guest release pending content" while completing all independent implementation work.

### B-11. Publish and verify GitHub Pages

Outcome: The accepted page is reachable on the user's GitHub domain.

Requirements: FR-12; AT-13, AT-16; requirements section 10.

Primary surfaces: Local Git repository, existing GitHub repository, Pages settings, live project URL.

Work:

- Recheck existing remote, current access, source files, and the intended publishing diff.
- Create the first reviewed commit and push `main` to the existing `origin` during the authorized implementation/release task.
- Configure Pages: "Deploy from a branch", `main`, `/docs`. Confirm HTTPS.
- Inspect the GitHub-managed deployment run and wait for its outcome.
- Verify the actual URL reported by Pages, including asset loading, anchor navigation, content, and map/contact links.
- Add the verified canonical/Open Graph URL if necessary, publish that final change, and verify the final deployed revision.
- Hand off the URL and editing guide. Record any operational limitation precisely.

Acceptance:

- [ ] `main` exists remotely and contains the reviewed static site.
- [ ] Pages source is `main:/docs`, with `docs/index.html` and `.nojekyll` present.
- [ ] The final deployment completes successfully and the actual URL is recorded.
- [ ] `https://thanhvt18.github.io/wedding-faq/` works over HTTPS, unless GitHub reports a different authoritative URL that is documented.
- [ ] No root-path assumption breaks styles, icons, optional scripts, or navigation.
- [ ] The live update timestamp and content match the intended commit, including at least one real content update if available.
- [ ] The owner receives concise editing and targeted rollback instructions.

Evidence: Final deployment/run reference, published commit, verified URL, and postdeployment phone/browser smoke check. Do not equate an expected URL or a successful push with a successful deployment.

## 5. Optional follow-up items

### B-12. Add copy helpers and a print layout

Priority: P1. Depends on B-08. Scope: `docs/assets/main.js`, optional buttons, print CSS.

- Copy a written address or the canonical page URL using feature detection and a real user action.
- Announce success accessibly; if clipboard access fails, keep selectable text and provide clear Vietnamese feedback.
- Keep helper buttons hidden when their JavaScript behavior is unavailable.
- Print the essential schedule, addresses, coach details, and contacts with expanded FAQ content where appropriate; suppress decorative/navigation clutter.

Acceptance:

- [ ] Clipboard success, denied access, and JavaScript-disabled states have useful outcomes.
- [ ] No core action depends on the enhancement script, and the 10 KiB JS budget remains satisfied.
- [ ] Print preview is readable and does not cut off critical travel information.

### B-13. Add a share QR code and optional calendar file

Priority: P1. Depends on B-11 and confirmed C-01/C-04/C-05.

- Generate a static QR code containing only the verified site URL, with a visible text-link fallback.
- Provide a calendar file only after the organizer confirms what event(s) to include, dates, start/end times or durations, and venues.
- Use a correct Vietnam timezone or equivalent UTC timestamps and test import in a calendar client.
- Document that a downloaded calendar file does not automatically update after the page changes; regenerate it when its underlying event details change.

Acceptance:

- [ ] A phone scan reaches the production project URL.
- [ ] Calendar import shows the confirmed event on the correct date/time, with no guessed end time or private guest data.
- [ ] Optional artifacts remain small, current, and useful without a runtime service.

### B-14. Add repeatable browser smoke tests for frequent updates

Priority: P1. Depends on B-08. Development-only tooling; no change to the static deployment architecture.

- Choose a small browser test setup, such as Playwright, only when repeated maintenance justifies it.
- Cover relative paths at a prefix, anchor navigation, native FAQ controls, JavaScript-disabled content, count consistency, and absence of guest-roster UI/data.
- Keep external Maps/telephone target assertions deterministic; real destination accuracy remains an organizer/browser review.
- Use synthetic fixtures only; temporary reports and screenshots stay in `/tmp`.
- If adding CI later, document whether it actually gates publishing. Do not present a parallel CI run as a Pages deployment gate.

Acceptance:

- [ ] Tests exercise guest outcomes instead of mirroring markup implementation.
- [ ] Tests pass reproducibly without live Google requests or real calls.
- [ ] No runtime dependency or mandatory build is added for ordinary content edits.
- [ ] Test configuration/lockfiles are maintained normally; generated outputs are not hand-edited or committed unnecessarily.

### B-15. Add an approved couple photograph

Priority: P2. Depends on an owner-provided or approved image.

- Optimize the asset, give it intrinsic dimensions and meaningful alternative text, and preserve readable foreground content.
- Remove unnecessary metadata, respect cropping of both people, and recheck phone layout/performance.

Acceptance:

- [ ] The image is approved, appropriately cropped, and within the photo/transfer budgets.
- [ ] The page remains complete and attractive if the image fails to load.

## 6. Requirement-to-work traceability

| Requirement group | Delivery items | Main acceptance scenarios |
| --- | --- | --- |
| Welcome and family details | B-01, B-03 | AT-01, AT-02, AT-14 |
| Addresses, Maps, schedule | B-01, B-04 | AT-03, AT-04, AT-18 |
| Outbound coach and counts | B-01, B-05 | AT-05, AT-06, AT-10 |
| Return journey | B-01, B-06 | AT-06, AT-07 |
| FAQ, contacts, update states | B-07 | AT-08, AT-09, AT-11, AT-14 |
| Visual/accessibility/performance/privacy | B-02, B-08 | AT-09 through AT-15, AT-18 |
| Simple editing and deployment | B-09, B-11 | AT-13, AT-16 |
| Real content and release readiness | B-01, B-10 | AT-17 plus all relevant guest flows |

## 7. Release checklist

- [ ] All P0 work items are complete, or the handoff explicitly says the work is a local draft awaiting named content gates.
- [ ] No ambiguous date, 13:30 interpretation, event venue, or required pickup information remains.
- [ ] Both home directions and all offered coach routes are verified with the organizer.
- [ ] Public counts are consistent; the private roster is absent from every public artifact.
- [ ] Primary and trip-leader contact actions work.
- [ ] Real-content mobile, keyboard, no-JavaScript, and path-prefix checks pass.
- [ ] Performance and visual evidence is recorded honestly; temporary artifacts are outside the repository.
- [ ] The final commit has a successful Pages deployment and a verified HTTPS URL before calling the site live.
- [ ] README editing, publication, and rollback instructions match the actual implementation.
- [ ] The owner receives the live URL, relevant unresolved optional details, and a reminder to recheck transport details before the wedding.

Technical decisions and official GitHub/Google/accessibility references are documented next to the relevant claims in [requirements.md](requirements.md). Recheck GitHub account/Pages settings before implementation because the observed state may change after this planning date.
