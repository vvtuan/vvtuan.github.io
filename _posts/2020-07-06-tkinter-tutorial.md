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

###  Getting user input with `Entry` widgets

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

## Controlling Layout With Geometry Managers

## Making Your Applications Interactive

## Examples App

## Sources
- [Python](https://docs.python.org/3/library/tkinter.html)
- [Real Python](https://realpython.com/python-gui-tkinter/)
- [TkinterBook](https://effbot.org/tkinterbook/)
- [Python Course](https://www.python-course.eu/python_tkinter.php)
- [GeeksforGeeks](https://www.geeksforgeeks.org/python-gui-tkinter/)
- [DataCamp](https://www.datacamp.com/community/tutorials/gui-tkinter-python)
- [Stack Overflow](https://stackoverflow.com/)
