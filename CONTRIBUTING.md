# Contributing to What Remains

This project is at the design and setup stage. Read the [first playable milestone](docs/design.md) before proposing work. The most useful early contributions help make that milestone playable and easy to build.

## Small, reviewable changes

1. Describe the player-visible problem or intended behavior.
2. Keep the change focused on one part of the current milestone.
3. Explain how to reproduce and verify it, including the engine version used.
4. For gameplay changes, test the player and any AI actor using the same system. Record any checks you could not run. Once multiplayer exists, include host and remote-client tests.
5. Include screenshots or a short recording when movement, layout, UI, or animation changes.

Until a runnable project exists, documentation reviews and help validating the development setup are useful contributions. Feature proposals should explain how they improve scavenging, competition for resources, survival, or building in the first district.

## Code and content

- Put core rules in C++ and expose useful tuning controls to Blueprints.
- Keep item and construction definitions separate from their runtime state.
- Give persisted objects stable identifiers and version changes to save data.
- For generation changes, record world seeds and generator versions. Check neighboring sections in different load orders, navigation across their boundaries, and saved changes after a revisit.
- Use Git LFS for Unreal assets and large binary source files. Install and initialize it before adding those files.
- Record asset origin, license, source redistribution rights, and attribution in [ASSETS.md](ASSETS.md).
- Coordinate edits to binary assets to reduce conflicts. Keep changes to unrelated maps and assets out of a contribution.
- Keep credentials, personal save files, generated build output, and local editor settings outside Git.

Contributions to original project code and documentation use MIT, matching the repository. Third-party material keeps its own stated terms. A contribution should identify any material with different licensing.

## AI-assisted contributions

AI assistance is welcome. Contributors remain responsible for understanding the change, checking its sources, and testing its behavior. State what was actually built and played. For generated assets, record the tool and applicable license with the asset entry.

## Writing

Use clear language and concrete behavior descriptions. Use ASCII punctuation in place of Unicode em dashes. Describe planned features as planned until a playable implementation exists.
