# Development setup

## Current status

The repository contains the project foundation. An Unreal project, build scripts, playable content, and automated gameplay checks will be added during the first implementation milestone.

Development began from a WSL workspace. The suggested first editor target is native Windows. Linux support can be qualified after the first Windows build works. These are initial development choices, not promised release platforms.

## Prerequisites for the first implementation

1. Install a stable Unreal Engine 5 release through Epic's official distribution. Record its full version when creating the project and use that version across contributors.
2. Install the C++ development tools required by that engine release. Follow [Epic's Visual Studio setup instructions](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine).
3. Check the development machine against [Epic's hardware requirements](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-and-software-specifications-for-unreal-engine). Record the GPU, RAM, resolution, and graphics settings used for performance measurements.
4. Install Git and Git LFS. Run `git lfs install` in the development checkout before adding or fetching Unreal assets.
5. For a Windows editor, keep its working checkout on a Windows drive. Use Git to share changes with a separate WSL checkout when needed.

The `.gitattributes` file already marks Unreal assets and common binary art formats for Git LFS. No binary assets are included yet. Git LFS must be working before those files are committed.

Engine installation requires the contributor's Epic account and license agreement. The repository does not distribute the engine.

## First implementation task

Create a C++ project named `WhatRemains` in the repository root. Prefer a minimal project with project-owned placeholder geometry, then add a first-person character and an urban test space. Keep the initial code module small.

Record the exact engine and compiler versions here. Add project-specific build and launch commands once they have been run successfully.

Completion criteria:

- A fresh checkout opens and compiles with the documented tools.
- The player can move around the test space and interact with a supply container.
- One AI scavenger can navigate to that container, take supplies, and return them to its stockpile.
- The player and scavenger use the same item-transfer rules; competing for the last item cannot duplicate it.
- A packaged development build launches on the development machine.
- The README documents controls and identifies the tests actually performed.

The first implementation is offline. Keep gameplay rules independent of the local player's input and UI, so human and AI controllers act through the same simulation. Future multiplayer will need replication, connection handling, identity, and network testing. Choose friend-hosted or dedicated-server operation when that milestone begins.

## Validation as features arrive

Test inventory transfers, placement, damage, saving, and loading with the player and AI scavengers. Include a case where both try to collect the same item. Verify that raided stockpiles remain depleted after loading. Add automated checks for rules that can lose or duplicate progress or resources.

Measure frame time and simulation time in the test district as infected and survivor counts rise. Record the hardware and test scenario. Set performance budgets from those results before expanding the map. Test persistence across streamed districts when streaming is introduced.

Useful references: [networking overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine) and [World Partition](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition-in-unreal-engine).
