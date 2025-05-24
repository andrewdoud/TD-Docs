

Cell Class - Derivative




# Cell Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Cell Class describes the contents of a single cell from a [DAT](DAT.html "DAT") operator table.
The [DAT Class](DAT_Class.html "DAT Class") offers many ways of accessing its individual cells.
[DAT](DAT.html "DAT") cells are always internally stored as strings, but may be accessed as numeric values.
**IMPORTANT**: `op('table1')[1,2]` is this python cell object which usually gets converted for you to the string in the cell. More safely use `op('table1')[1,2].val` which always gives you the string.
  

## Members
`valid` → `bool` **(Read Only)**:
> True if the referenced cell currently exists, False if it has been deleted.
`row` → `int` **(Read Only)**:
> The numeric row of the cell.
`col` → `int` **(Read Only)**:
> The numeric column of the cell.
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`val` → `str` :
> Get or set the cell contents, which are always stored as a string value.
## Methods
`run(*args, endFrame=False, fromOP=None, asParameter=False, group=None, delayFrames=0, delayMilliSeconds=0, delayRef=None)`→ `td.Run`:
> [Run](Run_Class.html "Run Class") the contents of the cell as a script, returning a Run object which can be used to optionally modify its execution.
> 
> * endFrame - (Keyword, Optional) If set to True, the execution will be delayed until the end of the current frame.
> * fromOP - (Keyword, Optional) Specifies an optional [operator](OP_Class.html "OP Class") from which the execution will be run relative to.
> * asParameter - (Keyword, Optional) When fromOP used, run relative to a parameter of fromOP.
> * group - (Keyword, Optional) Can be used to specify a group label string. This label can then be used with the [td.runs](Runs_Class.html "Runs Class") object to modify its execution.
> * delayFrames - (Keyword, Optional) Can be used to delay the execution a specific amount of frames.
> * delayMilliSeconds - (Keyword, Optional) Can be used to delay the execution a specific amount of milliseconds. This value is rounded to the nearest frame.
> * delayRef - (Keyword, Optional) Specifies an optional [operator](OP_Class.html "OP Class") from which the delay time is derived. If none is provided, will use the cell owner.
> * arg - (Optional) Arguments that will be made available to the script in a local tuple named args.
`offset(r, c)`→ `Cell | None`:
> The cell offset to this cell by the specified amount, or None.
> 
> * r - The number of rows from the cell. Positive values count down, while negative values count up.
> * c - The number of columns from the cell. Positive values count right, while negative values count left.
> 
> ```
> c = op('table1')['March', 'Sales']
> d = c.offset(-1, 2)  # one row up, two columns right of cell C
> 
> ```
### Casting to a Value[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Casting to a Value")]
The Cell Class implements all necessary methods to be treated as a number or a string, which in this case gets or sets its value. Therefore, an explicit call to get or set val is unnecessary when used in a parameter, or in an expression.
For example, the following are equivalent in a numeric parameter:
```
(float)n[1,2]
n[1,2].val
n[1,2]
```
Or equivalently, for a string parameter:
```
(str)n[1,2]
n[1,2].val
n[1,2]
```
Similarly, expressions on Cells will autocast themselves automatically:
```
n[1,2].val + 1 # string plus 1, error
n[1,2] + 1 # autocasted value plus 1
```
In the second case, the contents of the Cell are used to determine if numeric or string operations should be used.
For example, if cell n[1,2] contains "3" then:
```
n[1,2].val + n[1,2].val # will return "33" since .val is a string.
```
However,
```
n[1,2] + n[1,2] # will return 6 since the contents "3" are numeric.
```
If n[1,2] contained a non-numeric value such as "a" then
```
n[1,2] + n[1,2] # will return "aa"
```
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=Cell_Class&oldid=31561>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")