---
layout: post
author: "jacksonsr45"
title:  "Python Calculator"
date:   2020-2-15
---

<p class="intro"><span class="dropcap">A</span> simple way to implement a calculator, using Python!</p>

[Repository link](https://github.com/jacksonsr45/python_calculator)

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
import tkinter

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

Creating the frame in a function now leaves us with a line of code every time we create a new frame in this project, which in this case will be just this one.
Now let's create the display for our calculator.

```py
    def display(self, frame, font):
        display = tkinter.Entry(frame)
        display.configure(textvariable=self.value_display)
        display.configure(font=font)
        display.configure(justify='right')
        display.pack(side=tkinter.TOP, expand= tkinter.YES, fill= tkinter.BOTH)
        return display
```
It will also be a function similar to the one we placed above. And the code for our Calculator class will now have to look like this.


```py
import tkinter

class Calculator:
    def __init__(self):
        self.root = root
        self.root.title("Calculator")
        x = (self.root.winfo_screenwidth() // 2) - (550 // 2)
        y = (self.root.winfo_screenheight() // 2) - (600 // 2)
        self.root.geometry("550x600+{}+{}".format( x, y))
        
        self.value_display = tkinter.StringVar()
        
        self.frame = frame_calc(self.root, tkinter.TOP, 1, 4, "black")

        self.display(self.frame, ("Ubunto", 17))


    def frame_calc(self, root, side, bw, bd, bg):
        frame = tkinter.Frame(root, borderwidth= bw, bd= bw, bg= bg)
        frame.pack(side= side, expand=tkinter.YES, fill= tkinter.BOTH)
        return frame


    def display(self, frame, font):
        display = tkinter.Entry(frame)
        display.configure(textvariable=self.value_display)
        display.configure(font=font)
        display.configure(justify='right')
        display.pack(side=tkinter.TOP, expand= tkinter.YES, fill= tkinter.BOTH)
        return display
```
Note that we now have a self.value_display variable starting with tkinter.StringVar () and set to textvariable on our display.
In it will be the values of our display.
With that we run the calculator.py file we will have a screen with a display already!
Now we need to create a function with the calculator buttons and we will divide it into 3, two just to create the buttons on the screen and another one by extending the Buttons object of tkinter.
Let's start with the button.

```py
    def button(self, frame, side, text, command=None):
        button = tkinter.Button(frame)
        button.configure(text= text)
        button.configure(font= ("Ubunto", 14))
        button.configure(command=command)
        button.pack( side=side, expand=tkinter.YES, fill=tkinter.BOTH)
        return button 
```
Now create the buttons to clear the display on the screen!
```py
    def clear(self, root):
        for clear in (["CE"],["C"]):
            erase = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
            for row in clear:
                self.button( erase, tkinter.LEFT, row,
                            lambda storeObj=self.value_display, q= row: 
                                        storeObj.set(''))
```
Now we will create the buttons with the values for the calculator!
```py
    def button_calculator(self, root):
        for num_btn in ("()%","/789", "*456", "-123", "+.0"):
            btn_calc = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
            for row in num_btn:
                self.button( btn_calc, tkinter.LEFT, row,
                            lambda display= self.value_display, q=row: 
                                    display.set(display.get() + q))
```
Now our code should look like this!
```py
import tkinter

class Calculator:
    def __init__(self):
        self.root = root
        self.root.title("Calculator")
        x = (self.root.winfo_screenwidth() // 2) - (550 // 2)
        y = (self.root.winfo_screenheight() // 2) - (600 // 2)
        self.root.geometry("550x600+{}+{}".format( x, y))
        
        self.value_display = tkinter.StringVar()
        
        self.frame = frame_calc(self.root, tkinter.TOP, 1, 4, "black")

        self.display(self.frame, ("Ubunto", 17))

        self.clear(self.root)

        self.button_calculator(self.root)


    def frame_calc(self, root, side, bw, bd, bg):
        frame = tkinter.Frame(root, borderwidth= bw, bd= bw, bg= bg)
        frame.pack(side= side, expand=tkinter.YES, fill= tkinter.BOTH)
        return frame


    def display(self, frame, font):
        display = tkinter.Entry(frame)
        display.configure(textvariable=self.value_display)
        display.configure(font=font)
        display.configure(justify='right')
        display.pack(side=tkinter.TOP, expand= tkinter.YES, fill= tkinter.BOTH)
        return display
    
    
    def button(self, frame, side, text, command=None):
        button = tkinter.Button(frame)
        button.configure(text= text)
        button.configure(font= ("Ubunto", 14))
        button.configure(command=command)
        button.pack( side=side, expand=tkinter.YES, fill=tkinter.BOTH)
        return button 

    
    def clear(self, root):
        for clear in (["CE"],["C"]):
            erase = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
            for row in clear:
                self.button( erase, tkinter.LEFT, row,
                            lambda storeObj=self.value_display, q= row: 
                                        storeObj.set(''))


    def button_calculator(self, root):
        for num_btn in ("()%","/789", "*456", "-123", "+.0"):
            btn_calc = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
            for row in num_btn:
                self.button( btn_calc, tkinter.LEFT, row,
                            lambda display= self.value_display, q=row: 
                                    display.set(display.get() + q))
```

Now when executing the calculator.py file we already have our calculator with form, or almost and without functionality yet.
We must now put the = button and the logic for our app, we go to our button!

```py
    def equals(self, root):
        equals_button = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
        for value in "=":
            if value == '=':
                btn_equals = self.button( equals_button, tkinter.LEFT, value)
                btn_equals.bind('<ButtonRelease-1>',
                        lambda e, s=self, display=self.value_display: s.calc(display), '+')
            else:
                btn_equals = self.button( equals_button, tkinter.LEFT, value,
                        lambda display=self.value_display, s=' %s '%value: 
                                display.set(display.get()+s))
```
We have already left our calc () function, because we are already pressing buttons without it.
```py
    def calc(self, display):
        try: 
            display.set(eval(display.get()))
        except:
            display.set("ERROR")
```
With that we have our code ready for operation that will look like this.
```py
import tkinter

class Calculator:
    def __init__(self,root):
        self.root = root
        self.root.title("Calculator")
        x = (self.root.winfo_screenwidth() // 2) - (550 // 2)
        y = (self.root.winfo_screenheight() // 2) - (600 // 2)
        self.root.geometry("550x600+{}+{}".format( x, y))

        self.value_display = tkinter.StringVar()

        self.frame = self.frame_calc(self.root, tkinter.TOP, 1, 4, "black")

        self.display(self.frame, ("Ubunto", 17))

        self.clear(self.root)

        self.button_calculator(self.root)

        self.equals(self.root)


    def frame_calc(self, root, side, bw, bd, bg):
        frame = tkinter.Frame(root, borderwidth= bw, bd= bw, bg= bg)
        frame.pack(side= side, expand=tkinter.YES, fill= tkinter.BOTH)
        return frame


    def display(self, frame, font):
        display = tkinter.Entry(frame)
        display.configure(textvariable=self.value_display)
        display.configure(font=font)
        display.configure(justify='right')
        display.pack(side=tkinter.TOP, expand= tkinter.YES, fill= tkinter.BOTH)
        return display


    def button(self, frame, side, text, command=None):
        button = tkinter.Button(frame)
        button.configure(text= text)
        button.configure(font= ("Ubunto", 14))
        button.configure(command=command)
        button.pack( side=side, expand=tkinter.YES, fill=tkinter.BOTH)
        return button 


    def clear(self, root):
        for clear in (["CE"],["C"]):
            erase = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
            for row in clear:
                self.button( erase, tkinter.LEFT, row,
                            lambda storeObj=self.value_display, q= row: 
                                        storeObj.set(''))

    def button_calculator(self, root):
        for num_btn in ("()%","/789", "*456", "-123", "+.0"):
            btn_calc = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
            for row in num_btn:
                self.button( btn_calc, tkinter.LEFT, row,
                            lambda display= self.value_display, q=row: 
                                    display.set(display.get() + q))



    def equals(self, root):
        equals_button = self.frame_calc( root, tkinter.TOP, 1, 4, "white")
        for value in "=":
            if value == '=':
                btn_equals = self.button( equals_button, tkinter.LEFT, value)
                btn_equals.bind('<ButtonRelease-1>',
                        lambda e, s=self, display=self.value_display: s.calc(display), '+')
            else:
                btn_equals = self.button( equals_button, tkinter.LEFT, value,
                        lambda display=self.value_display, s=' %s '%value: 
                                display.set(display.get()+s))

    def calc(self, display):
        try: 
            display.set(eval(display.get()))
        except:
            display.set("ERROR")
```

[Repository link](https://github.com/jacksonsr45/python_calculator)

With that we reached the end of our calculator, in a very simple way. Thank you and see you later

jacksonsr45