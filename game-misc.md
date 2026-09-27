# Miscellaneous systems

[Content index](game-content-list.md) | [How to read the stats](game-content-stats.md)

Source snapshot: 2026-09-27. This records existing source definitions and configured values, not completed live acceptance testing. Runtime settings, level, inventory, and state can change gameplay outcomes.

## Feature inventory

| Area | Existing features |
| --- | --- |
| Main menu | Play flow, survivor selection, logbook, settings, and credits. |
| Game entry | Character spawning, entry acknowledgement, and respawn handling. Cross-server lobby joining remains unavailable. |
| Camera and controls | Shooter camera, shift lock, aiming, scope controls, and menu/input coordination. |
| Inventory | Item stacking, inventory display, tooltips, and item effect ownership. |
| Rewards and progression | Gold, XP, leveling, health/stat changes, and item rewards. |
| Interactables | Chests, chest pickups/reward feedback, and item pedestals. |
| Stage objectives | Rift Anchors, boss objectives, and stage travel; charge changes to 100 on encounter completion rather than filling on a timer. |
| World management | Stage rotation, map boundaries, and out-of-bounds recovery. |
| Enemy spawning | Combat directors, active/ambient enemy cards, placement, population limits, and difficulty-based pacing. |
| Enemy movement | Pathing, crowd spacing, ground/air placement, and articulated serpent movement. |
| Combat | Damage, projectiles, hitboxes, shields/protection, critical hits, and Railgunner weak points. |
| Communication | Chest, Rift Anchor, and inventory-item pings with world markers/highlights. |
| HUD | Health/status display, run statistics, objective feedback, and boss presentation. |
| Settings | Session settings for shadows, mouse sensitivity, and scope sensitivity. |
| Development tools | Enemy/boss spawning, item grants, configuration commands, and offline/Studio test fixtures. |

Useful implementation references: [gameplay feedback](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/docs/gameplay-feedback.md), [spawn directors](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/docs/spawn-directors.md), [Railgunner](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/docs/railgunner.md), [main menu](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/docs/main-menu.md), and [run statistics](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/docs/run-stats-hud.md). Current source takes precedence where older documentation differs.

## Numerical systems

- **XP:** 100 × current level to reach the next level; cumulative thresholds 0, 100, 300, 600, 1000 XP for levels 1–5.
- **Defense:** ordinary damage multiplier = 100 / (100 + nonnegative defense). Examples: defense 25 -> 80% damage taken; 50 -> 66.67%; 100 -> 50%. Shields, armor phases, and immunity may change the route.
- **Rift activation:** normal anchor activation requests 3 Parallax bosses. Command-triggered encounters request 1 selected boss. This is an encounter rule, separate from random spawn-card odds. [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/RiftEncounter.luau)

Features without a balance value (such as menu navigation or the existence of a map) remain in the content inventory. The following tables list configured numeric constants for shared systems; they are not claims about live overrides.

### Damage constants

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Damage.luau)

| Parameter | Value |
| --- | --- |
| DefenseScale | 100 |
| KnockbackDuration | 0.2 |
| ComboDuration | 3 |

### RiftEncounter constants

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/RiftEncounter.luau)

| Parameter | Value |
| --- | --- |
| EncounterBossCount | 3 |

### VoidRecovery constants

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Entity/VoidRecovery.luau)

| Parameter | Value |
| --- | --- |
| VoidHeight | -250 |
| SafeRadius | 4 |
| SampleInterval | 0.25 |
| HistorySize | 8 |

### Pings, pedestals, and Rift completion

- Pings: 1.5 s server cooldown, up to 800 studs for supported world targets, and 8 s marker lifetime. [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Pings/init.luau).
- Deadwood Basin's inactive shop configuration charges 50 gold for a uniform random White/Green item: 1/14 (7.14%) per item with the current pool, therefore 6/14 White and 8/14 Green. This is not a 50/50 rarity roll. Rustwake Wreck and Flooded Quarry currently have no shop cards. [Shop selection](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/ItemPedestals.luau).
- Normal Rift completion sets charge directly from 0 to 100 after all three encounter bosses die, then enables travel. It is not a timed charging percentage in the current implementation. Candidate anchor locations are chosen uniformly from saved BasePart markers; exact per-marker odds are `1 / eligible marker count`. [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/RiftEncounter.luau).
