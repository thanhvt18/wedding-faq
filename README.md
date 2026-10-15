# Wedding Guest Guide

This repository contains a framework-free Vietnamese wedding guest guide designed for GitHub Pages. The current page is a local draft. It is not guest-ready because the real names, date, addresses, map destinations, contacts, vehicle details, counts, and return plan have not been provided.

The site has no build step, package installation, remote fonts, analytics, embedded maps, or required JavaScript. Core information and FAQ disclosures remain usable when JavaScript is disabled.

## File layout

| File | Purpose |
| --- | --- |
| `docs/index.html` | All canonical guest-facing content and links |
| `docs/assets/styles.css` | Responsive presentation and print-safe styling |
| `docs/assets/favicon.svg` | Small local favicon |
| `docs/.nojekyll` | Keeps GitHub Pages from applying Jekyll processing |
| `requirements.md` | Product requirements and content gates, not guest-facing |
| `backlog.md` | Delivery plan, not guest-facing |

There is intentionally no `docs/assets/main.js`. No current requirement needs JavaScript.

## Where to edit content

Open `docs/index.html`. English comments identify every editable region:

| HTML comment | Stable anchor | Content |
| --- | --- | --- |
| `Editable section: Welcome` | `#welcome` | Couple names, wedding date, introduction, draft notice |
| `Editable section: Quick navigation` | `#navigation` | Main section links |
| `Editable section: Schedule` | `#schedule` | Event times, names, dates, venues, and transfer notes |
| `Editable section: Transport` | `#transport` | Outbound vehicles, pickup stops, return vehicles, counts, and leaders |
| `Editable section: Locations` | `#locations` | Groom and bride home addresses and verified Maps links |
| `Editable section: Families` | `#families` | Couple and parent display names |
| `Editable section: FAQ` | `#faq` | Practical answers that point to canonical sections |
| `Editable section: Contacts and update marker` | `#contact` | Public support contacts and the last content update |

Keep all guest-facing text in Vietnamese. Keep technical comments and documentation in English. Do not edit `requirements.md` or `backlog.md` during routine content updates.

## Local preview

No build is required. Run either preview from the repository root and stop it with `Ctrl+C` when finished.

Preview the `docs` folder as the site root:

```sh
rtk proxy python3 -m http.server 4173 --directory docs
```

Open `http://127.0.0.1:4173/`.

Preview from the repository root to reproduce a nested project path:

```sh
rtk proxy python3 -m http.server 4174 --directory .
```

Open `http://127.0.0.1:4174/docs/`. Confirm that the stylesheet and favicon load in both previews. Relative paths such as `./assets/styles.css` are required because the eventual GitHub Pages site lives under `/wedding-faq/`.

## Common content edits

Always replace pending text with organizer-approved facts. Never create plausible examples in public files.

### Change an event time

1. Find the event under `Editable section: Schedule`.
2. Update the visible value inside `<time>`.
3. Once the date is known, add or update its complete `datetime` value with the Vietnam offset, for example the confirmed date plus `T09:00:00+07:00`. Do not copy that example as event data.
4. Update any FAQ wording that directly mentions the same time.
5. Confirm chronological order and update the content timestamp.

Do not add a machine-readable date until the real calendar date is known. Do not convert wedding times through the visitor's device timezone.

### Add or correct a location and Maps destination

1. Update the written address in the matching location card: `#groom-home`, `#bride-home`, or a new unique venue card.
2. Replace the pending Maps message with a real `<a>` only after the family verifies the destination.
3. Use the owner-provided HTTPS share URL or a correctly encoded Google Maps URL.
4. If the link opens a new tab, include `target="_blank" rel="noopener noreferrer"` and make the link name location-specific.
5. Link the relevant schedule event to that exact location anchor.

The written address must remain useful if Google Maps is unavailable. Never link to a generic city search, a guessed coordinate, or the other family's home.

### Add or update a public phone number

1. Update the contact's visible name and role.
2. Add a readable display number.
3. Add a matching `tel:` link with the verified dialing value, normalized without changing the number's identity.
4. Update the responsible trip card and the contact section together.

Do not create empty, fake, or example telephone targets. Only add numbers approved for a public repository and public website.

### Update a vehicle plate or type

Find the relevant `trip-card` in the transport section. Replace its pending vehicle type or plate text. Keep an explicit pending plate only when the organizer approves that exception and guests can still identify the trip by its unique label, stop/time, and working leader contact.

### Add a pickup stop

1. Copy the complete `stop-card` block inside the correct outbound or return trip.
2. Give the section and heading new, unique IDs. Never reuse `outbound-stop-pending` or its heading ID.
3. Place the stop in actual route order.
4. Add its verified address, Maps destination, landmark, meeting time, boarding time, departure time, and aggregate registered count.
5. Reconcile the trip total after adding the stop.

Meeting, boarding, and departure times are separate facts. Do not assume they are equal.

### Add a second vehicle

1. Copy the complete `trip-card` article, including its stop cards.
2. Give the article, heading, and every stop a new unique ID.
3. Add a distinct public trip label, direction, date, vehicle, leader, stops, and aggregate counts.
4. Ensure guests can distinguish vehicles by text, not color alone.
5. Recheck all internal links and totals.

Outbound and return vehicles are independent. Do not copy counts, assignments, pickup stops, or drop-off points between directions unless the organizer separately confirms them.

### Reconcile aggregate counts

- Publish aggregate counts only, never passenger names, phone numbers, individual assignments, or a private roster link.
- A passenger contributes to one boarding stop for a specific trip and direction.
- The trip total must equal the sum of its boarding-stop counts.
- Unknown is not zero. Keep the total pending if any included stop count is unknown.
- If capacity is provided, stop publication and correct any total that exceeds it.
- Do not include return drop-off counts in a boarding total or combine outbound and return totals into a unique guest count.

Trip leaders must maintain named rosters privately outside this repository. The public site does not book or guarantee a seat.

### Update the content timestamp

After every organizer-approved content change, update both parts of the `<time>` element in `#contact`:

- visible text in `DD/MM/YYYY, HH:mm (giờ Việt Nam)` format;
- `datetime` in `YYYY-MM-DDTHH:mm:ss+07:00` format.

This must record an actual content update, not the visitor's page-open time.

## Pending content gates

The draft must not be shared as a guest-ready guide until the owner confirms:

- wedding date, whether events share a day, couple names, and approved parent presentation;
- both complete home addresses and separate verified Maps destinations;
- the actual venue for every event;
- whether “1h30” means 13:30, the preferred event name, and how it differs from the 11:00 lunch;
- public support and trip-leader names, roles, and telephone numbers;
- each outbound vehicle, route, date, pickup stop, landmark, meeting/boarding/departure time, and aggregate count;
- each return date, meeting point, departure time, vehicle, leader, aggregate count, and ordered Hanoi drop-offs;
- how guests register, change stops, report delays, and receive schedule changes;
- public suitability of family details, addresses, contacts, and vehicle plates.

Parking, accessibility, rain, attire, children, dietary, and accommodation guidance should only be added when the organizer supplies an approved answer or an appropriate public contact fallback.

## Privacy and public-source safety

Everything committed to this public repository can be read, copied, cached, and indexed by third parties. The `noindex, nofollow` metadata is only a best-effort request to search engines. It does not control access and does not prevent sharing, scraping, caching, or Git history retention.

Never place passenger names, personal assignments, passenger telephone numbers, private roster links, secrets, or unapproved personal details in HTML, comments, CSS, JavaScript, images, fixtures, screenshots, documentation, or commit history. Keep test fixtures and screenshots under `/tmp` and use only clearly synthetic, non-personal values.

There is no live booking, seat reservation, live count, coach tracking, form backend, analytics, cookie, or automatic update service. A content change becomes visible only after a new deployment and page reload.

## GitHub Pages setup and release

The planned source is `main:/docs` in the public repository. The expected project URL is `https://thanhvt18.github.io/wedding-faq/`, but it must not be called live until GitHub reports and serves the final URL successfully.

Before publication:

1. Complete every required content gate above.
2. Preview both local URL shapes and run structural, privacy, keyboard, responsive, and browser checks.
3. Review the full public diff. Branch-based Pages publishing has no custom quality gate, so checks must pass before the publishing commit.
4. Commit only the intended files and push `main` when publication is explicitly authorized.
5. In repository settings, open **Pages**, select **Deploy from a branch**, choose `main` and `/docs`, then save.
6. Wait for the Pages deployment workflow to finish successfully and confirm HTTPS.
7. Open the authoritative URL reported by GitHub. Check `/wedding-faq/`, assets, anchors, phone links, map destinations, and the update timestamp on a phone.
8. Add canonical and Open Graph URL metadata only after the production URL is verified, then republish and recheck if those tags are needed.

Do not treat a successful push or an expected URL as a successful deployment. This draft task does not commit, push, configure Pages, or publish anything.

## Editing through GitHub

For a routine content-only change, use GitHub's file editor on `docs/index.html`, preview the diff, update the timestamp, and commit with a concise English message. A package install or build command is not needed. Wait for the Pages deployment to finish, then verify the changed section on the live site.

## Troubleshooting

- **`main` is missing:** confirm the reviewed initial commit exists locally and push it only during an authorized release task. Do not create an unrelated branch as a workaround.
- **The page returns 404:** confirm Pages uses `main:/docs`, `docs/index.html` exists with the exact lowercase name, deployment succeeded, and the URL includes `/wedding-faq/`.
- **Styles or the favicon are missing:** keep asset references relative (`./assets/...`), check filename case, and test both local URL shapes.
- **The page is unstyled only under the repository prefix:** remove root-relative paths such as `/assets/styles.css`; project sites need relative paths.
- **Content appears stale:** compare the deployed commit with the intended commit, wait for deployment completion, and reload before changing the architecture.
- **An anchor lands incorrectly:** confirm the target ID is unique, the fragment matches it exactly, and no sticky element covers the heading.
- **A map or phone action is absent:** pending facts intentionally have no clickable action. Add one only after verification.

## Targeted rollback

If a published content change is wrong, identify the single bad commit and create a normal revert commit:

```sh
rtk git revert <bad-commit-sha>
```

Review the revert, push it through the normal authorized release flow, wait for Pages deployment, and verify recovery on the live site. A targeted revert preserves unrelated history. Do not force-push, reset the shared branch, or replace unrelated files.
