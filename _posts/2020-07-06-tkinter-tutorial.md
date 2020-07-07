---
layout: post
title: "Tkinter Tutorial"
subtitle: "Một số kinh nghiệm khi sử dụng Tkinter"
date:   2020-07-06
categories: [Python GUI Programming]
tags: [Python, GUI, Tkinter]
---

# Tkinter Tutorial

## A Simple Hello World Program

```python
import tkinter as tk

class Application(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.master = master
        self.pack()
        self.create_widgets()

    def create_widgets(self):
        self.hi_there = tk.Button(self)
        self.hi_there["text"] = "Hello Word\n(click me)"
        self.hi_there["command"] = self.say_hi
        self.hi_there.pack(side="top")

        self.quit = tk.Button(self, text="QUIT", fg="red", 
            command=self.master.destroy)
        self.quit.pack(side="bottom")

    def say_hi(self):
        print("hi there, everyone!")

root = tk.Tk()
app = Application(master=root)
app.mainloop()
```

### Options

#### Setting Options

```python
# Method 1
fred = Button(self, fg="red", bg="blue")

# Method 2
fred["fg"] = "red"
fred["bg"] = "blue"

# Method 3
fred.config(fg="red", bg="blue")
```

#### Packer Options

anchor, expand, fill, ipadx, ipady, padx, pady, side

### Coupling Widget Variables

```python
import tkinter as tk

class App(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.pack()

        self.entrythingy = tk.Entry()
        self.entrythingy.pack()

        # here is the application variable
        self.contents = tk.StringVar()
        # set it to some value
        self.contents.set("this is a variable")
        # tell the entry widget to watch this variable
        self.entrythingy["textvariable"] = self.contents

        # and here we get a callback when the user hits return.
        # we will have the program print out the value of the
        # application variable when the user hits return
        self.entrythingy.bind('<Key-Return>',
                              self.print_contents)

    def print_contents(self, event):
        print("hi. contents of entry is now ---->",
              self.contents.get())
        
root = tk.Tk()
app = App(master=root)
app.mainloop()
```

### The Window Manager

```python
import tkinter as tk

class App(tk.Frame):
    def __init__(self, master=None):
        super().__init__(master)
        self.pack()

# create the application
myapp = App()

#
# here are method calls to the window manager class
#
myapp.master.title("My Do-Nothing Application")
myapp.master.maxsize(1000, 400)

# start the program
myapp.mainloop()
```

### Bindings and Events

## Working With Widgets

| Widget Class | Description |
| :--- | :-------- |
| Label | A widget used to display text on the screen  |
| Button | A button that can contain text and can perform an action when clicked |
| Entry | A text entry widget that allows only a single line of text |
| Text | A text entry widget that allows multiline text entry |
| Frame | A rectangular region used to group related widgets or provide padding between widgets |
| Listbox |  |
| Checkbutton |  |
| Radiobutton |  |
| Combobox |  |
| Scrollbar |  |
| SizeGrip |  |
| Progressbar |  |
| Scale |  |
| Spinbox |  |

### Displaying Text and Images With Label Widgets

### Displaying Clickable Buttons With Button Widgets

###  Getting user input with Entry widgets

**Example 1.**
```python
import tkinter as tk

root = tk.Tk()

l = tk.Label(text="Name")
l.pack()

e1 = tk.Entry(fg="yellow", bg="blue", width=50)
e1.pack()

def e1_callback():
	print(e1.get())

def e1_delete():
	# e1.delete(first=0, last=3) # <-- 0 <= index < 3
	e1.delete(0, tk.END)

def e1_insert():
	e1.insert(0, "My name is ... ")

# Get
b11 = tk.Button(text="Retrieving text from Entry")
b11["command"] = e1_callback
b11.pack()
# Delete
b12 = tk.Button(text="Deleting text from Entry")
b12["command"] = e1_delete
b12.pack()
# Insert
b13 = tk.Button(text="Inserting  text from Entry")
b13["command"] = e1_insert
b13.pack()

# Quit
def root_destroy():
	root.destroy()
b_quit = tk.Button(text="Quit")
b_quit["command"] = root_destroy
b_quit.pack()

root.mainloop()
```

**Example 2.**
```python
import tkinter as tk

root = tk.Tk()

l = tk.Label(text="Name")
l.pack()

# Method 1
e1 = tk.Entry(fg="yellow", bg="blue", width=50)
e1.pack()
e1.delete(0, tk.END)
e1.insert(0, "a default value")
s = e1.get()

# Method 2
v = tk.StringVar()
e2 = tk.Entry(root, textvariable=v)
e2.pack()
v.set("a default value")
s2 = v.get()

# Quit
def root_destroy():
	root.destroy()
b_quit = tk.Button(text="Quit")
b_quit["command"] = root_destroy
b_quit.pack()

root.mainloop()
```

### Getting Multiline User Input With Text Widgets

**Example.**
```python
import tkinter as tk

root = tk.Tk()

# A text widget
text_box = tk.Text()
text_box.pack()

# get the letters from the text box
text_box.get("1.0") # <--  line = 1, column = 0
text_box.get("1.0", "1.5") # <-- line = 1, 0 <= column < 5
text_box.get("2.0", "2.5") # <-- line = 2, 0 <= column < 5

# delete
text_box.delete("1.0")
text_box.delete("1.0", "1.4")
text_box.delete("1.0", tk.END)
text_box.insert("1.0", "Hello")

# insert
text_box.insert("2.0", "World")
text_box.insert("2.0", "\nWorld")
text_box.insert(tk.END, "Put me at the end!")
text_box.insert(tk.END, "\nPut me on a new line!")

root.mainloop()
```

### Assigning Widgets to Frames With Frame Widgets

**Example.**
```python
import tkinter as tk

root = tk.Tk()

frame = tk.Frame()
frame.pack()
label = tk.Label(master=frame, text="Label")
label.pack()

frame_a = tk.Frame()
label_a1 = tk.Label(master=frame_a, text="I'm in Frame A1", fg="blue", bg="yellow")
label_a1.pack()
label_a2 = tk.Label(master=frame_a, text="I'm in Frame A2", fg="red")
label_a2.pack()

frame_b = tk.Frame()
label_b = tk.Label(master=frame_b, text="I'm in Frame B")
label_b.pack()

# Swap the order of `frame_a` and `frame_b`
frame_b.pack()
frame_a.pack()

root.mainloop()
```

### Adjusting Frame Appearance With Reliefs

Frame widgets can be configured with a relief attribute that creates a border around the frame: 

- tk.FLAT: Has no border effect (the default value).
- tk.SUNKEN: Creates a sunken effect.
- tk.RAISED: Creates a raised effect.
- tk.GROOVE: Creates a grooved border effect.
- tk.RIDGE: Creates a ridged effect.

**Example.**
```python
import tkinter as tk

border_effects = {
    "flat": tk.FLAT,
    "sunken": tk.SUNKEN,
    "raised": tk.RAISED,
    "groove": tk.GROOVE,
    "ridge": tk.RIDGE,
}

window = tk.Tk()

for relief_name, relief in border_effects.items():
    frame = tk.Frame(master=window, relief=relief, borderwidth=5)
    frame.pack(side=tk.LEFT)
    label = tk.Label(master=frame, text=relief_name)
    label.pack()

window.mainloop()
```

### Understanding Widget Naming Conventions

| Widget Class | Variable Name Prefix |	Example
| :---: | :---: | :---:|
| Label |	lbl | lbl_name |
| Button | btn | btn_submit |
| Entry | ent | ent_age |
| Text | txt | txt_notes |
| Frame | frm | frm_address |

## Controlling Layout With Geometry Managers

### The .pack() Geometry Manager

**Example 1.**
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=100, height=100, bg="red")
frame1.pack()

frame2 = tk.Frame(master=window, width=50, height=50, bg="yellow")
frame2.pack()

frame3 = tk.Frame(master=window, width=25, height=25, bg="blue")
frame3.pack()

window.mainloop()
```

**Example 2.**
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, height=100, bg="red")
frame1.pack(fill=tk.X)

frame2 = tk.Frame(master=window, height=50, bg="yellow")
frame2.pack(fill=tk.X)

frame3 = tk.Frame(master=window, height=25, bg="blue")
frame3.pack(fill=tk.X)

window.mainloop()
```

**Example 3.**
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=200, height=100, bg="red")
frame1.pack(fill=tk.Y, side=tk.LEFT)

frame2 = tk.Frame(master=window, width=100, bg="yellow")
frame2.pack(fill=tk.Y, side=tk.LEFT)

frame3 = tk.Frame(master=window, width=50, bg="blue")
frame3.pack(fill=tk.Y, side=tk.LEFT)

window.mainloop()
```

**Example 4.**
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=200, height=100, bg="red")
frame1.pack(fill=tk.BOTH, side=tk.LEFT, expand=True)

frame2 = tk.Frame(master=window, width=100, bg="yellow")
frame2.pack(fill=tk.BOTH, side=tk.LEFT, expand=True)

frame3 = tk.Frame(master=window, width=50, bg="blue")
frame3.pack(fill=tk.BOTH, side=tk.LEFT, expand=True)

window.mainloop()
```

### The .place() Geometry Manager

**Example.**
```python
import tkinter as tk

window = tk.Tk()

frame = tk.Frame(master=window, width=150, height=150)
frame.pack()

label1 = tk.Label(master=frame, text="I'm at (0, 0)", bg="red")
label1.place(x=0, y=0)

label2 = tk.Label(master=frame, text="I'm at (75, 75)", bg="yellow")
label2.place(x=75, y=75)

window.mainloop()
```

### The .grid() Geometry Manager

**Example 1.**
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack()

window.mainloop()
```

**Example 2.**
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack()

window.mainloop()
```

**Example 3.**
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)

        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack(padx=5, pady=5)

window.mainloop()
```

**Example 4.**
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    window.columnconfigure(i, weight=1, minsize=75)
    window.rowconfigure(i, weight=1, minsize=50)

    for j in range(0, 3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)

        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack(padx=5, pady=5)

window.mainloop()
```

**Example 5.**
```python
import tkinter as tk

window = tk.Tk()
window.columnconfigure(0, minsize=250)
window.rowconfigure([0, 1], minsize=100)

label1 = tk.Label(text="A")
label1.grid(row=0, column=0)

label2 = tk.Label(text="B")
label2.grid(row=1, column=0)

window.mainloop()
```

**Example 6.**
```python
import tkinter as tk

window = tk.Tk()
window.columnconfigure(0, minsize=250)
window.rowconfigure([0, 1], minsize=100)

label1 = tk.Label(text="A")
label1.grid(row=0, column=0, sticky="n") # <-- n: top-center, e: right-center, s: bottom-center, w: left-center

label2 = tk.Label(text="B")
label2.grid(row=1, column=0, sticky="n")

window.mainloop()
```

**Example 7.**
```python
import tkinter as tk

window = tk.Tk()
window.columnconfigure(0, minsize=250)
window.rowconfigure([0, 1], minsize=100)

label1 = tk.Label(text="A")
label1.grid(row=0, column=0, sticky="ne")

label2 = tk.Label(text="B")
label2.grid(row=1, column=0, sticky="sw")

window.mainloop()
```

**Example 8.**
```python
import tkinter as tk

window = tk.Tk()

window.rowconfigure(0, minsize=50)
window.columnconfigure([0, 1, 2, 3], minsize=50)

label1 = tk.Label(text="1", bg="black", fg="white")
label2 = tk.Label(text="2", bg="black", fg="white")
label3 = tk.Label(text="3", bg="black", fg="white")
label4 = tk.Label(text="4", bg="black", fg="white")

label1.grid(row=0, column=0)
label2.grid(row=0, column=1, sticky="ew")
label3.grid(row=0, column=2, sticky="ns")
label4.grid(row=0, column=3, sticky="nsew")

window.mainloop()
```

.grid() | .pack()
:---: | :---:
sticky="ns"| fill=tk.Y
sticky="ew" | fill=tk.X
sticky="nsew" | fill=tk.BOTH

## Making Your Applications Interactive

### Using Events and Event Handlers

```python
# Assume that this list gets updated automatically
events_list = []

# Run the event loop
while True:
    # If events_list is empty, then no events have occurred and you
    # can skip to the next iteration of the loop
    if events_list == []:
        continue

    # If execution reaches this point, then there is at least one
    # event object in events_list
    event = events_list[0]
```

```python
events_list = []

# Create an event handler
def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

while True:
    if events_list == []:
        continue
    event = events_list[0]

    # If event is a keypress event object
    if event.type == "keypress":
        # Call the keypress event handler
        handle_keypress(event)
```

```python
import tkinter as tk

# Create a window object
window = tk.Tk()

# Create an event handler
def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

# Run the event loop
window.mainloop()
```

### Using .bind()

**Example 1.**
```python
import tkinter as tk

window = tk.Tk()

def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

# Bind keypress event to handle_keypress()
window.bind("<Key>", handle_keypress)

window.mainloop()
```

**Example 2.**
```python
import tkinter as tk

window = tk.Tk()

def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

# Bind keypress event to handle_keypress()
window.bind("<Key>", handle_keypress)

def handle_click(event):
    print("The button was clicked!")

button = tk.Button(text="Click me!")
button.pack()
button.bind("<Button-1>", handle_click)

button2 = tk.Button(text="Click me! 2")
button2.pack()
button2.bind("<Button-1>", handle_click)

window.mainloop()
```

**Note.**

Syntax:
```python
window.bind("<event_name>", a_command)
```
where `event_name` can be any of Tkinter's events.

Tkinter's events | Using
:---: | :---: 
`<Key>` | Ban phim
`<Button-1>` | event occurs whenever the left mouse button
`<Button-2>` | event occurs whenever the middle mouse button
`<Button-3>` | event occurs whenever the right mouse button
`<Enter>` | Enter

Tham khao them tai: https://effbot.org/tkinterbook/tkinter-events-and-bindings.htm

### Using command

**Example 1.**
```python
import tkinter as tk

def increase():
    value = int(lbl_value["text"])
    lbl_value["text"] = f"{value + 1}"


def decrease():
    value = int(lbl_value["text"])
    lbl_value["text"] = f"{value - 1}"

window = tk.Tk()

window.rowconfigure(0, minsize=50, weight=1)
window.columnconfigure([0, 1, 2], minsize=50, weight=1)

btn_decrease = tk.Button(master=window, text="-", command=decrease)
btn_decrease.grid(row=0, column=0, sticky="nsew")

lbl_value = tk.Label(master=window, text="0")
lbl_value.grid(row=0, column=1)

btn_increase = tk.Button(master=window, text="+", command=increase)
btn_increase.grid(row=0, column=2, sticky="nsew")

window.mainloop()
```

**Example 2.**
```python
import random
import tkinter as tk

def roll():
    lbl_result["text"] = str(random.randint(1, 6))

window = tk.Tk()
window.columnconfigure(0, minsize=150)
window.rowconfigure([0, 1], minsize=50)

btn_roll = tk.Button(text="Roll", command=roll)
lbl_result = tk.Label()

btn_roll.grid(row=0, column=0, sticky="nsew")
lbl_result.grid(row=1, column=0)

window.mainloop()
```

## Examples App

### Building a Temperature Converter

```python
import tkinter as tk

def fahrenheit_to_celsius():
    """Convert the value for Fahrenheit to Celsius and insert the
    result into lbl_result.
    """
    fahrenheit = ent_temperature.get()
    celsius = (5/9) * (float(fahrenheit) - 32)
    lbl_result["text"] = f"{round(celsius, 2)} \N{DEGREE CELSIUS}"

# Set-up the window
window = tk.Tk()
window.title("Temperature Converter")
window.resizable(width=False, height=False)

# Create the Fahrenheit entry frame with an Entry
# widget and label in it
frm_entry = tk.Frame(master=window)
ent_temperature = tk.Entry(master=frm_entry, width=10)
lbl_temp = tk.Label(master=frm_entry, text="\N{DEGREE FAHRENHEIT}")

# Layout the temperature Entry and Label in frm_entry
# using the .grid() geometry manager
ent_temperature.grid(row=0, column=0, sticky="e")
lbl_temp.grid(row=0, column=1, sticky="w")

# Create the conversion Button and result display Label
btn_convert = tk.Button(
    master=window,
    text="\N{RIGHTWARDS BLACK ARROW}",
    command=fahrenheit_to_celsius
)
lbl_result = tk.Label(master=window, text="\N{DEGREE CELSIUS}")

# Set-up the layout using the .grid() geometry manager
frm_entry.grid(row=0, column=0, padx=10)
btn_convert.grid(row=0, column=1, pady=10)
lbl_result.grid(row=0, column=2, padx=10)

# Run the application
window.mainloop()
```

### Building a Text Editor

```python
import tkinter as tk
from tkinter.filedialog import askopenfilename, asksaveasfilename

def open_file():
    """Open a file for editing."""
    filepath = askopenfilename(
        filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")]
    )
    if not filepath:
        return
    txt_edit.delete(1.0, tk.END)
    with open(filepath, "r") as input_file:
        text = input_file.read()
        txt_edit.insert(tk.END, text)
    window.title(f"Simple Text Editor - {filepath}")

def save_file():
    """Save the current file as a new file."""
    filepath = asksaveasfilename(
        defaultextension="txt",
        filetypes=[("Text Files", "*.txt"), ("All Files", "*.*")],
    )
    if not filepath:
        return
    with open(filepath, "w") as output_file:
        text = txt_edit.get(1.0, tk.END)
        output_file.write(text)
    window.title(f"Simple Text Editor - {filepath}")

window = tk.Tk()
window.title("Simple Text Editor")
window.rowconfigure(0, minsize=800, weight=1)
window.columnconfigure(1, minsize=800, weight=1)

txt_edit = tk.Text(window)
fr_buttons = tk.Frame(window, relief=tk.RAISED, bd=2)
btn_open = tk.Button(fr_buttons, text="Open", command=open_file)
btn_save = tk.Button(fr_buttons, text="Save As...", command=save_file)

btn_open.grid(row=0, column=0, sticky="ew", padx=5, pady=5)
btn_save.grid(row=1, column=0, sticky="ew", padx=5)

fr_buttons.grid(row=0, column=0, sticky="ns")
txt_edit.grid(row=0, column=1, sticky="nsew")

window.mainloop()
```

## Sources
- [Python](https://docs.python.org/3/library/tkinter.html)
- [Real Python](https://realpython.com/python-gui-tkinter/)
- [TkinterBook](https://effbot.org/tkinterbook/)
- [Python Course](https://www.python-course.eu/python_tkinter.php)
- [GeeksforGeeks](https://www.geeksforgeeks.org/python-gui-tkinter/)
- [DataCamp](https://www.datacamp.com/community/tutorials/gui-tkinter-python)
- [Stack Overflow](https://stackoverflow.com/)
