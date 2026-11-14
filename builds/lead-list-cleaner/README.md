# Build #1a: Lead List Cleaner & Issues Reporter (v1)

An n8n + Google Sheets data-hygiene pipeline built for small B2B agencies to clean, normalize, and deduplicate raw outbound lead lists before launching cold email campaigns.

## The Problem It Solves
Raw lead lists exported from scrapers or merged by hand usually contain formatting errors (`"  sARA  "`), messy job titles (`"chief executive officer"`), personal email addresses (`@gmail.com`), role-based inboxes (`info@`, `sales@`), and multiple contacts at the same company domain. Sending to raw lists hurts sender reputation and wastes daily sending caps.

Instead of silently deleting rows, this workflow separates campaign-ready contacts from problematic rows and generates an auditable **Issues Report** and **Executive Summary**.

## Architecture

```mermaid
flowchart LR
    A[("Google Sheets\n(Raw_Leads)")] --> B["n8n: Get Rows"]
    B --> C["JS Code Node:\nClean, Flag & Dedupe"]
    C --> D{"IF Node:\nstatus == 'clean'?"}
    C --> E["JS Code Node:\nBuild Summary Metrics"]
    D -- "True" --> F[("Cleaned Tab")]
    D -- "False" --> G[("Issues Tab\n(with issue_reason)")]
    E --> H[("Summary Tab")]
    I["Error Trigger"] --> J[("Error_Log Tab")]
