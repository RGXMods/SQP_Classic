# SQP_Classic

SQP_Classic is the Classic-only fork of SimpleQuestPlates. Work on the `classic-fork` branch and keep it distinct from Retail `main`. `SQP_Classic.toc` targets Classic Era (`11509`), Burning Crusade Classic (`20506`), and Mists of Pandaria Classic (`50504`); it must not gain the Retail interface target. The addon requires `RGX-Framework` and stores settings in `SQPClassicSettings`.

## Layout

- `SQP_Classic.toc` loads `SimpleQuestPlates.xml`, which defines localization and runtime load order.
- `locales/` contains the `enUS` baseline and locale overrides.
- `data/` contains the fork's compatibility layer, quest/nameplate logic, event handling, commands, and hand-built options UI.
- `media/` contains the fork's icon, logo, screenshots, and other documentation assets.
- `docs/` contains the fork changelog, README, description, and roadmap.

## Fork Rules

- Preserve Classic compatibility guards in `data/compat.lua` and `data/compat_mop.lua`; do not replace them with Retail-only APIs.
- Use the RGX database, lifecycle, timer, and slash-command integrations already present, but preserve raw event/timer compatibility paths where the fork currently needs them.
- Port shared changes from SimpleQuestPlates selectively. Do not overwrite fork-specific TOC metadata, `SQPClassicSettings`, compatibility code, options modules, media paths, or Classic version labeling.
- Preserve the script order in `SimpleQuestPlates.xml`. Keep `SQP_Classic.toc` and `SQP.VERSION` in `data/core.lua` synchronized when changing versions.
- `docs/CHANGES.md` contains the current fork release notes.

## Testing And Release

- There is no build step or automated test suite. Install the repository as `SQP_Classic` with a matching Classic build of `RGX-Framework`. Test each changed supported flavor with `/reload`, `/sqp help`, `/sqp status`, `/sqp test`, quest/nameplate updates, target and mouseover detection, options and previews, persistence, and locale fallback behavior.
- Release tags and versions must retain the fork's `-classic` identity. The inherited `.github/workflows/release.yml` currently references the absent `SimpleQuestPlates.toc` and accepts only plain semantic-version tags, so do not claim or rely on automated packaging until that workflow is repaired for `SQP_Classic.toc` and Classic-suffixed versions.

## Repository Workflow

- The GitLab project under `rgxmods/warcraft` is authoritative. Normal work belongs on task branches and must merge through GitLab merge requests, never directly to the default branch.
- Shared CI is included from `rgxmods/warcraft/RGX-Framework` at `/.gitlab/ci/addon.yml`; validation must pass before publishing to the GitHub mirror.
- The GitHub `RGXMods` repository is downstream distribution, not development authority.
- Keep GitLab and GitHub release tags identical, and use protected GitLab release tags.
- Preserve any existing working Wago connection and ID exactly. Never create a new Wago connection without explicit user direction.
- Publishing integrations prohibited by the shared validation policy are retired and must not be restored.
- The root `README.md` must remain detailed and project-specific. Narrow distribution edits must not replace or truncate installation, features, compatibility, usage, media, or support content.
- Verify relative README assets. Do not overwrite newer compatibility facts with stale monorepo or history text.
