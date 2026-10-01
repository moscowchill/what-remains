# Working on What Remains

Read README.md, docs/design.md, and docs/architecture.md before changing gameplay or project structure. Also read docs/world-generation.md before changing generation, streaming, or persistence.

## Project direction

- Unreal Engine, grounded realistic visuals, and an extensive procedurally generated city with first-person scavenging, infected, construction, and competing settlements.
- Use a world seed, stable generated identities, connected map sections, and persistent changes. Establish supported traversal limits through testing.
- Build offline play against AI scavengers and hostile survivors first. Human multiplayer comes later. AI survivors and players use the same validated gameplay actions.
- Keep work tied to a small playable milestone. Record proposals separately from implemented behavior.

## Engineering

- Inspect Git status and preserve unrelated work.
- Use the documented engine version. Record compiler and runtime validation honestly.
- Keep gameplay state under one simulation authority, including offline. Test competition between player and AI actions. Future multiplayer puts that authority on the server and adds host and remote-client tests.
- Persist stable object identities and use versioned save data.
- Record generator and content-kit versions with each world. Generation order must not change base layouts or reset saved changes.
- Keep new services and dependencies proportional to a demonstrated need.
- Read ASSETS.md before adding external content. Keep asset source and license records complete.
- Use Git LFS for binary assets as configured in .gitattributes.
- Keep credentials, engine files, build output, and private saves outside the repository.

## Communication

- State what changed and how it was verified.
- A source review or static check does not establish a successful Unreal build or playtest.
- Never write Unicode em dashes. Scan new and edited text before finalizing.
