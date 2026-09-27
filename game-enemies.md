# Enemies and bosses

[Content index](game-content-list.md) | [How to read the stats](game-content-stats.md)

Source snapshot: 2026-09-27. This records existing source definitions and configured values, not completed live acceptance testing. Runtime settings, level, inventory, and state can change gameplay outcomes.

## Roster

22 [enemy definitions](../src/ReplicatedStorage/Modues/Enemies), including bosses, summons, and size variants. Names are spaced for readability; this list includes enemies belonging to inactive maps.

- Adult Antlion
- Balloon Bomb
- Barkback
- Dune Skitter
- Dune Viper
- Foundation Titan
- Glass Tail
- Knight
- Magma Worm
- Necromancer
- Noob
- Parallax
- Quarry Slime
- Quarry Slime Medium
- Quarry Slime Small
- Reed Stalker
- Royal Guard
- Rustback
- Shardling
- Shieldbearer
- Skeleton
- Wrecking Ball Guest

Railgunner weak-point configuration now exists for all 22 definitions. See the [weak-point implementation notes](enemy-weak-points.md) for verification limits.

Spawn pools, percentages by difficulty, timing, and population limits are in [maps and spawning](game-maps.md#enemy-spawn-selection-chances).

## Reading enemy stats

Attack damage is a base stat, not necessarily the damage of every attack. Attacks may multiply it or supply a fixed damage value. Attack speed is a stat multiplier, not a guaranteed attacks-per-second rate. Defense normally scales incoming damage by `100 / (100 + max(0, Defense))`; enemy protection can override that calculation. Enemy stats are set on spawn to `base + (EnemyLevel - 1) × per-level gain`. The run difficulty index supplies EnemyLevel (1–5); missing gains mean no extra gain from that definition. Gold and XP columns are configured kill rewards.

Source expressions are retained when a value depends on runtime state, rig geometry, or another module; they are not invented numeric defaults. Field names in detailed tables match the code for easy lookup.

## Base stats

| Enemy | HP | Damage | Defense | Attack speed | Move speed | HP/level | Damage/level | Gold | XP | Director cost |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [AdultAntlion](../src/ReplicatedStorage/Modues/Enemies/AdultAntlion/init.luau) | 110 | 16 | 4 | 1 | 15 | 24 | 3 | 18 | 18 | 32 |
| [BalloonBomb](../src/ReplicatedStorage/Modues/Enemies/BalloonBomb/init.luau) | 40 | 300 | 0 | 1 | 8 | 6 | 20 | 10 | 10 | 30 |
| [Barkback](../src/ReplicatedStorage/Modues/Enemies/Barkback/init.luau) | 140 | 16 | 12 | 1 | 10 | 40 | 2 | 14 | 14 | 35 |
| [DuneSkitter](../src/ReplicatedStorage/Modues/Enemies/DuneSkitter.luau) | 110 | 14 | 0 | 1 | 9 | 20 | 2 | 12 | 12 | 10 |
| [DuneViper](../src/ReplicatedStorage/Modues/Enemies/DuneViper/init.luau) | 180 | 20 | 5 | 1 | 9 | 0 | 0 | 24 | 24 | 20 |
| [FoundationTitan](../src/ReplicatedStorage/Modues/Enemies/FoundationTitan/init.luau) | 6000 | 36 | 35 | 1 | 32 | 1500 | 5 | 150 | 250 | Not director-purchased |
| [GlassTail](../src/ReplicatedStorage/Modues/Enemies/GlassTail.luau) | 200 | 16 | 15 | 1 | 2.4 | 40 | 3 | 22 | 22 | 30 |
| [Knight](../src/ReplicatedStorage/Modues/Enemies/Knight/init.luau) | 100 | 12 | 53.8462 | 0.8 | 10 | 30 | 3 | 10 | 10 | 25 |
| [MagmaWorm](../src/ReplicatedStorage/Modues/Enemies/MagmaWorm/init.luau) | 420 | 26 | 15 | 1 | 12 | 0 | 0 | 40 | 40 | 40 |
| [Necromancer](../src/ReplicatedStorage/Modues/Enemies/Necromancer/init.luau) | 240 | 16 | 25 | 1 | 8 | 40 | 3 | 45 | 45 | 65 |
| [Noob](../src/ReplicatedStorage/Modues/Enemies/Noob/init.luau) | 55 | 8 | 0 | 1 | 3 | 10 | 1 | 10 | 10 | 20 |
| [Parallax](../src/ReplicatedStorage/Modues/Enemies/Parallax/init.luau) | 4500 | 24 | 15 | 1 | 5.5 | 900 | 4 | 150 | 250 | 150 |
| [QuarrySlime](../src/ReplicatedStorage/Modues/Enemies/QuarrySlime/init.luau) | 260 | 24 | 0 | 1 | 5 | 65 | 3 | 12 | 18 | 45 |
| [QuarrySlimeMedium](../src/ReplicatedStorage/Modues/Enemies/QuarrySlimeMedium/init.luau) | 95 | 14 | 0 | 1 | 7 | 20 | 2 | 6 | 8 | Not director-purchased |
| [QuarrySlimeSmall](../src/ReplicatedStorage/Modues/Enemies/QuarrySlimeSmall/init.luau) | 35 | 7 | 0 | 1 | 9 | 6 | 1 | 3 | 4 | Not director-purchased |
| [ReedStalker](../src/ReplicatedStorage/Modues/Enemies/ReedStalker/init.luau) | 85 | 14 | 0 | 1 | 12 | 15 | 3 | 18 | 18 | 30 |
| [RoyalGuard](../src/ReplicatedStorage/Modues/Enemies/RoyalGuard/init.luau) | 500 | 24 | 100 | 1 | 9 | 150 | 3 | 40 | 40 | 60 |
| [Rustback](../src/ReplicatedStorage/Modues/Enemies/Rustback.luau) | 420 | 100 | 50 | 1 | 2 | 120 | 3 | 30 | 30 | 45 |
| [Shardling](../src/ReplicatedStorage/Modues/Enemies/Shardling/init.luau) | 45 | 8 | 0 | 1 | 12 | 8 | 1 | 0 | 0 | Not director-purchased |
| [Shieldbearer](../src/ReplicatedStorage/Modues/Enemies/Shieldbearer/init.luau) | 360 | 18 | 25 | 1 | 8 | 100 | 2 | 30 | 30 | 40 |
| [Skeleton](../src/ReplicatedStorage/Modues/Enemies/Skeleton/init.luau) | 80 | 12 | 5 | 0.8 | 10 | 18 | 2 | 10 | 10 | 10 |
| [WreckingBallGuest](../src/ReplicatedStorage/Modues/Enemies/WreckingBallGuest/init.luau) | 900 | 24 | 50 | 1 | 10 | 225 | 4 | 60 | 60 | 80 |

FoundationTitan and Shardling have no director purchase card/cost in their definitions; the medium/small Quarry Slimes arise from splitting. Absence from a map pool means no automatic selection from that pool, not that an enemy cannot be summoned or spawned by a command.

## Attack, movement, spawning, and protection details

These are level-1 raw attack amounts before the target's defense/protection, not guaranteed health removed:

| Enemy | Raw damage examples |
| --- | --- |
| Adult Antlion | Bite 20 (1.25x); acid spit 16 (1x). |
| Balloon Bomb | Explosion 300 base. |
| Barkback | Snap 16 (1x); charge 24 (1.5x). |
| Dune Skitter | Bite 14; sand spit 11.2 (0.8x). |
| Dune Viper | Emerge 24 (1.2x); venom impact 20; lingering venom 7 per tick (0.35x), interval 0.75 s. |
| Foundation Titan | Fixed slam 36, finger projectile 18, beam 9 per tick. These fixed Amount values do not automatically use its AttackDamage level gain. |
| Glass Tail | Pincer contact 12 (0.75x), two scheduled contacts; volley projectile 12, three projectiles. |
| Knight | Strike 12 (1x). |
| Magma Worm | Eruption 33.8 (1.3x); body contact 16.9 (0.65x), shared per-target contact interval 0.6 s. |
| Necromancer | Bolt 16 (1x). |
| Noob | Pellet 4 (0.5x), 1-4 pellets per burst. |
| Parallax | Fixed volley 9, laser 9, beam 12 per tick. These fixed Amount values do not automatically use its AttackDamage level gain. |
| Quarry Slime / Medium / Small | Strike 24 / 14 / 7 (1x). |
| Reed Stalker | Projectile 14 (1x). |
| Royal Guard | Sweep 24; thrust 30 (1.25x). |
| Rustback | Ram 100 (1x). |
| Shardling | Strike 8 (1x). |
| Shieldbearer | Base strike 18; broken-shield multiplier 0.5 produces 9. |
| Skeleton | Strike 12 (1x). |
| Wrecking Ball Guest | Swing 24; slam 36 (1.5x); rampage 6 per 0.5 s hit interval (0.25x). |

Quarry Slime children inherit the shared attack: 3.2 s cooldown, contact at `1.04 / attack rate`, completion at `2.8 / attack rate`; start ranges are 12 / 10 / 7.5 for large / medium / small. A large slime splits into two medium slimes, each of which can split into two small slimes. Splits require capacity and two valid clear placements, so blocked splits are not guaranteed. [Attack](../src/ReplicatedStorage/Modues/Enemies/QuarrySlime/Attack.luau), [splitting](../src/ReplicatedStorage/Modues/Enemies/QuarrySlime/Protection.luau).

Foundation Titan's exposed CoreIdle phase sets defense to zero and doubles incoming damage for its configured 6 s core window. Necromancer has a separate 240 raw-damage barrier; summoning costs 80 barrier, summons two Skeletons, and caps living summons at six. Royal Guard breaks armor after 300 raw damage and changes defense from 100 to 20. Shieldbearer's shield has 240 durability and a 110-degree arc. See the linked definitions, tuning, and protection modules below.

Detailed fields supplement the base-stat summary. Multipliers apply to base AttackDamage unless the attack source specifies otherwise. Expressions such as `math.rad(110)` specify angles in radians derived from the displayed degrees. Indexed attack/pack rows preserve their source order. Legacy Spawn.Chance values are listed for completeness only; use the map director tables for actual card selection.

### AdultAntlion

[Source](../src/ReplicatedStorage/Modues/Enemies/AdultAntlion/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.4 |
| Spawn.MinDistance | 30 |
| Spawn.MaxDistance | 50 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 48 |
| HitVolume.Size | Vector3.new(4.5, 4.5, 7) |
| HitVolume.Offset | CFrame.new(0, 0.4, 0) |
| Position.Mode | "Ground" |
| Position.AgentRadius | 3 |
| Position.AgentHeight | 4.5 |
| Position.RootHeight | 1.6 |
| Position.FlightOffset | Vector3.new(0, 0.4, 0) |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | true |
| Position.TurnDuration | 0.25 |

### AdultAntlion / Bite

[Source](../src/ReplicatedStorage/Modues/Enemies/AdultAntlion/Bite.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 2.6 |
| StartRange | Tuning.BiteRange |
| Range | Tuning.BiteRange |
| HalfWidth | 2.8 |
| Height | 6 |

### AdultAntlion / Spit

[Source](../src/ReplicatedStorage/Modues/Enemies/AdultAntlion/Spit.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 3.8 |
| StartRange | Tuning.SpitRange |
| Projectile.Mode | "Normal" |
| Projectile.Detection | "Server" |
| Projectile.Predict | false |
| Projectile.StopAtWorld | true |
| Projectile.Speed | Tuning.ProjectileSpeed |
| Projectile.Lifetime | Tuning.ProjectileLifetime |

### AdultAntlion / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/AdultAntlion/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| RootHeight | 1.6 |
| TakeoffDistance | 46 |
| LandingDistance | 20 |
| GroundSpeed | 15 |
| FlyHeight | 10 |
| FlightSpeed | 16 |
| FlightDuration | 30 |
| RestDuration | 4 |
| TakeoffDuration | 1.6 |
| LandingDuration | 1.6 |
| BiteRange | 7 |
| BiteContact | 0.9 |
| BiteDuration | 1.8 |
| SpitRange | 72 |
| SpitRelease | 1 |
| SpitDuration | 2 |
| ProjectileSpeed | 42 |
| ProjectileLifetime | 2.5 |

### BalloonBomb

[Source](../src/ReplicatedStorage/Modues/Enemies/BalloonBomb/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.MinDistance | 24 |
| Spawn.MaxDistance | 40 |
| Spawn.MinHeight | 8 |
| Spawn.MaxHeight | 15 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "Bomb" |
| HitVolume.Size | Vector3.new(3, 7, 3) |
| HitVolume.Offset | CFrame.identity |
| Attack.StartRange | 6 |
| Attack.Radius | 12 |
| Attack.Fuse | 0.8 |
| Attack.Offset | Vector3.new(0, -2, 0) |
| Position.Mode | "Fly" |
| Position.AgentRadius | 1.5 |
| Position.AgentHeight | 7 |
| Position.RootHeight | 3.5 |

### Barkback

[Source](../src/ReplicatedStorage/Modues/Enemies/Barkback/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.4 |
| Spawn.MinDistance | 30 |
| Spawn.MaxDistance | 50 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 48 |
| HitVolume.Size | Vector3.new(4.6, 3.2, 5.3) |
| HitVolume.Offset | CFrame.new(0, 0, -0.69) |
| Position.AgentRadius | 2.5 |
| Position.AgentHeight | 3.2 |
| Position.RootHeight | 1.6 |
| Position.RepathInterval | 1 |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | true |

### Barkback / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/Barkback/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 4 |
| StartRange | Tuning.ChargeRange |

### Barkback / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/Barkback/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| RootHeight | 1.6 |
| SnapRange | 7 |
| ChargeRange | 26 |
| ChargeMinimum | 10 |
| ChargeSpeed | 24 |
| ChargeDistance | 30 |
| ChargeWindup | 0.9 |
| ChargeDuration | 1.25 |
| ChargeRecovery | 1.2 |
| SnapHit | 0.533333 |
| SnapDuration | 1.2 |
| Strike.Range | 7 |
| Strike.HalfWidth | 3 |
| Strike.Height | 6 |

### DuneSkitter

[Source](../src/ReplicatedStorage/Modues/Enemies/DuneSkitter.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.65 |
| Spawn.Chance | 0.16 |
| Spawn.MinDistance | 28 |
| Spawn.MaxDistance | 44 |
| Spawn.FloorSearch | 12 |
| HitVolume.Size | Vector3.new(3.7, 3.5, 6) |
| HitVolume.Offset | CFrame.new(0, 0, -1) |
| Movement.Walk | 2.4375 |
| Movement.Run | 9 |
| Movement.RunThreshold | 4 |
| Attacks.1.Name | "Bite" |
| Attacks.1.Kind | "Melee" |
| Attacks.1.Range | 6.5 |
| Attacks.1.HalfWidth | 2.4 |
| Attacks.1.Height | 6 |
| Attacks.1.Duration | 1.33333 |
| Attacks.1.Contacts.1 | 0.5 |
| Attacks.1.Cooldown | 2.1 |
| Attacks.1.Multiplier | 1 |
| Attacks.2.Name | "SandSpit" |
| Attacks.2.Kind | "Projectile" |
| Attacks.2.MinRange | 10 |
| Attacks.2.Range | 42 |
| Attacks.2.Height | 16 |
| Attacks.2.Duration | 1.66667 |
| Attacks.2.Contacts.1 | 0.666667 |
| Attacks.2.Cooldown | 4 |
| Attacks.2.Multiplier | 0.8 |
| Attacks.2.Speed | 34 |
| Attacks.2.Lifetime | 1.6 |
| Attacks.2.Count | 1 |
| Attacks.2.Spread | 0 |
| Attacks.2.Size | 0.65 |
| Attacks.2.Color | Color3.fromRGB(210, 164, 95) |
| Position.Mode | "Ground" |
| Position.AgentRadius | 1.85 |
| Position.AgentHeight | 3.5 |
| Position.RootHeight | 1.75 |
| Position.WaypointTolerance | 0.25 |
| Position.RepathInterval | 1 |

### DuneViper

[Source](../src/ReplicatedStorage/Modues/Enemies/DuneViper/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.4 |
| Spawn.Chance | 0.12 |
| Spawn.MinDistance | 30 |
| Spawn.MaxDistance | 48 |
| Spawn.FloorSearch | 48 |
| HitVolume.Size | Vector3.new(2.8, 4, 10) |
| HitVolume.Offset | CFrame.new(0, 2, 4) |
| Position.Mode | "Ground" |
| Position.AgentRadius | 1.4 |
| Position.AgentHeight | 4 |
| Position.RootHeight | 0 |
| Position.RepathInterval | 1 |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | false |

### DuneViper / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/DuneViper/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | Tuning.Cooldown |
| StartRange | Tuning.Range |

### DuneViper / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/DuneViper/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| Range | 38 |
| CloseRange | 12 |
| BurrowSpeed | 18 |
| BurrowMinimum | 0.85 |
| BurrowRecovery | 0.7 |
| EmergeDuration | 1.4 |
| StrikeAt | 0.7 |
| StrikeRadius | 4.5 |
| SpitDuration | 1.6 |
| SpitReleaseAt | 0.65 |
| VenomDuration | 6.8 |
| VenomInterval | 0.75 |
| VenomRadius | 7 |
| Height | 7 |
| Cooldown | 1.5 |
| EmergeCooldown | 5 |
| SpitCooldown | 5 |
| LaunchSpeed | 38 |
| StunDuration | 0.5 |

### FoundationTitan

[Source](../src/ReplicatedStorage/Modues/Enemies/FoundationTitan/init.luau)

| Parameter | Configured value |
| --- | --- |
| Persistent | true |
| WeakPoint | "WeakPoint" |
| DeathDuration | Motion.Titan.Clips.Death.Duration |
| HitVolume.Size | Vector3.new(100, 90, 90)*0.5 |
| HitVolume.Offset | CFrame.new(0, 30*0.5, 0) |
| Position.Mode | "Fly" |
| Position.PreserveFacing | true |
| Position.TurnDuration | 0.7 |
| Position.AgentRadius | Tuning.FlightSize.X/2 |
| Position.AgentHeight | Tuning.FlightSize.Y |
| Position.FlightOffset | Vector3.new(0, 30, 0)*Module.Scale |

### FoundationTitan / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/FoundationTitan/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "BossAttack" |
| Cooldown | 0 |

### FoundationTitan / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/FoundationTitan/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| Scale | 0.5 |
| ChaseDistance | 18 |
| PatrolSpeed | 32 |
| WanderRadius | 70 |
| HoverHeight | 6 |
| AttackMoveScale | 0.8 |
| SlamCooldown | 10 |
| BeamCooldown | 12 |
| VolleyCooldown | 8 |
| TurnDuration | 0.7 |
| PoseBlendDuration | 0.35 |
| DetectionRadius | 320 |
| IdleDuration | 2 |
| CoreDuration | 6 |
| CoreDamageMultiplier | 2 |
| SlamRadius | 6 |
| SlamHeight | 7 |
| SlamDamage | 36 |
| BeamRange | 220 |
| BeamDamage | 9 |
| BeamTick | 0.35 |
| AimInterval | 0.05 |
| AimSpeed | 26 |
| FingerSpeed | 65 |
| FingerDamage | 18 |
| FingerArc | 8 |
| FingerImpactGroundReach | 6 |
| MaxShardlings | 12 |
| ShardlingLifetime | 45 |
| ShardlingRootHeight | 1.84 |
| SpawnCooldown | 10 |
| FlightSize | Vector3.new(36, 72, 36)*Module.Scale |
| FlightOffset | Vector3.new(0, 30, 0)*Module.Scale |

### GlassTail

[Source](../src/ReplicatedStorage/Modues/Enemies/GlassTail.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.85 |
| Spawn.Chance | 0.1 |
| Spawn.MinDistance | 32 |
| Spawn.MaxDistance | 48 |
| Spawn.FloorSearch | 12 |
| HitVolume.Size | Vector3.new(8.5, 3.2, 7) |
| HitVolume.Offset | CFrame.new(0, 0, -0.5) |
| Movement.Walk | 1.8 |
| Attacks.1.Name | "PincerCombo" |
| Attacks.1.Kind | "Melee" |
| Attacks.1.Range | 8.5 |
| Attacks.1.HalfWidth | 4.5 |
| Attacks.1.Height | 6 |
| Attacks.1.Duration | 2 |
| Attacks.1.Contacts.1 | 0.625 |
| Attacks.1.Contacts.2 | 1 |
| Attacks.1.Cooldown | 3 |
| Attacks.1.Multiplier | 0.75 |
| Attacks.2.Name | "GlassVolley" |
| Attacks.2.Kind | "Projectile" |
| Attacks.2.MinRange | 9 |
| Attacks.2.Range | 55 |
| Attacks.2.Height | 20 |
| Attacks.2.Duration | 2 |
| Attacks.2.Contacts.1 | 0.875 |
| Attacks.2.Cooldown | 4.5 |
| Attacks.2.Multiplier | 0.75 |
| Attacks.2.Speed | 38 |
| Attacks.2.Lifetime | 1.8 |
| Attacks.2.Count | 3 |
| Attacks.2.Spread | math.rad(6) |
| Attacks.2.Size | 0.55 |
| Attacks.2.Color | Color3.fromRGB(255, 194, 72) |
| Position.Mode | "Ground" |
| Position.AgentRadius | 4.5 |
| Position.AgentHeight | 3.2 |
| Position.RootHeight | 1.6 |
| Position.RepathInterval | 1.2 |

### Knight

[Source](../src/ReplicatedStorage/Modues/Enemies/Knight/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.MinDistance | 24 |
| Spawn.MaxDistance | 40 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "Head" |
| HitVolume.Size | Vector3.new(5, 6.4, 3.5) |
| HitVolume.Offset | CFrame.identity |
| Position.AgentRadius | 2.5 |
| Position.AgentHeight | 6.4 |
| Position.RootHeight | 3.2 |
| Position.RepathInterval | 1 |

### Knight / KnightStrike

[Source](../src/ReplicatedStorage/Modues/Enemies/Knight/KnightStrike.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 0 |
| StartRange | 9 |
| Range | 10 |
| HalfWidth | 3 |
| Height | 7 |
| Windup | 0.7 |
| Strike | 0.12 |
| Recovery | 0.65 |
| DamageMultiplier | 1 |
| CueHeight | 3.15 |

### MagmaWorm

[Source](../src/ReplicatedStorage/Modues/Enemies/MagmaWorm/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.5 |
| Spawn.Chance | 0.06 |
| Spawn.MinDistance | 38 |
| Spawn.MaxDistance | 56 |
| Spawn.FloorSearch | 48 |
| Spawn.UseAgentBounds | true |
| HitVolume.Size | Vector3.new(8, 10, 116) |
| HitVolume.Offset | CFrame.new(0, 5, 54) |
| Position.Mode | "Ground" |
| Position.AgentRadius | 4 |
| Position.AgentHeight | 10 |
| Position.RootHeight | 0 |
| Position.RepathInterval | 1 |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | false |

### MagmaWorm / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/MagmaWorm/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | Tuning.Cooldown |
| StartRange | Tuning.Range |

### MagmaWorm / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/MagmaWorm/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| Range | 90 |
| DiveDuration | 0.35 |
| BurrowMinimum | 0.2 |
| BurrowSpeed | 72 |
| BreachDuration | 1.2 |
| BreachHitAt | 0.2 |
| BreachRadius | 10 |
| LeapDistance | 36 |
| Height | 18 |
| Cooldown | 0 |
| TransitDistance | 40 |
| ContactRadius | 3 |
| ContactInterval | 0.6 |
| ContactMultiplier | 0.65 |

### Necromancer

[Source](../src/ReplicatedStorage/Modues/Enemies/Necromancer/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.Chance | 0.08 |
| Spawn.MinDistance | 32 |
| Spawn.MaxDistance | 48 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "WeakPoint" |
| HitVolume.Size | Vector3.one*5 |
| HitVolume.Offset | CFrame.identity |
| Barrier | 240 |
| Attack.Range | 55 |
| Attack.HeightTolerance | 8 |
| Attack.Bolt.Windup | 0.9 |
| Attack.Bolt.Active | 0.15 |
| Attack.Bolt.Recovery | 0.9 |
| Attack.Bolt.Cooldown | 3 |
| Attack.Bolt.Speed | 28 |
| Attack.Bolt.Homing | math.rad(120) |
| Attack.Bolt.Lifetime | 2 |
| Attack.Bolt.Size | 1.1 |
| Attack.Bolt.Color | Color3.fromRGB(165, 95, 235) |
| Attack.Bolt.DamageMultiplier | 1 |
| Attack.Summon.Windup | 1.8 |
| Attack.Summon.Active | 0.25 |
| Attack.Summon.Recovery | 1.1 |
| Attack.Summon.Cooldown | 12 |
| Attack.Summon.InitialCooldown | 4 |
| Attack.Summon.Count | 2 |
| Attack.Summon.LivingCap | 6 |
| Attack.Summon.BarrierCost | 80 |
| Attack.Summon.Spawn.MinDistance | 8 |
| Attack.Summon.Spawn.MaxDistance | 16 |
| Attack.Summon.Spawn.FloorSearch | 8 |
| Attack.Summon.Spawn.HeightTolerance | 5 |
| Position.Mode | "Ground" |
| Position.AgentRadius | 2.5 |
| Position.AgentHeight | 5 |
| Position.RootHeight | 2.5 |
| Position.RepathInterval | 1 |

### Necromancer / Combat

[Source](../src/ReplicatedStorage/Modues/Enemies/Necromancer/Combat.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "Ability" |
| Cooldown | 0 |
| Projectile.Mode | "Normal" |
| Projectile.Detection | "Server" |
| Projectile.Predict | false |
| Projectile.StopAtWorld | true |
| Projectile.CheckMuzzle | true |
| Projectile.Speed | Tuning.Bolt.Speed |
| Projectile.Homing | Tuning.Bolt.Homing |
| Projectile.Lifetime | Tuning.Bolt.Lifetime |
| Projectile.Range | Tuning.Range |

### Noob

[Source](../src/ReplicatedStorage/Modues/Enemies/Noob/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.MinDistance | 24 |
| Spawn.MaxDistance | 40 |
| Spawn.MinHeight | 15 |
| Spawn.MaxHeight | 50 |
| Spawn.FloorSearch | 12 |
| Spawn.PackRadius | 12 |
| Spawn.Patterns.1.FlightType | "Follow" |
| Spawn.Patterns.1.Count | 1 |
| Spawn.Patterns.2.FlightType | "Pack" |
| Spawn.Patterns.2.Count | 3 |
| WeakPoint | "Head" |
| HitVolume.Size | Vector3.new(4, 5, 3) |
| HitVolume.Offset | CFrame.identity |
| Attack.Range | 65 |
| Attack.Windup | 0.85 |
| Attack.MinPellets | 1 |
| Attack.MaxPellets | 4 |
| Attack.SpreadAngle | 10 |
| Attack.PelletSpeed | 32 |
| Attack.PelletLifetime | 2.25 |
| Attack.DamageMultiplier | 0.5 |
| Attack.Recovery | 1.2 |
| Position.Mode | "Fly" |
| Position.AgentRadius | 2 |
| Position.AgentHeight | 5 |
| Position.RootHeight | 3 |

### Noob / SlingshotBurst

[Source](../src/ReplicatedStorage/Modues/Enemies/Noob/SlingshotBurst.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 0 |
| Projectile.Mode | "Normal" |
| Projectile.Detection | "Server" |
| Projectile.Predict | false |
| Projectile.Speed | Tuning.PelletSpeed |
| Projectile.Lifetime | Tuning.PelletLifetime |

### Parallax

[Source](../src/ReplicatedStorage/Modues/Enemies/Parallax/init.luau)

| Parameter | Configured value |
| --- | --- |
| Persistent | true |
| Spawn.MinDistance | 50 |
| Spawn.MaxDistance | 80 |
| Spawn.MinHeight | 25 |
| Spawn.MaxHeight | 50 |
| Spawn.FloorSearch | 48 |
| WeakPoint | "WeakPoint" |
| DeathDuration | 2 |
| HitVolume.Size | Vector3.new(40, 40, 30) |
| HitVolume.Offset | CFrame.identity |
| Position.Mode | "Fly" |
| Position.PreserveFacing | true |
| Position.TurnDuration | 0.6 |
| Position.AgentRadius | Tuning.FlightSize.X/2 |
| Position.AgentHeight | Tuning.FlightSize.Y |
| Position.FlightOffset | Vector3.zero |

### Parallax / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/Parallax/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "BossAttack" |
| Cooldown | 0 |

### Parallax / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/Parallax/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| HoverHeight | 18 |
| ChaseDistance | 58 |
| PatrolSpeed | 5.5 |
| DetectionRadius | 320 |
| DriftRadius | 12 |
| FlightSize | Vector3.new(24, 26, 14) |
| FlightOffset | Vector3.zero |
| SpawnCooldown | 10 |
| EntranceDuration | 2 |
| DeathDuration | 2 |
| IdleDuration | 1.6 |
| CombinedDuration | 0.8 |
| BlendDuration | 0.25 |
| ReturnDuration | 1.9 |
| AttackRange | 180 |
| VolleySpeed | 52 |
| VolleyDamage | 9 |
| VolleyStart | 1.8 |
| VolleyInterval | 0.65 |
| VolleyWaves | 3 |
| VolleySpacing | 2.5 |
| LaserStart | 1.6 |
| LaserInterval | 0.5 |
| LaserDuration | 0.22 |
| LaserLock | 0.25 |
| LaserWarning | 1 |
| LaserDamage | 9 |
| LaserRadius | 0.65 |
| BeamRange | 240 |
| BeamRadius | 2 |
| BeamDamage | 12 |
| BeamTick | 0.25 |
| BeamAimSpeed | 24 |

### QuarrySlime

[Source](../src/ReplicatedStorage/Modues/Enemies/QuarrySlime/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| HopRate | 1.1 |
| DeathDuration | 0.35 |
| SpawnDuration | 0.6 |
| Spawn.MinDistance | 32 |
| Spawn.MaxDistance | 52 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 16 |
| HitVolume.Size | Vector3.new(8.8, 5.5, 7.3) |
| HitVolume.Offset | CFrame.identity |
| Position.AgentRadius | 6.4 |
| Position.AgentHeight | 6.2 |
| Position.RootHeight | 2.8 |
| Position.RepathInterval | 1 |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | true |
| Position.RecoverWhileStopped | false |

### QuarrySlime / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/QuarrySlime/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 3.2 |
| StartRange | Tuning.QuarrySlime.StartRange |

### QuarrySlime / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/QuarrySlime/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| QuarrySlime.Child | "QuarrySlimeMedium" |
| QuarrySlime.RootHeight | 2.8 |
| QuarrySlime.Radius | 6.4 |
| QuarrySlime.Height | 6.2 |
| QuarrySlime.BodySize | Vector3.new(8.8, 5.5, 7.3) |
| QuarrySlime.AttackRadius | 8.8 |
| QuarrySlime.StartRange | 12 |
| QuarrySlime.Health | 260 |
| QuarrySlime.Damage | 24 |
| QuarrySlime.Speed | 5 |
| QuarrySlime.HopRate | 1.1 |
| QuarrySlime.Gold | 12 |
| QuarrySlime.XP | 18 |
| QuarrySlimeMedium.Child | "QuarrySlimeSmall" |
| QuarrySlimeMedium.RootHeight | 1.6 |
| QuarrySlimeMedium.Radius | 4.8 |
| QuarrySlimeMedium.Height | 3.8 |
| QuarrySlimeMedium.BodySize | Vector3.new(4.1, 3.1, 5.2) |
| QuarrySlimeMedium.AttackRadius | 7.2 |
| QuarrySlimeMedium.StartRange | 10 |
| QuarrySlimeMedium.Health | 95 |
| QuarrySlimeMedium.Damage | 14 |
| QuarrySlimeMedium.Speed | 7 |
| QuarrySlimeMedium.HopRate | 1.5 |
| QuarrySlimeMedium.Gold | 6 |
| QuarrySlimeMedium.XP | 8 |
| QuarrySlimeSmall.RootHeight | 0.75 |
| QuarrySlimeSmall.Radius | 2.1 |
| QuarrySlimeSmall.Height | 1.9 |
| QuarrySlimeSmall.BodySize | Vector3.new(2.9, 1.4, 2.3) |
| QuarrySlimeSmall.AttackRadius | 4.5 |
| QuarrySlimeSmall.StartRange | 7.5 |
| QuarrySlimeSmall.Health | 35 |
| QuarrySlimeSmall.Damage | 7 |
| QuarrySlimeSmall.Speed | 9 |
| QuarrySlimeSmall.HopRate | 1.9 |
| QuarrySlimeSmall.Gold | 3 |
| QuarrySlimeSmall.XP | 4 |

### QuarrySlimeMedium

[Source](../src/ReplicatedStorage/Modues/Enemies/QuarrySlimeMedium/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| HopRate | 1.5 |
| DeathDuration | 0.35 |
| SpawnDuration | 0.6 |
| Spawn.MinDistance | 32 |
| Spawn.MaxDistance | 52 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 16 |
| HitVolume.Size | Vector3.new(4.1, 3.1, 5.2) |
| HitVolume.Offset | CFrame.identity |
| Position.AgentRadius | 4.8 |
| Position.AgentHeight | 3.8 |
| Position.RootHeight | 1.6 |
| Position.RepathInterval | 1 |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | true |
| Position.RecoverWhileStopped | false |

### QuarrySlimeSmall

[Source](../src/ReplicatedStorage/Modues/Enemies/QuarrySlimeSmall/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| HopRate | 1.9 |
| DeathDuration | 0.35 |
| SpawnDuration | 0.6 |
| Spawn.MinDistance | 32 |
| Spawn.MaxDistance | 52 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 16 |
| HitVolume.Size | Vector3.new(2.9, 1.4, 2.3) |
| HitVolume.Offset | CFrame.identity |
| Position.AgentRadius | 2.1 |
| Position.AgentHeight | 1.9 |
| Position.RootHeight | 0.75 |
| Position.RepathInterval | 1 |
| Position.ServerPlayback | true |
| Position.AvoidPlayers | true |
| Position.RecoverWhileStopped | false |

### ReedStalker

[Source](../src/ReplicatedStorage/Modues/Enemies/ReedStalker/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 0.5 |
| Spawn.MinDistance | 32 |
| Spawn.MaxDistance | 52 |
| Spawn.MinHeight | 10 |
| Spawn.MaxHeight | 18 |
| Spawn.FloorSearch | 48 |
| HitVolume.Size | Vector3.new(4.5, 5.5, 5.5) |
| HitVolume.Offset | CFrame.new(0, 0.5, -0.75) |
| Position.Mode | "Fly" |
| Position.AgentRadius | 4.5 |
| Position.AgentHeight | 7.6 |
| Position.RootHeight | 3.8 |
| Position.ServerPlayback | true |
| Position.TurnDuration | 0.25 |

### ReedStalker / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/ReedStalker/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 3.8 |
| StartRange | Tuning.Range |
| Projectile.Mode | "Normal" |
| Projectile.Detection | "Server" |
| Projectile.Predict | false |
| Projectile.StopAtWorld | true |
| Projectile.Speed | Tuning.ProjectileSpeed |
| Projectile.Lifetime | Tuning.ProjectileLifetime |

### ReedStalker / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/ReedStalker/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| RootHeight | 3.8 |
| Range | 72 |
| Windup | 1.03333 |
| Duration | 2.2 |
| ProjectileSpeed | 42 |
| ProjectileLifetime | 2.5 |
| Muzzle | Vector3.new(0, 1.35, -3.65) |

### RoyalGuard

[Source](../src/ReplicatedStorage/Modues/Enemies/RoyalGuard/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.Chance | 0.1 |
| Spawn.MinDistance | 30 |
| Spawn.MaxDistance | 46 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "WeakPoint" |
| HitVolume.Size | Vector3.one*5 |
| HitVolume.Offset | CFrame.identity |
| Armor.RawDamageThreshold | 300 |
| Armor.BrokenDefense | 20 |
| Attack.HeightTolerance | 3.5 |
| Attack.DisplacementTolerance | 0.75 |
| Attack.Cooldown | 0.6 |
| Attack.ComboChance | 0.3 |
| Attack.ComboGap | 0.35 |
| Attack.Sweep.StartRange | 10 |
| Attack.Sweep.Reach | 11 |
| Attack.Sweep.Arc | math.rad(150) |
| Attack.Sweep.HalfWidth | math.rad(8) |
| Attack.Sweep.Windup | 1 |
| Attack.Sweep.Active | 0.55 |
| Attack.Sweep.Recovery | 1.15 |
| Attack.Sweep.DamageMultiplier | 1 |
| Attack.Thrust.StartRange | 13 |
| Attack.Thrust.Reach | 14 |
| Attack.Thrust.HalfWidth | 1.6 |
| Attack.Thrust.Windup | 0.95 |
| Attack.Thrust.Active | 0.22 |
| Attack.Thrust.Recovery | 1.4 |
| Attack.Thrust.DamageMultiplier | 1.25 |
| Guard.SearchRadius | 32 |
| Guard.SearchInterval | 1 |
| Guard.HeightTolerance | 5 |
| Guard.Distance | 7 |
| Guard.EngageRadius | 18 |
| Guard.HoldTolerance | 2 |
| Position.Mode | "Ground" |
| Position.AgentRadius | 2.5 |
| Position.AgentHeight | 5 |
| Position.RootHeight | 2.5 |
| Position.RepathInterval | 1 |

### RoyalGuard / Combat

[Source](../src/ReplicatedStorage/Modues/Enemies/RoyalGuard/Combat.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "Ability" |
| Cooldown | 0 |

### Rustback

[Source](../src/ReplicatedStorage/Modues/Enemies/Rustback.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| SpawnDuration | 1.1 |
| Spawn.Chance | 0.08 |
| Spawn.MinDistance | 28 |
| Spawn.MaxDistance | 44 |
| Spawn.FloorSearch | 12 |
| HitVolume.Size | Vector3.new(9.5, 5.8, 7.5) |
| HitVolume.Offset | CFrame.new(0, 0.65, 0) |
| Movement.Walk | 1.11176 |
| Attacks.1.Name | "Ram" |
| Attacks.1.Kind | "Melee" |
| Attacks.1.Range | 8.5 |
| Attacks.1.HalfWidth | 4.5 |
| Attacks.1.Height | 7 |
| Attacks.1.Duration | 2.66667 |
| Attacks.1.Contacts.1 | 0.875 |
| Attacks.1.Cooldown | 3.5 |
| Attacks.1.Multiplier | 1 |
| Position.Mode | "Ground" |
| Position.AgentRadius | 4.8 |
| Position.AgentHeight | 5.8 |
| Position.RootHeight | 2.25 |
| Position.RepathInterval | 1.2 |

### Shardling

[Source](../src/ReplicatedStorage/Modues/Enemies/Shardling/init.luau)

| Parameter | Configured value |
| --- | --- |
| WeakPoint | "WeakPoint" |
| DeathDuration | Motion.Shardling.Clips.Death.Duration |
| HitVolume.Size | Vector3.new(2.8, 3.7, 2.2) |
| HitVolume.Offset | CFrame.identity |
| Position.AgentRadius | 0.9 |
| Position.AgentHeight | 3.7 |
| Position.RootHeight | 1.84 |
| Position.RepathInterval | 1 |

### Shardling / Attack

[Source](../src/ReplicatedStorage/Modues/Enemies/Shardling/Attack.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 0.3 |
| StartRange | 4.5 |
| Range | 5 |
| HalfWidth | 2 |
| Height | 4 |

### Shieldbearer

[Source](../src/ReplicatedStorage/Modues/Enemies/Shieldbearer/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.Chance | 0.18 |
| Spawn.MinDistance | 28 |
| Spawn.MaxDistance | 44 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "WeakPoint" |
| HitVolume.Size | Vector3.one*5 |
| HitVolume.Offset | CFrame.identity |
| Attack.StartRange | 7 |
| Attack.Range | 7.5 |
| Attack.HalfWidth | 3 |
| Attack.Height | 5 |
| Attack.StartArc | math.rad(80) |
| Attack.Windup | 0.7 |
| Attack.Active | 0.12 |
| Attack.Recovery | 0.85 |
| Attack.Cooldown | 2.8 |
| Attack.BrokenDamageMultiplier | 0.5 |
| Attack.DisplacementTolerance | 0.5 |
| Position.Mode | "Ground" |
| Position.AgentRadius | 2.5 |
| Position.AgentHeight | 5 |
| Position.RootHeight | 2.5 |
| Position.RepathInterval | 1 |
| Position.PreserveFacing | true |

### Shieldbearer / Combat

[Source](../src/ReplicatedStorage/Modues/Enemies/Shieldbearer/Combat.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "Ability" |
| Cooldown | Tuning.Cooldown |

### Shieldbearer / Tuning

[Source](../src/ReplicatedStorage/Modues/Enemies/Shieldbearer/Tuning.luau)

| Parameter | Configured value |
| --- | --- |
| Stats.MaxHealth | 360 |
| Stats.AttackDamage | 18 |
| Stats.Defense | 25 |
| Stats.AttackSpeed | 1 |
| Stats.MoveSpeed | 8 |
| Shield.Durability | 240 |
| Shield.Arc | math.rad(110) |
| Shield.HalfWidth | 3 |
| Shield.HalfHeight | 2.5 |
| Shield.ForwardOffset | 2.6 |
| Shield.TurnSpeed | math.rad(65) |
| Shield.MaximumTurnStep | 0.2 |
| Attack.StartRange | 7 |
| Attack.Range | 7.5 |
| Attack.HalfWidth | 3 |
| Attack.Height | 5 |
| Attack.StartArc | math.rad(80) |
| Attack.Windup | 0.7 |
| Attack.Active | 0.12 |
| Attack.Recovery | 0.85 |
| Attack.Cooldown | 2.8 |
| Attack.BrokenDamageMultiplier | 0.5 |
| Attack.DisplacementTolerance | 0.5 |

### Skeleton

[Source](../src/ReplicatedStorage/Modues/Enemies/Skeleton/init.luau)

| Parameter | Configured value |
| --- | --- |
| SpawnDuration | 1.5 |
| Spawn.MinDistance | 24 |
| Spawn.MaxDistance | 40 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "Head" |
| HitVolume.Size | Vector3.new(3.5, 5.3, 1.5) |
| HitVolume.Offset | CFrame.new(0, 0.59, 0) |
| Position.AgentRadius | 1.75 |
| Position.AgentHeight | 5.3 |
| Position.RootHeight | 2.04 |
| Position.RepathInterval | 1 |

### Skeleton / SkeletonStrike

[Source](../src/ReplicatedStorage/Modues/Enemies/Skeleton/SkeletonStrike.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "MainAttack" |
| Cooldown | 0 |
| StartRange | 6 |
| Range | 7 |
| HalfWidth | 3 |
| Height | 6 |
| Windup | 0.4 |
| SwingStartup | 0.1 |
| Strike | 0.12 |
| Recovery | 0.65 |
| DamageMultiplier | 1 |
| CueHeight | 1.99 |

### WreckingBallGuest

[Source](../src/ReplicatedStorage/Modues/Enemies/WreckingBallGuest/init.luau)

| Parameter | Configured value |
| --- | --- |
| Spawn.Chance | 0.12 |
| Spawn.MinDistance | 30 |
| Spawn.MaxDistance | 46 |
| Spawn.Height | 0 |
| Spawn.FloorSearch | 12 |
| WeakPoint | "WeakPoint" |
| HitVolume.Size | Vector3.one*6 |
| HitVolume.Offset | CFrame.identity |
| Attack.HeightTolerance | 4 |
| Attack.MaximumSampleGap | 0.2 |
| Attack.Swing.StartRange | 10 |
| Attack.Swing.Radius | AttackMotion.SwingReach |
| Attack.Swing.ContactPadding | 1 |
| Attack.Swing.Windup | 0.45 |
| Attack.Swing.Active | 0.38 |
| Attack.Swing.Recovery | 1.47 |
| Attack.Swing.Cooldown | 3.3 |
| Attack.Swing.DamageMultiplier | 1 |
| Attack.Slam.Radius | 6 |
| Attack.Slam.Height | 5 |
| Attack.Slam.Windup | 0.85 |
| Attack.Slam.Active | 0.12 |
| Attack.Slam.Recovery | 1.15 |
| Attack.Slam.Cooldown | 6 |
| Attack.Slam.DamageMultiplier | 1.5 |
| Attack.Rampage.MinRange | 12 |
| Attack.Rampage.StartRange | 36 |
| Attack.Rampage.Radius | AttackMotion.RampageReach |
| Attack.Rampage.Windup | 0.65 |
| Attack.Rampage.Active | 3.2 |
| Attack.Rampage.Slowdown | 0.4 |
| Attack.Rampage.Recovery | 1.6 |
| Attack.Rampage.Cooldown | 24 |
| Attack.Rampage.InitialCooldown | 8 |
| Attack.Rampage.DamageMultiplier | 0.25 |
| Attack.Rampage.DamageInterval | 0.5 |
| Attack.Rampage.SpeedScale | 2.2 |
| Attack.Rampage.TurnSpeed | math.rad(80) |
| Attack.Rampage.LookAhead | 4 |
| Attack.Rampage.FloorClearance | 0.2 |
| Position.Mode | "Ground" |
| Position.AgentRadius | 3 |
| Position.AgentHeight | 6 |
| Position.RootHeight | 3 |
| Position.RepathInterval | 1 |

### WreckingBallGuest / Combat

[Source](../src/ReplicatedStorage/Modues/Enemies/WreckingBallGuest/Combat.luau)

| Parameter | Configured value |
| --- | --- |
| Type | "Ability" |
| Cooldown | 0 |
