# Rain game reference

Inventory, stats, item effects, attack behavior, and spawn settings, organized by category.

| Category | Reference |
| --- | --- |
| Items | [All 15 item definitions, exact values, stacking, triggers, and reward odds](game-items.md) |
| Enemies and bosses | [All 22 enemy definitions, base stats, attacks, rewards, and protection](game-enemies.md) |
| Characters | [Commando and Railgunner stats, abilities, reload, and damage examples](game-characters.md) |
| Maps and spawning | [Four map configurations, spawn percentages, difficulty, caps, and economy](game-maps.md) |
| Miscellaneous systems | [Progression, combat, pings, Rift encounters, UI, and recovery](game-misc.md) |

[Content index](game-content-list.md) | [How to read the stats](game-content-stats.md)

## Source and scope

Recorded 2026-09-27 from the Rain worktree based on [`b49a73f60f7f`](https://github.com/DrasticDeveloping/rain/tree/b49a73f60f7fb18db88dffe87783fa2c208e28a7), including the local enemy weak-point/death-animation changes from this task. Source links are pinned to that base revision for the existing balance and attack implementation; those links do not claim the later local enemy changes are committed in the game repository.

Numbers describe source defaults. Active server overrides, level gains, inventory, phase, protection, population limits, and available space can change outcomes. Spawn percentages are conditional card-selection probabilities, not fixed per-second spawn rates. Inactive maps and debug-only content are labeled.

## Verification status

Item descriptions were checked against their effect handlers and inventory stacking logic. Attack summaries were checked against ability, damage, projectile, and protection code. Category links and source paths were checked, and spawn-weight normalization was checked across all four maps, both channels, and five difficulty tiers.

The local Rain implementation configures Railgunner weak points for all 22 enemy definitions and removes death animations from AdultAntlion, Barkback, DuneViper, MagmaWorm, and ReedStalker. Its recorded offline run passed 81 of 82 checks; the remaining check concerns map spawn/startup dependencies. Live acceptance remains blocked by Renium's TextChatService font snapshot mismatch. This documentation is not a claim that every feature passed live playtesting.
