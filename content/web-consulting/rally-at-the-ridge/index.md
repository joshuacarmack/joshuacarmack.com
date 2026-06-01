---
title: Rally at the Ridge — Car Show Management System
showDate: false
showTaxonomies: false
showTableOfContents: true
---

## The Problem

Running a car show involves a lot of moving parts — and for a long time, most of them were handled with paper forms, spreadsheets, and a lot of manual work the day of the event. Entry lists had to be printed in advance, check-in was done by searching through stacks of paper, class assignments were tracked in Excel, and judging results were tallied by hand.

The result was a process that was stressful to run, slow for participants, and prone to errors.

## What I Built

Rally at the Ridge is a full-stack web application built to handle every stage of the car show workflow — before, during, and after the event.

### Pre-Registration

Participants register their vehicles online before the event. The registration form collects vehicle details, owner contact information, and class preference. Entries are stored in a database and confirmation emails are sent automatically. Coordinators can view and manage registrations from an admin dashboard.

### Day-of Check-in

When participants arrive at the show, check-in staff can look them up by name, confirmation number, or vehicle details. Pre-registered participants are checked in with a few clicks. Walk-up registrations are also handled in the same system. Class assignments are confirmed or adjusted at check-in, and each vehicle gets a printed number placard generated from the system.

### Class and Entry Management

The admin dashboard gives organizers full visibility into all entries, organized by class. Entries can be moved between classes, flagged, or noted by staff. The system handles the count and display logic so judges always have an accurate roster.

### Judging

Judges work from a view of their assigned class, marking their top picks directly in the application. The system aggregates results as judging proceeds, giving organizers a live picture of where each class stands without waiting for judges to turn in paper ballots.

### Awards

When judging is complete, the awards view displays winners by class. Organizers can mark awards as given, track remaining awards, and generate a final results summary.

## Tech Stack

Built with a PHP backend, MySQL database, and a straightforward HTML/CSS/JS frontend optimized for use on tablets and phones in the field. Deployed on a VPS with a simple admin login system.

## The Result

The switch from paper to this system cut check-in times significantly, eliminated the class-assignment confusion that had been an annual headache, and gave the organizing team real-time visibility into the event that they had never had before. Judges liked being able to work from their phones rather than carrying clipboards, and getting results at the end of the night was fast.

---

*Interested in something similar for your event? [Get in touch.](mailto:contact@joshuacarmack.com)*
