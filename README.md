# Mailmodo (mailmodo)

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

Mailmodo is an AI-powered interactive email marketing and automation platform headquartered in Bengaluru with a presence in San Francisco. It pioneered AMP-for-Email at scale, letting brands embed forms, quizzes, polls, carousels, and calendars directly inside the inbox to drive engagement and conversions without a landing-page round-trip. The platform layers AI assistance on top of campaigns, journeys, segmentation, and analytics, and exposes a REST API for contact management, transactional sends, broadcast and bulk triggers, custom event ingestion, and campaign reporting.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- Email
- Interactive Email
- AMP for Email
- Marketing Automation
- Transactional Email
- Campaigns
- Journeys
- Customer Engagement

## Timestamps

- **Created:** 2026-05-25
- **Modified:** 2026-05-25

## APIs

### Mailmodo REST API

REST API for managing contacts, contact lists, custom events, campaigns, templates, and campaign reports. Used to drive transactional sends, bulk triggers, journey enrollment, and AMP-for-Email interactive campaigns. Authentication is via an API key issued from the Mailmodo dashboard and passed in the `mmApiKey` request header.

- **Human URL:** [https://www.mailmodo.com/developers/](https://www.mailmodo.com/developers/)
- **Base URL:** `https://api.mailmodo.com`

#### Tags

- Email
- Contacts
- Campaigns
- Templates
- Events
- AMP for Email

#### Properties

- [Documentation](https://www.mailmodo.com/developers/)
- [API Reference](https://developers.mailmodo.com/)
- [Quickstart](https://www.mailmodo.com/developers/8e957152b6128-getting-started-with-mailmodo-api/)
- [Authentication](https://manage.mailmodo.com/app/settings/apikey)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/openapi/mailmodo-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-schema/mailmodo-contact-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-schema/mailmodo-campaign-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-schema/mailmodo-template-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-schema/mailmodo-event-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-structure/mailmodo-contact-structure.json)
- [JSON Structure](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-structure/mailmodo-campaign-structure.json)
- [J S O N- L D](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/json-ld/mailmodo-context.jsonld)
- [Example](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/examples/mailmodo-trigger-campaign-example.json)
- [Example](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/examples/mailmodo-add-contact-example.json)
- [Example](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/examples/mailmodo-add-event-example.json)
- [Rate Limits](https://www.mailmodo.com/pricing/)
- [Postman Collection](collections/mailmodo.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/mailmodo.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Website](https://www.mailmodo.com)
- [Documentation](https://www.mailmodo.com/developers/)
- [API Reference](https://developers.mailmodo.com/)
- [Support](https://support.mailmodo.com/)
- [Sign Up](https://manage.mailmodo.com/auth/signup)
- [Portal](https://manage.mailmodo.com/)
- [Console](https://manage.mailmodo.com/app/settings/apikey)
- [Pricing](https://www.mailmodo.com/pricing/)
- [Terms of Service](https://www.mailmodo.com/gdpr/termsandconditions/)
- [Privacy Policy](https://www.mailmodo.com/gdpr/privacypolicy/)
- [Blog](https://www.mailmodo.com/blog/)
- [GitHub Organization](https://github.com/mailmodo)
- [GitHub Repository](https://github.com/mailmodo/mailmodo-mcp)
- [Spectral Rules](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/rules/mailmodo-rules.yml)
- [Vocabulary](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/vocabulary/mailmodo-vocabulary.yml)
- [Plans](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/plans/mailmodo-plans-pricing.yml)
- [Rate Limits](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/rate-limits/mailmodo-rate-limits.yml)
- [Fin Ops](https://raw.githubusercontent.com/api-evangelist/mailmodo/refs/heads/main/finops/mailmodo-finops.yml)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)
- [Solutions](undefined)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
