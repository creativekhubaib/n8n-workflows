# Lead Intake (practice workflow)

**Status:** practice workflow, built to learn n8n. Not a client product.

## What it does
This workflow receives incoming lead data via a webhook, cleans the formatting, and validates required fields (name, email, company, and headcount). Valid leads are scored based on team size, job title, and business email domain, then assigned a priority tier (`hot`, `warm`, or `cold`) and a recommended next action. The cleaned, scored lead—or a list of validation errors—is returned immediately in the webhook response.[cite: 1]

## How it works
1. **Webhook:** Listens for incoming `POST` requests at `/lead-intake`.
2. **Clean and Score (Code):** Formats text fields (e.g., title-casing names, lowercasing emails), checks for missing or invalid data, and calculates a score out of 100 based on ICP criteria.
3. **Is Valid? (IF):** Checks if the lead passed all validation rules (`valid === true`).
4. **Add Tier (Set):** *(True branch)* Assigns a `tier` (`hot`, `warm`, `cold`) and a `next_action` based on the calculated score.
5. **Respond OK / Respond Error:** Returns a `200` JSON response with the enriched lead data, or a `400` JSON response listing what failed validation.[cite: 1, 2]

## What it doesn't do yet
* No CRM or database sync (data is only returned in the HTTP response)
* No duplicate lead detection
* No Slack or email notifications for hot leads
* No error alerting or webhook authentication[cite: 1]

## Setup
1. Import `lead-intake-practice.json` in n8n[cite: 1]
2. Activate the workflow or click **Test workflow** (no external credentials are needed)[cite: 1]
3. Send a `POST` request to the webhook URL using the sample input below[cite: 1]

## Sample input / output

**Sample Input (`POST /lead-intake`):**
```json
{
  "name": "  sara khan ",
  "email": "Sara@AcmeTech.io",
  "company": "Acme Tech",
  "title": "Head of Growth",
  "headcount": 25
}
