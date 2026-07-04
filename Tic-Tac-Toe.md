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

This project is a solid next step after a calculator because it introduces **game state management** and **GUI event handling** while remaining easy to understand.
