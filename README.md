# What Remains

A first-person survival game about scavenging a ruined city, competing for supplies, surviving infected, and building a place worth returning to.

The goal is a large open city with multiple settlements competing for limited resources. Start with an offline game against AI scavengers and hostile survivors. Later, human players can inhabit and compete through settlements in the same world. The visual direction is grounded and realistic, using Unreal Engine.

**Status: project foundation.** This repository currently contains the design, technical direction, and contribution setup. There is no playable build or Unreal project yet. Features below are planned.

## The first playable milestone

A player establishes a shelter in one dense city district, searches buildings, encounters infected and rival scavengers, raids an AI group's supplies, and brings materials home to build a barricade. AI scavengers collect from the same finite supplies and carry them back to their own stockpile.

Saving and loading preserves the player's progress, depleted containers, rival supplies, and construction. This district is the first part of the larger city. It proves the core systems before we build more districts.

| Area | Initial scope |
| --- | --- |
| World | One dense urban district, a player shelter, scavenging sites, and one hostile outpost |
| Combat | First-person movement, one firearm, reloading, damage, and one infected type |
| Infected | Sight and hearing, pursuit, attack, and a response to blocked paths |
| Rivals | AI survivors that scavenge, carry resources home, defend supplies, and fight |
| Scavenging | Ammunition, medical supplies, building materials, and limited container contents |
| Building | One useful barricade type with placement rules, damage, and repair |
| Persistence | Player state, finite resource ownership, containers, rival stockpiles, and construction |
| Multiplayer | A later milestone introduces human-controlled survivors and competing settlements |

## Technical direction

- Unreal Engine 5, with an exact stable version recorded when the first project is created and built.
- C++ for core gameplay rules and persistence; Blueprints for scene composition, presentation, and tuning.
- A central simulation owns combat, item transfers, construction, and saves from the first offline prototype. Future multiplayer will place that authority on a server.
- World Partition for world streaming as the environment grows, with persistent gameplay state managed separately.
- Local game AI for infected and rival survivors. Future language-model integrations can propose goals or dialogue through a bounded interface.

The architecture is a starting proposal. We will refine it through small, playable changes and measured performance.

## Start here

- [Game design and the first milestone](docs/design.md)
- [Technical foundations](docs/architecture.md)
- [Development setup](docs/development.md)
- [Contributing](CONTRIBUTING.md)
- [Asset sources and licensing](ASSETS.md)

The first implementation task is to create the Unreal C++ project, a first-person character, and an AI scavenger that competes with the player for one supply container. See the setup document for prerequisites and completion criteria.

## Open source

Original project code and documentation use the [MIT license](LICENSE). Unreal Engine is proprietary software with source access under [Epic's license](https://www.unrealengine.com/eula/unreal). Contributors obtain Unreal separately.

Third-party code and assets retain their own licenses. Every shared asset must have recorded permission to redistribute its source files. The repository begins with no third-party game assets.

Repository: [moscowchill/what-remains](https://github.com/moscowchill/what-remains).
