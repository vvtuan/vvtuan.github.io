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

## Tk Concepts

### Widgets

### Geometry Management

### Event Handling

## Widgets

## Geometry Manager

## Menus

## Windows and Dialogs

## Organizing Complex Interfaces

## Fonts, Colors, Images

## Canvas

## Text

## Tree

## Styles and Themes

## IDLE Modernization

## Sources

- [Stack Overflow](https://stackoverflow.com/)
- [Real Python](https://realpython.com/python-gui-tkinter/)
- [TkDocs](https://tkdocs.com/tutorial/index.html)
