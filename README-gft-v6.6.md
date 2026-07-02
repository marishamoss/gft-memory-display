# Memory Display — Personal Prototype
**v6.6 · Pro dogfood build**

This is the *personal prototype* of the display that became
[MemoryLUV](https://github.com/marishamoss/memory-luv-kit) — the live display
running in a real caregiving environment. It is the testbed for **MemoryLUV
Pro** features before they reach the commercial product.

This repo is **not** the for-sale product. The commercial configurator and
generated display live in `memory-luv-kit`. The two codebases are related but
intentionally separate: this one changes fast and serves one household; that
one changes carefully and serves customers.

---

## What this display does

Runs full-screen in a browser (mirrored from a laptop to a wall-mounted
monitor) and shows, at a glance:

- Large current time and full date
- Live local weather (Open-Meteo, refreshed every 30 minutes)
- Today's caregiver — day shift / night shift (7 PM handoff), with
  date-specific substitutes
- Today's schedule with full-screen pop-up reminders and a chime
- Medication reminders at three daily times
- Recurring water and movement prompts, including optional YouTube exercise
  video overlays with countdown
- "For Today" suggestions — daily, weekly, and date-specific (birthdays,
  call reminders), plus US holidays calculated dynamically each year
- Day / evening / night modes that dim automatically

---

## What's new in v6.6

**Large Print restored.** Schedule and For Today items are back to 55px
(titles 45px) for readability from across the room.

**Remote config (MemoryLUV Pro core).** The display can now pull its entire
configuration — caregivers, substitutes, events, reminders, suggestions —
from a Cloudflare Worker config store instead of relying solely on values
baked into this file:

- **On every page load**, the display fetches the latest config from the
  Worker.
- **Every 60 seconds**, a silent background poll checks whether the config
  changed and applies updates *in place* — no reload, no white flash. An
  edit made from a phone appears on the display within about a minute.
- **First-ever connection self-seeds the store** with the config baked into
  this file, so the schedule already in the source becomes the starting
  point automatically.
- **Fallback chain:** live Worker config → last successfully fetched config
  (cached in localStorage) → the config baked into this file. A network
  problem can never blank the display.
- **Overlay-safe:** the poll skips its cycle while a reminder overlay is on
  screen, so pop-ups are never interrupted.

**Editing moves to the phone.** Configuration edits now happen through a
mobile web editor served by the Worker at `<worker-url>/edit` — structured
fields and a Save button instead of hand-editing JavaScript in the GitHub
app. Direct source editing still works and remains the fallback.

If `WORKER_URL` in `index.html` is left as its placeholder, all remote
features stay dormant and the display behaves exactly like v6.5 — fully
local. This makes the file safe to deploy before the Worker exists.

---

## Architecture (Pro dogfood)

| Piece | Where it lives | Job |
|---|---|---|
| Display (`index.html`) | This repo, served via GitHub Pages | Renders everything; polls for config changes |
| Config store | Cloudflare Worker + KV namespace `MEMORYLUV_CONFIGS` | Holds the schedule; one JSON record per display |
| Mobile editor | Served by the Worker at `/edit` | Phone-friendly editing of every config section |

**Code vs. data:** GitHub is the *code* layer (layout, logic, features).
The Worker is the *data* layer (who's here today, what's happening, when).
After v6.6, routine schedule changes never touch this repo.

**Identity:** each display has a long random `DISPLAY_ID` (part of its
config URL) and a secret `DISPLAY_KEY` (sent in a request header). The key
is required to read *and* write. The first save to a new ID claims it
permanently (trust-on-first-use).

---

## Config schema

The Worker stores one JSON object per display. Field names match the
variables in `index.html`:

`location` · `weeklyCaregivers` · `substituteCaregivers` ·
`nightCaregivers` · `substituteNightCaregivers` · `specificDateEvents` ·
`weeklyEvents` · `dailyReminders` · `weeklyReminders` ·
`recurringReminders` · `dailySuggestions` · `weeklySuggestions` ·
`specificSuggestions`

Any field missing from the remote config keeps its baked-in value, so
partial configs are safe.

---

## Privacy note (read before forking this pattern)

This repo is public, which means the schedule data baked into
`index.html` — names, appointments, coverage times — is publicly readable,
and in v6.6 the display key committed in the source grants write access to
the config store. This is a **known, accepted trade-off for the dogfood
phase only**: the URL is obscure, the stakes of vandalism are low, and the
key can be rotated by generating a new ID/key pair and re-seeding.

The production fix — serving the display privately from the Worker itself
rather than public GitHub Pages — is on the Pro productization roadmap and
is a hard requirement before any customer data flows through this
architecture.

---

## Deployment status

- [x] v6.6 display code (this file)
- [x] Worker v0.2 code written and tested (config store + `/edit` editor)
- [x] Cloudflare account, nameservers, KV namespace `MEMORYLUV_CONFIGS`
- [ ] Worker deployed (blocked by Cloudflare Workers outage at time of writing)
- [ ] KV bound to Worker as variable name `CONFIGS`
- [ ] `WORKER_URL` in `index.html` updated with the real Worker address
- [ ] First connect verified (console: "store is empty — seeding")
- [ ] Phone editor connected and first remote edit confirmed on the display

---

## Version history

- **v6.6** — Remote config via Cloudflare Worker; 60-second in-place update
  polling; mobile editor at `/edit`; Large Print restored (55px items /
  45px titles)
- **v6.5** — Dynamic holiday calculation (Easter, MLK, Thanksgiving, etc.
  computed per year); styled video countdown; muted autoplay for Chrome
- Earlier — substitute caregiver system, night-shift handoff at 7 PM,
  YouTube exercise video overlays, day/evening/night modes

---

*Personal project · © 2026 Rituli Moss Studio LLC. Related commercial
product: MemoryLUV, a LUVWORKS product.*
