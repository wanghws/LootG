# CLAUDE.md

## Project Overview

LootG is a World of Warcraft addon that displays loot notifications as scrolling text and combat state indicators.

**Deduplication:** every display path (`LOOT_SLOT_CLEARED`, `CHAT_MSG_LOOT`, `CHAT_MSG_CURRENCY`, `SHOW_LOOT_TOAST`) records shown items in the `recentlyShown` table keyed by item/currency ID. A different event source for the same ID within 5 seconds is skipped; the same source is treated as a new pickup. Expired entries are lazily swept inside `Util.MarkRecentlyShown`.

## SavedVariables

`LootGDB` — legacy flat SavedVariable, kept in the `.toc` only so `_MigrateLegacyDB` can read it once and then nil it out.

## Testing

Standalone Lua specs (no WoW client needed), run from the repo root:
- `lua tests/lootg_utils_spec.lua` — dedup/util logic in LootGUtils.lua
- `lua tests/lootg_migration_spec.lua` — `LootG:_MigrateLegacyDB` SavedVariables migration

Manual in-game testing:
- `/lootg test` — display a test loot notification
- `/lootg debug` — print debug state
- Right-click the addon compartment button for test display

## Development Notes

- `LootGUtils.lua` must stay WoW-API-free — the standalone specs load it outside the game.
- All icon references use numeric **fileID** values (e.g., `236681` for Achievement_Reputation_01), not string texture paths.
- `C_CurrencyInfo.GetCoinTextureString()` returns text with inline coin icons — do not add a separate icon parameter when displaying money.
- Patch 12.1.5 removed the deprecated global fallbacks (`GetItemInfo`, `GetItemCount`, `GetItemQualityColor`, `GetCoinTextureString`, `tContains`, `Round`, …). Always call the namespaced API (`C_Item.*`, `C_CurrencyInfo.*`, `C_AddOns.*`, `Settings.*`) directly — no `or LegacyGlobal` fallbacks.
- Color text by item quality with `ColorManager.GetFormattedStringForItemQuality(text, quality)` (emits a `|cnIQ<n>:` token that honors the player's quality color overrides). Game-generated links already carry `|cff…` or `|cnIQ…` colors — don't re-wrap them.
- The addon uses WoW's frame pooling pattern to avoid GC pressure during rapid loot events.
- Localization keys must be added to all three language blocks in Locales.lua (en default, zhCN, zhTW).
- Language: code comments and commit messages are in Chinese.

## Release Workflow

Releases are cut through the `/release` command (`.claude/commands/release.md`, mirrored for Codex at `.agents/skills/source-command-release/SKILL.md`; both are local and gitignored). Do **not** push unless the user asks.

The `## Version:` in `LootG.toc` is always the *next* unreleased version; the last released one is the latest `v*` tag. The changelog lives only in `CHANGELOG.md` — the READMEs link to it.

Nothing uploads to CurseForge/WoWInterface — those are manual uploads of the generated zip.
