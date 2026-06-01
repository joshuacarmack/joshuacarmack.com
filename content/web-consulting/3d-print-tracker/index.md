---
title: 3D Printing Tracker
showDate: false
showTaxonomies: false
showTableOfContents: true
---

## The Problem

After a while with a 3D printer, you accumulate a lot of prints — and a lot of questions. How much filament did that part actually use? What settings worked well for PETG on that printer? How much has this spool actually cost me? Why did that print fail last time?

I was keeping notes in a text file and trying to remember settings from print to print. It was not working.

## What I Built

A self-hosted web application for logging, searching, and analyzing 3D print jobs. Built for my own use, so it does exactly what I needed and nothing more.

### Print Log

Every print gets a log entry: printer, filament, material type, nozzle temp, bed temp, layer height, estimated vs. actual print time, weight of filament used, and a pass/fail/partial result. Notes field for anything else worth remembering.

### Filament Inventory

Spools are tracked in the system. When a print is logged with a specific spool, the weight used is deducted from the spool's remaining estimate. Running low on a material is visible at a glance.

### Cost Tracking

Each spool is logged with its purchase price and weight. The system calculates cost per gram and applies it to each print, so I have a running cost estimate per job and per project.

### Search and Filter

The full print history is searchable and filterable by printer, filament, material, date range, and result. Looking up what settings worked last time for a specific material on a specific printer takes seconds.

### Analytics

Summary views show total prints by month, filament consumption over time, failure rate by material, and cost totals. Mostly useful for satisfying curiosity, but occasionally genuinely helpful.

## Tech Stack

Built with Python (Flask) and SQLite, running in Docker on my home server. Simple HTML/CSS/JS frontend — no framework needed for a single-user tool. Data is backed up automatically with the rest of my homelab.

## Notes

This was built for personal use and is not a polished commercial product. But it scratches an itch that nothing off the shelf quite addressed for me, and it is a good example of the kind of purpose-built internal tooling I can build for clients who have a specific workflow problem to solve.

---

*Have a workflow problem that needs a custom tool? [Get in touch.](mailto:contact@joshuacarmack.com)*
