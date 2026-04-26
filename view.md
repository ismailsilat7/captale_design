### Logical View

- `CapTaleSystem` is the top-level controller.
- `Cap` is the shared player state.
- `Lobby` is the hub that routes to scene modules.
- Each city module handles one gameplay domain.
- `MessageManager` provides shared notification support.
- `Timer` supports time-based behavior in messaging and Space Shooter.

### Development View

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

### Process View

- The system runs a single frame-based game loop.
- Each frame performs input handling, state updates, and rendering.
- `CapTaleSystem` dispatches behavior based on the current scene state.
- Scene modules may run their own internal update logic, timers, and collision checks.
- Raylib handles real-time keyboard, mouse, drawing, and audio operations.

### Physical View

- Execution environment is a Windows desktop machine.
- The game runs as a native C++ executable.
- Raylib provides the graphics, audio, and windowing layer.
- Assets are loaded from the local filesystem relative to the project folder.
- Save data is read from and written to `characterData.txt` in the project root.

### Scenarios

- Entering a city from the lobby.
- Playing Pong, Car City, Space Shooter, Earn City, ATM City, or Energy City.
- Managing tokens through room entry and ATM conversion.
- Managing energy through movement drain and Energy City item collection.
- Saving progress on exit and restoring progress on the next run.