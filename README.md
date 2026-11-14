# n8n Workflows

Exported n8n workflows I build while learning and shipping automation for B2B agencies.

## Rules
- Credentials never go in Git. Every export is checked for keys, tokens and personal emails before commit.

## Workflows

| Workflow | What it does | Status |
| :--- | :--- | :--- |
| `lead-intake-practice` | Cleans and scores a lead sent to a webhook, returns a tier or a list of errors | Working |
| [`lead-list-cleaner`](builds/lead-list-cleaner/) | Reads a messy lead sheet, normalizes names/titles/domains, dedupes by domain, and routes bad rows (`gmail`, `info@`, missing titles, duplicates) to an Issues tab with summary metrics | Working |

## Structure
- `builds/` : exported workflow JSON files and project documentation
- `notes/` : short learning notes
