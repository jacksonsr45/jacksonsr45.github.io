---
layout: post
author: "jacksonsr45"
title:  "Python"
date:   2020-2-14
---

<p class="intro"><span class="dropcap">A</span> simple way to implement a calculator, using Python!</p>

To start with, we should set up a structure to organize our code, although a simple calculator can be a lot.

# **calculator**
- app #folder
    - src #folder
        - app_calculator.py #file
    - main.py #file
- calculator.py #file   

In calculator.py the code will look like this

```py

from app.main import Main

if __name__ == "__main__":
    Main()
```

Now in our main.py file

```py
import tkinter
from app.src.app_calculator import Calculator

class Main:
    def __init__(self):
        root = tkinter.Tk()
        Calculator(root)
        root.mainloop()
``` 

Now in our app_calculator.py file 

```py

import tkinter 

class Calculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Calculator")
        x = (self.root.winfo_screenwidth() // 2) - (550 // 2)
        y = (self.root.winfo_screenheight() // 2) - (600 // 2)
        self.root.geometry("550x600+{}+{}".format( x, y))
```

Then we have our structure for the code, which in this case will be in app_calculator.py
We start root in main.py and assign it to Calculator, as soon as we call calculator we already start root.mainloop () of our app.
We give the screen a name with 
```py 
    self.root.title ("Calculator") 
``` 
in app_calculator.py

And with 
```py
    self.root.geometry() 
```
we determine the size of the canvas, which in this case we are beyond determining the size. Also determining that it opens in the middle of the monitor!
This way as soon as we execute calculator.py file, we will open the empty window that we will use to mount our app_calculator on it.
Next step is to assemble the components for our app, which in Python is very simple.
We will follow an order in the assembly that in this case from top to bottom, and apply ok. But it could be done in many other ways.

now in app_calculator.py file we declare this function!
```py
    def frame_calc(self, root, side, bw, bd, bg):
        frame = tkinter.Frame(root, borderwidth= bw, bd= bw, bg= bg)
        frame.pack(side= side, expand=tkinter.YES, fill= tkinter.BOTH)
        return frame
```
And now we call the function we created to start our frame.

```py
class Calculator:
    def __init__(self):
        self.root = root
        self.root.title("Calculator")
        x = (self.root.winfo_screenwidth() // 2) - (550 // 2)
        y = (self.root.winfo_screenheight() // 2) - (600 // 2)
        self.root.geometry("550x600+{}+{}".format( x, y))

        self.frame = frame_calc(self.root, tkinter.TOP, 1, 4, "black")


    def frame_calc(self, root, side, bw, bd, bg):
        frame = tkinter.Frame(root, borderwidth= bw, bd= bw, bg= bg)
        frame.pack(side= side, expand=tkinter.YES, fill= tkinter.BOTH)
        return frame
```
