# Paubox

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

Paubox is a HIPAA compliant, HITRUST certified email infrastructure company serving healthcare organizations in the United States. Its products encrypt outbound email without recipient portals, passwords, or plugins, and work alongside Google Workspace and Microsoft 365. The developer surface is three REST APIs on api.paubox.com — the Paubox Email API for transactional email (send, bulk send, message receipt, Handlebars dynamic templates, templated messages) with an SMTP relay alternative at smtp.paubox.com:587; the Paubox Marketing API for HIPAA compliant campaign mailings, drip campaigns, subscribers, subscription lists, tracking links and campaign analytics; and the Paubox Forms API for building, hosting and processing secure patient intake forms with public respondent endpoints and scoped management endpoints. Paubox publishes OpenAPI 3.0 definitions for all three, official SDKs for ten languages, a Node-based CLI, delivery webhooks, an llms.txt, an A2A agent card, a published Agent Skill, and a hosted MCP server at mcp.paubox.com exposing 30 tools across email, forms and marketing.

**Areas:** Email · HIPAA · Healthcare · Compliance · Transactional Email · Email Marketing · Forms · Security · Encryption · Messaging · A2A

## Paubox on APIs.io

Everything profiled for Paubox is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/paubox/](https://apis.io/providers/paubox/)** — or go straight to one of the APIs or properties below.

### APIs (13)

- [Paubox MCP Server](https://apis.io/apis/paubox/paubox-mcp-server/) — Hosted Model Context Protocol server exposing 30 Paubox tools across email, forms and email marketing to MCP-compatible AI clients. Reachable over…
- [Paubox Analytics API](https://apis.io/apis/paubox/paubox-analytics-api/) — Campaign analytics and reporting operations
- [Paubox Campaign Mailings API](https://apis.io/apis/paubox/paubox-campaign-mailings-api/) — Campaign mailing management and sending operations
- [Paubox Drip Campaigns API](https://apis.io/apis/paubox/paubox-drip-campaigns-api/) — Drip campaign management and automation operations
- [Paubox Dynamic Templates API](https://apis.io/apis/paubox/paubox-dynamic-templates-api/) — Manage and use dynamic Handlebars templates for email content
- [Paubox Form management API](https://apis.io/apis/paubox/paubox-form-management-api/) — Create, list, update, copy, and archive forms (requires API key)
- [Paubox Forms API](https://apis.io/apis/paubox/paubox-forms-api/) — Retrieve form definitions and accept submissions
- [Paubox Messages API](https://apis.io/apis/paubox/paubox-messages-api/) — Send individual or bulk transactional email
- [Paubox Submissions API](https://apis.io/apis/paubox/paubox-submissions-api/) — List and export form submissions (requires API key)
- [Paubox Subscribers API](https://apis.io/apis/paubox/paubox-subscribers-api/) — Subscriber management operations
- [Paubox Subscription Lists API](https://apis.io/apis/paubox/paubox-subscription-lists-api/) — Subscription list management operations
- [Paubox Subscriptions API](https://apis.io/apis/paubox/paubox-subscriptions-api/) — Subscriber opt-in and opt-out operations
- [Paubox Tracking Links API](https://apis.io/apis/paubox/paubox-tracking-links-api/) — Tracking link analytics and data operations

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Paubox Email Webhooks](https://apis.io/asyncapis/paubox/paubox-email-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Paubox MCP Server](https://apis.io/servers/paubox/paubox-mcp-server/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Paubox Agentic Access](https://apis.io/agentic-access/paubox/paubox-agentic-access/)

#### JSON Schema (51)

The data models the API reads and writes.

- [BulkCreateResponse](https://apis.io/schemas/paubox/paubox-bulk-create-response/)
- [BulkCreateSubscribersRequest](https://apis.io/schemas/paubox/paubox-bulk-create-subscribers-request/)
- [BulkDeleteCampaignMailingsRequest](https://apis.io/schemas/paubox/paubox-bulk-delete-campaign-mailings-request/)
- [BulkSendRequest](https://apis.io/schemas/paubox/paubox-bulk-send-request/)
- [BulkSendResponse](https://apis.io/schemas/paubox/paubox-bulk-send-response/)
- [BulkSubscriptionChangeRequest](https://apis.io/schemas/paubox/paubox-bulk-subscription-change-request/)
- [BulkSubscriptionChangeResponse](https://apis.io/schemas/paubox/paubox-bulk-subscription-change-response/)
- [CampaignAnalyticsResponse](https://apis.io/schemas/paubox/paubox-campaign-analytics-response/)
- [CampaignDeliveriesTableResponse](https://apis.io/schemas/paubox/paubox-campaign-deliveries-table-response/)
- [CampaignMailingWriteResponse](https://apis.io/schemas/paubox/paubox-campaign-mailing-write-response/)
- [CampaignMailingsResponse](https://apis.io/schemas/paubox/paubox-campaign-mailings-response/)
- [CampaignTableResponse](https://apis.io/schemas/paubox/paubox-campaign-table-response/)
- [CopyFormRequest](https://apis.io/schemas/paubox/paubox-copy-form-request/)
- [CreateCampaignMailingRequest](https://apis.io/schemas/paubox/paubox-create-campaign-mailing-request/)
- [CreateFormRequest](https://apis.io/schemas/paubox/paubox-create-form-request/)
- [CreateSubscriberRequest](https://apis.io/schemas/paubox/paubox-create-subscriber-request/)
- [CreateSubscriptionListRequest](https://apis.io/schemas/paubox/paubox-create-subscription-list-request/)
- [CreateSubscriptionRequest](https://apis.io/schemas/paubox/paubox-create-subscription-request/)
- [CreateSubscriptionResponse](https://apis.io/schemas/paubox/paubox-create-subscription-response/)
- [DetailedSubscriberResponse](https://apis.io/schemas/paubox/paubox-detailed-subscriber-response/)
- [DripCampaignResponse](https://apis.io/schemas/paubox/paubox-drip-campaign-response/)
- [DripCampaignsResponse](https://apis.io/schemas/paubox/paubox-drip-campaigns-response/)
- [DynamicTemplateListResponse](https://apis.io/schemas/paubox/paubox-dynamic-template-list-response/)
- [DynamicTemplateResponse](https://apis.io/schemas/paubox/paubox-dynamic-template-response/)
- [dynamic_templates_body](https://apis.io/schemas/paubox/paubox-dynamic-templates-body/)
- …and 26 more published on APIs.io

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Paubox Context](https://apis.io/jsonld/paubox/paubox-context/)

#### Overlays (15)

OpenAPI overlays, including conversational phrasing for each operation.

- [Paubox Analytics Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-analytics-api-phrasing-overlay/)
- [Paubox Campaign Mailings Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-campaign-mailings-api-phrasing-overlay/)
- [Paubox Drip Campaigns Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-drip-campaigns-api-phrasing-overlay/)
- [Paubox Dynamic Templates Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-dynamic-templates-api-phrasing-overlay/)
- [Paubox Email Api Overlay](https://apis.io/overlays/paubox/paubox-email-api-overlay/)
- [Paubox Form Management Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-form-management-api-phrasing-overlay/)
- [Paubox Forms Api Overlay](https://apis.io/overlays/paubox/paubox-forms-api-overlay/)
- [Paubox Forms Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-forms-api-phrasing-overlay/)
- [Paubox Marketing Api Overlay](https://apis.io/overlays/paubox/paubox-marketing-api-overlay/)
- [Paubox Messages Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-messages-api-phrasing-overlay/)
- [Paubox Submissions Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-submissions-api-phrasing-overlay/)
- [Paubox Subscribers Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-subscribers-api-phrasing-overlay/)
- [Paubox Subscription Lists Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-subscription-lists-api-phrasing-overlay/)
- [Paubox Subscriptions Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-subscriptions-api-phrasing-overlay/)
- [Paubox Tracking Links Api Phrasing Overlay](https://apis.io/overlays/paubox/paubox-tracking-links-api-phrasing-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Paubox API Rules](https://apis.io/rules/paubox/paubox-rules/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Paubox Authentication](https://apis.io/security/paubox/paubox-authentication/)
- [Paubox Domain Security](https://apis.io/security/paubox/paubox-domain-security/)
- [Paubox Trust Center](https://apis.io/security/paubox/paubox-trust-center/)
- [Paubox Vulnerability Disclosure](https://apis.io/security/paubox/paubox-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Paubox Plans Pricing](https://apis.io/plans/paubox/paubox-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Paubox Rate Limits](https://apis.io/rate-limits/paubox/paubox-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.paubox.com/)
- [Documentation](https://docs.paubox.com/welcome)
- [Getting started](https://docs.paubox.com/email-api/quickstart)
- [API reference](https://docs.paubox.com/email-api)
- [Pricing](https://www.paubox.com/pricing/paubox-email-api)
- [Sign up](https://www.paubox.com/pricing/paubox-email-api)
- [Support](https://support.paubox.com/)
- [Blog](https://www.paubox.com/blog)
- [Security](https://www.paubox.com/.well-known/security.txt)
- [Compliance](https://www.paubox.com/security)
- [Terms of service](https://www.paubox.com/terms-of-service)
- [Privacy policy](https://www.paubox.com/privacy-policy)
- [GitHub](https://github.com/Paubox)
- [Status](https://status.paubox.com/)

## API Evangelist rating

**Kin Score 77.0** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 73.5 |
| Contract governance | 35.6 |
| Operational transparency | 76.3 |
| Developer ergonomics | 78.6 |
| Access clarity | 92.1 |

**Agent readiness 60.9** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 32.0** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/paubox/](https://apis.io/providers/paubox/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Paubox: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/paubox/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
