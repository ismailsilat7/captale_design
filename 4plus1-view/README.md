# 4+1 View - CapTale

## Table of Contents

- [Overview](#overview)
- [Logical View](#logical-view)
- [Development View](#development-view)
- [Process View](#process-view)
- [Physical View](#physical-view)
- [Scenario View](#scenario-view)

## Overview

The 4+1 view of CapTale presents the system from five complementary perspectives: logical, development, process, physical, and scenario. Together, these views explain what the system is, how it is structured in code, how it behaves at runtime, how it is deployed, and how major user journeys work end to end.

CapTale is a city-based educational game centered on a shared player state, a lobby hub, and multiple city modules. A state-driven controller coordinates transitions between scenes while each module owns its own gameplay loop and rules.

## Logical View

The logical view focuses on the main domain objects and how they interact.

Reference diagram: [Class Diagram](../class-diagram/README.md)

- `CapTaleSystem` is the top-level controller.
- `Cap` is the shared player state.
- `Lobby` routes the player to scene modules.
- Each city module handles one gameplay domain.
- `MessageManager` provides shared notification support.
- `Timer` supports time-based behavior in messaging and Space Shooter.
- State transitions are centralized in `CapTaleSystem` to reduce coupling between city modules.

## Development View

The development view maps the architecture to source files and modules.

Reference diagram: [Class Diagram](../class-diagram/README.md)

- `main.cpp` contains the application shell and state machine.
- `headers/cap.h` contains the shared player object.
- `headers/lobby.h` contains lobby logic and room detection.
- `headers/message.h` contains the message subsystem.
- `headers/customCity.h` contains cap selection.
- `headers/pongCity.h` contains Pong gameplay.
- `headers/carCity.h` contains Car City gameplay.
- `headers/atmCity.h` contains ATM logic.
- `headers/earningCity.h` contains Earn City quiz logic.
- `headers/energyCity.h` contains Energy City logic.
- `headers/spaceShooter.h` and `headers/sprites.h` contain Space Shooter and its entity hierarchy.
- `headers/custom_timer.h` contains the reusable timer utility.
- `headers/settings.h` and `headers/spaceShooterSettings.h` define constants.

## Process View

The process view describes how the game runs at runtime.

Reference diagrams: [Activity Diagram](../activity-diagram/README.md) and [Sequence Diagram](../sequence-diagram/README.md)

- The system runs a single frame-based game loop.
- Each frame follows a pipeline of input handling, state update, collision or timer checks, then rendering.
- `CapTaleSystem` dispatches behavior based on the current scene state.
- Scene modules execute internal logic independently while following the shared frame contract.
- Timers are evaluated during updates to trigger delayed effects, cooldowns, and time-based events.
- Raylib handles real-time keyboard, mouse, drawing, and audio operations.

## Physical View

The physical view describes the runtime environment and storage setup.

Reference diagram: [Deployment Diagram](../deployment-diagram/README.md)

- Execution happens on a desktop or laptop machine.
- The game runs as a native C++ executable.
- Raylib provides graphics, audio, and windowing support.
- Assets are loaded from the local filesystem relative to the project folder.
- Save data is read from and written to `characterData.txt` in the project root.

## Scenario View

The scenario view captures representative end-to-end user journeys.

Reference diagram: [Use Case Diagram](../usecase-diagram/README.md)

- Entering a city from the lobby.
- Playing Pong, Car City, Space Shooter, Earn City, ATM City, or Energy City.
- Managing tokens through room entry and ATM conversion.
- Managing energy through movement drain and Energy City item collection.
- Saving progress on exit and restoring progress on the next run.

