# Summit Leads — NPP Campaign Showcase

This folder contains the standalone source for the interactive New Paradigm Projects campaign showcase.

## Entry point

- `index.html` — responsive campaign showcase with playable video previews, linked static creatives, campaign-specific landing-page CTAs, and a clear demo-only notice.

## Landing-page routes expected on the Summit Leads portfolio

- Storm Damage: `/npp/storm-damage/`
- Preventative Roof Inspections: `/npp/preventative-roof-inspections/`
- Roof Repairs & Maintenance: `/npp/roof-repairs-maintenance/`

## Asset source

The showcase references the original video and image files in the campaign folders in this repository using GitHub raw-content URLs. The asset files are not duplicated.

## Demo safety

This showcase is a presentation layer only. It does not submit lead data to GoHighLevel, create contacts, reserve calendar slots, or send customer or salesperson notifications. The existing campaign landing pages provide the simulated qualification and booking flow.

## Deployment note

The showcase file is intended to be integrated into the Summit Leads portfolio site's source project at the route `/npp/campaign-showcase/`. Do not deploy this single file as the root of the existing portfolio: the portfolio contains other pages and routes that must remain in the deployment.
