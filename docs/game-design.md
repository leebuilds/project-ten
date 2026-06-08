# Project Ten — Game Design Document

Full design specification for Project Ten. See the [project README](../README.md) for a short overview.

A 2D sci-fi action game built in Godot.

## Game Plan

The player ventures out from base across hostile terrain, **collecting materials and upgrades** needed to strengthen their mech. Combat is intermittent — nest encounters and larger fights punctuate exploration, not the other way around. Each area ends in a **three-phase king battle** that tests everything gathered.

### Core Loop

1. **Briefing** — Opening cutscene on first spawn: scavenge materials, certify your mech, join the fleet bound for the alien homeworld.
2. **Venture out** — Leave Command Base (or area base) and cross open terrain toward the next objective.
3. **Collect** — Gather scrap, alloy, health packs, and **salvage powerups** from wreckage and caches along the route; materials are the primary reward.
4. **Fight occasionally** — Disturb alien nests for small basic encounters; face larger waves before or after save points.
5. **Prep at save points** — Swap loadout, upgrade on-foot gear, checkpoint progress (5+ save points per area).
6. **Boss sequence** — After clearing an area, leave the area base to trigger a three-phase king fight: on-foot wave → mech wave → mech upgrade break → king + forces.
7. **Return & advance** — Extract to Command Base, invest in mech ports, unlock the next (harder) area — or trigger the **ending cutscene** after the Act 3 king falls.

### Setting & Tone

- **Top-down 2D** sci-fi action across a single hostile planet, **Keth-9** — a scorched, open wasteland of collapsed domes, gutted research campuses, and rusted outdoor infrastructure overrun by alien biology. No intact cities; everything is ruins under sky.
- Exploration and material collection drive progression; combat is a hazard of the route, not the main activity.
- Minor aliens nest in the environment; king aliens anchor three-phase boss sequences at the end of each area.
- Mechs deploy during boss phases 2 and 3 — the payoff for materials gathered across the area.

---

## World Landscape

The game is played from a **fixed top-down camera** at a slight angle (~15° tilt for depth). The player sees their character, enemies, projectiles, and terrain hazards on a readable 2D plane — similar to a tactical action game. Walls and cliffs render as raised edges with drop shadows; tall structures and boss aliens extend above the tile layer so they remain visible over smaller units.

### The Planet

Keth-9 is a rocky exoplanet with thin atmosphere, harsh wind, and exposed terrain. Human settlement never took hold — only outdoor research sites, transit pylons, and prefab lab modules scattered across the surface, now shattered and overgrown. Three **areas** ring a central **Command Base** bunker. Each area is a long overland route from **entry point → 5+ save points → area base → boss arena**. Difficulty and material quality scale with each new area.

```
                    [ Orbital Wreckage ]
                           |
              +------------+------------+
              |                         |
    [ Ruined Colonies ] --- [ Command Base ] --- [ Bio-Mechanical Hives ]
              |                         |
              +-------- canyon --------+
```

---

### Command Base
*Hub — safe zone between missions*

A buried military bunker at the center of the map, half-swallowed by rock and alien roots. Top-down view shows:

- **Interior layout** — Rectangular rooms connected by corridors: **crafting bay**, **mech hangar** (port upgrade terminals), **armory** (loadout swaps), and **mission board**.
- **Visual tone** — Cold blue UI lighting, exposed rebar, flickering holo-screens. Clean grid floors contrast with the organic chaos outside.
- **NPC presence** — Static terminals only; no civilians. Reinforces isolation.
- **Map position** — Always accessible from the world map; fast-travel anchor.

---

### Bio-Mechanical Hives
*Act 1 — outdoor lab corruption zone*

The southeastern quadrant. A destroyed **xenobiology field campus** in open country — cracked foundations, collapsed greenhouse domes, and prefab lab shelters half-buried in pulsing alien tissue. From above, the zone reads as **purple-green organic spread** crawling across broken concrete pads and rusted fencing in open air.

**Terrain features**
- **Spore channels** — Glowing vein-like growth along cracked pavement and dirt paths; acid puddles pool here after Spore Slinger attacks.
- **Membrane floors** — Alien tissue overgrowing lab floor tiles; slow movement 15%.
- **Collapsed dome walls** — Curved wreckage forming partial rings; block line of sight, create flank routes around the outside.
- **Specimen tanks** — Outdoor containment cylinders ruptured and leaking; burst into acid if disturbed.
- **Field sensor poles** — Bent metal poles and dead holo-displays; ambient wreckage, some drop scrap on salvage.

**Landmarks**
- Area entry beacon (save point 1)
- Ruined greenhouse dome (save point 2)
- Open-air sample pit (save point 3 — larger ambush after)
- Spore channel bridge (save point 4)
- Collapsed lab wing (save point 5 — larger ambush before)
- Prefab shelter cluster (save point 6)
- **Hive area base** — Forward camp inside a sealed lab block; end of exploration
- **Matriarch arena** — Collapsed central biodome; boss sequence only

**Top-down readability**
- Acid puddles use bright green fill + animated edge ripple.
- Spore projectiles arc visibly before landing (shadow telegraphs impact point).
- Rupture Hound rush paths show a brief ground scratch trail during wind-up.

---

### Ruined Colonies
*Act 2 — scorched outdoor research zone*

The western quadrant. Not a city — a string of **destroyed outdoor research stations** across barren scrubland: collapsed comms arrays, burnt solar farms, and gutted prefab lab blocks connected by cracked service roads. Reads as **dust, grey rubble, and rusted steel** under a pale sky with flickering amber hazard beacons.

**Terrain features**
- **Rubble berms** — Earth and concrete mounds from demolished foundations; narrow gaps force Phalanx encounters, wide routes allow flanking around the outside.
- **Salvage wreckage** — Overturned rovers, supply crates, and antenna frames block shots; destroy for scrap.
- **Exposed pipeline trenches** — Open channels between station pads; long sightlines favor Needle Drones, trench walls reward melee approach from below grade.
- **Collapsed solar arrays** — Tilted panel racks act as half-cover walls; paths weave between rows.
- **Dust storm patches** — Occasional visibility reduction in open ground between stations.

**Landmarks**
- Area entry beacon (save point 1)
- Burnt-out relay station (save point 2 — larger ambush after; Phalanx tutorial)
- Pipeline trench crossing (save point 3)
- Crashed survey rover depot (save point 4)
- Solar farm wreckage (save point 5 — larger ambush before)
- Comms array foundation (save point 6)
- **Colony area base** — Reinforced survey camp at the drill site perimeter; end of exploration
- **Regent arena** — Circular excavation pit; boss sequence only

**Top-down readability**
- Carapace Guards face direction with a visible shell arc indicator (120° frontal shield).
- Phalanx formations show a linked shield glow between units.
- Spine Volley spikes telegraph landing zones as red diamond markers.

---

### Orbital Wreckage
*Act 3 — crash-site wasteland*

The northern quadrant. A cargo ship broke apart on re-entry over open desert; hull fragments, fuel cells, and cargo pods litter a vast **outdoor crater field** beside a dried riverbed. Reads as **charred metal, electric blue discharge, and open sky** — no enclosed hangars, all combat in the open among debris.

**Terrain features**
- **Debris fields** — Random obstacle clusters across open ground; paths shift between missions (light procedural layout).
- **Live wire zones** — Exposed conduit and capacitor leaks on the ground; Insulated Plating negates.
- **Crater rim gaps** — Drop into the impact basin or off cliff edges is instant death (respawn at last save point).
- **Cargo pods** — Scattered cover in open terrain; some hide material caches or Signal Cysts.
- **Fuel fire patches** — Burning leaks from ruptured cells; chip damage in a visible flame radius.

**Landmarks**
- Area entry beacon (save point 1)
- Split hull section spanning a ravine (save point 2 — larger ambush after; first Arc Lancer)
- Fuel cell spill zone (save point 3)
- Fallen loading crane (save point 4)
- Cargo pod field (save point 5 — larger ambush before)
- Crater rim overlook (save point 6)
- **Wreckage area base** — Emergency shelter built inside a hollowed cargo pod; end of exploration
- **Overmind arena** — Open crater floor; boss sequence only

**Top-down readability**
- Arc trails linger as blue-white lines on the ground for 1s.
- Signal Cyst sonar pings show expanding ring before spawn.
- Ring Laser sweep displays as a rotating wedge sector — player dodges into safe gaps.

---

### Save Points & En Route

| Location type | Visual | Function |
|---|---|---|
| **Save point** | Deployed supply crate with green holo-beacon | Swap weapon, armor, character; upgrade items; checkpoint |
| **En route** | Quick-access weapon rack on the HUD; pause menu | **Swap weapon type only** — no checkpoint |
| **Command Base** | Bunker interior terminals | Crafting, mech ports, full loadout |
| **Boss intermission** | Emergency drop-pod beacon in arena | Full prep + mech port upgrade; between Wave 2 and 3 |

Each area places **at least 5 save points** between the entry point and the area base, spaced across the overland route. Top-down, they read as a **single glowing tile** the player walks onto to open the full prep menu. En route, the player can hot-swap **weapon type** mid-mission. Save points also **restore full health**.

A special **Boss Intermission Save** appears between boss phases 2 and 3 — full prep plus **mech port upgrades** using materials collected during the area.

---

### Cover Positions

Combat zones place **hard cover** objects the player can hide behind to recharge health mid-battle. Top-down, cover tiles show a **blue shield icon** when the player is positioned correctly (behind the object, break in enemy line of sight).

| Cover type | Biome | Blocks fire | Notes |
|---|---|---|---|
| Collapsed dome wall | Hives | ✓ | Curved wreckage; room for 1 player |
| Prefab lab shelter | Hives | ✓ | Rectangular block; common near encounters |
| Salvage wreckage | Colonies | ✓ | Rovers, crates, antenna frames |
| Pipeline trench wall | Colonies | ✓ | Below-grade cover; strong vs Needle Drones |
| Solar array rack | Colonies | Half | Blocks ranged; chargers can path around |
| Cargo pod | Wreckage | ✓ | Standard outdoor cover |
| Hull fragment | Wreckage | ✓ | Large debris; fits 1–2 player widths |

**Cover rules**
- Player must stand adjacent to the cover's protected side and **not fire** to begin recharging.
- Taking damage or leaving cover pauses regen; re-enter to resume.
- Enemies path around cover and use flanking abilities (Rupture Rush, Arc Thrust) to pull the player out.
- Destroying salvage cover for scrap removes that regen spot — trade healing position for materials.

---

### Environmental Hazards (Landscape)

Shared across biomes; rendered as distinct top-down tile overlays:

| Hazard | Biome | Visual | Effect |
|---|---|---|---|
| Acid puddle | Hives | Green pool, bubbling | Chip damage; slow 20% |
| Collapsing foundation | Colonies | Cracked concrete pads, shake anim | Falls through after 1.5s on tile |
| Spore cloud | Hives | Purple fog patch | Blocks vision radius slightly |
| Electric floor | Wreckage | Blue crackle tile | Slow + damage unless insulated |
| Void gap | Wreckage | Crater edge / ravine drop | Instant fall death |
| Dust storm | Colonies | Brown haze patch in open ground | Slightly reduced vision radius |

Hazards affect **both player and enemies** where noted in combat design — acid and electric tiles also damage aliens.

---

### Area Progression

Each of the three areas follows the same structure. Difficulty, enemy density, and material drops increase per area.

```
New game → Opening cutscene → Command Base (player control)
     ↓ launch into area
Area Entry (Save 1) ──materials── nest encounters ── larger fight ──
     ↓
Save 2 → Save 3 → Save 4 → Save 5 → (Save 6+ optional)
     ↓                          ↑
     └── explore, collect ──────┘   larger fights before/after some saves
     ↓
Area Base (exploration complete)
     ↓ leave area base → boss triggered
┌─ Boss Phase 1 — on-foot basic wave (quick)
├─ Boss Phase 2 — mech wave + overpowered basics (larger)
├─ Boss Intermission Save — upgrade mech ports + loadout
├─ Boss Phase 3 — mech: king + overpowered + basics → Kingbreaker finisher
     ↓
Extract → Command Base → king core reward → next area unlocked
     ↓ (after Act 3 king only)
Ending cutscene → game complete screen
```

#### Exploration Phase
*Entry point → area base*

| Beat | What happens |
|---|---|
| **Terrain travel** | Open overland movement between landmarks; materials, salvage objects, and powerup drops along the path |
| **Nest encounter** | Walking near a visible alien nest triggers a small basic-alien group (2–5 grunts); quick fight, scrap drop |
| **Larger encounter** | Scripted mini-horde placed directly **before or after** a save point (6–10 basics, sometimes 1 elite); alloy chance |
| **Save points** | Minimum **5** between entry and area base; checkpoint, full loadout prep, full heal |
| **Area base** | Forward camp at route end; reaching it marks exploration **complete**; safe rest, no boss yet |

#### Boss Sequence
*Leaving area base → king arena*

Triggered the **next time** the player exits the area base toward the boss zone after exploration is complete.

| Phase | Mode | Opposition | Purpose |
|---|---|---|---|
| **1 — Skirmish** | On foot | Quick wave of basic aliens (8–12) | Warm-up; spend on-foot skills |
| **2 — Assault** | Mech | Larger wave (15–20) + **overpowered** basics mixed in | First mech test; drop pod deploy after Phase 1 clear |
| **Intermission** | Save point | Mech port upgrade + loadout swap | Spend area materials on mech before finale |
| **3 — King** | Mech | **King alien** + overpowered basics + basic grunts → **Kingbreaker finisher** | Clear adds; last drop enables one-shot king kill |

#### Difficulty Scaling

| Area | Exploration | Overpowered ratio | King phase pressure |
|---|---|---|---|
| **Bio-Mechanical Hives** (Act 1) | Fewer nests, generous material nodes | 1 overpowered per 8 basics | King + 2 overpowered + 6 basics |
| **Ruined Colonies** (Act 2) | More nests, rarer alloy nodes | 1 per 5 basics | King + 4 overpowered + 10 basics |
| **Orbital Wreckage** (Act 3) | Dense nests, high-risk high-reward nodes | 1 per 3 basics | King + 6 overpowered + 14 basics |

#### Area Bases

Each area ends at a forward **area base** — a prefab shelter with supply cache, distinct from Command Base.

| Area | Area base location |
|---|---|
| Hives | Sealed lab bunker at the far edge of the corrupted campus |
| Colonies | Buried relay bunker at the last research station |
| Wreckage | Intact cargo-pod shelter at the crater rim |

---

## Opening Cutscene

Plays **once** on first spawn when starting a new game. The player lands on Keth-9 before gaining control at Command Base.

### Trigger

| Condition | Behavior |
|---|---|
| **New game, first launch** | Cutscene plays automatically after spawn |
| **Resume save** | Skipped — player loads directly to their save point |
| **Restart game** | Cutscene plays again on first spawn |

### Cutscene Beats

| Beat | Visual | Narration / text |
|---|---|---|
| 1 | Drop pod descends through atmosphere; Keth-9 surface visible below — ruined labs, alien growth, dust storms | *"Welcome to Keth-9, soldier. Fleet Command has assigned you to the forward operating theater."* |
| 2 | Pod lands in a clearing; holo-display flickers to life with fleet insignia | *"You have been selected for the battle fleet. But before you ship out, your mech must be certified combat-ready."* |
| 3 | Camera pans across the wasteland — wreckage, nests, distant alien silhouettes | *"Scavenge materials from the planet surface. Upgrade your mech at Command Base. Fight through three hostile zones and prove your unit in king-class engagements."* |
| 4 | Holo-map shows fleet in orbit and a distant alien homeworld | *"Once your mech passes certification, you will be airlifted to the fleet — and deployed to the alien homeworld."* |
| 5 | Screen holds on the player's faceplate reflection; comms crackle | **"Good luck, soldier."** |
| 6 | Fade to black → cut to **Command Base** interior | Player gains control at the mission board |

Cutscene is skippable after 3s (tap / confirm). Total runtime ~35s.

### Handoff to Gameplay

After the cutscene, the player spawns inside **Command Base** with:
- Default on-foot loadout (Vanguard, Pulse Carbine, Light Recon Suit)
- Empty mech port investment — mech hangar terminal highlighted with a tutorial prompt
- Mission board showing **Bio-Mechanical Hives** as the first available area

No combat during the intro. The first fight occurs when the player leaves Command Base and enters the Hives entry beacon.

### Story Bookends

| Moment | Message |
|---|---|
| **Opening** | Scavenge → upgrade → certify mech → join fleet → homeworld |
| **Ending** | Mech certified → added to fleet → homeworld deployment confirmed |

The opening establishes the goal; the ending delivers on it.

---

## Ending & Game Complete

After the **Signal Overmind** is destroyed in Orbital Wreckage (Act 3), the campaign ends with a short cutscene and a completion screen. Acts 1 and 2 kings still award king cores and unlock the next area as normal — only Act 3 triggers the finale.

### Ending Cutscene

Plays immediately after the Kingbreaker hit (or final kill if the finisher was missed) on the Signal Overmind.

| Beat | Visual | Narration / text |
|---|---|---|
| 1 | King shatters; arena debris clears | — |
| 2 | Camera pulls back from the mech; drop ships arrive overhead | *"Target neutralized. Keth-9 perimeter secure."* |
| 3 | Mech lifts into a carrier bay; hangar doors close | *"Mech unit certified combat-ready."* |
| 4 | Fleet of warships breaks orbit; star map highlights a distant alien homeworld | *"Your mech has been added to the battle fleet en route to the alien homeworld."* |
| 5 | Fade to black | *"Mission complete."* |

Cutscene is skippable after 3s (tap / confirm). Total runtime ~30s.

### Game Complete Screen

A full-screen notification overlays after the cutscene (or on skip).

```
┌─────────────────────────────────────────┐
│           MISSION COMPLETE              │
│                                         │
│   Keth-9 cleared. Your mech joins the   │
│   fleet bound for the alien homeworld.  │
│                                         │
│   [ Restart Game ]   [ Resume Save ]    │
└─────────────────────────────────────────┘
```

| Option | Behavior |
|---|---|
| **Restart Game** | Returns to title / new game; clears campaign progress; mech port investment resets |
| **Resume Save** | Loads the **most recent save point** (boss intermission, area save, or Command Base — whichever was last) |

**Resume does not** place the player after the ending — the story is complete. Resume is for continuing to explore, farm materials, or re-fight bosses before the Act 3 finale. If the player resumes after beating Act 3, they load their last save from **before** the Signal Overmind fight.

A **campaign complete** flag is set in save data so the game complete screen can be re-viewed from the title menu.

---

## Confirmed Design Decisions

### 1. Enemy Archetypes

Minor aliens have distinct roles — ranged, charger, shield-bearer, summoner — so fights reward positioning and target priority rather than pure DPS. See [Minor Alien Types](#minor-alien-types) for full specs.

### 2. Stackable Materials & Crafting

Materials are stackable and tiered. Drops scale with enemy difficulty — common scrap from grunts, rare alloys from elites, king-tier cores from bosses — but players can grind lower tiers and combine them at the **base** instead of being hard-gated (e.g. 5× scrap → 1× alloy, 3× alloy → 1× king core). **Crafting is base-only**; it is not available at save points or en route.

### 3. Exploration-First Area Progression

Gameplay prioritizes **collecting mech upgrade materials** across overland terrain. Basic alien fights are nest-triggered or placed around save points — not constant combat. Each area has **5+ save points** between entry and area base, then a **three-phase boss sequence** (on-foot wave → mech wave → intermission mech upgrade → mech king fight). See [Area Progression](#area-progression).

### 4. Three-Phase Boss Structure

| Phase | Foot / Mech | Content |
|---|---|---|
| 1 | On foot | Quick basic-alien wave |
| 2 | Mech | Larger wave with overpowered basics |
| Intermission | Save + upgrade | Mech port investment using area materials |
| 3 | Mech | King alien + overpowered + basic forces → **Kingbreaker finisher** |

Wave 3 ends with a **Kingbreaker Payload** — dropped by the last add, aimed in mech, one-shots the king. See [Kingbreaker Payload](#kingbreaker-payload).

Mech play style is defined by **upgrade port** investment — see [Mech System](#mech-system).

### 5. Opening & Ending Cutscenes

**Opening** (first spawn only) — Fleet briefing on Keth-9: scavenge materials, upgrade and certify your mech, then ship out to the alien homeworld. Ends with *"Good luck, soldier."* → cut to Command Base. See [Opening Cutscene](#opening-cutscene).

**Ending** (Act 3 king defeated) — Mech certified, added to the battle fleet, homeworld deployment confirmed. **Game complete** screen offers **Restart Game** or **Resume Save**. See [Ending & Game Complete](#ending--game-complete).

### 6. Powerup Trade-Offs

Salvageable objects drop **powerups** alongside materials. Every powerup carries a trade-off — buffs are never free. See [Salvage Powerups](#salvage-powerups).

### 7. Health, Ammo & Cover

**Ammo is unlimited** — no ammo pickups or reload limits. Weapon choice and positioning matter, not resource conservation.

**Health recharges in cover only.** Duck behind hard cover mid-battle to passively regain HP. Out of cover, there is no passive regen.

| Regen mode | Rate | Condition |
|---|---|---|
| **Standard** | 6 HP/s | Behind hard cover, not firing |
| **Rapid Recovery** | 18 HP/s | Standard regen + active Health Pack buff |

**Health packs** — retrievable consumables found in the world (supply crates, enemy drops, salvage nodes). Pick up to inventory (max **3** carried). Activate manually while in cover to gain **Rapid Recovery for 12s**. Does not heal instantly; amplifies cover regen only. Buff timer runs whether or not you stay in cover — use before a sustained heal window.

Health packs are separate from powerups (combat trade-offs) and materials (crafting). Save points restore full health.

### 8. Base, Save Points & En Route

| Action | En route | Save point | Boss intermission | Command Base |
|---|---|---|---|---|
| Swap weapon | ✓ | ✓ | ✓ | ✓ |
| Swap armor | — | ✓ | ✓ | ✓ |
| Swap character | — | ✓ | ✓ | ✓ |
| Upgrade items | — | ✓ | ✓ | ✓ |
| Craft materials | — | — | — | ✓ |
| Mech port upgrades | — | — | ✓ | ✓ |

**En route** — swap **weapon type** only via pause menu. Quick adaptation mid-mission (e.g. pull Scatter Launcher before a drone stack) without a checkpoint.

**Save points** — full prep: swap **weapon**, **armor**, or **character**, and **upgrade items**. Safe beats spaced across the area route (5+ per area).

**Boss intermission** — between boss Wave 2 and Wave 3: checkpoint, full heal, and **mech upgrade** using materials collected during the area run. Last chance to invest before the king wave.

**Command Base** offers everything a save point does, plus **crafting** (combining materials into higher tiers). **Mech port upgrades** are available at Command Base anytime and at the **boss intermission** using materials collected during the area run. Return to Command Base between areas for long-term investment; spend remaining run materials at the intermission before Wave 3.

---

## Combat Resources

On-foot combat only. Mech phase uses the [Energy system](#energy--overheat) instead of health packs.

### Ammo

All weapons have **unlimited ammunition**. Fire rate, wind-ups, and overheat-style ability cooldowns are the only pacing limits — never ammo scarcity.

### Health & Cover Flow

```
Take damage → break line of sight → get behind hard cover → stop firing → regen (slow)
                                                      ↓
                              use Health Pack → Rapid Recovery 12s → regen (fast)
```

| Source | Type | Where found |
|---|---|---|
| **Health Pack** | Consumable (max 3) | Supply crates, elite drops, hidden caches |
| **Powerup** | Buff w/ trade-off (max 2) | Salvage objects, nest caches, elite corpses |
| **Cover regen** | Passive | Hard cover objects in combat zones |
| **Full heal** | Checkpoint | Save points, base |

**UI feedback** — Cover objects pulse blue when usable; a green +HP/s indicator appears while regen is active; Health Pack buff shows a countdown bar on the HUD.

### Interaction with Characters & Armor

| Factor | Effect on regen |
|---|---|
| **Vanguard** | +2 HP/s in cover (8 standard / 20 rapid) — tank recovers slightly faster |
| **Ranger** | No bonus; relies on cover positioning and range |
| **Breacher** | Cover regen pauses 1s after self-damage from Breach Charge |
| **Bulwark Frame** | Regen continues through 1 chip-damage hit without breaking (once per cover session) |
| **Light Recon Suit** | −1 HP/s in cover — speed armor trade-off |

---

## Salvage Powerups

Breaking salvageable objects during exploration drops **materials** and a chance at a **powerup**. Powerups are combat buffs with built-in downsides — separate from health packs (healing) and scrap/alloy (crafting).

### How Salvaging Works

Approach a salvage object and hold interact to break it down. Takes 1.5s; vulnerable to nearby nest alerts.

| Yield | Chance |
|---|---|
| Scrap (1–3) | 100% |
| Alloy (1) | 15% (25% in Act 2+, 35% in Act 3) |
| Powerup | 40% per salvage break |

**Inventory** — Max **2** powerups carried. Picking up a third requires discarding one. Powerups persist until used or replaced at a save point (save points do not stock powerups — only what you carried in).

### Salvage Sources

| Object | Biome | Also drops | Notes |
|---|---|---|---|
| Salvage wreckage | Colonies | Common powerups | Rovers, crates, antenna frames; destroys cover |
| Field sensor pole | Hives | Utility powerups | Quick break, low scrap |
| Specimen tank | Hives | Defensive powerups | Acid burst if broken without Spore Filter |
| Cargo pod | Wreckage | Offensive powerups | May contain hidden alloy |
| Collapsed solar array | Colonies | Defensive / utility | Slower break, higher alloy chance |
| Nest cache | All | Any pool | Revealed after clearing a nest; guaranteed powerup |
| Elite corpse | All | Rare powerups | Dropped by overpowered kills in ambushes |

---

### Powerup Catalog

All powerups activate instantly on pickup (auto-use) or via hotkey if inventory is full. Durations stack by refreshing the timer, not doubling the effect.

#### Offensive

| Powerup | Buff | Trade-off | Duration |
|---|---|---|---|
| **Overcharge Rounds** | +50% weapon damage | −20% move speed | 15s |
| **Fury Catalyst** | +30% fire rate | Take +20% damage | 12s |
| **Piercing Core** | Shots pierce +1 target | −15% stagger/knockback | 20s |
| **Breach Detonator** | AoE/explosive radius +40% | Self-damage on detonation (−5 HP per burst) | 15s |

#### Defensive

| Powerup | Buff | Trade-off | Duration |
|---|---|---|---|
| **Reactive Plating** | −30% damage taken | −15% weapon damage dealt | 10s |
| **Kinetic Dampener** | Immune to knockback and stagger | −10% move speed | 18s |
| **Spore Neutralizer** | Immune to acid and spore chip | −10% max HP until next save point | 20s |
| **Hardlight Barrier** | Absorb next 40 damage | Cannot sprint/boost roll while active | Until broken |

#### Utility

| Powerup | Buff | Trade-off | Duration |
|---|---|---|---|
| **Targeting Uplink** | Weak points glow; +20% accuracy | Ability cooldowns +50% | 20s |
| **Scrap Magnet** | Salvage breaks yield double scrap/alloy | Alerts nests within 3 tiles on activate | 30s |
| **Adrenal Surge** | +25% move speed | Weapon spread +30% (less accurate) | 12s |
| **EMP Capsule** | Stuns all aliens in 3-tile radius (2s) | Player weapon disabled 1s after pulse | Instant |

#### Risk / Reward

| Powerup | Buff | Trade-off | Duration |
|---|---|---|---|
| **Stim Injector** | Instant +25% HP | −2 HP/s for 10s after | Instant + DoT |
| **Volatile Rounds** | Kills explode for AoE (small) | +15% self-damage from all sources | 15s |
| **Glass Cannon Injector** | +75% damage | Max HP reduced to 50% for duration | 12s |

---

### Salvage Drop Pools

Which powerups appear depends on the object salvaged.

| Pool | Objects | Common drops | Rare drops |
|---|---|---|---|
| **Offensive** | Cargo pods, elite corpses | Overcharge Rounds, Fury Catalyst | Glass Cannon Injector |
| **Defensive** | Specimen tanks, solar arrays | Reactive Plating, Kinetic Dampener | Hardlight Barrier |
| **Utility** | Sensor poles, nest caches | Targeting Uplink, Adrenal Surge | EMP Capsule |
| **Mixed** | Salvage wreckage, general crates | Any common powerup | Piercing Core, Scrap Magnet |

**Rare powerups** — 10% of powerup drops from any source.

---

### When to Salvage

| Situation | Recommendation |
|---|---|
| Between nest fights | Safe break window; stack buffs before larger ambush |
| Before save point | Grab powerup, then prep loadout at save — buff carries forward |
| During combat | Risky — 1.5s interact is interruptible; break cover objects only if desperate |
| Before boss Wave 1 | Salvage remaining objects on route; buffs do **not** carry into mech phases |

Powerups are **on-foot only** — they expire or are stripped when boarding the mech at boss Wave 2. The sole exception is the boss-exclusive **Kingbreaker Payload** (see below).

---

## Kingbreaker Payload

A **boss-finisher powerup** used exclusively at the end of Wave 3. Not found in exploration, salvage, or nests — only dropped by the **last alien killed** in the Wave 3 horde (always a basic grunt, never the king or an Overpowered).

### Wave 3 Finale Flow

```
Wave 3 starts — king + overpowered + basics (king invulnerable while adds live)
     ↓
Mech clears all adds and overpowered units
     ↓
Last alien killed drops Kingbreaker Payload → auto-equips to mech weapon
     ↓
Finisher Aim mode — slow move, line up crosshair on exposed king core
     ↓
Fire once — hit = king destroyed; miss = payload lost, king enrages
```

### Rules

| Rule | Detail |
|---|---|
| **King invulnerability** | King cannot be damaged until every add and Overpowered unit in Wave 3 is dead |
| **Drop trigger** | Final kill in the Wave 3 horde; payload spawns at corpse, auto-collects |
| **Auto-equip** | Immediately replaces mech primary fire for one charged shot; no inventory slot |
| **Finisher Aim** | 8s window; mech move speed −50%; camera zooms slightly; king's core glows as target |
| **Hit** | Instant kill; king collapse cinematic; **king core** reward; Act 3 hit triggers [ending cutscene](#ending--game-complete) |
| **Miss** | Payload dissipates; king **enrages** (+25% attack speed, +15% damage); finish by normal mech DPS |

### Visual & Feel

- Payload reads as a oversized glowing slug round slotting into the mech barrel — color matches area theme (green/hive, amber/colony, blue/wreckage).
- Crosshair is a diamond reticle; king's exposed core pulses during aim window.
- On hit: screen freeze 0.3s, king shatters, shockwave clears arena debris.
- Cannot be saved, crafted, or found outside Wave 3.

### Per-Area Presentation

| King | Payload name (UI) | Core weak point exposed |
|---|---|---|
| **Brood Matriarch** | Hivebreaker Round | Sternum core between spore sacs |
| **Carapace Regent** | Regentbreaker Round | Glowing back core through cracked shell |
| **Signal Overmind** | Overbreaker Round | Crystalline heart at ring center |

---

## Minor Alien Types

Eight minor alien species across four archetypes. Each has readable attack tells, a clear counter, and biome placement. Material drops: **scrap** (common grunt), **alloy** (elite or mini-boss variants).

### Ranged

#### Spore Slinger
*Bio-mechanical hives*

| | |
|---|---|
| **Role** | Area-denial ranged |
| **Durability** | Low HP, no armor |
| **Behavior** | Maintains mid-range distance; retreats if the player closes within melee range |

**Attacks**
- **Lobbed Spore** — Arcing projectile leaves a small acid puddle on impact (2s duration). Tell: rears back and inflates spore sac (0.8s wind-up).
- **Spore Burst** — Fan of 3 spores at close range when cornered. Tell: sac pulses green before popping.

**Counter** — Close distance during lob wind-up; sidestep arc and punish the retreat. Prioritize over chargers while active.

**Drops** — 1–2 scrap

---

#### Needle Drone
*Ruined colonies, orbital wreckage*

| | |
|---|---|
| **Role** | Single-target pressure |
| **Durability** | Very low HP; dies in 1–2 hits |
| **Behavior** | Hovers at long range; strafes slowly left/right between bursts |

**Attacks**
- **Needle Burst** — 5-round rapid fire at the player's last known position. Tell: targeting laser appears on the ground (0.5s) before the burst.
- **Swarm Stack** — Groups of 3–5 drones overlap fire timing for staggered bursts.

**Counter** — Move perpendicular when the laser appears; burst-fire one drone at a time. AoE weapons clear stacks efficiently.

**Drops** — 1 scrap per drone

---

### Charger

#### Rupture Hound
*Bio-mechanical hives*

| | |
|---|---|
| **Role** | Melee rush / knockback |
| **Durability** | Medium HP |
| **Behavior** | Patrols until player enters detection range; commits to a single rush vector |

**Attacks**
- **Rupture Rush** — Fast dash with knockback on hit. Tell: lowers body and emits a low growl / ground scratch (0.6s). Travels in a straight line.
- **Recovery Stagger** — Slides 0.4s after a missed rush; vulnerable window.

**Counter** — Dodge perpendicular at the scratch tell; punish during recovery. Shields absorb one rush but break on impact.

**Drops** — 2–3 scrap

---

#### Arc Lancer
*Orbital wreckage*

| | |
|---|---|
| **Role** | Mid-range lunge |
| **Durability** | Medium HP, light side armor |
| **Behavior** | Holds position behind other units; lunges when player is within 4-tile range |

**Attacks**
- **Arc Thrust** — Lunge with an electric trail along the path (lingers 1s). Tell: lance tip sparks blue (0.7s wind-up).
- **Overcharge** — On hit, applies a brief slow (1.5s). Miss triggers recovery stagger like Rupture Hound.

**Counter** — Backstep or jump over the trail; attack from the side during wind-up. Insulated armor negates the slow.

**Drops** — 2–3 scrap; **1 alloy** (elite variant with golden lance tip)

---

### Shield-Bearer

#### Carapace Guard
*Bio-mechanical hives, ruined colonies*

| | |
|---|---|
| **Role** | Frontal wall |
| **Durability** | High HP; frontal shell negates all damage |
| **Behavior** | Faces the player; turns slowly (90°/s). Never retreats |

**Attacks**
- **Shell Bash** — Short-range slam if the player sits in front too long. Tell: shell vibrates / cracks glow (1.0s).
- **Brace** — Stops moving and hardens shell for 2s after taking flank damage; reflects 25% melee damage during brace.

**Counter** — Flank or bait a turn with a feint run, then strike the exposed back. Explosives and melee from behind bypass the shell.

**Drops** — 3–4 scrap

---

#### Phalanx Brood
*Ruined colonies*

| | |
|---|---|
| **Role** | Formation tank |
| **Durability** | Medium HP per unit; shared frontal shield arc when linked |
| **Behavior** | Moves as a row of 3; shield arc covers 120° in front of the formation |

**Attacks**
- **Advance** — Slow forward push while shields are linked. Tell: units click carapaces together (audible clack).
- **Shield Break** — Killing one unit breaks the arc; survivors scatter and become individual Carapace Guards (reduced HP).

**Counter** — Flank or use AoE to break the link. A single flank kill collapses the formation. Pull them apart with knockback weapons.

**Drops** — 2 scrap per unit; **1 alloy** if the full phalanx is broken without killing individuals first

---

### Summoner

#### Brood Nurseling
*Bio-mechanical hives*

| | |
|---|---|
| **Role** | Spawner |
| **Durability** | Low HP; priority target |
| **Behavior** | Stays at the back of enemy groups; never engages in melee |

**Attacks**
- **Spawn Pod** — Releases 2 Needle Drones every 8s. Tell: abdomen swells and pulses (1.2s); interruptible.
- **Panic Spill** — On death, releases 1 final drone and a small acid pool beneath the corpse.

**Counter** — Focus fire during the swell tell to interrupt the spawn. Kill before other adds overwhelm. Ranged builds excel.

**Drops** — 2–3 scrap; spawned drones drop scrap separately

---

#### Signal Cyst
*Orbital wreckage, ruined colonies*

| | |
|---|---|
| **Role** | Stationary spawner / zone control |
| **Durability** | Medium HP; rooted, cannot move |
| **Behavior** | Placed in chokepoints; pulses on a fixed timer regardless of player distance |

**Attacks**
- **Pulse Wave** — Every 10s, spawns 1 Rupture Hound at the nearest open tile. Tell: cyst flashes red and emits a sonar ping (1.5s).
- **Spike Retaliation** — Fires ground spikes if struck in melee. Tell: surface cracks (0.4s). Ranged-only safe DPS window.

**Counter** — Destroy early with ranged weapons; time kills to the pulse tell to avoid a spawn. Spike Retaliation punishes melee rushdown.

**Drops** — 3–4 scrap; **1 alloy** (first kill per mission zone)

---

### Encounter Composition Notes

| Biome | Common mix | Player challenge |
|---|---|---|
| **Bio-mechanical hives** | Spore Slingers + Rupture Hounds + Brood Nurselings | Area denial + rush pressure + add management |
| **Ruined colonies** | Needle Drones + Carapace Guards + Phalanx Broods | Target priority + flanking |
| **Orbital wreckage** | Arc Lancers + Signal Cysts + Needle Drone stacks | Lane control + spawn timers + spacing |

**Overpowered variants** (golden markings, +75% HP, +50% damage) appear in boss Waves 2 and 3, and as occasional elites in later-area ambushes. Drop alloy instead of scrap.

**Nest encounters** use standard basics only — never Overpowered. See [Area Progression](#area-progression).

---

## Player Types

Three playable **characters**, six **weapons**, and five **armor** sets. Any character can equip any weapon or armor; swap weapons en route, full loadout at save points. Each option has a hard counter to specific alien types.

### Characters

#### Vanguard
*Frontline brawler*

| | |
|---|---|
| **Role** | Melee tank / interrupt |
| **Base stats** | High HP, medium speed, low ranged damage |
| **Passive** | **Stand Ground** — Takes 25% less knockback; recovers from stagger 30% faster |

**Ability: Shoulder Rush** (6s cooldown)
- Short forward dash that staggers chargers on contact. Tell on enemy: same scratch cue as Rupture Rush — use to collide head-on and cancel their rush.
- Effective in boss Wave 1 on-foot skirmishes and larger ambushes.

**Best vs** — Rupture Hound, Arc Lancer (closes gap during wind-up), Carapace Guard (bait turn → backstab)

**Weak vs** — Needle Drone stacks, Spore Slinger area denial, Signal Cyst (melee punished by spikes)

**Ideal loadout** — Thermal Blade + Bulwark Frame or Flanker Harness

---

#### Ranger
*Precision marksman*

| | |
|---|---|
| **Role** | Single-target ranged DPS |
| **Base stats** | Low HP, high speed, high ranged damage |
| **Passive** | **Focus** — Standing still for 0.5s grants +20% accuracy and +1 pierce on next shot |

**Ability: Target Lock** (8s cooldown)
- Marks one enemy for 4s; marked enemies take +30% damage and reveal hidden weak points (e.g. Carapace Guard back shell glows).
- Interrupts Brood Nurseling swell — firing the mark during the 1.2s tell cancels the spawn.

**Best vs** — Brood Nurseling, Needle Drone, Signal Cyst (safe ranged DPS)

**Weak vs** — Rupture Hound (low HP punishes mistakes), Phalanx Brood without pierce/AoE support

**Ideal loadout** — Pulse Carbine or Rail Spear + Light Recon Suit or Spore Filter

---

#### Breacher
*AoE demolitions*

| | |
|---|---|
| **Role** | Crowd control / formation break |
| **Base stats** | Medium HP, medium speed, high AoE damage |
| **Passive** | **Demolition** — Explosive and AoE attacks deal +25% damage to grouped enemies (2+ within 2 tiles) |

**Ability: Breach Charge** (10s cooldown)
- Plants a charge on the ground or on a Carapace Guard's back; detonates after 1s for heavy AoE. Breaks Phalanx linked shields instantly if 2+ units are in blast radius.
- Destroys acid puddles from Spore Slingers on detonation.

**Best vs** — Phalanx Brood, Needle Drone stacks, Spore Slinger puddles, grouped hive encounters

**Weak vs** — Arc Lancer (needs spacing during lunge), single Carapace Guard (overkill, slow TTK)

**Ideal loadout** — Scatter Launcher or Flak Cannon + Insulated Plating or Spore Filter

---

### Weapons

All weapons have **unlimited ammo**.

| Weapon | Type | Fire pattern | Hard counter | Upgrade path (scrap → alloy) |
|---|---|---|---|---|
| **Pulse Carbine** | Ranged | 3-round burst, medium range | Brood Nurseling (interrupt swell), Needle Drone (1-burst kill) | +1 round per tier; tier 3 adds mark synergy with Ranger |
| **Rail Spear** | Ranged/melee | Charged pierce shot or melee thrust | Phalanx Brood (line pierce through formation), Signal Cyst (safe spike-range poke) | +pierce count; tier 3 pierce ignores frontal shell at reduced damage |
| **Scatter Launcher** | AoE | Wide cone, short range | Needle Drone stacks, Spore Burst fan attack | +cone width; tier 3 knockback on hit |
| **Flak Cannon** | AoE/air | Arcing flak burst, anti-hover | Needle Drone (hover), Brood Nurseling adds | +burst radius; tier 3 destroys projectiles in air |
| **Thermal Blade** | Melee | Fast slashes, backstab bonus ×2 | Carapace Guard (flank), Rupture Hound (recovery punish) | +attack speed; tier 3 applies brief stagger on backstab |
| **Shock Net** | Utility/CC | Short-range net, 2s root | Rupture Hound (rush interrupt), Arc Lancer (lunge interrupt) | +root duration; tier 3 chains to 1 nearby enemy |

---

### Armor

| Armor | Passive | Hard counter | Trade-off |
|---|---|---|---|
| **Light Recon Suit** | +15% move speed; dodge roll has 2 iframe frames | Arc Lancer trail (outrun), Needle Burst (reposition) | −10% max HP |
| **Bulwark Frame** | Absorbs one charger hit per mission (shield breaks, must re-equip at save point) | Rupture Rush, Arc Thrust | −10% move speed |
| **Insulated Plating** | Immune to electric slow and trail damage | Arc Lancer Overcharge and trail | No bonus vs non-electric threats |
| **Flanker Harness** | +30% speed when moving toward an enemy's exposed back; backstab damage +15% | Carapace Guard, Phalanx Brood (flank collapse) | Frontal damage taken +10% |
| **Spore Filter** | Immune to acid puddles and Spore Burst chip damage | Spore Slinger, Brood Nurseling Panic Spill | −5% ranged damage |

---

### Counter Matrix

Recommended pairings when entering a biome. Swap at save points before each zone.

| Alien | Best character | Best weapon | Best armor |
|---|---|---|---|
| Spore Slinger | Breacher | Scatter Launcher | Spore Filter |
| Needle Drone | Ranger / Breacher | Flak Cannon / Pulse Carbine | Light Recon Suit |
| Rupture Hound | Vanguard | Shock Net / Thermal Blade | Bulwark Frame |
| Arc Lancer | Ranger | Pulse Carbine | Insulated Plating |
| Carapace Guard | Vanguard | Thermal Blade | Flanker Harness |
| Phalanx Brood | Breacher | Scatter Launcher / Breach Charge | Flanker Harness |
| Brood Nurseling | Ranger | Pulse Carbine | Light Recon Suit |
| Signal Cyst | Ranger | Rail Spear | Insulated Plating |

| Biome | Suggested squad approach |
|---|---|
| **Bio-mechanical hives** | Breacher + Scatter Launcher clears adds; Ranger switches in for Nurselings; Vanguard handles Hounds |
| **Ruined colonies** | Vanguard + Thermal Blade flanks Guards; Breacher breaks Phalanx; Ranger picks off Drones |
| **Orbital wreckage** | Ranger + Rail Spear destroys Cysts at range; Insulated Plating for Lancers; Shock Net for stray Hound spawns |

### Upgrade Notes

- Weapon and armor upgrades cost **scrap** at save points; tier 2–3 require **alloy**.
- Character abilities upgrade separately (ability cooldown −10% per tier) and are tied to the character, not the weapon.
- On-foot weapon upgrades are separate from mech port investment — see [Mech System](#mech-system).

---

## King Alien Types

One king alien per area. Boss fights are **three-phase sequences** — not a single duel. Waves 1 and 2 are horde fights using that area's basic alien roster; Wave 3 introduces the king amid overpowered and basic reinforcements. Kings drop **king cores** on Wave 3 victory.

### Boss Sequence Overview

| Phase | Mode | Content |
|---|---|---|
| **Wave 1 — Skirmish** | On foot | Quick basic-alien wave; biome mix, no king, no Overpowered |
| **Wave 2 — Assault** | Mech | Scaled-up horde + Overpowered basics mixed in; drop pod after Wave 1 |
| **Intermission** | Save + upgrade | Checkpoint, full heal, mech port upgrades using area materials |
| **Wave 3 — King** | Mech | King + forces → clear all adds → **Kingbreaker Payload** → finisher one-shot |

---

### The Brood Matriarch
*Bio-mechanical Hives — Act 1 king*

| | |
|---|---|
| **Silhouette** | Towering bloated abdomen on multiple spindly legs; spore sacs glow along the spine |
| **Wave 1 forces** | 8 basics — Spore Slingers, Rupture Hounds, Needle Drones |
| **Wave 2 forces** | 15 basics + 3 Overpowered (1 Slinger, 1 Hound, 1 Nurseling) |
| **Wave 3 forces** | Matriarch + 2 Overpowered + 6 basics |

**Wave 1 — On foot**
- Short arena skirmish; standard nest aliens at exploration difficulty.
- Counter with on-foot loadout built during the area run.

**Wave 2 — Mech**
- Drop pod deploys after Wave 1 clear.
- Overpowered Nurseling spawns adds mid-wave — prioritize with Scatter Pod or EMP Burst.

**Intermission** — Spend area materials on mech ports; recommended: Damage or Shield investment.

**Wave 3 — Mech (king attacks)**
- King **invulnerable** until 2 Overpowered + 6 basics are eliminated.
- **Hive Flood** — Acid creep at arena edges (slows mech 30%). Tell: abdomen glows green (1.5s). Counter: Cyclone jump jets.
- **Brood Eruption** — Reinforcement spawn: 2 Overpowered Hounds + 4 basics. Tell: sternum splits (1.0s). Counter: Scatter Pod; clear adds, not the king.
- **Matriarch Lunge** — Full-arena body slam. Tell: rears up (2.0s). Counter: Siegeframe Bastion Shield.

**Finisher** — Last add drops **Hivebreaker Round**; aim at exposed sternum core. Matriarch Lunge tells stop during Finisher Aim.

**Mech counters** — Damage 4+ Cyclone + Scatter Pod for add clear; aim carefully — miss triggers enrage

---

### The Carapace Regent
*Ruined Colonies — Act 2 king*

| | |
|---|---|
| **Silhouette** | Towering armored alien in layered shell plates; ridge of chitin spikes along its back |
| **Wave 1 forces** | 10 basics — Carapace Guards, Needle Drones, Phalanx Brood |
| **Wave 2 forces** | 18 basics + 4 Overpowered (2 Guards, 1 Phalanx unit, 1 Lancer) |
| **Wave 3 forces** | Regent + 4 Overpowered + 10 basics |

**Wave 1 — On foot**
- Phalanx Brood anchors the wave; Breacher Breach Charge or flanker approach from exploration prep.

**Wave 2 — Mech**
- Overpowered Carapace Guards require flanking in mech — Lancer Boost Slide or Cyclone Hammer Arm from behind.
- Overpowered Phalanx unit breaks formation if one link is destroyed.

**Intermission** — Invest ports before the king; Rail Cannon + Damage port recommended.

**Wave 3 — Mech (king attacks)**
- King **invulnerable** until 4 Overpowered + 10 basics are eliminated.
- **Shell Rotate** — Swaps frontal weak point every 8s. Tell: segments click. Counter: Targeting Array module.
- **Spine Barrage** — Spike rain 4s. Tell: spine ridge spins up (1.2s). Counter: Deployable Cover.
- **Regent Stampede** — Double charge. Tell: lowers spine ridge (1.5s). Counter: Shock Lance stagger.

**Finisher** — Last add drops **Regentbreaker Round**; back core exposed through cracked shell — do not confuse with Shell Rotate weak point.

**Mech counters** — Clear adds fast with AoE; Targeting Array helps line up finisher

---

### The Signal Overmind
*Orbital Wreckage — Act 3 king*

| | |
|---|---|
| **Silhouette** | Floating crystalline core surrounded by rotating wreckage rings; cables hang like tentacles |
| **Wave 1 forces** | 12 basics — Arc Lancers, Rupture Hounds, Needle Drone stacks |
| **Wave 2 forces** | 20 basics + 6 Overpowered (2 Lancers, 2 Hounds, 2 Signal Cysts) |
| **Wave 3 forces** | Overmind + 6 Overpowered + 14 basics |

**Wave 1 — On foot**
- Densest Wave 1; Insulated Plating strongly recommended for Arc Lancer trails.

**Wave 2 — Mech**
- Overpowered Signal Cysts rooted in arena — destroy with Hammer Arm before they pulse Hounds.
- Highest Overpowered ratio in the campaign.

**Intermission** — Last port investment before finale; Capacitor Bank or Mobility ports help survive Core Overload.

**Wave 3 — Mech (king attacks)**
- King **invulnerable** until 6 Overpowered + 14 basics are eliminated.
- **Ring Laser** — Sweeping beam 3s. Tell: core brightens (1.5s). Counter: Lancer Boost Slide through ring gap.
- **Spawn Tower** — King raises 2 towers (Overpowered Cysts) while adds remain. Counter: Hammer Arm (2 hits each).
- **Core Overload** — Arena shrinks via electric fence while adds remain. Tell: core pulses red (2.0s).

**Finisher** — Last add drops **Overbreaker Round**; crystalline heart exposed at ring center — hardest aim window (moving target between ring gaps). A successful finisher triggers the **campaign ending cutscene**.

**Mech counters** — Cyclone + Hammer Arm for add/tower clear; Boost Slide positions for finisher shot

---

## Mech System

Mechs deploy during boss **Wave 2** and **Wave 3**. Play style is defined by investing materials into four **upgrade ports** on your chassis — at **Command Base** between areas and at the **boss intermission** before Wave 3. The same Siegeframe can become a damage-heavy brawler or a near-invulnerable wall depending on where you spend scrap, alloy, and king cores gathered during exploration.

Chassis, mech weapon, utility, and passive module are equipped at Command Base before entering an area. **Mech port upgrades** are available at Command Base and the boss intermission; on-foot item upgrades at save points do not affect port levels. The active character grants a **+15% bonus** to their matching chassis archetype.

### Upgrade Ports

Each port has **5 tiers**. Materials are spent at Command Base (permanent campaign investment) or at the **boss intermission** (spend area run materials before Wave 3). You cannot max every port — specialization is the point.

| Port | Governs | Per tier (cumulative) |
|---|---|---|
| **Damage** | Weapon output, stagger, weak-point bonus | +12% mech weapon damage; +5% stagger duration |
| **Shield** | HP, barrier power, damage reduction | +10% max HP; +8% Bastion Shield absorption; +3% flat damage reduction |
| **Mobility** | Speed, dodge iframes, boost cost | +6% move speed; +1 dodge iframe; −5% boost Energy cost |
| **Reactor** | Energy pool, recharge, overheat recovery | +10 max Energy; +1/s recharge; −0.3s overheat lockout |

**Tier costs**

| Tier | Cost |
|---|---|
| 1 | 10 scrap |
| 2 | 20 scrap |
| 3 | 15 alloy |
| 4 | 25 alloy |
| 5 | 1 king core |

Total to max one port: 30 scrap + 40 alloy + 1 king core. A full campaign yields enough to heavily invest in 2 ports and partially fill a third.

---

### Build Profiles

How port investment shapes play style. All examples use the same chassis — ports define the feel.

#### Glass Cannon
*Damage 5 · Shield 1 · Mobility 3 · Reactor 2*

| Stat | Result |
|---|---|
| Damage output | ~+60% weapon damage; staggers land reliably |
| Survivability | Low HP; shield barely helps |
| Play style | Burst during tells, end fights fast before taking hits |

**Best kings** — Carapace Regent (core burn), Signal Overmind (Core Overload race)

---

#### Bulwark
*Shield 5 · Damage 2 · Mobility 1 · Reactor 3*

| Stat | Result |
|---|---|
| Damage output | Modest; wins through attrition |
| Survivability | ~+50% HP, ~+40% shield absorption, ~+15% damage reduction |
| Play style | Hold ground, absorb slams and barrages, chip away safely |

**Best kings** — Brood Matriarch (survive Lunge + Flood), Carapace Regent (outlast Barrage)

---

#### Striker
*Mobility 5 · Damage 4 · Shield 1 · Reactor 1*

| Stat | Result |
|---|---|
| Damage output | High; reposition for weak-point shots |
| Survivability | Fragile but rarely hit |
| Play style | Boost through gaps, dodge lasers, punish recovery windows |

**Best kings** — Signal Overmind (Ring Laser gaps), Carapace Regent (dodge Stampede)

---

#### Sustain
*Reactor 5 · Damage 3 · Shield 3 · Mobility 2*

| Stat | Result |
|---|---|
| Damage output | Moderate sustained DPS |
| Survivability | Balanced; never overheats |
| Play style | Hold fire through tells, dump Energy in safe windows, repeat |

**Best kings** — Any king with long mech phases; especially Overmind Core Overload

---

### Energy & Overheat

Base stats are modified by **Reactor port** tier. Example at Reactor 0 vs Reactor 5:

| | Reactor 0 | Reactor 5 |
|---|---|---|
| Max Energy | 100 | 150 |
| Recharge | 12/s | 17/s |
| Overheat lockout | 3.0s | 1.5s |

| Action | Energy cost |
|---|---|
| Primary fire (per second) | 8/s |
| Chassis ability | 25 |
| Utility | 20 |
| Boost/dodge | 10 (−5% per Mobility tier) |

Hitting **0 Energy** triggers **Overheat** — forced cooldown, mech rooted. High Reactor builds overheat less; high Damage builds must manage burst windows.

---

### Chassis

Base stats before port investment. Ports stack on top.

| Chassis | Archetype | Base HP | Base speed | Chassis ability | Character synergy |
|---|---|---|---|---|---|
| **Siegeframe** | Tank | High | Slow | **Bastion Shield** — Frontal barrier 4s; absorbs 50% damage (25 Energy) | Vanguard +15% shield duration |
| **Lancer** | Ranged DPS | Low | Fast | **Boost Slide** — Lateral dash, 4 iframe frames (10 Energy) | Ranger +15% damage on weak points |
| **Cyclone** | AoE | Medium | Medium | **Jump Jets** — Short hop; clears hazards, avoids 1 slam (25 Energy) | Breacher +15% AoE radius |

**Chassis × port synergy**
- **Siegeframe** — Shield port amplifies Bastion Shield; natural Bulwark builds
- **Lancer** — Damage + Mobility ports stack; natural Glass Cannon / Striker builds
- **Cyclone** — Damage port boosts AoE cleave; Mobility helps reposition between slams

---

### Mech Weapons

Equipped at base. Damage port tiers apply to whichever weapon is mounted.

| Mech weapon | Archetype source | Pattern | Scales with Damage port |
|---|---|---|---|
| **Siege Fists** | Thermal Blade / melee | Slow heavy punches, frontal stagger | Stagger duration per tier |
| **Rail Cannon** | Pulse Carbine / Rail Spear | Charged pierce shot, single-target | Charge damage and pierce bonus |
| **Scatter Pod** | Scatter Launcher / Flak | Wide cone salvo, clears adds | Cone width at tiers 3 and 5 |
| **Hammer Arm** | Breach Charge / AoE | Overhead slam, structure damage | Structure damage (towers, shields) |

---

### Utilities & Passive Modules

One utility slot and one passive module per mech. Equipped at base; module effects stack with port investment.

| Utility | Effect | Pairs well with |
|---|---|---|
| **Shock Lance** | Staggers charger-type moves (20 Energy) | Damage port — opens burst windows |
| **Deployable Cover** | Wall for 6s (20 Energy) | Shield port — double-layer defense |
| **EMP Burst** | Disables adds/towers 3s (20 Energy) | Damage port — safe burst on disabled targets |
| **Coolant Flush** | Exits Overheat; restores 50 Energy (20 Energy) | Reactor port — rapid re-entry to combat |

| Module | Passive | Pairs well with |
|---|---|---|
| **Reinforced Plating** | −20% damage taken | Shield port — maximum tank |
| **Capacitor Bank** | +20 max Energy | Reactor port — near-permanent uptime |
| **Targeting Array** | Weak points glow; +10% core damage | Damage port — king killer |
| **Hazard Seals** | Immune to acid/electric floor | Mobility port — ignore terrain, keep moving |

---

### King ↔ Mech Build Guide

Recommended port focus per king. Weapon and utility suggestions assume that investment.

| King | Port focus | Chassis | Weapon | Utility |
|---|---|---|---|---|
| **Brood Matriarch** | Shield 4+ or Damage 4+ (add clear) | Siegeframe / Cyclone | Scatter Pod / Siege Fists | EMP Burst |
| **Carapace Regent** | Damage 4+ (core burn) or Shield 4+ (survive Barrage) | Lancer / Siegeframe | Rail Cannon | Deployable Cover |
| **Signal Overmind** | Mobility 3+ Damage 4+ or Reactor 4+ Sustain | Lancer / Cyclone | Hammer Arm / Rail Cannon | Coolant Flush |

**Boss intermission tip** — Materials collected during exploration fund port tiers here. Wave 2 performance reveals build gaps; invest in the port that failed before Wave 3.

**Finisher tip** — Wave 3 is about **clearing adds**, not damaging the king. Save mech Energy for add clear, then line up the Kingbreaker shot. A miss means fighting an enraged king without the finisher.

---

## Additional Ideas

### Combat & World

- **Environmental hazards** — Acid pools, collapsing floors, alien spore clouds — shared danger for player and enemies.
- **Branching mission paths** — Optional high-risk routes with better material drops.

### Meta & Polish

- **Salvage routing** — Optional paths with extra wreckage for powerup/material farming at the cost of nest exposure.
- **Codex / bestiary** — Unlock entries by defeating enemy types.
- **New Game+ scaling** — Tougher compositions and new king modifiers on **Restart Game** playthroughs.
- **Juice** — Screen shake, hit-stop, particle bursts on kills and mech impacts.
- **Clear UI feedback** — Material counts, crafting recipes, upgrade previews, and boss phase indicators.
