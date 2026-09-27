# Retail Procurement System

**[Try the live demo →](https://script.google.com/macros/s/AKfycbxEbC171UpwwwNuAp_61v4qCw_1DJiqk5va4E1D-i2T4LddPTAL6XEKHtl7NrKtSQIi/exec)**

## TL;DR

This is a simulated retail inventory and procurement system, built to show how a lean team can move from raw sales data to approved purchase orders — automatically, with just enough human review built in.

It covers the full loop: tracking stock, flagging what needs to be reordered, moving inventory between a warehouse and stores, applying supplier discounts, and running purchase orders through a two-stage approval process. Everything runs inside a simple control panel, with no spreadsheet visible to the end user.

I built this after running into the same problem in a real, rapidly growing 10-store operation with no budget for an ERP and no clear path to getting one. This approach helped me to cut stockouts by 90% and improve purchasing margins by 5% in that real operation. This project, albeit with completely fictional data, showcases that ideology from the ground up, as a hands-on demonstration of it.

Built using Google Sheets, Apps Script, and AI (Claude, ChatGPT and Gemini) as a development partner throughout.

Read the full case study below for the constraints, the decision to build it myself, and how the system actually works.
---

## Table of Contents

- [The Situation](#the-situation)
- [The Constraint](#the-constraint)
- [The Decision to Build](#the-decision-to-build)
- [What It Does](#what-it-does)
  - [Data](#data)
  - [Transfers](#transfers)
  - [Purchasing](#purchasing)
- [What the Production Tool Would Look Like](#what-the-production-tool-would-look-like)
- [Results](#results)
- [This Portfolio Version](#this-portfolio-version)
- [What's Next](#whats-next)
---
## The Situation

I managed operations for a retail company running 10 stores and one central warehouse, carrying over 10,000 SKUs and buying from 30+ suppliers. The business was growing fast — new stores opening, more products added, more suppliers coming on board — and the systems tracking all of it hadn't grown with it.

Stock levels lived in spreadsheets that different people updated at different times. Reorder decisions were made by whoever noticed a shelf was empty, not by any consistent logic. Purchase orders were built manually, supplier by supplier, with no structured way to check whether a discount threshold had been hit or a promotion was worth stocking up for. None of this scaled to 10 stores and 10,000+ SKUs without someone spending most of their week just keeping the numbers straight.

## The Constraint

The obvious fix was an ERP system — something built to handle inventory, procurement, and purchasing end to end. But a small, rapidly growing retail company doesn't have enterprise software money, and it doesn't have an IT department to run an implementation either. Most ERP platforms assume both.

Even setting cost aside, the timeline didn't work. Implementations run months, not weeks, and the business needed something working now, not after a quarter of vendor selection and configuration. There also wasn't a clear internal owner for "go find us a system" — no one on the team had done an ERP rollout before, and hiring a consultant to scope one out was its own budget problem.

So the choice came down to two options: keep running the same manual process and absorb the cost in time, errors, and stockouts, or build something in-house using tools the company already had.

## The Decision to Build

I chose to build it myself, using Google Sheets and Apps Script — tools already available, with no new licensing cost and no vendor dependency. Google Sheets could hold the data; Apps Script could turn that data into logic: calculating reorder points, generating transfer requests, building purchase orders, and routing approvals, all without needing a database or a dedicated dev team.

AI tools (Claude, ChatGPT, and Gemini) were a genuine part of how this got built, not just a footnote. I'm not a software engineer by training — my background is operations. AI let me translate what I understood operationally (safety stock logic, approval workflows, supplier discount structures) into working code, faster than learning to write all of it from scratch, and without needing to hand the project to someone else.

## What It Does

The system covers three connected phases, each solving a specific part of the problem.

### Data

Everything starts with knowing what's actually in stock and what needs to be reordered. The system tracks stock levels per item, per location, and calculates safety stock and reorder points by analyzing consumption patterns over time — accounting for how fast something sells and how long it takes a supplier to deliver it. This replaced a process where reorder decisions were reactive (someone notices a shelf is empty) with one that's calculated ahead of time.

### Transfers

Before ordering anything new from a supplier, the system checks whether the warehouse already has stock that could go to a store that needs it. It allocates available warehouse stock across stores based on actual need and urgency — not first-come-first-served — so nothing sits in the warehouse while a store runs out. A manager reviews and approves or rejects each transfer before it's finalized, so the system recommends but doesn't act unilaterally.

### Purchasing

For whatever isn't covered by a transfer, the system generates purchase orders — checking supplier pricing, applying volume discounts where thresholds are met, and padding orders where it makes sense to take fuller advantage of a supplier agreement. Purchase orders go through a two-stage approval: a store or purchasing team member requests approval, then a purchasing manager signs off (or sends it back for changes) before anything is finalized. This built in a real checkpoint, rather than letting purchasing decisions happen without oversight.

## What the Production Tool Would Look Like

A few things about this system would work differently in an actual production deployment, as opposed to this portfolio demonstration:

- **No manual data refresh.** In production, historical data wouldn't need to be regenerated — the system would already hold prior months of real data, with current-week POS data uploaded on a regular basis instead.
- **Stock counts from barcode scans, not simulation.** Current stock would come from barcode-scan data uploaded per store location, and the system would calculate stock levels automatically from that, rather than relying on a simulated ledger.
- **A closed loop.** Approved purchase orders would update stock automatically as they're received, and reorder recommendations would continuously adjust based on how each store is actually performing — rather than running as a one-way, start-to-finish process.
- **Authentication and roles.** The current build assumes a small, known team, so there's no login or role-based access layer yet. That's a natural next step for a production rollout, not a gap in the underlying design.

## Results

This approach — automated reorder logic, warehouse-to-store transfers based on real need, and structured purchasing with built-in approval — cut critical stockouts by 90%, from 10 to 1 per store monthly, and improved purchasing margins by 5%, delivering over $40,000 in annual savings, in the real 10-store operation this was built for.

## This Portfolio Version

This build uses entirely fictional data — a simulated 12-month transaction history across 10 stores and one warehouse, generated to reflect realistic patterns (including a handful of items running genuinely short, so the reorder and transfer logic has something real to respond to). It exists to let anyone evaluating this work see and use the actual system, rather than just reading a description of one.

## What's Next

A Purchasing Analysis dashboard is in progress — built for management, to show how well the system is taking advantage of supplier agreements to improve margins, giving the relevant people visibility into exactly where those savings are coming from.
