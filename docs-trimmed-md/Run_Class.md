

Run Class - Derivative




# Run Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Run class describes a single instance of a delayed script execution. See [Run Command Examples](Run_Command_Examples.html "Run Command Examples") for more info.
They can be accessed from the [runs](Runs_Class.html "Runs Class") object. Scripts can be executed with delays with the following methods:
```
DAT.run()
Cell.run()
td.run()
```
  

## Members
`active` → `bool` :
> Get or set whether or not this script will execute once its target frame is reached.
`group` → `str` :
> Get or set the group label associated with this script.
`isCell` → `bool` **(Read Only)**:
> Returns true when the source is a [cell](Cell_Class.html "Cell Class"), from a Cell.run() call.
`isDAT` → `bool` **(Read Only)**:
> Returns true when the source is a [DAT](DAT_Class.html "DAT Class"), from a DAT.run() call.
`isString` → `bool` **(Read Only)**:
> Returns true when the source is a string, from a td module run() call
`path` → `OP` **(Read Only)**:
> The [operator](OP_Class.html "OP Class") location from which this script will execute.
`remainingFrames` → `int` :
> Get or set the remaining number of frames before the execution will occur.
`remainingMilliseconds` → `int` :
> Get or set the remaining number of milliseconds before the execution will occur.
`source` → `DAT | Cell | str` **(Read Only)**:
> The source of the run. It will be either a [DAT](DAT_Class.html "DAT Class"), [cell](Cell_Class.html "Cell Class"), or string.
## Methods
`kill()`→ `None`:
> Kill this run before it executes, and remove it from the global runs list, located in the [td Module](Td_Module.html "Td Module").
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=Run_Class&oldid=31454>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")