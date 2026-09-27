# Characters

[Content index](game-content-list.md) | [How to read the stats](game-content-stats.md)

Source snapshot: 2026-09-27. This records existing source definitions and configured values, not completed live acceptance testing. Runtime settings, level, inventory, and state can change gameplay outcomes.

## Roster

Two [character definitions](https://github.com/DrasticDeveloping/rain/tree/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters):

| Character | Existing kit |
| --- | --- |
| Commando | Primary Fire, Phase Round, Tactical Dive, Suppressive Fire. |
| Railgunner | Primary, secondary/scope, utility, and special abilities; scoped weak-point targeting and reload mechanics. |

## Stats and abilities

| Character / ability | What it does |
| --- | --- |
| Commando: Primary Fire | Repeating aimed hitscan shot, up to 250 studs, with a 0.25 s base cooldown and 1x attack damage. |
| Commando: Phase Round | A piercing projectile traveling at 120 studs/s for up to 2 s. Starts at 3x attack damage and adds 1.2x for each successive target. |
| Commando: Tactical Dive | Moves in the current movement direction, or forward when stationary, for 0.35 s at 4.5x movement speed with an upward boost of 22. It interrupts primary fire; base cooldown is 4 s. |
| Commando: Suppressive Fire | Fires `max(1, floor(6 * AttackSpeed))` aimed shots over 0.6 s. Each deals 1x attack damage and applies a 1 s stun; base cooldown is 6 s. |
| Railgunner: Primary, unscoped | Fires a homing smart round at 100 studs/s, with 150-stud targeting range and a 0.25 s base interval; deals 1x attack damage. |
| Railgunner: Secondary / scoped primary | Scoping enables a piercing rifle shot with 1000-stud range and 10x attack damage before weak-point and reload bonuses. Firing exits scope and starts the reload sequence. |
| Railgunner: Utility | Throws a concussion device up to 16 studs. After a 1 s fuse it pushes the owner and enemies within 14 studs, subject to line of sight; it deals no damage. Holds two charges, replenished one every 6 s; throws have a 0.15 s activation cooldown. Throwing another device detonates the previous active device. |
| Railgunner: Special | Charges for `2 / AttackSpeed` seconds, then provides a three-second window to fire a 40x Super shot. Firing imposes `5 / AttackSpeed` seconds of recovery, followed by the 15 s special cooldown. |

Railgunner utility pushes the owner with strength 65 for 1 s and enemies with strength 60 for 0.5 s. It does not push other players. [Concussion device](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Railgunner/Concussion/init.luau).

| Character | HP | Attack damage | Defense | Attack speed | Move speed | HP/level | Damage/level | Passive healing |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Commando | 100 | 20 | 10 | 1 | 16 | +20 | No built-in per-level damage gain | 1 + 0.2 × (level - 1) HP/s |
| Railgunner | 110 | 12 | 0 | 1 | 16 | +33 | +2.4 | 1 + 0.2 × (level - 1) HP/s |

Railgunner declares 1% critical chance and critical damage multiplier 2; its scoped weak-point rules use the dedicated ballistics path. XP to advance from level L is `100 × L`; total XP to reach level L is `50 × L × (L - 1)`. Sources: [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Commando/init.luau), [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Railgunner/init.luau), [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Entity/Character.luau), [Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Entity/XP.luau).

### Commando / PhaseRound

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Commando/PhaseRound.luau)

| Parameter | Configured value |
| --- | --- |
| Cooldown | 3 |
| DamageMultiplier | 3 |
| DamageIncrement | 1.2 |
| Projectile.Mode | "Normal" |
| Projectile.Detection | "Server" |
| Projectile.Predict | true |
| Projectile.Speed | 120 |
| Projectile.Lifetime | 2 |
| Projectile.Piercing | true |

### Commando / PrimaryFire

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Commando/PrimaryFire.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 0.25 |
| RepeatWhileHeld | true |
| Range | 250 |
| DamageMultiplier | 1 |
| Projectile.Mode | "Hitscan" |
| Projectile.Detection | "Server" |
| Projectile.Predict | true |
| Projectile.Range | Module.Range |
| Projectile.CheckMuzzle | true |

### Commando / SuppressiveFire

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Commando/SuppressiveFire.luau)

| Parameter | Configured value |
| --- | --- |
| Cooldown | 6 |
| Duration | 0.6 |
| BaseShots | 6 |
| DamageMultiplier | 1 |
| StunDuration | 1 |
| TrackAim | true |
| InterruptPrimary | true |
| Projectile | PrimaryFire.Projectile |

### Commando / TacticalDive

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Commando/TacticalDive.luau)

| Parameter | Configured value |
| --- | --- |
| Cooldown | 4 |
| Duration | 0.35 |
| SpeedMultiplier | 4.5 |
| UpwardBoost | 22 |
| InterruptPrimary | true |

### Railgunner weapon, reload, scope, utility, and special tuning

[Source](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Railgunner/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| SmartDamage | 1 |
| SmartInterval | 0.25 |
| SmartRange | 150 |
| SmartSpeed | 100 |
| SmartTurnSpeed | math.rad(240) |
| SmartCone | math.cos(math.rad(120)) |
| RifleDamage | 10 |
| RifleRange | 1000 |
| RifleRadius | 0.35 |
| PierceMultiplier | 0.5 |
| ReloadBonus | 5 |
| ReloadDuration | 2 |
| ReloadPerfectAt | 0.5 |
| ReloadWindow | 0.2 |
| ScopeDuration | 0.116667 |
| ScopeOutDuration | 0.14 |
| ScopeFieldOfView | 32 |
| ScopeSensitivity | 0.75 |
| UnscopeDuration | 0.233333 |
| SuperDamage | 40 |
| SuperRadius | 1.5 |
| SuperWeakPointMultiplier | 1.5 |
| SuperChargeDuration | 2 |
| SuperHoldDuration | 3 |
| SuperRecoveryDuration | 5 |
| SuperCooldown | 15 |
| DeviceCooldown | 6 |
| DeviceFuse | 1 |
| DeviceRadius | 14 |
| DeviceThrowRange | 16 |
| DeviceImpulse | 65 |
| DeviceEnemyImpulse | 60 |
| DeviceEnemyDuration | 0.5 |

### Railgunner damage examples

At level 1 with no items and no reload bonus: smart shot = 12 raw damage; rifle body hit = 120; Super body hit = 480. A weak point multiplies rifle/Super damage by `CriticalDamage + CriticalChance/100`, initially `2 + 1/100 = 2.01`. Super adds another 1.5x weak-point multiplier: rifle weak point = 241.2 and Super weak point = 1447.2 raw damage. These are before defense and protection.

A perfect reload adds 5 to the rifle/Super attack multiplier, not 5 damage: rifle body becomes 180; Super body becomes 540. Rifle damage halves for every additional pierced target (`0.5^(hit index - 1)`); Super does not use that falloff. Super's proc coefficient is 3, ordinary shots use 1. At attack-speed rate 1, the perfect window spans 0.4-0.6 s after reload starts; attack speed changes its width. [Ballistics](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Railgunner/Ballistics.luau), [reload](https://github.com/DrasticDeveloping/rain/blob/b49a73f60f7fb18db88dffe87783fa2c208e28a7/src/ReplicatedStorage/Modues/Characters/Railgunner/Weapon.luau).

Commando: primary is 20 raw damage at a base 0.25 s cooldown; Phase Round begins at 60 and adds 24 per additional pierced target; Suppressive Fire begins with six 20-damage shots across 0.6 s, with 1 s stun. Ability rate/scaling and target protection still apply.
