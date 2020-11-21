# functional-python
A python decorator that enforces functional programming within a function.

The decorator requires the function to use no global variables unless the variables are all caps or builtin to python.

Example:

from math import pi
from functional import functional

STATIC_GLOBAL_VAR = 100
nonStaticGlobal = -100

@functional
def goodFunction(): # will not raise an exception
    #global STATIC_GLOBAL_VAR
    #STATIC_GLOBAL_VAR -= 1
    #print(STATIC_GLOBAL_VAR)
    #print(print)

goodFunction()

@functional
def badFunction(): # will raise an exception
    #global nonStaticGlobal
    #nonStaticGlobal -= 1
    #print(nonStaticGlobal)

badFunction()
