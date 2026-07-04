A great beginner-friendly GUI game project is **Rock, Paper, Scissors** using Tkinter. It teaches GUI programming, event handling, random numbers, conditions, and scorekeeping.

---

# Project: Rock Paper Scissors Game

## Features

* 🎮 Graphical User Interface (Tkinter)
* 👤 Player vs Computer
* 🎲 Random computer choice
* 🏆 Live score tracking
* 🔄 Play unlimited rounds
* 🗑️ Reset score
* ❌ Exit button
* 🎨 Light, modern interface

---

## Python Code

```python
import tkinter as tk
from tkinter import messagebox
import random

# ---------------- Main Window ----------------

root = tk.Tk()
root.title("Rock Paper Scissors")
root.geometry("500x550")
root.configure(bg="#F5F7FA")
root.resizable(False, False)

# ---------------- Variables ----------------

player_score = 0
computer_score = 0

choices = ["Rock", "Paper", "Scissors"]

# ---------------- Functions ----------------

def play(player):

    global player_score
    global computer_score

    computer = random.choice(choices)

    player_choice.config(text=f"Player : {player}")
    computer_choice.config(text=f"Computer : {computer}")

    if player == computer:
        result.config(text="It's a Draw!", fg="#FF9800")

    elif (
        (player == "Rock" and computer == "Scissors") or
        (player == "Paper" and computer == "Rock") or
        (player == "Scissors" and computer == "Paper")
    ):

        player_score += 1
        result.config(text="You Win!", fg="green")

    else:
        computer_score += 1
        result.config(text="Computer Wins!", fg="red")

    score.config(
        text=f"Player : {player_score}     Computer : {computer_score}"
    )


def reset():

    global player_score
    global computer_score

    player_score = 0
    computer_score = 0

    player_choice.config(text="Player : ")
    computer_choice.config(text="Computer : ")

    score.config(text="Player : 0     Computer : 0")

    result.config(text="Choose Your Move", fg="#2C3E50")


# ---------------- Heading ----------------

title = tk.Label(
    root,
    text="Rock Paper Scissors",
    font=("Segoe UI", 22, "bold"),
    bg="#F5F7FA",
    fg="#2C3E50"
)

title.pack(pady=20)

# ---------------- Result ----------------

result = tk.Label(
    root,
    text="Choose Your Move",
    font=("Segoe UI", 16),
    bg="#F5F7FA",
    fg="#2C3E50"
)

result.pack(pady=10)

# ---------------- Choices ----------------

player_choice = tk.Label(
    root,
    text="Player : ",
    font=("Segoe UI", 14),
    bg="#F5F7FA"
)

player_choice.pack()

computer_choice = tk.Label(
    root,
    text="Computer : ",
    font=("Segoe UI", 14),
    bg="#F5F7FA"
)

computer_choice.pack(pady=10)

# ---------------- Score ----------------

score = tk.Label(
    root,
    text="Player : 0     Computer : 0",
    font=("Segoe UI", 15, "bold"),
    bg="#F5F7FA",
    fg="#1565C0"
)

score.pack(pady=15)

# ---------------- Buttons ----------------

frame = tk.Frame(root, bg="#F5F7FA")
frame.pack(pady=20)

rock = tk.Button(
    frame,
    text="🪨 Rock",
    font=("Segoe UI", 13, "bold"),
    width=12,
    bg="#AEDFF7",
    command=lambda: play("Rock")
)

rock.grid(row=0, column=0, padx=10)

paper = tk.Button(
    frame,
    text="📄 Paper",
    font=("Segoe UI", 13, "bold"),
    width=12,
    bg="#C8E6C9",
    command=lambda: play("Paper")
)

paper.grid(row=0, column=1, padx=10)

scissors = tk.Button(
    frame,
    text="✂ Scissors",
    font=("Segoe UI", 13, "bold"),
    width=12,
    bg="#FFE5B4",
    command=lambda: play("Scissors")
)

scissors.grid(row=0, column=2, padx=10)

# ---------------- Bottom Buttons ----------------

bottom = tk.Frame(root, bg="#F5F7FA")
bottom.pack(pady=30)

reset_btn = tk.Button(
    bottom,
    text="Reset",
    width=12,
    font=("Segoe UI", 12, "bold"),
    bg="#D6EAF8",
    command=reset
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

## Concepts Used

* Tkinter GUI
* Labels
* Buttons
* Frames
* Variables
* Functions
* `if-elif-else`
* `random.choice()`
* Global variables
* Event-driven programming

---

## Sample Interface

```text
----------------------------------------------------
            Rock Paper Scissors
----------------------------------------------------

        Choose Your Move

Player   : Rock
Computer : Scissors

Player : 3        Computer : 2

+-----------+ +-----------+ +-----------+
| 🪨 Rock   | | 📄 Paper  | | ✂ Scissors|
+-----------+ +-----------+ +-----------+

        +---------+   +---------+
        | Reset   |   | Exit    |
        +---------+   +---------+
```

### Other beginner-friendly game ideas

* 🎯 Number Guessing Game (GUI)
* ❌⭕ Tic-Tac-Toe
* 🐍 Snake Game
* 🧱 Brick Breaker
* 🚗 Car Racing Game
* 🐦 Flappy Bird
* 🧠 Memory Card Matching Game
* 🔢 2048 Game
* 🎈 Balloon Pop Game
* 🎲 Dice Rolling Simulator

If you're building projects for a portfolio or classroom, **Tic-Tac-Toe** and **Snake Game** are excellent next steps because they introduce game logic, state management, and more advanced GUI techniques.
