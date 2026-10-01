# What Remains: architecture direction

Status: proposed implementation boundaries. No Unreal project, AI implementation, save system, networking implementation, or gameplay tests exist yet.

## Engine and project structure

Use Unreal Engine. Pin one engine release and its supported compiler before creating the project, then document how contributors install and build it. Verify a packaged build when changing engine versions.

Use C++ for gameplay rules, inventories, resource transfers, combat, building validation, and persistence. Use Blueprints for content composition, presentation, animation hooks, and designer tuning. Store item and building definitions as data assets with stable keys.

Start with one gameplay module and a small number of components, using Unreal's movement, collision, navigation, and AI facilities. Add modules or plugins when implementation establishes a useful boundary.

## One authority for an offline world

The first playable is offline solo. A central authoritative simulation in the local process owns health, ammunition, containers, carried supplies, stockpiles, placed structures, and persistent changes. UI, player input, and AI controllers request actions through its gameplay interfaces.

Separate control decisions from character capabilities. Human-controlled and AI-controlled survivors use the same validated operations for taking supplies, depositing items, firing, receiving damage, and interacting with structures.

Validate the acting character, distance, current state, interaction rules, and available resources. Building placement also checks collision and supported attachment points. Keep these rules independent of a local camera or player UI.

Make resource transfers and building costs single authoritative transactions. Every item stack has one location and quantity. Failed placement leaves materials intact, competing attempts to take the last item resolve once, and repeated requests cannot spend or grant resources twice.

Give characters a settlement affiliation and give stockpiles a settlement owner. Define ordinary transfers and hostile looting as validated actions with explicit access rules. Successful raids move existing inventory into the raider's possession.

## Rival survivors and infected

Local survivor AI is required in the first playable. Begin with a small behavior tree or state machine: choose a supply site, travel, collect what is available, return, and deposit. Add a basic response to perceived threats and a guard behavior for the outpost.

Scavengers and guards use finite inventories, ammunition, health, and the same resource rules as the player. AI plans may become invalid when someone empties a container or blocks a route; recheck conditions when an action executes and choose another valid action when it fails.

Infected use local sight, hearing, pursuit, attack, and death behavior. They can target the player and rival survivors. Validate navigation, line of sight, and attack positions around doors and barricades for both enemy types.

No language-model backend is required. A future service might suggest dialogue or bounded goals behind an optional adapter; it would still use validated gameplay actions and need request limits, timeouts, cost limits, and a local fallback.

## A district that can grow into a city

The full map target is a large city. Begin with one dense authored district and plan the map around [World Partition](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition-in-unreal-engine), confirming setup against the pinned engine version before substantial content work.

Streaming controls loaded regions and actors. The save system owns persistent gameplay state. Loading an actor applies its stored inventory, health, affiliation, position, and other relevant changes; removed objects must remain removed.

Give regions and authored persistent objects stable identifiers. Generate identifiers for newly created structures and pickups. References must survive actor unloading and changes in load order.

Keep the initial scavenging routes and outpost within the playable district. Budget active AI, navigation work, loaded content, and update frequency. Measure loaded-region and actor costs before introducing complicated distant simulation.

Outside loaded regions, preserve world records without running full character simulation. The first prototype may pause those actors explicitly. Save their carried resources and state before unloading so returning does not reset the competition.

Approximate offscreen scavenging or settlement activity can follow a proven district. Any later approximation must preserve resource ownership and reconcile with loaded actors. The initial prototype does not promise a continuously simulated whole city.

## Persistence and recovery

Use a versioned save format with a world identifier, content version, player record, settlement records, and stable identifiers for persistent objects. Store inventories, stockpiles, barricades, looted containers, survivor state, and changes to infected spawns.

Store definition keys and gameplay data rather than raw object pointers. Capture both loaded actors and persistent records for unloaded regions so a save includes the city's changed state.

Maintain one writer per world. Capture a consistent snapshot at a gameplay transaction boundary so transfers between a scavenger and stockpile cannot be saved halfway through. Write the snapshot away from the gameplay loop where practical.

Write to a temporary file in the same directory, check serialization and file writes, then use the target platform's supported atomic replacement procedure. Keep at least one known-good backup and test interrupted writes and corrupt files.

Validate format and content versions before applying a save. Unsupported versions leave existing saves intact. Add explicit migrations when the schema changes and preserve a backup before migration.

Define autosave timing, shutdown saves, death inventory transfers, and recovery behavior in the first persistence milestone. Restarting or streaming a region must not refill containers, duplicate carried supplies, or revive recorded dead actors.

## Multiplayer later

Future human players should enter the same competition for resources, potentially operating separate settlements. Preserve the boundaries between action requests, authoritative state, controller decisions, and presentation to support that work.

Networking remains a later implementation: move authoritative ownership to a server, validate remote requests, replicate state, and design prediction, session identity, joining, reconnecting, and save ownership. These boundaries reduce coupling but do not guarantee a conversion without significant changes and testing.

Choose hosting, authentication, population targets, and settlement permissions before that milestone. Players spread across the city will increase simulation and streaming demands and require new performance measurements.

## Content and licensing

Keep project source, redistributable assets, and optional restricted assets identified. Record provenance and license terms in the asset manifest before importing content. A fresh clone should eventually run with the public asset set and placeholders for optional restricted assets.

The code license does not automatically cover third-party art, audio, fonts, or engine content. Keep Unreal Engine source and installed binaries outside the public repository; contributors obtain the engine under [Epic's terms](https://www.unrealengine.com/eula/unreal). Select version-control handling for large assets before importing them.

## Planned verification gates

- Package and launch a clean checkout with the documented engine and toolchain.
- Complete the offline supply run, including an AI scavenger collecting and depositing finite supplies.
- Race the player and AI for the last item; check repeated transfers, failed placement, and death for duplication.
- Exercise infected and human combat, navigation, line of sight, and blocked entrances around the barricade.
- Raid the outpost and verify that the stockpile loses exactly what the player takes.
- Restart from a save and compare inventories, stockpiles, cleared objects, survivor state, and barricades.
- Unload and reload a region and verify that its changed state and carried supplies persist.
- Test interrupted saves, corrupt latest saves, backup recovery, and unsupported save versions.
- Profile the district with recorded hardware, loaded regions, and active survivor and infected counts.

These checks are planned. Record results with the implementation that runs them.
