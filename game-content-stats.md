# Game stats reference

The numerical reference is now split by category:

- [Items: values, stacking, and drop odds](game-items.md)
- [Enemies and bosses: base stats and attack details](game-enemies.md)
- [Characters: stats, abilities, and damage examples](game-characters.md)
- [Maps: spawn chances, difficulty, and economy](game-maps.md)
- [Miscellaneous systems](game-misc.md)

[Back to the content index](game-content-list.md).

## Reading the stats

Source snapshot: 2026-09-27. Saved code values, not measured live-server settings. Runtime `/config` changes, inventory, level, attack state, and protection can change outcomes. Distances use studs and times use seconds unless stated.

Attack damage is a base stat, not necessarily the damage of every attack. Attacks may multiply it or supply a fixed damage value. Attack speed is a stat multiplier, not a guaranteed attacks-per-second rate. Defense normally scales incoming damage by `100 / (100 + max(0, Defense))`; enemy protection can override that calculation. Enemy stats are set on spawn to `base + (EnemyLevel - 1) × per-level gain`. The run difficulty index supplies EnemyLevel (1–5); missing gains mean no extra gain from that definition. Gold and XP columns are configured kill rewards.

Source expressions are retained when a value depends on runtime state, rig geometry, or another module; they are not invented numeric defaults. Field names in detailed tables match the code for easy lookup.
