# Wedding Guest Guide - Requirements

Status: Implementation-ready specification; real event content is still required before guest release.
Last updated: 2026-10-15, Asia/Ho_Chi_Minh.
Companion delivery plan: [backlog.md](backlog.md).

## 1. Purpose and success criteria

Create a small, friendly Vietnamese landing page that guests can open from a shared link to prepare for the wedding and travel between Hanoi and Nam Dinh. Prioritize practical answers on a phone: when to attend, where to go, where and when to board the coach, whom to call, and when the return journey departs.

Success means:

- A guest can reach the schedule, directions, or coach information with one section-navigation tap after opening the page.
- The date and the three main ceremony times are easy to find without reading decorative content.
- A guest can identify the correct pickup location, departure time, vehicle, and trip leader without contacting the couple for routine questions.
- Older relatives can read text and activate controls comfortably.
- The owner can edit event information in one HTML file through GitHub and publish it without installing a frontend framework or running a build.
- Core information, FAQ disclosure controls, map links, and telephone links work even when JavaScript is disabled.

## 2. Confirmed facts, decisions, and unknowns

### 2.1 User-provided facts

| Topic | Confirmed information |
| --- | --- |
| Language | All guest-facing content must be Vietnamese with proper diacritics. |
| Family information | Groom, groom's parents/family, bride, and bride's parents/family. |
| Directions | Separate Google Maps directions for the groom's home and bride's home. |
| Outbound travel | Coach pickup locations and times in Hanoi; wedding travel involves Nam Dinh. |
| Coach information | Trip leader's name and telephone, pickup stops, vehicle plate/type, passenger counts, and return departure time. |
| Engagement ceremony | 09:00. |
| Lunch | 11:00. |
| Wedding celebration | User supplied "1h30". Interpret provisionally as 13:30 because it follows lunch; confirm before guest release. |
| Visual style | Simple, approachable, intimate, cheerful, and softly colored. |
| Hosting | A GitHub-provided domain with a simple update and deployment process. |
| Passenger privacy | User explicitly selected public aggregate counts per pickup stop; trip leaders retain named passenger lists privately. This supersedes the initial request for an on-page passenger list. |

Do not infer the wedding date from the current date. Do not assume that all events take place at the same address, that the two homes are in the same locality, or that both travel directions have the same passengers or stops.

### 2.2 Repository and account evidence

Read-only checks completed on 2026-10-15:

| Check | Observed result |
| --- | --- |
| Local working directory | `/Users/liamvu/Documents/my-project/wedding-faq` |
| Git remote | `https://github.com/thanhvt18/wedding-faq.git` |
| Authenticated GitHub account | `thanhvt18`, verified through authenticated `GET /user`. |
| Repository | `thanhvt18/wedding-faq`, public. |
| Current account permissions | Admin, maintain, push, and pull available. |
| Default/local branch name | `main`. |
| Commits and remote branches | No local commits; remote branch list is empty. The first push must create `main`. |
| Pages state | Repository reports `has_pages: false`; the Pages endpoint returns HTTP 404, consistent with no configured Pages site. |
| Initial project content | Empty `requirements.md` and `backlog.md`; no application or framework to preserve. |

Expected project-site URL after deployment: `https://thanhvt18.github.io/wedding-faq/`. This is a planned URL, not a verified live deployment. Repository ownership and GitHub authentication were checked separately; a Git remote alone does not establish account identity.

### 2.3 Default implementation decisions

- A single static HTML page, handwritten CSS, and a small optional JavaScript enhancement file.
- Publish `main:/docs` using GitHub Pages "Deploy from a branch".
- Public counts only; no named passenger roster, passenger search, login, or passenger database.
- Native anchor navigation and native `<details>/<summary>` FAQ disclosures.
- Google Maps links rather than an embedded map or Maps JavaScript SDK.
- Mobile-first layout with no mandatory photo, animation, external font, or third-party script.
- Event content lives in `docs/index.html`; avoid a JSON-driven renderer that would make essential information depend on JavaScript.
- Use a compact visible update timestamp and an optional notice for schedule changes.

These choices match the small information-only scope and preserve readability when scripts or external services fail. Static hosting and the project URL format are documented by [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages).

## 3. Scope and priorities

### 3.1 Required for the first guest release

1. Welcome area, couple's names, confirmed date, and quick navigation.
2. Both families and the names of the couple and parents, using owner-approved presentation.
3. Distinct locations for both homes and any separate ceremony or reception venue.
4. A dated schedule covering 09:00, 11:00, and the provisionally interpreted 13:30 event.
5. Outbound and return coach information, contacts, pickup instructions, vehicle details, and aggregate counts.
6. Practical Vietnamese FAQ and a contact section.
7. Clear missing-information states during drafting, accurate update timestamps, and a final content review.
8. Responsive, accessible, fast loading, JavaScript-independent core content.
9. GitHub Pages deployment instructions and an owner editing guide.

### 3.2 Useful follow-up enhancements

- Copy address and copy page link buttons, with explicit failure feedback.
- A print stylesheet for a one-page or compact travel reference.
- A static QR code for the verified production URL.
- A calendar download after event dates, venues, and duration are confirmed.
- An optional couple photograph, compressed and explicitly provided or approved by the owner.
- Browser smoke-test automation if content updates become frequent.

### 3.3 Out of scope

- RSVP processing, online seat booking, a payment or gift collection system, authentication, an admin dashboard, a CMS, a database, or server-side code.
- Publishing passenger names, individual travel assignments, phone numbers, IDs, or a private roster link.
- Live coach tracking, inferred traffic predictions, automatic messages, or automatic Google Sheets synchronization.
- A custom domain purchase, a root-level user site repository, or hosting through another provider.
- Background music, autoplay video, large galleries, countdowns, and decorative loading screens.

## 4. Guest journeys and information architecture

### 4.1 Main journeys

| Guest need | Expected path | Completion condition |
| --- | --- | --- |
| Find the wedding time | Open page, read date, tap schedule | See dated events with times and locations. |
| Travel independently | Tap locations, select the correct home/venue | Read the full address and open the matching Maps destination. |
| Join the coach | Tap transport, find outbound vehicle and pickup stop | See meeting instructions, boarding/departure time, leader contact, and count. |
| Return to Hanoi | Open return-trip information | See return meeting point, departure time, drop-off plan, and contact. |
| Ask for a seat or change a stop | Read transport FAQ, call trip leader | Understand that a leader confirms the assignment privately. |
| Resolve a last-minute problem | Tap contact or the leader's phone link | Reach a named responsible person; no need to guess whom to call. |

### 4.2 Page order and stable anchors

| Order | Section | Anchor | Key content |
| --- | --- | --- | --- |
| 1 | Welcome | `#welcome` | Names, date, warm introduction, compact date/time summary, optional notice. |
| 2 | Quick navigation | `#navigation` | Schedule, transport, locations, FAQ, and contact links. |
| 3 | Schedule | `#schedule` | Dated chronological event list. |
| 4 | Transport | `#transport` | Outbound trips, counts, then clearly separate return trips. |
| 5 | Locations | `#locations` | Groom's home, bride's home, additional venues when applicable. |
| 6 | Families | `#families` | Two equally prominent family blocks. |
| 7 | FAQ | `#faq` | Practical native disclosure items. |
| 8 | Contact and footer | `#contact` | Primary support contact, optional backup, update timestamp, thank-you. |

Provide individual location anchors such as `#groom-home` and `#bride-home`, and unique trip/stop anchors when useful. Navigation wraps on narrow screens. Do not hide primary information inside a carousel, modal, or collapsed FAQ. A compact sticky navigation is acceptable only if it never covers content or keyboard focus.

## 5. Functional requirements

### FR-01. Welcome and navigation

- Render a Vietnamese page title, one main heading, the couple's names, and the confirmed calendar date.
- Show the three event times in the schedule; the welcome summary may link to it rather than repeat editable details.
- Show a warm short introduction and clear links to schedule, transport, locations, FAQ, and contacts.
- When the date is unknown in a draft, show an explicit pending state instead of a sample date.
- Include a keyboard-accessible skip link to the main content.

### FR-02. Family information

- Separate groom-side and bride-side blocks with Vietnamese headings.
- Each block supports the person's full name, father's display name, mother's display name, and an optional short family introduction.
- Honorifics and family circumstances are owner-supplied. Do not invent occupations, birthdays, addresses, family relationships, or wording about absent relatives.
- The owner can explicitly omit a parent field; an intentionally omitted field is not a validation error. Otherwise collect the requested parents' names before release.
- Family phone numbers and portraits are optional and only included when approved for public display.

### FR-03. Locations and Maps

- Show two unmistakably different home cards even if they share a locality.
- Each published location has a label, complete written address, verified Google Maps destination, and optional entrance/landmark/parking instructions.
- Support a separate lunch or reception venue; events reference the actual relevant location.
- A Maps link must take guests to the corresponding location, not to a generic city search or the other family's home.
- Prefer an owner-verified map share link or `https://www.google.com/maps/search/?api=1&query=<encoded-destination>`; a directions link can use `https://www.google.com/maps/dir/?api=1&destination=<encoded-destination>`.
- Properly encode Vietnamese addresses. A verified coordinate or Place ID may improve precision; do not guess coordinates.
- Retain readable address text when Maps cannot open. New-tab links use appropriate `rel` attributes and understandable accessible names.
- Do not request geolocation or load a map iframe on initial page load. Standard [Google Maps URLs](https://developers.google.com/maps/documentation/urls/get-started) do not require an API key and can open an installed app or browser.

### FR-04. Wedding schedule

- Render events in chronological order, grouped by explicit calendar date if events span multiple days.
- Include 09:00 engagement ceremony, 11:00 lunch, and provisional 13:30 wedding celebration. Confirm the afternoon interpretation and the owner's preferred event names before release.
- Each event shows its time, title, location link, and any relevant arrival or transfer instructions.
- Store machine-readable timestamps with `+07:00` when dates are known; display `DD/MM/YYYY` and 24-hour `HH:mm` in Vietnam time.
- Do not parse a date-only string through a timezone conversion that changes the displayed day. Do not use the guest device's timezone for wedding times.
- Do not infer event end times, journey durations, or whether lunch and the wedding celebration are the same meal. Ask the owner to clarify this distinction.

### FR-05. Outbound coach information

- Support one or more vehicles/trips without changing the page architecture.
- Each trip includes a clear public label, route, date, leader name and callable number, vehicle type, plate or explicit pending status, capacity if confirmed, and passenger count.
- Each Hanoi pickup stop includes a unique label, full address, verified Maps link, meeting instructions/landmark, boarding time, departure time when separately specified, and aggregate passenger count.
- Label boarding time and departure time distinctly; never invent an arrival buffer or assume they are identical.
- Order stops in the actual route order. Show the destination and estimated arrival only if provided by the organizer, with estimated times labeled accordingly.
- State how to register, change pickup stops, or report a delay through the trip leader. Counts are informational and do not reserve a seat.
- When multiple vehicles use the same stop, distinguish them by trip label, time, plate when available, and leader.
- A late plate assignment may remain pending on a published page only if guests can identify the trip through its label, stop/time, and working leader contact.

### FR-06. Counts and private passenger management

- Display aggregate passenger counts per trip and pickup stop. Do not display a passenger list, passenger lookup, individual assignments, or passenger phone numbers.
- The leader maintains the full named roster outside this public repository and site. Its storage or management interface is not part of this project.
- Counts represent registered passengers for that specific direction and date, not remaining seats or total wedding attendance.
- A passenger contributes to exactly one pickup stop for a given trip; leader reconciliation happens privately before updating public totals.
- For each trip, the displayed total equals the sum of its boarding-stop counts. Unknown counts are labeled pending, not rendered as zero.
- Counts are nonnegative integers. If capacity is supplied, flag any total exceeding that capacity for organizer correction before release.
- Outbound and return totals are separate. Do not sum them into a unique guest count, or assume everyone returns on the same vehicle.
- Keep names out of HTML comments, scripts, JSON, test fixtures, screenshots, committed documents, and Git history. Hiding information visually does not make it private.

### FR-07. Return journey

- Give the Nam Dinh-to-Hanoi journey a clear heading and full date.
- Show return meeting location/address/Maps link, boarding or meeting time, departure time, vehicle/leader, and Hanoi drop-off locations in order.
- Identify estimated arrival times as estimates only when the organizer supplies them.
- Do not automatically reuse outbound pickup stops as return drop-off points or copy outbound passenger totals.
- If a return trip has multiple boarding stops, apply the same count reconciliation as outbound. Drop-off counts are optional and are not added to boarding totals.
- Unknown return times must be visibly pending in drafts. Guest release requires a confirmed departure time or an explicit organizer-approved pending notice with a working contact and a plan to communicate the final time.

### FR-08. FAQ and practical guidance

- Use native `<details>/<summary>` controls with visible focus states. Multiple answers may stay open.
- FAQ items link to canonical schedule/transport/location sections rather than duplicating dates, numbers, and addresses in prose.
- Cover event attendance, independent travel, coach registration, changing stops, late arrival, return travel, parking, and whom to call.
- Include dress guidance, children/older guests, accessibility, dietary needs, weather arrangements, and accommodation only with organizer-provided answers or a clear contact-based fallback.
- Avoid promises about parking, accessibility, food, child seating, accommodation, or transport that the organizer has not confirmed.
- Do not add a submission form that has no real receiving service.

### FR-09. Contact actions

- Display at least one public, owner-approved contact name, role, and telephone number.
- Trip cards link directly to the responsible leader; a backup contact is recommended for the ceremony period when the couple may be unavailable.
- Use valid `tel:` links and a human-readable number. Normalize the underlying dialing number without changing its identity.
- Optional Zalo/group links require an owner-provided URL and approval to make the invitation publicly accessible. Omit otherwise.
- In drafts, missing contacts produce readable pending text with no fake or empty telephone link.

### FR-10. Updates and incomplete information

- Show an organizer-maintained "last updated" timestamp in Vietnam time. Do not replace it with the visitor's current time.
- An optional visible notice can call attention to a changed pickup stop, time, or vehicle. Keep details in their canonical section.
- Do not silently display fabricated names, dates, numbers, addresses, map destinations, or license plates.
- Missing core event data blocks guest release. Optional empty fields are omitted; pending operational fields follow the explicit exceptions above.
- Do not call counts or schedules live. Updates become visible after a new deployment and page reload.

### FR-11. Share metadata

- Provide UTF-8, `lang="vi"`, viewport metadata, a Vietnamese title/description, and a small favicon.
- Metadata must not contain passenger information or unapproved personal details.
- After the production URL is confirmed, configure canonical/Open Graph URLs to include `/wedding-faq/`.
- Use `noindex, nofollow` as a best-effort indexing preference for this personal guide. Explain in the editing guide that it does not restrict access or prevent sharing, scraping, or caching.
- Rich previews vary by messaging app; clear readable content must not depend on a preview image.

### FR-12. Editing and publishing

- Keep all guest-facing event text in `docs/index.html`, grouped under clear English section comments.
- Put presentation in `docs/assets/styles.css`; add `docs/assets/main.js` only for optional enhancements.
- Keep core content in HTML. Avoid duplicating canonical times/addresses in JavaScript or a second configuration file.
- Document common edits: change a time, update a phone number, correct a map pin, change a plate, reconcile counts, add a stop, add a second vehicle, and update the timestamp.
- A content edit requires no package install or build command. Native Pages deployment publishes committed static files.
- Root-level planning and contributor documents are outside the Pages publication folder, but remain public in the public GitHub repository.

## 6. Content contract and validation rules

These are editing and validation contracts for semantic HTML, not a requirement to create a database or JSON API. Use stable section IDs and `<time>` elements where applicable.

| Record | Required fields for release | Optional or conditional fields |
| --- | --- | --- |
| Wedding | Couple's approved names; event date(s); timezone; welcome text | Short notice; approved photo |
| Family | Side; person name; requested parent names or explicit owner-approved omission | Family introduction; public contact |
| Location | Stable ID; label; complete address; verified Maps URL | Landmark; entrance; parking; accessibility note |
| Event | Stable ID; date; local time; title; valid location reference | Arrival advice; end time; transfer note |
| Public contact | Name; role; verified phone display and dialing value | Approved messaging URL |
| Vehicle | Stable label; type; plate or approved pending text | Confirmed capacity |
| Trip | Stable ID; direction; date; leader; vehicle; destination; boarding stops; total or explicit pending state | Estimated arrival; operational note |
| Boarding stop | Label; location; route order; boarding/departure timing; count or pending state | Distinct meeting time; landmark |
| Return drop-off | Location; route order | Organizer-provided arrival estimate |
| FAQ item | Stable ID; Vietnamese question; answer or canonical section link | Category |
| Update marker | Actual content update datetime with Vietnam offset | Notice expiry date if useful |

Validation rules:

1. IDs must be unique; every internal location, trip, and section reference must resolve.
2. Published external links must use intended HTTPS destinations, except `tel:` telephone links. No placeholder `href="#"`, empty URLs, or `javascript:` URLs.
3. Dates and times are valid and chronologically consistent within each itinerary. Flag unexpected overnight travel or ceremony overlaps for organizer confirmation.
4. Distinguish `0` from unknown. A stop with zero registered passengers may remain visible if the coach still serves it; otherwise the organizer removes it.
5. If any boarding-stop count is unknown, do not publish a fabricated exact trip total. Use pending totals until reconciled.
6. HTML values are text, not injected markup. Escape special characters when editing names or addresses.
7. Any document, image, or future downloadable artifact in `docs/` is public. No private roster is permitted elsewhere in this public repository either.
8. Phone numbers, map pins, and official event details are validated with the organizer, not inferred from unrelated internet results.

## 7. Vietnamese copy guidance

Technical documentation and comments are English. The following guest-facing copy is intentionally Vietnamese, as explicitly requested. Names and actual logistics must be supplied by the owner.

| Purpose | Suggested Vietnamese copy |
| --- | --- |
| Page title | `Thông tin ngày vui của chúng mình` |
| Welcome | `Chúng mình rất vui được đón bạn đến chung vui cùng hai gia đình. Mọi thông tin về lịch trình, đường đi và xe đưa đón đều ở đây nhé!` |
| Navigation | `Lịch trình` / `Xe đưa đón` / `Địa điểm` / `Câu hỏi thường gặp` / `Liên hệ` |
| Family labels | `Nhà trai` / `Chú rể` / `Bố chú rể` / `Mẹ chú rể` / `Nhà gái` / `Cô dâu` / `Bố cô dâu` / `Mẹ cô dâu` |
| Home labels | `Nhà chú rể` / `Nhà cô dâu` |
| Event labels | `Lễ ăn hỏi` / `Bữa trưa thân mật` / `Tiệc cưới` |
| Trip headings | `Chiều đi: Hà Nội đến Nam Định` / `Chiều về: Nam Định đến Hà Nội` |
| Coach labels | `Trưởng đoàn` / `Điểm đón` / `Giờ có mặt` / `Giờ xe đón` / `Giờ khởi hành` / `Biển số xe` / `Loại xe` / `Số khách đã đăng ký` |
| Map action | `Mở Google Maps` or `Xem đường đi` with a location-specific accessible name |
| Call action | `Gọi trưởng đoàn` / `Gọi người hỗ trợ` |
| Pending | `Thông tin đang được cập nhật. Bạn liên hệ trưởng đoàn để được hỗ trợ nhé!` |
| Date pending in draft | `Ngày tổ chức đang được cập nhật` |
| Counts explanation | `Số lượng được tổng hợp theo từng điểm đón. Bạn liên hệ trưởng đoàn để xác nhận chỗ và điểm đón của mình nhé!` |
| Update label | `Cập nhật lần cuối:` |
| Estimated time | `Dự kiến` |
| Footer | `Cảm ơn bạn đã dành thời gian đến chung vui cùng chúng mình!` |

Recommended FAQ questions:

1. `Mình nên có mặt lúc mấy giờ?`
2. `Lễ ăn hỏi, bữa trưa và tiệc cưới diễn ra ở đâu?`
3. `Mình tự đi thì xem đường đến nhà trai, nhà gái ở đâu?`
4. `Mình đăng ký đi xe hoặc đổi điểm đón như thế nào?`
5. `Làm sao biết mình đã được xếp chỗ trên xe?`
6. `Nếu đến điểm đón muộn thì mình liên hệ ai?`
7. `Xe từ Nam Định về Hà Nội lúc mấy giờ, trả khách ở đâu?`
8. `Ở địa điểm tổ chức có chỗ gửi xe không?`
9. `Mình nên mặc gì để vừa thoải mái vừa phù hợp?`
10. `Nếu đi cùng trẻ nhỏ, người lớn tuổi hoặc cần hỗ trợ di chuyển thì báo ai?`
11. `Mình ăn chay hoặc có nhu cầu ăn uống đặc biệt thì liên hệ ai?`
12. `Nếu trời mưa hoặc lịch trình thay đổi thì xem thông báo ở đâu?`

Questions 1-7 and 12 are required; include questions 8-11 when the organizer supplies practical answers or directs guests to an appropriate contact. Do not treat suggested copy as confirmation of logistics.

## 8. Visual and interaction requirements

### 8.1 Design direction

Use a warm ivory background, soft pink and pale sage surfaces, dark readable text, generous spacing, and restrained floral or rounded decorative details. Decorations must not compete with travel information.

Suggested CSS tokens, subject to measured contrast verification:

| Token | Starting value | Intended use |
| --- | --- | --- |
| Background | `#FFF9F5` | Main page |
| Surface | `#FFFFFF` | Cards and FAQ |
| Soft pink | `#F6E2E1` | Decorative highlights |
| Soft sage | `#E9F0E8` | Secondary section surfaces |
| Text | `#513D3D` | Body text and headings |
| Accent | `#9B4B5A` | Buttons, links, emphasized times |

- Use a system font stack with Vietnamese support; an installed serif may be used for headings. Do not rely on a remotely loaded font.
- Body text should be at least 16 CSS pixels, preferably 17-18 on phones, with approximately 1.5-1.7 line height.
- Keep prose lines comfortable to scan and the overall page around 1040-1120 pixels maximum width.
- Use one column on phones; two-column family/location cards are appropriate on larger screens.
- Use a vertical schedule and readable trip/stop cards instead of a wide itinerary spreadsheet on mobile.
- Use roughly 16-20 pixel phone gutters, consistent spacing, and restrained 12-20 pixel corner radii.
- No text over busy images. No all-caps paragraphs, continuous confetti, scroll-triggered reveal dependency, or decorative text that loses Vietnamese accents.

### 8.2 Accessibility and responsive behavior

- Target WCAG 2.2 AA practices relevant to this page. Verify normal text contrast of at least 4.5:1 and large text at least 3:1, following [W3C contrast guidance](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html).
- Primary touch controls should be at least 44 by 44 CSS pixels as a project usability target.
- Use real links/buttons, heading hierarchy, landmarks, list semantics, and visible keyboard focus.
- Keep all content readable at 200% zoom and without page-level horizontal scrolling at 320 CSS pixels wide.
- Test 320, 375/390, 768, and 1440 pixel viewport widths, including long Vietnamese names and addresses.
- Anchor navigation must not leave section headings hidden under sticky UI. Browser back/forward and direct hash links must work.
- Icons supplement text; decorative icons are hidden from assistive technology. Meaningful photographs need appropriate alternative text.
- Respect reduced-motion preferences if smooth scrolling or transitions are used.
- Buttons for enhancements appear only when their functionality is available; failures retain a usable manual fallback.

## 9. Technical architecture and quality targets

### 9.1 Proposed repository structure

```text
wedding-faq/
  requirements.md
  backlog.md
  README.md                 # English setup, editing, release, and rollback guide
  docs/
    .nojekyll              # Empty file, disables Jekyll processing
    index.html             # All canonical Vietnamese guest content
    assets/
      styles.css
      favicon.svg
      main.js              # Add only when an enhancement needs it
      images/              # Add only for approved, optimized assets
```

The initial implementation has no required `package.json`, framework, bundler, database, or build output. Future QA tooling may add development-only dependencies without changing guest delivery. Do not add generated files merely to imitate a framework project.

Use relative asset URLs such as `./assets/styles.css`, not `/assets/styles.css`, because this is a project site under `/wedding-faq/`. Same-page navigation uses fragment links. Do not implement client-side routes that require server rewrite rules.

### 9.2 Nonfunctional requirements

| ID | Requirement | Acceptance evidence |
| --- | --- | --- |
| NFR-01 | Readable core content without JavaScript or third-party services | Browser check with scripts disabled; Maps unavailable does not hide addresses. |
| NFR-02 | Fast initial load | Required HTML/CSS/JS combined at most 100 KiB uncompressed; optional JS at most 10 KiB; no third-party initial requests. |
| NFR-03 | Image discipline | If added, each ordinary photo at most 200 KiB; explicit dimensions; below-fold images lazy-loaded; initial page transfer target at most 500 KiB. |
| NFR-04 | Performance | Representative mobile Lighthouse performance target at least 95; lab LCP target at most 2.5 seconds and CLS at most 0.1. Record environment and investigate regressions. |
| NFR-05 | Accessibility and layout | Keyboard, zoom, contrast, focus, long-content, and viewport checks in section 8 pass. |
| NFR-06 | Correctness and privacy | No broken anchors/assets, wrong destinations, unsupported promises, fabricated data, private roster data, or uncaught application errors. |
| NFR-07 | Compatibility | Verify current stable Chrome and Safari, including Android/iPhone guest flows when available; smoke-test desktop Firefox. Record any unavailable devices. |
| NFR-08 | Maintainability | Common content edits are documented and require no build; timestamps and repeated references stay consistent. |

Web Vitals thresholds describe user experience, but a local audit is not field evidence. INP of at most 200 ms is an interaction goal; do not claim a measured field percentile from a small prelaunch test. See [Web Vitals](https://web.dev/articles/vitals).

No analytics, cookies, local-storage identifiers, service worker, or runtime API is required. Avoid an offline cache that could keep old coach times visible. A simple loaded page remains readable if connectivity drops, but reopening offline is not promised.

## 10. GitHub Pages deployment plan

### 10.1 Selected route

Use the existing public repository and publish the `docs` folder on `main`. GitHub supports branch publication from the root or `/docs`; branch publication still runs a GitHub-managed deployment workflow. No custom workflow is necessary for this buildless site. See [publishing source configuration](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

Keep the project URL under `/wedding-faq/`; a repository named `thanhvt18.github.io` is unnecessary for this request. Public repositories are eligible for GitHub Pages on GitHub Free; no paid plan is needed for this repository. See [GitHub Pages availability](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages).

### 10.2 First deployment runbook

This is a future implementation/release procedure. The current task only creates the planning documents and checks existing account access.

1. Implement and locally review the page. Review all files for public suitability and complete the release-content checklist in section 11.
2. Create `docs/index.html`, the required assets, and empty `docs/.nojekyll`. GitHub documents entry files and the `.nojekyll` behavior in [site creation](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).
3. Preview locally from `docs/`, for example `rtk proxy python3 -m http.server 4173 --directory docs`. Also serve the repository root and visit `/docs/` to test operation under a path prefix. Stop the server after testing.
4. Check the diff, add the intended files, commit with an English message, and push `main` to the existing `origin`. This creates the currently missing remote branch. Do not add an agent co-author automatically.
5. Open `https://github.com/thanhvt18/wedding-faq/settings/pages`.
6. In "Build and deployment", select "Deploy from a branch", choose `main`, select `/docs`, and save.
7. Confirm HTTPS is enabled and avoid mixed-content resources, following [GitHub HTTPS guidance](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https).
8. Inspect the "pages build and deployment" run in the repository Actions tab. Verify it finishes successfully before sharing the URL.
9. Open the URL shown by GitHub Pages. Check `/wedding-faq/`, all anchors/assets, phone links, and both home map destinations. Verify the latest content/update timestamp on a phone.
10. Record the verified URL and deployment evidence in the project handoff. A green deployment alone is not evidence that content or map destinations are correct.

Use `gh-axi` for future GitHub CLI operations, inspecting its current help before choosing commands. Do not store tokens, print credentials, or infer successful Git push authentication merely from API access. Existing API authentication is working; actual push remains untested until release work.

### 10.3 Routine updates and recovery

- Edit `docs/index.html` using GitHub's file editor or a local checkout, then review the changes and update the content timestamp.
- Check affected logistics and reconcile related counts before committing. Push/commit to `main`; branch publication starts automatically.
- This simple publication route has no custom test gate. Perform required checks before the publishing commit; do not assume future CI will prevent a bad Pages release.
- Wait for the deployment run, then verify the affected section on the live URL. Avoid promising instant propagation.
- For a bad content update, revert the specific published commit, publish the revert, and verify recovery. Preserve unrelated edits; do not force-push or reset shared history.
- For a 404, check the branch exists, the source is `main:/docs`, the entry file is `docs/index.html`, the deployment succeeded, and the URL includes `/wedding-faq/`.
- For missing styling, check relative URLs and filename case. For stale content, compare the deployed commit and reload before changing architecture.

## 11. Content collection and release gates

Implementation can start immediately with clearly labeled draft states. Sending the site to wedding guests requires the following content decisions. Collect private details privately; only commit the approved public subset.

| ID | Information to collect or confirm | Why it matters | Release rule |
| --- | --- | --- | --- |
| C-01 | Wedding date and whether all events occur on one day | Guests cannot plan from times alone | Required. |
| C-02 | Couple's names and approved parent/family presentation | Requested family information | Required, with explicit omissions allowed. |
| C-03 | Both homes' full addresses and verified Maps pins | Avoid arriving at the wrong house | Required. |
| C-04 | Location for each event; separate reception venue if any | Do not assume events share one home | Required. |
| C-05 | Confirm 13:30; explain the 11:00 lunch versus 13:30 celebration | Avoid an ambiguous meal/ceremony schedule | Required. |
| C-06 | Public trip leader and primary support names/numbers | Guests need a working help channel | Required for offered transport. |
| C-07 | Vehicle labels/types, plates, capacity where known | Help guests board the correct vehicle | Labels/type required; plate may use FR-05 pending exception. |
| C-08 | Hanoi pickup stops, dates, exact meeting/departure times, map pins, landmarks | Make pickup actionable | Required for offered transport. |
| C-09 | Aggregate counts per boarding stop and direction | Keep travel information consistent | Confirmed counts or explicit pending states; no invented zero. |
| C-10 | Return date, meeting point/time, departure, vehicles, Hanoi drop-offs | Guests need a way home | Required or explicit FR-07 pending-time exception. |
| C-11 | How/when to register for transport or change a stop; late-arrival instructions | Set expectations and avoid missed pickup | Contact-based instructions required; deadlines only if supplied. |
| C-12 | Confirm public suitability of family details, addresses, contacts, and vehicle plates | This is a public personal event guide | Owner content review before release. |
| C-13 | Parking, last-mile access, walking/step constraints, rain arrangements | Useful for independent travelers and older guests | Recommended; use a contact fallback if unknown. |
| C-14 | Dress guidance, dietary contact, children, and accommodation advice | Reduce common guest questions | Optional organizer-approved answers. |

Further suggestions for the owner:

- Provide a backup contact who will be available during the ceremonies.
- Explain transfer arrangements between homes or venues if guests need to move during the day.
- Identify a recognizable pickup landmark and clarify which side of the road guests should wait on.
- Confirm whether travelers may join only one direction and whom to tell if their plans change.
- Provide any luggage, accessibility, or child-seat arrangements as concrete organizer guidance without making unsupported guarantees.
- Set a final-check time before the wedding to verify plates, numbers, departure times, and map pins.
- Decide when to remove detailed travel/contact information after the wedding. Removing it later cannot guarantee removal from third-party caches or Git history.

## 12. Acceptance scenarios and definition of done

| ID | Scenario | Expected outcome |
| --- | --- | --- |
| AT-01 | Open on a 375/390 pixel phone | Vietnamese date/names and useful navigation appear without obstructive decoration. |
| AT-02 | Follow each section link and a direct `#transport` URL | Correct section is reached, heading visible, back/forward works. |
| AT-03 | Read schedule | Dates, 09:00, 11:00, confirmed 13:30, and correct event venues are unambiguous. |
| AT-04 | Open both home map links | Distinct verified destinations; written addresses remain visible on the page. |
| AT-05 | Find an outbound pickup for each offered vehicle | Date, stop, landmark, time, plate/status, leader, and count are available together. |
| AT-06 | Reconcile passenger totals | Each trip total matches known boarding-stop counts; unknowns, zero, and capacity checks behave correctly. |
| AT-07 | Read return travel | Return meeting point, departure date/time/status, vehicle/contact, and drop-offs are distinct from outbound. |
| AT-08 | Use phone and FAQ controls | Correct dialing targets; keyboard-operable native disclosures and readable focus indicators. |
| AT-09 | Disable JavaScript | All core information, navigation, FAQs, Maps, and telephone links remain usable. |
| AT-10 | Inspect page source and public repository content | No passenger roster, passenger identifiers, hidden private records, or secrets. |
| AT-11 | Test missing draft fields | Explicit Vietnamese pending text; no fake dates, map links, plates, or phone numbers. |
| AT-12 | Test 320/768/1440 pixels, 200% zoom, and long names | No clipped content, overlapping controls, page-level horizontal scroll, or lost diacritics. |
| AT-13 | Deploy under `/wedding-faq/` and reload | Entry page, relative assets, and anchors work over HTTPS without console/resource errors. |
| AT-14 | Review family and FAQ copy | Both families represented as approved; practical answers contain no invented commitments. |
| AT-15 | Run a representative mobile performance audit | Size budgets met; performance evidence recorded with the environment and any limitations. |
| AT-16 | Edit a pickup time or count and publish | Only canonical content needs changing; timestamp is updated; live page reflects the deployed commit. |
| AT-17 | Review all publishable content | Required C-items resolved; permitted pending exceptions are explicit and actionable. |
| AT-18 | Preview at a path prefix and with third-party access unavailable | Assets still load at a prefix; useful page content does not depend on Maps loading. |

Definition of done for implementation: all P0 backlog items have evidence, required content gates are resolved, the owner can follow the editing guide, visual and functional checks pass, and the deployed URL is verified. Draft implementation may finish before content collection, but must be reported as a draft rather than guest-ready. There is no deployed site as part of this documentation task.
