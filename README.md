# Sector Ruler - Balanced Supply Curve Variant

This is a personal balance edit of **Sector Ruler** for *X4: Foundations*.

Original mod: Sector Ruler by Anghelos92, with credits on the Nexus page to Anghelos92, DeadAir, Logicalallamprey, bassted89, and other credited contributors. The original Nexus description says the mod addresses sector ownership and welfare-module mechanics by making sector ownership generate income, increase allowed ships/modules, and add late-game pressure through supply limits, military threat war, and a galaxy-wide crisis. See the original mod page for permissions, requirements, and credits: https://www.nexusmods.com/x4foundations/mods/1327

## What this variant changes

This edit keeps the core Sector Ruler concept: owning sectors gives income and supply capacity, while exceeding supply limits can destroy assets and excessive military strength can trigger war.

The balance focus is to make expansion feel more staged:

- Early game starts slightly tighter for economy fleets.
- Mid-game sector ownership gives stronger gains.
- Late-game gains slow down, so the player still needs to manage overexpansion.
- At more than 9 sectors, the original sector-crisis cap still triggers the Galactic Crisis / point-of-no-return logic. Normal war-threshold balancing is superseded by crisis behaviour, but supply values continue to increase so very large empires still have defined logistics limits.
- Fight Rank and Trade Rank provide small prestige bonuses to supply limits. Fight Rank also provides a command-prestige bonus to the military war threshold.

## Organisation stages used for balancing

These names are for design/readability only. They are not shown in-game as titles.

| Owned sectors | Stage |
|---:|---|
| 0 | Free Trader Outfit |
| 1 | Sector Claimant |
| 2 | Security Charter |
| 3 | Trade Compact |
| 4 | Free League |
| 5 | Protectorate Authority |
| 6 | Sector Republic |
| 7 | Gate Network Bloc |
| 8 | Major Power Coalition |
| 9 | Great Power Hegemony |
| 10+ | Galactic Crisis |

## Supply weights

The original Sector Ruler supply weights are preserved:

| Object | Supply used |
|---|---:|
| XL military ship | 21 |
| L military/miner/trader ship | 9 |
| M military/miner/trader ship | 3 |
| S military/miner/trader ship | 1 |
| Scavenger ship | 1 |
| Utility ship, builder, auxiliary, Teuta/dismantler | 1 |
| Shipbuilding/equipment module | 1 |
| Defence module/admin centre | 1 |

## Military supply

Fight Rank is added as a prestige bonus. X4 exposes named Fight/Trade ranks as 31 displayed tiers; internally these are expected to be 0-30, so max rank adds +60 military supply.

| Sectors | Base military supply |
|---:|---:|
| 0 | 180 |
| 1 | 230 |
| 2 | 290 |
| 3 | 365 |
| 4 | 455 |
| 5 | 555 |
| 6 | 640 |
| 7 | 715 |
| 8 | 780 |
| 9 | 840 |
| 10+ | 840 + 50 per sector above 9 |

Final formula:

```text
Military supply = military sector curve + (fight_rank * 2)
```

## Military threat war threshold

The war threshold is now a staged alarm curve. It is intentionally lower than the military supply cap, because the great powers can tolerate a state navy but still become alarmed by an oversized military. Fight Rank adds a command-prestige bonus to the threshold: `fight_rank`, up to +30 at max internal rank.

At 10+ owned sectors, the normal military alarm threshold is no longer the main limiter. The original Sector Ruler sector-crisis cap still applies: exceeding the crisis sector threshold triggers the Galactic Crisis / point-of-no-return logic regardless of the normal war-threshold value.

| Sectors | Base war threshold before Fight Rank bonus |
|---:|---:|
| 0 | 140 |
| 1 | 175 |
| 2 | 210 |
| 3 | 252 |
| 4 | 294 |
| 5 | 343 |
| 6 | 378 |
| 7 | 406 |
| 8 | 427 |
| 9 | 440 |
| 10+ | Galactic Crisis logic takes over |

Final formula before crisis:

```text
War threshold = base war threshold + fight_rank
```

Crisis rule:

```text
If owned sectors exceed the crisis sector cap, Galactic Crisis / point-of-no-return logic triggers regardless of the normal war threshold.
```

## Mining supply

Trade Rank is added as a small prestige bonus. Max internal Trade Rank 30 adds +30 mining supply.

| Sectors | Base mining supply |
|---:|---:|
| 0 | 120 |
| 1 | 154 |
| 2 | 196 |
| 3 | 250 |
| 4 | 316 |
| 5 | 390 |
| 6 | 454 |
| 7 | 510 |
| 8 | 558 |
| 9 | 600 |
| 10+ | 600 + 32 per sector above 9 |

Final formula:

```text
Mining supply = mining sector curve + trade_rank
```

## Trading supply

Trade Rank is added as a small prestige bonus. Max internal Trade Rank 30 adds +30 trading supply.

| Sectors | Base trading supply |
|---:|---:|
| 0 | 72 |
| 1 | 94 |
| 2 | 122 |
| 3 | 158 |
| 4 | 204 |
| 5 | 254 |
| 6 | 298 |
| 7 | 336 |
| 8 | 370 |
| 9 | 400 |
| 10+ | 400 + 22 per sector above 9 |

Final formula:

```text
Trading supply = trading sector curve + trade_rank
```

## Other prestige bonuses

| Category | Bonus formula |
|---|---|
| Defence modules | +1 supply per 3 Fight Ranks, max +10 at internal rank 30 |
| Utility ships | +1 supply per 10 combined Trade+Fight ranks, max +6 |
| Scavengers | +1 supply per 5 Trade Ranks, max +6 |
| Shipbuilding modules | unchanged |

## Notes

- The original options menu still contains some legacy per-sector supply settings. The curved categories in this variant use fixed curves rather than those linear per-sector settings.
- A new game should not be required, matching the original mod's installation guidance.
- Back up your save before using any modified gameplay script.
- This is a balance edit, not an official update of Sector Ruler.
