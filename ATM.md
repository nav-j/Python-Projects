```
import tkinter as tk
from tkinter import messagebox, simpledialog

# Initial balance
balance = 10000


# Function to check balance
def check_balance():
    messagebox.showinfo(
        "Account Balance",
        f"Your current balance is: ₹{balance:.2f}"
    )


# Function to deposit money
def deposit_money():
    global balance

    try:
        amount = simpledialog.askfloat(
            "Deposit Money",
            "Enter amount to deposit:"
        )

        if amount is None:
            return

        if amount <= 0:
            messagebox.showerror(
                "Invalid Amount",
                "Deposit amount must be greater than zero."
            )
        else:
            balance += amount
            messagebox.showinfo(
                "Deposit Successful",
                f"₹{amount:.2f} deposited successfully.\n"
                f"New balance: ₹{balance:.2f}"
            )

    except ValueError:
        messagebox.showerror(
            "Invalid Input",
            "Please enter a numeric amount."
        )


# Function to withdraw money
def withdraw_money():
    global balance

    try:
        amount = simpledialog.askfloat(
            "Withdraw Money",
            "Enter amount to withdraw:"
        )

        if amount is None:
            return

        if amount <= 0:
            messagebox.showerror(
                "Invalid Amount",
                "Withdrawal amount must be greater than zero."
            )

        elif amount > balance:
            messagebox.showerror(
                "Insufficient Balance",
                "You do not have enough balance."
            )

        else:
            balance -= amount
            messagebox.showinfo(
                "Withdrawal Successful",
                f"₹{amount:.2f} withdrawn successfully.\n"
                f"Remaining balance: ₹{balance:.2f}"
            )

    except ValueError:
        messagebox.showerror(
            "Invalid Input",
            "Please enter a numeric amount."
        )


# Function to exit the ATM
def exit_atm():
    if messagebox.askyesno(
        "Exit ATM",
        "Are you sure you want to exit?"
    ):
        root.destroy()


# Create main window
root = tk.Tk()
root.title("ATM Management System")
root.geometry("350x400")
root.resizable(False, False)

# Heading
heading = tk.Label(
    root,
    text="ATM MANAGEMENT SYSTEM",
    font=("Arial", 16, "bold")
)
heading.pack(pady=20)

# Initial balance information
info = tk.Label(
    root,
    text="Welcome!\nInitial Balance: ₹10,000",
    font=("Arial", 12)
)
info.pack(pady=10)

# Menu buttons
tk.Button(
    root, text="1. Check Balance",
    width=22, command=check_balance
).pack(pady=7)

tk.Button(
    root, text="2. Deposit Money",
    width=22, command=deposit_money
).pack(pady=7)

tk.Button(
    root, text="3. Withdraw Money",
    width=22, command=withdraw_money
).pack(pady=7)

tk.Button(
    root, text="4. Exit",
    width=22, command=exit_atm
).pack(pady=7)

# Run application
root.mainloop()
```
