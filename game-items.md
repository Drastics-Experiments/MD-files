# Items

[Content index](game-content-list.md) | [How to read the stats](game-content-stats.md)

Source snapshot: 2026-09-27. This records existing source definitions and configured values, not completed live acceptance testing. Runtime settings, level, inventory, and state can change gameplay outcomes.

## Inventory

14 regular item definitions plus one debug-only item. Names, rarity, and effects below come from the [current item modules](../src/ReplicatedStorage/Modues/Items), rather than older concept documents.

| Item | Rarity | Effect |
| --- | --- | --- |
| Bloxy Cola | White | Kills temporarily increase attack speed. |
| Cheezburger | White | Kills restore health. |
| Knight Armor | White | Increases maximum health. |
| Linked Sword | White | Close-range shots trigger bonus slash damage. |
| Pizza Slice | White | Consumed at low health for an emergency heal. |
| Speed Coil | White | Increases movement speed. |
| Builders Hard Hat | Green | Large incoming hits temporarily grant armor. |
| Checkpoint Flag | Green | Staying in a small area creates healing for nearby players. |
| Clockwork Shades | Green | Increases critical chance; grants weak-point damage for Railgunner instead. |
| Darkheart Sword | Green | Successful shot hits restore health. |
| Gravity Coil | Green | Improves jump height and air control. |
| Happy Home Balloon | Green | Adds midair jumps, restored on landing. |
| Telamon's Boombox | Green | Shot hits can chain sound damage between enemies. |
| Venomshank Sword | Green | Shot hits can apply stacking poison. |
| Debug Damage | Red; debug only | Multiplies attack damage; excluded from chest rewards. |

## Stats and stacking

Descriptions below are from the current item definitions. Additional tunable fields are included beneath each item; proc coefficients can scale trigger chances or effects as implemented in the linked source.

### Bloxy Cola — White

Kills grant +20% attack speed per copy for 3s

[Source](../src/ReplicatedStorage/Modues/Items/BloxyCola/init.luau)

| Parameter | Value |
| --- | --- |
| Duration | 3 |
| AttackBonus | 0.2 |

### Builders Hard Hat — Green

Hits of 20% max health grant +60 armor per copy for 3s (8s cooldown)

[Source](../src/ReplicatedStorage/Modues/Items/BuildersHardHat/init.luau)

| Parameter | Value |
| --- | --- |
| Threshold | 0.2 |
| DefensePerCopy | 60 |
| Duration | 3 |
| Cooldown | 8 |

### Checkpoint Flag — Green

Stay within 3 studs for 3s to heal all players 3 health/s in a 6-stud radius; extra copies add 1 health/s and 10% base radius

[Source](../src/ReplicatedStorage/Modues/Items/CheckpointFlag/init.luau)

| Parameter | Value |
| --- | --- |
| PlacementDelay | 3 |
| PlacementRadius | 3 |
| HealingRadius | 6 |
| HealingPerSecond | 3 |
| RadiusBonusPerAdditionalCopy | 0.1 |
| HealingPerAdditionalCopy | 1 |

### Cheezburger — White

Kills restore 4 health per copy

[Source](../src/ReplicatedStorage/Modues/Items/Cheezburger/init.luau)

| Parameter | Value |
| --- | --- |
| HealingPerKill | 4 |

### Clockwork Shades — Green

+10% critical-hit chance per copy; Railgunner gains weak-point damage instead

[Source](../src/ReplicatedStorage/Modues/Items/ClockworkShades/init.luau)

| Parameter | Value |
| --- | --- |
| Modifiers.CriticalChance.Add | 10 |

### Darkheart Sword — Green

Successful shot hits restore 1 health per copy, scaled by proc coefficient

[Source](../src/ReplicatedStorage/Modues/Items/DarkheartSword/init.luau)

| Parameter | Value |
| --- | --- |
| HealingPerCopy | 1 |

### Debug Damage — Red

+400% attack damage per copy (5x with one). Debug only; never awarded by chests.

[Source](../src/ReplicatedStorage/Modues/Items/DebugDamage.luau)

| Parameter | Value |
| --- | --- |
| DebugOnly | true |
| Modifiers.AttackDamage.Multiply | 5 |

### Gravity Coil — Green

+50% jump height × square root of copies; improved air control

[Source](../src/ReplicatedStorage/Modues/Items/GravityCoil.luau)

| Parameter | Value |
| --- | --- |
| JumpBonus | 0.5 |
| AirControl | 6 |

### Happy Home Balloon — Green

Gain 1 extra midair jump per copy; landing restores your jumps

[Source](../src/ReplicatedStorage/Modues/Items/HappyHomeBalloon/init.luau)

| Parameter | Value |
| --- | --- |
| JumpInterval | 0.15 |

### Knight Armor — White

+15 maximum health per copy

[Source](../src/ReplicatedStorage/Modues/Items/KnightArmor.luau)

| Parameter | Value |
| --- | --- |
| Modifiers.MaxHealth.Add | 15 |

### Linked Sword — White

Shots within 12 studs slash for +50% damage per copy

[Source](../src/ReplicatedStorage/Modues/Items/LinkedSword/init.luau)

| Parameter | Value |
| --- | --- |
| Range | 12 |
| DamageMultiplier | 0.5 |

### Pizza Slice — White

Consumed at 20% health or lower to restore 50% max health

[Source](../src/ReplicatedStorage/Modues/Items/PizzaSlice/init.luau)

| Parameter | Value |
| --- | --- |
| HealthThreshold | 0.2 |
| HealFraction | 0.5 |
| Update | Module.OnDamaged |

### Speed Coil — White

+15% movement speed per copy

[Source](../src/ReplicatedStorage/Modues/Items/SpeedCoil.luau)

| Parameter | Value |
| --- | --- |
| Modifiers.MoveSpeed.Multiply | 1.15 |

### Telamon's Boombox — Green

25% chance on shot hit to chain sound to 3 enemies for 80% shot damage; extra copies add 2 targets and 2 studs of range

[Source](../src/ReplicatedStorage/Modues/Items/TelamonsBoombox/init.luau)

| Parameter | Value |
| --- | --- |
| Chance | 0.25 |
| DamageMultiplier | 0.8 |
| Targets | 3 |
| TargetsPerCopy | 2 |
| Range | 20 |
| RangePerCopy | 2 |

### Venomshank Sword — Green

10% chance per copy on shot hit to poison for 240% base damage over 3s; poison stacks

[Source](../src/ReplicatedStorage/Modues/Items/VenomshankSword/init.luau)

| Parameter | Value |
| --- | --- |
| ChancePerCopy | 0.1 |
| TickInterval | 0.25 |
| Ticks | 12 |
| DamagePerTick | 0.2 |

## Additional item formulas

Let `n` be item copies and `p` be the triggering shot's proc coefficient.

- Venomshank: poison chance = `min(1, 0.1 * n * p)`; 12 ticks, each 0.2 * attack damage, at 0.25 s intervals. Successful procs add separate poison stacks.
- Telamon's Boombox: trigger threshold = `0.25 * p`; up to `3 + 2 * (n - 1)` chain targets; range `20 + 2 * (n - 1)`; chain damage is 0.8 * supplied shot damage.
- Darkheart: healing = `n * p` HP per qualifying shot hit.
- Linked Sword: within 12 studs, bonus raw damage = `0.5 * n * AttackDamage`; it is not 50% of an already multiplied rifle/Super hit.
- Gravity Coil: jump-height multiplier = `1 + 0.5 * sqrt(n)`; air-control bonus remains 6 while owned.
- Checkpoint Flag: healing radius = `6 * (1 + 0.1 * (n - 1))`; healing = `3 + (n - 1)` HP/s. Requires remaining within 3 studs for 3 s to plant.

These formulas come from the item modules linked in the item section. Healing is bounded by missing health, and actual damage follows the target's protection/defense path.

## Chest selection and item reward odds

Chest weights are also relative, filtered by remaining credits, available markers, and per-stage caps. Each newly participating player adds that map’s InteractibleCredits budget; caps multiply by participant count. A qualifying item is selected uniformly from the chest’s item pool, excluding DebugOnly items. With the current unmodified pools, White-only rewards are 1/6 (16.67%) per White item, and Green-only rewards are 1/8 (12.5%) per Green item. The debug Red item has 0% chest chance. Chest-card weights do not mean item-rarity odds across a whole stage. Sources: [Source](../src/ServerScriptService/InteractibleDirector.luau), [Source](../src/ServerScriptService/ItemPedestals.luau).

Map-specific chest prices, budgets, weights, and caps are in [maps and spawning](game-maps.md).
