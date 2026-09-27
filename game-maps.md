# Maps and spawning

[Content index](game-content-list.md) | [How to read the stats](game-content-stats.md)

Source snapshot: 2026-09-27. This records existing source definitions and configured values, not completed live acceptance testing. Runtime settings, level, inventory, and state can change gameplay outcomes.

## Map inventory

Four map configuration modules exist. The active rotation is determined by [MapConfig](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/MapConfig/init.luau).

| Map | Current integration |
| --- | --- |
| Rustwake Wreck | Included in the active stage rotation. |
| Flooded Quarry | Included in the active stage rotation. |
| Heights Expansion | Existing map/configuration; outside the current rotation. |
| Deadwood Basin | Existing map/configuration; outside the current rotation. |

Other designs in [map-layouts](https://github.com/DrasticDeveloping/rain/tree/b49a73f60f7fb18db88dffe87783fa2c208e28a7/docs/map-layouts) are concept/planning assets and are not counted as playable maps here.

Enemy HP, damage, rewards, and individual attack settings are in [enemies and bosses](game-enemies.md).

## Difficulty and spawn timing

| Tier / enemy level | Active run time | Income multiplier | Bank multiplier |
| --- | --- | --- | --- |
| Easy / 1 | 0–179.999 s | 1 | 1 |
| Normal / 2 | 180–359.999 s | 1.3 | 1.25 |
| Hard / 3 | 360–599.999 s | 1.7 | 1.5 |
| Insane / 4 | 600–899.999 s | 2.2 | 2 |
| Nightmare / 5 | 900 s onward | 3 | 2.5 |

The schedule uses accumulated active run time, not time since the current map loaded. See [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/ServerConfig.luau) and [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/Gameplay.luau).

The director uses `M = (1 + 0.6 × (participants - 1)) × (1 + 0.2 × (stage - 1)) × difficulty income multiplier`. Active income interpolates from InitialIncome to FinalIncome over SpawnRampDuration, then multiplies by M. Ambient income is AmbientIncome × M. Purchase intervals divide by M; bank capacities multiply by the tier bank multiplier. Banks start empty. A selected purchase waits for enough credits; it is not rerolled just because the bank is temporarily short.

## Enemy spawn selection chances

Each percentage below is `effective card weight / sum of eligible effective weights × 100`. It describes a **new card selection**, not a chance each frame, per kill, or per individual enemy. Tables assume all listed positive-weight cards fit bank/population capacity, stage gates are satisfied, and no placement cooldown excludes them. Pattern/pack counts, credit cost, spawn timing, space, and population limits change observed spawn frequency. The director picks uniformly among eligible pack patterns after choosing a card.

`DifficultyWeights` overrides the card’s fallback `Weight`. `Progression` can additionally ramp a card’s weight using active run time. `Spawn.Chance` fields on some definitions are not read by this director and are not the percentages below. Placement attempts expire after 8 seconds; failed placements can temporarily exclude a card for twice its current channel interval. See [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/CombatDirector.luau).

### RustwakeWreck — active rotation


**Active pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Parallax | 0.1 | 1 | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0.1 -> 0.79% |
| DuneSkitter | 4 | 1 | 6 -> 57.14% | 5 -> 47.62% | 4 -> 34.78% | 3 -> 24.00% | 2 -> 15.87% |
| Rustback | 1 | 1 | 0.5 -> 4.76% | 1 -> 9.52% | 2 -> 17.39% | 3 -> 24.00% | 4 -> 31.75% |
| GlassTail | 2 | 1 | 1.5 -> 14.29% | 2 -> 19.05% | 3 -> 26.09% | 4 -> 32.00% | 4 -> 31.75% |
| DuneViper | 1 | 1 | 1 -> 9.52% | 1 -> 9.52% | 1 -> 8.70% | 1 -> 8.00% | 1 -> 7.94% |
| AdultAntlion | 1 | 1 | 1 -> 9.52% | 1 -> 9.52% | 1 -> 8.70% | 1 -> 8.00% | 1 -> 7.94% |
| MagmaWorm | 0.5 | 1 | 0.5 -> 4.76% | 0.5 -> 4.76% | 0.5 -> 4.35% | 0.5 -> 4.00% | 0.5 -> 3.97% |

Tier cells show **weight -> conditional selection percentage**.

**Ambient pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| DuneSkitter | 4 | 1 | 6 -> 66.67% | 5 -> 55.56% | 4 -> 40.00% | 3 -> 27.27% | 2 -> 18.18% |
| Rustback | 1 | 1 | 0.5 -> 5.56% | 1 -> 11.11% | 2 -> 20.00% | 3 -> 27.27% | 4 -> 36.36% |
| GlassTail | 2 | 1 | 1.5 -> 16.67% | 2 -> 22.22% | 3 -> 30.00% | 4 -> 36.36% | 4 -> 36.36% |
| DuneViper | 1 | 1 | 1 -> 11.11% | 1 -> 11.11% | 1 -> 10.00% | 1 -> 9.09% | 1 -> 9.09% |

Tier cells show **weight -> conditional selection percentage**.

Map-specific weight progression: `{}`. Percentages above are the full-weight baseline; a nonempty progression table changes them during its ramp.

| Spawn/economy setting | Value |
| --- | --- |
| InteractibleCredits | 240 |
| Spawning.InitialIncome | 2 |
| Spawning.FinalIncome | 4 |
| Spawning.AmbientIncome | 0.75 |
| Spawning.SpawnRampDuration | 900 |
| Spawning.ActiveInterval | 2 |
| Spawning.AmbientInterval | 10 |
| Spawning.ActiveBankCapacity | 180 |
| Spawning.AmbientBankCapacity | 90 |
| Population.MaximumEnemies | 180 |
| Population.MaximumLocalEnemies | 40 |
| Population.MaximumAmbientEnemies | 12 |
| Population.LocalRadius | 120 |
| Population.DespawnDistance | 600 |
| Population.DespawnDelay | 30 |
| AmbientPlacement.MinDistance | 70 |
| AmbientPlacement.MaxDistance | 110 |
| AmbientPlacement.FloorSearch | 48 |
| AmbientDetectionRadius | 40 |

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/MapConfig/RustwakeWreck.luau)

**Chest cards**

| Chest template | Gold cost | Director cost | Weight | Item rarity | Max per stage per participant | Opening seconds |
| --- | --- | --- | --- | --- | --- | --- |
| ChestTemplates:WaitForChild("ScoutCache") | 50 | 15 | 10 | "White" | 20 | 0.4 |
| ChestTemplates:WaitForChild("CargoCache") | 50 | 15 | 2 | "White" | 4 | 0.4 |
| ChestTemplates:WaitForChild("VaultCache") | 150 | 45 | 3 | "Green" | 4 | 0.75 |

### FloodedQuarry — active rotation


**Active pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Parallax | 0.05 | 1 | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0.05 -> 0.99% |
| ReedStalker | 1 | 1 | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 19.80% |
| Barkback | 1 | 1 | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 19.80% |
| DuneViper | 1 | 1 | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 19.80% |
| AdultAntlion | 1 | 1 | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 19.80% |
| QuarrySlime | 1 | 1 | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 20.00% | 1 -> 19.80% |

Tier cells show **weight -> conditional selection percentage**.

**Ambient pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| QuarrySlime | 1 | 1 | 1 -> 100.00% | 1 -> 100.00% | 1 -> 100.00% | 1 -> 100.00% | 1 -> 100.00% |

Tier cells show **weight -> conditional selection percentage**.

Map-specific weight progression: `{}`. Percentages above are the full-weight baseline; a nonempty progression table changes them during its ramp.

| Spawn/economy setting | Value |
| --- | --- |
| InteractibleCredits | 150 |
| Spawning.InitialIncome | 4 |
| Spawning.FinalIncome | 6 |
| Spawning.AmbientIncome | 1.5 |
| Spawning.SpawnRampDuration | 900 |
| Spawning.ActiveInterval | 2 |
| Spawning.AmbientInterval | 10 |
| Spawning.ActiveBankCapacity | 180 |
| Spawning.AmbientBankCapacity | 90 |
| Population.MaximumEnemies | 120 |
| Population.MaximumLocalEnemies | 12 |
| Population.MaximumAmbientEnemies | 4 |
| Population.LocalRadius | 120 |
| Population.DespawnDistance | 600 |
| Population.DespawnDelay | 30 |
| AmbientPlacement.MinDistance | 70 |
| AmbientPlacement.MaxDistance | 110 |
| AmbientPlacement.FloorSearch | 16 |
| AmbientDetectionRadius | 40 |

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/MapConfig/FloodedQuarry.luau)

**Chest cards**

| Chest template | Gold cost | Director cost | Weight | Item rarity | Max per stage per participant | Opening seconds |
| --- | --- | --- | --- | --- | --- | --- |
| ChestTemplates:WaitForChild("ScoutCache") | 50 | 15 | 10 | "White" | 10 | 0.4 |
| ChestTemplates:WaitForChild("CargoCache") | 50 | 15 | 2 | "White" | 4 | 0.4 |
| ChestTemplates:WaitForChild("VaultCache") | 150 | 45 | 3 | "Green" | 3 | 0.75 |

### HeightsExpansion — inactive map configuration


**Active pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Parallax | 0.1 | 1 | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0.1 -> 0.78% |
| Skeleton | 1 | 1 | 6 -> 68.73% | 5 -> 53.48% | 4 -> 38.10% | 3 -> 26.79% | 2 -> 15.62% |
| Knight | 1 | 1 | 2 -> 22.91% | 3 -> 32.09% | 4 -> 38.10% | 4 -> 35.71% | 4 -> 31.25% |
| Noob | 0.2 | 1 | 0.2 -> 2.29% | 0.4 -> 4.28% | 0.6 -> 5.71% | 0.8 -> 7.14% | 1 -> 7.81% |
| BalloonBomb | 0.05 | 1 | 0.05 -> 0.57% | 0.1 -> 1.07% | 0.2 -> 1.90% | 0.3 -> 2.68% | 0.5 -> 3.91% |
| WreckingBallGuest | 0.12 | 1 | 0.12 -> 1.37% | 0.2 -> 2.14% | 0.4 -> 3.81% | 0.8 -> 7.14% | 1.5 -> 11.72% |
| RoyalGuard | 0.1 | 1 | 0.1 -> 1.15% | 0.2 -> 2.14% | 0.4 -> 3.81% | 0.8 -> 7.14% | 1.5 -> 11.72% |
| Necromancer | 0.08 | 1 | 0.08 -> 0.92% | 0.15 -> 1.60% | 0.3 -> 2.86% | 0.6 -> 5.36% | 1 -> 7.81% |
| Shieldbearer | 0.18 | 1 | 0.18 -> 2.06% | 0.3 -> 3.21% | 0.6 -> 5.71% | 0.9 -> 8.04% | 1.2 -> 9.38% |

Tier cells show **weight -> conditional selection percentage**.

**Ambient pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Skeleton | 3 | 1 | 6 -> 75.00% | 5 -> 62.50% | 4 -> 50.00% | 3 -> 42.86% | 2 -> 33.33% |
| Knight | 2 | 1 | 2 -> 25.00% | 3 -> 37.50% | 4 -> 50.00% | 4 -> 57.14% | 4 -> 66.67% |

Tier cells show **weight -> conditional selection percentage**.

Map-specific weight progression: `{'Knight': {'Start': '0.1', 'Full': '0.3'}, 'Noob': {'Start': '0.1', 'Full': '0.3'}, 'BalloonBomb': {'Start': '0.25', 'Full': '0.5'}, 'Shieldbearer': {'Start': '0.4', 'Full': '0.7'}, 'Necromancer': {'Start': '0.5', 'Full': '0.8'}, 'RoyalGuard': {'Start': '0.6', 'Full': '0.9'}, 'WreckingBallGuest': {'Start': '0.75', 'Full': '1'}}`. Percentages above are the full-weight baseline; a nonempty progression table changes them during its ramp.

| Spawn/economy setting | Value |
| --- | --- |
| InteractibleCredits | 240 |
| Spawning.InitialIncome | 2 |
| Spawning.FinalIncome | 4 |
| Spawning.AmbientIncome | 0.75 |
| Spawning.SpawnRampDuration | 900 |
| Spawning.ActiveInterval | 2 |
| Spawning.AmbientInterval | 10 |
| Spawning.ActiveBankCapacity | 180 |
| Spawning.AmbientBankCapacity | 90 |
| Population.MaximumEnemies | 400 |
| Population.MaximumLocalEnemies | 40 |
| Population.MaximumAmbientEnemies | 12 |
| Population.LocalRadius | 120 |
| Population.DespawnDistance | 600 |
| Population.DespawnDelay | 30 |
| AmbientPlacement.MinDistance | 70 |
| AmbientPlacement.MaxDistance | 110 |
| AmbientPlacement.FloorSearch | 48 |
| AmbientDetectionRadius | 40 |

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/MapConfig/HeightsExpansion.luau)

**Chest cards**

| Chest template | Gold cost | Director cost | Weight | Item rarity | Max per stage per participant | Opening seconds |
| --- | --- | --- | --- | --- | --- | --- |
| ChestTemplates:WaitForChild("ArmoryChest") | 50 | 15 | 4 | "White" | 24 | 0.4 |
| ChestTemplates:WaitForChild("ClassicReliquaryChest") | 150 | 45 | 1 | "Green" | 4 | 0.75 |

### DeadwoodBasin — inactive map configuration


**Active pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Parallax | 0.05 | 1 | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0 -> 0.00% | 0.05 -> 0.99% |
| Barkback | 1 | 1 | 4 -> 80.00% | 3 -> 66.67% | 2 -> 50.00% | 1.5 -> 33.33% | 1 -> 19.80% |
| ReedStalker | 1 | 1 | 1 -> 20.00% | 1.5 -> 33.33% | 2 -> 50.00% | 3 -> 66.67% | 4 -> 79.21% |

Tier cells show **weight -> conditional selection percentage**.

**Ambient pool**

| Enemy | Fallback weight | Minimum stage | Easy | Normal | Hard | Insane | Nightmare |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Barkback | 1 | 1 | 4 -> 100.00% | 3 -> 100.00% | 2 -> 100.00% | 1.5 -> 100.00% | 1 -> 100.00% |

Tier cells show **weight -> conditional selection percentage**.

Map-specific weight progression: `{}`. Percentages above are the full-weight baseline; a nonempty progression table changes them during its ramp.

| Spawn/economy setting | Value |
| --- | --- |
| InteractibleCredits | 0 |
| Spawning.InitialIncome | 4 |
| Spawning.FinalIncome | 6 |
| Spawning.AmbientIncome | 1.5 |
| Spawning.SpawnRampDuration | 900 |
| Spawning.ActiveInterval | 2 |
| Spawning.AmbientInterval | 10 |
| Spawning.ActiveBankCapacity | 180 |
| Spawning.AmbientBankCapacity | 90 |
| Population.MaximumEnemies | 400 |
| Population.MaximumLocalEnemies | 40 |
| Population.MaximumAmbientEnemies | 12 |
| Population.LocalRadius | 120 |
| Population.DespawnDistance | 600 |
| Population.DespawnDelay | 30 |
| AmbientPlacement.MinDistance | 70 |
| AmbientPlacement.MaxDistance | 110 |
| AmbientPlacement.FloorSearch | 48 |
| AmbientDetectionRadius | 40 |

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ServerScriptService/MapConfig/DeadwoodBasin.luau)

**Chest cards**

| Chest template | Gold cost | Director cost | Weight | Item rarity | Max per stage per participant | Opening seconds |
| --- | --- | --- | --- | --- | --- | --- |

For chest selection and item reward odds, see [item acquisition](game-items.md#chest-selection-and-item-reward-odds).


### Heights Expansion: time-dependent odds

The earlier Heights tables are hypothetical full-weight comparisons. Early tiers do not actually reach all of those full weights: use the progression formula `effective weight = tier weight * clamp((min(run seconds / 900, 1) - Start) / (Full - Start), 0, 1)` before normalizing. Cards without a progression entry use their tier weight unchanged.

| Enemy | Begins ramping after | Full weight at |
| --- | --- | --- |
| Knight | 90 s | 270 s |
| Noob | 90 s | 270 s |
| BalloonBomb | 225 s | 450 s |
| Shieldbearer | 360 s | 630 s |
| Necromancer | 450 s | 720 s |
| RoyalGuard | 540 s | 810 s |
| WreckingBallGuest | 675 s | 900 s |

**Cards: actual tier-start snapshots**, assuming no card exclusion by capacity, stage, or placement cooldown. Probabilities change continuously between these snapshots while ramps are active.

| Enemy | 0 s | 180 s | 360 s | 600 s | 900 s |
| --- | --- | --- | --- | --- | --- |
| Parallax | 0.00% | 0.00% | 0.00% | 0.00% | 0.78% |
| Skeleton | 100.00% | 74.63% | 45.87% | 31.88% | 15.62% |
| Knight | 0.00% | 22.39% | 45.87% | 42.50% | 31.25% |
| Noob | 0.00% | 2.99% | 6.88% | 8.50% | 7.81% |
| BalloonBomb | 0.00% | 0.00% | 1.38% | 3.19% | 3.91% |
| WreckingBallGuest | 0.00% | 0.00% | 0.00% | 0.00% | 11.72% |
| RoyalGuard | 0.00% | 0.00% | 0.00% | 1.89% | 11.72% |
| Necromancer | 0.00% | 0.00% | 0.00% | 3.54% | 7.81% |
| Shieldbearer | 0.00% | 0.00% | 0.00% | 8.50% | 9.37% |

**AmbientCards: actual tier-start snapshots**, assuming no card exclusion by capacity, stage, or placement cooldown. Probabilities change continuously between these snapshots while ramps are active.

| Enemy | 0 s | 180 s | 360 s | 600 s | 900 s |
| --- | --- | --- | --- | --- | --- |
| Skeleton | 100.00% | 76.92% | 50.00% | 42.86% | 33.33% |
| Knight | 0.00% | 23.08% | 50.00% | 57.14% | 66.67% |
