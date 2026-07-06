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

