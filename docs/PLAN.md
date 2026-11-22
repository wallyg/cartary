# Cartary — Plan (Draft v0.1)

Status: **APPROVED 2026-11-22.** No code and no sprint has started yet. Groundwork is next.
Date: 2026-11-22

---

## 1. What we're building

**Cartary is a shared map library for you and your family.** It replaces Google My Maps as the place your maps *live*, fixes its limits (formatting, icons, flat lists, clunky mobile editing), and keeps the Google Maps things you like (directions, reviews).

**Who it's for**
- You: the main editor, mostly on a laptop in the evening, plus quick adds from your phone while traveling.
- Your family: kids on PCs now (iPads and phones later) who view, and sometimes add to, shared maps.
- Today a small close circle. It may grow later, but we won't design for that yet.

**What "done" looks like for v1.0** (the first version your family really uses on a trip)
1. All ~127 of your My Maps are imported and browsable.
2. You can see everything near you across all maps, filtered by category, in one view.
3. You can add or edit a place on a laptop, and it shows up on a phone browser within seconds.
4. Your kids can log in from a PC and see the shared maps.
5. You can export any view back to Google My Maps (the insurance policy).
6. Directions open in Google Maps in one tap, and each place shows Google's rating, reviews and hours.

**Not in v1.0:** the native iPhone app (that's v2.0), offline-first editing, public sharing, routes/itineraries.

---

## 2. Key ideas (the "why" behind the design)

1. **Cartary owns the data.** Google My Maps becomes a one-time import source. Google has no way to read or write My Maps from an app, so a live link isn't possible. You can retire My Maps when you're ready.
2. **One pile of places, with maps as saved filters.** Every place carries tags: region (Buenos Aires), category (dining), source (your old "Palermo" map), status (been / want to go). A "map" is a saved view, such as "Buenos Aires" or "Burger Spots". One café can appear in many views without being copied.
3. **Insurance export.** Any view exports as a KML file you can upload into My Maps, and the whole library can be backed up as files. You are never locked in.
4. **Web first, native later.** The web app serves your kids and your laptop. The iPhone app comes after the web version is solid, and it reuses the same backend.

---

## 3. Proposed tech (needs your approval — you asked to approve dependencies)

| Piece | Proposal | Why | Alternative |
|---|---|---|---|
| Web app | React + TypeScript | Same family of tools as FlickrFetch | — |
| Backend and sync | **Supabase** (database, login, live sync, sharing rules, file storage) | Built for small shared groups; handles "who can see/edit what"; supports location queries (near me); low cost at family scale | Firebase |
| Base map | **Google Maps** (recommended) | Full tie-in: directions, reviews, hours, photos; custom icons and styling are supported | Mapbox, with Google deep links only |
| Hosting | Static web hosting (Vercel or Netlify) | Simple, cheap | — |
| Later: iPhone | React Native, sharing code and the backend with the web | Native feel, offline caching, share-sheet quick-add | Swift |
| Import/export | KML/KMZ reader and writer | The format My Maps uses | — |

**Google rules to verify in Groundwork:**
- Cartary can store only Google's place ID and fetch ratings, reviews and hours live. It can't copy that content into its own database.
- Google likely requires that content to appear on a Google map.
- Google Maps charges by usage. Expected to be small for a family, but unverified. We'll set a spending cap.

---

## 4. Data model (plain language)

- **Circle:** a group of people, such as "Our Family". Has members with roles: owner, editor or viewer.
- **Place:** name, location, your notes, category, tags, status, icon, Google place ID, who added it, source map and layer, dates.
- **View (a "map"):** a saved filter, such as region = Buenos Aires AND category = dining. Belongs to a circle.
- **Source:** where an import came from (original map title, layer, date), so nothing is lost.
- **Later:** photos, itineraries and days.

---

## 5. Sprint roadmap

Sprints are named by what's in them. Versions are 0.x until the first family-ready release at v1.0. Each sprint ends with a changelog entry, a UAT checklist and a push to GitHub, per your working rules.

| # | Sprint | Ships as | What's in it |
|---|---|---|---|
| 1 | **Groundwork** | none | Create repo and `assets/brand/`. Set up Supabase, hosting and login skeleton. **Three decision spikes:** (a) Google Takeout "My Maps" export test, (b) Google vs Mapbox terms and cost, (c) My Maps import limits and icon behavior. Name clearance check. |
| 2 | **Import & Library** | v0.1 | Import KML/KMZ, with layers becoming categories and the original map kept as a source tag. Bulk-import your ~127 maps. Review screen for messy layers. Duplicate-place suggestions you approve. |
| 3 | **Map & Browse** | v0.2 | Base map with custom icons. Filters (region, category, tag, source, status). Saved views (your new "maps"). List view. Search. Place detail card with open-in-Google-Maps for directions. |
| 4 | **Export & Backup** | v0.3 | Export any view as KML for My Maps, with automatic splitting for size limits. Full-library backup. Round-trip test back into My Maps. |
| 5 | **Edit & Organize** | v0.4 | Add a place by search or dropped pin. Edit notes, tags and category. Bulk tagging. Merge duplicates. Undo and edit history. |
| 6 | **Circles & Sharing** | v0.5 | Accounts, family invitations, roles, live sync across devices. Shared views. **First time your kids can use it.** |
| 7 | **Google Details** | v0.6 | Live ratings, reviews, hours and photos per place via Google place ID. Near-me sort. |
| 8 | **Travel-Ready** | v0.7 | Fast quick-add on a phone browser. Installable to the home screen. Caching for places you've already opened. Performance on slow connections. |
| 9 | **Polish & Launch** | **v1.0** | Remaining quick wins, brand pass, in-app changelog, onboarding for family, test on a real trip. |

After v1.0:
- **v2.0 — Native iPhone app:** React Native on the same backend, offline-first, share-sheet quick-add ("share this place from Google Maps into Cartary"), iPad support.
- **v3.0 — Beyond family:** more circles, routes and itineraries, public share links, richer collaboration.

---

## 6. Backlog (to become GitHub issues once the repo exists)

Every item gets an issue and a version label, per your rules. Proposed:

**v0.x**
- KML/KMZ import with layer-to-category mapping
- Bulk import from Takeout
- Import review screen
- Duplicate detection and merge
- Region auto-tagging from coordinates
- Filters and saved views
- Place detail card
- Open in Google Maps (directions)
- KML export with size-limit splitting
- Full-library backup
- Add place by search and by dropped pin
- Bulk tagging
- Edit history and undo
- Circles, invites and roles
- Live sync
- Google ratings, reviews and hours
- Near-me sort
- Installable web app and caching

**v2.0**
- Native iPhone app
- Offline-first sync
- Share-sheet quick-add
- iPad layout

**v3.0**
- Itineraries and routes
- Public share links
- Multiple circles

**Quick wins:** none yet.
**Known bugs:** none yet.

---

## 7. Risks

| Risk | What it means | How we handle it |
|---|---|---|
| Takeout may not export My Maps | We'd have to export ~127 maps by hand | Test in Groundwork; fallback is a batch routine of one-per-map exports |
| Google terms or cost | Could rule out Google as base map | Verify in Groundwork; Mapbox fallback |
| Messy layers | Layers mean different things in different maps | Review screen, auto-suggestions, you approve |
| Duplicate places | Same spot saved in several maps | Suggest merges; you approve uncertain ones |
| Web offline limits | A web app caches less than a native app | Be honest in v1.0; native app in v2.0 fixes it |
| Kids' accounts | Ages and account types may affect sign-in options | Open question below |
| Name clearance | "Cartary" may conflict with an existing trademark or App Store name | Check in Groundwork, before more is invested |

---

## 8. Decisions made (2026-11-22)

1. **Tech approved:** React + TypeScript, Supabase (separate project), Google Maps as the leading base map (pending terms and cost check), static hosting.
2. **Sign-in:** the main users have Google accounts and turn 13 in January 2027, so "Sign in with Google" is the primary login.
3. **Repo:** public, MIT licensed. Rules: never commit secrets, restrict the Google Maps key by domain, keep personal places and family trip details out of the repo and issues.
4. **Sprint order:** as drafted (Export & Backup early); to be reviewed after a few sprints.
5. **Takeout test:** runs during Groundwork.

**Open:** trademark / App Store name clearance for "Cartary" (Groundwork).
