---
layout: page
title: Synodi
description: The trip and the tab, together in one app. A trip companion and expense splitter for iOS and Android.
img: /assets/img/synodi_logo.png
redirect:
importance: 1
category: Synodi
related_publications: false
---

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/synodi_logo.png" title="Synodi" alt="Synodi logo" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

[Synodi](https://synodi.app) is a mobile app I founded and built that brings the trip and the tab together in one place. Most expense splitters only care about the money; Synodi is built around the trip itself, so planning, splitting, and settling up all live alongside each other.

**What it does**

- **Trips with a look of their own** — every trip gets its own page, its own ledger, and its own theme, colors, and fonts.
- **Multi-currency support** — log expenses in whatever currency you paid in; each one converts to the trip's base currency at entry, so balances and settlements always stay in one clear number.
- **Fair splits, including lodging** — split evenly, or split lodging by nights stayed so the person who left early pays only their share.
- **Settlement, simple or detailed** — one clean answer to "who owes who," with a full breakdown behind it, settled either traditionally or with simplified (minimum-transaction) payments.
- **Receiver-confirmed payments** — payments count once the person receiving them confirms, and everyone is notified when money moves.

**How it's built**

Synodi is a React Native (Expo) app in a pnpm monorepo, backed by Supabase (Postgres, Auth, Storage, Realtime, and Edge Functions) with row-level security on every table. All money is stored as integer cents, and the settlement plan is always derived from the underlying expenses rather than stored, so balances always sum to zero. The marketing site is built with Next.js and Tailwind and deployed on Vercel.

<div class="d-flex flex-wrap justify-content-center mt-4 mb-4" style="gap: 1rem;">
  <a class="btn btn-theme btn-lg" href="https://synodi.app" target="_blank" rel="noopener"><i class="fa-solid fa-globe"></i>&nbsp; Visit synodi.app</a>
  <a class="btn btn-theme btn-lg" href="https://apps.apple.com/us/app/synodi/id6804848840" target="_blank" rel="noopener"><i class="fa-brands fa-apple"></i>&nbsp; Download on the App Store</a>
  <a class="btn btn-theme btn-lg" href="https://play.google.com/store/apps/details?id=com.synodi.app" target="_blank" rel="noopener"><i class="fa-brands fa-google-play"></i>&nbsp; Get it on Google Play</a>
</div>
