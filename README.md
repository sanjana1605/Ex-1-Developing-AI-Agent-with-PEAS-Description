# Ex-1-Developing-AI-Agent-with-PEAS-Description

**Name:** Sanjana Sri N

**Register Number:** 2305003007

## Aim:

To find the PEAS description for the given AI problem and develop an AI agent.

## Theory :

PEAS stands for:
```
P-Performance measure

E-Environment

A-Actuators

S-Sensors
```

It’s a framework used to define the task environment for an AI agent clearly.


## Pick an AI Problem


**1.** Self-driving car

**2.** Chess playing agent

**3.** Vacuum cleaning robot

**4.** Email spam filter

**5.** Personal assistant (like Siri or Alexa)

## Developing AI Agent with PEAS Description – Chess Agent

### Agent: Chess Playing Agent (Statement-based, turn-by-turn)

**Performance Measure:**

Maximizes chances of winning the game (capturing opponent King).

Minimizes number of moves to checkmate.

Plays valid moves according to chess rules (simplified for demonstration).

Ensures turn-taking between White and Black.

**Environment:**

Simplified chess environment (statement-based).

Two-player turn-based game (White vs Black).

No physical board; moves represented as statements (e.g., “White plays e2 → e4”).

Fully observable in terms of last move and current turn.

**Actuators:**

Executes a move for the current player (updates last move and game state).

Switches turn to the other player.

Updates the “King alive” status if a capture occurs.

**Sensors:**

Checks whose turn it is (White or Black).

Observes previous moves executed.

Detects if either King has been captured.

## Algorithm:

**Step 1:** Initialize the game by setting White to play first, both Kings alive, and move counter to zero.

**Step 2:** Define the possible moves for White and Black pieces.

**Step 3:** Repeat the following steps until one King is captured:

3.1. Check whose turn it is.

3.2. If White’s turn, select a move from White’s possible moves.

3.3. If Black’s turn, select a move from Black’s possible moves.

3.4. Record the move as the last move executed.

3.5. Increment the move counter by one.

3.6. If enough moves have been played, randomly check if the opponent’s King is captured and update status.

3.7. If both Kings are alive, switch the turn to the other player.

3.8. Optionally, display the last move and the next turn.

**Step 4:** Stop the game when one King is captured.

**Step 5:** Declare the winner based on which King is still alive.

**Step 6:** Optionally, print a summary of total moves and the sequence of moves played.

### Example Program:
```
class VacuumCleanerAgent:
    def __init__(self):
        # Initialize the agent's state (location and dirt status)
        self.location = "A"  # Initial location (can be "A" or "B")
        self.dirt_status = {"A": False, "B": False}  # Initial dirt status (False means no dirt)

    def move_left(self):
        # Move the agent to the left if possible
        if self.location == "B":
            self.location = "A"

    def move_right(self):
        # Move the agent to the right if possible
        if self.location == "A":
            self.location = "B"

    def suck_dirt(self):
        # Suck dirt in the current location if there is dirt
        if self.dirt_status[self.location]:
            self.dirt_status[self.location] = False
            print(f"Sucked dirt in location {self.location}")

    def do_nothing(self):
        # Do nothing
        pass

    def perform_action(self, action):
        # Perform the specified action
        if action == "left":
            self.move_left()
        elif action == "right":
            self.move_right()
        elif action == "suck":
            self.suck_dirt()
        elif action == "nothing":
            self.do_nothing()
        else:
            print("Invalid action")

    def print_status(self):
        # Print the current status of the agent
        print(f"Location: {self.location}, Dirt Status: {self.dirt_status}")
```

### Example usage:

```
agent = VacuumCleanerAgent()
```

### Move the agent, suck dirt, and do nothing

```
agent.perform_action("left")
agent.print_status()
agent.perform_action("suck")
agent.print_status()
agent.perform_action("nothing")
agent.print_status()
```

### Sample Output:

<img width="570" height="77" alt="image" src="https://github.com/user-attachments/assets/70bf8483-1b65-46d6-ab8b-eeda6d591f36" />


## Program:

```
import random

class ChessAgent:
    def __init__(self):
        self.turn = "White"
        self.last_move = None
        self.moves_white = ["e2 → e4", "d2 → d4", "g1 → f3", "c2 → c4", "f1 → c4"]
        self.moves_black = ["e7 → e5", "d7 → d5", "g8 → f6", "c7 → c5", "f8 → c5"]
        self.white_king_alive = True
        self.black_king_alive = True
        self.move_count = 0

    def perform_action(self, action):
        if action == "play":
            if self.turn == "White":
                move = random.choice(self.moves_white)
                self.last_move = f"White plays {move}"
            else:
                move = random.choice(self.moves_black)
                self.last_move = f"Black plays {move}"

            self.move_count += 1

            if self.move_count > 5:
                if random.random() < 0.2:
                    if self.turn == "White":
                        self.black_king_alive = False
                        self.last_move += " — Black King captured."
                    else:
                        self.white_king_alive = False
                        self.last_move += " — White King captured."

            if self.white_king_alive and self.black_king_alive:
                self.turn = "Black" if self.turn == "White" else "White"

        elif action.startswith("move"):
            parts = action.split()
            if len(parts) == 3:
                self.last_move = f"{self.turn} moves {parts[1]} → {parts[2]}"
                self.turn = "Black" if self.turn == "White" else "White"
            else:
                print("Invalid move format. Use: move e2 e4")
        else:
            print("Invalid action")

    def print_status(self):
        if not self.white_king_alive:
            print("Game Over. Black Wins.\n")
        elif not self.black_king_alive:
            print("Game Over. White Wins.\n")
        else:
            print(self.last_move if self.last_move else "Game started. White to play.")
            print(f"Next Turn: {self.turn}\n")

```
### Usage: 

```
agent = ChessAgent()

while agent.white_king_alive and agent.black_king_alive:
    agent.perform_action("play")
    agent.print_status()
```
### Output:

<img width="624" height="366" alt="image" src="https://github.com/user-attachments/assets/e255575d-763e-43d9-86d9-44a1bbc6a4e3" />


### Result:

The program to develop an AI Agent with PEAS has been successfully implemented .
