# Activity Diagram - CapTale

## Table of Contents (Subdiagrams)

- [Main Game Loop](#main-game-loop)
- [City Entry and Lobby](#city-entry-and-lobby)
- [Car Game](#car-game)
- [Pong Game](#pong-game)
- [Space Shooter Game](#space-shooter-game)

The activity diagrams of CapTale describe control flow across the game lifecycle, lobby navigation, and city gameplay modules. They highlight decision points, parallel frame operations, state transitions, and exit paths that define how the game progresses from initialization to shutdown.

This project uses Lucidchart for activity diagram design. You can view the diagram using the link below directly on Lucidchart:

[View the activity diagram on Lucidchart](https://lucid.app/lucidchart/c274b7fe-3fd4-420e-9830-b75c31624aa7/edit?viewport_loc=-7110%2C2946%2C16013%2C7877%2C0_0&invitationId=inv_4c82e0a8-76a8-40da-848f-4e7475dc2866)

Alternatively, you can view or download the combined activity-diagram canvas as a PDF or PNG:

- [Download Combined PDF](Activity%20Diagrams%20-%20CapTale.pdf)
- [Download Combined PNG](Activity%20Diagrams%20-%20CapTale.png)

The combined canvas is also broken down into separate activity diagrams:

- [Main Game Loop](main-game-loop.png)
- [City Entry and Lobby](cityentry-and-lobby.png)
- [Car Game](car-game.png)
- [Pong Game](pong-game.png)
- [Space Shooter Game](spaceshooter-game.png)

## Diagram Descriptions

### Main Game Loop

![Main Game Loop](main-game-loop.png)

The Main Game Loop kicks off by initializing the window and system before entering a continuous frame cycle. Within each loop, the state logic simultaneously processes input and updates state, while the display system renders messages and visual assets in parallel. After these concurrent operations, the system checks for a game-over condition. If the game is still active, it returns to the frame start; if finished, it performs final cleanup by saving data, unloading textures, and closing the window to conclude the lifecycle.

### City Entry and Lobby

![City Entry and Lobby](cityentry-and-lobby.png)

The process begins in the Lobby state where players navigate into interactive rooms and press Enter to initiate entry. The Lobby system then evaluates token requirements; if tokens are needed but unavailable, `CapTaleSystem` displays a warning message. Successful validation leads to token deduction and a transition to the selected scene, where the city update and draw loop runs continuously. At any point, the player can press `L` to exit the city, which triggers a return to the `LOBBY` state and concludes the session.

### Car Game

![Car Game](car-game.png)

This activity diagram shows the Car City gameplay loop in CapTale. After initializing the car and level assets, `CarCity` enters a continuous frame loop where the player steers the car while obstacles, coins, and power-ups are updated. During each frame, the system checks collisions: hitting an obstacle can either trigger a second-life pause or set the game to over, while collecting coins increases score and power-ups apply temporary effects such as slowing traffic or spawning extra coins. The game also updates score and difficulty as time passes. If a game-over state occurs, the player can press `R` to reset the game, restore entities, and begin the loop again.

### Pong Game

![Pong Game](pong-game.png)

The Pong game begins with the player selecting a mode and level, initiating a gameplay loop that concurrently updates paddles, ball movement, and collisions. The `PongCity` state machine handles scoring and monitors for pause via the `P` key, allowing the player to resume, restart, or return to the menu. If a win/lose target is reached, the system displays a summary screen where the player can choose Replay or Exit. If the target is not met and the game remains unpaused, the loop cycles back to maintain continuous play until a final result is achieved.

### Space Shooter Game

![Space Shooter Game](spaceshooter-game.png)

The `SpaceShooter` sequence begins with the player selecting a mode and confirming via `RIGHT_SHIFT`, triggering initialization of timers and flags. The core gameplay loop runs concurrent processes for audio, movement, shooting, and entity updates before checking collisions or time limits. If no game-over condition is met, the player can continue or manually exit by pressing `L`. If the game ends, a summary screen appears, and pressing `L` sets `returnToLobby` to true, terminating the minigame and returning the player to the Lobby.

