# RoomKeyPMS (roomkeypms)

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
