# 🚗 Car Search Tracker

A personal web app for tracking cars during a used car search — built to live on GitHub Pages with your data stored directly in this repo as `cars.json`.

## What it does

When you're shopping for a used car across AutoTrader, Facebook Marketplace, and dealer sites, it's easy to lose track of which Carfax belongs to which listing, which ones you've already ruled out, and which are still worth pursuing. This app keeps everything in one place.

**Per car, you can track:**
- Year, make, model, trim
- Price and mileage
- Dealer or private seller
- Listing URL
- Carfax status (clean / accident / salvage / lemon)
- Reported damage amount
- Provinces previously registered in (Quebec is flagged automatically ⚠)
- Number of owners and service records
- Any other Carfax flags (odometer issues, US history, fleet use, etc.)
- Your own notes

**Views:** toggle between a card view (good for browsing) and a table view (good for comparing).

**Statuses:** mark cars as Active, Favourite, Pending, or Ruled Out. Ruled-out cars are dimmed and hidden by default so they don't clutter your view — but they're never deleted.

## Setup

### 1. Fork or clone this repo

Make it public (required for free GitHub Pages).

### 2. Enable GitHub Pages

Repo → **Settings** → **Pages** → Source: `Deploy from branch` → branch: `main`, folder: `/ (root)` → Save.

Your app will be live at `https://yourusername.github.io/your-repo-name/` within a minute.

### 3. Get a GitHub personal access token

Go to [github.com/settings/tokens/new](https://github.com/settings/tokens/new):
- Give it a name (e.g. "car search app")
- Check the **`repo`** scope
- Click **Generate token**
- Copy it immediately — you only see it once

### 4. Get an Anthropic API key (optional, for Carfax AI parsing)

Go to [console.anthropic.com](https://console.anthropic.com) → API Keys → Create key.

This is only needed if you want to use the paste-to-autofill feature. Without it, everything else works fine.

### 5. Configure the app

Open your app → click **Settings** → fill in:
- GitHub username
- Repository name
- Personal access token
- Anthropic API key (optional)

Both keys are stored only in your browser's `localStorage` and are sent only to GitHub and Anthropic directly — they never go anywhere else.

## How data is stored

Your car data lives in `cars.json` in this repo. Every time you add, edit, or delete a car, the app commits an updated `cars.json` automatically. You get a full version history for free via git — so you can always roll back to a previous state if needed.

The app also caches data in `localStorage` for instant load times. On startup it fetches the latest from GitHub and merges any local-only entries.

## Carfax paste-to-autofill

When adding a car, open the Carfax PDF in your browser or PDF viewer, select all (Ctrl+A), copy (Ctrl+C), and paste the text into the Carfax field in the app. Click **Parse with AI** and it will auto-fill:

- Carfax status
- Reported damage amount
- Provinces registered
- Number of owners
- Service record count
- Any notable flags (odometer issues, US history, fleet/rental use, open recalls, etc.)

Review the filled fields before saving — AI parsing is good but not perfect.

## Backup

Despite GitHub being the primary store, you can also click **Export JSON** at any time to download a `cars-backup.json` file. You can re-import it on any device using **Import JSON**. Duplicate entries are skipped on import.

## Local development

It's a single `index.html` file with no build step. Just open it in a browser — though note the GitHub sync won't work when running from `file://` due to CORS. Use a simple local server if needed:

```bash
npx serve .
# or
python3 -m http.server
```
