---
layout: post
author: "jacksonsr45"
title:  "Python"
date:   2020-2-14
---

<p class="intro"><span class="dropcap">P</span>ython, how to declare variables and functions in a simplified way!</p>

Python is a computer language that makes it easier for younger users, and even the most experienced users. For having simple syntaxes without the verbiage that JAVA has.
 
When declaring a variable in python, even though it has a type, we don't need to worry about declaring it at first because it already recognizes it automatically.
  
```py 
  num = 1
  print(num)
```

When executing the code above we have a variable **num** an integer value.

```py 
  num = "string"
  print(num)
```

However, if we assign to **num** the value of a string there will be no error, we will only delete the value already assigned, and the variable is now of a string type.

We can directly assign a value to the variable.

```py 
  num = 1 + 1
  print(num)
```

or


```py 
  num = 1
  num += 1
  print(num)
```

Create a function and assign the variable.


```py 
  def fun( num1, num2):
    return num1 + num2

  num = fun(2,2)
  print(num)
```

Summing up python brings us facilities to have cleaner codes and clutter, but very effective.