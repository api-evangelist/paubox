---
name: paubox-collect-form-submissions
description: >-
  Retrieve a Paubox Form definition, submit a respondent's answers, and read or export the
  resulting submissions. Use when an agent runs a patient intake, consent or survey
  conversation and must land the answers in a HIPAA compliant store.
api: Paubox Forms API
base_url: https://api.paubox.com/v1/forms
operations:
  - getPublicForm
  - createFormSubmission
  - listForms
  - getForm
  - listFormSubmissions
  - exportSubmissionsCsv
  - exportSubmissionCsv
  - exportSubmissionPdf
  - getFormStats
source: openapi/paubox-forms-api-openapi.yaml
generated: '2026-08-26'
method: generated
---

# Collect and read Paubox Form submissions

## Two tiers of endpoint

The Forms API is split, and the split is load-bearing for an agent:

- **Public respondent endpoints** — `getPublicForm` and `createFormSubmission` — take
  **no credential at all**. The form's UUID *is* the access control. An agent can render
  and submit a form knowing only the form ID.
- **Management endpoints** — everything else — require a Paubox API key that carries the
  `forms` scope, sent as `Authorization: Bearer YOUR_API_KEY`. A key scoped only to the
  Email API is rejected with `401`. The Forms API does **not** accept the `Token token=`
  header used by the Marketing API.

## Running an intake conversation

1. **Fetch the form** — `getPublicForm` (`GET /public/form_data/{form_id}`). Returns the
   full definition: HTML, JSON schema and CSS. Read the JSON schema to know which fields
   exist and which are required, and ask the respondent for exactly those.
2. **Submit the answers** — `createFormSubmission`
   (`POST /api/forms/{form_id}/submissions`). On success the service stores the
   submission, increments the form's submission count, emails any configured recipients,
   and returns **`201` with no body**. Do not expect a submission ID back.

## Reading submissions afterwards (authenticated)

- `listFormSubmissions` (`GET /api/forms/{form_id}/submissions`) is paginated. Each
  submission's `form_data` is a **JSON-encoded string**, not an object — parse it before
  using it.
- `exportSubmissionsCsv` returns every submission as a CSV attachment (`form_data.csv`),
  first column "Created At" then one column per field label.
- `exportSubmissionCsv` and `exportSubmissionPdf` do the same for a single submission; the
  PDF includes signature images for signable forms.
- `getFormStats` returns active form count, total submissions, and submissions in the last
  7 days.

## Managing forms

`listForms`, `createForm`, `updateForm` (partial — omitted fields are left unchanged),
`copyForm` (new title, submission count resets to 0, no vanity URL), `archiveForm`,
`unarchiveForm`.

## Traps the docs call out explicitly

- **`archiveForm` and `unarchiveForm` do not verify the form exists.** An unknown form ID
  still returns `200`. A `200` from these two operations is **not** evidence the form was
  found. Confirm with `getForm` if the outcome matters.
- **`unarchiveForm` does not reactivate.** Archiving sets `active` to `false`;
  unarchiving leaves `active` false. To make the form accept submissions again you must
  also call `updateForm` with `active: true`. This is the reversal path for archiving and
  it takes two calls, not one.
- `403` on a management endpoint means the key is valid but the resource belongs to a
  different customer — not a scope problem.
