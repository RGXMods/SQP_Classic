# v1.9.8-classic - 2026-08-22

## Changes
- **Classic Era fixes**: removed a call to the nonexistent `SQP:RegisterEvents()` at load (events self-register in `data/events.lua`) and migrated all 215 obsolete `SQPSettings` global references to the canonical `SQP:GetSettings()` accessor backed by the RGX database
- **Version display** now reads TOC metadata instead of a hardcoded string
- **Release pipeline** corrected for the fork: packager now ships the zip as `SQP_Classic/` (was `SimpleQuestPlates/`, which the client would not load), and the workflow reads `SQP_Classic.toc`

# v1.9.7-classic - 2026-08-08

## Changes
- **RGX-Framework integration**: Migrated from standalone to RGX-Framework with cross-version compat layer
- **DB migration**: `SQPClassicSettings` → `RGX:NewDatabase("SQPClassicSettings", ...)` with `profileIsGlobal = true`
- **Timers**: Replaced manual `C_Timer` usage with `RGX:After` / `RGX:Every`
- **Minimap**: Uses `RGXMinimap:Create()` 
- **Slash commands**: Registered via `RGX:RegisterSlashCommand`
- **Events**: Registered via `RGX:RegisterEvent` with compat layer API shims
- **Backward-compat**: `SQPClassicSettings` global remains as proxy to `SQP.db.global`
- **Compat layer**: Uses RGX-Framework's new `core/compat.lua` for Classic API shims

## v1.9.6-classic - 2026-08-07
- Forked from SQP v1.9.6 (pre-RGX-Framework integration) for Classic-only maintenance.
- TOC: Classic-only interfaces 11509 (Classic Era), 20506 (TBC Anniversary), 50504 (MoP Classic).
- Renamed addon to SQP_Classic, SavedVariables to SQPClassicSettings.
- Removed RGX-Framework dependency (was OptionalDeps in v1.9.7+).

## v1.9.6
- Fixed slash command robustness issues:
  - Replaced unsafe input trimming with safe string normalization.
  - Added explicit `/sqp version` handling.
  - Added missing debug handlers for `debug target` and `debug nameplates`.
  - Added resilient localization fallbacks for command/status output.
- Expanded `enUS` baseline localization with missing runtime keys used by commands/options.
- Removed legacy option modules that were no longer loaded by `SimpleQuestPlates.xml`:
  - `data/options_colors.lua`
  - `data/options_font.lua`
  - `data/options_quest_icons.lua`
  - `data/options_rgx.lua`
- Cleaned and synchronized repository documentation (root README, directory READMEs, roadmap, assistant docs).
- Updated release workflow support link to `discord.gg/rgxmods`.
- Standardized release notes source to `docs/CHANGES.md` only (removed `docs/CHANGELOG.md` references).
- Completed locale coverage:
  - Added locale modules for `enGB`, `itIT`, `koKR`, `ptBR`, and `zhTW`.
  - Filled all locale modules with full key coverage for runtime-safe lookups.
- Updated options tab layout to dynamically fill the full tab row width with no trailing gap.
- Refreshed the stylized root README and directory docs to match current commands, locale coverage, and assets.
