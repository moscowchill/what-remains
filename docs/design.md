# What Remains: design brief

Status: proposed direction. This repository currently contains documentation, with no game runtime or verified gameplay.

## The game we want to make

A first-person survival game set in a vast, realistically rendered procedural city after a zombie outbreak. The player builds a base, searches abandoned places, fights or avoids infected, and competes with other survivors for scarce local supplies. Unreal Engine is the selected engine.

The full game should support multiple settlements competing for the city's resources. AI survivors will populate that competition first. Human players and their settlements can join this same kind of struggle in a later multiplayer version.

A world seed generates more districts as the player explores, aiming for the feeling of a world that keeps going. Assemble city layouts from designed streets, buildings, interiors, and landmarks. District character and landmark placement should make exploration varied and navigable. Technical travel limits will be measured as the generator develops.

Resources remain finite at each location. Exploring farther can uncover fresh supplies; travel time, carrying capacity, and danger should make nearby contested resources and rival stockpiles valuable. Returning to a district preserves its depleted supplies and the player's construction.

The world, characters, locations, and story will be original. Survival fiction and games can inform the atmosphere; this project does not adopt characters, settings, or specific lore from D. J. Molles or Fallout.

## First playable: one contested city district

Build an offline solo version in one small generated urban district spanning several adjacent map sections. Include a player shelter, several accessible scavenging locations, infected, rival AI scavengers, and one defended survivor outpost with a stockpile. Use fixed test seeds while developing the generator.

Rival survivors are part of the first playable. They should collect actual supplies from the same finite containers available to the player and carry those supplies home. Raiding their stockpile gives the player another way to obtain resources that rivals have collected.

Use placeholder geometry and clearly licensed assets while this interaction takes shape. The district should demonstrate useful urban spaces: streets, interiors, narrow approaches, and routes between the shelter, supply sites, and outpost. Its streets and AI routes must connect across generated section boundaries. The larger procedural city remains the intended world.

A supply run should take roughly 10-15 minutes:

1. Check the base stash and choose which supplies to seek.
2. Leave with limited ammunition and carrying capacity.
3. Search buildings while rival scavengers pursue the same resources.
4. Fight or avoid infected and decide whether to confront the survivors.
5. Loot an accessible supply site or raid the defended outpost stockpile.
6. Return home, store supplies, and spend materials on a barricade.
7. Save and resume with the district's depleted supplies and changed bases intact.

## Mechanics needed for that loop

| Area | First playable behavior |
| --- | --- |
| World generation | A seed creates connected map sections with a reachable shelter, supplies, and rival outpost. |
| Movement | First-person walking, sprinting, looking, and interaction with reliable collision. |
| Combat | One firearm, finite ammunition, reload, hit feedback, health, and a simple death rule. |
| Infected | One type that sees and hears survivors, pursues, attacks, and can die. |
| Rival survivors | Local AI that travels to supplies, takes items, returns to its outpost, and fights nearby threats. |
| Outpost | One rival group, a defended location, and a stockpile that holds real collected supplies. |
| Inventory | Ammunition, medical supplies, and building materials with limited carrying capacity. |
| Ownership | Every supply stack is in one container, inventory, or world pickup at a time. |
| Base building | Place, damage, repair, and remove one snapped barricade type at designated entrances. |
| Persistence | Save player and rival inventories, stockpiles, depleted containers, deaths, and placed barricades. |

Gunfire should create a tradeoff: clearing an immediate threat can alert infected or rival survivors. Tune hearing range, ammunition supply, and actor counts through playtests.

Player and AI survivors use the same rules for taking supplies, carrying items, spending ammunition, and receiving damage. Keep the first resource model finite and understandable. Supplies move between locations; a completed scavenging task must not create an extra reward copy.

Test both infected and armed survivors around doors and barricades. Infected need a reachable attack position against a blocking barricade. Survivors need a valid route or combat response when an entrance is blocked.

For the first playable, propose respawning at the shelter with carried supplies left in one recoverable container. Test whether this creates enough tension. Death must transfer each item exactly once.

## Offline supply-run acceptance

The first milestone is complete when these checks can be demonstrated in the same playable build:

- The player leaves the shelter, scavenges a building, and returns with useful supplies.
- A rival scavenger takes finite items from a supply site, returns, and deposits them in its outpost stockpile.
- The player and an AI trying to take the same final item cannot duplicate it or create a negative count.
- Firing spends ammunition and alerts a nearby infected or survivor; damage and death resolve consistently.
- Infected can threaten both the player and rival survivors in the test area.
- The player can raid the defended stockpile and carry its contents back to their base.
- Building and repairing a barricade spend the required materials exactly once.
- Infected and human AI navigate the test area and respond to a blocked entrance without walking through it.
- Death creates one recoverable inventory, with no duplicate items after saving and reloading.
- A save and restart preserve depleted containers, rival carried supplies, both stockpiles, deaths, and barricades.
- Unloading and reloading a district region preserves its changed resources and occupants.
- The same seed and generation versions produce the same base layout when neighboring sections load in different orders.
- The player and AI cross generated boundaries with connected streets, collision, and navigation.
- Several fixed seeds produce reachable supplies and an outpost; repeated travel keeps active content within a measured budget.

Record hardware, engine version, loaded area, active survivor and infected counts, and frame times. Set a performance target once the intended hardware is known.

## Order of work

1. Establish the Unreal project and a small seeded urban layout. Prove connected sections, stable object identities, and basic save-and-revisit behavior before expanding the generator.
2. Implement shared inventory and interaction rules; prove that an AI scavenger competes for supplies and brings them home.
3. Add first-person combat, infected, and basic survivor combat around the supply route.
4. Add stockpile raiding and the barricade, including navigation and attack behavior.
5. Complete persistent world changes, recovery checks, and the full offline supply run.
6. Improve atmosphere and measured performance, then grow the building kit and district variety while testing longer exploration.

Multiplayer follows a proven solo version. More settlements, broader city simulation, vehicles, elaborate crafting, and external AI services should follow evidence from the playable district. Local survivor AI is required now; distant simulation and language-model-driven residents can come later.

## Decisions still needed

- What city setting, district types, and landmark styles should give the generated world its identity?
- Should infected create slow pressure, fast pursuit, or a mix?
- How aggressive and capable should rival survivors be in the first district?
- How demanding should survival be, and how much progress should death put at risk?
- Which development hardware, player hardware, and desktop platform should the first build support?
- What eventual human population and number of competing settlements should multiplayer target?
