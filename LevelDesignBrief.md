# JuggernautArena — Level Design Brief

*Starter doc for level/map designers. Read this before opening Studio.*

## 1. What the game is

JuggernautArena is an **asymmetric PvP arena shooter** on Roblox. Each round:

- **1 player is the Boss** — a hand-picked, oversized character with unique health scaling (scales up with attacker count), unique physics (move speed, gravity, hitbox size), and a fixed loadout of powerful weapons/abilities.
- **Everyone else is an Attacker** — smaller, faster, weaker individually, armed with a chosen loadout of guns/melee/abilities from a shared equipment pool.

The two sides fight in a single arena until time runs out (decided by point/damage totals) or one side is wiped. Think **"4-12 regular players vs. 1 monster,"** not team-vs-team symmetric shooter.

Movement is a **custom Quake/Source-style system** — bunny-hopping, air-strafing, and momentum-based movement are intentional and core to how Attackers evade the Boss. This is not default Roblox walk/jump physics, so maps need to support skill-expressive movement (ramps, ledges, gaps), not flat hallways.

Combat is a mix of **hitscan, projectile, and melee** weapons, all server-validated with lag compensation — meaning fights can happen at range *and* up close, and the map needs to support both.

## 2. The core design tension maps need to solve

Every map exists to balance one thing: **the Boss is slow-ish but hits like a truck and has tons of HP; Attackers are fast and mobile but individually fragile.**

A good JuggernautArena map:
- Gives Attackers **routes to kite, juke, and break line of sight** from the Boss (corners, pillars, doorways, verticality).
- Gives the Boss **enough open space and shortcuts** to cut off kiting and not feel like it's chasing forever (collapsing terrain, central chokepoints, multiple paths converging).
- Rewards **movement tech** (bhop ramps, jump pads, ledges to strafe-jump between) without trivializing the Boss's ability to catch people.
- Avoids pure sniper sightlines across the whole map (no map-spanning open field with zero cover) and avoids pure maze/corridor crawls (kills the movement system's purpose).
- Has a **readable layout** — in the heat of a chase, both the Boss and Attackers need to instantly understand where they are and where the nearest cover/escape route is.

## 3. Structural requirements (the must-haves)

- **Scale**: needs to comfortably fit a Boss-sized hitbox (some bosses are much larger than a standard Roblox character) moving through doorways, halls, and tight spaces without clipping or getting stuck. Always test geo at the largest boss's scale, not just default R15.
- **Verticality**: at least 2-3 meaningful elevation tiers (ground floor, mid platforms, rooftops/catwalks) connected by ramps, stairs, jump pads, or strafe-jump gaps — not just elevators.
- **Loop-friendly layout**: multiple paths that loop back into each other so Attackers can juke around the Boss rather than dead-ending.
- **Mix of open and tight spaces**: large-ish central arena/courtyard area for big fights, flanked by tighter rooms/alleys for breaking line of sight.
- **Spawn fairness**: distinct Attacker spawn zone(s) and Boss spawn point, positioned so the Boss doesn't have a free first hit and Attackers aren't instantly cornered.
- **Performance-conscious geometry**: avoid excessive unique meshes/parts; this is a fast-paced PvP shooter, not a walking sim — frame rate and server step time matter more than visual density.
- **No infinite-stall spots**: no single room/corner where an Attacker can be permanently safe from the Boss, and no spot where the Boss can wall off all approaches.

## 4. Inspirations — broad genre touchpoints

**Asymmetric "hunt the monster" PvP** (closest genre match):
- **Evolve** (Turtle Rock) — 4 hunters vs. 1 monster, arena/jungle-style maps with verticality and stalking routes. Closest direct analog to our Boss-vs-Attackers structure.
- **Dead by Daylight** (Behaviour) — 1 killer vs. 4 survivors, loop-heavy maps built around breaking chase lines with structures (the "loop" — a small structure survivors circle to lose the killer). Steal the *loop* concept directly.
- **Friday the 13th: The Game** — similarly asymmetric, cabin/woods maps with chokepoints and hiding routes.

**Movement-tech shooters** (for how terrain should reward strafing/bhopping):
- **Quake III Arena / Quake Live** — classic arena maps: ramps, jump pads, rocket-jump-friendly verticality, no flat floors.
- **Counter-Strike (Source/CS2)** — de_dust2, de_mirage: tight chokepoints connecting mid-sized open areas, extremely readable callouts/landmarks per area.
- **Titanfall 2** — wall-running and verticality married to readable, loop-y multiplayer maps; good reference for "big mech-scale character moving through human-scale architecture," which maps directly onto our Boss-in-a-normal-building scenario.
- **Apex Legends** — modern movement-shooter map design: rooftops, zip-lines-equivalents, mixed POI density.

**Roblox-specific references** (for scale/budget sanity, not necessarily design quality):
- Games like **Phighting!**, **Arsenal**, or **Bedwars** for examples of compact, readable, performant Roblox PvP arenas at a similar production scale to what we need.

## 5. Specific map archetypes we want

Pick from or riff on these — variety across the map rotation matters more than depth on any one:

1. **Industrial Facility** — warehouse/factory interior. Crates and machinery as cover, catwalks above, forklift-scale doorways the Boss can still fit through. (Evolve "Wraith Trap"-style verticality.)
2. **Urban Block** — a few connected buildings, alleys, and a rooftop layer. CS-style chokepoint streets connecting 2-3 open courtyards. Attackers can break vertical sightlines via rooftop hops.
3. **Overgrown Ruins / Temple** — outdoor arena with broken walls, pillars, and elevation changes via rubble ramps. Good testbed for bhop ramps and pillar-juking the Boss.
4. **Underground Complex** — tighter corridors and rooms (sewer/bunker/mine), high tension, short sightlines, good for melee-heavy or close-range bosses; needs extra care that the Boss isn't unstoppable in tight halls.
5. **Open Arena / Colosseum** — a circular or symmetric central pit ringed by elevated platforms — closest to a "pure" Quake arena map, good for a rotation map that's all about movement skill.

We are **not** looking for: open battle-royale-scale terrain, realistic large-scale cities, or puzzle/exploration-driven layouts. Every map should be playable start-to-finish as a single combat arena, roughly **comparable in footprint to a CS:GO map** (not MOBA-map scale, not battle-royale scale).

## 6. Deliverable expectations

- Greybox layout first for approval (blocky geometry, correct scale/proportions, marked spawn points) before any art pass.
- Test pass at Boss scale (we'll provide a placeholder oversized rig) to confirm no clipping/stuck spots.
- Final geometry should use `SpawnArea`-tagged parts for spawn zones and avoid blocking weapon raycasts unintentionally (flag any glass/thin geo that needs the `RayExclude` tag).
- Keep part count and unique meshes reasonable — we'll provide a budget per map once greybox is approved.
