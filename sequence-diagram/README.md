# Sequence Diagram - CapTale

## Table of Contents (Subdiagrams)

- [Enter City](#enter-city)
- [Energy City](#energy-city)
- [ATM City](#atm-city)
- [Earn City](#earn-city)
- [Space Shooter](#space-shooter)
- [Pong City](#pong-city)

The sequence diagrams of CapTale focus on runtime interaction flow between the player, `CapTaleSystem`, and city modules. They show how input is processed frame-by-frame, how states transition between Lobby and city scenes, and how shared systems such as `Cap` and `MessageManager` coordinate gameplay outcomes.

This project uses Lucidchart for sequence diagram design. You can view the diagram using the link below directly on Lucidchart:

[View the sequence diagram on Lucidchart](https://lucid.app/lucidchart/799498df-aa35-4534-bba3-077fed70ceca/edit?viewport_loc=-34539%2C-8469%2C43777%2C21535%2C0_0&invitationId=inv_4552f0dc-fa60-40eb-a3cc-17536c6f0704)

Alternatively, you can view or download the combined sequence-diagram canvas as a PDF or PNG:

- [Download Combined PDF](sequence-diagram.pdf)
- [Download Combined PNG](sequence-diagram.png)

The combined canvas is also broken down into separate sequence diagrams:

- [Enter City](enter-city.png)
- [Energy City](energy-city.png)
- [ATM City](atm-city.png)
- [Earn City](earn-city.png)
- [Space Shooter](space-shooter.png)
- [Pong City](pong-city.png)

## Diagram Descriptions

### Enter City

![Enter City](enter-city.png)

This sequence diagram details the player city entry flow in CapTale, tracing execution from raw input through `CapTaleSystem`'s update loop down to state transition. It covers how `Lobby` handles room detection via `checkContains()`, enforces token requirements for gated rooms (`PONG`, `CAR`, `SPACESHOOTER`) by either deducting tokens or surfacing a denial message through `MessageManager`, and allows direct entry into open-access rooms (`ATM`, `EARN`, `ENERGY`, `EAT`). On successful entry, `CapTaleSystem` updates its state to the corresponding city enum and hands off execution to the relevant city module on the next frame.

### Energy City

![Energy City](energy-city.png)

This sequence diagram illustrates the Energy City gameplay flow in CapTale, showing how the player restores the shared Cap energy meter through item collection. After the player enters Energy City from the Lobby, control shifts to the `EnergyCity` scene, where the main update loop continuously runs each frame. Within this loop, the player moves the basket horizontally to catch falling objects while `EnergyCity` manages spawning and movement of each item. When a collision between the basket and an item is detected, the system determines the item type: collecting a Fruit calls `Cap.increaseEnergy(2)`, while collecting a Cap item grants larger recovery through `Cap.increaseEnergy(10)`. After each successful collection, the updated energy value is reflected in the on-screen energy bar rendered to the player. When the player presses `L`, `EnergyCity` ends the scene and returns control to the Lobby.

### ATM City

![ATM City](atm-city.png)

This sequence diagram represents the ATM City token conversion flow in CapTale, showing how the player exchanges earned cash for usable game tokens. When the player enters ATM City from the Lobby, the active scene changes to the `ATMCity` module. Inside this scene, pressing `W` initiates the withdrawal process, prompting `ATMCity` to read the player’s current cash balance from `Cap`. The system then converts available cash into tokens using the fixed conversion formula $\text{cash} \div 50$, adds the resulting tokens to the player’s token balance, and resets the stored cash value to zero after the transaction completes. Once conversion succeeds, `ATMCity` sends a notification to `MessageManager`, which displays a message showing the amount converted and the player’s updated token total. When the player presses `L`, the ATM interaction ends and control returns to the Lobby.

### Earn City

![Earn City](earn-city.png)

This sequence diagram describes the Earn City quiz flow in CapTale, where the player answers questions to increase or decrease in-game cash balance. After the player enters Earn City from the Lobby, control shifts to the `EarnCity` module, where the quiz cycle continues until the player leaves. By pressing `E`, the player starts or continues the quiz, causing `EarnCity` to load a random question and display the prompt with multiple-choice options. The player then submits an answer using `A`, `B`, `C`, `D`, or chooses Skip. If the selected answer is correct, `EarnCity` rewards the player through `Cap.addCash(reward)`, followed by confirmation of the earned amount. If the answer is incorrect, the system applies a penalty through `Cap.removeCash()`, deducting either the defined penalty or remaining available cash, then displays the loss. If the player skips, `EarnCity` immediately loads the next question without modifying cash. Pressing `L` exits the quiz and returns control to the Lobby, preserving updated cash for later use.

### Space Shooter

![Space Shooter](space-shooter.png)

This sequence diagram shows the Space Shooter flow in CapTale from entering the city to returning to the Lobby. When the player enters the Space Shooter room, `CapTaleSystem` changes the game state to `SPACE_CITY` and begins calling `SpaceShooter.update()` each frame. Before the game starts, the player selects a difficulty by pressing `1`, `2`, or `3`, then confirms with `RIGHT_SHIFT`, which configures game settings. During gameplay, the player moves the ship and fires while `SpaceShooter` updates lasers, meteors, and power-ups, then checks collisions. If the player presses `L`, or the game sets `returnToLobby` after game over, `CapTaleSystem` calls `SpaceShooter.restart()` and switches state back to the Lobby.

### Pong City

![Pong City](pong-city.png)

This sequence diagram outlines the Pong City flow in CapTale from entry to exit. When the player enters the Pong room, `CapTaleSystem` changes game state to `PONG_CITY` and begins calling `PongCity.update()` each frame. The player first chooses whether to play against AI or another player, then selects a difficulty before the game starts. During gameplay, paddles and ball are updated continuously while `PongCity` checks collisions and updates scores. If the game is paused, the player can resume or restart. After a win or loss, the player may replay or return to the menu. Pressing `L` at any time exits the minigame and returns the player to the Lobby.

