---
name: Paubox
description: Use when building HIPAA-compliant email, marketing campaigns, or secure intake forms. Reach for this skill when agents need to send transactional email, manage subscriber lists, collect patient data via forms, check delivery status, or integrate Paubox into applications via REST API, SMTP, SDKs, CLI, or MCP Server.
metadata:
    mintlify-proj: paubox
    version: "1.0"
---

# Paubox Skill

## Product summary

Paubox is a HIPAA-compliant, HITRUST-certified email and forms platform for healthcare. It provides transactional email (Email API), marketing campaigns (Marketing API), secure intake forms (Forms API), and command-line tools (CLI and MCP Server) for sending encrypted email, managing subscriber lists, collecting patient data, and checking delivery status. All APIs use Bearer token authentication with API keys generated per domain. Base URLs: `https://api.paubox.com/v1/email` (Email API), `https://api.paubox.com/v1/marketing` (Marketing API), `https://api.paubox.com/v1/forms` (Forms API). Official SDKs exist for C#, Go, Java, Node.js, Perl, PHP, Python, Rails, Ruby, and Rust. See [Paubox documentation](https://docs.paubox.com) for complete reference.

## When to use

Use this skill when:
- **Sending transactional email**: appointment reminders, password resets, delivery notifications, care instructions
- **Managing marketing campaigns**: drip sequences, newsletters, bulk sends to subscriber lists
- **Collecting patient data**: intake forms, consent forms, surveys, waivers via secure HIPAA-compliant forms
- **Checking delivery status**: tracking message opens, bounces, failures via tracking IDs
- **Integrating Paubox into applications**: via REST API, SMTP, language-specific SDKs, CLI, or MCP Server
- **Automating healthcare workflows**: CI/CD pipelines, AI agents, scheduled tasks
- **Ensuring HIPAA compliance**: all Paubox services are HIPAA-compliant with BAA included

## Quick reference

### Authentication

| Method | Format | Use case |
|--------|--------|----------|
| **Email API** | `Authorization: Bearer YOUR_API_KEY` | REST API calls to send email, check status, manage templates |
| **Email API (legacy)** | `Authorization: Token token=YOUR_API_KEY` | Older integrations (Bearer preferred) |
| **Marketing API** | `Authorization: Token token=YOUR_API_KEY` | Campaigns, subscribers, analytics |
| **Forms API** | `Authorization: Bearer YOUR_API_KEY` with `forms` scope | Form management endpoints only |
| **SMTP** | Username: `apikey`, Password: `YOUR_API_KEY` | SMTP relay at `smtp.paubox.com:587` |

### Email API endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/messages` | POST | Send a single email |
| `/bulk_messages` | POST | Send up to 50 emails in one request |
| `/message_receipt` | GET | Check delivery status by tracking ID |
| `/dynamic_templates` | POST/GET/PUT/DELETE | Create, retrieve, update, delete Handlebars templates |
| `/templated_messages` | POST | Send email using a stored template |

### CLI commands

| Command | Purpose |
|---------|---------|
| `paubox send` | Send a single email with optional attachments |
| `paubox status <trackingId>` | Check delivery and open status |
| `paubox forms get <formId>` | Fetch form metadata |
| `paubox forms submit <formId>` | Submit form response with optional attachments |
| `paubox auth login` | Store API key in OS keychain |
| `paubox config set defaultFrom <email>` | Set default sender address |

### Sending limits

| Limit | Value |
|-------|-------|
| Max recipients per message | 100 |
| Max attachment size (total per message) | 50 MB |
| Bulk messages (recommended max per request) | 50 |
| SMTP rate limit | 500 messages per minute per IP |

### Common HTTP status codes

| Code | Meaning | Action |
|------|---------|--------|
| `200` | Success | Message accepted for delivery |
| `400` | Bad Request | Check: verified domain, required fields, base64 attachments |
| `401` | Unauthorized | Verify API key and Authorization header format |
| `422` | Unprocessable Entity | Unverified `from` domain or semantic error |
| `429` | Rate Limited | Back off and retry; use bulk endpoint for high volume |
| `500, 502, 503, 504` | Server Error | Retry with exponential backoff |

## Decision guidance

### When to use Email API vs Marketing API

| Need | Use Email API | Use Marketing API |
|------|---------------|-------------------|
| Send transactional email (password reset, appointment reminder) | ✓ | |
| Send to a single recipient or small list | ✓ | |
| Send bulk campaigns to subscriber lists | | ✓ |
| Track opt-ins and opt-outs | | ✓ |
| Use dynamic templates with Handlebars | ✓ | |
| Manage subscribers and subscriptions | | ✓ |
| Get campaign analytics (opens, clicks) | | ✓ |

### When to use REST API vs SMTP vs SDK

| Scenario | Use REST API | Use SMTP | Use SDK |
|----------|-------------|---------|--------|
| Sending from application code | ✓ | ✓ | ✓ (preferred) |
| Sending from terminal or CI/CD | | | ✓ (use CLI) |
| Existing SMTP integration | | ✓ | |
| Need language-specific error handling | | | ✓ |
| Simple one-off sends | ✓ | | |

### When to use Forms API vs Email API

| Need | Use Forms API | Use Email API |
|------|---------------|---------------|
| Collect patient intake data | ✓ | |
| Collect signatures | ✓ | |
| Send email to recipients | | ✓ |
| Embed form in application | ✓ | |
| Export submissions as CSV/PDF | ✓ | |

## Workflow

### Sending a transactional email via REST API

1. **Verify your domain**: Go to Paubox dashboard > Settings > Domains, add your domain, add the SPF record to your DNS provider, verify.
2. **Generate an API key**: Settings > API Keys, click your domain, Add API Key, copy immediately (displayed once only).
3. **Construct the request**: Build JSON with `recipients`, `headers` (subject, from), and `content` (text/plain and/or text/html).
4. **Include authentication**: Add `Authorization: Bearer YOUR_API_KEY` header.
5. **Send the request**: POST to `https://api.paubox.com/v1/email/messages`.
6. **Save the tracking ID**: Response includes `sourceTrackingId`; store it to check delivery status later.
7. **Verify delivery**: Use the tracking ID with `GET /message_receipt` to check status (delivered, opened, failed, pending).

### Sending email via CLI

1. **Install**: `npm install -g paubox-cli`
2. **Authenticate**: `paubox auth login`, enter your API key (stored in OS keychain).
3. **Send**: `paubox send --to recipient@example.com --from sender@yourdomain.com --subject "Hi" --text "Hello"` or `--html "<p>Hello</p>"`.
4. **Check status**: `paubox status <trackingId>` (from send output).
5. **Optional**: Set default sender with `paubox config set defaultFrom sender@yourdomain.com` to omit `--from` on future sends.

### Sending bulk email

1. **Prepare a list**: Array of up to 50 message objects, each with recipients, headers, content.
2. **POST to bulk endpoint**: `POST /bulk_messages` with the same authentication and base structure as single sends.
3. **Track individually**: Each message in the response includes its own `sourceTrackingId`; store all to track delivery.
4. **For higher volume**: Loop over batches of 50 rather than sending all at once.

### Creating and sending a marketing campaign

1. **Create a campaign mailing**: POST to `/marketing/campaign_mailings` with subject, html_part, text_part.
2. **Save the ID**: Response includes the mailing ID (UUID).
3. **Send a test**: GET `/campaign_mailings/{id}/send_test_email?to_email=you@example.com` to preview rendering.
4. **Create or select a list**: Either a subscription list (explicit membership) or dynamic list (filter-based).
5. **Send or schedule**: POST to `/campaign_mailings/{id}/send` (now) or `/schedule` (future time) with the list ID.
6. **Track progress**: Use analytics endpoints (`/analytics/campaigns`, `/analytics/deliveries`) to measure opens, clicks, bounces.

### Collecting patient data via Forms API

1. **Create a form**: POST to `/api/forms` with title, description, form_json (JSON schema), form_html, form_css, or create in dashboard.
2. **Get the form ID**: Response includes the UUID.
3. **Render the form**: GET `/public/form_data/{form_id}` (no auth required) to retrieve HTML, schema, CSS for client-side rendering.
4. **Accept submissions**: POST to `/api/forms/{form_id}/submissions` (no auth required) with form_data (key-value pairs) and optional attachments.
5. **Retrieve submissions**: GET `/api/forms/{form_id}/submissions` (requires auth with forms scope) to list all responses.
6. **Export**: GET `/api/forms/{form_id}/submissions/submission-csv` or `/submission-pdf` to export as CSV or PDF.

### Using dynamic templates

1. **Create a template**: Upload a `.hbs` file with Handlebars syntax (variables, conditionals, loops) via POST `/dynamic_templates`.
2. **Name it**: The `data[name]` value becomes the template identifier.
3. **Send templated messages**: POST to `/templated_messages` with template_name, template_values (JSON string), and message (recipients, headers).
4. **Update or delete**: Use PUT or DELETE on `/dynamic_templates/{id}` to modify or remove templates.

## Common gotchas

- **API key exposed**: Never commit API keys to source control. Use environment variables or secrets managers. If exposed, generate a new key immediately and revoke the old one.
- **Unverified domain**: Sending from a domain not verified in Settings > Domains always returns 400 Bad Request. Verify SPF record propagation (up to 48 hours).
- **Missing required fields**: Email requires `recipients` (non-empty array), `headers.subject`, `headers.from`, and at least one of `content.text/plain` or `content.text/html`. Missing any returns 400.
- **Base64 attachment encoding**: Attachment `content` must be valid base64. Invalid encoding returns 400. Use SDK helpers to encode files automatically.
- **Template values as string**: When sending templated messages, `template_values` must be a JSON-encoded **string**, not a JSON object. Stringify before including in request.
- **Marketing API errors in 200 response**: Marketing API write endpoints (create, update campaign) return 200 OK even on validation failure; check the `errors` key in the response body, not just the status code.
- **Webhook retries**: Paubox does not retry failed webhook deliveries. If your endpoint is down, notifications are lost. Use polling with `/message_receipt` as a fallback.
- **Forms scope required**: Forms API management endpoints require an API key with the `forms` scope. A key without it returns 401. Public endpoints (get form, submit) require no auth.
- **Rate limits**: Email API has per-plan rate limits; 429 Too Many Requests means back off. SMTP has a 500 messages/minute per IP limit. Use bulk endpoint for high volume.
- **Subscription list vs dynamic list**: Subscription list membership is explicit (you add/remove subscribers). Dynamic list membership is computed from filters. Use the correct bulk endpoint (`bulk_global_*` vs `dynamic_bulk_*`).
- **Global vs list-level opt-out**: Marketing API has two levels: list-level (unsubscribe from one list) and global (opt out of everything). Treat global opt-out as permanent unless the recipient requests resubscription.
- **SMTP password with newlines**: When pasting a base64-encoded API key into SMTP config, check for stray spaces or line breaks. SMTP is line-based; even a newline breaks authentication.

## Verification checklist

Before submitting work with Paubox:

- [ ] **API key is valid**: Test with a simple request (e.g., `paubox auth login` or a test email send).
- [ ] **Domain is verified**: Check Settings > Domains; SPF record is added to DNS and verified.
- [ ] **Sender address matches verified domain**: The `from` address must belong to a domain you verified.
- [ ] **Required fields present**: Email requires recipients, subject, from, and at least one content type (text/plain or text/html).
- [ ] **Attachments are base64-encoded**: If including attachments, verify content is valid base64 and total size ≤ 50 MB.
- [ ] **Template values are JSON strings**: For templated messages, `template_values` is a stringified JSON object, not a raw object.
- [ ] **Tracking ID saved**: After sending, store the `sourceTrackingId` to check delivery status later.
- [ ] **No PHI in public threads**: Never post patient data, recipient addresses, or message content in GitHub discussions. Use support@paubox.com for sensitive issues.
- [ ] **Credentials not in source control**: API keys are in environment variables or secrets manager, not hardcoded.
- [ ] **Error handling in place**: Check response status and `errors` key (for Marketing API) to detect failures.
- [ ] **Rate limits respected**: For high volume, use bulk endpoint (max 50 per request) and respect SMTP 500/minute limit.

## Resources

- **Full documentation**: [https://docs.paubox.com/llms.txt](https://docs.paubox.com/llms.txt) — comprehensive page-by-page navigation for all APIs, SDKs, and tools.
- **Email API reference**: [https://docs.paubox.com/email-api](https://docs.paubox.com/email-api) — base URL, authentication, conventions, and all endpoints.
- **Marketing API reference**: [https://docs.paubox.com/marketing](https://docs.paubox.com/marketing) — campaigns, subscribers, subscriptions, analytics.
- **Forms API reference**: [https://docs.paubox.com/forms/index](https://docs.paubox.com/forms/index) — form management, submissions, exports.

---

> For additional documentation and navigation, see: https://docs.paubox.com/llms.txt