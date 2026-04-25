# Use Case Diagram - CapTale

The use case diagrams of CapTale describe player-facing interactions across the lobby, resource cities, and paid game cities. They capture entry conditions, normal interaction paths, alternate actions, blocked-entry scenarios, and end states after each interaction.

This project uses Lucidchart for use case diagram design. You can view the diagram using the link below directly on Lucidchart:

[View the use case diagram on Lucidchart](https://lucid.app/lucidchart/f713de3b-f2ec-4b79-8156-c22b93847dd1/edit?view_items=NChR3ZelhBGz&page=.Q4MUjXso07N&invitationId=inv_0ad2c2dd-28f2-4fad-9ce5-a383bace50c0)

You can also view the separated use case diagram images:

- [Lobby Module](lobby.png)
- [Resource City Module](resource-city.png)
- [Game City Module](game-city.png)

## Use Case Descriptions

### Lobby Module

**Name:** Lobby Navigation and City Entry  
**Brief Description:** Player moves in the lobby, selects a destination, and enters an allowed city.  
**Actor(s):** Player  
**Preconditions:** Game is running; player is in `LOBBY` state.

**Basic Flow:**

1. Player navigates the lobby.
2. System detects current room overlap.
3. Player presses Enter to confirm entry.
4. System validates entry conditions.
5. System switches to the selected module/state.

**Alternate Flow:**

1. Player opens Manual from lobby icon/menu.
2. System switches to `GAME_MANUAL`.

**Exception Flow:**

1. Entry is token-gated and player lacks tokens.
2. System shows blocked-entry message and remains in lobby.

**Post Conditions:** Player is either in the selected module or still in lobby with feedback shown.

### Resource City Module

**Name:** Enter and Use Resource City  
**Brief Description:** Player enters ATM/Earn/Energy city to restore energy, earn cash, or convert cash to tokens.  
**Actor(s):** Player  
**Preconditions:** Player is in lobby and enters a resource room.

**Basic Flow:**

1. Player enters a resource city.
2. System switches to selected resource module.
3. Module executes city-specific loop:
	- Energy City: catch items to increase energy.
	- Earn City: answer quiz to gain/lose cash.
	- ATM City: convert cash to tokens and reset cash.
4. Player returns to lobby.

**Alternate Flow:**

1. In Earn City, player skips question.
2. System loads next question with no cash change.

**Exception Flow:**

1. Incorrect answer or penalty event occurs.
2. System applies penalty but does not allow negative cash.

**Post Conditions:** Player resources (energy/cash/tokens) are updated and bounded; state returns to lobby on exit.

### Game City Module

**Name:** Enter and Play Paid Game City  
**Brief Description:** Player enters Pong/Car/Space Shooter, plays the city loop, and can pause/restart/return.  
**Actor(s):** Player  
**Preconditions:** Player is in lobby and targets a paid game room.

**Basic Flow:**

1. Player confirms entry to a paid city.
2. System checks and deducts required tokens.
3. System switches state to selected game city.
4. Game loop runs (input, update, collisions, render).
5. Player exits with return control (for example, `L`), and system returns to lobby.

**Alternate Flow:**

1. Player pauses or restarts according to city rules.
2. Module resumes gameplay or restarts round/session.

**Exception Flow:**

1. Token check fails.
2. Entry is blocked and warning is displayed.

**Post Conditions:** Tokens are updated if entry succeeds; state returns to lobby on exit; game progress is updated.

