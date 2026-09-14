# AGENTS.md

ClassicalNotes: an Android app (Kotlin/Compose) for tracking classical music concerts attended or planned — performances, set lists of works, performers, conductors, and venues, with listening notes per piece. Client for a self-hosted FastAPI backend ([ClassicalNotes-Server](https://github.com/chaddy50/ClassicalNotes-Server)).

## Stack

- Kotlin + Jetpack Compose
- Retrofit 2 + kotlinx.serialization for the backend API
- Hilt for dependency injection
- Jetpack DataStore for local settings (e.g. the API server URL)
- Navigation Compose

## Layout

Package root: `app/src/main/java/com/chaddy50/concerttracker/`

- `data/`
  - `domain/` — domain models
  - `local/` — local persistence (DataStore, etc.)
  - `external/` — API clients (the backend, MusicBrainz, Open Opus, OpenStreetMap Nominatim)
  - `repository/` — repositories mediating between local/external data and UI
  - `sync/` — sync logic
  - `enum/` — shared enums
- `ui/`
  - `screens/` — top-level screens
  - `composables/` — reusable composables
  - `theme/` — Compose theming
- `navigation/` — nav graph (`routes/`, `topBarActions/`)
- `dependencyInjection/` — Hilt modules
- `util/` — general-purpose helpers

## Commands

- `./gradlew testDebugUnitTest` — unit tests (mirrors CI's `unit-tests` job in `.github/workflows/ci.yml`, which runs on push/PR).

## Conventions

- A "performance" is a specific concert/set-list instance, distinct from the underlying "work" (piece) and "performer" — don't collapse these when adding features.
- New data-layer code follows domain model → repository layering; UI reads through repositories, not raw API/local sources directly.
- External metadata (composers/works via Open Opus, performers via MusicBrainz, venues via Nominatim) is fetched through `data/external/`, not called ad hoc from UI or repositories.

## Git & Commits

- **Never include Claude (or any AI assistant) as a commit co-author or contributor.** No `Co-Authored-By: Claude` trailer, no "Generated with Claude Code" line, no assistant mention in commit messages, PR titles, or PR descriptions. Write commits as the author, describing the change and why.
- Create commits only when explicitly asked.
