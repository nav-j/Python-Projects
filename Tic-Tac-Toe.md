A **Tic-Tac-Toe** game is an excellent intermediate Python project. It demonstrates:

* ✅ Tkinter GUI
* ✅ Functions
* ✅ Lists
* ✅ Loops
* ✅ Conditional statements
* ✅ Event handling
* ✅ Winner detection
* ✅ Draw detection
* ✅ Reset functionality

---

# Python Code: Tic-Tac-Toe Game (Tkinter)

```python
import tkinter as tk
from tkinter import messagebox

# ---------------- Window ----------------

root = tk.Tk()
root.title("Tic-Tac-Toe")
root.geometry("420x520")
root.configure(bg="#F5F7FA")
root.resizable(False, False)

# ---------------- Variables ----------------

current_player = "X"
board = [""] * 9
buttons = []

# ---------------- Functions ----------------

def check_winner():
    winning_combinations = [
        [0,1,2],
        [3,4,5],
        [6,7,8],
        [0,3,6],
        [1,4,7],
        [2,5,8],
        [0,4,8],
        [2,4,6]
    ]

    for combo in winning_combinations:
        a, b, c = combo

        if board[a] == board[b] == board[c] != "":
            buttons[a].config(bg="#A5D6A7")
            buttons[b].config(bg="#A5D6A7")
            buttons[c].config(bg="#A5D6A7")

            messagebox.showinfo("Winner", f"Player {board[a]} Wins!")

            disable_buttons()
            return True

    if "" not in board:
        messagebox.showinfo("Game Over", "It's a Draw!")
        return True

    return False


def click(position):

    global current_player

    if board[position] == "":

        board[position] = current_player

        buttons[position].config(
            text=current_player,
            state="disabled"
        )

        if not check_winner():

            if current_player == "X":
                current_player = "O"
            else:
                current_player = "X"

            status.config(text=f"Player {current_player}'s Turn")


def disable_buttons():

    for button in buttons:
        button.config(state="disabled")


def reset_game():

    global current_player
    global board

    current_player = "X"

    board = [""] * 9

    status.config(text="Player X's Turn")

    for button in buttons:
        button.config(
            text="",
            state="normal",
            bg="white"
        )

# ---------------- Heading ----------------

title = tk.Label(
    root,
    text="Tic-Tac-Toe",
    font=("Segoe UI", 22, "bold"),
    bg="#F5F7FA",
    fg="#2C3E50"
)

title.pack(pady=15)

# ---------------- Status ----------------

status = tk.Label(
    root,
    text="Player X's Turn",
    font=("Segoe UI", 15),
    bg="#F5F7FA",
    fg="#1565C0"
)

status.pack()

# ---------------- Game Board ----------------

frame = tk.Frame(root, bg="#F5F7FA")
frame.pack(pady=20)

for row in range(3):
    for col in range(3):

        index = row * 3 + col

        button = tk.Button(
            frame,
            text="",
            width=6,
            height=3,
            font=("Segoe UI", 22, "bold"),
            bg="white",
            fg="#2C3E50",
            activebackground="#D6EAF8",
            command=lambda i=index: click(i)
        )

        button.grid(
            row=row,
            column=col,
            padx=5,
            pady=5
        )

        buttons.append(button)

# ---------------- Bottom Buttons ----------------

bottom = tk.Frame(root, bg="#F5F7FA")
bottom.pack(pady=20)

reset_btn = tk.Button(
    bottom,
    text="New Game",
    width=12,
    font=("Segoe UI", 12, "bold"),
    bg="#AEDFF7",
    command=reset_game
)

reset_btn.grid(row=0, column=0, padx=10)

exit_btn = tk.Button(
    bottom,
    text="Exit",
    width=12,
    font=("Segoe UI", 12, "bold"),
    bg="#F8D7DA",
    command=root.destroy
)

exit_btn.grid(row=0, column=1, padx=10)

root.mainloop()
```

---

# Features

* ✅ Two-player game (Player X vs Player O)
* ✅ Clean light-themed interface
* ✅ Detects all winning combinations
* ✅ Detects draw
* ✅ Highlights the winning row in green
* ✅ Prevents overwriting occupied cells
* ✅ "New Game" button to reset the board
* ✅ Exit button

---

# Python Concepts Used

* Tkinter GUI
* Buttons
* Labels
* Frames
* Lists
* Nested `for` loops
* Functions
* `if-else` statements
* Global variables
* Event handling with `command`
* Lambda functions
* Message boxes

---

# Sample Interface

```text
-----------------------------------------
          Tic-Tac-Toe
-----------------------------------------

        Player X's Turn

+-------+-------+-------+
|       |       |       |
+-------+-------+-------+
|       |       |       |
+-------+-------+-------+
|       |       |       |
+-------+-------+-------+

      [ New Game ] [ Exit ]
```
## Explaination

This is a **Tic-Tac-Toe game** built using **Tkinter**, Python's standard GUI library. I'll explain it section by section so you understand not only **what** the code does but also **why** it's written that way.

---

# Overall Program Flow

```text
Start Program
      │
      ▼
Create Window
      │
      ▼
Create Variables
      │
      ▼
Create Functions
      │
      ▼
Create Labels
      │
      ▼
Create 3×3 Buttons
      │
      ▼
Create New Game & Exit Buttons
      │
      ▼
Wait for User Click
      │
      ▼
Check Winner
      │
      ▼
Win / Draw / Continue
```

---

# 1. Import Libraries

```python
import tkinter as tk
from tkinter import messagebox
```

### Explanation

* `tkinter` is used to create the graphical interface (window, buttons, labels, etc.).
* `messagebox` is used to display popup messages.

Example:

```
+--------------------+
|      Winner        |
|  Player X Wins!    |
|        OK          |
+--------------------+
```

---

# 2. Create the Main Window

```python
root = tk.Tk()
```

### Explanation

Creates the main application window.

Everything in the game is placed inside this window.

---

```python
root.title("Tic-Tac-Toe")
```

Sets the title shown at the top of the window.

---

```python
root.geometry("450x500")
```

Sets the window size.

* Width = 450 pixels
* Height = 500 pixels

---

```python
root.configure(bg="#F5F7FA")
```

Changes the background color.

---

```python
root.resizable(False, False)
```

Prevents the user from resizing the window.

---

# 3. Variables

```python
current_player = "X"
```

Stores whose turn it is.

Initially:

```
current_player = "X"
```

Player X always starts.

---

```python
board = [""] * 9
```

Creates the game board.

Initially it looks like:

```python
[
"",
"",
"",
"",
"",
"",
"",
"",
""
]
```

Each position represents one square.

```
0 | 1 | 2
---------
3 | 4 | 5
---------
6 | 7 | 8
```

Example after some moves:

```python
[
"X",
"O",
"",
"",
"X",
"",
"",
"",
"O"
]
```

---

```python
buttons = []
```

Stores all button widgets.

Later each button is added:

```
buttons[0]
buttons[1]
...
buttons[8]
```

This makes it easy to access any square.

---

# 4. check_winner()

```python
def check_winner():
```

Purpose:

Checks if someone has won.

---

## Winning Combinations

```python
winning_combinations = [
    [0,1,2],
    [3,4,5],
    [6,7,8],
    [0,3,6],
    [1,4,7],
    [2,5,8],
    [0,4,8],
    [2,4,6]
]
```

These represent all possible winning lines.

```
0 1 2

3 4 5

6 7 8
```

Rows

```
0 1 2

3 4 5

6 7 8
```

Columns

```
0
3
6

1
4
7

2
5
8
```

Diagonals

```
0
 4
  8
```

and

```
2
 4
6
```

---

## Loop

```python
for combo in winning_combinations:
```

Checks every winning pattern one by one.

---

```python
a,b,c = combo
```

Suppose

```python
combo = [0,1,2]
```

then

```
a = 0

b = 1

c = 2
```

---

```python
if board[a] == board[b] == board[c] != "":
```

Checks whether

```
X X X

or

O O O
```

and ensures they're not empty.

---

If true:

```python
buttons[a].config(bg="#A5D6A7")
```

Makes the winning buttons green.

---

```python
messagebox.showinfo(...)
```

Displays

```
Player X Wins!
```

---

```python
disable_buttons()
```

Stops players from clicking after the game ends.

---

Returns

```python
True
```

meaning the game has finished.

---

## Draw

```python
if "" not in board:
```

If no empty cells remain:

```
Draw
```

Shows:

```
It's a Draw!
```

---

# 5. click()

```python
def click(position):
```

Runs whenever a player clicks a square.

Example

Click top-left

```
position = 0
```

Click center

```
position = 4
```

---

```python
global current_player
```

Allows the function to modify the global variable.

Without `global`, changing `current_player` inside the function would only affect a temporary local variable.

---

```python
if board[position] == "":
```

Allows a move only if the square is empty.

This prevents overwriting an existing X or O.

---

```python
board[position] = current_player
```

Stores the player's symbol in the board list.

Example:

Before

```
["","","","","","","","",""]
```

After X clicks the center (position 4)

```
["","","","","X","","","",""]
```

---

```python
buttons[position].config(
    text=current_player,
    state="disabled"
)
```

Updates the button to display the symbol and disables it so it can't be clicked again.

---

```python
if not check_winner():
```

Checks if the game is still ongoing.

If there's no winner or draw, switch turns.

---

```python
if current_player == "X":
    current_player = "O"
else:
    current_player = "X"
```

Alternates turns between X and O.

---

```python
status.config(...)
```

Updates the label to show whose turn is next.

---

# 6. disable_buttons()

```python
def disable_buttons():
```

Purpose:

Disable every game button after someone wins.

---

```python
for button in buttons:
```

Loops through all 9 buttons.

---

```python
button.config(state="disabled")
```

Prevents any further moves.

---

# 7. reset_game()

Purpose:

Start a new game.

---

```python
current_player = "X"
```

Player X starts again.

---

```python
board = [""] * 9
```

Clears the game board.

---

```python
status.config(...)
```

Updates the status label.

---

```python
button.config(
    text="",
    state="normal",
    bg="white"
)
```

Resets every button by:

* Clearing the text
* Enabling it
* Restoring the white background

---

# 8. Heading Label

```python
title = tk.Label(...)
```

Creates the title:

```
Tic-Tac-Toe
```

---

```python
title.pack(pady=15)
```

Places the title in the window with 15 pixels of vertical padding.

---

# 9. Status Label

Displays whose turn it is.

Initially:

```
Player X's Turn
```

This label changes after every valid move.

---

# 10. Game Board Frame

```python
frame = tk.Frame(root)
```

A `Frame` is like a container that groups related widgets.

Here it holds the 3×3 grid of buttons.

---

# 11. Create the 3×3 Grid

```python
for row in range(3):
    for col in range(3):
```

Creates 9 buttons.

Rows:

```
0
1
2
```

Columns:

```
0
1
2
```

So the buttons are arranged as:

```
0 1 2

3 4 5

6 7 8
```

---

```python
index = row * 3 + col
```

Converts the row and column into a single board index.

Examples:

| Row | Col | Index |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 0   | 2   | 2     |
| 1   | 0   | 3     |
| 1   | 1   | 4     |
| 1   | 2   | 5     |
| 2   | 0   | 6     |
| 2   | 1   | 7     |
| 2   | 2   | 8     |

---

```python
command=lambda i=index: click(i)
```

This is a **lambda function** that tells each button which board position it represents.

Without using `i=index`, every button would incorrectly end up using the last value of `index` (8).

---

```python
buttons.append(button)
```

Stores each button in the `buttons` list so it can be accessed later (for changing text, color, or disabling it).

---

# 12. Bottom Buttons

## New Game

```python
command=reset_game
```

When clicked, it resets the board and starts a fresh game.

---

## Exit

```python
command=root.destroy
```

Closes the application window.

---

# 13. Start the Application

```python
root.mainloop()
```

This starts Tkinter's **event loop**.

It waits for user actions such as:

* Clicking a game square
* Clicking "New Game"
* Clicking "Exit"
* Closing the window

Without `mainloop()`, the window would appear briefly and then immediately close.

---

## Concepts Used in This Project

This Tic-Tac-Toe game demonstrates many important Python and Tkinter concepts:

* Variables
* Lists
* Functions
* `global` variables
* Nested loops (`for` inside `for`)
* Conditional statements (`if`, `else`)
* Lambda functions
* GUI widgets (`Tk`, `Frame`, `Label`, `Button`)
* Event handling with `command`
* List indexing
* Win-condition logic
* Resetting application state
* Message boxes
* Widget configuration using `.config()`

Understanding this project gives you a solid foundation for building more advanced GUI games such as Connect Four, Snake, Minesweeper, Chess, or Sudoku.

