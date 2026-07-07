```
import tkinter as tk
from tkinter import messagebox
import math

# ---------------------- Functions ----------------------

def press(value):
    entry.insert(tk.END, value)

def clear():
    entry.delete(0, tk.END)

def backspace():
    text = entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, text[:-1])

def equal():
    try:
        expression = entry.get()
        result = eval(expression)
        entry.delete(0, tk.END)
        entry.insert(0, result)
    except:
        messagebox.showerror("Error", "Invalid Expression")

def sqrt():
    try:
        value = float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.sqrt(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

def square():
    try:
        value = float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, value ** 2)
    except:
        messagebox.showerror("Error", "Invalid Input")

def power():
    try:
        nums = entry.get().split(",")
        result = math.pow(float(nums[0]), float(nums[1]))
        entry.delete(0, tk.END)
        entry.insert(0, result)
    except:
        messagebox.showinfo(
            "Power",
            "Enter Base and Power separated by comma.\nExample: 2,5"
        )

def factorial():
    try:
        value = int(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.factorial(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

def sin():
    try:
        value = math.radians(float(entry.get()))
        entry.delete(0, tk.END)
        entry.insert(0, math.sin(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

def cos():
    try:
        value = math.radians(float(entry.get()))
        entry.delete(0, tk.END)
        entry.insert(0, math.cos(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

def tan():
    try:
        value = math.radians(float(entry.get()))
        entry.delete(0, tk.END)
        entry.insert(0, math.tan(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

def log():
    try:
        value = float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.log10(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

def ln():
    try:
        value = float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.log(value))
    except:
        messagebox.showerror("Error", "Invalid Input")

# ---------------------- Window ----------------------

root = tk.Tk()
root.title("Scientific Calculator")
root.geometry("520x650")
root.resizable(False, False)
root.configure(bg="#F5F7FA")
# entry = tk.Entry(
#    root,
 #   font=("Arial", 22),
  #  bd=8,
   # relief="sunken",
    #justify="right"
#)#

entry = tk.Entry(
    root,
    font=("Arial", 22, "bold"),
    bd=5,
    relief="flat",
    justify="right",
    bg="white",
    fg="#2C3E50",
    insertbackground="#2C3E50"
)
entry.grid(row=0, column=0, columnspan=5, padx=10, pady=10, sticky="nsew")

# ---------------------- Button Style ----------------------

btn_font = ("Arial", 14, "bold")
width = 6
height = 2

# ---------------------- Scientific Buttons ----------------------

scientific = [
    ("√", sqrt),
    ("x²", square),
    ("xʸ", power),
    ("!", factorial),
    ("C", clear),

    ("sin", sin),
    ("cos", cos),
    ("tan", tan),
    ("log", log),
    ("ln", ln),
]

r = 1
c = 0

for text, cmd in scientific:
    tk.Button(
        root,
        text=text,
        command=cmd,
        width=width,
        height=height,
        font=btn_font,
      #  bg="#4CAF50",
       # fg="white"
        bg="#AEDFF7",      # Light Blue
        fg="#2C3E50"
    ).grid(row=r, column=c, padx=5, pady=5)

    c += 1
    if c > 4:
        c = 0
        r += 1

# ---------------------- Calculator Buttons ----------------------

buttons = [
    "7","8","9","/","⌫",
    "4","5","6","*","(",
    "1","2","3","-",")",
    "0",".","+","=",
]

row = 3
col = 0

for item in buttons:

    if item == "=":
        cmd = equal

    elif item == "⌫":
        cmd = backspace

    else:
        cmd = lambda x=item: press(x)

    tk.Button(
        root,
        text=item,
        command=cmd,
        width=width,
        height=height,
        font=btn_font,
       # bg="#2d89ef",
       # fg="white"
        bg="#FFFFFF",
        fg="#2C3E50",
        activebackground="#D6EAF8",
        activeforeground="#2C3E50"
    ).grid(row=row, column=col, padx=5, pady=5)

    col += 1

    if col > 4:
        col = 0
        row += 1

# π Button
tk.Button(
    root,
    text="π",
    command=lambda: press(str(math.pi)),
    width=width,
    height=2,
    font=btn_font,
   bg="#AEDFF7",      # Light Blue
fg="#2C3E50"
).grid(row=7, column=0, padx=5, pady=5)

# e Button
tk.Button(
    root,
    text="e",
    command=lambda: press(str(math.e)),
    width=width,
    height=2,
    font=btn_font,
   bg="#AEDFF7",      # Light Blue
fg="#2C3E50"
).grid(row=7, column=1, padx=5, pady=5)

root.mainloop()
```

## improved version

```
import tkinter as tk
from tkinter import messagebox
import math

#Functions
def press(value):
    entry.insert(tk.END, value)

def clear():
    entry.delete(0, tk.END)

def backspace():
    text=entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, text[:-1])

def equal():
    try:
        expression=entry.get()
        result=eval(expression)
        entry.delete(0,tk.END)
        entry.insert(0, result)
    except:
        messagebox.showerror("Error!","Invalid Expression")


def sqrt():
    try:
        value=float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.sqrt(value))
    except:
        messagebox.showerror("Error!","Invalid Input")

def square():
    try:
        value=float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, value**2)
    except:
        messagebox.showerror("Error!","Invalid Input")

def power():
    try:
        nums=entry.get().split(",")
        result= math.pow((float(nums[0])), float(nums[1]))
        entry.delete(0, tk.END)
        entry.insert(0, result)
    except:
        messagebox.showerror("Error!","Invalid Input")

def factorial():
    try:
        value=int(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.factorial(value))
    except:
        messagebox.showerror("Error!","Invalid Input")

def sin():
    try:
        value=math.radians(float(entry.get()))                
        entry.delete(0, tk.END)
        entry.insert(0, round(math.sin(value)))
    except:
        messagebox.showerror("Error!","Invalid Input")

def cos():
    try:
        value=math.radians(float(entry.get()))
        entry.delete(0, tk.END)
        entry.insert(0, round(math.cos(value),10))
    except:
        messagebox.showerror("Error!","Invalid Input")

def tan():
    try:
        value=(float(entry.get()))
        if value % 180==90:
                entry.delete(0, tk.END)
                entry.insert(0,"undefined")
                return
        value= math.radians(value)
        result=round(math.tan(value),10)
        entry.delete(0, tk.END)
        entry.insert(0,result)
    except:
        messagebox.showerror("Error!","Invalid Input")

def log():
    try:
        value=float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.log10(value))
    except:
        messagebox.showerror("Error!","Invalid Input")

def ln():
    try:
        value=float(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, math.log(value))
    except:
        messagebox.showerror("Error!","Invalid Input")

#Main Window
root=tk.Tk()
root.title("Scientific Calculator")
root.geometry("520x650")
root.resizable(False,False)         
root.configure(bg="#F5F7FA")      

entry=tk.Entry(
    root,
    font=("Arial",22,"bold"),
    bd=5,                           
    relief="flat",                  
    justify="right",                
    bg="white",
    fg="#2C3E50",                 
    insertbackground="#2C3E50",   
    )
entry.grid(row=0 , column=0 , columnspan=5 , padx=10 , pady=10 , sticky="nsew")


#button style
btn_font=("Arial",14,"bold")
width=6
height=2

# Scientific Buttons
scientific=[
    ("√",sqrt),
    ("x²",square),
    ("xʸ",power),
    ("!",factorial),
    ("C",clear),

    ("sin",sin),
    ("cos",cos),
    ("tan",tan),
    ("log",log),
    ("ln",ln)
]

row=1
column=0

for text,cmd in scientific:
    tk.Button(
        root,
        text=text,
        command=cmd,
        height=height,
        width=width,
        font=btn_font,
        bg="#AEDFF7",
        fg="#2C3E50"
    ).grid(row=row , column=column , padx=5 , pady=5)

    column += 1
    if column>4:
        column = 0
        row +=1

# Calculator Buttons
buttons=[
    "7","8","9","/","⌫",
    "4","5","6","*","(",
    "1","2","3","-",")",
    "0",".","+","="
]

r=3
c=0

for item in buttons:

    if item == "=":
        cmd = equal
    elif item == "⌫":
        cmd = backspace
    else:
        cmd = lambda x=item : press(x)


    tk.Button(
        root,
        text=item,
        font=btn_font,
        command=cmd,
        height=height,
        width=width,
        bg="#FFFFFF",
        fg="#2C3E50",
        activebackground="#D6EAF8",
        activeforeground="#2C3E50"
    ).grid(row=r , column=c , padx=5 , pady=5)

    c += 1
    if c>4:
        c = 0
        r += 1

# π button
tk.Button(
    root,
    text="π",
    font=btn_font,
    command= lambda : press(str(math.pi)),
    height=height,
    width=width,
    bg="#AEDFF7",
    fg="#2C3E50"
).grid(row=7 , column=0 , padx=5 , pady=5)


# e button
tk.Button(
    root,
    text="e",
    font=btn_font,
    command= lambda: press(str(math.e)),
    height=height,
    width=width,
    bg="#AEDFF7",
    fg="#2C3E50"
).grid(row=7 , column=1 , padx=5 , pady=5)


root.mainloop()

```

## Explaination

This program is a **Scientific Calculator** built using **Tkinter** (GUI) and Python's **math** module. It allows users to perform both basic arithmetic and scientific calculations through a graphical interface.

I'll explain it section by section.

---

# Overall Program Flow

```text
Start Program
      │
      ▼
Import Libraries
      │
      ▼
Define Calculator Functions
      │
      ▼
Create Main Window
      │
      ▼
Create Entry Box
      │
      ▼
Create Scientific Buttons
      │
      ▼
Create Number & Operator Buttons
      │
      ▼
Create π and e Buttons
      │
      ▼
Wait for User Input (mainloop)
```

---

# 1. Import Libraries

```python
import tkinter as tk
from tkinter import messagebox
import math
```

### Explanation

### `import tkinter as tk`

Imports the Tkinter library and gives it the shorter name `tk`.

Used to create:

* Window
* Buttons
* Labels
* Entry box

---

### `from tkinter import messagebox`

Imports the messagebox module.

Used to display popup messages.

Example:

```
+---------------------+
| Error!              |
| Invalid Expression  |
|        OK           |
+---------------------+
```

---

### `import math`

Imports Python's math library.

Provides functions like:

```python
math.sqrt()
math.sin()
math.cos()
math.tan()
math.log()
math.factorial()
math.pi
math.e
```

---

# 2. press() Function

```python
def press(value):
    entry.insert(tk.END, value)
```

### Purpose

Adds the clicked button's value into the entry box.

Example:

Current Entry

```
12
```

Click

```
+
```

Result

```
12+
```

---

### `entry.insert()`

Syntax

```python
entry.insert(position, text)
```

Here

```python
tk.END
```

means

> Insert at the end.

---

# 3. clear()

```python
def clear():
    entry.delete(0, tk.END)
```

Deletes everything inside the entry box.

Example

Before

```
12+35
```

After

```
(empty)
```

---

# 4. backspace()

```python
text = entry.get()
```

Gets the current text.

Example

```
12345
```

---

```python
text[:-1]
```

Removes the last character.

Example

```
12345
```

becomes

```
1234
```

---

Then

```python
entry.insert(0, text[:-1])
```

Displays the updated text.

---

# 5. equal()

```python
expression = entry.get()
```

Gets the mathematical expression.

Example

```
15+20/5
```

---

```python
result = eval(expression)
```

`eval()` evaluates the expression.

Example

```
15+20/5
```

becomes

```
19
```

---

Then

```python
entry.insert(0, result)
```

Shows the answer.

---

### Exception Handling

```python
except:
```

If the user enters

```
10++*
```

instead of crashing,

it shows

```
Invalid Expression
```

---

# 6. sqrt()

```python
value=float(entry.get())
```

Reads the number.

Example

```
49
```

---

```python
math.sqrt(value)
```

Calculates

```
√49
```

Result

```
7
```

---

# 7. square()

```python
value**2
```

Raises the number to power 2.

Example

```
9
```

becomes

```
81
```

---

# 8. power()

Suppose user enters

```
2,5
```

---

```python
split(",")
```

Produces

```python
["2","5"]
```

---

Then

```python
math.pow(2,5)
```

Result

```
32
```

---

So this function expects input like:

```
Base,Exponent
```

Example

```
3,4
```

Result

```
81
```

---

# 9. factorial()

```python
math.factorial(value)
```

Example

```
5
```

Result

```
120
```

Because

```
5×4×3×2×1
```

---

# 10. sin()

```python
value = math.radians(float(entry.get()))
```

The calculator accepts degrees.

Python's `math.sin()` requires radians.

Example

```
90°
```

becomes

```
1.5708 radians
```

---

Then

```python
math.sin(value)
```

returns

```
1
```

---

### Why `round()`?

Without rounding

```
0.99999999998
```

With rounding

```
1
```

---

# 11. cos()

Same process.

Example

```
60°
```

Result

```
0.5
```

---

# 12. tan()

First

```python
if value % 180 == 90
```

Checks

```
90°

270°

450°
```

because tan is undefined there.

Instead of crashing,

it displays

```
undefined
```

Otherwise

```python
math.tan()
```

is calculated.

---

# 13. log()

```python
math.log10(value)
```

Computes base-10 logarithm.

Example

```
100
```

Result

```
2
```

because

```
10² = 100
```

---

# 14. ln()

```python
math.log(value)
```

Computes the natural logarithm.

Base

```
e
```

Example

```
ln(e)
```

Result

```
1
```

---

# 15. Main Window

```python
root = tk.Tk()
```

Creates the main application window.

---

```python
root.title()
```

Sets the window title.

---

```python
root.geometry("520x650")
```

Window size

```
520 × 650
```

---

```python
root.resizable(False,False)
```

Prevents resizing.

---

```python
root.configure(bg="#F5F7FA")
```

Sets the background color.

---

# 16. Entry Widget

```python
entry = tk.Entry(...)
```

This is the calculator display.

Example

```
----------------------
|            25+10   |
----------------------
```

---

### Important Properties

### `font`

Text size.

---

### `justify="right"`

Numbers appear on the right side.

Like a real calculator.

---

### `insertbackground`

Changes the cursor color.

---

# 17. Grid Layout

```python
entry.grid(...)
```

Places the entry box.

---

```python
columnspan=5
```

The display stretches across all five columns.

---

# 18. Button Style

```python
btn_font
```

Stores the font.

Instead of writing

```python
font=("Arial",14,"bold")
```

20 times,

you define it once and reuse it.

---

# 19. Scientific Button List

```python
scientific = [
("√",sqrt),
...
]
```

Each tuple contains

```
(Button Text , Function)
```

Example

```
("√",sqrt)
```

means

```
Button shows

√

↓

Calls sqrt()
```

---

# 20. Creating Scientific Buttons

```python
for text,cmd in scientific:
```

Loops through every tuple.

Instead of writing ten separate `Button()` calls, one loop creates them all.

---

```python
command = cmd
```

Assigns the corresponding function to each button.

---

# 21. Calculator Buttons

```python
buttons = [...]
```

Stores all number and operator buttons.

```
7 8 9 /

4 5 6 *

1 2 3 -

0 . + =
```

---

# 22. Lambda Function

```python
lambda x=item: press(x)
```

Suppose the button text is

```
7
```

Clicking it runs

```python
press("7")
```

If the button text is

```
+
```

It runs

```python
press("+")
```

This single lambda handles all number and operator buttons.

---

# 23. Equal Button

```python
if item == "=":
    cmd = equal
```

Clicking

```
=
```

calls

```python
equal()
```

instead of inserting "=" into the entry box.

---

# 24. Backspace Button

```python
elif item=="⌫":
```

Calls

```python
backspace()
```

instead of inserting the symbol.

---

# 25. π Button

```python
command=lambda: press(str(math.pi))
```

Clicking π inserts

```
3.141592653589793
```

into the entry box.

---

# 26. e Button

```python
command=lambda: press(str(math.e))
```

Inserts

```
2.718281828459045
```

---

# 27. mainloop()

```python
root.mainloop()
```

Starts Tkinter's event loop.

The program now waits for user actions such as:

* Clicking buttons
* Typing into the entry box
* Closing the window

Without `mainloop()`, the window would open and close immediately.

---

# Concepts Used in This Project

This scientific calculator demonstrates many important Python and Tkinter concepts:

* **Functions** (`def`)
* **Exception handling** (`try` / `except`)
* **Modules** (`math`, `tkinter`)
* **GUI widgets** (`Tk`, `Entry`, `Button`)
* **Lambda functions**
* **Lists** (button definitions)
* **Loops** (`for`)
* **String methods** (`split()`)
* **Type conversion** (`int()`, `float()`)
* **Mathematical functions** (`sqrt`, `pow`, `factorial`, `sin`, `cos`, `tan`, `log`)
* **Grid layout manager**
* **Widget methods** (`insert()`, `delete()`, `get()`, `grid()`)

By understanding this project, you'll have a strong foundation for creating more advanced Tkinter applications such as unit converters, billing systems, login forms, attendance systems, or even full-featured desktop applications.
