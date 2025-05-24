

# Prims_Class

Prims Class - Derivative




# Prims Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Prims class describes the set of [prim objects](Prim_Class.html "Prim Class") (primitives) owned by one [SOP](SOP_Class.html "SOP Class").
  

## Members
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
## Methods
No operator specific methods.
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`len(Prims)`→ `int`:
> Returns the total number of prims.
> 
> ```
> a = len(op('box1').prims)
> 
> ```
`[index]`→ `td.Prim`:
> Get a specific prim given an integer index.
> 
> ```
> n = op('box1').prims[0]
> 
> ```
`Iterator`→ `td.Prim`:
> Iterate over each prim.
> 
> ```
> for m in op('box1').prims:
> 	# do something with m, which is a Prim
> 
> ```
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=Prims_Class&oldid=12170>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")