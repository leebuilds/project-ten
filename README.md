# Project Ten

A **top-down 2D sci-fi action game** built in Godot. You land on the hostile planet **Keth-9**, scavenge materials to upgrade your mech, and fight through three overrun zones to earn a place in the fleet bound for the alien homeworld.

## Summary

Exploration and material collection drive the game — combat punctuates the journey rather than filling it. You cross open wasteland between save points, disturb alien nests, salvage wreckage for upgrades, and prep your loadout at checkpoints. Each area ends in a **three-phase boss fight**: on-foot wave → mech wave → king battle with a **Kingbreaker** finisher one-shot.

**Opening:** Fleet briefing — *"Good luck, soldier."* → Command Base.  
**Ending:** Mech certified combat-ready → joins the battle fleet → game complete.

## Core Loop

1. **Briefing** — Opening cutscene (new game only)
2. **Explore** — Cross terrain, collect scrap/alloy, salvage powerups
3. **Fight occasionally** — Nest encounters and larger ambushes near save points
4. **Prep** — 5+ save points per area; swap weapons en route only
5. **Boss** — On-foot wave → mech wave → upgrade intermission → king + Kingbreaker finisher
6. **Advance** — Three areas (Hives → Colonies → Wreckage), escalating difficulty

## Key Systems

| System | Detail |
|---|---|
| **Progression** | Stackable materials; craft at Command Base; mech port upgrades (Damage / Shield / Mobility / Reactor) |
| **Combat** | Unlimited ammo; health regen in cover; health packs boost regen |
| **On foot** | 3 characters, 6 weapons, 5 armor sets — full swap at save points |
| **Mech** | Deploys in boss Waves 2–3; build style via port investment |
| **Powerups** | Salvage drops with trade-offs; Kingbreaker finisher at end of Wave 3 |

## Documentation

Full design specs — aliens, bosses, mechs, biomes, cutscenes, tables, and balance notes:

- **[docs/game-design.md](docs/game-design.md)** — complete game design document
- **[docs/README.md](docs/README.md)** — documentation index with section links
