# Summit Leads — NPP Campaign Showcase

This folder contains the source and handoff notes for the interactive New Paradigm Projects campaign demonstration.

## Live demo

- Campaign showcase: https://npp-campaign-showcase.vercel.app/
- Summit Leads portfolio: https://summit-leads-website-portfolio.vercel.app/

The showcase is deployed as a small standalone Vercel project because the existing portfolio's original source repository is not connected/available in the current deployment workspace. This keeps the existing portfolio deployment intact.

## Existing campaign landing pages

- Storm Damage Roof Inspections: https://summit-leads-website-portfolio.vercel.app/npp/storm-damage/
- Preventative Roof Inspections: https://summit-leads-website-portfolio.vercel.app/npp/preventative-roof-inspections/
- Roof Repairs & Maintenance: https://summit-leads-website-portfolio.vercel.app/npp/roof-repairs-maintenance/

## Source files

- `npp-campaign-showcase/index.html` — responsive campaign showcase with playable video previews, linked static creatives, campaign-specific landing-page CTAs, and a demo-only notice.
- `DAVID-DEMO-GUIDE.md` — suggested demo sequence, qualification rules, test cases, and safety notes.

## Asset source

The showcase references original video and image files in the campaign folders in this repository using GitHub raw-content URLs. The media files are not duplicated.

## Demo safety

The showcase and campaign landing pages are presentation/demo only. They do not submit lead data to GoHighLevel, create contacts, reserve real calendar slots, or send customer or salesperson notifications. A sample booking confirmation is not a live appointment.

## Integration note

The showcase is currently deployed at its own Vercel URL and links directly to the existing Summit Leads landing pages. It has not been inserted into the Summit Leads portfolio homepage/navigation because the original portfolio source repository has not yet been identified. Do not replace the existing portfolio deployment with a single-file deployment.
