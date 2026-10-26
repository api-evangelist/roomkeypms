# RoomKeyPMS (roomkeypms)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

RoomKeyPMS is a cloud property management system (PMS) for independent hotels and small chains across the US and Canada, with a team of hoteliers behind roughly 70,000 managed rooms. Alongside the core PMS it sells Pulse (AI marketing and guest messaging), Embedded Payments, Capital (growth financing), Mobile Guest, a built-in Distribution/CRS module, and an integrations marketplace.

**API access model (important):** RoomKeyPMS publishes a **real REST API** (JSON or XML, selectable via request header) with endpoint paths, parameters, and behavior **documented publicly** on its support portal under three API types - Pulling Reservation Data, POS, and Statistics and Forecasts. Confirmed endpoints and query parameters are reproduced faithfully below and in `openapi/roomkeypms-openapi.yml`, sourced directly from RoomKeyPMS's own support articles and version release notes. What is **not** open is *access*: there is no self-serve signup or public sandbox. A hotel's IT team must email RoomKeyPMS support and the property must sign off before RoomKeyPMS issues an API key and per-hotel credentials. The exact production API base host is also not published as a standalone value - it is inferred here from RoomKeyPMS's own Help/reference portal and should be confirmed once credentials are issued.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/roomkeypms/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/roomkeypms/refs/heads/main/apis.yml)

## Tags

- Hospitality
- Hotel Technology
- Property Management System
- PMS
- Reservations
- POS
- Gated API

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### RoomKeyPMS Reservation Data API

Pull reservation and guest-profile data by hotel - arrival-based reservations, real-time in-house guests, checked-out guests, cancellations, and reserved-but-not-yet-arrived bookings - each including name, address, email preferences, length of stay, booking source, room/rate, and (since API v2.8.0.2) confirmation numbers from OTA/channel partners (Booking.com, Expedia, TravelClick, SynXis, and others).

- **Human URL:** [https://support.roomkeypms.com/a/1919225-api-type-pulling-reservation-data](https://support.roomkeypms.com/a/1919225-api-type-pulling-reservation-data)
- **Base URL:** `https://www.welcometorsi.net/RoomkeyApi/api`

#### Confirmed Endpoints

- `GET /hotels/{hotelId}/reservations/guestprofile` - reservations by arrival date (`key`, `fromDate`, `toDate`; max 60-day range)
- `GET /hotels/{hotelId}/reservations/guestprofile/inhouse` - real-time in-house guest list (`key`)
- `GET /hotels/{hotelId}/reservations/guestprofile/checkedout` - checked-out guests (`key`, `fromDate`, `toDate`; max 60-day range)
- `GET /hotels/{hotelId}/reservations/guestprofile/cancellations` - cancelled reservations (`key`, `fromDate`, `toDate`)
- `GET /hotels/{hotelId}/reservations/guestprofile/reserved` - reserved, not-yet-arrived reservations (`key`, `fromDate`, `toDate`)

There is no endpoint that returns only records changed since the last call. RoomKeyPMS recommends polling every 10-15 minutes, never in parallel, staggered across properties.

#### Properties

- [Documentation](https://support.roomkeypms.com/a/972656-api-documentation)
- [API Reference](https://support.roomkeypms.com/a/1919225-api-type-pulling-reservation-data)
- [OpenAPI](openapi/roomkeypms-openapi.yml) - [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### RoomKeyPMS POS Integration API

Lets a third-party point-of-sale system (restaurant, retail, spa) look up a guest by room number and post a charge to that guest's folio, so on-property spend outside the PMS lands on the guest's bill. Charge posting requires a configured CostCentre per property and is subject to per-guest credit-limit and payment-method rules.

- **Human URL:** [https://support.roomkeypms.com/a/1687788-api-type-pos](https://support.roomkeypms.com/a/1687788-api-type-pos)
- **Base URL:** `https://www.welcometorsi.net/RoomkeyApi/api`

#### Confirmed Endpoints

- `GET /hotels/{hotelId}/guests/roominquiry` - guest/room lookup by room number (`key`, `roomNumber`)
- `POST /hotels/{hotelId}/transactions/roomcharges` - post a charge to a guest folio (`key`)
- `GET /hotels/{hotelId}/reservations/guestprofile/inhouse` - shared in-house guest list, used to validate room/guest before posting

#### Properties

- [Documentation](https://support.roomkeypms.com/a/972656-api-documentation)
- [API Reference](https://support.roomkeypms.com/a/1687788-api-type-pos)
- [OpenAPI](openapi/roomkeypms-openapi.yml) - [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### RoomKeyPMS Statistics and Forecasts API

Exposes hotel-level statistics for business-intelligence use. The only sub-path confirmed in RoomKeyPMS's public release notes is the receipts endpoint, returning transaction records (date, amount, details, transaction time) for a hotel over a date range. RoomKeyPMS's marketing describes broader ADR, occupancy, and forecast data as part of this API type, but exact sub-paths beyond receipts are not reproduced in public support articles (`endpointsModeled` for that portion).

- **Human URL:** [https://support.roomkeypms.com/m/55959/c/261470](https://support.roomkeypms.com/m/55959/c/261470)
- **Base URL:** `https://www.welcometorsi.net/RoomkeyApi/api`

#### Confirmed Endpoints

- `GET /hotels/{hotelId}/statistics/receipts` - transaction receipts (`key`, `fromDate`, `toDate`; adds `ReservationUniqueID` per channel-partner integration since v2.8.0.2)

#### Properties

- [Documentation](https://support.roomkeypms.com/a/972656-api-documentation)
- [API Reference](https://support.roomkeypms.com/m/55959/c/261470)
- [OpenAPI](openapi/roomkeypms-openapi.yml) - [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [LinkedIn](https://ca.linkedin.com/company/roomkeypms)
- [Website](https://roomkeypms.com/)
- [Documentation](https://support.roomkeypms.com/a/972656-api-documentation)
- [Plans](plans/roomkeypms-plans-pricing.yml)
- [Rate Limits](rate-limits/roomkeypms-rate-limits.yml)
- [Fin Ops](finops/roomkeypms-finops.yml)

## Pricing

RoomKeyPMS does not publish self-serve, public list pricing. It is sold as a contract-priced ("user-pay"), quote-based platform sized by property; the API itself carries no separately documented fee and is bundled into the platform subscription once access is granted. See [plans/roomkeypms-plans-pricing.yml](plans/roomkeypms-plans-pricing.yml).

## WebSocket Review

RoomKeyPMS does not expose a documented public WebSocket API. See [review.yml](review.yml) for the full findings - the API is request/response REST only (JSON or XML), with no Server-Sent Events or WebSocket transport documented anywhere in RoomKeyPMS's public materials.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
