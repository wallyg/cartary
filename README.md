# Cartary

**Your world, mapped.**

Cartary is a shared map library for families and close circles. It's a home for the maps you've built in Google My Maps, with richer organization, better formatting, and sync across devices, while keeping the Google Maps features you like (directions, reviews).

> **Status:** Planning. No app code yet. See the [plan](docs/PLAN.md).

## The idea

- **One pile of places, with maps as saved filters.** Every place carries tags (region, category, source map, status). A "map" is a saved view, so one place can appear in many views without being copied.
- **You own your data.** Import your Google My Maps once, edit in Cartary, and export back to KML any time for My Maps or other apps.
- **Shared.** Close circles (family) see and edit the same maps, synced across devices.
- **Web first, native iPhone app later.**

## Planned stack

React + TypeScript web app, Supabase (database, sign-in, live sync, sharing rules), Google Maps for the base map and place details (pending terms and cost check), React Native for the iPhone app later.

## Roadmap

See [docs/PLAN.md](docs/PLAN.md) and the GitHub issues, labeled by version.

## Brand

Brand assets live in [`assets/brand/`](assets/brand/).

## License

MIT, see [LICENSE](LICENSE).
